import java .io.*;

import java.io.BufferedReader;

public class CRC {

    public static void main(String[] args) throws IOException {

        BufferedReader br = new BufferedReader(new InputStreamReader(System.in));

          System.out.println("Enter Generator:");

          String gen = br.readLine();

          System.out.println("Enter Data:");

          String data = br.readLine();

          String code = data;

          while(code.length() < (data.length() + gen.length() - 1))

           code = code + "0";

          code = data + div(code,gen);

          System.out.println("The transmitted Code Word is: " + code);

          System.out.println("Please enter the received Code Word: ");

          String rec = br.readLine();

          if(Integer.parseInt(div(rec,gen)) == 0)

           System.out.println("The received code word contains no errors.");

          else

           System.out.println("The received code word contains errors.");

         }

         static String div(String num1,String num2)

         {

          int pointer = num2.length();

          String result = num1.substring(0, pointer);

          String remainder = "";

          for(int i = 0; i < num2.length(); i++)

          {

           if(result.charAt(i) == num2.charAt(i))

            remainder += "0";

           else

            remainder += "1";

          }

          while(pointer < num1.length())

          {

           if(remainder.charAt(0) == '0')

           {

            remainder = remainder.substring(1, remainder.length());

            remainder = remainder + String.valueOf(num1.charAt(pointer));

            pointer++;

           }

           result = remainder;

           remainder = "";

           for(int i = 0; i < num2.length(); i++)

           {

            if(result.charAt(i) == num2.charAt(i))

             remainder += "0";

            else

             remainder += "1";

           }

          }

          return remainder.substring(1,remainder.length());

    }

}
___&&&&&&&&&--66667778888888

import java.net.*;
import java.io.*;
public class Client
{
    public static void main( String args[]) throws Exception
    {
        Socket cs = new Socket("localhost",1234);
    BufferedReader kb = new BufferedReader(new InputStreamReader(System.in));
    BufferedReader br = new BufferedReader(new InputStreamReader(cs.getInputStream()));
    DataOutputStream dos = new DataOutputStream(cs.getOutputStream());
 
    System.out.println(" Enter text..");
    System.out.println(" if client 'quit' type  exit");
      
    String s1,s4=null; 
    while(!(s1=kb.readLine()).equals("exit"))
    {
        //System.out.println(" data  send to server machine");
         dos.writeBytes(s1+"\n");
        
        s4 = br.readLine();
        //System.out.println(" data  receive from  server machine");
        System.out.println("Server said : "+s4);
        System.out.println("Enter text ");
        
    }
System.out.println("Terminated..");
        cs.close(); 
        dos.close();
        kb.close();
    }
}
__________&&&&&&&&&55666677777
import java.net.*;

import java.io.*;

public class Server

{

    public static void main( String args[]) throws Exception

    {

        ServerSocket srs = new ServerSocket(1234);

        System.out.println("Server is running...");

        Socket ss=srs.accept();

        System.out.println("connection establised");

BufferedReader kb = new BufferedReader(new InputStreamReader(System.in));

BufferedReader br = new BufferedReader(new InputStreamReader(ss.getInputStream()));

DataOutputStream dos = new DataOutputStream(ss.getOutputStream());

 

 while(true)

 {

  //System.out.println("server repeat as long as client not send null");

  String s2,s3; 

  while((s2=br.readLine())!=null)

  {

     System.out.println("Client said : "+s2);

     System.out.println("Enter text ");

    s3 = kb.readLine();

//System.out.println("Answer send to client machine");

     dos.writeBytes(s3+"\n");

  }

  System.out.println("Terminated..");

  ss.close(); 

  srs.close();

  dos.close();

  kb.close();

  System.exit(0);

  }

 }

}




