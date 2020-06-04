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

#IMPORT PIC FROM IMG

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
#### What does “managed code” mean?
#### What is an assembly?
#### What is the difference between an EXE and a DLL?
#### What is strong-typing versus weak-typing? Which is preferred? Why?
#### What is a namespace?
#### Explain sealed class in C#?
#### What is explicit vs. implicit conversion? Give examples of both of them.
#### Is a struct stored on the heap or stack?
#### Can a struct have methods?
#### Can DateTimes be null?
#### List out the differences between Array and ArrayList in C#?
#### How is the using() pattern useful? What is IDisposable? How does it support deterministic finalization?
#### How can you make sure that objects using dedicated resources (database connection, files, hardware, OS handle, etc.) are released as early as possible?
#### Why to use keyword “const” in C#? Give an example.
#### What is the difference between “const” and “readonly” variables in C#?
#### What is a property in C#?
#### List out two different types of errors in C#?
#### What is the difference between “out” and “ref” parameters in C#?
#### Can we override private virtual method in C#?
#### What's the difference between IEquatable and just overriding Object.Equals()?
#### Explain the differences between public, protected, private and internal. Explain access modifier – “protected internal” in C#!
#### What’s the difference between using `override` and `new` keywords when defining method in child class?
#### Explain StringBuilder class in C#!
#### How we can sort the array elements in descending order in C#?
#### Can you use a value type as a generic type argument in C#? For example when implementing an interface like (IEquatable).
#### What are Nullable Types in C#?
#### Conceptually, what is the difference between early-binding and late-binding?
#### What is delegate, event, callback, multicast delegate?
#### What is enum in C#?
#### What is null-conditional operator?
#### What is null-coalescing operator?
#### What is serialization?
#### What is the difference between Finalize() and Dispose() methods?
#### How do you inherit a class from another class in C#?
#### What is difference between “is” and “as” operators in C#?
#### What are indexers in C# .NET?
#### What is the difference between returning IQueryable<T> vs. IEnumerable<T>?
#### What is LINQ? Explain the idea of extension methods.
#### What are the advantages and disadvantages of lazy loading?
#### How to use of “yield” keyword? Mention at least one practical scenario where it can be used?
#### What are attributes in C#? Give some examples of usage of them.
#### By what mechanism does NUnit know what methods to test?
#### What is the GAC? What problem does it solve?
#### What is the largest number you can work with in C#?

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


