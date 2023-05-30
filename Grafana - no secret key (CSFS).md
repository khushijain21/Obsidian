
```
{{- include "cpro-grafana.istio.grafanaInitIstio" . }}

{{- if .Values.SetDatasource.enabled -}}

apiVersion: {{ template "cpro-grafana.grafanaApiVersion.job" . }}

kind: Job

metadata:

  labels:

    {{- include "cpro-grafana.app.labels-v3" . | nindent 4 }}

    {{- include "cpro-grafana.labelsOrAnnotations" (tuple .Values.grafana.labels .Values.global.labels) | indent 4}}

  name: {{ template "cpro-grafana.setDatasource" . }}

  annotations:

    {{- include "cpro-grafana.labelsOrAnnotations" (tuple .Values.grafana.annotations .Values.global.annotations) | indent 4}}

    "helm.sh/hook": post-install

    "helm.sh/hook-weight": "{{ add .Values.helmDeleteImage.hookWeight 8 }}"

    # "helm.sh/hook-delete-policy": hook-succeeded,before-hook-creation

spec:

  activeDeadlineSeconds: {{ default 300 .Values.SetDatasource.activeDeadlineSeconds }}

  backoffLimit: 10

  template:

    metadata:

      labels:

        {{- include "cpro-grafana.app.labels-v3" . | nindent 8 }}

        component: "{{ .Values.name }}"

{{- include "cpro-grafana.labelsOrAnnotations" (tuple .Values.grafana.labels .Values.custom.pod.labels .Values.global.labels) | indent 8}}

      annotations:

        sidecar.istio.io/inject: "{{ $.istio.enabled }}"

{{- include "cpro-grafana.labelsOrAnnotations" (tuple .Values.grafana.annotations .Values.custom.pod.annotations .Values.global.annotations) | indent 8}}

{{- if .Values.rbac.pspUseAppArmor }}

{{- include "cpro-grafana.labelsOrAnnotations" (tuple .Values.custom.pod.apparmorAnnotations) | indent 8}}

{{- end }}

    spec:

      automountServiceAccountToken: true

      serviceAccountName: {{ template "cpro-grafana.serviceAccountName" . }}

      securityContext:

      {{$securityContextvalue := dict "cSecCtx" .Values.securityContext "ctx" . }}

      {{- include "cpro-grafana.securitycontext" $securityContextvalue | nindent 8 }}

      {{- if .Values.seLinuxOptions.enabled }}

        seLinuxOptions:

          level: {{ .Values.seLinuxOptions.level }}

          role: {{ .Values.seLinuxOptions.role }}

          type: {{ .Values.seLinuxOptions.type }}

          user: {{ .Values.seLinuxOptions.user }}

      {{- end }}

{{ include "cpro-common-lib.imagePullSecrets" (dict "workloadName" .Values.grafana "root" .) | indent 6 }}      

      containers:

      - name: {{ template "cpro-grafana.setDatasourceContainer" . }}

{{- include "cpro-grafana.utility.image" . | nindent 8}}

{{- include "cpro-grafana.terminationMessage" . | nindent 8 }}

        env:

          {{- include "cpro-grafana.timeZoneName" . | nindent 10 }}

        resources:

{{ toYaml .Values.SetDatasource.resources | indent 10 }}

        securityContext:

        {{$securityContextvalue := dict "cSecCtx" .Values.SetDatasource.containerSecurityContext "ctx" . }}

        {{- include "cpro-grafana.containerSecurityContext" $securityContextvalue | nindent 10 }}

        # command: ["/bin/sh", "-c"]

        command: ["sleep", "infinity"]

	        args:
	
	          - -c
	
	          - |
	
	            /scripts/curl_entrypoint.sh
	
	            {{- if eq .Values.scheme "https" }}
	
	            until $(curl --output /dev/null --silent --head --fail --insecure https://{{ template "cpro-grafana.service.name" . }}:{{ .Values.service.port }}/api/health); do
	
	                printf '.'
	
	                sleep 1
	
	            done
	
	            {{ else if eq .Values.scheme "http" }}
	
	            until $(curl --output /dev/null --silent --head --fail http://{{ template "cpro-grafana.service.name" . }}:{{ .Values.service.port }}/api/health); do
	
	                printf '.'
	
	                sleep 1
	
	            done
	
	            {{- end }}
	
	  
	
	            {{- if $.istio.enabled }}
	
	            until [ $(curl --fail --silent --output /dev/stderr --write-out "%{http_code}" localhost:15020/healthz/ready) -eq 200 ]; do
	
	              echo "Waiting for proxy..."
	
	              sleep 1
	
	            done
	
	  
	
	            echo "istio-proxy available"
	
	            {{- end }}
	
	  
	
	            key=`/usr/bin/secretdata --admin --secretname={{ template "cpro-grafana.fullname" . }} --sensitivedata={{ .Values.sensitiveDataSecretName }} --namespace={{ .Release.Namespace }}` ; goretval=$?
	
	            if [ $goretval !=0 ]; then
	
	              echo "Failed to copy file grafana sensitive data to key!"
	
	              exit 1
	
	            fi
	
	  
	
	            proxy_user=$(echo -ne "$key" | cut -d':' -f1)
	
	  
	
	            {{- range $key_ini, $value := index .Values "grafana_ini" }}
	
	              {{- range $elem, $elemVal := $value }}
	
	                {{- if and (eq $key_ini "auth.basic") (eq $elem "enabled") ( $elemVal ) }}
	
	  
	
	                auth=$(echo -ne "$key" | base64 --wrap 0)
	
	                curl_opts=( --header 'Authorization: Basic '${auth} --insecure --connect-timeout 5 --max-time 30 --retry 3 --silent --globoff)
	
	  
	
	                {{- else if and (eq $key_ini "auth.proxy") (eq $elem "enabled") ( $elemVal ) }}
	
	                  {{- range $elem_header, $elemVal_header := $value }}
	
	                    {{- if (eq $elem_header "header_name") }}
	
	  
	
	                    curl_opts=( --header '{{ $elemVal_header }}: '${proxy_user} --insecure --connect-timeout 5 --max-time 30 --retry 3 --silent --globoff)
	
	                    {{ end }}
	
	  
	
	                {{- end }}
	
	                {{- end }}
	
	              {{- end }}
	
	            {{- end }}
	
	  
	
	            grafana_hostname={{ template "cpro-grafana.service.name" . }}
	
	            grafana_port={{ .Values.service.port }}
	
	            protocol={{ .Values.scheme }}
	
	            prom_method="POST"
	
	            prom_api="/api/datasources"
	
	  
	
	            curl -v -H "Content-Type:application/json;charset=UTF-8" \
	
	            -H "Accept: application/json" "${curl_opts[@]}" \
	
	            -X ${prom_method} ${protocol}://${grafana_hostname}:${grafana_port}${prom_api} \
	
	            --data-binary \
	
	            {{- with .Values.SetDatasource.datasource }}
	
	            '{"name":"{{ .name }}","type":"{{ .type }}","url":"{{ .url }}","database":"{{ .database }}","jsonData":{{ .jsonData | toJson }},"secureJsonData":{{ .secureJsonData | toJson }},"access":"{{ .access }}","isDefault":{{ .isDefault }},"user":"{{ .user }}","basicAuth":{{ .basicAuth }},"basicAuthUser":"{{ .basicAuthUser }}","editable":{{ .editable }}}'
	
	            {{- end }}
	
	  
	
	            {{- if $.istio.enabled }}
	
	            curl -X POST http://localhost:15020/quitquitquit
	
	            {{- end }}

  

      restartPolicy: {{ .Values.SetDatasource.restartPolicy }}

{{- with .Values.nodeSelector }}

      nodeSelector:

{{ toYaml . | indent 8 }}

{{- end }}

{{- with .Values.affinity }}

      affinity:

{{ toYaml . | indent 8 }}

    {{- end }}

{{- with .Values.tolerations }}

      tolerations:

{{ toYaml . | indent 8 }}

    {{- end }}

{{- end -}}
```



![[Pasted image 20230522171627.png]]