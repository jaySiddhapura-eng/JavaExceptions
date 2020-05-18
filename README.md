# **Exception Handling in JAVA**

------

## What is Exception in JAVA ?

1. Unwanted or unexpected event that can occur during **RUN TIME**

2. Error != Exception [both can be thrown by a running app]
   1. **Error**: A problem/condition which app should not try to <u>catch</u>
   2. **Exception**:  A problem/condition which app might try to <u>catch</u>

## What is throwing an Exception ?

1. During exception occurrence, **Exception object** is being created<br><br>
2. Exception object holds information about: 
   1. **Name** of exception
   2. **Description** of exception
   3. **State of program** where exception occurred<br><br>
3. Runtime system searches the **Call Stack** 
   1. Call Stack: A list of methods which can handle the occurred exception
   2. The block of code in above mentioned method, which handles the exception called **Exception handler**<br><br>
4. What if runtime unable to find the suitable exception handler 
   1. **Default Exception Handler**(DEH) is being called
   2. DEH terminates the program, and print exception information.<br><br>

## How to handle an exception manually ?

1. Exception handling is managed by following 5 keywords

   1. TRY
   2. CATCH
   3. THROW
   4. THROWS
   5. FINALLY<br><br>

2. **TRY block**

   1. A program statement which can raise the exception goes into TRY block
   2. TRY block can contain more then one statement, which can produce exception<br><br>

3. **CATCH block**

   1. CATCH block catches exception which is thrown during execution of TRY block
   2. Also holds statements which can resolve/handle the exception in some rational manner
   3. There can be more then one catch blocks to accommodate multiple exception handling<br><br>

4. **THROW**

   1. THROW keyword is used to explicitly throw an exception
   2. THROW is follow by instance of an exception
   3. It is used within the method
   4. Sample:

      ~~~java
      void method(){
          throw new ArithmeticException("/ by 0");
      }
      ~~~

5. **THROWS**

   1. THROWS keyword is used to declare that method can produce **exception/exceptions**
   2. It works similar to the try and catch block
   3. Sample:

      ~~~java
      // example method declares oen type of exception
      void method1()throws ArithmeticException{  
      //statements which can produce exception
      } 
      
      // example method produces multiple type of exceptions
      void method2() throws ArithmeticException, NullPointerException{
          // statements which can produce exceptions
      }
      ~~~

6. **FINALLY**

   1. Any statement that absolutely must be executed after TRY block is put in FINALLY block<br><br>
   2. If exception occurred and did not handled properly, anything after try catch clause will not be executed and results into runtime error

      Sample:

      ~~~java
      class finalKeywordDemo{
          public void method3(){
              try{
              	int i = 10;
              	int result = i/0; // this statement will produce arithmatic exception
                  // due to wrong type of exception catching 
                  // this excption will be uncatched
              }
              catch(NullPointerException exception){
                  System.out.println("Null pointer exception caught");
                  // we are trying to catch wrong type of exception    
              }
              //following statement will not be executed
              // due to uncatched execption is generated in try/catch block
      		System.out.println("Outside try-catch clause");
          }
      }
      ~~~

      Output:

      ~~~java
      Exception in thread "main" java.lang.ArithmeticException: / by zero
      	at com.company.finalKeywordDemo.method3(finalKeywordDemo.java:7)
      	at com.company.Main.main(Main.java:7)
      ~~~

   3. If we use FINALLY block and above situation occurs, then FINALLY block will be executed regardless of uncatch exception

      Sample:

      ~~~java
      class finalKeywordDemo1{
          public void method4(){
              try{
              	int i = 10;
              	int result = i/0; // this statement will produce arithmatic exception
                  // due to wrong type of exception catching 
                  // this excption will be uncatched
              }
              catch(NullPointerException exception){
                  System.out.println("Null pointer exception caught");
                  // we are trying to catch wrong type of exception    
              }
              finally{
                  System.out.println("final statement executed");
                  // although uncatched exception generted
                  // finally block will be executed before giving runtime error   
              }
              //following statement will not be executed
              // due to uncatched execption is generated in try/catch block
      		System.out.println("Outside try-catch clause");
          }
      }
      ~~~

      Output:

      ~~~java
      final statement executed
          
      Exception in thread "main" java.lang.ArithmeticException: / by zero
      	at com.company.finalKeywordDemo1.method4(finalKeywordDemo1.java:7)
      	at com.company.Main.main(Main.java:7)
      ~~~

## Types of  Built-in exceptions

|                Types                |                         Explanation                          |
| :---------------------------------: | :----------------------------------------------------------: |
|       **ArithmeticException**       |     Exception occurred in arithmetic operation (/ by 0)      |
| **ArrayIndexOutOfBoundsException**  |          Array has been accessed with illegal index          |
|     **ClassNotFoundException**      |                  Accessing undefined class                   |
|      **FileNotFoundException**      |        Unable to find the file or file does not open         |
|           **IOException**           |         Input/output operation failed or interrupted         |
|      **InterruptedException**       | Thread is interrupted during its ongoing state [multi threading] |
|      **NoSuchFieldException**       |      Class does not contain field or variable specified      |
|      **NoSuchMethodException**      |           Accessing the method which is not found            |
|      **NullPointerException**       |                While referring to null object                |
|      **NumberFormatException**      |         Unable to convert string into numeric format         |
|        **RuntimeException**         |              Exception occurred during runtime               |
| **StringIndexOutOfBoundsException** | The index is either negative or bigger then the size of string |

## User-defined Exception

 1. User can also define the custom exceptions, to create the exception following steps should be performed

    1. Create the custom exception class by extending the Exception class

       ~~~java
       class customException extends Exception
       ~~~

    2. Implement the default constructor [User can parameterize the constructor with String] 

       ~~~java
       customException(){
       }
       
       customException(String str){
           super(str);
       }
       ~~~

    3. To raise the above implemented exception create the object of above implemented class

       ~~~java
       customException CE = new customException();
       throw CE;
       ~~~

    4. And throw the exception using **THROW** keyword

       Sample:

       ~~~java
       public class Main {
           static int accno[] = {1001, 1002, 1003, 1004};
           static String name[] = {"P1", "P2", "P3", "P4", "P5"};
           static double bal[] = {10000.00, 12000.00, 5600.0, 999.00, 1100.55};
           
           public static void main(String[] args) {
               try {
                   System.out.println("ACCNO" + "\t" + "CUSTOMER" + "\t" + "BALANCE");
                   for(int i = 0;i<5;i++){
                       System.out.println(accno[i] + "\t" + name[i] + "\t" + bal[i]);
                       
                       if(bal[i] < 1000){
                           customException CE = new customException("balance less then 1000");
                           throw CE;
                       }
                   }
               } catch (customException e){
                   e.printStackTrace();
               }
           }
       }
       ~~~

       
