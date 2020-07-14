<img src="images/wawa.jpg" width="100" height="100"/>

[![Build Status](https://travis-ci.org/openmrs/openmrs-core.svg?branch=master)](https://travis-ci.org/openmrs/openmrs-core) [![Coverage Status](https://coveralls.io/repos/github/openmrs/openmrs-core/badge.svg?branch=master)](https://coveralls.io/github/openmrs/openmrs-core?branch=master) [![Codacy Badge](https://api.codacy.com/project/badge/Grade/a51303ee46c34775a7c31c8d6016da6b)](https://www.codacy.com/app/openmrs/openmrs-core?utm_source=github.com&amp;utm_medium=referral&amp;utm_content=openmrs/openmrs-core&amp;utm_campaign=Badge_Grade)

## Application on Spring Security JWT 
POC to demonstrate the knowledge on Spring Security and JWT

#### Table of Contents

1. [Build](#build)
   1. [Prerequisites](#prerequisites)
   2. [Build Command](#build-command)
   3. [Deploy](#deploy)
2. [Navigating the repository](#navigating-the-repository)
3. [Technology](#technology)
4. [API Documentation](#API-Documentation)
   1. [UML Diagram](#UML-Diagram)
   2. [Dependent Downstream Servicesm](#Dependent-Downstream-Services)
5. [Deployments](#Deployments)
6. [Testing](#Testing)
6. [DataSource configuration](#DataSource-configuration)
7. [Exception handling](Exception-handling)
7. [Coding Standards](#Coding-Standards)
8. [POM Dependencies](#POM-Dependencies)
9. [Collaboration](#Collaboration)
10. [License](#license)

## Build

### Prerequisites

#### Java

Install Java8 (https://www.oracle.com/java/technologies/java8.html).
If you want to build the master branch you will need a Java JDK of minimum version 8.

#### Maven

Install the build tool [Maven](https://maven.apache.org/).

You need to ensure that Maven uses the Java JDK needed for the branch you want to build.

To do so execute

```bash
mvn -version
```

which will tell you what version Maven is using. Refer to the [Maven docs](https://maven.apache.org/configure.html) if you need to configure Maven.

#### Git

Install the version control tool [git]https://github.com/wawa/) and clone this repository with

```bash
git clone  https://github.com/wawa/admin-toolstack-config.git
```

### Build Command

After you have taken care of the [Prerequisites](#prerequisites)

Execute the following

```bash
cd openmrs-core
mvn clean package
```


### Deploy

For development purposes you can simply deploy the `openmrs.war` into the application server jetty via

```bash
cd openmrs-core/webapp
mvn jetty:run
```

If all goes well (check the console output) you can access the OpenMRS application at `localhost:8080/openmrs`.

Refer to [Getting Started as a Developer - Maven](https://wiki.openmrs.org/display/docs/Maven) for some more information
on useful Maven commands and build options.

## Navigating the repository

The project tree is set up as follows:

<table>
 <tr>
  <td>api/</td>
  <td>Java and resource files for building the java api jar file.</td>
 </tr>
 <tr>
  <td>web/</td>
  <td>Java and resource files that are used in the webapp/war file.</td>
 </tr>
 <tr>
  <td>webapp/</td>
  <td>files used in building the war file (contains JSP files on older versions).</td>
 </tr>
 <tr>
  <td>pom.xml</td>
  <td>The main maven file used to build and package OpenMRS.</td>
 </tr>  
</table>

## Technology

- **Spring Boot**     - Server side framework
- **JPA**             - Entity framework
- **Lombok**          - Provides automated getter/setters
- **Actuator**        - Application insights on the fly
- **Spring Security** - Spring's security layer
- **Thymeleaf**       - Template Engine
- **Devtools**        - Support Hot-Code Swapping with live browser reload
- **JJWT**            - JWT tokens for API authentication
- **Swagger**         - In-built swagger2 documentation support
- **Docker**          - Docker containers
- **Junit**           - Unit testing framework
- **H2**              - H2 database embedded version



## API Documentation
POC to demonstrate the knowledge on Spring Security and JWT
JWT (shortened from JSON Web Token) is the missing standardization for using tokens to authenticate on the web in general, not only for REST services. Currently, it is in draft status as RFC 7519. It is robust and can carry a lot of information, but is still simple to use even though its size is relatively small. Like any other token, JWT can be used to pass the identity of authenticated users between an identity provider and a service provider (which are not necessarily the same systems). It can also carry all the user’s claim, such as authorization data, so the service provider does not need to go into the database or external systems to verify user roles and permissions for each request; that data is extracted from the token.

### UML Diagram
Detailed UML Diagram for the Application

<img src="images/uml.jpg" width="350" height="350"/>

### Dependent Downstream Services
   [Spring Security](https://spring.io/guides/topicals/spring-security-architecture)

   [JWT](https://jwt.io/introduction/)


## Deployments

### Deploy Microservice

[Deploying a Microservice Via an automated CI/CD Pipeline](https://wawaappdev.atlassian.net/wiki/spaces/EE/pages/659751676/SBB+-+BE+Deploy+Microservice)

### Deploy UI Web App
[Deploying UI Web App](https://wawaappdev.atlassian.net/wiki/spaces/EE/pages/660046657/SBB+-+FE+Deploy+UI+Web+App)

### Deploying a Microservice to Docker Container
[Deploying a Microservice to Docker Container](https://www.javainuse.com/devOps/docker/docker-jar)


## Testing
## Unit test cases
There are multiple unit test cases written to cover the different components of the application. However there is a global application test suite file _**UnitTests.java**_ that combines all the test cases in a logical manner to create a complete suite. It can be run from command prompt using the following command -

````
mvn clean test -Dtest=ApplicationUnitTests
````

## Integration test cases
There are multiple integration test cases written to cover the different components of the application. However there is a global application test suite file _**ApplicationTests.java**_ that combines all the test cases in a logical manner to create a complete suite. It can be run from command prompt using the following command -

````
mvn clean test -Dtest=SpringApplicationTests
````


## DataSource configuration
1. Maven Dependencies
<img src="images/pom.JPG" width="400" height="550"/>
2. application.properties
DataSource configuration is provided by external configuration properties ( spring.datasource.* ) in application.properties file.
The properties configuration decouple the configuration from application code. This way, we can import the datasource configurations from even configuration provider systems.
Below given configuration shows sample properties for H2, MySQL, Oracle and SQL server databases.
<img src="images/maven.JPG" width="400" height="400"/>
3. DataSource Bean
Recommended way to create DataSource bean is using DataSourceBuilder class within a class annotated with the @Configuration annotation. The datasource uses the underlying connection pool as well.
<img src="images/jpa.JPG" width="400" height="550"/>
4. JNDI DataSource
If we deploy your Spring Boot application to an Application Server, we might want to configure and manage the DataSource by using the Application Server’s built-in features and access it by using JNDI.
We can do this using the spring.datasource.jndi-name property. e.g.
<img src="images/jndi.JPG" width="800" height="90"/>


## Exception handling
  ### Default spring validation support
       To apply default validation, we only need to add relevant annotations in proper places. i.e.
       1.Annotate model class with required validation specific annotations such as @NotEmpty, @Email etc.
       2.Enable validation of request body by @Valid annotation
  ### Exception model classes
      Creating seperate classes to denote specific business usecase failure and return them when that usecase fail.
      e.g. I have created RecordNotFoundException class for all buch scenarios where a resource is requested by it’s ID, and resource is not found in the system.
      <img src="images/exception.JPG" width="400" height="400"/>
  ### Custom ExceptionHandler
      Now add one class extending ResponseEntityExceptionHandler and annotate it with @ControllerAdvice annotation.
      ResponseEntityExceptionHandler is a convenient base class for to provide centralized exception handling across all @RequestMapping methods through @ExceptionHandler           methods. @ControllerAdvice is more for enabling auto-scanning and configuration at application startup.
      <img src="images/customexception.JPG" width="400" height="400"/>



## Coding Standards

[Best Coding Standards](https://google.github.io/styleguide/javaguide.html)

[Best practices for effective & efficient agile code reviews](https://queue-it.com/blog/agile-code-review-best-practices/)

## POM Dependencies


## Collaboration

Confluence(https://wawaappdev.atlassian.net/secure/Dashboard.jspa)

## License

[Engineering Team3](https://wawaappdev.atlassian.net/secure/RapidBoard.jspa?rapidView=280&projectKey=EN3) © [WAWA](https://www.wawa.com/)

