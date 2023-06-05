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

7) JSP Expression Language to print values (JSTL for traversing data ex., list, map) :
- just add <%@page isELIgnored="false" %> in your jsp page 
- no need to store value in variable you can directly write key names for printing values in ${key name}
- JSTL dependency :
```
<!-- https://mvnrepository.com/artifact/jstl/jstl -->
<dependency>
    <groupId>jstl</groupId>
    <artifactId>jstl</artifactId>
    <version>1.2</version>
</dependency>
```
- To use the JSTL add taglib library in your jsp page where you want to use this dependency
```
Link : https://docs.oracle.com/javaee/5/jstl/1.1/docs/tlddocs/c/tld-summary.html

<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
```

Example using JSTL :
```
<!-- This is using JSTL dependency -->
		Traversing list of values 
		 <c:forEach var="friend" items="${friends}">
		 	<h3>${friend}</h3>
			<!-- you can use out also. see below -->
		 	<h1><c:out value="${friend}"></c:out></h1>
		 </c:forEach>
```

8) Sending data from view to controller :
	- using HTML form : view->controller
	- HttpServletRequest ka use karake hum data get kar sakate hai
		-getParameter("name of field")
	- Spring MVC :
		-  @RequestParam (for getting one value)
		-  @ModelAttribute (for getting multiple value which present in your class or  entity class)
	- @RequestMapping Annotation :
		- to map USRLs 
		- use for particular handler method or entire class
		- method request GET, POST etc.
		
	- @RequestParam Annotation :
		- By default it's a required if you want to make optional the give attribute required=false
		- type conversion applied automaticlly 
		- when an @RequestParam is used on a Map<String, String> or MultivalueMap<String, String> argument the map is populated with all request parameters 
	
	- @ModelAttribute :
		- we can use above the method or as a handler method attribute or variable 
		- which fields you want to make that field in seprate class
		- your class fields should match with form data field 

- Example for Sending data from view to controller
```
form.jsp 

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
    <%@page isELIgnored="false" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>${Header}</h1>
	<h1>${Desc}</h1>
	<!-- this for using HttpRequestServlet -->
	<form action="form" method="post">
  		<label>First name:</label>
  		<input type="text" name="fname"><br>
  		
  		<label>Last name:</label>
  		<input type="text" name="lname"><br>
  		
  		<label>Email ID:</label>
  		<input type="email" name="email"><br>
  		
  		<label>Password :</label>
  		<input type="password" name="password"><br>
  		
  		<input type="submit" value="Submit">
	</form>
</body>
</html>
```

```
success.jsp

<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
    <%@page isELIgnored="false" %>
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
	<h1>${Header}</h1>
	<h1>${Desc}</h1>
	<!-- this is output for using @RequestParam and HttpRequestServlet -->
	<h2>Welcome, ${fname} ${lname}</h2>
	<h2>It's your email id : ${email}</h2>
	<h2>And this is your password : ${password}</h2>
	
	<!-- This is for using @ModelAttribute -->
	<h2>Welcome, ${user.fname} ${user.lname}</h2>
	<h2>It's your email id : ${user.email}</h2>
	<h2>And this is your password : ${user.password}</h2>
	
</body>
</html>
```

```
user.java

package com.spring.mvc.model;

public class User {
	private String fname;
	private String lname;
	private String email;
	private String password;
	public User() {
		super();
		// TODO Auto-generated constructor stub
	}
	public User(String fname, String lname, String email, String password) {
		super();
		this.fname = fname;
		this.lname = lname;
		this.email = email;
		this.password = password;
	}
	public String getFname() {
		return fname;
	}
	public void setFname(String fname) {
		this.fname = fname;
	}
	public String getLname() {
		return lname;
	}
	public void setLname(String lname) {
		this.lname = lname;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getPassword() {
		return password;
	}
	public void setPassword(String password) {
		this.password = password;
	}
	@Override
	public String toString() {
		return "User [fname=" + fname + ", lname=" + lname + ", email=" + email + ", password=" + password + "]";
	}	
}
```

```
controller 

package com.spring.mvc.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ModelAttribute;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestMapping;

import com.spring.mvc.model.User;

@Controller
@RequestMapping("/form")
public class FormController {
//	@GetMapping()
//	public String getForm() {
//		return "form";
//	}
	
	/*
	//using servlet : old way
	@PostMapping()
	public String handleForm1(HttpServletRequest req, Model model) {
		String name = req.getParameter("fname");
		String lname = req.getParameter("lname");
		String email = req.getParameter("email");
		String password = req.getParameter("password");
		System.out.println(name);
		System.out.println(lname);
		System.out.println(email);
		System.out.println(password);
		
		//taking data fom controller to view page
		model.addAttribute("fname", name);
		model.addAttribute("lname", lname);
		model.addAttribute("email", email);
		model.addAttribute("password", password);
		return "success";
	}
	*/
	
	/*
	//using request param
	@PostMapping()
	public String handleForm2(
			@RequestParam("fname") String fname,
			@RequestParam("lname") String lname,
			@RequestParam("email") String email,
			@RequestParam("password") String password,
			Model model) {
		System.out.println(fname);
		System.out.println(lname);
		System.out.println(email);
		System.out.println(password);
		
		//process
		
		//taking data fom controller to view page
		model.addAttribute("fname", fname);
		model.addAttribute("lname", lname);
		model.addAttribute("email", email);
		model.addAttribute("password", password);
		return "success";
	}
	*/
	
	/*
	//it's a very lengthy. using module attrribute your code will be reduce
	@PostMapping()
	public String handleForm3(
			@RequestParam("fname") String fname,
			@RequestParam("lname") String lname,
			@RequestParam("email") String email,
			@RequestParam("password") String password,
			Model model) {
		User user = new User();
		user.setEmail(email);
		user.setFname(fname);
		user.setLname(lname);
		user.setPassword(password);
		System.out.println(user);
		
		//process
		
		//taking data fom controller to view page
		model.addAttribute("user",user);
		return "success";
	}
	*/
	
	/*This is the common method for model
	 * This will call automatically before handler methods
	 * no need to write code again and again in bothe the handler methods*/
	@ModelAttribute
	public void commonMethodForModel(Model m) {
		m.addAttribute("Header", "Form");
		m.addAttribute("Desc", "This is the description of form");
	}
	
	@GetMapping
	public String showHeading(Model m) {
//		m.addAttribute("Header", "Form");
//		m.addAttribute("Desc", "This is the description of form");
		return "form";
	}
	
	//using @ModelAttribute
	@PostMapping()
	public String handleForm3(@ModelAttribute User user, Model m) {
//		m.addAttribute("Header", "Form");
//		m.addAttribute("Desc", "This is the description of form");
		return "success";
	}
}
```

9) User Registration Form Using Spring MVC and ORM :
	- Dependency : spring ORM(5.2.3), hibernate-core(5.4.2), mySQL connector(5.1.30), spring mvc 
	- HibernateTemplateClass : HibernateTemplate is the class of org.springframework.orm.hibernate3. HibernateTemplate provides the integration of hibernate and spring. Spring manages database connection DML, DDL etc commands by itself. HibernateTemplate has the methods like save,update, delete etc. Try to understand how to configure HibernateTemplate in our spring application.

Add xml configuration in application.xml of spring application.
```
<bean id="hibernateTemplate" class="org.springframework.orm.hibernate3.HibernateTemplate">
<property name="sessionFactory">
  <ref bean="sessionFactory" />
</property>
```

- (access will be like this)controller->service layer->database layer(dao, repository)->DB
- 
