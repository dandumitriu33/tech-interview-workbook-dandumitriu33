# Programming Basics questions

## Computer science

### Data structures

#### What is the purpose of a list (array in some programming languages) data structure? Name some methods of it!

Lists are one of the most versatile data structures. They are mutable as opposed to strings, can be indexed, sliced, sorted and iterated. In most programming languages, arrays contain data of the same type only. In Python lists can contain multiple types of data combined. Arrays have a special module in Python that has to be imported (from array import *).

- lst.sort() and sorted() - will sort the elements in the list in place or in a copy respectively  
- lst.append() - adds an element at the end of the list  
- lst.insert(0, 'a') - inserts 'a' at index 0  
- lst.remove(value) - removes the first instance of that value  
- lst.reverse() - reverses the list in place and returns None  

#### What is the difference between a list/array and a set?

A list can mainly contain multiple items with the same value while sets can contain only unique values, duplicates are removed.
Lists have certain operations that can be performed on them, but not on sets, such as sort, find, count, reverse. Sets also 
have specific operations that can be performed only on them, such as: intersection, union, difference, symmetric difference.

#### What is the purpose and methods of a dictionary/map data structure?

The dictionary's main characteristic is that it has a unique set of keys, which can have values assigned to them. It allows 
you to store and retrieve elements by referencing a key. As dictionaries are referenced by key, they have very fast lookups. 
As they are primarily used for referencing items by key, they are not sorted.

### Algorithms

#### Fibonacci sequences. Write a method (or pseudo code), that generates the Fibonacci sequences.

        def fibonacci_sequence():
            user_number = int(input('How many Fibonacci numbers do you want to know? '))
            fibonacci_numbers = []
            first_number = 0
            second_number = 1
            fibonacci_numbers.append(first_number)
            fibonacci_numbers.append(second_number)

            # as 0 and 1 are already 2 numbers in the list, the next section will
            # add the remaining numbers (up to user_number) of the sequence in the list

            i = 0
            while i < user_number - 2:
                new_number = fibonacci_numbers[-1] + fibonacci_numbers[-2]
                fibonacci_numbers.append(new_number)
                i += 1
            return fibonacci_numbers


        print(fibonacci_sequence())

#### How do you find a max value in a list/array if you can’t use any built-in functions?

One way is to assign the maximum to the first element and then pass through the list once, comparing the
maximum to each element. If the element in the list is greater, then the maximum will take the element's value
and continue.

        numbers = [5, 20, 14, 2, 31]

        
        def find_max(arr):
            max_of_list = arr[0]
            for i in arr:
                if i > max_of_list:
                    max_of_list = i
            return max_of_list


        print(find_max(numbers))

        # 31


#### How do you find the average of values in a list/array if you can’t use any built-in functions?

A simple way to do it would be to add the values of all the elements in the list and then divide it 
by the total number of elements. 

        numbers = [5, 20, 14, 2, 31]


        def find_average(arr):
            counter = 0
            sum = 0
            for i in arr:
                sum += i
                counter += 1
            return sum/counter


        print(find_average(numbers))

        # 14.4


#### What do we call an *in-place* sort?

The in-place sort is the operation that modifies the data without creating a separate sorted copy along
side the original. It sorts it in place, it manipulates the original.

        numbers = [5, 20, 14, 2, 31]

        numbers.sort()
        print(numbers)

        # [2, 5, 14, 20, 31]


#### Explain an algorithm which sorts a list!

Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent 
elements if they are in the wrong order. It loops thorugh the list n times where n is the number
of elements. In the improved version, the algorithm stops after it runs a pass where it doesn't 
perform a swap.

        numbers = [5, 20, 14, 2, 31]


        def bubble_sort(arr):
            n = len(arr)
            for i in range(n):
                for j in range(0, n-i-1):
                    if arr[j] > arr[j+1]:
                        arr[j], arr[j+1] = arr[j+1], arr[j]
            return arr


        print(bubble_sort(numbers))

        # [2, 5, 14, 20,31]


        numbers = [5, 20, 14, 2, 31]


        def bubble_sort(arr):
            n = len(arr)
            for i in range(n):
                swapped = False
                for j in range(0, n-i-1):
                    if arr[j] > arr[j+1]:
                        arr[j], arr[j+1] = arr[j+1], arr[j] 
                        swapped = True
                if swapped is False:
                    break
            return arr


        print(bubble_sort(numbers))

        # [2, 5, 14, 20, 31]


