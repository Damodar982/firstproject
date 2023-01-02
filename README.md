# firstproject
this is my first project
package com.first.project;
import java.util.Random;
import java.util.Scanner;
class Account{
	 long accountNo=123456l;
	 String password="Damodar@98";
	 double balance=5000;
	Scanner scannerObj=new Scanner(System.in);
//method to verify account number
     void accountNumberVerification() {
    	 System.out.print(" enter the account no : ");long num=scannerObj.nextLong();
    	 if(num==accountNo) {
    		 passwordCheck();
    	 }
    	 else  {
    		 System.out.println("please enter the correct account number :");
    		 accountNumberVerification();
    	 }	 
     }
 //method to verify account password
	 void passwordCheck() {
		 System.out.println("enter the password :"); String pass=scannerObj.next();
		 if(password.equals(pass)) {
			 System.out.println("success ");
		 }
		 else {
			 System.out.println("you have enterd  wrong password ");
			 System.out.println("please enter the valid password :");
			 passwordCheck();
		 }
	 }
}
class NextOptions extends Account{
//method to display the options
	void enterDigit() { 
		System.out.println("welcome to the Indian Bank");
		int deposit=1,withdraw =2,transfer=3,logout=4;
		System.out.println("1=deposit\n2=withdraw\n3=transfer\n4=logout");
		System.out.print("choose the option :");
		int Options =scannerObj.nextInt();
		if(Options>4||Options<=0) {
			System.out.println("choose the correct option ");
			enterDigit();
		}
//conditions to check the entered option with available options
		if(Options==deposit) {
			System.out.print("enter the deposit amount :");
			double depositAmount=scannerObj.nextDouble();
			balance=balance+depositAmount;
			System.out.println("your current balance :"+balance);
			enterDigit();
		}
		if(Options==withdraw) {
			System.out.print("enter the withdraw amount :");
			double withdrawAmount=scannerObj.nextDouble();
			if(withdrawAmount>balance) {
				System.out.println("you have insufficient balance ");
				System.out.println("choose the amount with in the available balance ");
				enterDigit();
			}
			balance=balance-withdrawAmount;
			System.out.println("your withdrwal amount is :"+withdrawAmount);
			System.out.println("updated balance :"+balance);
			enterDigit();
		}
		if(Options==transfer) {
			System.out.print("generate the otp :");
			Random ran=new Random();  //random class  to generate otp
			  long newOtp =ran.nextLong(1000,9999);
			  System.out.println(newOtp);
			  System.out.print("enter the generated otp :");
			  long enteredOtp=scannerObj.nextLong();
			  System.out.println("entered otp is :"+enteredOtp);
			  if(enteredOtp==newOtp) {
				  System.out.print("enter the account number to transfer :");long newAccountNumber=scannerObj.nextLong();
				  System.out.println("enter the amount to transfer :");double transferAmount=scannerObj.nextDouble();
				  if(transferAmount>balance) {
						System.out.println("you have insufficient balance ");
						System.out.println("choose the amount with in the available balance ");
						enterDigit();
				  }
			     balance=balance-transferAmount;
			     System.out.println("your transfer amount is :"+transferAmount);
					System.out.println("updated balance after transfer :"+balance);
					enterDigit();
			  }
			  else
			  {
				  System.out.println("you have entered wrong otp :");
				  enterDigit();
			  }
		}
		if(Options==logout) {
			System.out.println("you are successfully logged out");
			accountNumberVerification();
		}
	}
}
public class BankProject {
	public static void main(String[] args) {
		System.out.println("Credentials verification ");
		Account a=new Account();
		a.accountNumberVerification();
		NextOptions obj1=new NextOptions();
		obj1.enterDigit();
	}
}
