# Enterprise module (C# branch)

### ASP.NET Core, WCF

#### What Is the difference between .NET Core and .NET Standard? How do they relate to “classic” .NET?

.NET Framework is the original implementation of .NET. It supports running websites, services, desktop apps, and more on Windows.

.NET Core is a cross-platform implementation for running websites, services, and console apps on Windows, Linux, and macOS. .NET Core is open source on GitHub.

.NET Standard is a specification that describes specific feature implementations that a .NET Runtime like .NET Core, .NET Framework, Mono, Xamarin or Unity has to implement - at minimum - to support that version of the Standard.

For library authors targeting .NET Standard provides the same feature set across all supported platforms - if it compiles to .NET Standard it'll very likely run on those frameworks. For consumers it's an easy way to tell which platforms a .NET Standard component can work on.

In concrete terms this means that when you build a library you can target .NET Standard and expect the compiled assembly/package to work on any of the platforms that support that version of .NET Standard.

If you're building libraries, you'll want to target the lowest version of .NET Standard that your library can work with. But for most intents and purposes I think that .NET Standard 2.0 is the new baseline for anything useful going forward.

https://weblog.west-wind.com/posts/2019/Feb/19/Using-NET-Standard-with-Full-Framework-NET

I used it once when upgrading an app from .NET Framework to .NET Core. The library was upgraded to .NET Standard first so that it was supported by both .NET Framework and .NET Core and the rest of the modules were upgraded gradually.


#### What is ASP.NET MVC?

MVC is a design pattern used to decouple user-interface (view), data (model), and application logic (controller). This pattern helps to achieve separation of concerns. ASP.NET has it's own implementation of this pattern, including a quick start project template.


#### Can you explain Model, Controller and View in MVC?

Using the MVC pattern for websites, requests are routed to a Controller that is responsible for working with the Model to perform actions and/or retrieve data. The Controller chooses the View to display, and provides it with the Model. The View renders the final page, based on the data in the Model.


#### Explain the page lifecycle of MVC.

Http Request > HttpApplication Processing Pipeline > Http Response

Inside the pipeline we have the Routing and the MVC handler.

Inside the MVC Handler, the request goes through the following stages:

Controller Creation > Authentication and Authorization > Model Binding > Action Method Invocation > Result Execution (View, etc.)

https://docs.microsoft.com/en-us/aspnet/mvc/overview/getting-started/lifecycle-of-an-aspnet-mvc-5-application


#### What is Razor View Engine?

Razor View engine is a markup syntax which helps us to write HTML and server-side code in web pages using C# or VB.NET. It is server-side markup language however it is not at all a programming language.

Razor is a templating engine and ASP.NET MVC has implemented a view engine which allows us to use Razor inside of an MVC application to produce HTML. However, Razor does not have any ties with ASP.NET MVC.

Now, Razor Syntax is compact which minimizes the characters to be used, however it is also easy to learn.


#### What you mean by Routing in MVC?

ASP.NET introduced Routing to eliminate the needs of mapping each URL with a physical file. Routing enables us to define a URL pattern that maps to the request handler. This request handler can be a file or class. In ASP.NET MVC, it is the Controller class and Action method.


#### What is Layout in MVC?

An application may contain common parts in the UI which remains the same throughout the application such as the logo, header, left navigation bar, right bar or footer section. ASP.NET MVC introduced a Layout view which contains these common UI parts, so that we don't have to write the same code in every page.


#### What ConfigureServices() method does in Startup.cs?

The ConfigureServices method is:

* Optional.
* Called by the host before the Configure method to configure the app's services.
* Where configuration options are set by convention.  

The host may configure some services before Startup methods are called. 

For features that require substantial setup, there are Add{Service} extension methods on IServiceCollection. For example, AddDbContext, AddDefaultIdentity, AddEntityFrameworkStores, and AddRazorPages


#### What Configure() method does in Startup.cs?

The Configure method is used to specify how the app responds to HTTP requests. The request pipeline is configured by adding middleware components to an IApplicationBuilder instance.

        public class Startup
        {
            public Startup(IConfiguration configuration)
            {
                Configuration = configuration;
            }

            public IConfiguration Configuration { get; }

            public void ConfigureServices(IServiceCollection services)
            {
                services.AddRazorPages();
            }

            public void Configure(IApplicationBuilder app, IWebHostEnvironment env)
            {
                if (env.IsDevelopment())
                {
                    app.UseDeveloperExceptionPage();
                }
                else
                {
                    app.UseExceptionHandler("/Error");
                    app.UseHsts();
                }

                app.UseHttpsRedirection();
                app.UseStaticFiles();

                app.UseRouting();

                app.UseAuthorization();

                app.UseEndpoints(endpoints =>
                {
                    endpoints.MapRazorPages();
                });
            }
        }


#### What is wwwroot folder in ASP.NET Core?

Static files, such as HTML, CSS, images, and JavaScript, are assets an ASP.NET Core app serves directly to clients by default.
Static files are stored within the project's web root directory. The default directory is {content root}/wwwroot, but it can be changed with the UseWebRoot method.

