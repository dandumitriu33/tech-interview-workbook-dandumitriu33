# General enterprise questions

## Software engineering

### Architectures

#### What is n-tier (or multi-tier) architecture?  

An N-Tier Application program is one that is distributed among three or more separate computers in a distributed network.

The most common form of n-tier is the 3-tier Application, and it is classified into three categories.

User interface programming in the user's computer
Business logic in a more centralized computer, and
Required data in a computer that manages a database.
This architecture model provides Software Developers to create Reusable application/systems with maximum flexibility.

In N-tier, "N" refers to a number of tiers or layers are being used like – 2-tier, 3-tier or 4-tier, etc. It is also called “Multi-Tier Architecture”.

The n-tier architecture is an industry-proven software architecture model. It is suitable to support enterprise level client-server applications by providing solutions to scalability, security, fault tolerance, reusability, and maintainability. It helps developers to create flexible and reusable applications.

https://www.guru99.com/n-tier-architecture-system-concepts-tips.html

#### What are microservices? Advantages and disadvantages?

Microservices are a way of breaking large software projects into loosely coupled modules, which communicate with each other through simple Application Programming Interfaces (APIs).

#### Advantages of microservices  
The advantages of microservices seem strong enough to have convinced some big enterprise players such as Amazon, Netflix, and eBay to adopt the methodology. Compared to more monolithic design structures, microservices offer:  
* Improved fault isolation: Larger applications can remain mostly unaffected by the failure of a single module.  
* Eliminate vendor or technology lock-in: Microservices provide the flexibility to try out a new technology stack on an individual service as needed. There won’t be as many dependency concerns and rolling back changes becomes much easier. With less code in play, there is more flexibility.  
* Ease of understanding: With added simplicity, developers can better understand the functionality of a service.  
* Smaller and faster deployments: Smaller codebases and scope = quicker deployments, which also allow you to start to explore the benefits of Continuous Deployment.  
* Scalability: Since your services are separate, you can more easily scale the most needed ones at the appropriate times, as opposed to the whole application. When done correctly, this can impact cost savings.  

#### Disadvantages of microservices  
In general, the main negative of microservices is the complexity that any distributed system has.  
* Communication between services is complex: Since everything is now an independent service, you have to carefully handle requests traveling between your modules. In one such scenario, developers may be forced to write extra code to avoid disruption. Over time, complications will arise when remote calls experience latency.  
* More services equals more resources: Multiple databases and transaction management can be painful.  
* Global testing is difficult: Testing a microservices-based application can be cumbersome. In a monolithic approach, we would just need to launch our WAR on an application server and ensure its connectivity with the underlying database. With microservices, each dependent service needs to be confirmed before testing can occur.  
* Debugging problems can be harder: Each service has its own set of logs to go through.  
* Deployment challengers: The product may need coordination among multiple services, which may not be as straightforward as deploying a WAR in a container.  
* Large vs small product companies: Microservices are great for large companies, but can be slower to implement and too complicated for small companies who need to create and iterate quickly, and don’t want to get bogged down in complex orchestration.


#### What is Separation of Concerns?

In computer science, separation of concerns (SoC) is a design principle for separating a computer program into distinct sections such that each section addresses a separate concern.

The separation of concerns (SoC) is one of the most fundamental principles in software development.

It is so crucial that 2 out of 5 SOLID principles (Single Responsibility and Interface Segregation) are direct derivations from this concept.

The principle is simple: don’t write your program as one solid block, instead, break up the code into chunks that are finalized tiny pieces of the system each able to complete a simple distinct job.


#### What is a layered design and why is it important in enterprise applications?

Components within the layered architecture pattern are organized into horizontal layers, each layer performing a specific role within the application (e.g., presentation logic or business logic). Although the layered architecture pattern does not specify the number and types of layers that must exist in the pattern, most layered architectures consist of four standard layers: presentation, business, persistence, and database. In some cases, the business layer and persistence layer are combined into a single business layer, particularly when the persistence logic (e.g., SQL or HSQL) is embedded within the business layer components.  

