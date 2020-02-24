# DePaCoG  

NOTE: I suggest reading README in IntelliJ or different markdown viewer as Bitbucket markdown is not previewing correctly via website.
  
DePaCog is a code generator implemented using an object-oriented design approach that generates the code for a number of design patterns. The user can choose from preexisting design patterns or choose to implement their own using a minimal amount of effort thanks to the flexible nature of the programs design.  
  
The project currently has the following patterns implemented in **BOTH** Java and Scala:  
  
1. AbstractFactory  
  
2. Builder  
  
3. ChainOfResponsibility  
  
4. Facade  
  
5. Factory  
  
6. Mediator  
  
7. Template  
  
8. Visitor  
  
## Getting Started  
  
These instructions will get you a copy of the project up and running on your local machine for development and testing purposes.  
  
### Prerequisites:  
  
What things you need to install the software and how to install them  
  
* [IntelliJ](https://www.jetbrains.com/idea/download/) - IDE  
* [JDK 11 or above](https://www.oracle.com/java/technologies/javase-downloads.html) - Java Development Kit  
  
### Installing:  
  
A step by step series of examples that tell you how to get a development environment up and running  
  
1. Clone the repo from the following source into a designated folder on your local machine  
	```
	git clone https://tparch3@bitbucket.org/tparch3/trevor_parchem_hw1.git
	```

2. Open up and run IntelliJ. If you're on the welcome screen click "Import Project" otherwise if you have another project open, click "File" > "New" > "Project from Existing Sources... and select the directory named:  
	```
	FirstName_LastName_HW1 
	```

 3. 'Import Project' Dialog opens and select 'Import project from external model' and select 'Gradle' then click Finish.  
3. If your IntelliJ project is not setup to use auto-import then at the bottom right of the screen an information prompt should appear saying "IntelliJ IDEA found a gradle build script" and click the option:  
	```
	Import Gradle Project 
	```
 5. Your project should be set-up once the gradle project was successfully imported which can be seen in the 'Build' toolbar section of IntelliJ.   
Refer to this following documentation if you run into any issues:  
   * [Gradle - Help by Jetbrains](https://www.jetbrains.com/help/idea/gradle.html)  
  
  
  
## Configuration:  
  
The **application configuration file** is stored under the path:  
``` 
src/main/resources/application.conf  
```  
which gives you access to be able to change the desired Template Code and Template Code Config Paths, as well as enter the desired output extension for the file you are trying to generate i.e. (.scala or .java) as well as the output directory folder where you want to store the generated files. Check the FAQ for how to switch between generating design patterns in Scala and Java  
  
The **logging configuration file** is stored under the path:   
```  
src/main/resources/logback.xml  
```  
which allows you to change the level of logging reported in stdout. By default this is set to the 'error' level to not flood the console with logging information during the execution of the program.  
  
### FAQ:  
**How do I switch between generating design patterns for Java and Scala?**  
Answer:   
Enter the configuration file and change the following parameters to  
```  
TEMPLATEDIRECTORYPATH = "src/main/resources/DesignPatternTemplates/Java/"  
TEMPLATECONFIGPATH = "src/main/resources/TemplateConfigs/Java/"  
  
OUTPUTFILEEXTENSION = ".java"  
```  
Change the TemplateDirectoryPath  & TemplateConfigPath to pull from the the Scala Folder  
```  
TEMPLATEDIRECTORYPATH = "src/main/resources/DesignPatternTemplates/Scala/"  
TEMPLATECONFIGPATH = "src/main/resources/TemplateConfigs/Scala/"  
```  
As well as change the OUTPUTFILEXTENSION to .scala  
```  
OUTPUTFILEEXTENSION = ".scala"  
```  
  
Repeat this vice versa for going between java and scala as well as any other languages you choose to implement the Templates and Configs for following the same file hierarchy.  
  
  
## Running the Program:  
  
1. Navigate to the terminal and enter the following gradle command  
	```
	 gradle clean build run --console=plain 
	```
 2. The following output will be displayed in the terminal and prompt you for which design pattern you want to generate  
	```
	Welcome to DePaCoG Design Pattern Generator!
	
	Choose from the following listed patterns to generate by
	entering their name case insensitive in the command prompt below
	Enter 'exit' command when complete to generate all files produced!
	
	Enter 'help' to see usage examples
	
	1) AbstractFactory
	2) Builder
	3) ChainOfResponsibility
	4) Facade
	5) Factory
	6) Mediator
	7) Template
	8) Visitor
	> Enter command: 
	```

3. Enter the name of the design pattern you wish to generate into stdin i.e   
'abstractfactory'. If you enter an unknown command, the program will display 'Unknown Command recognized and reprompt you to enter the name of one of the design patterns listed above  
	```
	abstractfactory
	```

 4. The program will now prompt for the name of the file you wish to generate  
	```
	Please enter the name of the file you wish to generate:
	```
	   i.e
	```
	testfactory
	```
 5. The program will generate the file you requested. You can continue to generate more design patterns or enter 'exit' to complete and allow your generated files to be saved in the path designated in the 'application.conf' which by default is "src/Output/"  
	```
	File generated at src/Output/testFactory.java
	> Enter command: 
	```
## Running the Tests:  
  
1. Navigate to the terminal and enter the following gradle command  
	```
	gradle clean test --info
	```
	 This command will run the test suite and generate an index.html output of the 9 Unit Tests in the build folder 			  at the path: 
	```
	Finished generating test html results (0.043 secs) into: C:\Users\Tcpar\IdeaProjects\Trevor_Parchem_hw1\build\reports\tests\test
	```
2. Or you can navigate to the test folder under src/test/ in the project in IntelliJ and right click 'Run Tests' to see the results of the Unit Tests in a more visually appeasing GUI format  
  
## Deployed & Assembled with:  
  
* [Gradle](https://gradle.org/) - Dependency Management  
* [JUnit](https://junit.org/junit5/) - Unit Testing Framework  
* [Logback](http://logback.qos.ch/) - Logging Framework  
* [SLF4J](http://www.slf4j.org/) - Simple Logging Facade for Logback  
* [Typesafe](https://github.com/lightbend/config) - Configuration Management Framework  
* [CommonsIO](https://commons.apache.org/proper/commons-io/) - Utility Library for File Operations  
* [Json-Simple](https://code.google.com/archive/p/json-simple/) - Library for simple JSON parsing for Code Generation  
  
# Design and Modeling Documentation:  
  
### Design Pattern Factory:  
Firstly, I designed the core of the Design Pattern Generator using the **Abstract Factory Design Pattern** to provide an interface for creating families of related or dependent objects i.e. in this case design patterns. Factory class extends AbstractDesignPatternFactory to generate objects of concrete class based on type information from the user. Using this reusable class avoids creating the objects it requires directly so that it can request the objects it requires at run-time from the factory object. This is especially important because this enables run-time flexibility via object composition to determine and generate patterns on the fly during runtime because the user may not know which design pattern to generate and it wouldn't make sense to have objects for all patterns at all time. Using this design pattern was also instrumental in the fact that it easily allows flexibility for adding more design patterns simply by implementing the interface and added to the factory class at a later date. The class can be configured with a factory object, which it uses to create objects and the factory object can be exchanged dynamically. The cons of this approach is that it requires extending the Factory interface to extend an object of the same family so in order to add another design pattern, the Factory itnerface must be extended. Another disadvantage as it adds another layer of indirection so the clients are dependent on the DesignFactory object  
  
### Code Generation:  
After designing and implementing AbstractFactory for the design patterns I began to work on the Code Generator. I decided to model the code generator using the **Template Design Pattern** which allowed me to define the generic skeleton of the algorithm for generating code and then refer the implementation to the subclasses. These steps of the Code Generator algorithm can be redefined without changing the algorithm's structure. I used an abstract class with an abstract method of generate() where each concrete CodeGenerator class will need to implement depending on the implementation, i.e JSON Template Parse or Java AST Parser for generating the code then had the Teamplate Method of the Template design pattern generateCode() that would call the abstract method generate() which is used as an API for Design Pattern Objects to generate code and output file for use in Design Pattern Factory objects.  
  
I decided on using template files in the given languages, (Java & Scala) which would have a user generated template of the Design Pattern where the Template can be as simple or complex as possible. By using a template file, the user has the most flexibility. There is no need to pass whole input parameters if the user wants the typical design pattern and in the case if they want a custom implementation they can quickly modify the template and its corresponding config without modifying any of the code. The con with this approach is it is hard to extend behavior at only specific points in the code.  
  
The template files are either in Java and Scala and use the following abstraction  
```  
class __CLASSNAME__ implements __INTERFACE__name {  
 __VARTYPE__ __VARNAME__ = __VARCONTAINS__;}  
```  
With each template is an associated JSON Object which has design pattern implementation information:  
```  
{  
 "__CLASSNAME__":"Dog", "__INTERFACENAME__":"Animal", "__VARTYPE__":"int", "__VARNAME__":"age", "__VARCONTAINS__":"3",}  
```  
The premise of the code generation algorithm is that it retrieves the template file written in Java/Scala (or easily expanded to other languages) and then parses the JSON Template Config file which holds design pattern implementation and simply replaces all instances of the key with the value in the JSON file and generates the code. This allows for the most flexibility as the user can easily generate a 10 line design pattern or a 1000 line design pattern with complex inheritance, methods, classes, and abstractions. Any modifications to the design pattern are completely **independent** of the code which is incredibly useful for generating many versions of patterns on the fly.  
  
### User Interface:  
Lastly, I designed the user interface using the **Facade Design Pattern** which serves as a user interface facade and hide the complexities and inner workings and only expose the core functionality i.e. generating a design pattern to the client while not exposing its inner workings. The UIFacade interface contains one method start() which starts the program event loop. The UIFacade is implemented by the UserInterface class which holds private concrete objects of the AbstractDesignPatternFactory as well as the CodeGenerator classes that allow delegation of user calls to these classes with a default constructor that instantiates those objects automatically. The only public method available to the user is the start() method which creates a scanner, displays the instructions to the user on how to work the program and the input is handled via a switch case that if a design pattern in the application.conf list of design patterns is inputted, it prompts the user of the name of the file they wish to generate and calls the generateDesignPattern() method in the facade that uses the Abstract Factory to generate design patterns. By using the JSON Template Code Generator parser, the user doesn't have to enter complex user calls for each method and class and variable for their design patterns. This flexibility allows for them to generate the same template many times or easily modify on the fly without changing the codebase of Design Patterns already implemented.   
  
### Conclusion:  
Overall this design made adding Design Patterns and modifying them incredibly simple and made the program really use to use. The modification of already implemented Design Patterns can be done without changes to the codebase. Adding more language support is as easy as generating a Template file in the given language as well as the corresponding JSON Config for that template. Adding a new design pattern would be as simple as adding a new class that implements the interface for the AbstractFactory without touching any of CodeGeneration and UserInterface logic and updating the application.conf list of Design Patterns. In the case of adding a new code generation technique such as Java AST parser, it would be as simple as adding a new implementation by subclassing the Template Algorithm for code generation and passing that object around. The overall experience was really enjoyable and I felt like I have learnt a lot in such a short amount of time about the coupling/decoupling of abstractions and how to model them depending on different needs.
