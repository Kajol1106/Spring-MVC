## Spring MVC
- sub famework of Spring framework which is used to build a web application.
- build on the top of Servlet API
- it follows the MVC(Model-View-Controller) design pattern.
- it implement all the basic features of core spring framework lie IOC(Inversion of Control), DI(Dependency Injection).

1) Why Spring MVC : 
- seprate each role model, view, controller etc.
- powerful configuration
- it is sub framework of spring framework. use of spring core features like IOC etc.
- rapid application development
- it is flexible, easy to test and much features.

2) MVC Design Pattern :
- Model - Data (business logic)
- View- presents data to user (User interface)
- Controller- interface b/w model and view
- way to organize the code in our application

3) Problem without MVC design pattern :
- one person doing take order, prepare food, final delivery it will be very hectic for that person because if at the time of making food other person will come. (will get problem like this way to doing work)
- one for take order, one for preparing food, one person for doing delivery means all work will be fine (problem will be solved using this way)

4) Working of Spring MVC :
- Client(request)-> Front Controller(DispatcherServlet)(Delegate the request)(using handover mapping controller ko request dega)-> Controller(Handles the request)(sare layer ki help le sakata hai like DAO, Service etc.)(delegate rendering of response)-(model)->Front Controller(view resolver ka use karake response wapas Front controller ko bhej dega)-> client(response) 

5) Creating Spring MVC project in Eclipse :
- configure the dispatcher servlet in web.xml
  ```
  <!-- configure dispatcher servlet -->
  <servlet>
  	<servlet-name>dispatcher</servlet-name>
  	<servlet-class>org.springframework.web.servlet.DispatcherServlet</servlet-class>
  </servlet>
  <servlet-mapping>
  	<servlet-name>dispatcher</servlet-name>
  	<!-- / means sare url ke request handle karna -->
  	<url-pattern>/</url-pattern>
  </servlet-mapping>
  ```
- create spring configuration file (dispatcher-servlet.xml- web.xml mein jo name servlet ke liye diya hai wahi use karna) in WEB-INF 
  ```
  <beans xmlns="http://www.springframework.org/schema/beans"
	xmlns:context="http://www.springframework.org/schema/context"
	xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
	xsi:schemaLocation="
  http://www.springframework.org/schema/beans
  http://www.springframework.org/schema/beans/spring-beans.xsd
  http://www.springframework.org/schema/context
  http://www.springframework.org/schema/context/spring-context.xsd">
 
	<context:component-scan base-package="base package name" />
 
	<bean class="org.springframework.web.servlet.view.InternalResourceViewResolver">
		<property name="prefix">
			<value>/WEB-INF/views/</value>
		</property>
		<property name="suffix">
			<value>.jsp</value>
		</property>
	</bean>
  </beans>
  ```
- configure view resolver
  ```
  /WEB-INF/views/name.jsp (create a view directory in WEB-INF) folder
  ```
- create controller
  ```
  package com.spring.mvc;

  import org.springframework.stereotype.Controller;
  import org.springframework.web.bind.annotation.GetMapping;
  import org.springframework.web.bind.annotation.RequestMapping;

  @Controller
  @RequestMapping("/home")
  public class HomeController {
	  @GetMapping
	  public String home() {
		  System.out.println("This is home page url");
		  return "index";		//jsp page name
	  }
  }
  ```
- create a view to show(page)
```
index.jsp :
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>This is the index or home page</h1>
</body>
</html>
```

- pom.xml file :
```

```

6) Sending data from controller to view :
- Model or ModelAndView mein data rakh ke hum le ja sakate hai data view tak
- Model method : addAttribut(String key, Object value)
- ModelAndView : addObject(String key, Object value)

7)JSP Expression Language to print values (JSTL for traversing) :
- just add <%@page isELIgnored="false" %> in your jsp page 
- no need to store value in variable you can directly write key names for printing values in ${key name}
