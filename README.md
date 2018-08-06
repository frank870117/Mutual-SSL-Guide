# SSL-Guide
Basic Tutorial that teaches you how to set up a secure SSL with Liberty

## Step I: set up a basic liberty server

### Please refer to the [IBM Cloud HelloWorld](https://github.com/IBM-Cloud/java-helloworld) for a more comprehensive set-up 

We utilize Apache Maven to build this project. Please refer to the [Maven Website](http://maven.apache.org/) for instructions on how to install Apache Maven.

1. Clone from the follow repositorary: https://github.com/IBM-Cloud/java-helloworld.git

2. Move into the java-helloworld folder, then issue the command **mvn clean install** to create the /target/JavaHelloWorldApp.war file

3. You should see the following output: 
```
[INFO] Packaging webapp
[INFO] Assembling webapp [JavaHelloWorldApp] in [/[Insert-Directory]/java-helloworld/target/JavaHelloWorldApp-1.0-SNAPSHOT]
[INFO] Processing war project
[INFO] Copying webapp resources [/[Insert-Directory]/java-helloworld/src/main/webapp]
[INFO] Webapp assembled in [24 msecs]
[INFO] Building war: /[Insert-Directory]/java-helloworld/target/JavaHelloWorldApp.war
```
4. while you are in the java-helloworld folder, run **mvn liberty:run-server** to start up the server
  *Make sure you do not have a running application using Port:9080* 
  
5. You should see the following output:
```
  [INFO]  The server defaultServer has been launched.
  [INFO]  Monitoring dropins for applications.
  [INFO]  Web application available (default_host): http://YourLocalAddress:9080/JavaHelloWorldApp/
  [INFO]  Application JavaHelloWorldApp started in X seconds.
  [INFO]  The server installed the following features: [servlet-3.1].
  [INFO]  The server defaultServer is ready to run a smarter planet.
```
6. Check out your default server using the *http://[InsertLocalAddress]:9080/JavaHelloWorldApp/* from *Web application available (default_host)*






Servlet.java: 
  annotation: @servletSecurity @HttpConstraint 
  commented out basicAuthenticationMechanism
  for transportGuarantee, specify the path as javax.servlet.annotation.ServletSecurity.TransportGuarantee.CONFIDENTIAL
    (might be unnecessary, need testing)
  
index.html
  href: redirect to servlet or adminonly from server.xml
  
bootstrap.properties
  default http/https port location and context root
  
server.xml
  keyStore: default id and password
  basicRegistry: show user(name), user password, group(admin/user)
  httpEndpoint: called from bootstrap
  webApplcation: where the Servlet is stored (war file)
  traceSpecification: enable trace functionality
  
web.xml
  added the security constraint: transport guarantee confidential 

"/finish/target/liberty/wlp/usr/servers/defaultServer/resources/security"
  removed the key 
  
how it works:
  The client(browser/website) wants to access Liberty. key.jks is a self-signed SSL certificate. When the client visits Liberty, it checks its certificate with list of trusted CAs. In this case, since the cerificate was self-signed, we need to add a browser exception sayign that we trust this entity. 
  
what is mutual connection? 
  The website has its certificate attached to it. The server verifies the client certificate
  doesnt support jks 
  
  https://gist.github.com/mtigas/952344 --> generate a crt and pkcs12 
  
  
  
