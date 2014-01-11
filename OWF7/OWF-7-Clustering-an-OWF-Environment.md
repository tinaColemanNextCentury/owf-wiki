# Appendix B Clustering an OWF Environment
This following section details how to modify Tomcat and Apache HTTP Server configurations for clustering OWF. Configuring OWF in a clustered environment tends to differ widely between specific web application servers. Be sure to refer to an individual application server’s documentation for specific details on how it should be configured for clustering.  

Find general installation instructions and configurations required for Tomcat clustering in the [Tomcat documentation](http://tomcat.apache.org/tomcat-6.0-doc/cluster-howto.html).

For purposes of this document, assume that the Apache HTTP Server and Load Balancer have been installed on a host named cluster and OWF is on two separate hosts named `node1` and `node2`.

##Tomcat Configuration
Navigate to `/apache-tomcat-7.0.21/conf/server.xml`, and make the following changes:
 
1.	Add the `jvmRoute` attribute to the `Engine` element. The attribute should be a string that uniquely identifies the node in the cluster: 

        <Engine name="Catalina" defaultHost="localhost" jvmRoute="node1">
2.	Uncomment the `Cluster` element that is in the `Engine` element:

        <Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster"/>
3.	Comment out any `Connector` elements with their protocol attribute set to HTTP/1.1 and uncomment the `Connector` element with its protocol set to AJP/1.3. Use port="8009" and redirectPort="8443":

        <Connector port="8009" protocol="AJP/1.3" redirectPort="8443"/>

> *Note: For max performance, uncomment the AprLifecycleListener (this isn't strictly clustering related).* 

The `server.xml` file must include: 

        <?xml version='1.0' encoding='utf-8'?>
        <Server port="8005" shutdown="SHUTDOWN">

          <Listener className="org.apache.catalina.core.AprLifecycleListener" SSLEngine="on" />
          <Listener className="org.apache.catalina.core.JasperListener" />
          <Listener className="org.apache.catalina.core.JreMemoryLeakPreventionListener" />
          <Listener className="org.apache.catalina.mbeans.GlobalResourcesLifecycleListener" />
          <Listener className="org.apache.catalina.core.ThreadLocalLeakPreventionListener" />

          <Service name="Catalina">

            <Connector port="8009" protocol="AJP/1.3" redirectPort="8443" />
            <Engine name="Catalina" defaultHost="localhost" jvmRoute="node1">

              <Cluster className="org.apache.catalina.ha.tcp.SimpleTcpCluster"/>

              <Host name="localhost"  appBase="webapps" unpackWARs="true" autoDeploy="true"></Host>

            </Engine>
          </Service>
        </Server>

##OWF Configuration
Copy `etc/override/ehcache.xml` into `apache-tomcat-7.0.21/lib`.

Configure `apache-tomcat-7.0.21/lib/OzoneConfig.properties` to use the host and port through which clients will be accessing OWF and not the host and port of this particular node:

        ozone.host = cluster
        ozone.port = 8443

##OS Configuration
For best performance, make sure the Apache Portable Runtime (APR) and Apache Tomcat Native libraries are installed on the node servers. The procedure is optional and installation varies by OS.  Accordingly, be sure to refer to [Tomcat's native document](http://tomcat.apache.org/native-doc/) and [Tomcat's APR document](http://tomcat.apache.org/tomcat-6.0-doc/apr.html) for information on setting up APR/Native on a specific OS.

> _Note: If the associated load balancer and node servers are behind a firewall, make sure all relevant ports are open for TCP/UDP (Examples: 8009, 8080, 8443, etc)._

##Apache HTTP/Load Balancer Configuration
In the following installation example, Apache Web Server (httpd) 2.x is used. Refer to the [Apache Documentation](http://httpd.apache.org/) for download access, installation instructions, and configuration information.

1.	Install `mod_jk` (The Apache Tomcat Connector and load balancer). Please refer to [Tomcat Documentation](http://tomcat.apache.org/connectors-doc/index.html) for download, install, and configuration.
Depending on the distribution installed, the exact layout of configuration files vary, but the following changes need to be made to the server’s httpd configuration:
2.	Change the Listen configurations to 8080 and 8443, instead of 80 and 443:

        Listen 8080
        Listen 8443
3.	Use a LoadModule directive to `load mod_jk`:

        LoadModule jk_module modules/mod_jk.so
4.	Configure `mod_jk` with the following properties:
   * `JkWorkersFile` - This should be the location of a `workers.properties` file (described below)
   * `JkLogLevel` info - Can be set to 'debug' if extra logging is desired
   * `JkOptions +ForwardDirectories - allows paths like `https://localhost:8443/owf/` to work
   * `JkMount /owf*` balancer - tells `mod_jk` to foward requests for `/owf` to the worker named balancer (defined in `workers.properties`)
   * `JkMount /cas*` node1 - tells `mod_jk` to forward requests for `/cas` to the worker named `node1` (defined in `workers.properties`)
5.	Make sure that `mod_ssl` gets loaded:

        LoadModule ssl_module modules/mod_ssl.so
6.	Configure SSL with the following properties:
   * `SSLEngine` on
   * `SSLCertificateFile` - the certificate for the server
   * `SSLCertificateKeyFile` - the private key for the server
   * `SSLCertificateChainFile` - the CA chain for the server 
   * `SSLCACertificateFile` - the CA used to validate client certs 
   * `SSLVerifyClient optional` - for behavior equivalent to tomcat's clientAuth="want" (can be changed as desired)
   * `SSLOptions +ExportCertData` - needed for OWF to obtain cert information
7.	Create a `workers.properties` file, which needs to be referenced in the `JkWorkersFile` property described above.

The names of workers need to be the same as the `jvmRoute` that was set on the corresponding node. The `worker.list` entry defines which workers are accessible from within the Apache server’s httpd configuration.
<br>The sample below includes three workers: the actual load balancer (whose type is set to 'lb') and a worker for each node.

    #Expose the balanced worker, and also owfcluster02 so we can route
    #all CAS requests directly to it (not clustering CAS)
    worker.list=balancer,node1
    worker.balance.type=lb
    worker.balancer.balance_workers=node1,node2
    worker.node1.type=ajp13
    worker.node1.host=node1
    worker.node1.port=8009
    worker.node2.type=ajp13
    worker.node2.host=node2
    worker.node2.port=8009

