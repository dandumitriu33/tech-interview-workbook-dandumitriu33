# Web with Python questions

## Software design

### Clean code

#### Point out 5 suggestions, how to format an SQL query!

* multiple lines
* keyword on the left side, the rest of the code on the right
* spaces around the "=" character
* avoid too much commenting

#### What layers can you name in a simple web application?

* server
* presentation layer
* business/application layer
* persistent storage layer

### Error handling
#### What error can occur, when an array does not have an element on the requested index?

* Python - IndexError
* JavaScript - undefined

#### What is the “finally” block, and how would you use it?

Statements that are executed after the try statement completes. These statements execute regardless of whether an exception was thrown or caught.

#### Why should we catch special exception types?

A common use case for this is to only catch (and silence) a small subset of expected errors, and then re-throw the error in other cases. It mainly improves user experience as less functionality interruptions result in a smoother experience.

### Security
#### What is SQL injection? How to protect an application against it?

**SQL injection** is a code injection technique, used to attack data-driven applications, in which malicious SQL statements are inserted into an entry field for execution (e.g. to dump the database contents to the attacker).

Protection measures can be:
 * escape characters - .replace(“‘“, “‘’”)
 * pattern checks
 * database user permissions

#### What is XSS? How to protect an application against it?

**Cross-site scripting** (XSS) is a type of computer security vulnerability typically found in web applications. XSS enables attackers to inject client-side scripts into web pages viewed by other users. A cross-site scripting vulnerability may be used by attackers to bypass access controls such as the same-origin policy.

Protection measures can be:
* validation
* HTML sanitization
* disabling scripting or selectively disabling scripting
* cookie security

#### How to properly store passwords?

Hashed with salt.

#### What is HTTPS?

**Hypertext Transfer Protocol Secure** (HTTPS) is an extension of the Hypertext Transfer Protocol (HTTP). It is used for secure communication over a computer network, and is widely used on the Internet. In HTTPS, the communication protocol is encrypted using Transport Layer Security (TLS) or, formerly, its predecessor, Secure Sockets Layer (SSL). The protocol is therefore also often referred to as HTTP over TLS, or HTTP over SSL.

#### What is encryption and decryption?

In cryptography, **encryption** is the process of encoding a message or information in such a way that only authorized parties can access it and those who are not authorized cannot. Encryption does not itself prevent interference but denies the intelligible content to a would-be interceptor. In an encryption scheme, the intended information or message, referred to as plaintext, is encrypted using an encryption algorithm–a cipher–generating ciphertext that can be read only if decrypted.

#### What is hashing?

A **hash function** is any function that can be used to map data of arbitrary size to fixed-size values. The values returned by a hash function are called hash values, hash codes, digests, or simply hashes. The values are used to index a fixed-size table called a hash table. Use of a hash function to index a hash table is called **hashing** or **scatter storage addressing**.

#### What is the difference between encryption and hashing? When would you use which?

**Purpose of hashing**

* Hashing can be used to compare a large amount of data. Hash values can be created for different data, meaning that it is easier comparing hashes than the data itself.
* It is easy to find a record when the data is hashed.
* Hashing algorithms are used in cryptographic applications like a digital signature.
* Hashing is used to generate random strings to avoid duplication of data stored in databases.
* Geometric hashing – widely used in computer graphics to find closet pairs and proximity problems in planes. It is also called grid method and it has also been adopted in telecommunications.

**Purpose of encryption**

The main idea of encryption is to protect data from an unauthorized person who wants to read or get information from a message that was not intended for them. Encryption enhances security when sending messages through the Internet or through any given network. The following are key elements of security that encryption helps to enhance.

* **Confidentiality** – Encrypted messages cannot be read or changed by another person.
* **Encrypt** – It transforms data in such a way that only specific individuals can transform the message.
* **Granular access control** – Users are limited to what they can see and do.
* It makes auditing for **accountability** easy. In the case of a message leak, it is easy to trace who did that and when thus security breaches can be sorted out efficiently.
* **Authentication** – the origin of the message received can be traced thus facilitating authentication.

#### What encryption methods do you know?

