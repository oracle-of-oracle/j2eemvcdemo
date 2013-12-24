index.html
---------------------------------------------------------------------------
<!DOCTYPE html>
<html>
<head>
<meta charset="ISO-8859-1">
<title>J2EE and MVC Demo program</title>
</head>
<body>
<h1>The View pages are implemented in JSP</h1>
<h1>The controller is implemented as J2eedemo servlet</h1>
<h1> Please click <a href="Userregistrationpage.jsp">in userregistration page</a></h1>
</body>
</html>

Userregistrationpage.jsp
------------------------------------------------------------------------------
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
 <form action="/j2eedemo" method="post">
Enter the First Name:<input type="text" name="fname"><br>
Enter the Last Name	:<input type="text" name="lname"><br>
Enter your Age		:<input type="number" name="age"><br>
<input type="radio" name="gender" value="male">Male<br>
<input type="radio" name="gender" value="female">Female<br>
<input type="submit" value="REGISTER">
</form>

</body>
</html>

j2eedemoServlet.java
--------------------------------------------------------------------
package com.skn.j2eedemo;
import java.io.IOException;
import javax.servlet.RequestDispatcher;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import javax.servlet.http.HttpSession;
import com.skn.j2eedemo.user;

@SuppressWarnings("serial")
public class J2eedemoServlet extends HttpServlet{
	HttpSession session;
	user user1;
	public void doPost(HttpServletRequest req, HttpServletResponse resp)
			throws IOException, ServletException {
		session = req.getSession();
		user1=(user)session.getAttribute("u1");
		String Fname=req.getParameter("fname");
		String Lname=req.getParameter("lname");
		int Age  =Integer.parseInt(req.getParameter("age"));
		String Gender=req.getParameter("gender");
		if(user1==null)
		{
			user1=new user();
		}
		user1.setFname(Fname);
		user1.setLname(Lname);
		user1.setAge(Age);
		user1.setGender(Gender);
		session.setAttribute("user1", user1);
		RequestDispatcher rd = req.getRequestDispatcher("TestData.jsp");
       rd.forward(req, resp);
	}
}

user.java
----------------------------------------------------------------------
package com.skn.j2eedemo;

import java.io.Serializable;

public class user implements Serializable {
	private String fname,lname,gender;
	private int age;
	
	public int getAge() {
		return age;
	}
	public void setAge(int age) {
		this.age = age;
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
	public String getGender() {
		return gender;
	}
	public void setGender(String gender) {
		this.gender = gender;
	}
}
TestData.jsp
<%@ page language="java" contentType="text/html; charset=ISO-8859-1"
    pageEncoding="ISO-8859-1"%>
<!DOCTYPE html PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
<html>
<head>
<meta http-equiv="Content-Type" content="text/html; charset=ISO-8859-1">
<title>Insert title here</title>
</head>
<body>
<h1>Person Information</h1>
        <h2>The first name of the user  is ${user1.fname}</h2> 
        <h2>The last name of the user  is ${user1.lname}</h2>
        <h2>The age of the user  is ${user1.age}</h2>
        <h2>The gender of the user is ${user1.gender}</h2>
        
</body>
</html>

web.xml
--------------------------------------------------------------------------
<?xml version="1.0" encoding="utf-8"?>
<web-app xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
xmlns="http://java.sun.com/xml/ns/javaee"
xmlns:web="http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd"
xsi:schemaLocation="http://java.sun.com/xml/ns/javaee
http://java.sun.com/xml/ns/javaee/web-app_2_5.xsd" version="2.5">
	<servlet>
		<servlet-name>J2eedemo</servlet-name>
		<servlet-class>com.skn.j2eedemo.J2eedemoServlet</servlet-class>
	</servlet>
	<servlet-mapping>
		<servlet-name>J2eedemo</servlet-name>
		<url-pattern>/j2eedemo</url-pattern>
	</servlet-mapping>
	<welcome-file-list>
		<welcome-file>index.html</welcome-file>
	</welcome-file-list>
</web-app>