#### What’s the usage of [InternalsVisibleTo] attribute? What are pros and cons of it?

The InternalsVisibleTo attribute is a well-known attribute for testing assemblies. The internal methods of an assembly become visible to the test project. This allows you to test the internal methods without using reflection, so your tests are more maintainable.

Pros  
* Allows your test libraries to access internal classes and methods for additional testing and coverage
* Keeps your public API limited to what you want to publish
* Provides greater flexibility for internal refactoring and backwards compatibility
* Reduces the surface area of your public API  

Cons  
* Easily abused, so things usually marked “private” are now marked “internal”
* Potential loss of encapsulation
* Decision about what should be public could be wrong
* Essentially two levels of “public” visibility that have to be managed
* Enforces bi-directional dependencies between assemblies


#### Explain what is WCF?

Windows Communication Foundation (WCF) is a framework for building service-oriented applications. Using WCF, you can send data as asynchronous messages from one service endpoint to another. A service endpoint can be part of a continuously available service hosted by IIS, or it can be a service hosted in an application. An endpoint can be a client of a service that requests data from a service endpoint. The messages can be as simple as a single character or word sent as XML, or as complex as a stream of binary data.  

A few sample scenarios include:
* A secure service to process business transactions.
* A service that supplies current data to others, such as a traffic report or other monitoring service.
* A chat service that allows two people to communicate or exchange data in real time.
* A dashboard application that polls one or more services for data and presents it in a logical presentation.


#### Mention what is the endpoint in WCF and what are the three major points in WCF?

WCF offers its services to its clients using an endpoint. An endpoint comprises three key elements, the address, binding and contract. WCF endpoints provide the necessary resources and directions, which help clients to communicate with the various services WCF offers.

* Address - Specifies the location of the service which will be like http://Myserver/MyService.Clients will use this location to communicate with the service.
* Binding - Specifies how the two parties will communicate in terms of transport, encoding and protocols
* Contract - Specifies the interface between client and the server. It's a simple interface with some attributes.


#### Object Relational Mapping, Entity Framework

#### What is an ORM? What are benefits, when to use?

Object-relational-mapping is the idea of being able to write queries using the object-oriented paradigm of your preferred programming language.
Long story short, we are trying to interact with our database using our language of choice instead of SQL.  
Here’s where the Object-relational-mapper comes in. When most people say “ORM” they are referring to a library that implements this technique.

Benefits  
* You get to write in the language you are already using
* It abstracts away the database system so that switching from MySQL to PostgreSQL, or others, is easy
* Depending on the ORM you get a lot of advanced features out of the box, such as support for transactions, connection pooling, migrations, seeds, streams, and others
* Many of the queries you write will perform better than if you wrote them yourself

#### What is Entity Framework? What are the advantages, limitations?

Entity Framework Core is a modern object-database mapper for .NET. It supports LINQ queries, change tracking, updates, and schema migrations. EF Core works with many databases, including SQL Database (on-premises and Azure), SQLite, MySQL, PostgreSQL, and Azure Cosmos DB.

Advantages

* One common syntax (LINQ) for all object queries whether it is database or not , Pretty fast if used as intended , easy to implement SoC , less coding required to accomplish complex tasks.
* Its fast and straight forward using LINQ/FE objects For Add/Modify/Delete/Update.
* Easy to map business objects (with drag & drop tables on environment). It keeps a good performance when you work with a small / middle domain model.

Disadvantages
* You have to think in a non-traditional way of handling data , not available for every database.
* If there is any schema change in database FE won’t work!!! You have to update the schema in solution as well!!!
* It's limited when you work with a huge domain model. -Scalability.


#### What is lazy loading?

Lazy loading is the process whereby an entity or collection of entities is automatically loaded from the database the first time that a property referring to the entity/entities is accessed. Lazy loading means delaying the loading of related data, until you specifically request for it.


#### What is the difference between code first and DB first approach?

Code First Approach

In code first approach we will first create entity classes with properties defined in it. Entity framework will create the database and tables based on the entity classes defined. So database is generated from the code. When the dot net code is run database will get created. 

Advantages  
* You can create  the database and tables from your business objects.
* You can specify which related collections are to be eager loaded, or not be serialized at all.
* Database version control.
* Good for small applications.  

Disadvantages  
* You have to write everything related to database in the visual studio code.
* For stored procedures you have to map stored procedure using Fluent API and write Stored Procedure inside the code.
* If you want to change anything in the database tables you to make changes in the entity classes in the code file and run the update-database from the  package manager console.
* Not preferred for Data intensive applications.  

Database First Approach

In this approach Database and tables are created first. Then you create entity Data Model using the created database.
 
Advantages  

* Simple to create the data model
* Graphical  user interface.
* Mapping and creation of keys and relationships are easy as you need not have to write any code.
* Preferred for data intense and large applications

Disadvantages  
* Using an existing database to generate a .edmx model file and the associated code models results in a giant pile of auto generated code.
* When you need to add any functionality to generated model you have to extend the model class generated. 