* **Symmetric encryption** – Uses the same secret key to encrypt and decrypt the message. The secret key can be a word, a number or a string of random letters.  Both the sender and the receiver should have the key. It is the oldest technique of encryption.
* **Asymmetric encryption** – It deploys two keys, a public key known by everyone and a private key known only by the receiver. The public key is used to encrypt the message and a private key is used to decrypt it. Asymmetric encryption is little slower than symmetric encryption and consumes more processing power when encrypting data.
* **Hybrid encryption** – It is a process of encryption that blends both symmetric and asymmetric encryption. It takes advantage of the strengths of the two encryptions and minimizes their weakness.

#### What hashing methods do you know?

* **MD4** – It is a hash function created by Ronald Rivest in 1990. It has a length of 128 bits and has influenced many posterior designs like WMD5, WRIPEMD and WSHA family. The security of this algorithm has however been criticized even by the creator himself.
* **SHA** algorithm – Secure Hash Algorithm was designed by the National Security Agency to be used in their digital signature algorithm. It has a length of 160 bits. Just like the latter, security weaknesses in it means that it is no longer used SHA and SHA-1, organizations are using strong SHA-2 (256 bit) algorithm for the cryptographic purpose. (How to move from SHA1 to SHA2 algorithm?)
* **RIPMEND** – It is a cryptographic hash algorithm designed by Hans Dobbertin. It has a length of 160 bits. It was developed in the framework of the EU project RIPE.
* **WHIRLPOOL** algorithm – It is algorithm design by Vincent Rijmen and Paul Barreto. It has a length of 2256 bits and produces the 512-bit message digest.
* **TIGER** algorithm – It is a new and fast algorithm. It used by modern computers.  It hashes more than 132M bits per second. It has thus far proved to be more efficient than all the hashing algorithms discussed. It has no restrictions on its usage that means it has no patents.

#### How/where would you store sensitive data (like db password, API key, ...) of your application?

Environment variables.

## Computer science

### Algorithms

#### What is the difference between Stack and Queue data structure?

**Stack** - last in first out  
**Queue** - first in first out

#### What is BubbleSort? Describe the main logic of this sorting algorithm.

**Bubble Sort** is the simplest sorting algorithm that works by repeatedly swapping the adjacent elements if they are in the wrong order.

#### Explain the process of finding the maximum and minimum value in a list of numbers!

Looping through the list(unordered) and comparing every element to the given max/min.
If the list is ordered, we can use the divide and conquer algorithm.

#### Explain the process of calculating the average value in an array of numbers!

Adding all the elements and then dividing the sum by the number of elements

#### What is Big O complexity? Explain time and space complexity!

**Big O notation** is a mathematical notation that describes the limiting behavior of a function when the argument tends towards a particular value or infinity.
In computer science, big O notation is used to classify algorithms according to how their running time or space requirements grow as the input size grows.  
In computer science, the **time complexity** is the computational complexity that describes the amount of time it takes to run an algorithm. Time complexity is commonly estimated by counting the number of elementary operations performed by the algorithm, supposing that each elementary operation takes a fixed amount of time to perform. Thus, the amount of time taken and the number of elementary operations performed by the algorithm are taken to differ by at most a constant factor. The time complexity is commonly expressed using big O notation, typically O(n), O(n log n), O(n*Alpha), O(2*n) etc., where n is the input size in units of bits needed to represent the input.  
In computer science, the **space complexity** of an algorithm or a computer program is the amount of memory space required to solve an instance of the computational problem as a function of the size of the input. It is the memory required by an algorithm to execute a program and produce output. It has the same O(n) type notation.

#### Explain the process of calculating the average value in a linked list of numbers!

**Iterative Solution**: O(n)
1. Initialise a pointer ptr with the head of the linked list and a sum variable with 0
2. Start traversing the linked list using a loop until all the nodes get traversed
3. Add the value of current node to the sum i.e. sum += ptr -> data
4. Increment the pointer to the next node of linked list i.e. ptr = ptr ->next
5. Divide sum by total number of node and Return the average


### Procedural
#### How the CASE condition works in SQL?

Similar to an IF statement where a result is displayed based on a condition.