* Overall agility - low  
Overall agility is the ability to respond quickly to a constantly changing environment. While change can be isolated through the layers of isolation feature of this pattern, it is still cumbersome and time-consuming to make changes in this architecture pattern because of the monolithic nature of most implementations as well as the tight coupling of components usually found with this pattern.  
* Ease of deployment - low  
Depending on how you implement this pattern, deployment can become an issue, particularly for larger applications. One small change to a component can require a redeployment of the entire application (or a large portion of the application), resulting in deployments that need to be planned, scheduled, and executed during off-hours or on weekends. As such, this pattern does not easily lend itself toward a continuous delivery pipeline, further reducing the overall rating for deployment.
* Testability - high  
Because components belong to specific layers in the architecture, other layers can be mocked or stubbed, making this pattern is relatively easy to test. A developer can mock a presentation component or screen to isolate testing within a business component, as well as mock the business layer to test certain screen functionality.
* Performance - low  
While it is true some layered architectures can perform well, the pattern does not lend itself to high-performance applications due to the inefficiencies of having to go through multiple layers of the architecture to fulfill a business request.
* Scalability - low  
Because of the trend toward tightly coupled and monolithic implementations of this pattern, applications build using this architecture pattern are generally difficult to scale. You can scale a layered architecture by splitting the layers into separate physical deployments or replicating the entire application into multiple nodes, but overall the granularity is too broad, making it expensive to scale.
* Ease of development - high  
Ease of development gets a relatively high score, mostly because this pattern is so well known and is not overly complex to implement. Because most companies develop applications by separating skill sets by layers (presentation, business, database), this pattern becomes a natural choice for most business-application development. The connection between a company’s communication and organization structure and the way it develops software is outlined is what is called Conway’s law.

https://www.oreilly.com/library/view/software-architecture-patterns/9781491971437/ch01.html

#### What is Dependency Injection?

Dependency Injection (DI) is a software design pattern. It allows us to develop loosely-coupled code. The intent of Dependency Injection is to make code maintainable. Dependency Injection helps to reduce the tight coupling among software components. Dependency Injection reduces the hard-coded dependencies among your classes by injecting those dependencies at run time instead of design time technically.  
It’s a way to achieve the SOLID IoC - Inversion of Control.

#### What is the DAO pattern? When and how to implement?

In computer software, a data access object (DAO) is a pattern that provides an abstract interface to some type of database or other persistence mechanism. By mapping application calls to the persistence layer, the DAO provides some specific data operations without exposing details of the database. This isolation supports the single responsibility principle. It separates what data access the application needs, in terms of domain-specific objects and data types (the public interface of the DAO), from how these needs can be satisfied with a specific DBMS, database schema, etc. (the implementation of the DAO).

The primary advantage of using data access objects is the relatively simple and rigorous separation between two important parts of an application that can but should not know anything of each other, and which can be expected to evolve frequently and independently. Changing business logic can rely on the same DAO interface, while changes to persistence logic do not affect DAO clients as long as the interface remains correctly implemented.

All details of storage are hidden from the rest of the application (see information hiding). Thus, possible changes to the persistence mechanism can be implemented by just modifying one DAO implementation while the rest of the application isn't affected. DAOs act as an intermediary between the application and the database. They move data back and forth between objects and database records. Unit testing the code is facilitated by substituting the DAO with a test double in the test, thereby making the tests independent of the persistence layer.

#### What is SOA? When to use?

Service-oriented architecture (SOA) is a style of software design where services are provided to the other components by application components, through a communication protocol over a network. A SOA service is a discrete unit of functionality that can be accessed remotely and acted upon and updated independently, such as retrieving a credit card statement online. SOA is also intended to be independent of vendors, products and technologies.

SOA can be seen as part of the continuum which ranges from the older concept of distributed computing and modular programming, through SOA, and on to practices of mashups, SaaS, and cloud computing (which some see as the offspring of SOA).

Also from https://www.guru99.com/soa-principles.html

A service-oriented architecture (SOA) is an architectural pattern in computer software design in which application components provide services to other components via a communications protocol, typically over a network. The principles of service-orientation are independent of any product, vendor or technology.


### Testing
#### What are unit test, integration test, system test, regression test, acceptance test? What is the major difference between these?

* Unit testing is a software testing method by which individual units of source code—sets of one or more computer program modules together with associated control data, usage procedures, and operating procedures—are tested to determine whether they are fit for use.  
* Integration testing is a level of software testing where individual units are combined and tested as a group. The purpose of this level of testing is to expose faults in the interaction between integrated units. Test drivers and test stubs are used to assist in Integration Testing.  
* System testing is a level of testing that validates the complete and fully integrated software product. The purpose of a system test is to evaluate the end-to-end system specifications. Usually, the software is only one element of a larger computer-based system.  
* Regression testing is defined as a type of software testing to confirm that a recent program or code change has not adversely affected existing features. Regression Testing is nothing but a full or partial selection of already executed test cases which are re-executed to ensure existing functionalities work fine.  
* Acceptance testing, a testing technique performed to determine whether or not the software system has met the requirement specifications. The main purpose of this test is to evaluate the system's compliance with the business requirements and verify if it has met the required criteria for delivery to end users.  

