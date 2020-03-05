
  In class (snippet below) NameBoundCDIProxiesInterceptor  line 23
  application class isSynthetic returns "true" when this RESTEasy integtration-test
  test is run using wildfly.  When this test is run using quarkus isSynthetic returns "false". 

   /** The application context, used for retrieving the {@link ApplicationPath} value. */
19   @Context Application application;
20
21   @Override
22   public void filter(ContainerRequestContext requestContext, ContainerResponseContext responseContext) throws IOException {
23      boolean b = application.getClass().isSynthetic(); // todo debug remove
24      Object entity = application.getClass().isSynthetic() ? in + responseContext.getEntity() + "-out" : responseContext.getEntity();
25      responseContext.setEntity(entity);
26   }

-------------------------


Before running the test install this archive in your local repo.
Here is the cmd to do it.

mvn install:install-file \
   -Dfile=___FIX_THIS___/lib/utils-arquillian-utils-4.5.0-SNAPSHOT.jar \
   -DgroupId=org.jboss.resteasy \
   -DartifactId=utils-arquillian-utils \
   -Dversion=4.5.0-SNAPSHOT \
   -Dpackaging=jar 

Execution env.
    jdk 11.0.2
    mvn 3.6.0
    quarkus 999-SNAPSHOT
    
 
Set breakpoints in 
    NameBoundCDIProxiesInterceptor  line 23


  Compile project:
    mvn clean test -DskipTests=true
  
  Run tests
    mvn test
    or
    mvn test -Dmaven.surefire.debug
  