```SQL
SELECT OrderID, Quantity,
CASE WHEN Quantity > 30 THEN "The quantity is greater than 30"
WHEN Quantity = 30 THEN "The quantity is 30"
ELSE "The quantity is under 30"
END AS QuantityText
FROM OrderDetails;
```

#### How the switch-case condition works in JavaScript?

Similar to multiple IF, ELSE IF statements.

```Javascript
let day;
switch (new Date().getDay()) {
 case 0:
  day = "Sunday";
  break;
 case 1:
  day = "Monday";
  break;
 case 2:
  day = "Tuesday";
  break;
 case 3:
  day = "Wednesday";
  break;
 case 4:
  day = "Thursday";
  break;
 case 5:
  day = "Friday";
  break;
 case 6:
  day = "Saturday";
}
document.getElementById("demo").innerHTML = "Today is " + day;
```

#### How to achieve a switch-case-like structure in Python?

Multiple IF and ELIF statements.

#### Explain variable scoping in Python!

In Python, the **LEGB** rule is used to decide the order in which the namespaces are to be searched for scope resolution.  
The scopes are listed below in terms of hierarchy(highest to lowest/narrowest to broadest):
* **Local**(L): Defined inside function/class
* **Enclosed**(E): Defined inside enclosing functions(Nested function concept)
* **Global**(G): Defined at the uppermost level
* **Built-in**(B): Reserved names in Python builtin modules

#### What’s the difference between const and var in JavaScript?

**var**: The scope of a variable defined with the keyword “var” is limited to the “function” within which it is defined. If it is defined outside any function, the scope of the variable is global  
var is **“function scoped”**  
**let**: The scope of a variable defined with the keyword “let” or “const” is limited to the “block” defined by curly braces i.e. {}  
**const**: The scope of a variable defined with the keyword “const” is limited to the block defined by curly braces. However if a variable is defined with keyword const, it cannot be reassigned.
“const” cannot be re-assigned to a new value, however, it can be mutated.  
**let** and **const** are **“block scoped”**

#### What does a list comprehension look like in Python?

```Python
even_squares = [num*num for num in range(11) if num%2==0]
```

#### What does a “ternary expression” look like in Python?

```Python
x = a if True else b
```
For example, x = 4 if b > 8 else 9 is read aloud as x will be 4 if b is greater than 8 otherwise 9.

#### What does the "ternary expression" look like in JavaScript?

```Javascript
condition ? exprIfTrue : exprIfFalse
```

#### How to import a function from another module in Python?

```Python
from util import bubble_sort
```

#### How to import a function from another module in JavaScript?

```Javascript
export function bubbleSort (theList) { … };
import { bubbleSort } from “/utils.js”;
```


### Functional
#### What is recursion?

**Recursion** in computer science is a method of solving a problem where the solution depends on solutions to smaller instances of the same problem. Such problems can generally be solved by iteration, but this needs to identify and index the smaller instances at programming time. At the opposite, recursion solves such recursive problems by using functions that call themselves from within their own code. The approach can be applied to many types of problems, and recursion is one of the central ideas of computer science.

#### Write a recursive function which calculates the Fibonacci numbers!

```Python
def Fibonacci(n):
    if n<0:
        print("Incorrect input")
    # First Fibonacci number is 0
    elif n==1:
        return 0
    # Second Fibonacci number is 1
    elif n==2:
        return 1
    else:
        return Fibonacci(n-1)+Fibonacci(n-2)
  
print(Fibonacci(9))
```

#### How to store a function in a variable in Python?

```Python
def foo():
	return ‘hello foo’
test = foo
print(test()) # will print hello foo
```

#### List the ways of defining a callable logical unit in JavaScript!

* var
* let
* const
* function

#### What is an event listener? How to attach one?

The EventListener interface represents an object that can handle an event dispatched by an EventTarget object.  

```Javascript
const buttonElement = document.getElementById('btn'); 
// Add a handler for the 'click' event by providing a callback function. 
// Whenever the element is clicked, a pop-up with "Element clicked!" will 
// appear. 
buttonElement.addEventListener('click', function (event) { 
alert('Element clicked through function!'); 
});
```

#### How to trigger an event in JavaScript?

* do the action is is set up to listen to
* simulate the action with a method, for example the mouse click method .clcik()