Usually the order is: Unit testing > Integration Testing > System Testing > Acceptance Testing

#### What is code coverage? Why is it used? How you can measure?

In computer science, test coverage is a measure used to describe the degree to which the source code of a program is executed when a particular test suite runs. A program with high test coverage, measured as a percentage, has had more of its source code executed during testing, which suggests it has a lower chance of containing undetected software bugs compared to a program with low test coverage. Many different metrics can be used to calculate test coverage; some of the most basic are the percentage of program subroutines and the percentage of program statements called during execution of the test suite.


#### What does mocking mean? How would you do it 'manually' (i. e. without using any fancy framework)?

Mocking is primarily used in unit testing. An object under test may have dependencies on other (complex) objects. To isolate the behavior of the object you want to replace the other objects by mocks that simulate the behavior of the real objects. This is useful if the real objects are impractical to incorporate into the unit test. 

In a few words, mocking is creating objects that simulate the behavior of real objects.

Without using frameworks, create a method/object that simulates the behavior of a real method/object.

#### What is a test case? What is an assertion? Give examples!

In software engineering, a test case is a specification of the inputs, execution conditions, testing procedure, and expected results that define a single test to be executed to achieve a particular software testing objective, such as to exercise a particular program path or to verify compliance with a specific requirement. Test cases underlie testing that is methodical rather than haphazard. A battery of test cases can be built to produce the desired coverage of the software being tested. Formally defined test cases allow the same tests to be run repeatedly against successive versions of the software, allowing for effective and consistent regression testing.

An assertion is a condition that must be tested to confirm conformance to a requirement.

        [TestMethod]
        public void Add(int a, int b)
        {
            // arrange
            var expected = 9;
            
            // act
            var result = app.Add(4, 5);

            // assert
            Assert.AreEqual(expected, result);
        }


#### What is TDD? What are the benefits?

TDD is a practice when a programmer writes a functional test before building a code.

Modular programming code  
Since specialists write small tests at a time, and it helps them create more modular code, otherwise they can't be tested properly. Test-driven development is the right way to learn and understand basic principles of a good modular structure. Also, TDD tools make it possible to develop a good architecture. To make code testable, it should be a modular code. The matter is that various architectural challenges may arise when tests are written.

Easy refactoring and code maintenance  
TDD provides all participants with a transparency of integration process and it also increases a security when developers want to reorganize the code that has just been written. Since TDD practices allow specialists to write modular tests before they write a final version of the code, it is much easier and faster to perform code refactoring. If a code was written a long time ago, it is rather difficult to make refactoring, but if that code was supplemented with a set of modular tests, the refactoring process becomes much simpler.

Fruitful team collaboration  
Test-driven development also makes it's contribution to the successful and more productive collaboration between developers. Team members can easily edit code that was written by other developers because if code starts functioning improperly due to new changes, tests will show it immediately. That is why test-driven development can be beneficial.

Bugs prevention  
Given that we start from writing tests, not from coding, according to TDD principles, it helps us prevent any bugs that may arise during software development. Any problems with functionality or some other failure will be detected at the very beginning of the development since we test while developing. That means, the sooner we find a bug, the faster we fix it. Common bugs can be detected immediately.

Requirements clarification  
In addition, using test-driven development methodology, we can clarify all requirements one more time and it makes our job more accurate. We can study again what input data we should provide, and see what results and if it is what the customer wants to get.

#### What are the unit testing best practices? (Eg. how many assertion should a test case contain?)

