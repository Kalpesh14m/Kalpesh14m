# Servlet :man_technologist:	:computer:

## What is a Java Servlet

servlets are platform independent Java based web components that are managed by containers. These components generate dynamic content. They are in actual fact Java classes that are compiled to byte code that can be dynamically loaded and run by java web servers. Servlets communicate with web clients via request/response within the servlet container.

The major addition to the servlet 4.0 specification is the HTTP 2.0 specification implementation. More importantly it now implements Server Push and NIO!

Servlets run in the “servlet containers” and with these containers comes a bouquet of benefits. For example security, thread handling, monitoring and all those lovely things that we need, but don’t want to focus on when building solutions in the real world under the ever present “time crunch!”


### The Life Cycle of a Servlet

No explanation of servlets would be complete without a thorough understanding of the Servlet life cycle. Once we understand this from a component interaction perspective, Servlets become a lot simpler to implement. Especially in the context of multithreading and concurrency.

There are five main steps in the this life cycle:

- Loading

- Instantiation

- Initialisation

- Service

- Destruction

![](https://user-images.githubusercontent.com/25608527/99196316-a4a67880-27b1-11eb-9107-43b1f39e6fbb.png)


### Servlets:

1. When a request is received by the container for a Servlet. The class is loaded via the Class Loader.

2. The container instantiates the servlet class.

3. The init method which is found in the `javax.servlet.Servletinterface` is invoked by the web container.

4. The service method is invoked once the above three steps have been completed. Thereafter every time this instance of the Servlet is required to fulfil a 
request the service method is invoked.

5. Finally the container calls the destroy method in order to remove this instantiated class. At this point the servlet cleans up any memory or threads etc. that are no longer required.

---

## ServletLifeCycle.java
```
package com.java.kalpesh;

import java.io.IOException;
 
import javax.servlet.Servlet;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
 
public class ServletLifeCycle implements Servlet {
public class ServletLifeCycle implements Servlet {
 
    @Override //Servlet Life Cycle Method
    public void init(ServletConfig config) throws ServletException {
        /**
         * Called by the servlet container to indicate to a servlet that the servlet is being placed into service.
         *
         * The servlet container calls the <code>init</code> method exactly once after instantiating the servlet. 
         *
         * The init method must complete successfully before the servlet can receive any requests.
         *
         * The servlet container cannot place the servlet into service if the init method Throws a ServletException
         *
         * Does not return within a time period defined by the Web server
         */
    }
 
    @Override
    public ServletConfig getServletConfig() {
        /**
         *
         * Returns a {@link ServletConfig} object, which contains initialization and startup parameters for this servlet. 
         * The ServletConfig object returned is the one passed to the init method.
         *
         * Implementations of this interface are responsible for storing the ServletConfig object so that this method can return it. 
         *
         * The {@link GenericServlet} class, which implements this interface, already does this.
         */
        return null;
    }
 
    @Override //Servlet Life Cycle Method
    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        /**
         * Called by the servlet container to allow the servlet to respond to a request.
         *
         * This method is only called after the servlet's init() method has completed successfully.
         *
         * The status code of the response always should be set for a servlet that throws or sends an error.
         *
         * Servlets typically run inside multithreaded servlet containers that can handle multiple requests concurrently. 
         * Developers must be aware to synchronize access to any shared resources such as files, network connections, and as well as the servlet's class and instance variables.
         * More information on multithreaded programming in Java is available in the Java tutorial on multi-threaded programming.
         *
         */
    }
 
    @Override
    public String getServletInfo() {
        /**
         * Returns information about the servlet, such as author, version, and copyright.
         * 
         * The string that this method returns should be plain text and not markup of any kind (such as HTML, XML, etc.).
         */
        return null;
    }
 
    @Override //Servlet Life Cycle Method
    public void destroy() {
        /**
         * Called by the servlet container to indicate to a servlet that the servlet is being taken out of service. 
         *
         * This method is only called once all threads within the servlet's service method have exited or after a timeout period has passed. 
         * After the servlet container calls this method, it will not call the servic method again on this servlet.
         *
         * This method gives the servlet an opportunity to clean up any resources that are being held (for example, memory, file handles, threads) and make
         * sure that any persistent state is synchronized with the servlet's current state in memory.
         */
    }
}
```

---

## Example of Servlet:

```
package com.java.kalpesh;

import java.io.IOException;
import java.io.PrintWriter;
 
import javax.servlet.GenericServlet;
import javax.servlet.Servlet;
import javax.servlet.ServletConfig;
import javax.servlet.ServletException;
import javax.servlet.ServletRequest;
import javax.servlet.ServletResponse;
import javax.servlet.annotation.WebServlet;
 
@WebServlet("/ServletLifeCycle")
public class ServletLifeCycle implements Servlet {
     
    private ServletConfig servletConfig = null;
 
    @Override //Servlet Life Cycle Method
    public void init(ServletConfig config) throws ServletException {
        this.servletConfig = config;
        System.out.println("Servlet has been loaded by the class loader and instantiated already!!!");
        System.out.println("init(ServletConfig config) method invoked!");
        System.out.println("Servlet Name: " + servletConfig.getServletName());
    }
 
    @Override
    public ServletConfig getServletConfig() {
        return this.servletConfig;
    }
 
    @Override //Servlet Life Cycle Method
    public void service(ServletRequest req, ServletResponse res) throws ServletException, IOException {
        System.out.println("service(ServletRequest req, ServletResponse res) method invoked!");
        //set content type for response
        res.setContentType("text/html");
        PrintWriter out = res.getWriter();
        out.print("<b>com.jcg.example.servlet.ServletLifeCycle Example</b>");
    }
 
    @Override
    public String getServletInfo() {
        return "Codedictator Servlet Life Cycle Example";
    }
 
    @Override //Servlet Life Cycle Method
    public void destroy() {
        System.out.println("destroy() method invoked!");
    }
}
```

---

## Java Servlet Example in Eclipse IDE

Let’s walk through a step by step tutorial on creating a Java Servlet in Eclipse IDE. Using Eclipse as an IDE makes the job much faster. 

---

### 1. Downloading and Installing Eclipse IDE

**Navigate to the link:** [https://www.eclipse.org/downloads/](https://www.eclipse.org/downloads/) and download the latest release of Eclipse IDE for Java Developers. A zip file would be downloaded in your system. Extract that zip file in your preferred location. To launch Eclipse, click on the Eclipse icon in the Eclipse folder extracted from the last step.

---

### 2. Installing and Configuring Tomcat in Eclipse

To run any web application including Servlets, a web server is required. For this example, we will be using Apache Tomcat server as it is one of the most famous web server and quite easy to configure.

**Navigate to the link:** [https://tomcat.apache.org/download-90.cgi](https://tomcat.apache.org/download-90.cgi) .
- Scroll down the page to the ‘Binary Distributions’ section. Under it, you can see ‘Core’ section. From that section, download the zip file as per your Operating System.

- Extract the zip folder in any preferred location.

- In Eclipse, right click on the Servers tab located at the bottom. From the options, click on New->Server.

- Select Apache from the list and the appropriate version of the Tomcat server. Click Next.

- After that, in the dialog box that appears, populate the Tomcat installation directory as the location of the Tomcat folder extracted in Step 3.

- Click Finish.

---

### 3. Creating the Project

#### 3.1 To make a Servlet enabled web project

Follow the below steps:

- Launch Eclipse and then click on File -> New -> Dynamic Web Project.

- Mention the Project name as ‘ServletDemo’ and Target Runtime as Apache Tomcat and Click on Next.

- Enable the Checkbox which says ‘Generate web.xml deployment descriptor’.

- Click Finish.

**NOTE:** The above steps set up the Project structure.


#### 3.2 Now we will download the `javax servlet jar` and include it in the build path of the project.

Follow the below steps:

**Navigate to the link:** [https://mvnrepository.com/artifact/javax.servlet/servlet-api](https://mvnrepository.com/artifact/javax.servlet/servlet-api)

- Download the JAR.

- Copy the JAR into the directory ServletDemo/WebContent/WEB-INF/lib.

- Right click on the Project ServletDemo and click on Build Path -> Configure Build Path.

- Add the JAR into the Build Path by browsing to the location ServletDemo/WebContent/WEB-INF/lib.

**NOTE:** The above steps would allow us to use servlet API to create servlets in Eclipse. 

#### 3.3 Now we will write code to create a Servlet. 

Follow the below steps :

Right click on src folder in the Project and click on New -> Class and mention the class name as ServletDemo. This will open the Eclipse editor for the class ServletDemo. Write the below code in the ServletDemo class :

```
import java.io.IOException;
import java.io.PrintWriter;
 
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
 
public class ServletDemo extends HttpServlet{
    private String msg;
    @Override
    public void init() throws ServletException {
          msg = "Welcome To CodeDictator";
    }
 
    @Override
    public void doGet(HttpServletRequest request,HttpServletResponse response)
          throws ServletException, IOException 
    {
        // Setting up the content type of webpage
        response.setContentType("text/html");
        // Writing message to the web page
        PrintWriter out = response.getWriter();
        out.println("<h1>" + msg + "</h1>");
    }
 
    @Override
    public void destroy() {
          /* leaving empty for now this can be
           * used when we want to do something at the end
           * of Servlet life cycle
           */
    }
}
```    

**A brief discussion on the above methods :**

- **init( ) :** This method is called only for the first HTTP request and not for the subsequent requests. So this method is used for one time initializations.

- **doGet( ) :** All GET requests are handled by this method.

- **destroy( ) :** This method is called once at the end of the lifecycle of the servlet and is used to close external connections like DB connections, closing files etc.

#### 3.4 Now we will create an HTML file index.html which will contain a link to call the servlet. The location of index.html would be `ServletDemo/WebContent`.

```
<!DOCTYPE html>
<html>
   <head>
   <meta charset="UTF-8">
      <title>Servlet Demo</title>
   </head>
   <body>
      <a href="welcome">Click to call Servlet</a>
   </body>
</html>
```

#### 3.5 Now we need to map the Servlet to a specific URL. As we are calling welcome page upon clicking the link on the `index.html` so we are going to map the Servlet with the welcome page. The place to do this mapping is `web.xml` which is present in `WebContent/WEB-INF/web.xml`.

`Web.xml` is also called as ___deployment descriptor___. The deployment descriptor describes the classes, resources and configurations of the web application. Whenever the web server receives a request for the web application, it uses `web.xml` to map the URL with the code that is made to handle that request. Web.xml resides at `WEB-INF/web.xml`.
```
<?xml version="1.0" encoding="UTF-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns="http://java.sun.com/xml/ns/javaee" xsi:schemaLocation="http://java.sun.com/xml/ns/javaee http://java.sun.com/xml/ns/javaee/web-app_3_0.xsd" id="WebApp_ID" version="3.0">
  <display-name>ServletDemo</display-name>
  <welcome-file-list>
    <welcome-file>index.html</welcome-file>
    <welcome-file>index.htm</welcome-file>
    <welcome-file>index.jsp</welcome-file>
    <welcome-file>default.html</welcome-file>
    <welcome-file>default.htm</welcome-file>
    <welcome-file>default.jsp</welcome-file>
  </welcome-file-list>
   
  <servlet>
    <servlet-name>ServletDemo</servlet-name>
    <servlet-class>ServletDemo</servlet-class>
  </servlet>
 
  <servlet-mapping>
    <servlet-name>ServletDemo</servlet-name>
    <url-pattern>/welcome</url-pattern>
  </servlet-mapping>
 
</web-app>
```

---

### 4. Run

Finally, to run this, right click on `index.html` and choose Run As -> Run on Server.

Eclipse will open the in-built browser with the address as [`http://localhost:8080/ServletDemo/index.html`](http://localhost:8080/ServletDemo/index.html). You will see the link ‘Click to call Servlet’. Upon clicking the link, you will see the below output :

`Welcome To Codedictator`

---

## Index of Learning:

![](https://user-images.githubusercontent.com/25608527/98762583-fdff5800-23fd-11eb-90b3-3934763c5bf7.png)

![](https://user-images.githubusercontent.com/25608527/98762584-ffc91b80-23fd-11eb-9c02-990edbc77eb1.png)

![](https://user-images.githubusercontent.com/25608527/98762589-022b7580-23fe-11eb-9b3e-7640c7bcd746.png)

![](https://user-images.githubusercontent.com/25608527/98762593-035ca280-23fe-11eb-8f7c-88499042b6c9.png)

---

| Index | Topics | Repo |
| :-------------: | :------------- |:-------------| 
| 1 | **Servlet** | [https://github.com/Kalpesh14m/Servlet-Demo](https://github.com/Kalpesh14m/Servlet-Demo) |
| 2 | **Servlet:** Login Registration Demo | [https://github.com/Kalpesh14m/Servlet-Login-Reg-Demo](https://github.com/Kalpesh14m/Servlet-Login-Reg-Demo) |
