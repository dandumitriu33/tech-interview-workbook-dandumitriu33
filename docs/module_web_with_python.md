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

Via the backend - for example Flask with the psycopg2 driver and environment variables.

#### When do you use the DISTINCT keyword in SQL?

When there are multiple responses with the same name. Inside a table, a column often contains many duplicate values; and sometimes you only want to list the different (distinct) values.

#### What are aggregate functions in SQL? Give 3 examples.

* **AVG** – calculates the average of a set of values.
* **COUNT** – counts rows in a specified table or view.
* **MIN** – gets the minimum value in a set of values.
* **MAX** – gets the maximum value in a set of values.
* **SUM** – calculates the sum of values.

#### What kind of JOIN types do you know in SQL? Could you give examples?

* **(INNER) JOIN**: Returns records that have matching values in both tables
* **LEFT (OUTER) JOIN**: Returns all records from the left table, and the matched records from the right table
* **RIGHT (OUTER) JOIN**: Returns all records from the right table, and the matched records from the left table
* **FULL (OUTER) JOIN**: Returns all records when there is a match in either left or right table

#### What are the constraints in sql?

Constraints can be specified when the table is created with the CREATE TABLE statement, or after the table is created with the ALTER TABLE statement.  
* **NOT NULL** - Ensures that a column cannot have a NULL value
* **UNIQUE** - Ensures that all values in a column are different
* **PRIMARY KEY** - A combination of a NOT NULL and UNIQUE. Uniquely identifies each row in a table
* **FOREIGN KEY** - Uniquely identifies a row/record in another table
* **CHECK** - Ensures that all values in a column satisfies a specific condition
* **DEFAULT** - Sets a default value for a column when no value is specified
* **INDEX** - Used to create and retrieve data from the database very quickly

#### What is a cursor in SQL? Why would you use one?

The SELECT statement returns a set of rows which is called a result set. However, sometimes, you may want to process a data set on a row by row basis. This is where cursors come into play.  
A database **cursor** is an object that enables traversal over the rows of a result set. It allows you to process individual rows returned by a query.

#### What are database indexes? When to use?

**Indexes** are special lookup tables that the database search engine can use to speed up data retrieval. Simply put, an index is a pointer to data in a table. An index in a database is very similar to an index in the back of a book.
A database index is a data structure that improves the speed of data retrieval operations on a database table at the cost of additional writes and storage space to maintain the index data structure. Indexes are used to quickly locate data without having to search every row in a database table every time a database table is accessed. Indexes can be created using one or more columns of a database table, providing the basis for both rapid random lookups and efficient access of ordered records.

#### What are database transactions? When to use?

**Transactions** solve the problem of modifying the database in an atomic way, so that when there's data change in multiple tables, and an error happens, all changes can be reverted back.  
A database transaction symbolizes a unit of work performed within a database management system (or similar system) against a database, and treated in a coherent and reliable way independent of other transactions. A transaction generally represents any change in a database. Transactions in a database environment have two main purposes:  
* To provide reliable units of work that allow correct recovery from failures and keep a database consistent even in cases of system failure, when execution stops (completely or partially) and many operations upon a database remain uncompleted, with unclear status.  
* To provide isolation between programs accessing a database concurrently. If this isolation is not provided, the programs' outcomes are possibly erroneous.  
In a database management system, a transaction is a single unit of logic or work, sometimes made up of multiple operations. Any logical calculation done in a consistent mode in a database is known as a transaction. One example is a transfer from one bank account to another: the complete transaction requires subtracting the amount to be transferred from one account and adding that same amount to the other.  
A database transaction, by definition, must be **atomic** (it must either complete in its entirety or have no effect whatsoever), **consistent** (it must conform to existing constraints in the database), **isolated** (it must not affect other transactions) and **durable** (it must get written to persistent storage). Database practitioners often refer to these properties of database transactions using the acronym **ACID**.

#### What kind of database relations do you know? How to define them?