* Naming your tests  
The name of your test should consist of three parts:  
1. The name of the method being tested.
2. The scenario under which it's being tested.
3. The expected behavior when the scenario is invoked.  
* Arranging your tests
Arrange, Act, Assert is a common pattern when unit testing. As the name implies, it consists of three main actions:  
1. Arrange your objects, creating and setting them up as necessary.
2. Act on an object.
3. Assert that something is as expected.  
* Write minimally passing tests
The input to be used in a unit test should be the simplest possible in order to verify the behavior that you are currently testing.  
Why?  
Tests become more resilient to future changes in the codebase.
Closer to testing behavior over implementation.
* Avoid magic strings
Naming variables in unit tests is as important, if not more important, than naming variables in production code. Unit tests should not contain magic strings.  
Why?  
Prevents the need for the reader of the test to inspect the production code in order to figure out what makes the value special.
Explicitly shows what you're trying to prove rather than trying to accomplish.  
* Avoid logic in tests  
When writing your unit tests avoid manual string concatenation and logical conditions such as if, while, for, switch, etc.  
Why?  
Less chance to introduce a bug inside of your tests.  
Focus on the end result, rather than implementation details.  
* Prefer helper methods to setup and teardown  
If you require a similar object or state for your tests, prefer a helper method than leveraging Setup and Teardown attributes if they exist.  
Why?  
Less confusion when reading the tests since all of the code is visible from within each test.  
Less chance of setting up too much or too little for the given test.  
Less chance of sharing state between tests, which creates unwanted dependencies between them.  
* Avoid multiple asserts  
When writing your tests, try to only include one Assert per test. Common approaches to using only one assert include:  
1. Create a separate test for each assert.
2. Use parameterized tests.  
Why?  
If one Assert fails, the subsequent Asserts will not be evaluated.  
Ensures you are not asserting multiple cases in your tests.  
Gives you the entire picture as to why your tests are failing.  
* Validate private methods by unit testing public methods  
In most cases, there should not be a need to test a private method. Private methods are an implementation detail. You can think of it this way: private methods never exist in isolation. At some point, there is going to be a public facing method that calls the private method as part of its implementation. What you should care about is the end result of the public method that calls into the private one.

https://docs.microsoft.com/en-us/dotnet/core/testing/unit-testing-best-practices


#### What is arrange/act/assert pattern?

Arrange, Act, Assert is a common pattern when unit testing. As the name implies, it consists of three main actions:

* Arrange your objects, creating and setting them up as necessary.  
* Act on an object.  
* Assert that something is as expected.  
Why?  
Clearly separates what is being tested from the arrange and assert steps.  
Less chance to intermix assertions with "Act" code.  
Readability is one of the most important aspects when writing a test. Separating each of these actions within the test clearly highlight the dependencies required to call your code, how your code is being called, and what you are trying to assert. While it may be possible to combine some steps and reduce the size of your test, the primary goal is to make the test as readable as possible.


### DevOps
#### What is continuous integration? Why is CI important?

Continuous integration involves testing each modification a developer introduces to the codebase automatically, immediately when they occur. Continuous integration involves an automatic build. The automatic build runs in a precise order, coupling its operation with user authentication. A code modification fed to the codebase prompts the system to test the build for errors and crashes automatically.

Throughout the automation of processes, continuous integration eradicates manual deployment that has human errors. Automation of the self-testing build based on set criterion eliminates the need for human intervention during implementation. This facilitates the reduction of labor on redundant activities, liberating people to engage in higher order work.

#### Why are tests important in the CI workflow?

While automated testing is not strictly part of CI it is typically implied. One of the key benefits of integrating regularly is that you can detect errors quickly and locate them more easily. As each change introduced is typically small, pinpointing the specific change that introduced a defect can be done quickly.

#### Name some software that help the CI workflow!

* Jenkins
* Azure Pipelines

#### What is Continuous Delivery?

Continuous Delivery is the ability to get changes of all types—including new features, configuration changes, bug fixes and experiments—into production, or into the hands of users, safely and quickly in a sustainable way.

#### What is Continuous Deployment?

Continuous Deployment (CD) is a software release process that uses automated testing to validate if changes to a codebase are correct and stable for immediate autonomous deployment to a production environment. The software release cycle has evolved over time.
In Continuous Delivery, the deployment is manual.

#### What is DevOps?

DevOps is a set of practices that combines software development (Dev) and IT operations (Ops). It aims to shorten the systems development life cycle and provide continuous delivery with high software quality. DevOps is complementary with Agile software development; several DevOps aspects came from Agile methodology.


### Software Methodologies
#### What kind of software-lifecycle models do you know?

A software development life cycle (SDLC) model is a conceptual framework describing all activities in a software development project from planning to maintenance. This process is associated with several models, each including a variety of tasks and activities.

* Waterfall
* Agile - SCRUM
* Others: V Shaped, Prototype, Spiral, Iterative and incremental, Magic box

#### What is a UML diagram? What kind of diagram types do you know?

