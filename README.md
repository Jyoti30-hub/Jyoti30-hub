package com.model;
public class User {
	public int regid;
	public String name;
	public int age;
	public String email;
	public String userName;
	public String password;
	
	

	public User(int regid, String name, int age, String email, String userName, String password) {
		super();
		this.regid = regid;
		this.name = name;
		this.age = age;
		this.email = email;
		this.userName = userName;
		this.password = password;
	}

}

===========================================================================

package com.service;
import java.security.SecureRandom;
import java.util.Scanner;

import com.model.User;

public class LogBook {
	Scanner s=new Scanner(System.in);
	public User register()
	{
	System.out.println("Enter your regid: ");
	int id=s.nextInt();
	System.out.println("Enter your name: ");
	String nm=s.next()+s.nextLine();
	System.out.println("Enter your age: ");
	int age=s.nextInt();
	System.out.println("Enter your email: ");
	String eml=s.next()+s.nextLine();
	String uname=nm+"@LogBook";
	String pass=LogBook.PassGen();
	User u1=new User(id, nm, age, eml, uname, pass);
	return u1;
	}
	
	public void login(User u)
	{
		System.out.println("Enter your username:");
		String unm=s.next();
		if(unm.equals(u.userName))
		{
			System.out.println("Enter your password:");
			String pass=s.next();
			if(pass.equals(u.password))
			{
				System.out.println("Login Successfull");
			}
			else
			{
				System.out.println("password incorrect");
			}
		}
		else
		{
			System.out.println("Username incorrect");
		}
	
	
    }
	public void logout()
	{
		System.out.println("Logged out successfully......");
		System.exit(0);
	}
	
	public static String PassGen()
	{
		SecureRandom sr=new SecureRandom();
		String lowerCase="abcdefghijklmnopqrstuvwxyz";
		String upperCase=lowerCase.toUpperCase();
		String splChar="!@#$%^&*";
		String num="0123456789";
		String allChar=lowerCase+upperCase+splChar+num;
		StringBuffer sb=new StringBuffer(9);
		
		for(int i=0;i<8;i++)
		{
			sb.append(allChar.charAt(sr.nextInt(allChar.length())));
		}
		String res=sb.toString();
		return res;
	}

}

===========================================================================

package com.customer;
import java.util.Scanner;

import com.model.User;
import com.service.LogBook;

public class Test {

	public static void main(String[] args) {
		Scanner s=new Scanner(System.in);
		LogBook lb=new LogBook();
		User u=null;
		
		while(true)
		{		
		System.out.println("Welcome to vault Access............");
		System.out.println("1.Register yourself.......\n2.Login\n3.Logout");
		System.out.println("Enter your choice");
		int ch=s.nextInt();
		
		switch(ch)
		{
		case 1:
			u=lb.register();
			System.out.println("Registration completed...");
			System.out.println("Username:"+u.userName);
			System.out.println("Password:"+u.password);
			System.out.println("You can login now.....");
		break;
		case 2:
			lb.login(u);
		break;
		case 3:
			lb.logout();
		break;
		default:
			System.out.println("Invalid Option...");
			break;
			
		}
	}
  }
}
