# OOP questions

## Software design

### Error handling

#### What does 'fail fast' mean in terms of exception handling? Why is it a good practice?

In object-oriented programming, a fail-fast-designed object initializes the internal state of the object in 
the constructor, launching an exception if something is wrong (vs allowing non-initialized or partially 
initialized objects that will fail later due to a wrong "setter").

The fail fast principle stands for stopping the current operation as soon as any unexpected error occurs. 
Adhering to this principle generally results in a more stable solution.

In most cases, adhering to the fail fast principle means we should shut down the application (probably, 
with a polite apology) in case of any unexpected situation.

There are cases where we don’t have to kill the whole process, though. If the software is inherently stateless 
meaning that it doesn’t store any state in memory between the operations, it might be just fine to halt only 
the operation the error took place in and let the application continue working.

An example here is a web server. Requests it processes don’t leave any marks in the server’s memory so we 
don’t have to shut it down. Another good example would be a background job.
https://enterprisecraftsmanship.com/posts/fail-fast-principle/


## Computer Science

### Data structures

#### How to find the middle element of singly linked list in O(n)?

Method 1:
Traverse the whole linked list and count the no. of nodes. Now traverse the list again till count/2 and 
return the node at count/2.  
Method 2:
Traverse linked list using two pointers. Move one pointer by one and other pointer by two. When the fast 
pointer reaches end slow pointer will reach middle of the linked list.  
https://www.geeksforgeeks.org/write-a-c-function-to-print-the-middle-of-the-linked-list/

#### Given an array of integers going from 1 to 100 (both inclusive) there is a duplicated entry. How to find it?

Traverse the array and place the numbers as keys and the +1 as values in a HashMap. We can have try/catch 
block to test the keys:  

        HashMap<Integer, Integer> db = new HashMap<Integer, Integer>();
        for (int i=1; i<=100; I++) {
            try {
                System.out.println(“The duplicate is: “ + i);
                Break;
            }
            catch (Exception e) {
            }
            db.put(i, 1);
        }

#### What is a linked list? How to find if a linked list has a loop?

Linked List are linear data structures where the elements are not stored in contiguous locations and 
every element is a separate object with a data part and address part. The elements are linked using 
pointers and addresses. Each element is known as a node. Due to the dynamicity and ease of insertions 
and deletions, they are preferred over the arrays. It also has few disadvantages like the nodes cannot 
be accessed directly instead we need to start from the head and follow through the link to reach to a 
node we wish to access.

https://stackoverflow.com/questions/2663115/how-to-detect-a-loop-in-a-linked-list

        boolean hasLoop(Node first) {
            Node slow = first;
            Node fast = first;
        
            while(fast != null && fast.next != null) {
                slow = slow.next;          // 1 hop
                fast = fast.next.next;     // 2 hops 
        
                if(slow == fast)  // fast caught up to slow, so there is a loop
                    return true;
            }
            return false;  // fast reached null, so the list terminates
        }

#### What is the Big O time complexity of the common operations in an ArrayList, LinkedList, HashMap? And of a bubble sort, quicksort, finding items in a Binary Search tree?

https://www.baeldung.com/java-collections-complexity

ArrayList  
The ArrayList in Java is backed by an array. This helps to understand the internal logic of its 
implementation. A more comprehensive guide for the ArrayList is available in this article.

So, let's first focus on the time complexity of the common operations, at a high level:

add() – takes O(1) time  
add(index, element) – in average runs in O(n) time  
get() – is always a constant time O(1) operation  
remove() – runs in linear O(n) time. We have to iterate the entire array to find the element qualifying 
for removal  
indexOf() – also runs in linear time. It iterates through the internal array and checking each element 
one by one. So the time complexity for this operation always requires O(n) time  
contains() – implementation is based on indexOf(). So it will also run in O(n) time  

LinkedList  
LinkedList is a linear data structure which consists of nodes holding a data field and a reference to another node. For more LinkedList features and capabilities, have a look at this article here.

Let's present the average estimate of the time we need to perform some basic operations:

add() – supports O(1) constant-time insertion at any position  
get() – searching for an element takes O(n) time  
remove() – removing an element also takes O(1) operation, as we provide the position of the element  
contains() – also has O(n) time complexity  

https://www.quora.com/What-is-the-Big-O-for-operations-in-a-Hashmap

Java 8 has a HashMap which degrades into a tree for collisions.

This means it is O(1) typically and O(log N) in the worst case.

> why does the contains() key function take O(N) in best and worst case.

This happens if all the keys are mapped to the same bucket in the hash map and you have an implementation 
which is a linked list to handle collisions (as Java 1 to 7 did)

https://www.bigocheatsheet.com/

Bubble Sort = best Ω(n) worst Θ(n^2)	  
Quicksort = best Θ(n log(n)) worst O(n^2)  
Search Binary Search Tree = O(n)

#### How does HashMap work?

HashMap in Java works on hashing principle. It is a data structure which allows us to store object and 
retrieve it in constant time O(1) provided we know the key. In hashing, hash functions are used to link 
key and value in HashMap. Objects are stored by calling put(key, value) method of HashMap and retrieved 
by calling get(key) method. When we call put method, hashcode() method of the key object is called so 
that hash function of the map can find a bucket location to store value object, which is actually an 
index of the internal array, known as the table. HashMap internally stores mapping in the form of Map. 
Entry object which contains both key and value object. When you want to retrieve the object, you call 
the get() method and again pass the key object. This time again key object generate same hash code 
(it's mandatory for it to do so to retrieve the object and that's why HashMap keys are immutable e.g. 
String) and we end up at same bucket location. If there is only one object then it is returned and 
that's your value object which you have stored earlier. Things get little tricky when collisions occur.

#### Why is it important for keys in a map to have an immutable type? (Consider String for example.)

HashMap works on the principle of hashing, we have put(key, value) and get(key) method for storing and 
retrieving Objects from HashMap. When we pass Key and Value object  to put() method on Java HashMap, 
HashMap implementation calls hashCode method on Key object and applies returned hashcode into its own 
hashing function to find a bucket location for storing Entry object, important point to mention is 
that HashMap in Java stores both key and value object as Map.Entry in a bucket which is essential to 
understand the retrieving logic. 