A UML diagram is a diagram based on the UML (Unified Modeling Language) with the purpose of visually representing a system along with its main actors, roles, actions, artifacts or classes, in order to better understand, alter, maintain, or document information about the system.

Class diagram.

#### What is a UML class diagram? What are the typical elements?

Class diagrams are one of the most useful types of diagrams in UML as they clearly map out the structure of a particular system by modeling its classes, attributes, operations, and relationships between objects.


#### What kind of design patterns do you know? Bring at least 3 examples.

* Singleton - A class of which only a single instance can exist
* Factory - Creates an instance of several derived classes
* Object Pool - Avoid expensive acquisition and release of resources by recycling objects that are no longer in use

#### What is the purpose of the Iterator Pattern?

The Iterator pattern is very commonly used in Java and .Net programming environments. This pattern is used to get a way to access the elements of a collection object in a sequential manner without any need to know its underlying representation.

The iterator pattern falls under the behavioral pattern category.


#### What do you know about the SOLID principles?

SOLID is an acronym for 5 important design principles when doing OOP (Object Oriented Programming). These 5 principles were introduced by Robert C. Martin (Uncle Bob), in his 2000 paper Design Principles and Design Patterns.

* Single-responsibility principle
A class should only have a single responsibility, that is, only changes to one part of the software's specification should be able to affect the specification of the class.
* Open–closed principle
"Software entities ... should be open for extension, but closed for modification."
* Liskov substitution principle
"Objects in a program should be replaceable with instances of their subtypes without altering the correctness of that program." Or, you giva a dog a command and the dog commands its feet. You don't command the feet of the dog directly.
* Interface segregation principle
"Many client-specific interfaces are better than one general-purpose interface."
* Dependency inversion principle
One should "depend upon abstractions, not concretions."


#### How would you separate data storage code and business logic code (which uses stored data) in an application?

* Data Access Layer (usually a library that has the controllers to access the DB)
* Business Logic Layer (the part that manipulates the data from the Data Access Layer for other parts of the program)

## Computer science

### Data Structures
#### What is the difference between Stack and Queue data structure?

|                         Stack                        |                                                    Queue                                                    |
|:----------------------------------------------------:|:-----------------------------------------------------------------------------------------------------------:|
|    Based on the LIFO principle - last in first out   |                               Based on the FIFO principle - first in first out                              |
|     Insert and delete only from one end - the top    |                               Insert (rear) and delete (front) - opposite ends                              |
|                 Insert is called Push                |                                           Insert is called Enqueue                                          |
|                 Delete is called Pop                 |                                           Delete is called Dequeue                                          |
| One pointer - the top - the last element in the list | Two pointers - the front - points to the first inserted elem  - the rear - points to the last inserted elem |
|             Used in recursion algorithms             |                                        Used in sequential mechanisms                                        |


#### What is a graph? What are simple graphs? What are directed graphs? What are weighted graphs?

In computer science, a graph is an abstract data type that is meant to implement the undirected graph and directed graph concepts from the field of graph theory within mathematics.

A graph data structure consists of a finite (and possibly mutable) set of vertices (also called nodes or points), together with a set of unordered pairs of these vertices for an undirected graph or a set of ordered pairs for a directed graph. These pairs are known as edges (also called links or lines), and for a directed graph are also known as arrows. The vertices may be part of the graph structure, or may be external entities represented by integer indices or references.

A graph data structure may also associate to each edge some edge value, such as a symbolic label or a numeric attribute (cost, capacity, length, etc.).

* Simple graph - just nodes and edges  
* Directed graph - nodes and edges that have a direction  
* Weighted graph - nodes and edges that have a number (weight) associated with it (km, cost, etc.)
* Finite and Infinite graphs
* Multi graph
* Null graph
* Others: Complete, Pseudo, REgular, Bipartite, Labelled, Digraph


#### What are trees? What are binary trees? What are binary search trees?

In computer science, a tree is a widely used abstract data type that simulates a hierarchical tree structure, with a root value and subtrees of children with a parent node, represented as a set of linked nodes.

A tree data structure can be defined recursively as a collection of nodes (starting at a root node), where each node is a data structure consisting of a value, together with a list of references to nodes (the "children"), with the constraints that no reference is duplicated, and none points to the root.

Binary tree - a tree data structure in which each node has at most two children, which are referred to as the left child and the right child.

Binary search tree - a node-based binary tree data structure which has the following properties:
* The left subtree of a node contains only nodes with keys lesser than the node’s key.
* The right subtree of a node contains only nodes with keys greater than the node’s key.
* The left and right subtree each must also be a binary search tree.

