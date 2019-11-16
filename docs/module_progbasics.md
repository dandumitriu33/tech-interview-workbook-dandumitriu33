# Programming Basics questions

## Computer science

### Data structures

#### What is the purpose of a list (array in some programming languages) data structure? Name some methods of it!

Lists are one of the most versatile data structures. They are mutable as opposed to strings, can be indexed, sliced, sorted and iterated. In most programming languages, arrays contain data of the same type only. In Python lists can contain multiple types of data combined. Arrays have a special module in Python that has to be imported (from array import *).

st.sort() and sorted() - which will sort the elements in the list in place or in a copy respectively
lst.append() - which adds an element at the end of the list
lst.insert(0, 'a') - which inserts 'a' at index 0
lst.remove(value) - which removes the first instance of that value
lst.reverse() - which reverses the list in place and returns Nonelooking like it's been marked up with tags or formatting instructions.


#### What is the difference between a list/array and a set?

#### A list can mainly contain multiple items with the same value while sets can contain only unique values, duplicates are removed.
#### Lists have certain operations that can be performed on them, but not on sets, such as sort, find, count, reverse. Sets also 
#### have specific operations that can be performed only on them, such as: intersection, union, difference, symmetric difference.


#### What is the purpose and methods of a dictionary/map data structure?

#### The dictionary's main characteristic is that it has a unique set of keys, which can have values assigned to them. It allows 
#### you to store and retrieve elements by referencing a key. As dictionaries are referenced by key, they have very fast lookups. 
#### As they are primarily used for referencing items by key, they are not sorted.


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
    while i < user_number -2:
        new_number = fibonacci_numbers[-1] + fibonacci_numbers[-2]
        fibonacci_numbers.append(new_number)
        i += 1
    return fibonacci_numbers
 print(fibonacci_sequence())


#### How do you find a max value in a list/array if you can’t use any built-in functions?

#### numbers = [5, 20, 14, 2, 31]
#### 
#### 
#### def find_max(arr):
####     max_of_list = arr[0]
####     for i in arr:
####         if i > max_of_list:
####             max_of_list = i
####     return max_of_list
#### 
#### 
#### print(find_max(numbers))


#### How do you find the average of values in a list/array if you can’t use any built-in functions?

#### numbers = [5, 20, 14, 2, 31]
#### 
#### 
#### def find_average(arr):
####     sum = 0
####     for i in arr:
####         sum += i
####     return sum/len(arr)
#### 
#### 
#### print(find_average(numbers))


#### What do we call an *in-place* sort?

#### numbers = [5, 20, 14, 2, 31]
#### 
#### numbers.sort()
#### print(numbers)
#### 
#### # [2, 5, 14, 20, 31]


#### Explain an algorithm which sorts a list!

#### Bubble Sort is the simplest sorting algorithm that works by repeatedly swapping the adjacent
#### elements if they are in the wrong order. In the improved version, the algorithm only stops after
#### it runs a pass where it doesn't perform a swap.

#### numbers = [5, 20, 14, 2, 31]
#### 
#### 
#### def bubble_sort(arr):
####     n = len(arr)
####     for i in range(n):
####         for j in range(0, n-i-1):
####             if arr[j] > arr[j+1]:
####                 arr[j], arr[j+1] = arr[j+1], arr[j]
####     return arr
#### 
#### 
#### print(bubble_sort(numbers))
#### # [2, 5, 14, 20,31]


#### numbers = [5, 20, 14, 2, 31]
#### 
#### 
#### def bubble_sort(arr):
####     n = len(arr)
####     for i in range(n):
####         swapped = False
####         for j in range(0, n-i-1):
####             if arr[j] > arr[j+1]:
####                 arr[j], arr[j+1] = arr[j+1], arr[j] 
####                 swapped = True
####         if swapped is False:
####             break
####     return arr
#### 
#### 
#### print(bubble_sort(numbers))
#### 
#### # [2, 5, 14, 20, 31]


### Programming paradigms - procedural

#### What is the call stack?
#### What is “Stack overflow”?
#### What are the main parts of a function?

### Programming languages - Python  
#### How do you use a dictionary in Python?
#### What does it mean that an object is immutable in Python?
#### What is conditional expression in Python?
#### What are different types of arguments in Python?
#### What is variable shadowing? (context: variable scope)
#### What can happen if you try to delete/drop/add an item from a List, while you are iterating over it in Python?
#### What is the "golden rule" of variable scoping in Python (context: LEGB)? What is the lifetime of variables?
#### If you need to access the iterator variable after a for loop, how would you do it in Python?
#### What type of elements can a list contain in Python?
#### What is slice operator in Python and how to use?
#### What arithmetic operators (+,*,-,/) can be used on lists in Python? What do they do?
#### What is the purpose of the in and not in membership operators in Python?
#### What does the + operator mean when used with strings in Python?
#### Explain f strings in Python?
#### Name 4 iterable types in Python!
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