key object generate same hash code (it's mandatory for it to do so to retrieve the object and that's 
why HashMap keys are immutable e.g. String

https://javarevisited.blogspot.com/2011/02/how-hashmap-works-in-java.html

### Other

#### What is a garbage collector, in a nutshell?

https://www.baeldung.com/jvm-garbage-collectors

In simple words, GC works in two simple steps known as Mark and Sweep:

Mark – it is where the garbage collector identifies which pieces of memory are in use and which are not
Sweep – this step removes objects identified during the “mark” phase  

Advantages:

No manual memory allocation/deallocation handling because unused memory space is automatically handled by GC
No overhead of handling Dangling Pointer
Automatic Memory Leak management (GC on its own can't guarantee the full proof solution to memory leaking, 
however, it takes care of a good portion of it)

## Programming paradigms

### Procedural

#### What is casting? What is the difference between up vs downcasting?

Casting is the process of making a variable behave as a variable of another type. If a class shares an 
IS-A or inheritance relationship with another class or interface, their variables can be cast to each 
other's type. 

Upcasting is casting to a supertype, while downcasting is casting to a subtype. Upcasting is always 
allowed, but downcasting involves a type check and can throw a ClassCastException

#### Which order should we catch the exceptions? Why?

When catching exceptions you want to always catch the most specific first and then the most generic 
(as RuntimeException or Exception). For instance, imagine you would like to catch the 
StringIndexOutOfBoundsException thrown by the String.charAt(index) method but your code could also 
throw a NullPointerException, here's how you could go to catch the exceptions:

        String s = null;
        try {
          s.charAt(10);
        } catch ( NullPointerExeption e ) {
          System.out.println("null");
          e.printStackTrace();
        } catch ( StringIndexOutOfBoundsException e ) {
          System.out.println("String index error!");
          e.printStackTrace();
        } catch ( RuntimeException e ) {
          System.out.println("runtime exception!");
          e.printStackTrace();
        }

So, with this order, I am making sure the exceptions are caught correctly and they are not tripping over 
one another, if it's a NullPointerException it enters the first catch, if a StringIndexOutOfBoundsException 
it enters the second and finally if it is something else that is a RuntimeException (or inherits from it, 
like a IllegalArgumentException) it enters the third catch.

### Object-oriented

#### What is a class?

A class is a user defined blueprint or prototype from which objects are created. It represents the set 
of properties or methods that are common to all objects of one type. 

#### What is an object?

It is a basic unit of Object Oriented Programming and represents real life entities. A typical Java program 
creates many objects, which interact by invoking methods.

#### What is a constructor?

A Java constructor is special method that is called when an object is instantiated. In other words, when 
you use the new keyword. The purpose of a Java constructor is to initializes the newly created object 
before it is used. 

#### Do we require parameter for constructors?

No but it is possible for a Java constructor to take parameters. These parameters can then be used to 
initialize the internal state (fields) of the newly created object.

#### What is an interface?

An interface is a reference type in Java. It is similar to class. It is a collection of abstract methods. 
A class implements an interface, thereby inheriting the abstract methods of the interface.

#### What are access modifiers?

A Java access modifier (public, private, package, protected) specifies which classes can access a given 
class and its fields, constructors and methods. Access modifiers can be specified separately for a 
class, its constructors, fields and methods.

#### What is data hiding?

Data hiding is a software development technique specifically used in object-oriented programming (OOP) 
to hide internal object details (data members). Data hiding ensures exclusive data access to class members 
and protects object integrity by preventing unintended or intended changes.

#### Can a static method use non-static members?

Yes, via reference. there is a legitimate way to access any non-static member from the static context in 
Java by creating instances. You need to first create an object of the class whose non-static members or 
non-static method you want to access.

        public class Hello {
        
          private static int aStaticVariable = 1;
          private int aNonStaticVariable = 2;
        
          private static void aStaticMethod() {
            Hello object = new Hello();
            System.out.println(object.aNonStaticVariable);
            object.aNonStaticMethod();
          }
        
          private void aNonStaticMethod() {
            System.out.println(aStaticVariable);
          }
        
        }

#### What is the difference between hiding a static method and overriding an instance method?

The distinction between hiding and overriding has important implications. The version of the overridden 
method that gets invoked is the one in the subclass. The version of the hidden method that gets invoked 
depends on whether it is invoked from the superclass or the subclass. (they can have different algorithms 
for example)

When overriding a method, you might want to use the @Override annotation that instructs the compiler that 
you intend to override a method in the superclass. If, for some reason, the compiler detects that the 
method does not exist in one of the superclasses, it will generate an error.

If a subclass defines a class method with the same signature as a class method in the superclass, the 
method in the subclass hides the one in the superclass.

#### Define the following terms: Instantiation, Attribute, Method

Instantiate in Java means to call a constructor of a Class which creates an instance or object, of the 
type of that Class. Instantiation allocates the initial memory for the object and returns a reference.

An attribute is another term for a field. It's typically a public constant or a public variable that 
can be accessed directly.

A method is a collection of statements that perform some specific task and return the result to the 
caller. A method can perform some specific task without returning anything. Methods allow us to reuse 
the code without retyping the code. They are similar to functions in other languages.

#### Could we access a static variable (or method) from a non-static method? Why?

Yes, a non-static method can access a static variable or call a static method in Java. There is no 
problem with that because of static members i.e. both static variable and static methods belongs to 
a class and can be called from anywhere, depending upon their access modifier. For example, if a 
static variable is private then it can only be accessed from the class itself, but you can access 
a public static variable from anywhere. 

#### Could we access a non-static variable (or method) from a static method? Why?

You cannot access a non-static variable from a static method without an instance, because the variable 
doesn’t exist without the object/instance.

#### How many instances you have of a static variable of a given class?

There is only one instance of each static variable, and it is shared among all the objects of that class. 
Different objects cannot have different values for a static variable.

#### Why is it not a good practice to write a lot of static methods?

Creating static methods that take an instance is bad practice because any method that takes an instance 
should probably be an instance method. A better OO design would have everything being an object and all 
functions be instance methods. 

#### What are the features of static attributes and static methods of a class? What are the benefits, when to use them?

Essentially, static methods let you write procedural code in an object oriented language. It lets you call 
methods without having to create an object first. The only time you want to use a static method in a class 
is when a given method does not require an instance of a class to be created.

Benefit: can be used without the need to create an object

#### What is the ‘this’ reference?

The this is a keyword in Java which is used as a reference to the object of the current class, with in an 
instance method or a constructor. Using this you can refer the members of a class such as constructors, 
variables and methods.

#### What are base class, subclass and superclass?

In an OOP language, the base class is a class from which other classes are derived from. ... General the 
class that is derived from another class is called a subclass. The class from which it's derived is called 
the superclass. So the subclass is "under" the superclass.

#### Draw an object oriented family (as entities, with relations) on the whiteboard.

https://en.wikipedia.org/wiki/Class_diagram

![alt text](/docs/oop_img/UML_Class.jpg?raw=true)

#### Difference between overloading and overriding?

Overloading - same method name, multiple times, but with a different signature (parameters, parameter order)

Overriding - same signature, only once, different content than the superclass

#### What are the Object Oriented Principles? Explain the concepts with realistic examples!

https://medium.com/@cancerian0684/what-are-four-basic-principles-of-object-oriented-programming-645af8b43727

Encapsulation   
Encapsulation is the mechanism of hiding of data implementation by restricting access to public methods. 
Instance variables are kept private and accessor methods are made public to achieve this.

        private name = “John Smith”;

Data Abstraction  
Abstract means a concept or an Idea which is not associated with any particular instance. Using abstract 
class/Interface we express the intent of the class rather than the actual implementation. In a way, one 
class should not know the inner details of another in order to use it, just knowing the interfaces should 
be good enough.
        
        Interface Calculator {
            add(int x, int y);
        }


Polymorphism  
It means one name many forms. It is further of two types — static and dynamic. Static polymorphism is 
achieved using method overloading and dynamic polymorphism using method overriding. It is closely related 
to inheritance. We can write a code that works on the superclass, and it will work with any subclass type 
as well.

Inheritance  
Inheritances expresses “is-a” and/or “has-a” relationship between two objects. Using Inheritance, In 
derived classes we can reuse the code of existing super classes. In Java, concept of “is-a” is based on 
class inheritance (using extends) or interface implementation (using implements).
For example, FileInputStream "is-a" InputStream that reads from a file.

#### What is method overloading?

Method Overloading is a feature that allows a class to have more than one method having the same name, 
if their argument lists are different. It is similar to constructor overloading in Java, that allows a 
class to have more than one constructor having different argument lists.

#### What is method overriding?

If subclass (child class) has the same method as declared in the parent class, it is known as method 
overriding in Java. In other words, If a subclass provides the specific implementation of the method 
that has been declared by one of its parent class, it is known as method overriding.

#### Explain how object oriented languages attempt to simplify memory management for Programmers.

These environments invest a lot in the management and protection of system resources, including memory. 
C++ relies on programmers to deallocate memory in destructors, whereas Java and .NET use garbage 
collection.

#### Explain the “Single Responsibility” principle!

The single-responsibility principle (SRP) is a computer-programming principle that states that every 
module or class should have responsibility over a single part of the functionality provided by the 
software, and that responsibility should be entirely encapsulated by the class, module or function.

#### What is an object oriented program? Explain, show.

Object-oriented programming (OOP) is a programming paradigm based on the concept of "objects", which can 
contain data, in the form of fields (often known as attributes or properties), and code, in the form of 
procedures (often known as methods). A feature of objects is an object's procedures that can access and 
often modify the data fields of the object with which they are associated (objects have a notion of 
"this" or "self"). In OOP, computer programs are designed by making them out of objects that interact 
with one another.

        Human person1 = new Human(John); // behind the scenes the constructor sets the name
        person1.getName(); // will return John 

#### How do you make a class immutable? What do you need to watch out for?

Make your class final, so that no other classes can extend it.

Make all your fields final, so that they’re initialized only once inside the constructor and never modified 
afterward.  
Don’t expose setter methods.  
When exposing methods which modify the state of the class, you must always return a new instance of the class.  
If the class holds a mutable object:  
Inside the constructor, make sure to use a clone copy of the passed argument and never set your mutable 
field to the real instance passed through constructor, this is to prevent the clients who pass the object 
from modifying it afterwards. Make sure to always return a clone copy of the field and never return the real object instance.

        package com.programmer.gate.beans;
        public final class ImmutableStudent {
            private final int id;
            private final String name;
            public ImmutableStudent(int id, String name) {
                this.name = name;
                this.id = id;
            }
            public int getId() {
                return id;
            }
            public String getName() {
                return name;
            }
        }

#### How many instances can be created for an abstract class?

None. You can create instance of all other classes extending that abstract class. Because it's abstract and 
an object is concrete. An abstract class is sort of like a template, or an empty/partially empty structure, 
you have to extend it and build on it before you can use it.

## Programming languages



### Java

#### What is autoboxing and unboxing?

Autoboxing is the automatic conversion that the Java compiler makes between the primitive types and their 
corresponding object wrapper classes. For example, converting an int to an Integer, a double to a Double, 
and so on. If the conversion goes the other way, this is called unboxing.

#### If you have a variable, that shall store a positive whole number between 0 and 200, what primitive type would you use to store it?

Short or int

#### What is the "golden rule" of variable scoping in Java? What is the lifetime of variables?

The golden rule is that static code cannot access non-static members by their simple names. Static code is 
not executed in the context of an object, therefore the references this and super are not available.

Instance Variables  
A variable which is declared inside a class and outside all the methods and blocks is an instance variable. 
The general scope of an instance variable is throughout the class except in static methods. The lifetime of 
an instance variable is until the object stays in memory.
Class Variables  
A variable which is declared inside a class, outside all the blocks and is marked static is known as a class
 variable. The general scope of a class variable is throughout the class and the lifetime of a class variable 
 is until the end of the program or as long as the class is loaded in memory.
Local Variables  
All other variables which are not instance and class variables are treated as local variables including 
the parameters in a method. Scope of a local variable is within the block in which it is declared and the 
lifetime of a local variable is until the control leaves the block in which it is declared.

#### What is the purpose of the ‘equals()’ method?

The equals() method compares two objects for equality and returns true if they are equal. The equals() 
method provided in the Object class uses the identity operator ( == ) to determine whether two objects 
are equal. For primitive data types, this gives the correct result. For objects, however, it does not.

Main difference between .equals() method and == operator is that one is method and other is operator.
We can use == operators for reference comparison (address comparison) and .equals() method for content 
comparison. In simple words, == checks if both objects point to the same memory location whereas .equals() 
evaluates to the comparison of values in the objects.
If a class does not override the equals method, then by default it uses equals(Object o) method of the 
closest parent class that has overridden this method.

The java string equals() method compares the two given strings based on the content of the string. If 
any character is not matched, it returns false. If all characters are matched, it returns true.

The String equals() method overrides the equals() method of Object class.

#### What is the difference between '==' and 'equals()'?

Main difference between .equals() method and == operator is that one is method and other is operator.
We can use == operators for reference comparison (address comparison) and .equals() method for content 
comparison. In simple words, == checks if both objects point to the same memory location whereas .equals() 
evaluates to the comparison of values in the objects.

#### What does the ‘static’ keyword mean?

The static keyword in Java means that the variable or function is shared between all instances of that 
class as it belongs to the type, not the actual objects themselves. So if you have a variable: private 
static int i = 0; and you increment it ( i++ ) in one instance, the change will be reflected in all 
instances.

#### Why is the main() method declared as static? Explain.

Java main() method is always static, so that the compiler can call it without the creation of an object 
or before the creation of an object of the class. ... The main() method in Java must be declared public, 
static and void. If any of these are missing, the Java program will compile but a runtime error will be 
thrown.

#### What is the default access modifier in a class?

The data members, class or methods which are not declared using any access modifiers i.e. having default 
access modifier are accessible only within the same package.

#### What is the JVM?

A Java virtual machine (JVM) is a virtual machine that enables a computer to run Java programs as well as 
programs written in other languages that are also compiled to Java bytecode. The JVM is detailed by a 
specification that formally describes what is required in a JVM implementation. Having a specification 
ensures interoperability of Java programs across different implementations so that program authors using 
the Java Development Kit (JDK) need not worry about idiosyncrasies of the underlying hardware platform.

#### What is the difference between the JRE and the JDK?

JAVA DEVELOPMENT KIT  
The Java Development Kit (JDK) is a software development environment used for developing Java applications 
and applets. It includes the Java Runtime Environment (JRE), an interpreter/loader (Java), a compiler 
(javac), an archiver (jar), a documentation generator (Javadoc) and other tools needed in Java development.  

JAVA RUNTIME ENVIRONMENT
JRE stands for “Java Runtime Environment” and may also be written as “Java RTE.” The Java Runtime Environment 
provides the minimum requirements for executing a Java application; it consists of the Java Virtual Machine 
(JVM), core classes, and supporting files.  

JAVA VIRTUAL MACHINE  
It is a specification where working of Java Virtual Machine is specified. But implementation provider is 
independent to choose the algorithm. Its implementation has been provided by Sun and other companies.
An implementation is a computer program that meets the requirements of the JVM specification
Runtime Instance Whenever you write java command on the command prompt to run the java class, an instance 
of JVM is created.  

Difference betweem JDK, JRE and JVM  

JDK – Java Development Kit (in short JDK) is a Kit which provides the environment to develop and 
execute(run) the Java program. JDK is a kit(or package) which includes two things
Development Tools(to provide an environment to develop your java programs) and JRE (to execute your 
java program).  
Note : JDK is only used by Java Developers.  

JRE – Java Runtime Environment (to say JRE) is an installation package which provides environment to 
only run(not develop) the java program(or application)onto your machine. JRE is only used by them who 
only wants to run the Java Programs i.e. end users of your system.  

JVM – Java Virtual machine(JVM) is a very important part of both JDK and JRE because it is contained 
or inbuilt in both. Whatever Java program you run using JRE or JDK goes into JVM and JVM is responsible 
for executing the java program line by line hence it is also known as interpreter.

#### What is the difference between long and Long?

It also applies to Float to float, Integer to integer etc. long is a primitive type, while Long is a 
Java class (and so it will inherit Object)

#### Can a long store bigger numbers than a Long?

No. 2 to the 63rd pow -1 represented in 64 bits

#### What kind of packages do you know under java.util.* ? Bring at least 3 examples.

Date
HashMap
Arrays
ArrayList

#### What are the access modifiers in Java? Which one could we use for class?

private, public, protected and default(package)

Classes can only have 2 modifiers:  
public  
no modifier (default modifier)

#### Can an “enum” contain methods in Java? Explain.

Yes. https://docs.oracle.com/javase/tutorial/java/javaOO/enum.html

Java programming language enum types are much more powerful than their counterparts in other languages. 
The enum declaration defines a class (called an enum type). The enum class body can include methods and 
other fields. The compiler automatically adds some special methods when it creates an enum. For example, 
they have a static values method that returns an array containing all of the values of the enum in the 
order they are declared. This method is commonly used in combination with the for-each construct to 
iterate over the values of an enum type.

Each enum constant is declared with values for the mass and radius parameters. These values are passed 
to the constructor when the constant is created. Java requires that the constants be defined first, prior 
to any fields or methods. Also, when there are fields and methods, the list of enum constants must end 
with a semicolon.

Note: The constructor for an enum type must be package-private or private access. It automatically creates 
the constants that are defined at the beginning of the enum body. You cannot invoke an enum constructor 
yourself.
In addition to its properties and constructor, Planet has methods that allow you to retrieve the surface 
gravity and weight of an object on each planet. Here is a sample program that takes your weight on earth 
(in any unit) and calculates and prints your weight on all of the planets (in the same unit):

#### When would you use a private/protected/public attribute? What is the difference?

When you want to control the access to fields and methods from other parts of the program. Private - 
only that class has access, nothing else.

#### How do you prevent developers from subclassing a class?

To prevent inheritance, use the keyword "final" when creating the class. Or Abstract Class.

#### How do you prevent developers from overriding a method in a subclass?

Apart from final methods there are two more techniques which you can use to prevent a method from being 
overridden in Java. If you are familiar with private and static modifier in Java, then you may be knowing 
that private method is not accessible in subclass, which means they can not be overridden as well, because 
overriding happens at child class. Similarly, static methods can not be overridden in Java, because they 
are resolved and bonded during compile time, while overriding takes place at runtime. 

#### How do you prevent developers from changing the value of a variable?

Mark it as final.

#### Think about money ;) How would you store a currency value, that shall support decimal parts? Think it through again, and try to think outside of the box!

Java has Currency class that represents the ISO 4217 currency codes. BigDecimal is the best type for 
representing currency decimal values.
BigDecimal because of the  the loss of precision (or loss of significance).

All floating point values that can represent a currency amount (in dollars and cents) cannot be stored 
exactly as it is in the memory. So, if we want to store 0.1 dollars (10 cents), float/double can not store 
it as it is. Instead, the binary can store only a closer approximation value (0.100000001490116119384765625 
in decimal). The magnitude of this problem becomes significant (known as loss of significance) when we 
repetitively do arithmetic operations (multiply or divide) using these two data types. Below, we will 
demonstrate what this may look like.

Here is an example of the loss of precision using double:

        public class DoubleForCurrency {
            public static void main(String[] args) {
                double total = 0.2;
                for (int i = 0; i < 100; i++) {
                    total += 0.2;
                }
                System.out.println("total = " + total);
            }
        }
        
        Program output:
        
        total = 20.19999999999996

#### What happens if you try to call something, that you have no access to, because of data hiding?

An error is detected at compile time - it indicates the private access of the “something”.

#### What happens if you try to delete/drop an item from an array, while you are iterating over it?

An error is detected at compile time - it indicates the private access of the “something”.

#### What happens if you try to delete/drop/add an item from a List, while you are iterating over it?

You can’t delete/drop an item from an array. You either loop through it and form another array or use 
streams to form another array, without the target item.

#### What happens if you try to add an item to the end of an array, while you are iterating over it?

List length = 120
Exception in thread "main" java.lang.IndexOutOfBoundsException: Index 119 out of bounds for length 119

#### If you need to access the iterator variable after a for loop, how would you do it?

List length = 120
Exception in thread "main" java.lang.IndexOutOfBoundsException: Index 121 out of bounds for length 121

#### Which interfaces extend the Collection interface in Java. Which classes?

Create, initialize and all the steps needed in the access. The for loop is a block of code and the 
iterator variable is local to that block. 

https://stackoverflow.com/questions/477550/is-there-a-way-to-access-an-iteration-counter-in-javas-for-each-loop

No, but you can provide your own counter.

The reason for this is that the for-each loop internally does not have a counter; it is based on the 
Iterable interface, i.e. it uses an Iterator to loop through the "collection" - which may not be a 
collection at all, and may in fact be something not at all based on indexes (such as a linked list).

#### What is the connection between equals() and hashCode()? How are they used in HashMap?

https://docs.oracle.com/javase/8/docs/api/java/util/Collection.html

All Known Subinterfaces:  
BeanContext, BeanContextServices, BlockingDeque<E>, BlockingQueue<E>, Deque<E>, List<E>, NavigableSet<E>, 
Queue<E>, Set<E>, SortedSet<E>, TransferQueue<E>

All Known Implementing Classes:  
AbstractCollection, AbstractList, AbstractQueue, AbstractSequentialList, AbstractSet, ArrayBlockingQueue, 
ArrayDeque, ArrayList, AttributeList, BeanContextServicesSupport, BeanContextSupport, 
ConcurrentHashMap.KeySetView, ConcurrentLinkedDeque, ConcurrentLinkedQueue, ConcurrentSkipListSet, 
CopyOnWriteArrayList, CopyOnWriteArraySet, DelayQueue, EnumSet, HashSet, JobStateReasons, 
LinkedBlockingDeque, LinkedBlockingQueue, LinkedHashSet, LinkedList, LinkedTransferQueue, 
PriorityBlockingQueue, PriorityQueue, RoleList, RoleUnresolvedList, Stack, SynchronousQueue, TreeSet, 
Vector


#### What is the connection between equals() and hashCode()? How are they used in HashMap?

In HashMap, hashCode() is used to calculate the bucket and therefore calculate the index. equals 
method is used to check that 2 objects are equal or not. 

#### What is the difference between checked exceptions and unchecked exceptions? Could you bring example for each?

The biggest difference between checked and unchecked exceptions is that checked exceptions are forced 
by compiler and used to indicate exceptional conditions that are out of the control of the program (for 
example, I/O errors), while unchecked exceptions are occurred during runtime and used to indicate 
programming errors (for example, a null pointer).

Checked Exception Example

FileNotFoundException is a checked exception in Java. Anytime, we want to read a file from filesystem, 
Java forces us to handle error situation where file may not be present in place.

        public static void main(String[] args)
        {
            FileReader file = new FileReader("somefile.txt");
        }

In above case, you will get compile time error with message – Unhandled exception type FileNotFoundException.
To make program able to compile, you must handle this error situation in try-catch block. Below given code 
will compile absolutely fine.

        public static void main(String[] args)
        {
            try
            {
                FileReader file = new FileReader("somefile.txt");
            }
            catch (FileNotFoundException e)
            {
                //Alternate logic
                e.printStackTrace();
            }
        }

Unchecked Exception Example

Checkout the given code below. Above code does not give any compile time error. But when you the example, 
it throws NullPointerException. NullPointerException is unchecked exception in Java.
        
        public static void main(String[] args)
        {
            try
            {
                FileReader file = new FileReader("pom.xml");
                 
                file = null;
                 
                file.read();
            }
            catch (IOException e)
            {
                //Alternate logic
                e.printStackTrace();
            }
        }

#### What is Error in Java and how does it relate to Exception?

An Error "indicates serious problems that a reasonable application should not try to catch." An 
Exception "indicates conditions that a reasonable application might want to catch." Error along 
with RuntimeException & their subclasses are unchecked exceptions. All other Exception classes are 
checked exceptions.

#### When does 'finally' block run? What it is used for? Could you give an example from your projects when you would use 'finally'?

Finally runs after the try and catch blocks, regardless if the catch was activated.
It is used to make sure an action happens regardless of the result the initial code is trying to get.
In a database connection for example, whether the query is successful or not, the finally block will close the connection.
        
        try {
            conn = getConnection();
            stmt = conn.createStatement();

            // DB QUERY AND LOGIC
            
            rs.close();
            stmt.close();
            conn.close();
        }
        catch(SQLException se) {
            se.printStackTrace();
        }
        catch(Exception e){
            e.printStackTrace();
        }
        finally {
            try{
                if(stmt!=null)
                    stmt.close();
            }catch(SQLException se2){
            }
            try{
                if(conn!=null)
                    conn.close();
            }catch(SQLException se){
                se.printStackTrace();
            }
        }
        
        
#### What is the largest number you can work with in Java?

https://docs.oracle.com/javase/6/docs/api/constant-values.html#java.lang.Integer.MAX_VALUE
java.lang.Long
9223372036854775807L

#### When you use method overriding, can you change the access level of the method, from protected to public? Why?When you use method overriding, can you change the access level of the method, from public to protected? Why?

An overridden method can have a different access modifier but it cannot lower the access scope. 
Methods declared public in a superclass also must be public in all subclasses. Methods declared 
protected in a superclass must either be protected or public in subclasses; they cannot be private.

#### Can the main method be overridden? Explain your answer!

You cannot override a static method in Java because method overriding is based upon dynamic binding at 
runtime and static methods are bonded using static binding at compile time. Main is a static method.

#### When you use method overriding, can you throw fewer exceptions in the subclass than in the parent class? Why?

The overriding method must NOT throw checked exceptions that are new or broader than those declared by 
the overridden method. For example, a method that declares a FileNotFoundException cannot be overridden 
by a method that declares a SQLException, Exception, or any other non-runtime exception unless it's a 
subclass of FileNotFoundException.

The rule that you need to be able to refer to objects by their superclass is the Liskov Substitution 
Principle.

Since unchecked exceptions can be thrown anywhere then they are not subject to this rule. You can add 
an unchecked exception to the throws clause as a form of documentation if you want, but the compiler 
doesn't enforce anything about it.

The overriding method CAN throw any unchecked (runtime) exception, regardless of whether the overridden 
method declares the exception

https://stackoverflow.com/questions/5875414/why-cant-overriding-methods-throw-exceptions-broader-than-the-overridden-method

#### When you use method overriding, can you throw more exceptions in the subclass than in the parent class? Why?

The overriding method CAN throw any unchecked (runtime) exception, regardless of whether the overridden 
method declares the exception

#### What does "final" mean in case of a variable, method or a class?

It is constant, cannot be modified.

final is a non-access modifier applicable only to a variable, a method or a class. When a variable is 
declared with the final keyword, its value can't be modified, and is essentially, a constant.

#### What is the super keyword?

The super keyword refers to superclass (parent) objects. It is used to call superclass methods, and to 
access the superclass constructor. The most common use of the super keyword is to eliminate the confusion 
between superclasses and subclasses that have methods with the same name.

#### What are “generics”? When to use? Show examples.

Java Generic methods and generic classes enable programmers to specify, with a single method declaration, 
a set of related methods, or with a single class declaration, a set of related types, respectively. 
Generics also provide compile-time type safety that allows programmers to catch invalid types at compile time.

#### What is the benefit of having “generic” containers?

https://docs.oracle.com/javase/tutorial/java/generics/why.html

In a nutshell, generics enable types (classes and interfaces) to be parameters when defining classes, 
interfaces and methods. Much like the more familiar formal parameters used in method declarations, type 
parameters provide a way for you to re-use the same code with different inputs. The difference is that 
the inputs to formal parameters are values, while the inputs to type parameters are types.  
Stronger type checks at compile time.  
Elimination of casts  
Enabling programmers to implement generic algorithms.

#### Given two Java programs on two different machines. How can you communicate between the two? What are the possible ways?

https://docs.oracle.com/javase/tutorial/networking/sockets/

Client Server architecture over a network using sockets.

#### What is an annotation? What can be annotated and how? Show examples.

Annotations are used to provide supplement information about a program.

Annotations start with ‘@’.  
Annotations do not change action of a compiled program.  
Annotations help to associate metadata (information) to the program elements i.e. instance variables, 
constructors, methods, classes, etc.  
Annotations are not pure comments as they can change the way a program is treated by the compiler

        class Base 
        { 
             public void display() 
             { 
                 System.out.println("Base display()"); 
             } 
        } 
        class Derived extends Base 
        { 
             @Override
             public void display(int x) 
             { 
                 System.out.println("Derived display(int )"); 
             } 
          
             public static void main(String args[]) 
             { 
                 Derived obj = new Derived(); 
                 obj.display(); 
             } 
        }


### C&#35;

#### Explain the purpose of IL and how does it relate to CLR?

Managed code is written in one of the high-level languages that can be run on top of .NET, such as C#, Visual Basic, F# and others. When you compile code written in those languages with their respective compiler, you don’t get machine code. You get Intermediate Language code which the runtime then compiles and executes.


#### What does “managed code” mean?

To put it very simply, managed code is just that: code whose execution is managed by a runtime. In this case, the runtime in question is called the Common Language Runtime or CLR, regardless of the implementation (Mono or .NET Framework or .NET Core). CLR is in charge of taking the managed code, compiling it into machine code and then executing it. On top of that, runtime provides several important services such as automatic memory management, security boundaries, type safety etc.

#### What is an assembly?

Assemblies form the fundamental units of deployment, version control, reuse, activation scoping, and security permissions for .NET-based applications. An assembly is a collection of types and resources that are built to work together and form a logical unit of functionality. Assemblies take the form of executable (.exe) or dynamic link library (.dll) files, and are the building blocks of .NET applications. They provide the common language runtime with the information it needs to be aware of type implementations.

In .NET Core and .NET Framework, you can build an assembly from one or more source code files. In .NET Framework, assemblies can contain one or more modules. This allows larger projects to be planned so that several developers can work on separate source code files or modules, which are combined to create a single assembly. 


#### What is the difference between an EXE and a DLL?

* EXE is an extension used for executable files while DLL is the extension for a dynamic link library.
* An EXE file can be run independently while a DLL is used by other applications.
* An EXE file defines an entry point while a DLL does not.
* A DLL file can be reused by other applications while an EXE cannot.
* A DLL would share the same process and memory space of the calling application while an EXE creates its separate process and memory space.


#### What is strong-typing versus weak-typing? Which is preferred? Why?

In computer programming, programming languages are often colloquially classified as to whether the language's type system makes it strongly typed or weakly typed (loosely typed). However, there is no precise technical definition of what the terms mean and different authors disagree about the implied meaning of the terms and the relative rankings of the "strength" of the type systems of mainstream programming languages.

Generally, a strongly typed language has stricter typing rules at compile time, which implies that errors and exceptions are more likely to happen during compilation. Dynamically typed languages (where type checking happens at run time) can also be strongly typed. Most of these rules affect variable assignment, return values and function calling.

A weakly typed language has looser typing rules and may produce unpredictable results or may perform implicit type conversion at runtime.


#### What is a namespace?

Namespaces are heavily used in C# programming in two ways. First, .NET uses namespaces to organize its many classes, as follows:

System.Console.WriteLine("Hello World!");

System is a namespace and Console is a class in that namespace. The using keyword can be used so that the complete name is not required, as in the following example:

using System;

Console.WriteLine("Hello");
Console.WriteLine("World!");

Second, declaring your own namespaces can help you control the scope of class and method names in larger programming projects. Use the namespace keyword to declare a namespace, as in the following example:

        namespace SampleNamespace
        {
            class SampleClass
            {
                public void SampleMethod()
                {
                    System.Console.WriteLine(
                    "SampleMethod inside SampleNamespace");
                }
            }
        }

Namespaces have the following properties:
* They organize large code projects.
* They are delimited by using the . operator.
* The using directive obviates the requirement to specify the name of the namespace for every class.
* The global namespace is the "root" namespace: global::System will always refer to the .NET System namespace.


#### Explain sealed class in C#?

Once a class is defined as a sealed class, this class cannot be inherited. In C#, the “sealed” modifier is used to declare a class as sealed.

#### What is explicit vs. implicit conversion? Give examples of both of them.

Type conversion is converting one type of data to another type. It is also known as Type Casting. In C#, type casting has two forms −

Implicit type conversion − These conversions are performed by C# in a type-safe manner. For example, are conversions from smaller to larger integral types and conversions from derived classes to base classes.

Explicit type conversion − These conversions are done explicitly by users using the pre-defined functions. Explicit conversions require a cast operator.

        double d = 5673.74; 
        int i;
        
        // cast double to int.
        i = (int)d;


#### Is a struct stored on the heap or stack?

In C#, classes are always allocated on the heap. Structs are allocated on the stack, if a local function variable, or on the heap as part of a class if a class member.

http://clarkkromenaker.com/post/csharp-structs/


#### Can a struct have methods?

Structures can have methods, fields, indexers, properties, operator methods, and events. 

#### Can DateTimes be null?

DateTime is a value type, which, just like int and double, has no meaningful null value.
In C# you can default it to the equivalent to DateTime.MinValue:

DateTime d = default(DateTime);

That said, there is the Nullable< T> type, which is used to provide a null value for any value type T. The shorthand for Nullable< DateTime> in C# is DateTime?.


#### List out the differences between Array and ArrayList in C#?

Arrays are strongly-typed collections of the same data type and have a fixed length that cannot be changed during runtime. We can access the Array elements by numeric index. The array indexes start at zero. The default value of numeric array elements is set to zero, and the reference elements are set to null.

        int[] intArray=new int[]{2};
        intArray[0] = 1;
        intArray[1] = 2;


An Array list is not a strongly-typed collection. It can store the values of different data types or same datatype. The size of an array list increases or decreases dynamically so it can take any size of values from any data type. ArrayList is one of the most flexible data structures from C# Collections. ArrayList contains a simple list of values. ArrayList implements the IList interface using an array and very easily we can add, insert, delete, view etc. It is very flexible because we can add without any size information that is it will grow dynamically and also shrink.

        ArrayList Arrlst = new ArrayList();
        Arrlst.Add("Sagar");
        Arrlst.Add(1);
        Arrlst.Add(null);


#### How is the using() pattern useful? What is IDisposable? How does it support deterministic finalization?

Provides a convenient syntax that ensures the correct use of IDisposable objects. Beginning in C# 8.0, the using statement ensures the correct use of IAsyncDisposable objects.

The IDisposable Interface provides a mechanism for releasing unmanaged resources.

Providing a method for deterministic finalization is important because it eliminates a dependency on the indeterminate timing behavior of the finalizer. Even if the developer fails to call Close() explicitly, the finalizer will take care of the call. In such a case, the finalizer will run later than if it was called explicitly—but it will be called eventually.

An explicit call to Dispose() after using the specific part of the code that can cause a memory issue by not disposing of it. Dispose() is the method responsible for cleaning up the resources that are not related to memory and, therefore, subject to cleanup implicitly by the garbage collector.


#### How can you make sure that objects using dedicated resources (database connection, files, hardware, OS handle, etc.) are released as early as possible?

For the majority of the objects that your app creates, you can rely on the .NET garbage collector to handle memory management. However, when you create objects that include unmanaged resources, you must explicitly release those resources when you finish using them. The most common types of unmanaged resources are objects that wrap operating system resources, such as files, windows, network connections, or database connections. Although the garbage collector is able to track the lifetime of an object that encapsulates an unmanaged resource, it doesn't know how to release and clean up the unmanaged resource.

If your types use unmanaged resources, you should do the following:

Implement the dispose pattern. This requires that you provide an IDisposable.Dispose implementation to enable the deterministic release of unmanaged resources. A consumer of your type calls Dispose when the object (and the resources it uses) are no longer needed. The Dispose method immediately releases the unmanaged resources.

In the event that a consumer of your type forgets to call Dispose, provide a way for your unmanaged resources to be released. There are two ways to do this:

Use a safe handle to wrap your unmanaged resource. This is the recommended technique. Safe handles are derived from the System.Runtime.InteropServices.SafeHandle abstract class and include a robust Finalize method. When you use a safe handle, you simply implement the IDisposable interface and call your safe handle's Dispose method in your IDisposable.Dispose implementation. The safe handle's finalizer is called automatically by the garbage collector if its Dispose method is not called.

—or—

Override the Object.Finalize method. Finalization enables the non-deterministic release of unmanaged resources when the consumer of a type fails to call IDisposable.Dispose to dispose of them deterministically. Define a finalizer by overriding the Object.Finalize method.

 Warning

However, because object finalization can be a complex and an error-prone operation, we recommend that you use a safe handle instead of providing your own finalizer.

Consumers of your type can then call your IDisposable.Dispose implementation directly to free memory used by unmanaged resources. When you properly implement a Dispose method, either your safe handle's Finalize method or your own override of the Object.Finalize method becomes a safeguard to clean up resources in the event that the Dispose method is not called.


#### Why to use keyword “const” in C#? Give an example.

You use the const keyword to declare a constant field or a constant local. Constant fields and locals aren't variables and may not be modified.

        public const double GravitationalConstant = 6.673e-11;


#### What is the difference between “const” and “readonly” variables in C#?

A const is a compile-time constant whereas readonly allows a value to be calculated at run-time and set in the constructor or field initializer. So, a 'const' is always constant but 'readonly' is read-only once it is assigned.

#### What is a property in C#?

A property is a member that provides a flexible mechanism to read, write, or compute the value of a private field. Properties can be used as if they are public data members, but they are actually special methods called accessors.


#### List out two different types of errors in C#?

Syntax Errors  
* Syntax errors occur during development, when you make type mistakes in code.   

Runtime Errors (Exceptions)  
* Runtime errors occur during execution of the program.


#### What is the difference between “out” and “ref” parameters in C#?

The out is a keyword in C# which is used for the passing the arguments to methods as a reference type. It is generally used when a method returns multiple values. The out parameter does not pass the property.

        // C# program to illustrate the 
        // concept of out parameter 
        using System; 

        class GFG { 

            // Main method 
            static public void Main() 
            { 

                // Declaring variable 
                // without assigning value 
                int G; 

                // Pass variable G to the method 
                // using out keyword 
                Sum(out G); 

                // Display the value G 
                Console.WriteLine("The sum of" + 
                        " the value is: {0}", G); 
            } 

            // Method in which out parameter is passed 
            // and this method returns the value of 
            // the passed parameter 
            public static void Sum(out int G) 
            { 
                G = 80; 
                G += G; 
            } 
        } 


The ref is a keyword in C# which is used for the passing the arguments by a reference. Or we can say that if any changes made in this argument in the method will reflect in that variable when the control return to the calling method. The ref parameter does not pass the property.

        // C# program to illustrate the 
        // concept of ref parameter 
        using System; 

        class GFG { 

            // Main Method 
            public static void Main() 
            { 

                // Assign string value 
                string str = "Geek"; 

                // Pass as a reference parameter 
                SetValue(ref str); 

                // Display the given string 
                Console.WriteLine(str); 
            } 

            static void SetValue(ref string str1) 
            { 

                // Check parameter value 
                if (str1 == "Geek") { 
                    Console.WriteLine("Hello!!Geek"); 
                } 

                // Assign the new value 
                // of the parameter 
                str1 = "GeeksforGeeks"; 
            } 
        } 



#### Can we override private virtual method in C#?

No, you cannot access private methods in inherited classes. - They have to be protected in the base class to allow any sort of access.


#### What's the difference between IEquatable and just overriding Object.Equals()?

Defines a generalized method that a value type or class implements to create a type-specific method for determining equality of instances.

This interface is implemented by types whose values can be equated (for example, the numeric and string classes). A value type or class implements the Equals method to create a type-specific method suitable for determining equality of instances.


#### Explain the differences between public, protected, private and internal. Explain access modifier – “protected internal” in C#!

Private Access Modifier  
Objects that implement private access modifier are accessible only inside a class or a structure. As a result, we can’t access them outside the class they are created

Public Access Modifier  
Objects that implement public access modifiers are accessible from everywhere in our project. Therefore, there are no accessibility restrictions  

Protected Access Modifier  
The protected keyword implies that the object is accessible inside the class and in all classes that derive from that class. 

Internal Access Modifier  
The internal keyword specifies that the object is accessible only inside its own assembly (project)  but not in other assemblies

Protected Internal Access Modifier  
The protected internal access modifier is a combination of protected and internal. As a result, we can access the protected internal member only in the same assembly or in a derived class in other assemblies (projects)

Private Protected Access Modifier  
The private protected access modifier is a combination of the private and protected keywords. We can access members inside the containing class or in a class that derives from a containing class, but only in the same assembly(project). Therefore, if we try to access it from another assembly, we will get an error.


#### What’s the difference between using `override` and `new` keywords when defining method in child class?

Override changes a method in the sub-class.
New instantiates a new object from a class.


#### Explain StringBuilder class in C#!

Represents a mutable string of characters. It is useful for bringing multiple strings together in one string as opposed to concatenating a large number of immutable strings that would take much more memory.



#### How we can sort the array elements in descending order in C#?

Use the Reverse() method. That will give you a sorted array in descending order.


#### Can you use a value type as a generic type argument in C#? For example when implementing an interface like (IEquatable).

In a generic type or method definition, a type parameter is a placeholder for a specific type that a client specifies when they create an instance of the generic type. A generic class, such as GenericList< T> listed in Introduction to Generics, cannot be used as-is because it is not really a type; it is more like a blueprint for a type. To use GenericList< T>, client code must declare and instantiate a constructed type by specifying a type argument inside the angle brackets. The type argument for this particular class can be any type recognized by the compiler. Any number of constructed type instances can be created, each one using a different type argument, as follows:

        GenericList<float> list1 = new GenericList<float>();
        GenericList<ExampleClass> list2 = new GenericList<ExampleClass>();
        GenericList<ExampleStruct> list3 = new GenericList<ExampleStruct>();


#### What are Nullable Types in C#?

A nullable value type T? represents all values of its underlying value type T and an additional null value. For example, you can assign any of the following three values to a bool? variable: true, false, or null. An underlying value type T cannot be a nullable value type itself.

 Note

C# 8.0 introduces the nullable reference types feature. For more information, see Nullable reference types. The nullable value types are available beginning with C# 2.

Any nullable value type is an instance of the generic System.Nullable< T> structure. You can refer to a nullable value type with an underlying type T in any of the following interchangeable forms: Nullable< T> or T?.

You typically use a nullable value type when you need to represent the undefined value of an underlying value type. For example, a Boolean, or bool, variable can only be either true or false. However, in some applications a variable value can be undefined or missing. For example, a database field may contain true or false, or it may contain no value at all, that is, NULL. You can use the bool? type in that scenario.

Declaration and assignment
As a value type is implicitly convertible to the corresponding nullable value type, you can assign a value to a variable of a nullable value type as you would do that for its underlying value type. You can also assign the null value. For example:

        double? pi = 3.14;
        char? letter = 'a';

        int m2 = 10;
        int? m = m2;

        bool? flag = null;

        // An array of a nullable value type:
        int?[] arr = new int?[10];



#### Conceptually, what is the difference between early-binding and late-binding?

Early binding refers to events that occur at compile time.   
The opposite of early binding is late binding. Late binding refers to function calls that are not resolved until run time. 


#### What is delegate, event, callback, multicast delegate?

A delegate is a pointer to a function and you can invoke the pointed function via the delegate. They are used for callbacks.
Multicast delegates help to invoke multiple callbacks.
Events encapsulate delegate and implement publisher and subscriber model.
Events and Multicast are types of delegates. So delegate is the base for events and multicast.


#### What is enum in C#?

An enum is a special "class" that represents a group of constants (unchangeable/read-only variables).

To create an enum, use the enum keyword (instead of class or interface), and separate the enum items with a comma:

        enum Level 
        {
        Low,
        Medium,
        High
        }


#### What is null-conditional operator?

You can use the following operators and expressions when you access a type member:  
* . (member access): to access a member of a namespace or a type  
* [] (array element or indexer access): to access an array element or a type indexer  
* ?. and ?[] (null-conditional operators): to perform a member or element access operation only if an operand is non-null  
* () (invocation): to call an accessed method or invoke a delegate  
* ^ (index from end): to indicate that the element position is from the end of a sequence  
* .. (range): to specify a range of indices that you can use to obtain a range of sequence elements

Available in C# 6 and later, a null-conditional operator applies a member access, ?., or element access, ?[], operation to its operand only if that operand evaluates to non-null; otherwise, it returns null. That is,

    If a evaluates to null, the result of a?.x or a?[x] is null.

    If a evaluates to non-null, the result of a?.x or a?[x] is the same as the result of a.x or a[x], respectively.


#### What is null-coalescing operator?

The null-coalescing operator ?? returns the value of its left-hand operand if it isn't null; otherwise, it evaluates the right-hand operand and returns its result. The ?? operator doesn't evaluate its right-hand operand if the left-hand operand evaluates to non-null.


#### What is serialization?

Serialization is the process of converting an object into a stream of bytes to store the object or transmit it to memory, a database, or a file. Its main purpose is to save the state of an object in order to be able to recreate it when needed. The reverse process is called deserialization.

#### What is the difference between Finalize() and Dispose() methods?

The main difference between dispose() and finalize() is that the method dispose() has to be explicitly invoked by the user whereas, the method finalize() is invoked by the garbage collector, just before the object is destroyed.


#### How do you inherit a class from another class in C#?

In C#, it is possible to inherit fields and methods from one class to another. We group the "inheritance concept" into two categories:

Derived Class (child) - the class that inherits from another class  
Base Class (parent) - the class being inherited from  
To inherit from a class, use the : symbol.

In the example below, the Car class (child) inherits the fields and methods from the Vehicle class (parent):

        class Vehicle  // base class (parent) 
        {
        public string brand = "Ford";  // Vehicle field
        public void honk()             // Vehicle method 
        {                    
            Console.WriteLine("Tuut, tuut!");
        }
        }

        class Car : Vehicle  // derived class (child)
        {
        public string modelName = "Mustang";  // Car field
        }

        class Program
        {
        static void Main(string[] args)
        {
            // Create a myCar object
            Car myCar = new Car();

            // Call the honk() method (From the Vehicle class) on the myCar object
            myCar.honk();

            // Display the value of the brand field (from the Vehicle class) and the value of the modelName from the Car class
            Console.WriteLine(myCar.brand + " " + myCar.modelName);
        }
        }


#### What is difference between “is” and “as” operators in C#?

The difference between is and as operators are as follows: ... The is operator is of boolean type whereas as operator is not of boolean type. The is operator returns true if the given object is of the same type whereas as operator returns the object when they are compatible with the given type.

#### What are indexers in C# .NET?

C# indexers are usually known as smart arrays. A C# indexer is a class property that allows you to access a member variable of a class or struct using the features of an array. In C#, indexers are created using this keyword. Indexers in C# are applicable on both classes and structs.

        using System;  
        namespace Indexer_example1  
        {  
            class Program  
            {  
                class IndexerClass  
                {  
                    private string[] names = new string[10];  
                    public string this[int i]  
                    {  
                        get  
                        {  
                            return names[i];  
                        }  
                        set  
                        {  
                            names[i] = value;  
                        }  
                    }  
                }  
                static void Main(string[] args)  
                {  
                    IndexerClass Team = new IndexerClass();  
                    Team[0] = "Rocky";  
                    Team[1] = "Teena";  
                    Team[2] = "Ana";  
                    Team[3] = "Victoria";  
                    Team[4] = "Yani";  
                    Team[5] = "Mary";  
                    Team[6] = "Gomes";  
                    Team[7] = "Arnold";  
                    Team[8] = "Mike";  
                    Team[9] = "Peter";  
                    for (int i = 0; i < 10; i++)  
                    {  
                        Console.WriteLine(Team[i]);  
                    }  
                    Console.ReadKey();  
                }  
            }  
        }


#### What is the difference between returning IQueryable< T> vs. IEnumerable< T>?

The difference is that IQueryable< T> is the interface that allows LINQ-to-SQL (LINQ.-to-anything really) to work. So if you further refine your query on an IQueryable< T>, that query will be executed in the database, if possible.

For the IEnumerable< T> case, it will be LINQ-to-object, meaning that all objects matching the original query will have to be loaded into memory from the database.


#### What is LINQ? Explain the idea of extension methods.

Language-Integrated Query (LINQ) is the name for a set of technologies based on the integration of query capabilities directly into the C# language.

Extension methods enable you to "add" methods to existing types without creating a new derived type, recompiling, or otherwise modifying the original type. Extension methods are static methods, but they're called as if they were instance methods on the extended type. For client code written in C#, F# and Visual Basic, there's no apparent difference between calling an extension method and the methods defined in a type.

The following example shows how to call the standard query operator OrderBy method on an array of integers. The expression in parentheses is a lambda expression. Many standard query operators take lambda expressions as parameters, but this isn't a requirement for extension methods. 

        class ExtensionMethods2
        {

            static void Main()
            {
                int[] ints = { 10, 45, 15, 39, 21, 26 };
                var result = ints.OrderBy(g => g);
                foreach (var i in result)
                {
                    System.Console.Write(i + " ");
                }
            }
        }
        //Output: 10 15 21 26 39 45


#### What are the advantages and disadvantages of lazy loading?

Advantages of lazy loading:

* Minimizes start up time of the application.
* Application consumes less memory because of on-demand loading.
* Unnecessary database SQL execution is avoided.
* The only one disadvantage is that the code becomes complicated. As we need to do checks if the loading is needed or not, there is a slight decrease in performance.

But the advantages are far more than the disadvantages.

The Lazy< T> class
https://docs.microsoft.com/en-us/dotnet/api/system.lazy-1?view=netcore-3.1


#### How to use of “yield” keyword? Mention at least one practical scenario where it can be used?

When you use the yield contextual keyword in a statement, you indicate that the method, operator, or get accessor in which it appears is an iterator. Using yield to define an iterator removes the need for an explicit extra class (the class that holds the state for an enumeration, see IEnumerator<T> for an example) when you implement the IEnumerable and IEnumerator pattern for a custom collection type.

The following example shows the two forms of the yield statement.

        yield return <expression>;
        yield break;
You use a yield return statement to return each element one at a time.


#### What are attributes in C#? Give some examples of usage of them.

Attributes provide a powerful method of associating metadata, or declarative information, with code (assemblies, types, methods, properties, and so forth).

        [Serializable]
        public class SampleClass
        {
            // Objects of this type can be serialized.
        }



#### By what mechanism does NUnit know what methods to test?

Using attributes.

#### What is the GAC? What problem does it solve?

The Global Assembly Cache (GAC) is a folder in Windows directory to store the . NET assemblies that are specifically designated to be shared by all applications executed on a system. Assemblies can be shared among multiple applications on the machine by registering them in global Assembly cache(GAC).


#### What is the largest number you can work with in C#?

ulong  
0 to 18,446,744,073,709,551,615  
Unsigned 64-bit integer  
System.UInt64


### Database

#### How can you connect your application to a database server? What are the possible ways?

4 Driver types - https://www.tutorialspoint.com/jdbc/jdbc-driver-types.htm

Type 1: JDBC-ODBC Bridge Driver  
Type 2: JDBC-Native API  
Type 3: JDBC-Net pure Java  
Type 4: 100% Pure Java  

In a Type 4 driver, a pure Java-based driver communicates directly with the vendor's database 
through socket connection. This is the highest performance driver available for the database and 
is usually provided by the vendor itself.
        
        Class.forName()
        try {
           Class.forName("oracle.jdbc.driver.OracleDriver").newInstance();
        }
        
        DriverManager.registerDriver()
        try {
           Driver myDriver = new oracle.jdbc.driver.OracleDriver();
           DriverManager.registerDriver( myDriver );
        }

Database URL Formulation  
After you've loaded the driver, you can establish a connection using the DriverManager.getConnection() 
method. For easy reference, let me list the three overloaded DriverManager.getConnection() methods −

getConnection(String url)

getConnection(String url, Properties prop)

getConnection(String url, String user, String password)

#### What do you know about database normalization?

Database normalization is the process of structuring a relational database in 
accordance with a series of so-called normal forms in order to reduce data redundancy and improve 
data integrity. It was first proposed by Edgar F. Codd as part of his relational model.

Normalization entails organizing the columns (attributes) and tables (relations) of a database to 
ensure that their dependencies are properly enforced by database integrity constraints. It is 
accomplished by applying some formal rules either by a process of synthesis (creating a new 
database design) or decomposition (improving an existing database design).

https://en.wikipedia.org/wiki/Database_normalization

Normalization is a database design technique, which is used to design a relational database table up 
to higher normal form. The process is progressive, and a higher level of database normalization 
cannot be achieved unless the previous levels have been satisfied.

That means that, having data in unnormalized form (the least normalized) and aiming to achieve the 
highest level of normalization, the first step would be to ensure compliance to first normal form, 
the second step would be to ensure second normal form is satisfied, and so forth in order mentioned 
above, until the data conform to sixth normal form.