#### How can you store graphs in programs? What are the advantages/disadvantages per each?

There are three ways to store a graph in memory:

* Nodes as objects and edges as pointers
* A matrix containing all edge weights between numbered node x and node y
* A list of edges between numbered nodes

One way to analyze these is in terms of memory and time complexity (which depends on how you want to access the graph).

Storing nodes as objects with pointers to one another.  
The memory complexity for this approach is O(n) because you have as many objects as you have nodes. The number of pointers (to nodes) required is up to O(n^2) as each node object may contain pointers for up to n nodes.
The time complexity for this data structure is O(n) for accessing any given node.  

Storing a matrix of edge weights.  
This would be a memory complexity of O(n^2) for the matrix.
The advantage with this data structure is that the time complexity to access any given node is O(1).
Depending on what algorithm you run on the graph and how many nodes there are, you'll have to choose a suitable representation.

https://stackoverflow.com/questions/3287003/three-ways-to-store-a-graph-in-memory-advantages-and-disadvantages


#### What are graph traversal algorithms? What is BFS, how does it work? What is DFS, how does it work?

In computer science, graph traversal (also known as graph search) refers to the process of visiting (checking and/or updating) each vertex in a graph. Such traversals are classified by the order in which the vertices are visited. Tree traversal is a special case of graph traversal.

A breadth-first search (BFS) is another technique for traversing a finite graph. BFS visits the sibling vertices before visiting the child vertices, and a queue is used in the search process. This algorithm is often used to find the shortest path from one vertex to another.

