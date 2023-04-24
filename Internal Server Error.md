

1.  Delete Alert File List
```shell
curl -v -H "Content-Type: application/json" -X DELETE "http://khu-cpro-restserver.khushi.svc.cluster.local:8888/cpro/v2/alertfiles/%2Fetc%2Fconfig%2Frules?namespace=khushi&configmapName=doesNotExist"
```

	ouptut

```shell
	< HTTP/1.1 500 Server Error
	< Connection: close
	< Server: Jetty(9.4.49.v20220914)
```

	Remark:
	When ConfigMapName does not exist - the error can be redirected to 400 (bad request) instead and the message can indicate that the given resource name does not exist. Similarly for when namespace does not exist



2. Add Alert File
```shell
 curl -v -X POST "http://khu-cpro-restserver.khushi.svc.cluster.local:8888/cpro/v2/alertfiles?namespace=khushi&configmapName=doesNotexist&fileName=/etc/config/testfiles" -H "Content-Type: application/json"
```

	output
	
``` shell
< HTTP/1.1 500 Server Error

< Cache-Control: must-revalidate,no-cache,no-store

< Content-Type: text/html;charset=iso-8859-1

< Content-Length: 5043

< Connection: close

< Server: Jetty(9.4.49.v20220914)

## HTTP ERROR 500 java.lang.NoClassDefFoundError: Could not initialize class com.nokia.cpro.restapi.common.AlarmUtil

URI:

/cpro/v2/alertfiles

STATUS:

500

MESSAGE:

java.lang.NoClassDefFoundError: Could not initialize class com.nokia.cpro.restapi.common.AlarmUtil

SERVLET:

org.jboss.resteasy.plugins.server.servlet.HttpServletDispatcher-18a136ac

CAUSED BY:

java.lang.NoClassDefFoundError: Could not initialize class com.nokia.cpro.restapi.common.AlarmUtil

### Caused by:

java.lang.NoClassDefFoundError: Could not initialize class com.nokia.cpro.restapi.common.AlarmUtil                     

at com.nokia.cpro.restapi.configmap.impl.api.AlarmInterceptor.postProcess(AlarmInterceptor.java:27)

at org.jboss.resteasy.core.interception.ContainerResponseFilterRegistry$ContainerResponseFilterFacade.filter(ContainerResponseFilterReg

istry.java:47)

at org.jboss.resteasy.core.interception.ContainerResponseContextImpl.filter(ContainerResponseContextImpl.java:357)

at org.jboss.resteasy.core.ServerResponseWriter.executeFilters(ServerResponseWriter.java:219)

at org.jboss.resteasy.core.ServerResponseWriter.writeNomapResponse(ServerResponseWriter.java:95)

at org.jboss.resteasy.core.ServerResponseWriter.writeNomapResponse(ServerResponseWriter.java:69)

at org.jboss.resteasy.core.SynchronousDispatcher.writeResponse(SynchronousDispatcher.java:530)

at org.jboss.resteasy.core.SynchronousDispatcher.invoke(SynchronousDispatcher.java:461)

at org.jboss.resteasy.core.SynchronousDispatcher.lambda$invoke$4(SynchronousDispatcher.java:229)

at org.jboss.resteasy.core.SynchronousDispatcher.lambda$preprocess$0(SynchronousDispatcher.java:135)

at org.jboss.resteasy.core.interception.PreMatchContainerRequestContext.filter(PreMatchContainerRequestContext.java:358)

at org.jboss.resteasy.core.SynchronousDispatcher.preprocess(SynchronousDispatcher.java:138)

at org.jboss.resteasy.core.SynchronousDispatcher.invoke(SynchronousDispatcher.java:215)

at org.jboss.resteasy.plugins.server.servlet.ServletContainerDispatcher.service(ServletContainerDispatcher.java:245)

at org.jboss.resteasy.plugins.server.servlet.HttpServletDispatcher.service(HttpServletDispatcher.java:61)

at org.jboss.resteasy.plugins.server.servlet.HttpServletDispatcher.service(HttpServletDispatcher.java:56)

at javax.servlet.http.HttpServlet.service(HttpServlet.java:790)

at org.eclipse.jetty.servlet.ServletHolder.handle(ServletHolder.java:799)

at org.eclipse.jetty.servlet.ServletHandler.doHandle(ServletHandler.java:554)

at org.eclipse.jetty.server.handler.ScopedHandler.nextHandle(ScopedHandler.java:233)

at org.eclipse.jetty.server.handler.ContextHandler.doHandle(ContextHandler.java:1440)

at org.eclipse.jetty.server.handler.ScopedHandler.nextScope(ScopedHandler.java:188)

at org.eclipse.jetty.servlet.ServletHandler.doScope(ServletHandler.java:505)

at org.eclipse.jetty.server.handler.ScopedHandler.nextScope(ScopedHandler.java:186)

at org.eclipse.jetty.server.handler.ContextHandler.doScope(ContextHandler.java:1355)

at org.eclipse.jetty.server.handler.ScopedHandler.handle(ScopedHandler.java:141)

at org.eclipse.jetty.server.handler.ContextHandlerCollection.handle(ContextHandlerCollection.java:234)

at org.eclipse.jetty.server.handler.HandlerWrapper.handle(HandlerWrapper.java:127)

at org.eclipse.jetty.server.Server.handle(Server.java:516)

at org.eclipse.jetty.server.HttpChannel.lambda$handle$1(HttpChannel.java:487)

at org.eclipse.jetty.server.HttpChannel.dispatch(HttpChannel.java:732)

at org.eclipse.jetty.server.HttpChannel.handle(HttpChannel.java:479)

at org.eclipse.jetty.server.HttpConnection.onFillable(HttpConnection.java:277)

at org.eclipse.jetty.io.AbstractConnection$ReadCallback.succeeded(AbstractConnection.java:311)

at org.eclipse.jetty.io.FillInterest.fillable(FillInterest.java:105)

at org.eclipse.jetty.io.ChannelEndPoint$1.run(ChannelEndPoint.java:104)

at org.eclipse.jetty.util.thread.strategy.EatWhatYouKill.runTask(EatWhatYouKill.java:338)

at org.eclipse.jetty.util.thread.strategy.EatWhatYouKill.doProduce(EatWhatYouKill.java:315)

at org.eclipse.jetty.util.thread.strategy.EatWhatYouKill.tryProduce(EatWhatYouKill.java:173)

at org.eclipse.jetty.util.thread.strategy.EatWhatYouKill.run(EatWhatYouKill.java:131)

at org.eclipse.jetty.util.thread.ReservedThreadExecutor$ReservedThread.run(ReservedThreadExecutor.java:409)

at org.eclipse.jetty.util.thread.QueuedThreadPool.runJob(QueuedThreadPool.java:883)

at org.eclipse.jetty.util.thread.QueuedThreadPool$Runner.run(QueuedThreadPool.java:1034)

at java.base/java.lang.Thread.run(Thread.java:829)

[Powered by Jetty:// 9.4.49.v20220914](https://eclipse.org/jetty)
```

	Remark:
	When ConfigMapName does not exist - the error can be redirected to 400 (bad request) instead and the message can indicate that the given resource name does not exist. Similarly for when namespace/Filename does not exist

