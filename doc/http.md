To configure jitsi-videobridge to serve meet:

1. Add prosody certificates to java keystore
2. Configure authbind to allow jvb to use port 443
3. And configure jvb itself in
/usr/share/jitsi-videobridge/.sip-communicator/sip-communicator.properties
```
org.jitsi.videobridge.rest.jetty.host=::
org.jitsi.videobridge.rest.jetty.port=443
org.jitsi.videobridge.rest.jetty.ProxyServlet.hostHeader=example.meet.jit.si
org.jitsi.videobridge.rest.jetty.ProxyServlet.pathSpec=/http-bind
org.jitsi.videobridge.rest.jetty.ProxyServlet.proxyTo=http://localhost:5280/http-bind
org.jitsi.videobridge.rest.jetty.ResourceHandler.resourceBase=/usr/share/jitsi-meet
org.jitsi.videobridge.rest.jetty.ResourceHandler.alias./config.js=/etc/jitsi/meet/example.meet.jit.si-config.js
org.jitsi.videobridge.rest.jetty.RewriteHandler.regex=^/([a-zA-Z0-9]+)$
org.jitsi.videobridge.rest.jetty.RewriteHandler.replacement=/
org.jitsi.videobridge.rest.jetty.tls.port=443
org.jitsi.videobridge.TCP_HARVESTER_PORT=443
org.jitsi.videobridge.rest.jetty.sslContextFactory.keyStorePath=/etc/jitsi/videobridge/example.meet.jit.si.jks
org.jitsi.videobridge.rest.jetty.sslContextFactory.keyStorePassword=changeit
```
4. You need to start jvb with rest and xmpp interface running. Add the
following to jvb config in etc:
JVB_OPTS="--apis=rest,xmpp"
AUTHBIND=yes