#### What is a migration script?

In real world projects, data models change as features get implemented: new entities or properties are added and removed, and database schemas need to be changed accordingly to be kept in sync with the application. The migrations feature in EF Core provides a way to incrementally update the database schema to keep it in sync with the application's data model while preserving existing data in the database.

At a high level, migrations function in the following way:

1. When a data model change is introduced, the developer uses EF Core tools to add a corresponding migration describing the updates necessary to keep the database schema in sync. 
2. EF Core compares the current model against a snapshot of the old model to determine the differences, and generates migration source files; the files can be tracked in your project's source control like any other source file. The migration script is one of these files.
3. Once a new migration has been generated, it can be applied to a database in various ways. EF Core records all applied migrations in a special history table, allowing it to know which migrations have been applied and which haven't.


#### What is a navigation property?

Navigation properties are Entity Framework's way of representing Foreign Key relationships inside the database. Navigation properties allow you to define relationships between entities (rows in your database) in a way that makes sense in an object oriented language.


#### Name 3 different attributes used in EF Core, what can they do for you?

Configuration enables you to override EF Core's default behaviour. Configuration can be applied in two ways, using the Fluent API, and through DataAnnotation attributes.

Attributes are a kind of tag that you can place on a class or property to specify metadata about that class or property. Entity Framework Core makes use of attributes defined in the System.ComponentModel.DataAnnotations.Schema and System.ComponentModel.DataAnnotations namespaces.

ForeignKey  
* Specifies the property is used as a foreign key in a relationship.  
Required  
* Specifies that the property's value is required.  
MaxLength  
* Sets the maximum allowed length of the property value (string or array).

#### What is Signal R?

ASP.NET Core SignalR is an open-source library that simplifies adding real-time web functionality to apps. Real-time web functionality enables server-side code to push content to clients instantly.

Good candidates for SignalR:

* Apps that require high frequency updates from the server. Examples are gaming, social networks, voting, auction, maps, and GPS apps.  
* Dashboards and monitoring apps. Examples include company dashboards, instant sales updates, or travel alerts.  
* Collaborative apps. Whiteboard apps and team meeting software are examples of collaborative apps.
* Apps that require notifications. Social networks, email, chat, games, travel alerts, and many other apps use notifications.

Here are some features of SignalR for ASP.NET Core:

* Handles connection management automatically.
* Sends messages to all connected clients simultaneously. For example, a chat room.
* Sends messages to specific clients or groups of clients.
* Scales to handle increasing traffic.

SignalR supports the following techniques for handling real-time communication (in order of graceful fallback):

* WebSockets
* Server-Sent Events
* Long Polling  

SignalR automatically chooses the best transport method that is within the capabilities of the server and client.

#### What is GraphQL?

GraphQL is a query language and server-side runtime for application programming interfaces (APIs) that prioritizes giving clients exactly the data they request and no more.

GraphQL is designed to make APIs fast, flexible, and developer-friendly. It can even be deployed within an integrated development environment (IDE) known as GraphiQL. As an alternative to REST, GraphQL lets developers construct requests that pull data from multiple data sources in a single API call. 

Additionally, GraphQL gives API maintainers the flexibility to add or deprecate fields without impacting existing queries. Developers can build APIs with whatever methods they prefer, and the GraphQL specification will ensure they function in predictable ways to clients.

The first example shows how a client can construct a GraphQL query, asking an API to return specific fields in a shape you’ve specified.

        {
        me {
            name
        }
        }

A GraphQL API would return a result like this in JSON format:

        {
        "me": {
            "name": "Dorothy"
        }
        }

A client can also pass arguments as part of a GraphQL query, as seen in this example:

        {
        human(id: "1000") {
            name
            location
        }
        }

The result:

        {
        "data": {
            "human": {
            "name": "Dorothy,
            "location": "Kansas"
            }
        }
        }

So this query:

        query HeroComparison($first: Int = 3) {
        leftComparison: hero(location: KANSAS) {
            ...comparisonFields
        }
        rightComparison: hero(location: OZ) {
            ...comparisonFields
        }
        }

        fragment comparisonFields on Character {
        name
        friendsConnection(first: $first) {
            totalCount
            edges {
            node {
                name
            }
            }
        }
        }
    
Might produce this result:

        {
        "data": {
            "leftComparison": {
            "name": "Dorothy",
            "friendsConnection": {
                "totalCount": 4,
                "edges": [
                {
                    "node": {
                    "name": "Aunt Em"
                    }
                },
                {
                    "node": {
                    "name": "Uncle Henry"
                    }
                },
                {
                    "node": {
                    "name": "Toto"
                    }
                }
                ]
            }
            },
            "rightComparison": {
            "name": "Wizard",
            "friendsConnection": {
                "totalCount": 3,
                "edges": [
                {
                    "node": {
                    "name": "Scarecrow"
                    }
                },
                {
                    "node": {
                    "name": "Tin Man"
                    }
                },
                {
                    "node": {
                    "name": "Lion"
                    }
                }
                ]
            }
            }
        }
        }