### Programming paradigms - procedural


#### What is the call stack?

In computer science, a call stack is a stack data structure that stores information about the active subroutines 
of a computer program. This kind of stack is also known as an execution stack, program stack, control stack, 
run-time stack, or machine stack, and is often shortened to just "the stack".  

The primary purpose of a call stack is to store *the return addresses*. When a subroutine is called, the location 
(address) of the instruction at which the calling routine can later resume needs to be saved somewhere. One benefit
is that each task can have its own stack, and thus the subroutine can be thread-safe, that is, can be active 
simultaneously for different tasks doing different things. Another benefit is that by providing reentrancy, 
recursion is automatically supported.


#### What is “Stack overflow”?

In software, a stack overflow occurs if the call stack pointer exceeds the stack bound. The call stack may consist 
of a limited amount of address space, often determined at the start of the program. The size of the call stack depends 
on many factors, including the programming language, machine architecture, multi-threading, and amount of available memory. 
When a program attempts to use more space than is available on the call stack (that is, when it attempts to access memory 
beyond the call stack's bounds, which is essentially a buffer overflow), the stack is said to overflow, typically resulting 
in a program crash.

Stack Overflow https://stackoverflow.com/ is a question and answer site for professional and enthusiast programmers. It 
features questions and answers on a wide range of topics in computer programming.


#### What are the main parts of a function?

1. Keyword **def** marks the start of function header.
2. A function name to uniquely identify it. Function naming follows the same rules of writing identifiers in Python.
3. Parameters (arguments) through which we pass values to a function. They are optional.
4. A colon (:) to mark the end of function header.
5. Optional documentation string (docstring) to describe what the function does.
6. One or more valid python statements that make up the function body. Statements must have same indentation level (usually 4 spaces).
7. An optional return statement to return a value from the function.

        def function_named_greet(name_parameter):
            """This function greets
            the person passed in as
            parameter"""
            print("Hello, " + name + ". Good morning!")
            return 'Greet completed.'

### Programming languages - Python  
#### How do you use a dictionary in Python?

A dictionary is an example of a **key value store** also known as **Mapping** in Python. It allows you to store and retrieve
elements by referencing a key. As dictionaries are referenced by key, they have very fast lookups. As they are
primarily used for referencing items by key, they are not sorted.

        example_dictionary = {1: 'abc', 2: 'def', 3: 'xyz'}
        print(example_dictionary[3])

        example_dictionary[4] = 'www'
        print(example_dictionary)

        # xyz
        # {1: 'abc', 2: 'def', 3: 'xyz', 4: 'www'}

#### What does it mean that an object is immutable in Python?

Immutable variable values can't be changed once they are created. Immutable datatypes: int, float, str, tuple and frozensets.

        example_string = 'abc'
        example_string[0] = 'w'

        # example_string[0] = 'w'
        # TypeError: 'str' object does not support item assignment

#### What is a conditional expression in Python?

Conditional expressions, involving keywords such as if, elif, and else, provide Python programs with the ability to perform 
different actions depending on a boolean condition: True or False.

        variable_a = 5
        variable_b = 3
        if variable_a > variable_b:
            print('a > b')

        # a > b

#### What are different types of arguments in Python?

An argument is simply a value provided to a function when you call it:

        x = foo( 3 )         # 3 is the argument for foo
        y = bar( 4, "str" )  # 4 and "str" are the two arguments for bar

Arguments are usually contrasted with parameters, which are names used to specify what arguments a function will need when it 
is called. When a function is called, each parameter is assigned one of the argument values.

        # foo has two named parameters, x and y
        def foo ( x, y ):
            return x + y

        z = foo( 3, 6 )

foo is given two arguments, 3 and 6. The first argument is assigned to the first parameter, x. The second argument is assigned 
to the second parameter, y.

Python functions have two kinds of parameters: args (arguments) and kwargs (keyword arguments) args are required parameters, 
while kwargs have default values set.

The following function takes arg 'foo' and kwarg 'bar'

        def hello_world(foo, bar='bye'):
            print(foo)
            print(bar)
This is how you can call the function

        >>> hello_world('hello')
        hello
        bye
        >>> hello_world('hello', bar='cya')
        hello
        cya

#### What is variable shadowing? (context: variable scope)

In computer programming, *variable shadowing* occurs when a variable declared within a certain scope (decision block, method, 
or inner class) has the same name as a variable declared in an outer scope. At the level of identifiers (names, rather than 
variables), this is known as *name masking*. This outer variable is said to be *shadowed* by the inner variable, while the inner 
identifier is said to *mask* the outer identifier. This can lead to confusion, as it may be unclear which variable subsequent 
uses of the shadowed variable name refer to, which depends on the name resolution rules of the language.

The following Python code provides another example of variable shadowing:

        x = 0
        def outer():
            x = 1
            def inner():
                x = 2
                print("inner:", x)
            inner()
            print("outer:", x)
        outer()
        print("global:", x)

        # prints
        # inner: 2
        # outer: 1
        # global: 0

The keyword global (or nonlocal depending on the case) shall be used to avoid variable shadowing and assign to global variables:

        x = 0
        def outer():
            x = 1
            def inner():
                global x
                x = 2
                print("inner:", x)
            inner()
            print("outer:", x)
        outer()
        print("global:", x)

        # prints
        # inner: 2
        # outer: 1
        # global: 2

#### What can happen if you try to delete/drop/add an item from a List, while you are iterating over it in Python?

In a for loop, .pop() will shorten the list but will still go through.

        example_list = [1, 3, 4, 2, 5, 7, 4, 7]

        for i in example_list:
            print('word')
            example_list.pop()

        print(example_list)

        # word
        # word
        # word
        # word
        # [1, 3, 4, 2]

If we are working with a specific element at a certain index, and the list is shrunk for example under that index,
an IndexError will come up

        example_list = [1, 3, 4, 2, 5, 7, 4, 7]

        for i in example_list:
            print(example_list[5])
            example_list.pop()

        # 7
        # 7
        # 7
        # print(example_list[5])
        # IndexError: list index out of range

#### What is the "golden rule" of variable scoping in Python (context: LEGB)? What is the lifetime of variables?

[Built-in   [Global   [Enclosed   [Local   ]]]] LEGB hierarchy from broadest to narrowest.

**Namespaces**: A namespace is a container where names are mapped to objects, they are used to avoid confusions in 
cases where same names exist in different namespaces. They are created by modules, functions, classes etc.

**Scope**: A scope defines the hierarchical order in which the namespaces have to be searched in order to obtain 
the mappings of name-to-object(variables). It is a context in which variables exist and from which they are referenced. 
It defines the accessibility and the lifetime of a variable.

**Local Scope**: Local scope refers to variables defined in the current function. Always, a function will first look up for 
a variable name in its local scope. Only if it does not find it there, the outer scopes are checked.

**Enclosed Scope**: For the enclosed scope, we need to define an outer function enclosing the inner function otherwise 
it will be a global variable.

**The Lifetime** of a variable is the period throughout which the variable exits in the memory of your Python program. 
The lifetime of variables inside a function is as long as the function executes. These local variables are destroyed 
as soon as the function returns or terminates.


#### If you need to access the iterator variable after a for loop, how would you do it in Python?

The for-loop makes assignments to the variables in the target list. This overwrites all previous assignments to those 
variables including those made in the suite of the for-loop:

        for i in range(10):
            print(i)
            i = 5           # this will not affect the for-loop
                            # because i will be overwritten with the next
                            # index in the range

At the end of the iteration, depending on the outcome (it completes, it breaks), the 'i' variable will keep the last
value it received inside the loop.

        example_list = [1, 3, 4]

        for i in example_list:
            print('test')
        print(i)  # prints 4

The iterator variable can be used, but the value has to be carefully considered: Do you want to use the last value 
it had in the loop? Leave it as it is after the for loop. Do you want to use it in another statement/process/while? 
Keep in mind that you have to decide if you keep the value or assign a new value. Do you want to use it in a different 
for loop? This will reset the value inside the new for loop iteration. 

#### What type of elements can a list contain in Python?

A list can contain any assortment of objects. The elements of a list can all be the same type, of varying types or
can even contain complex objects, like functions, classes, and modules.

        >>> a = [2, 4, 6, 8]
        >>> a
        [2, 4, 6, 8]

        >>> a = [21.42, 'foobar', 3, 4, 'bark', False, 3.14159]
        >>> a
        [21.42, 'foobar', 3, 4, 'bark', False, 3.14159]

        >>> int
        <class 'int'>
        >>> len
        <built-in function len>
        >>> def foo():
        ...     pass
        ...
        >>> foo
        <function foo at 0x035B9030>
        >>> import math
        >>> math
        <module 'math' (built-in)>

        >>> a = [int, len, foo, math]
        >>> a
        [<class 'int'>, <built-in function len>, <function foo at 0x02CA2618>,
        <module 'math' (built-in)>]

#### What is the slice operator in Python and how do you use it?

For any iterable (for eg. a string, list, etc), Python allows you to slice and return a substring or sublist of its data.
Format for slicing:

        iterable_name[start:stop:step]

where,
- start is the first index of the slice. Defaults to 0 (the index of the first element)
- stop one past the last index of the slice. Defaults to len(iterable)
- step is the step size (better explained by the examples below)
Examples:

        a = "abcdef"
        a               # "abcdef"
                        # Same as a[:] or a[::] since it uses the defaults for all three indices 
        a[-1]           # "f"
        a[:]            # "adcdef"
        a[::]           # "abcdef"
        a[3:]           # "def" (from index 3, to end(defaults to size of iterable))
        a[:4]           # "abcd" (from beginning(default 0) to position 4 (excluded))
        a[2:4]          # "cd" (from position 2, to position 4 (excluded))

In addition, any of the above can be used with the step size defined:

        a[::2]          # "ace" (every 2nd element)
        a[1:4:2]        # "bd" (from index 1, to index 4 (excluded), every 2nd element)

Indices can be negative, in which case they're computed from the end of the sequence

        a[:-1]          # "abcde" (from index 0 (default), to the second last element (last element - 1))
        a[:-2]          # "abcd" (from index 0 (default), to the third last element (last element -2))
        a[-1:]          # "f" (from the last element to the end (default len())

Step sizes can also be negative, in which case slice will iterate through the list in reverse order:

        a[3:1:-1]       # "dc" (from index 2 to None (default), in reverse order)

This construct is useful for reversing an iterable

        a[::-1]         # "fedcba" (from last element (default len()-1), to first, in reverse order(-1))

Notice that for negative steps the default end_index is None.

        a[5:None:-1]    # "fedcba" (this is equivalent to a[::-1])
        a[5:0:-1]       # "fedcb" (from the last element (index 5) to second element (index 1)

#### What arithmetic operators (+,*,-,/) can be used on lists in Python? What do they do?

Lists can be concatenated with the + operator.

        a = [1, 2, 3, 4, 5, 6, 7, 7]
        b = [8, 9, 10]

        a = a + [7, 8] + b
        print(a)        # [1, 2, 3, 4, 5, 6, 7, 7, 7, 8, 8, 9, 10]

Lists can be multiplied with the * operator.

        a = [1, 2, 3, 4, 5, 6, 7, 7]
        b = [8, 9, 10]

        a = a * 2
        print(a)        # [1, 2, 3, 4, 5, 6, 7, 7, 1, 2, 3, 4, 5, 6, 7, 7]

The other operators can't be used on lists, including raising to power.

#### What is the purpose of the in and not in membership operators in Python?

Membership operators are operators used to validate the membership of a value. It tests for membership 
in a sequence, such as strings, lists, or tuples.

        x = 24
        y = 20
        numbers = [10, 20, 30, 40, 50]
        if x not in numbers:
            print("x is NOT in numbers")
        else:
            print("x is in numbers")
        if y in numbers:
            print("y is present in the given numbers")
        else:
            print("y is NOT present in the given numbers")
        # x is NOT in numbers
        # y is present in the given numbers

#### What does the + operator mean when used with strings in Python?

The + operator performs the concatenation operation between strings, placing the second string at the end of 
the first to form one final longer string.

        a = 'abra'
        b = 'cadabra'
        print(a+b)
        # abracadabra

#### Explain f strings in Python.

Python f-string is the newest Python syntax to do string formatting. It is available since Python 3.6. Python 
f-strings provide a faster, more readable, more concise, and less error prone way of formatting strings in Python. 
The f-strings have the f prefix and use {} brackets to evaluate values.

        name = 'Peter'
        age = 23

        print('%s is %d years old' % (name, age))
        print('{} is {} years old'.format(name, age))
        print(f'{name} is {age} years old')

        # all print
        # Peter is 23 years old

#### Name 4 iterable types in Python.

- string
- list
- tuple
- set
- dictionary

#### What is the difference between list/set/dictionary comprehension and a generator expression in Python?

A **list comprehension** for example is an elegant way of defining and creating a list. List comprehensions allow 
us to create lists using a for loop with less code. What normally takes 3-4 lines of code, can be compressed 
into just a single line.

A **generator expression** is somewhat similar to a list comprehension, but the former doesn’t construct a list 
object. Instead of creating a list and keeping the whole sequence in memory, the generator generates the next 
element in demand. When a normal function with a return statement is called, it terminates whenever it gets a 
return statement. But a function with a yield statement saves the state of the function and can be picked up 
from the same state, next time the function is called. The generator expression allows us to create a generator 
without the yield keyword.

The generator yields one item at a time and generates items only when in demand. Whereas, in a list comprehension, 
Python reserves memory for the whole list. Thus we can say that the **generator expressions are more memory efficient** 
**than list comprehensions**.

#### Does the order of the function definitions matter in Python? Why?

The order of the function definitions doesn't matter. What matters is when the calling of the function is done, it has
to be done after the function has been defined or it will cause a Name Error.

        def print_sum(a, b):
            print(sum_numbers(a, b))

        print_sum(2, 4)

        def sum_numbers(a, b):
            return a + b

This section would cause an error because print_sum is calling sum_numbers inside of it and sum_numbers is defined after.
The print_sum call is fine, the second call, the sum_numbers call, will cause the error.

#### What does unpacking mean in Python?

We use two operators * (for tuples) and ** (for dictionaries).
Consider a situation where we have a function that receives four arguments. We want to make call to this function and we 
have a list of size 4 with us that has all arguments for the function. If we simply pass list to the function, 
the call doesn’t work.

        def fun(a, b, c, d): 
            print(a, b, c, d) 
        
        my_list = [1, 2, 3, 4] 
        
        # This doesn't work 
        fun(my_list)
        # TypeError: fun() takes exactly 4 arguments (1 given)

**Unpacking** is the action where we use * to manipulate the list so that all elements of it can be passed as different parameters.

        def fun(a, b, c, d): 
            print(a, b, c, d) 

        my_list = [1, 2, 3, 4] 
        
        # Unpacking list into four arguments 
        fun(*my_list)
        # (1, 2, 3, 4)

        >>> range(3, 6)  # normal call with separate arguments 
        [3, 4, 5] 
        >>> args = [3, 6] 
        >>> range(*args)  # call with arguments unpacked from a list 
        [3, 4, 5] 

**Packing** is the action we take when we don’t know how many arguments need to be passed to a python function. We can use Packing 
to place all the arguments in a tuple.

        def mySum(*args): 
            sum = 0
            for i in range(0, len(args)): 
                sum = sum + args[i] 
            return sum 
        
        # Driver code 
        print(mySum(1, 2, 3, 4, 5)) 
        print(mySum(10, 20)) 

        # 15
        # 30

The above function mySum() does ‘packing’ to pack all the arguments that this method call receives into one single variable. Once we 
have this ‘packed’ variable, we can do things with it that we would with a normal tuple. args[0] and args[1] would give you the first 
and second argument, respectively. Since our tuples are immutable, you can convert the args tuple to a list so you can also modify, 
delete and re-arrange items in it.

#### What happens when you try to assign the result of a function which has no return statement to a variable in Python?

If the return statement is without an expression, the special value None is returned. If there is no return statement in the function code, 
the function ends, when the control flow reaches the end of the function body and the value "None" will be returned.

## Software engineering

### Debugging

#### What techniques can you use while debugging a program in Python?

- **Rubber Duck**: which is the act of a developer explaining their code to a rubber duck in hope of finding a bug
- **Print/trace**: using print statements inside the code to see how it executes
- **Using a Debugger**: for example VS Code has a Debugger with advanced features like tracking and breakpoints

#### What does step over, step into and step out mean while using the debugger?

- **Step Over**: A function is about to be invoked, but you're not interested in debugging this particular invocation, so you want the 
debugger to execute that function completely as one entire step. 
- **Step Into**: A function is about to be invoked, and you want to debug into the code of that function, so the next step is to go into 
that function and continue debugging step-by-step.
- **Step Out**: You're done debugging this function step-by-step, and you just want the debugger to run the entire function until it 
returns as one entire step.

#### How can you start to debug a program from a certain line using the debugger?

By using a line breakpoint.

**Line Breakpoint**: You don't care how it got there, but if execution reaches a particular line of code, you want the debugger to 
temporarily pause execution there so you can decide what to do.

### Version control

#### What are the advantages of using a version control system?

- easy **collaboration** when lots of people have to work on the same project, mainly because of the ability to merge files;
- **storing versions** (properly) - it clears up things like, how often do you save changes, how do you name the files after 
changes and most importantly, how can you easily tell what changes have been made
- **restoring previous versions** is extremely easy, just a few steps, most valuable when mistake consequences are minimized
- **backup** with different options depending on the project - distributed or centralized

#### What is the difference between the working directory, the staging area and the repository in git?

- **the working directory** is the part of the local repository where files are located
- **the staging area** is the part of the local repository called **the Index** where changes are added
- **the head** is the last area, where additions are commited from the Index
- **the repository** is the trees, the file system of the project, maintained by git

#### What are remote repositories in git?

A remote repository in Git is a common repository that all team members use to exchange their changes. In most cases, such a remote repository 
is stored on a code hosting service like GitHub or on an internal server. A local repository is stored on a team member's own computer.

#### Why does a merge conflict occur?

Merge conflicts happen when you merge branches that have competing commits, and Git needs your help to decide which changes to incorporate 
in the final merge. For example if two people worked on the same file on the same function, a decision needs to be made about what will be 
kept from that conflict.

#### Through what series of commands could you put a new file into a remote repository connected to your existing local repository?

1. git add file.txt
2. git commit -m "Add the file.txt to the project"
3. git push origin branch_name

#### What does it mean atomic commits and descriptive commit messages?

When making code changes, you want to make commits that are generally smaller and that encompass only one irreducible feature, fix, or 
improvement. This is what is called an atomic commit, mainly from the definition of atomic: of or forming a single irreducible unit or 
component in a larger system. This is especially useful on code reviews and roll backs.

#### What’s the difference between git and GitHub?

- **git** is the version control software itself
- **GitHub** is the popular website that many programming professionals use to display and work on code. The site itself uses the git 
software to maintain the users' code.

## Software design

### Clean code

#### What does clean code mean?

“Clean code is code that has been taken care of. Someone has taken the time to keep it simple and orderly. They have paid appropriate 
attention to details. They have cared.” Robert C. Martin - author of Clean Code

The principle behind clean code is that in the future, the code a person writes, will probably be read by another person, even the 
writer itself, and it will be much easier for that person to understand, troubleshoot or improve code that has been written with this 
in mind. The main points of clean code are: easy to understand, easy to maintain, easy to spot bugs, easy to test, DRY over WET, naming 
conventions, indentation and formatting.

#### What steps do we usually do during a clean code refactoring?

1. Read through the whole code
2. Summarize what is the purpose of the script in one sentence.
3. Run the code to see what is the end result
4. The code should keep runnable and show the same content when you finish the refactor
5. Do not forget to run the code frequently to check you are on the right track
6. How to refactor it?
    - Remove clutter: Clutter is anything in your code that does not add value
        - Format your code
        - Delete comments
    - Remove complexity:
        - bad names
        - long methods
        - deep conditionals
        - improper variable scopes (global, local)
    - Remove cleverness: If it's simple and elegant you wouldn't refer to it as 'clever'
    - Remove the 3 D's:
        - duplication
        - duplication
        - duplication
        - This can be applied by extracting the duplicated code parts into functions

### Error handling

#### What is exception handling?

There are some situations in which runtime errors are likely to occur. Whenever we try to read a file or get input from a user, 
there is a chance that something unexpected will happen – the file may have been moved or deleted, and the user may enter data 
which is not in the right format. Good programmers should add safeguards to their programs so that common situations like this 
can be handled gracefully – a program which crashes whenever it encounters an easily foreseeable problem is not very pleasant 
to use. Most users expect programs to be robust enough to recover from these kinds of setbacks.  

If we know that a particular section of our program is likely to cause an error, we can tell Python what to do if it does happen. 
Instead of letting the error crash our program we can intercept it, do something about it, and allow the program to continue.  

All the runtime (and syntax) errors that we have encountered are called exceptions in Python – Python uses them to indicate that 
something exceptional has occurred, and that your program cannot continue unless it is handled.  

#### What are the basics of exception handling in Python?

The try and except statements, with the additional else and finally options, are the basic exception handling workflow in Python.  

When an exception occurs, the normal flow of execution is interrupted. Python checks to see if the line of code which caused the 
exception is inside a try block. If it is, it checks to see if any of the except blocks associated with the try block can handle 
that type of exception. If an appropriate handler is found, the exception is handled, and the program continues from the next 
statement after the end of that try-except.  

If there is no such handler, or if the line of code was not in a try block, Python will go up one level of scope: if the line of 
code which caused the exception was inside a function, that function will exit immediately, and the line which called the function 
will be treated as if it had thrown the exception. Python will check if that line is inside a try block, and so on. When a function 
is called, it is placed on Python’s stack. Python traverses this stack when it tries to handle an exception.  

If an exception is thrown by a line which is in the main body of your program, not inside a function, the program will terminate. 
When the exception message is printed, you should also see a traceback – a list which shows the path the exception has taken, all 
the way back to the original line which caused the error.  

#### In which case should we catch an exception? Why?

In all cases because it can prevent the program from stopping and, if well constructed, can tell the users what they need to do next 
to correct the error. Validation is one major section where exception handling is very useful, you woudn't want your program to close
every time a typo is made in a data input page, several steps in your work flow.

#### What can/should we do with an exception in the ‘except’ block?

Mainly print information to help the user understand what happened and what needs to be done. Other blocks of code can be placed 
along side the print statement as in any other location.

#### What does the else and finally statement do in a try-except block in Python?

There are two other clauses that we can add to a try-except block: **else** and **finally**. The else clause will be executed only if the 
try clause doesn’t raise an exception:

        try:
            age = int(input("Please enter your age: "))
        except ValueError:
            print("Hey, that wasn't a number!")
        else:
            print("I see that you are %d years old." % age)

The finally clause will be executed at the end of the try-except block no matter what – if there is no exception, if an exception 
is raised and handled, if an exception is raised and not handled, and even if we exit the block using break, continue or return. 
We can use the finally clause for cleanup code that we always want to be executed:

        try:
            age = int(input("Please enter your age: "))
        except ValueError:
            print("Hey, that wasn't a number!")
        else:
            print("I see that you are %d years old." % age)
        finally:
            print("It was really nice talking to you.  Goodbye!")

## Software Development Methodologies

#### What is the main goal of a retrospective meeting?

The goal of the retrospective is for the team members to discuss among themselves about how the work went during the last sprint so 
that better ways can be found to meet the project's goals. This means the team should talk about its internal processes as well.

## Programming environment

### Unix

#### What is UNIX and what is Linux?
#### What do we call the shell in Linux?
#### What does root means in a Linux environment?
#### How do you access your personal files in Linux?
#### How can you install an application in Linux?
#### What is package management in Linux, what are repositories?
#### How do you navigate in the filesystem with the command line?
#### What does the following commands do: mkdir, rm, cat, cp, touch?
#### How can you look up what does a command do in Linux if you have no internet connection?
#### What does the following commands do: head, tail, more, less?
#### How do you download a file from internet using the terminal?