* One to One Relationships
* One to Many and Many to One Relationships
* Many to Many Relationships
* Self Referencing Relationships

#### You have a table with an “address” field which contains data like “3525, Miskolc, Régiposta 9.” (postcode, city, street name and address). How would you query all records related to Miskolc?

```SQL
SELECT * FROM table WHERE address LIKE ‘%Miskolc%’;
```

#### How would you keep track of what kind of data has changed after an UPDATE or DELETE operation in a table?

* A separate history table - with same columns + who made the change, when and more info
* Or log files from the backend (data_manager.py) which is more expensive resource wise

### HTML & CSS

#### What’s the difference between XML, XHTML and HTML?

First, there was **SGML**, the conceptual ancestor of both HTML and XML, which is a:
* **Standard** (S) (ISO 8879:1986), so that disparate organizations and programs can exchange documents
* **Generalized** (G), so that users can define new tags
* **Markup** (M), so that document content can be augmented with structural information describing the content
* **Language** (L), so that there's a grammar that defines the markup  
Then, **HTML** was created as a specific set of SGML tags used to define how web pages should be presented.  
**XML** was created as a simplification of SGML.  
**XHTML** was created to recast HTML as well-formed XML (requiring closing tags, for example, which hadn't been strictly necessary in SGML and HTML).  
**HTML 5** is the current version of HTML. It rejects the motivation behind XHTML and allows a looser specification of markup than the rules of XML would require.  

#### How to include a JavaScript file in a webpage?

```HTML
<script type=”text/javascript” src=”test.js” ></script>
````

#### How to include a CSS file in a webpage?

```HTML
<link rel=”stylesheet” type=”text/css” href=”cssfile.css” >
```

#### How to select an element using its id in CSS?

```CSS
#mainButton { color:gray; }
```

#### How to select elements using their class in CSS?

```CSS
.container { color:gray; }
```

#### How to select elements which have the ‘alpha’ and ‘beta’ classes in CSS?

```CSS
.alpha.beta.gamma { color: gray; }
```

#### How to select all list items in all ordered lists on the page in CSS?

```
ol li { color:gray; }
```

#### How to select elements using their attributes in CSS?

The **[attribute="value"]** selector is used to select elements with a specified attribute and value.

```CSS
a[target="_blank"] { background-color: yellow; }
```

#### What are UX and UI?

**User eXperience** (UX). Type your phone number on a numeric pad or select it from all the possible existing phone numbers? Also, slowness or errors can contribute to bad UX.   
User experience design is the process of developing and improving the quality of interaction between a user and all facets of a company.  
User experience design is, in theory, a non-digital (cognitive science) practice, but used and defined predominantly by digital industries.  
UX design is NOT about visuals; it focuses on the overall feel of the experience.  

**User Interface** (UI). The visual part of front end, that can have an effect on UX. It is a field independent of performance, backend functionality.

#### Please list some points that an application should fulfill to have good UX.

No matter what product or service they are designing, or what stage of the process they are at, UX designers will ask themselves the following questions:  
* Is the product **usable**? Is it logical, self-explanatory and easy to use?  
* Does the product or service **solve an existing user problem**?  
* Is it **accessible** (screen readers) for different categories of users?  
* Is the product or service **desirable**? Does it create a positive experience which the user would be happy to repeat?  
The asnwers should be as close as possible to the following:
* **Equitable use**: The design is useful and marketable to people with diverse abilities.
* **Flexibility in use**: The design accommodates a wide range of individual preferences and abilities.
* **Simple and intuitive use**: Use of the design is easy to understand, regardless of the user’s experience, knowledge, language skills, or current concentration level.
* **Perceptible information**: The design communicates necessary information effectively to the user, regardless of ambient conditions or the user’s sensory abilities.
* **Tolerance for error**: The design minimizes hazards and the adverse consequences of accidental or unintended actions.
* **Low physical effort**: The design can be used efficiently and comfortably and with a minimum of fatigue.
* **Size and space for approach and use**: Appropriate size and space is provided for approach, reach, manipulation, and use regardless of user’s body size, posture, or mobility.

#### What is XML, XSLT, DTD?

**eXtensible Stylesheet Language Transformations** (XSLT) is the recommended style sheet language for XML.  
XSLT is far more sophisticated than CSS. With XSLT you can add/remove elements and attributes to or from the output file. You can also rearrange and sort elements, perform tests and make decisions about which elements to hide and display, and a lot more. XSLT uses XPath to find information in an XML document.  
The purpose of a **Document Type Definition** (DTD) is to define the legal building blocks of an XML document. A DTD defines the document structure with a list of legal elements and attributes. ... This takes away the chance of having wrong data in your XML-Document.

#### What is the difference between HTML and XML?

| No.   | HTML                          | XML                                                           |
| :---: |:-----------------------------:| :------------------------------------------------------------:|
| 1. | HTML is used **to display data** and focuses on how data looks. | XML is a software and hardware independent tool used **to transport and store data**. It focuses on what data is. |
| 2. | HTML is a **markup language** itself. | XML provides a **framework to define markup languages**. |
| 3. | HTML is **not case sensitive**. | XML is **case sensitive**. |
| 4. | HTML is a presentation language. | XML is neither a presentation language nor a programming language. |
| 5. | HTML **has its own predefined tags**. | You can **define tags according to your need**. |
| 6. | In HTML, it is **not necessary to use a closing tag**. | XML **makes it mandatory to use a closing tag**. |
| 7. | HTML is **static** because it is used to display data. | XML is **dynamic** because it is used to transport data. |
| 8. | HTML **does not preserve whitespaces**. | XML **preserves whitespaces**. |

### Javascript

#### What is javascript?

**JavaScript** is a scripting or programming language that allows you to implement complex features on web pages. Every time a web page does more than just sit there and display static information for you to look at — displaying timely content updates, interactive maps, animated 2D/3D graphics, scrolling video jukeboxes, etc. — you can bet that JavaScript is probably involved. It is the third layer of the layer cake of standard web technologies, two of which are HTML and CSS.   

#### When to use AJAX? Bring examples of its usage.

Update info on pages without refreshing the entire page/messing up form fields, etc.  
It canbe used for example in a chat app/function, stock info for traders etc.  
Any javascript used should merely extend the core functionality, and your site should be coded to work elegantly in the absence of a javascript-enabled browser. If it adds value to the user, it is a good use of AJAX.

#### What is DOM and how to manipulate it from Javascript?

When a web page is loaded, the browser creates a **Document Object Model** of the page. The HTML DOM model is constructed as a tree of Objects beginning with the Document, the root element <html> and branching down to paragraphs <p> and Text: "My description of this product".  

With the object model, JavaScript gets all the power it needs to create dynamic HTML:
* JavaScript can **change** all the HTML **elements** in the page
* JavaScript can **change** all the HTML **attributes** in the page
* JavaScript can **change** all the CSS **styles** in the page
* JavaScript can **remove** existing HTML **elements and attributes**
* JavaScript can **add** new HTML **elements and attributes**
* JavaScript can **react** to all existing HTML **events** in the page
* JavaScript can **create** new HTML **events** in the page  
**HOW**: select an element and change it’s content or attributes via different commands like:

```JavaScript
document.getElementById(“click-me-link”).innerText=”click me to go to the other page”;
```

#### What are events and how/why to use them in Javascript?

**How**: JavaScript's interaction with HTML is handled through **events** that occur when the user or the browser manipulates a page. When the page loads, it is called an event. When the user clicks a button, that click too is an event. Other examples include events like pressing any key, closing a window, resizing a window, etc.  
Set event listeners and decide how they are handled:

```JavaScript
document.getElementById(“fancy-button”).setEventListener(‘click’, handleClickFancy)
function handleClickFancy() { alert: “fancy!!!!”;}
```
**Why**: functionality is enhanced/extended via JavaScript

#### What is event bubbling/capturing? How would you use it?

With **bubbling**, an event is first captured and handled by the innermost element and then propagated to outer elements. With capturing, the event is first captured by the outermost element and propagated to the inner elements.  

The bubbling principle is simple. When an event happens on an element, it first runs the handlers on it, then on its parent, then all the way up on other ancestors.  
* this (also known as event.currentTarget) is the <form> element, because the handler runs on it  
* event.target is the actual element inside the form that was clicked.


#### What is JSON and how do we use it?

**JavaScript Object Notation** (JSON) is a lightweight data-interchange format. It is easy for humans to read and write. It is easy for machines to parse and generate.  
It is an open-standard file format or data interchange format that uses human-readable text to transmit data objects consisting of attribute–value pairs and array data types (or any other serializable value). It is a very common data format, with a diverse range of applications, such as serving as replacement for XML in AJAX systems.  
JSON is a language-independent data format. It was derived from JavaScript, but many modern programming languages include code to generate and parse JSON-format data. The official Internet media type for JSON is application/json.   JSON filenames use the extension .json.

## Software engineering

### Version control

#### What type of branching strategy would you use?

**Git Flow** - feature branches, release branch, hotfix branch

#### What would you do if you find a bug on the production code (master branch)?

Create a **Hotfix** branch for the issue and after fixing it, merge it back into master.

#### How can you move changes from one branch to another in GIT?

```
git checkout target branch
git pull source branch
```

#### How does a VCS help with code reviews?

They can block push until the code is reviewed.  
When working on larger projects (like open source) there is a strict set of rules to be followed when making changes to code. In addition to Git, a code review process is added to ensure all merges of feature branches are well developed, tested and, even desired.  
When the code has been reviewed and approved based on all the evidence presented within, it is merged into the develop branch to await release.

#### What is your favorite git command? Why?

```
git commit -m "Add feature xyz"
```

It means I completed some work.

#### What does remote/local mean in Git? 

**Local** - the commits are stored locally, on the local machine. No need to use git push. Git log to see changes. Just git init and if you want you can add a remote server later and push the project, with the correct history.  
**Remote** - the repository is on a server somewhere else and the changes need to be pushed there.

### DevOps

#### Why is it good to use a package manager software?

**Package managers** are designed to eliminate the need for manual installs and updates. This can be particularly useful for large enterprises whose operating systems are based on Linux and other Unix-like systems, typically consisting of hundreds or even tens of thousands of distinct software packages.

Usually one command installs the software or updates it as opposed to downloading, extracting and going through installation wizards.

#### Why is it good to use a virtual environment for a project?

A **virtual environment** is a tool that helps to keep dependencies required by different projects separate by creating isolated python (for example) virtual environments for them. This is one of the most important tools that most of the Python developers use as one project mighe experience issues on newer versions of Python and must be kept under the old until the update.

### Networks

#### What kind of HTTP status codes do you know?

There are five classes defined by the standard:
* **1xx informational response** – the request was received, continuing process
* **2xx successful** – the request was successfully received, understood, and accepted
* **3xx redirection** – further action needs to be taken in order to complete the request
* **4xx client error** – the request contains bad syntax or cannot be fulfilled
* **5xx server error** – the server failed to fulfil an apparently valid request

#### What is an API?

An **Application Program Interface** (API) is a set of routines, protocols, and tools for building software applications. Additionally, APIs are used when programming graphical user interface (GUI) components. A good API makes it easier to develop a program by providing all the building blocks.  
An API isn’t the same as the remote server — rather it is the part of the server that receives requests and sends responses.  
It helps in general with lowering the amount of data/info that is worked with - a web page might only need to update a certain part, not a whole page with all the images and elements. For example, you could use JavaScript to just update that one part via an API.

#### What is REST API?

**Representational State Transfer** (REST) is a software architectural style that defines a set of constraints to be used for creating web services. Web services that conform to the REST architectural style, called RESTful web services, provide interoperability between computer systems on the Internet. RESTful web services allow the requesting systems to access and manipulate textual representations of web resources by using a uniform and predefined set of stateless operations.  
A RESTful API is an application program interface (API) that uses HTTP requests to GET, PUT, POST and DELETE data. REST technology is generally preferred to the more robust Simple Object Access Protocol (SOAP) technology because REST leverages less bandwidth, making it more suitable for internet usage.  
REST is an architectural style. An API is designed to expose certain aspects of an application's business logic on a server, and SOAP uses a service interface to do this while REST uses URIs.  
Recommendations for building RESTful APIs:
* keep it simple
* use nouns and not the verbs
* use the right HTTP methods
* use plurals
* use parameters
* use proper HTTP codes
* use versioning
* use pagination

#### What is JSON? When to use?

**JavaScript Object Notation** (JSON) is a standard text-based format for representing structured data based on JavaScript object syntax. It is commonly used for transmitting data in web applications (e.g., sending some data from the server to the client, so it can be displayed on a web page, or vice versa).  It is also used by different applications to cummunicate between themselves.

#### What is TCP/IP? What layers does it define, what are they responsible for?

The **Internet Protocol Suite** is the conceptual model and set of communications protocols used in the Internet and similar computer networks. It is commonly known as **TCP/IP** because the foundational protocols in the suite are the **Transmission Control Protocol** (TCP) and the **Internet Protocol** (IP).  
The TCP/IP model consists of five layers: the **application** layer, **transport** layer, **network** layer, **data link** layer and the **physical** layer.  
TCP/IP specifies how data is exchanged over the internet by providing end-to-end communications that identify how it should be broken into packets, addressed, transmitted, routed and received at the destination. TCP/IP requires little central management, and it is designed to make networks reliable, with the ability to recover automatically from the failure of any device on the network.

#### What’s the difference between TCP and UDP?

| TCP | UDP |
|:---:|:---:|
| TCP is a connection-oriented protocol. Connection-orientation means that the communicating devices should establish a connection before transmitting data and should close the connection after transmitting the data. | UDP is the Datagram oriented protocol. This is because there is no overhead for opening a connection, maintaining a connection, and terminating a connection. UDP is efficient for broadcast and multicast type of network transmission. |
| TCP is reliable as it guarantees delivery of data to the destination router. | The delivery of data to the destination cannot be guaranteed in UDP. |
| TCP provides extensive error checking mechanisms. It is because it provides flow control and acknowledgment of data. | UDP has only the basic error checking mechanism using checksums. |
| Sequencing of data is a feature of Transmission Control Protocol (TCP). this means that packets arrive in-order at the receiver. | There is no sequencing of data in UDP. If ordering is required, it has to be managed by the application layer. |
| TCP is comparatively slower than UDP. | UDP is faster, simpler and more efficient than TCP. |
| Retransmission of lost packets is possible in TCP, but not in UDP. | There is no retransmission of lost packets in User Datagram Protocol (UDP). |
| TCP has a (20-80) bytes variable length header. | UDP has a 8 bytes fixed length header. |
| TCP is heavy-weight. | UDP is lightweight. |
| TCP doesn’t support Broadcasting. | UDP supports Broadcasting. |
|  | UDP is used by DNS, DHCP, TFTP, SNMP, RIP, and VoIP. |

#### What does an HTTP Request look like? What are the most relevant HTTP header fields?

```
GET /home.html HTTP/1.1 
Host: developer.mozilla.org 
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10.9; rv:50.0) Gecko/20100101 Firefox/50.0 
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,*/*;q=0.8 Accept-Language: en-US,en;q=0.5 
Accept-Encoding: gzip, deflate, br 
Referer: https://developer.mozilla.org/testpage.html 
Connection: keep-alive 
Upgrade-Insecure-Requests: 1 
If-Modified-Since: Mon, 18 Jul 2016 02:36:04 GMT 
If-None-Match: "c561c68d0ba92bbeb8b0fff2a9199f722e3a621a" 
Cache-Control: max-age=0
```

#### What does an HTTP Response look like? What are the most relevant HTTP header fields?

```
HTTP/1.1 403 Forbidden
Server: Apache
Content-Type: text/html; charset=iso-8859-1
Date: Wed, 10 Aug 2016 09:23:25 GMT
Keep-Alive: timeout=5, max=1000
Connection: Keep-Alive
Age: 3464
Date: Wed, 10 Aug 2016 09:46:25 GMT
X-Cache-Info: caching
Content-Length: 220

<!DOCTYPE HTML PUBLIC "-//IETF//DTD HTML 2.0//EN>
(more data)
```

A typical status line looks like: HTTP/1.1 404 Not Found. It is the most important line of the response.

#### What is DNS? How does it work?

The **Domain Name System** (DNS) is the phonebook of the Internet. Humans access information online through domain names, like nytimes.com or espn.com. Web browsers interact through Internet Protocol (IP) addresses. DNS translates domain names to IP addresses so browsers can load Internet resources.  
The process of DNS resolution involves converting a hostname (such as www.example.com) into a computer-friendly IP address (such as 192.168.1.1). An IP address is given to each device on the Internet, and that address is necessary to find the appropriate Internet device - like a street address is used to find a particular home.  
The steps in a DNS lookup:  
1. A user types ‘example.com’ into a web browser and the query travels into the Internet and is received by a DNS recursive resolver  
2. The resolver then queries a DNS root nameserver (.)  
3. The root server then responds to the resolver with the address of a Top Level Domain (TLD) DNS server (such as .com or .net), which stores the information for its domains. When searching for example.com, our request is pointed toward the .com TLD  
4. The resolver then makes a request to the .com TLD
5. The TLD server then responds with the IP address of the domain’s nameserver, example.com  
6. Lastly, the recursive resolver sends a query to the domain’s nameserver  
7. The IP address for example.com is then returned to the resolver from the nameserver  
8. The DNS resolver then responds to the web browser with the IP address of the domain requested initially  
9. Once the 8 steps of the DNS lookup have returned the IP address for example.com, the browser is able to make the request for the web page:The browser makes a HTTP request to the IP address
10 The server at that IP returns the webpage to be rendered in the browser  

#### What is a web server?

A **web server** processes incoming network requests over HTTP and several other related protocols. The primary function of a web server is to store, process and deliver web pages to clients. The communication between client and server takes place using the Hypertext Transfer Protocol (HTTP).  
On the hardware side, a web server is a computer that stores web server software and a website's component files (e.g. HTML documents, images, CSS stylesheets, and JavaScript files). It is connected to the Internet and supports physical data interchange with other devices connected to the web.

#### Explain the client-server architecture.

The **client–server** model is a distributed application structure that partitions tasks or workloads between the providers of a resource or service, called servers, and service requesters, called clients. Often clients and servers communicate over a computer network on separate hardware, but both client and server may reside in the same system. A server host runs one or more server programs, which share their resources with clients. A client does not share any of its resources, but it requests content or service from a server. Clients therefore initiate communication sessions with servers, which await incoming requests. Examples of computer applications that use the client–server model are Email, network printing, and the World Wide Web.

#### What would you use a session for?

For a **web session**, the session is the data structure that an application uses to store temporary data that is useful only during the time a user is interacting with the application. It is also specific to the user.  
Sessions are a simple way to store data for individual users against a unique session ID. This can be used to persist state information between page requests. Session IDs are normally sent to the browser via session cookies and the ID is used to retrieve existing session data.

#### What would you use a cookie for?

An **HTTP cookie** (web cookie, browser cookie) is a small piece of data that a server sends to the user's web browser. The browser may store it and send it back with the next request to the same server. Typically, it's used to tell if two requests came from the same browser — keeping a user logged-in, for example. It remembers stateful information for the stateless HTTP protocol.  
Cookies are mainly used for three purposes:  
* **Session management** - Logins, shopping carts, game scores, or anything else the server should remember
* **Personalization** - User preferences, themes, and other settings
* **Tracking** - Recording and analyzing user behavior  
Cookies are sent with every request, so they can worsen performance

## Software Development Methodologies

#### What kind of software development methodologies do you know? What are the main features of these?

**Waterfall** - very well defined steps, when one step is completed, the next can start
**Agile** - short sprints of developing parts of the software, testing and delivering it as opposed to the entire product. Adaptability afterwards to cust modifications. Compared to the Waterfall method, it is faster.

#### What are the SCRUM roles?

Product Owner, Scrum Master, and the Development Team.

#### What are the SCRUM ceremonies?

The Sprint Planning meeting, Daily Scrum, Sprint Review meeting, and Sprint Retrospective meeting.

#### What are the SCRUM artifacts?

The Product Increment, Product Backlog, and Sprint Backlog.

#### What is the main goal of a retrospective meeting?

**Retrospectives** typically last 90 minutes and are there to help incorporate continuous improvement into the team culture and into the Sprint Cadence. This is where the Scrum Team meets to reflect on their previous Sprint and to figure out how to improve as a team by asking – what went well, what did not and what can be improved. It allows the team to focus on its overall performance and identify strategies for continuous improvement.  
Scrum ceremonies to be embedded in the process create a cadence in which the team can maximize their productivity, promote collaboration, maintain transparency, and most importantly, inspect and adapt on the way they go, so that they can continuously learn and improve from each other.

#### Explain, when would you recommend to use the waterfall methodology?

There are good things and bad about the Waterfall approach. On the positive side:  
* Developers and customers agree on what will be delivered early in the development lifecycle. This makes planning and designing more straightforward.  
* Progress is more easily measured, as the full scope of the work is known in advance.  
* Throughout the development effort, it’s possible for various members of the team to be involved or to continue with other work, depending on the active phase of the project. For example, business analysts can learn about and document what needs to be done, while the developers are working on other projects. Testers can prepare test scripts from requirements documentation while coding is underway.  
* Except for reviews, approvals, status meetings, etc., a customer presence is not strictly required after the requirements phase.  
* Because design is completed early in the development lifecycle, this approach lends itself to projects where multiple software components must be designed (sometimes in parallel) for integration with external systems.  
* Finally, the software can be designed completely and more carefully, based upon a more complete understanding of all software deliverables. This provides a better software design with less likelihood of the “piecemeal effect,” a development phenomenon that can occur as pieces of code are defined and subsequently added to an application where they may or may not fit well.  
* If the project owner/customer has these requirements or values them over agile.  
* It is very clear on outcomes. The Waterfall methodology generally comes with a really clear declaration of what it is this system is supposed to do in its fullness, not looking at what it’s going to do tomorrow, but what it’s going to do when the system is complete.  
* It’s good for sign off between a large number of stakeholders. If you’re trying to work with a large number of people, you need to maximise the communication between them and get them all on the same page and all in agreement that they’re going to spend the money or that they’re happy to go down this path. Waterfall, because it does all its documentation and such upfront, is really good for that. It is a benefit.  
* It forces decisions early. This has pros and cons but, if you have a limited budget and you’re working in a waterfall manner, this can make you think "can we afford all of this? Do we have to narrow our scope?". It makes you think about how you’re going to roll out the whole project, rather than thinking of it iteratively. There are pros and cons to that of course.  
* It allows for estimation or better estimation in quoting upfront. By bringing all of the documentation together (some of these are controversial) there is an argument that says then, you have a better idea of all the pieces that are in the project and you can produce a more accurate estimate or quote based on that.  
* It remains stable which is really good for large teams, for example if you’re working say in a space where you’ve got hundreds of people involved in a project. You need a process that remains stable and that people aren’t going to find changing on them day to day because then you need to change manager just to get your processes updated. You couldn’t do agile in a massive team because just the overhead of keeping the process updated would be too high.