```Javascript
document.getElementById("clickMeButton").clcik(); // clicks on the button
```

#### What is a callback function? Tell some examples of its usage.

A **callback** is a function that is to be executed after another function has finished executing — hence the name ‘call back’.  
In JavaScript, functions are objects. Because of this, functions can take functions as arguments, and can be returned by other functions. Functions that do this are called higher-order functions. Any function that is passed as an argument is called a callback function.  
Use cases:
* synchronous/asynchronous js, loding the dom before the “long execution functions” are done
* fetch actions with API info

#### What is a Python decorator? How does it work? Tell some examples of its usage.

A **decorator** wraps a function in additional functionality. They are a very powerful and useful tool in Python since it allows programmers to modify the behavior of a function or class. Decorators allow us to wrap another function in order to extend the behavior of the wrapped function, without permanently modifying it.  
In Decorators, functions are taken as the argument into another function and then called inside the wrapper function.  
For example, Flask assigns routes, manages the connection to the database via decorators and thus makes the code more readable. 

#### What is the difference between synchronous and asynchronous execution?

**Synchronous** execution is where the code lines are executed one after the other, top to bottom  
**Asynchronous** execution does have top to bottom execution but in addition, it allows for sending functions to the call queue which is executed after the call stack

## Programming languages

### SQL

#### How can you connect your application to a database server? What are the possible ways?
#### When do you use the DISTINCT keyword in SQL?
#### What are aggregate functions in SQL? Give 3 examples.
#### What kind of JOIN types do you know in SQL? Could you give examples?
#### What are the constraints in sql?
#### What is a cursor in SQL? Why would you use one?
#### What are database indexes? When to use?
#### What are database transactions? When to use?
#### What kind of database relations do you know? How to define them?
#### You have a table with an “address” field which contains data like “3525, Miskolc, Régiposta 9.” (postcode, city, street name and address). How would you query all records related to Miskolc?
#### How would you keep track of what kind of data has changed after an UPDATE or DELETE operation in a table?

### HTML & CSS

#### What’s the difference between XML, XHTML and HTML?
#### How to include a JavaScript file in a webpage?
#### How to include a CSS file in a webpage?
#### How to select an element using its id in CSS?
#### How to select elements using their class in CSS?
#### How to select elements which have the ‘alpha’ and ‘beta’ classes in CSS?
#### How to select all list items in all ordered lists on the page in CSS?
#### How to select elements using their attributes in CSS?
#### What are UX and UI?
#### Please list some points that an application should fulfill to have good UX.
#### What is XML, XSLT, DTD?
#### What is the difference between HTML and XML?

### Javascript

#### What is javascript?
#### When to use AJAX? Bring examples of its usage.
#### What is DOM and how to manipulate it from Javascript?
#### What are events and how/why to use them in Javascript?
#### What is event bubbling/capturing? How would you use it?
#### What is JSON and how do we use it?

## Software engineering

### Version control

#### What type of branching strategy would you use?
#### What would you do if you find a bug on the production code (master branch)?
#### How can you move changes from one branch to another in GIT?
#### How does a VCS help with code reviews?
#### What is your favorite git command? Why?
#### What does remote/local mean in Git? 

### DevOps

#### Why is it good to use a package manager software?
#### Why is it good to use a virtual environment for a project?

### Networks

#### What kind of HTTP status codes do you know?
#### What is a API?
#### What is REST API?
#### What is JSON? When to use?
#### What is TCP/IP? What layers does it define, what are they responsible for?
#### What’s the difference between TCP and UDP?
#### How does an HTTP Request look like? What are the most relevant HTTP header fields?
#### How does an HTTP Response look like? What are the most relevant HTTP header fields?
#### What is DNS? How does it work?
#### What is a web server?
#### Explain the client-server architecture.
#### What would you use a session for?
#### What would you use a cookie for?

## Software Development Methodologies

#### What kind of software development methodologies do you know? What are the main features of these?
#### What are the SCRUM roles?
#### What are the SCRUM ceremonies?
#### What are the SCRUM artifacts?
#### What is the main goal of a retrospective meeting?
#### Explain, when would you recommend to use the waterfall methodology?