A depth-first search (DFS) is an algorithm for traversing a finite graph. DFS visits the child vertices before visiting the sibling vertices; that is, it traverses the depth of any particular path before exploring its breadth. A stack (often the program's call stack via recursion) is generally used when implementing the algorithm.
The algorithm begins with a chosen "root" vertex; it then iteratively transitions from the current vertex to an adjacent, unvisited vertex, until it can no longer find an unexplored vertex to transition to from its current location. The algorithm then backtracks along previously visited vertices, until it finds a vertex connected to yet more uncharted territory. It will then proceed down the new path as it had before, backtracking as it encounters dead-ends, and ending only when the algorithm has backtracked past the original "root" vertex from the very first step.

#### How does dictionary work?

In computing, a hash table (hash map) is a data structure that implements an associative array abstract data type, a structure that can map keys to values. A hash table uses a hash function to compute an index, also called a hash code, into an array of buckets or slots, from which the desired value can be found. During lookup, the key is hashed and the resulting hash indicates where the corresponding value is stored.

Ideally, the hash function will assign each key to a unique bucket, but most hash table designs employ an imperfect hash function, which might cause hash collisions where the hash function generates the same index for more than one key. Such collisions are always accommodated in some way.

In a well-dimensioned hash table, the average cost (number of instructions) for each lookup is independent of the number of elements stored in the table. Many hash table designs also allow arbitrary insertions and deletions of key-value pairs, at (amortized) constant average cost per operation.

In many situations, hash tables turn out to be on average more efficient than search trees or any other table lookup structure. For this reason, they are widely used in many kinds of computer software, particularly for associative arrays, database indexing, caches, and sets.


#### Why is it important for keys in a hashmap to have an immutable type? (Consider string for example.)

If immutable, the object's hashcode wont change and it allows caching the hashcode of different keys which makes the overall retrieval process very fast. Also, if you put/add a key with a certain hashmap, you need to retrieve it based on the same hashmap - and immutable objects are safer.

### Algorithms
#### What is QuickSort? Describe the main logic of this sorting algorithm.

Quick Sort is a divide and conquer algorithm. It creates two empty arrays to hold elements less than the pivot value and elements greater than the pivot value, and then recursively sort the sub arrays. There are two basic operations in the algorithm, swapping items in place and partitioning a section of the array.

Quick Sort Algorithm: Steps on how it works:  
1. Find a “pivot” item in the array. This item is the basis for comparison for a single round.
2. Start a pointer (the left pointer) at the first item in the array.
3. Start a pointer (the right pointer) at the last item in the array.
4. While the value at the left pointer in the array is less than the pivot value, move the left pointer to the right (add 1). Continue until the value at the left pointer is greater than or equal to the pivot value.
5. While the value at the right pointer in the array is greater than the pivot value, move the right pointer to the left (subtract 1). Continue until the value at the right pointer is less than or equal to the pivot value.
6. If the left pointer is less than or equal to the right pointer, then swap the values at these locations in the array.
7. Move the left pointer to the right by one and the right pointer to the left by one.
8. If the left pointer and right pointer don’t meet, go to step 1.


## Software design

### Security

#### What is OAuth2?

OAuth 2 is an authorization framework that enables applications to obtain limited access to user accounts on an HTTP service, such as Facebook, GitHub, and DigitalOcean. **It works by delegating user authentication to the service that hosts the user account, and authorizing third-party applications to access the user account.** OAuth 2 provides authorization flows for web and desktop applications, and mobile devices.


#### What is Basic Authentication?

The concept of Basic Authentication is present in different technologies and usually represents a simple username and password combination that allows access for that user.


#### What is CORS, why it’s needed in browsers?

Cross-Origin Resource Sharing (CORS) is a mechanism that uses additional HTTP headers to tell browsers to give a web application running at one origin, access to selected resources from a different origin. A web application executes a cross-origin HTTP request when it requests a resource that has a different origin (domain, protocol, or port) from its own.

An example of a cross-origin request: the front-end JavaScript code served from https://domain-a.com uses XMLHttpRequest to make a request for https://domain-b.com/data.json.

For security reasons, browsers restrict cross-origin HTTP requests initiated from scripts. For example, XMLHttpRequest and the Fetch API follow the same-origin policy. This means that a web application using those APIs can only request resources from the same origin the application was loaded from unless the response from other origins includes the right CORS headers.

The CORS mechanism supports secure cross-origin requests and data transfers between browsers and servers. Modern browsers use CORS in APIs such as XMLHttpRequest or Fetch to mitigate the risks of cross-origin HTTP requests.


#### How can you initialize a CSRF attack?

Cross site request forgery (CSRF), also known as XSRF, Sea Surf or Session Riding, is an attack vector that tricks a web browser into executing an unwanted action in an application to which a user is logged in.

A successful CSRF attack can be devastating for both the business and user. It can result in damaged client relationships, unauthorized fund transfers, changed passwords and data theft—including stolen session cookies.

CSRFs are typically conducted using malicious social engineering, such as an email or link that tricks the victim into sending a forged request to a server. As the unsuspecting user is authenticated by their application at the time of the attack, it’s impossible to distinguish a legitimate request from a forged one.


#### What is JWT used for? Where to store it on client side?

A JWT technically is a mechanism to verify the owner of some JSON data. It’s an encoded string, which is URL safe, that can contain an unlimited amount of data (unlike a cookie), and it’s cryptographically signed.

When a server receives a JWT, it can guarantee the data it contains can be trusted because it’s signed by the source. No middleman can modify a JWT once it’s sent.

It’s important to note that a JWT guarantees data ownership but not encryption; the JSON data you store into a JWT can be seen by anyone that intercepts the token, as it’s just serialized, not encrypted.


A JWT needs to be stored in a safe place inside the user’s browser.

If you store it inside localStorage, it’s accessible by any script inside your page (which is as bad as it sounds, as an XSS attack can let an external attacker get access to the token).

Don’t store it in local storage (or session storage). If any of the third-party scripts you include in your page gets compromised, it can access all your users’ tokens.

The JWT needs to be stored inside an httpOnly cookie, a special kind of cookie that’s only sent in HTTP requests to the server, and it’s never accessible (both for reading or writing) from JavaScript running in the browser.


### Threaded programming

#### When do you need to use threads in an application?

* Faster processing - Ahsaring the processing taks between threads as opposed to only executing them on one reduces the time proportionally to the number of threads. At the same time, threads are sometimes called lightweight processes because they have their own stack but can access shared data. Because threads share the same address space as the process and other threads within the process, the operational cost of communication between the threads is low, which is an advantage.
* Async processing - where the UI layer needs to not be blocked by expensive operations and thus make the app seem unresponsive


#### What is a daemon thread?

The Daemon thread is a low priority thread that runs in background to perform tasks such as garbage collection.

Properties:  
* They can not prevent the JVM from exiting when all the user threads finish their execution.
* JVM terminates itself when all user threads finish their execution. If the JVM finds a running daemon thread, it terminates the thread and after that shuts itself down. The JVM does not care whether Daemon thread is running or not.
* It is an utmost low priority thread.


#### What is the difference between concurrent and parallel execution of code?

* Concurrency  
It means that an application is making progress on more than one task at the same time (concurrently). Well, if the computer only has one CPU the application may not make progress on more than one task at exactly the same time, but more than one task is being processed at a time inside the application. It does not completely finish one task before it begins the next. Instead, the CPU switches between the different tasks until the tasks are complete.

* Parallelism  
It means that an application splits its tasks up into smaller subtasks which can be processed in parallel, for instance on multiple CPUs at the exact same time.


#### What is the most important problem developers are faced when using threads?

Shared Access to Data  
If two threads access a shared variable without any kind of guard, writes to that variable can overlap. Let’s say both threads add 1 to the same memory location; they do this by reading the value in the memory location into a register, incrementing it, then writing it back. Thread 1 (T1) reads the value (let’s say ‘0’ initially), increments it, and writes 1 back. After T1 has read it, but before it writes the value back, T2 reads the 0 value, and then writes 1 back after T1. So despite two increments, the value is 1, when it should be 2.

The access has to be atomic, i.e., done in one operation, in order to prevent overlapping writes. This can be done in a number of ways. The .NET framework has an Interlocked Class with atomic increment and decrement methods; Java has java.util.concurrent.atomic.AtomicInteger with increment and decrement methods.


#### In what kind of situations can deadlocks occur?

Deadlock can occur in a situation when a thread is waiting for an object lock, that is acquired by another thread and second thread is waiting for an object lock that is acquired by first thread. Since, both threads are waiting for each other to release the lock, the condition is called deadlock.


#### What are possible ways to prevent deadlocks from occurring?

Lock Ordering
Deadlock occurs when multiple threads need the same locks but obtain them in different order.

If you make sure that all locks are always taken in the same order by any thread, deadlocks cannot occur. Look at this example:

Thread 1:

  lock A 
  lock B


Thread 2:

   wait for A
   lock C (when A locked)


Thread 3:

   wait for A
   wait for B
   wait for C
If a thread, like Thread 3, needs several locks, it must take them in the decided order. It cannot take a lock later in the sequence until it has obtained the earlier locks.

For instance, neither Thread 2 or Thread 3 can lock C until they have locked A first. Since Thread 1 holds lock A, Thread 2 and 3 must first wait until lock A is unlocked. Then they must succeed in locking A, before they can attempt to lock B or C.

Lock ordering is a simple yet effective deadlock prevention mechanism. However, it can only be used if you know about all locks needed ahead of taking any of the locks. This is not always the case.

Lock Timeout
Another deadlock prevention mechanism is to put a timeout on lock attempts meaning a thread trying to obtain a lock will only try for so long before giving up. If a thread does not succeed in taking all necessary locks within the given timeout, it will backup, free all locks taken, wait for a random amount of time and then retry. The random amount of time waited serves to give other threads trying to take the same locks a chance to take all locks, and thus let the application continue running without locking.

Here is an example of two threads trying to take the same two locks in different order, where the threads back up and retry:

Thread 1 locks A
Thread 2 locks B

Thread 1 attempts to lock B but is blocked
Thread 2 attempts to lock A but is blocked

Thread 1's lock attempt on B times out
Thread 1 backs up and releases A as well
Thread 1 waits randomly (e.g. 257 millis) before retrying.

Thread 2's lock attempt on A times out
Thread 2 backs up and releases B as well
Thread 2 waits randomly (e.g. 43 millis) before retrying.
In the above example Thread 2 will retry taking the locks about 200 millis before Thread 1 and will therefore likely succeed at taking both locks. Thread 1 will then wait already trying to take lock A. When Thread 2 finishes, Thread 1 will be able to take both locks too (unless Thread 2 or another thread takes the locks in between).

An issue to keep in mind is, that just because a lock times out it does not necessarily mean that the threads had deadlocked. It could also just mean that the thread holding the lock (causing the other thread to time out) takes a long time to complete its task.

Additionally, if enough threads compete for the same resources they still risk trying to take the threads at the same time again and again, even if timing out and backing up. This may not occur with 2 threads each waiting between 0 and 500 millis before retrying, but with 10 or 20 threads the situation is different. Then the likeliness of two threads waiting the same time before retrying (or close enough to cause problems) is a lot higher.


#### What does critical section or critical region mean in the context of concurrent programming?

In concurrent programming, concurrent accesses to shared resources can lead to unexpected or erroneous behavior, so parts of the program where the shared resource is accessed need to be protected in ways that avoid the concurrent access. This protected section is the critical section or critical region.