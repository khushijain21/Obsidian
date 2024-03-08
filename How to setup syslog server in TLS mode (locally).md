
1. Update the packages list and install the latest version of rsyslog.

`apt update`

`apt install rsyslog`

2. Create certificates

```
openssl genrsa -out ca.key 2048

openssl req -new -x509 -days 365 -key ca.key -subj "/C=CN/ST=GD/L=SZ/O=Acme, Inc./CN=Acme Root CA" -out ca-crt.pem

openssl req -newkey rsa:2048 -nodes -keyout syslog-key.pem -subj "/C=CN/ST=GD/L=SZ/O=Acme, Inc./CN=*.localhost.com" -out syslog.csr

openssl x509 -req -extfile <(printf "subjectAltName=DNS:localhost,DNS:www.localhost.com") -days 365 -in syslog.csr -CA ca-cert.pem -CAkey ca.key -CAcreateserial -out syslog-cert.pem
```

3. Change permissions of the file
```
chmod 777 *.pem
```

We only need ca-crt.pem, syslog-key.pem syslog-cert.pem files


4. Open the `rsyslog.conf` file and add the following lines.

```none
sudo vi /etc/rsyslog.conf
```

Please configure the path of certificates correctly below

```
# /etc/rsyslog.conf configuration file for rsyslog
#
# For more information install rsyslog-doc and see
# /usr/share/doc/rsyslog-doc/html/configuration/index.html
#
# Default logging rules can be found in /etc/rsyslog.d/50-default.conf


#################
#### MODULES ####
#################
global(   DefaultNetstreamDriver="gtls"   DefaultNetstreamDriverCAFile="/home/User/ca-crt.pem"   DefaultNetstreamDriverCertFile="/home/User/syslog-cert.pem"
DefaultNetstreamDriverKeyFile="/home/User/syslog-key.pem" )

module(load="imuxsock") # provides support for local system logging
#module(load="immark")  # provides --MARK-- message capability

# provides UDP syslog reception
module(load="imudp")
input(type="imudp" port="514")

# provides TCP syslog reception
module(load="imtcp" StreamDriver.Name="gtls" StreamDriver.Mode="1" StreamDriver.AuthMode="anon")
input(type="imtcp" port="514")

# provides kernel logging support and enable non-kernel klog messages
module(load="imklog" permitnonkernelfacility="on")

###########################
#### GLOBAL DIRECTIVES ####
###########################

#
# Use traditional timestamp format.
# To enable high precision timestamps, comment out the following line.
#
$ActionFileDefaultTemplate RSYSLOG_TraditionalFileFormat

# Filter duplicated messages
$RepeatedMsgReduction on

#
# Set the default permissions for all log files.
#
$FileOwner syslog
$FileGroup adm
$FileCreateMode 0640
$DirCreateMode 0755
$Umask 0022
$PrivDropToUser syslog
$PrivDropToGroup syslog

#
# Where to place spool and state files
#
$WorkDirectory /var/spool/rsyslog

#
# Include all config files in /etc/rsyslog.d/
#
$IncludeConfig /etc/rsyslog.d/*.conf

```

5. Install the below driver

```
sudo apt intall rsyslog-gnutls
```

6. Restart Syslog Server
```
sudo service rsyslog restart
```

7. You can check logs under by 

```
tail -f /var/log/syslog
```



