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

Immutable variable value can not be changed once they are created.

        example_string = 'abc'
        example_string[0] = 'w'

        # example_string[0] = 'w'
        # TypeError: 'str' object does not support item assignment

#### What is conditional expression in Python?
#### What are different types of arguments in Python?
#### What is variable shadowing? (context: variable scope)
#### What can happen if you try to delete/drop/add an item from a List, while you are iterating over it in Python?
#### What is the "golden rule" of variable scoping in Python (context: LEGB)? What is the lifetime of variables?
#### If you need to access the iterator variable after a for loop, how would you do it in Python?
#### What type of elements can a list contain in Python?
#### What is the slice operator in Python and how do you use it?
#### What arithmetic operators (+,*,-,/) can be used on lists in Python? What do they do?
#### What is the purpose of the in and not in membership operators in Python?
#### What does the + operator mean when used with strings in Python?
#### Explain f strings in Python.
#### Name 4 iterable types in Python.
#### What is the difference between list/set/dictionary comprehension and a generator expression in Python?
#### Does the order of the function definitions matter in Python? Why?
#### What does unpacking mean in Python?
#### What happens when you try to assign the result of a function which has no return statement to a variable in Python?

## Software engineering

### Debugging

#### What techniques can you use while debugging a program in Python?
#### What does step over, step into and step out mean while using the debugger?
#### How can you start to debug a program from a certain line using the debugger?

### Version control

#### What are the advantages of using a version control system?
#### What is the difference between the working directory, the staging area and the repository in git?
#### What are remote repositories in git?
#### Why does a merge conflict occur?
#### Through what series of commands could you put a new file into a remote repository connected to your existing local repository?
#### What does it mean atomic commits and descriptive commit messages?
#### What’s the difference between git and GitHub?

## Software design

### Clean code

#### What does clean code mean?
#### What steps do we usually do during a clean code refactoring?

### Error handling

#### What is exception handling?
#### What are the basics of exception handling in Python?
#### In which case should we catch an exception? Why?
#### What can/should we do with an exception in the ‘except’ block?
#### What does the else and finally statement do in a try-except block in Python?

## Software Development Methodologies

#### What is the main goal of a retrospective meeting?

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
