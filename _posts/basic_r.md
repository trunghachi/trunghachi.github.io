# R INRODUCTION

[Learn from w3schools](https://www.w3schools.com/r/r_intro.asp)

* It is a great resource for data analysis, data visualization, data science and machine learning
* It provides many statistical techniques (such as statistical tests, classification, clustering and data reduction)
* It is easy to draw graphs in R, like pie charts, histograms, box plot, scatter plot, etc++
* It works on different platforms (Windows, Mac, Linux)
* It is open-source and free
* It has a large community support
* It has many packages (libraries of functions) that can be used to solve different problems

## How to install:
[How to Install R](https://cloud.r-project.org/)

[R with Jupyter Notebook](https://marketsplash.com/tutorials/r/how-to-use-r-in-jupyter-notebooks/)

[R with VSCode](https://code.visualstudio.com/docs/languages/r)

## R Syntax


```R
"Hello World!"
5 + 5
```


'Hello World!'



10



```R
for (x in 1:10) {
  print(x)
}
```

    [1] 1
    [1] 2
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    [1] 7
    [1] 8
    [1] 9
    [1] 10
    


```R
# This is a comment
print("Hello World!")
```

    [1] "Hello World!"
    

## R Variables
### Creating Variables in R


```R
name <- "John"
age <- 40

name   # output "John"
age    # output 40
```


'John'



40



```R
name <- "John Doe"

name # auto-print the value of the name variable
```


'John Doe'



```R
for (x in 1:10) {
  print(x)
}
```

    [1] 1
    [1] 2
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    [1] 7
    [1] 8
    [1] 9
    [1] 10
    

### Concatenate Elements


```R
text <- "awesome"

paste("R is", text)
```


'R is awesome'



```R
text1 <- "R is"
text2 <- "awesome"

paste(text1, text2)
```


'R is awesome'



```R
num1 <- 5
num2 <- 10

num1 + num2
```


15


### Multiple Variables


```R
# Assign the same value to multiple variables in one line
var1 <- var2 <- var3 <- "Orange"

# Print variable values
var1
var2
var3
```


'Orange'



'Orange'



'Orange'


### Variable Names (Identifiers)
* A variable can have a short name (like `x` and `y`) or a more descriptive name (`age`, `carname`, `total_volume`). Rules for R variables are:
* A variable name must start with a letter and can be a combination of letters, digits, period(`.`)
* and underscore(`_`). If it starts with period(`.`), it cannot be followed by a digit.
* A variable name cannot start with a number or underscore (`_`)
* Variable names are case-sensitive (`age`, `Age` and `AGE` are three different variables)
* Reserved words cannot be used as variables (`TRUE`, `FALSE`, `NULL`, `if`...)


```R
# Legal variable names:
myvar <- "John"
my_var <- "John"
myVar <- "John"
MYVAR <- "John"
myvar2 <- "John"
.myvar <- "John"

# Illegal variable names:
# 2myvar <- "John"
# my-var <- "John"
# my var <- "John"
# _my_var <- "John"
# my_v@ar <- "John"
# TRUE <- "John"
```


```R
my_var <- 30 # my_var is type of numeric
my_var <- "Sally" # my_var is now of type character (aka string)
```

## R Basic Data Types
Basic data types in R can be divided into the following types:

* `numeric` - (10.5, 55, 787)
* `integer` - (1L, 55L, 100L, where the letter "L" declares this as an integer)
* `complex` - (9 + 3i, where "i" is the imaginary part)
* character (a.k.a. `string`) - ("k", "R is exciting", "FALSE", "11.5")
* logical (a.k.a. `boolean`) - (**TRUE** or **FALSE**)

We can use the class() function to check the data type of a variable:


```R
# numeric
x <- 10.5
class(x)

# integer
x <- 1000L
class(x)

# complex
x <- 9i + 3
class(x)

# character/string
x <- "R is exciting"
class(x)

# logical/boolean
x <- TRUE
class(x)
```


'numeric'



'integer'



'complex'



'character'



'logical'


## R Numbers
There are three number types in R:

* numeric
* integer
* complex

Variables of number types are created when you assign a value to them:


```R
x <- 10.5   # numeric
y <- 10L    # integer
z <- 1i     # complex
```


```R
# numeric
x <- 10.5
y <- 55

# Print values of x and y
x
y

# Print the class name of x and y
class(x)
class(y)
```


10.5



55



'numeric'



'numeric'



```R
# integer
x <- 1000L
y <- 55L

# Print values of x and y
x
y

# Print the class name of x and y
class(x)
class(y)
```


1000



55



'integer'



'integer'



```R
# complex
x <- 3+5i
y <- 5i

# Print values of x and y
x
y

# Print the class name of x and y
class(x)
class(y)
```


3+5i



0+5i



'complex'



'complex'


## Type Conversion
You can convert from one type to another with the **following functions**:

* `as.numeric()`
* `as.integer()`
* `as.complex()`


```R
x <- 1L # integer
y <- 2 # numeric

# convert from integer to numeric:
a <- as.numeric(x)

# convert from numeric to integer:
b <- as.integer(y)

# print values of x and y
x
y

# print the class name of a and b
class(a)
class(b)
```


1



2



'numeric'



'integer'


## R Math
### Build-in Math Function


```R
max(5, 10, 15)

min(5, 10, 15)

sqrt(16)

abs(-4.7)

ceiling(1.4)

floor(1.4)
```


15



5



4



4.7



2



1


## String Literals
Strings are used for storing text.

A string is surrounded by either single quotation marks, or double quotation marks:

`"hello"` is the same as `'hello'`:


```R
# Assign a String to a Variable

str <-"hello"
str
```


'hello'



```R
# Multiline string
str <- "Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua."

str # print the value of str
```


'Lorem ipsum dolor sit amet,\nconsectetur adipiscing elit,\nsed do eiusmod tempor incididunt\nut labore et dolore magna aliqua.'


However, note that R will add a "\n" at the end of each line break. This is called an escape character, and the n character indicates a new line.

If you want the line breaks to be inserted at the same position as in the code, use the cat() function:


```R
str <- "Lorem ipsum dolor sit amet,
consectetur adipiscing elit,
sed do eiusmod tempor incididunt
ut labore et dolore magna aliqua."

cat(str)
```

    Lorem ipsum dolor sit amet,
    consectetur adipiscing elit,
    sed do eiusmod tempor incididunt
    ut labore et dolore magna aliqua.

### String Length
There are many usesful string functions in R.

For example, to find the number of characters in a string, use the `nchar()` function:


```R
str <- "Hello World!"

nchar(str)
```


12


### Check a String
Use the `grepl()` function to check if a character or a sequence of characters are present in a string:


```R
str <- "Hello World!"

grepl("H", str)
grepl("Hello", str)
grepl("X", str)
```


TRUE



TRUE



FALSE


### Combine Two Strings
Use the `paste()` function to merge/concatenate two strings:


```R
str1 <- "Hello"
str2 <- "World"

paste(str1, str2)
```


'Hello World'


## Escape Characters
To insert characters that are illegal in a string, you must use an escape character.

An escape character is a backslash `\` followed by the character you want to insert.

An example of an illegal character is a double quote inside a string that is surrounded by double quotes:


```R
str <- "We are the so-called \"Vikings\", from the north."

str
cat(str)
```


'We are the so-called "Vikings", from the north.'


    We are the so-called "Vikings", from the north.

Note that auto-printing the str variable will print the backslash in the output. You can use the cat() function to print it without backslash.

Other escape characters in R:

| Code | Result |
|:-------:|------:|
| `\\` | Backslash |
| `\n` | New Line |
| `\r` | Carriage Return |
| `\t`| Tab |
| `\b` | Backspace |



## R Booleans (Logical Values)


```R
10 > 9    # TRUE because 10 is greater than 9
10 == 9   # FALSE because 10 is not equal to 9
10 < 9    # FALSE because 10 is greater than 9
```


TRUE



FALSE



FALSE



```R
a <- 10
b <- 9

a > b
```


TRUE



```R
a <- 200
b <- 33

if (b > a) {
  print ("b is greater than a")
} else {
  print("b is not greater than a")
}
```

    [1] "b is not greater than a"
    

## R Operators


R divides the operators in the following groups:

* Arithmetic operators
* Assignment operators
* Comparison operators
* Logical operators
* Miscellaneous operators

R Arithmetic Operators
Arithmetic operators are used with numeric values to perform common mathematical operations:

| Operator | Name | Example |
|:-------|:------|:-------:|
| `+` | Addition | `x + y` |
| `-` | Subtraction | `x - y` |
| `*` | Multiplication | `x * y` |
| `/` | Division | `x / y` |
| `^` | Exponent | `x ^ y` |
| `%%` | Modulus (Remainder from division) | `x %% y` |
| `%/%` | Integer Division | `x%/%y` |


```R
11+5
11-5
11/5
11^5
11%%5
11%/%5
```


16



6



2.2



161051



1



2


### R Assignment Operators
Assignment operators are used to assign values to variables:


```R
my_var <- 3

my_var <<- 3 # global asigner

3 -> my_var

3 ->> my_var

my_var # print my_var
```


3


### R Comparison Operators
Comparison operators are used to compare two values:

| Operator | Name | Example |
|:-------|:------|:-------:|
| `==` | Equal | `x == y` |	
| `!=` | Not equal | `x != y`|	
| `>`  | Greater than | `x > y`|
| `<` | Less than | `x < y` |
| `>=` | Greater than or equal to | `x >= y` |
| `<=` | Less than or equal to | `x <= y` |

### R Logical Operators
Logical operators are used to combine conditional statements:

| Operator | Description | Example |
|:-------|:------|:-------:|
|`&` | Element-wise Logical AND operator. It returns TRUE if both elements are TRUE| |
|`&&` | Logical AND operator - Returns TRUE if both statements are TRUE| |
| `|` | Elementwise- Logical OR operator. It returns TRUE if one of the statement is TRUE| |
| `||` | Logical OR operator. It returns TRUE if one of the statement is TRUE.| |
| `!`| Logical NOT - returns FALSE if statement is TRUE| |

R Miscellaneous Operators
Miscellaneous operators are used to manipulate data:

Operator	Description	Example
:	Creates a series of numbers in a sequence	x <- 1:10
%in%	Find out if an element belongs to a vector	x %in% y
%*%	Matrix Multiplication	x <- Matrix1 %*% Matrix2


### R Logical Operators
Logical operators are used to combine conditional statements:

| Operator | Description | Example |
|:-------|:------|:-------:|
| `&` | Element-wise Logical AND operator. It returns TRUE if both elements are TRUE | |
| `&&` | Logical AND operator - Returns TRUE if both statements are TRUE | |
| `\|` | Elementwise- Logical OR operator. It returns TRUE if one of the statement is TRUE | |
| `\|\|` | Logical OR operator. It returns TRUE if one of the statement is TRUE | |
| `!` | Logical NOT - returns FALSE if statement is TRUE | |

### R Miscellaneous Operators
Miscellaneous operators are used to manipulate data:

| Operator | Description | Example |
|:-------|:------|:-------:|
|`:`|Creates a series of numbers in a sequence|`x <- 1:10`|
|`%in%`|Find out if an element belongs to a vector|`x %in% y`|
|`%*%`|Matrix Multiplication|`x <- Matrix1 %*% Matrix2`|


## The if, if...else Statement


```R
a <- 33
b <- 200

if (b > a) {
  print("b is greater than a")
}
```

    [1] "b is greater than a"
    


```R
a <- 33
b <- 33

if (b > a) {
  print("b is greater than a")
} else if (a == b) {
  print ("a and b are equal")
}
```

    [1] "a and b are equal"
    


```R
a <- 200
b <- 33

if (b > a) {
  print("b is greater than a")
} else if (a == b) {
  print("a and b are equal")
} else {
  print("a is greater than b")
}
```

    [1] "a is greater than b"
    

### Nested `If` Statements


```R
x <- 41

if (x > 10) {
  print("Above ten")
  if (x > 20) {
    print("and also above 20!")
  } else {
    print("but not above 20.")
  }
} else {
  print("below 10.")
}
```

    [1] "Above ten"
    [1] "and also above 20!"
    


```R
a <- 200
b <- 33
c <- 500

if (a > b & c > a) {
  print("Both conditions are true")
}
```

    [1] "Both conditions are true"
    


```R
a <- 200
b <- 33
c <- 500

if (a > b | a > c) {
  print("At least one of the conditions is true")
}
```

    [1] "At least one of the conditions is true"
    

## Loops
Loops can execute a block of code as long as a specified condition is reached.

Loops are handy because they save time, reduce errors, and they make code more readable.

R has two loop commands:

* while loops
* for loops

### while loops


```R
i <- 1
while (i < 6) {
  print(i)
  i <- i + 1
}
print(i)
```

    [1] 1
    [1] 2
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    


```R
# break
i <- 1
while (i < 6) {
  print(i)
  i <- i + 1
  if (i == 4) {
    break
  }
}
```

    [1] 1
    [1] 2
    [1] 3
    


```R
# next
i <- 0
while (i < 6) {
  i <- i + 1
  if (i == 3) {
    next
  }
  print(i)
}
```

    [1] 1
    [1] 2
    [1] 4
    [1] 5
    [1] 6
    


```R
dice <- 1
while (dice <= 6) {
  if (dice < 6) {
    print("No Yahtzee")
  } else {
    print("Yahtzee!")
  }
  dice <- dice + 1
}
```

    [1] "No Yahtzee"
    [1] "No Yahtzee"
    [1] "No Yahtzee"
    [1] "No Yahtzee"
    [1] "No Yahtzee"
    [1] "Yahtzee!"
    

### for loops


```R
for (x in 1:10) {
  print(x)
}
```

    [1] 1
    [1] 2
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    [1] 7
    [1] 8
    [1] 9
    [1] 10
    


```R
fruits <- list("apple", "banana", "cherry")

for (x in fruits) {
  print(x)
}
```

    [1] "apple"
    [1] "banana"
    [1] "cherry"
    


```R
dice <- c(1, 2, 3, 4, 5, 6)

for (x in dice) {
  print(x)
}
```

    [1] 1
    [1] 2
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    


```R
# break
fruits <- list("apple", "banana", "cherry")

for (x in fruits) {
  if (x == "cherry") {
    break
  }
  print(x)
}
```

    [1] "apple"
    [1] "banana"
    


```R
# next
fruits <- list("apple", "banana", "cherry")

for (x in fruits) {
  if (x == "banana") {
    next
  }
  print(x)
}
```

    [1] "apple"
    [1] "cherry"
    


```R
dice <- 1:6

for(x in dice) {
  if (x == 6) {
    print(paste("The dice number is", x, "Yahtzee!"))
  } else {
    print(paste("The dice number is", x, "Not Yahtzee"))
  }
}
```

    [1] "The dice number is 1 Not Yahtzee"
    [1] "The dice number is 2 Not Yahtzee"
    [1] "The dice number is 3 Not Yahtzee"
    [1] "The dice number is 4 Not Yahtzee"
    [1] "The dice number is 5 Not Yahtzee"
    [1] "The dice number is 6 Yahtzee!"
    


```R
# Nested loops
adj <- list("red", "big", "tasty")

fruits <- list("apple", "banana", "cherry")
  for (x in adj) {
    for (y in fruits) {
      print(paste(x, y))
  }
}
```

    [1] "red apple"
    [1] "red banana"
    [1] "red cherry"
    [1] "big apple"
    [1] "big banana"
    [1] "big cherry"
    [1] "tasty apple"
    [1] "tasty banana"
    [1] "tasty cherry"
    

## Function
### Creating a Function
To create a function, use the `function()` keyword:


```R
my_function <- function() { # create a function with the name my_function
  print("Hello World!")
}
```


```R
my_function() # call the function named my_function
```

    [1] "Hello World!"
    


```R
my_function <- function(fname) {
  paste(fname, "Griffin")
}

my_function("Peter")
my_function("Lois")
my_function("Stewie")
```


'Peter Griffin'



'Lois Griffin'



'Stewie Griffin'


#### Number of Arguments
By default, a function must be called with the correct number of arguments. Meaning that if your function expects 2 arguments, you have to call the function with 2 arguments, not more, and not less (otherwise you will get an error):


```R
my_function <- function(fname, lname) {
  paste(fname, lname)
}

my_function("Peter", "Griffin")
```


'Peter Griffin'


#### Default parameter value


```R
my_function <- function(country = "Norway") {
  paste("I am from", country)
}

my_function("Sweden")
my_function("India")
my_function() # will get the default value, which is Norway
my_function("USA")
```


'I am from Sweden'



'I am from India'



'I am from Norway'



'I am from USA'


#### Return values


```R
my_function <- function(x) {
  return (5 * x)
}

print(my_function(3))
print(my_function(5))
print(my_function(9))
```

    [1] 15
    [1] 25
    [1] 45
    

### Nested Functions
There are two ways to create a nested function:

* Call a function within another function.
* Write a function within a function.
#### Call a function within another function


```R
Nested_function <- function(x, y) {
  a <- x + y
  return(a)
}

Nested_function(Nested_function(2,2), Nested_function(3,3))
```


10


#### Write a function within a function


```R
Outer_func <- function(x) {
  Inner_func <- function(y) {
    a <- x + y
    return(a)
  }
  return (Inner_func)
}
output <- Outer_func(3) # To call the Outer_func
output(5)
```


8


### Recursion


```R
tri_recursion <- function(k) {
  if (k > 0) {
    result <- k + tri_recursion(k - 1)
    print(result)
  } else {
    result = 0
    return(result)
  }
}
tri_recursion(6)
```

    [1] 1
    [1] 3
    [1] 6
    [1] 10
    [1] 15
    [1] 21
    

#### Global variables


```R
txt <- "awesome"
my_function <- function() {
  paste("R is", txt)
}

my_function()
```


'R is awesome'



```R
txt <- "global variable"
my_function <- function() {
  txt = "fantastic"
  paste("R is", txt)
}

my_function()

txt # print txt
```


'R is fantastic'



'global variable'


#### The Global Assignment Operator
Normally, when you create a variable inside a function, that variable is local, and can only be used inside that function.

To create a global variable inside a function, you can use the global assignment operator `<<-`


```R
# If you use the assignment operator <<-, the variable belongs to the global scope:
my_function <- function() {
txt <<- "fantastic"
  paste("R is", txt)
}

my_function()

print(txt)
```


'R is fantastic'


    [1] "fantastic"
    


```R
# Also, use the global assignment operator if you want to change a global variable inside a function:
txt <- "awesome"
my_function <- function() {
  txt <<- "fantastic"
  paste("R is", txt)
}

my_function()

paste("R is", txt)
```


'R is fantastic'



'R is fantastic'


# R DATA STRUCTURE

## Vector


```R
# Vector of strings
fruits <- c("banana", "apple", "orange")

# Print fruits
fruits
length(fruits)

# Vector of numerical values
numbers <- c(1, 2, 3)

# Print numbers
numbers

# Vector with numerical decimals in a sequence
numbers1 <- 1.5:6.5
numbers1

# Vector with numerical decimals in a sequence where the last element is not used
numbers2 <- 1.5:6.3
numbers2
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'banana'</li><li>'apple'</li><li>'orange'</li></ol>




3



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>2</li><li>3</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1.5</li><li>2.5</li><li>3.5</li><li>4.5</li><li>5.5</li><li>6.5</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1.5</li><li>2.5</li><li>3.5</li><li>4.5</li><li>5.5</li></ol>




```R
fruits <- c("banana", "apple", "orange", "mango", "lemon")
numbers <- c(13, 3, 5, 7, 20, 2)

sort(fruits)  # Sort a string
sort(numbers) # Sort numbers
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'apple'</li><li>'banana'</li><li>'lemon'</li><li>'mango'</li><li>'orange'</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>2</li><li>3</li><li>5</li><li>7</li><li>13</li><li>20</li></ol>




```R
fruits[1]
fruits[c(1,4)]

# Access all items except for the first item
fruits[c(-1)]
```


'banana'



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'banana'</li><li>'mango'</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'apple'</li><li>'orange'</li><li>'mango'</li><li>'lemon'</li></ol>




```R
# Change "banana" to "pear"
fruits[1] <- "pear"

# Print fruits
fruits
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'pear'</li><li>'apple'</li><li>'orange'</li><li>'mango'</li><li>'lemon'</li></ol>




```R
repeat_each <- rep(c(1,2,3), each = 3)

repeat_each
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>1</li><li>1</li><li>2</li><li>2</li><li>2</li><li>3</li><li>3</li><li>3</li></ol>




```R
repeat_times <- rep(c(1,2,3), times = 3)

repeat_times
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>2</li><li>3</li><li>1</li><li>2</li><li>3</li><li>1</li><li>2</li><li>3</li></ol>




```R
repeat_indepent <- rep(c(1,2,3), times = c(5,2,1))

repeat_indepent
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>1</li><li>1</li><li>1</li><li>1</li><li>2</li><li>2</li><li>3</li></ol>




```R
numbers <- seq(from = 0, to = 100, by = 20)

numbers
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>0</li><li>20</li><li>40</li><li>60</li><li>80</li><li>100</li></ol>



## List

A list in R can contain many different data types inside it. A list is a collection of data which is **ordered** and **changeable**.


```R
# List of strings
thislist <- list("apple", "banana", "cherry")

# Print the list
thislist
```


<ol>
	<li>'apple'</li>
	<li>'banana'</li>
	<li>'cherry'</li>
</ol>




```R
thislist <- list("apple", "banana", "cherry")
thislist[1] <- "blackcurrant"

# Print the updated list
thislist
```


<ol>
	<li>'blackcurrant'</li>
	<li>'banana'</li>
	<li>'cherry'</li>
</ol>




```R
length(thislist)
```


3



```R
"apple" %in% thislist
```


FALSE



```R
append(thislist, "orange")
```


<ol>
	<li>'blackcurrant'</li>
	<li>'banana'</li>
	<li>'cherry'</li>
	<li>'orange'</li>
</ol>




```R
thislist <- list("apple", "banana", "cherry")

append(thislist, "orange", after = 2)
```


<ol>
	<li>'apple'</li>
	<li>'banana'</li>
	<li>'orange'</li>
	<li>'cherry'</li>
</ol>




```R
thislist <- list("apple", "banana", "cherry")

newlist <- thislist[-1]

# Print the new list
newlist
```


<ol>
	<li>'banana'</li>
	<li>'cherry'</li>
</ol>




```R
thislist <- list("apple", "banana", "cherry", "orange", "kiwi", "melon", "mango")

(thislist)[2:5]
```


<ol>
	<li>'banana'</li>
	<li>'cherry'</li>
	<li>'orange'</li>
	<li>'kiwi'</li>
</ol>




```R
thislist <- list("apple", "banana", "cherry")

for (x in thislist) {
  print(x)
}
```

    [1] "apple"
    [1] "banana"
    [1] "cherry"
    


```R
list1 <- list("a", "b", "c")
list2 <- list(1,2,3)
list3 <- c(list1,list2)

list3
```


<ol>
	<li>'a'</li>
	<li>'b'</li>
	<li>'c'</li>
	<li>1</li>
	<li>2</li>
	<li>3</li>
</ol>



## Matrices


```R
# Create a matrix
thismatrix <- matrix(c(1,2,3,4,5,6), nrow = 3, ncol = 2)

# Print the matrix
thismatrix
```


<table class="dataframe">
<caption>A matrix: 3 × 2 of type dbl</caption>
<tbody>
	<tr><td>1</td><td>4</td></tr>
	<tr><td>2</td><td>5</td></tr>
	<tr><td>3</td><td>6</td></tr>
</tbody>
</table>




```R
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

thismatrix
```


<table class="dataframe">
<caption>A matrix: 2 × 2 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>cherry</td></tr>
	<tr><td>banana</td><td>orange</td></tr>
</tbody>
</table>




```R
thismatrix[1, 2]
```


'cherry'



```R
thismatrix[, 2]
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'cherry'</li><li>'orange'</li></ol>




```R
thismatrix[2,]
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'banana'</li><li>'orange'</li></ol>




```R
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

thismatrix
```


<table class="dataframe">
<caption>A matrix: 3 × 3 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>orange   </td><td>pear </td></tr>
	<tr><td>banana</td><td>grape    </td><td>melon</td></tr>
	<tr><td>cherry</td><td>pineapple</td><td>fig  </td></tr>
</tbody>
</table>




```R
thismatrix[c(1,2),]
```


<table class="dataframe">
<caption>A matrix: 2 × 3 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>orange</td><td>pear </td></tr>
	<tr><td>banana</td><td>grape </td><td>melon</td></tr>
</tbody>
</table>




```R
thismatrix[, c(1,2)]
```


<table class="dataframe">
<caption>A matrix: 3 × 2 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>orange   </td></tr>
	<tr><td>banana</td><td>grape    </td></tr>
	<tr><td>cherry</td><td>pineapple</td></tr>
</tbody>
</table>



### Add rows or columns


```R
# add rows or columns
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

newmatrix <- cbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# Print the new matrix
newmatrix
```


<table class="dataframe">
<caption>A matrix: 3 × 4 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>orange   </td><td>pear </td><td>strawberry</td></tr>
	<tr><td>banana</td><td>grape    </td><td>melon</td><td>blueberry </td></tr>
	<tr><td>cherry</td><td>pineapple</td><td>fig  </td><td>raspberry </td></tr>
</tbody>
</table>




```R
thismatrix <- matrix(c("apple", "banana", "cherry", "orange","grape", "pineapple", "pear", "melon", "fig"), nrow = 3, ncol = 3)

newmatrix <- rbind(thismatrix, c("strawberry", "blueberry", "raspberry"))

# Print the new matrix
newmatrix
```


<table class="dataframe">
<caption>A matrix: 4 × 3 of type chr</caption>
<tbody>
	<tr><td>apple     </td><td>orange   </td><td>pear     </td></tr>
	<tr><td>banana    </td><td>grape    </td><td>melon    </td></tr>
	<tr><td>cherry    </td><td>pineapple</td><td>fig      </td></tr>
	<tr><td>strawberry</td><td>blueberry</td><td>raspberry</td></tr>
</tbody>
</table>



### Remove rows or columns


```R
thismatrix <- matrix(c("apple", "banana", "cherry", "orange", "mango", "pineapple"), nrow = 3, ncol =2)

thismatrix
```


<table class="dataframe">
<caption>A matrix: 3 × 2 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>orange   </td></tr>
	<tr><td>banana</td><td>mango    </td></tr>
	<tr><td>cherry</td><td>pineapple</td></tr>
</tbody>
</table>




```R
#Remove the first row and the first column
thismatrix <- thismatrix[-c(1),-c(1)]

thismatrix
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'mango'</li><li>'pineapple'</li></ol>




```R
thismatrix <- matrix(c("apple", "banana", "cherry", "orange"), nrow = 2, ncol = 2)

"apple" %in% thismatrix
```


TRUE



```R
dim(thismatrix)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>2</li><li>2</li></ol>




```R
length(thismatrix)
```


4



```R
for (rows in 1:nrow(thismatrix)) {
  for (columns in 1:ncol(thismatrix)) {
    print(thismatrix[rows, columns])
  }
}
```

    [1] "apple"
    [1] "cherry"
    [1] "banana"
    [1] "orange"
    


```R
# Combine matrices
Matrix1 <- matrix(c("apple", "banana", "cherry", "grape"), nrow = 2, ncol = 2)
Matrix2 <- matrix(c("orange", "mango", "pineapple", "watermelon"), nrow = 2, ncol = 2)

# Adding it as a rows
Matrix_Combined <- rbind(Matrix1, Matrix2)
Matrix_Combined

# Adding it as a columns
Matrix_Combined <- cbind(Matrix1, Matrix2)
Matrix_Combined
```


<table class="dataframe">
<caption>A matrix: 4 × 2 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>cherry    </td></tr>
	<tr><td>banana</td><td>grape     </td></tr>
	<tr><td>orange</td><td>pineapple </td></tr>
	<tr><td>mango </td><td>watermelon</td></tr>
</tbody>
</table>




<table class="dataframe">
<caption>A matrix: 2 × 4 of type chr</caption>
<tbody>
	<tr><td>apple </td><td>cherry</td><td>orange</td><td>pineapple </td></tr>
	<tr><td>banana</td><td>grape </td><td>mango </td><td>watermelon</td></tr>
</tbody>
</table>



## Arrays

* Compared to matrices, arrays can have more than two dimensions. (something like the *tensors*)
* Arrays can only have one data type.


```R
# An array with one dimension with values ranging from 1 to 24
thisarray <- c(1:24)
thisarray

# An array with more than one dimension
multiarray <- array(thisarray, dim = c(4, 3, 2))
multiarray
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>2</li><li>3</li><li>4</li><li>5</li><li>6</li><li>7</li><li>8</li><li>9</li><li>10</li><li>11</li><li>12</li><li>13</li><li>14</li><li>15</li><li>16</li><li>17</li><li>18</li><li>19</li><li>20</li><li>21</li><li>22</li><li>23</li><li>24</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>2</li><li>3</li><li>4</li><li>5</li><li>6</li><li>7</li><li>8</li><li>9</li><li>10</li><li>11</li><li>12</li><li>13</li><li>14</li><li>15</li><li>16</li><li>17</li><li>18</li><li>19</li><li>20</li><li>21</li><li>22</li><li>23</li><li>24</li></ol>




```R
multiarray[2, 3, 2]
```


22



```R
multiarray[c(1),,1]
multiarray[,c(1),1]
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>5</li><li>9</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>2</li><li>3</li><li>4</li></ol>




```R
2 %in% multiarray
dim(multiarray)
length(multiarray)
```


TRUE



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>4</li><li>3</li><li>2</li></ol>




24



```R
for(x in multiarray){
  print(x)
}
```

    [1] 1
    [1] 2
    [1] 3
    [1] 4
    [1] 5
    [1] 6
    [1] 7
    [1] 8
    [1] 9
    [1] 10
    [1] 11
    [1] 12
    [1] 13
    [1] 14
    [1] 15
    [1] 16
    [1] 17
    [1] 18
    [1] 19
    [1] 20
    [1] 21
    [1] 22
    [1] 23
    [1] 24
    

## Data Frames

**Data Frames** are data displayed in a format as a *table*.

**Data Frames** can have different types of data inside it. While the first column can be `character`, the second and third can be `numeric` or `logical`. However, each column should have the same type of data.

Use the `data.frame()` function to create a data frame:


```R
# Create a data frame
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

# Print the data frame
Data_Frame
```


<table class="dataframe">
<caption>A data.frame: 3 × 3</caption>
<thead>
	<tr><th scope=col>Training</th><th scope=col>Pulse</th><th scope=col>Duration</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Strength</td><td>100</td><td>60</td></tr>
	<tr><td>Stamina </td><td>150</td><td>30</td></tr>
	<tr><td>Other   </td><td>120</td><td>45</td></tr>
</tbody>
</table>




```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame

summary(Data_Frame)
```


<table class="dataframe">
<caption>A data.frame: 3 × 3</caption>
<thead>
	<tr><th scope=col>Training</th><th scope=col>Pulse</th><th scope=col>Duration</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Strength</td><td>100</td><td>60</td></tr>
	<tr><td>Stamina </td><td>150</td><td>30</td></tr>
	<tr><td>Other   </td><td>120</td><td>45</td></tr>
</tbody>
</table>




       Training             Pulse          Duration   
     Length:3           Min.   :100.0   Min.   :30.0  
     Class :character   1st Qu.:110.0   1st Qu.:37.5  
     Mode  :character   Median :120.0   Median :45.0  
                        Mean   :123.3   Mean   :45.0  
                        3rd Qu.:135.0   3rd Qu.:52.5  
                        Max.   :150.0   Max.   :60.0  



```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame[1]

Data_Frame[["Training"]]

Data_Frame$Training
```


<table class="dataframe">
<caption>A data.frame: 3 × 1</caption>
<thead>
	<tr><th scope=col>Training</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Strength</td></tr>
	<tr><td>Stamina </td></tr>
	<tr><td>Other   </td></tr>
</tbody>
</table>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'Strength'</li><li>'Stamina'</li><li>'Other'</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'Strength'</li><li>'Stamina'</li><li>'Other'</li></ol>



### Add rows


```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

# Add a new row
New_row_DF <- rbind(Data_Frame, c("Strength", 110, 110))

# Print the new row
New_row_DF
```


<table class="dataframe">
<caption>A data.frame: 4 × 3</caption>
<thead>
	<tr><th scope=col>Training</th><th scope=col>Pulse</th><th scope=col>Duration</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Strength</td><td>100</td><td>60 </td></tr>
	<tr><td>Stamina </td><td>150</td><td>30 </td></tr>
	<tr><td>Other   </td><td>120</td><td>45 </td></tr>
	<tr><td>Strength</td><td>110</td><td>110</td></tr>
</tbody>
</table>



### Add columns


```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

# Add a new column
New_col_DF <- cbind(Data_Frame, Steps = c(1000, 6000, 2000))

# Print the new column
New_col_DF
```


<table class="dataframe">
<caption>A data.frame: 3 × 4</caption>
<thead>
	<tr><th scope=col>Training</th><th scope=col>Pulse</th><th scope=col>Duration</th><th scope=col>Steps</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Strength</td><td>100</td><td>60</td><td>1000</td></tr>
	<tr><td>Stamina </td><td>150</td><td>30</td><td>6000</td></tr>
	<tr><td>Other   </td><td>120</td><td>45</td><td>2000</td></tr>
</tbody>
</table>



### Remove rows and cols


```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

# Remove the first row and column
Data_Frame_New <- Data_Frame[-c(1), -c(1)]

# Print the new data frame
Data_Frame_New
```


<table class="dataframe">
<caption>A data.frame: 2 × 2</caption>
<thead>
	<tr><th></th><th scope=col>Pulse</th><th scope=col>Duration</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>2</th><td>150</td><td>30</td></tr>
	<tr><th scope=row>3</th><td>120</td><td>45</td></tr>
</tbody>
</table>



### Dim


```R
Data_Frame <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

dim(Data_Frame)
ncol(Data_Frame)
nrow(Data_Frame)
length(Data_Frame)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>3</li><li>3</li></ol>




3



3



3


### Combining Dataframes in col dim or in row dim


```R
Data_Frame1 <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame2 <- data.frame (
  Training = c("Stamina", "Stamina", "Strength"),
  Pulse = c(140, 150, 160),
  Duration = c(30, 30, 20)
)

New_Data_Frame <- rbind(Data_Frame1, Data_Frame2)
New_Data_Frame
```


<table class="dataframe">
<caption>A data.frame: 6 × 3</caption>
<thead>
	<tr><th scope=col>Training</th><th scope=col>Pulse</th><th scope=col>Duration</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Strength</td><td>100</td><td>60</td></tr>
	<tr><td>Stamina </td><td>150</td><td>30</td></tr>
	<tr><td>Other   </td><td>120</td><td>45</td></tr>
	<tr><td>Stamina </td><td>140</td><td>30</td></tr>
	<tr><td>Stamina </td><td>150</td><td>30</td></tr>
	<tr><td>Strength</td><td>160</td><td>20</td></tr>
</tbody>
</table>




```R
Data_Frame3 <- data.frame (
  Training = c("Strength", "Stamina", "Other"),
  Pulse = c(100, 150, 120),
  Duration = c(60, 30, 45)
)

Data_Frame4 <- data.frame (
  Steps = c(3000, 6000, 2000),
  Calories = c(300, 400, 300)
)

New_Data_Frame1 <- cbind(Data_Frame3, Data_Frame4)
New_Data_Frame1
```


<table class="dataframe">
<caption>A data.frame: 3 × 5</caption>
<thead>
	<tr><th scope=col>Training</th><th scope=col>Pulse</th><th scope=col>Duration</th><th scope=col>Steps</th><th scope=col>Calories</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Strength</td><td>100</td><td>60</td><td>3000</td><td>300</td></tr>
	<tr><td>Stamina </td><td>150</td><td>30</td><td>6000</td><td>400</td></tr>
	<tr><td>Other   </td><td>120</td><td>45</td><td>2000</td><td>300</td></tr>
</tbody>
</table>



## Factors

Factors are used to categorize data. Examples of factors are:

* Demography: Male/Female
* Music: Rock, Pop, Classic, Jazz
* Training: Strength, Stamina
To create a factor, use the `factor()` function and add a vector as argument:


```R
# Create a factor
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"))

# Print the factor
music_genre
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>Jazz</li><li>Rock</li><li>Classic</li><li>Classic</li><li>Pop</li><li>Jazz</li><li>Rock</li><li>Jazz</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Classic'</li><li>'Jazz'</li><li>'Pop'</li><li>'Rock'</li></ol>
</details>



```R
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"), levels = c("Classic", "Jazz", "Pop", "Rock", "Other"))

levels(music_genre)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'Classic'</li><li>'Jazz'</li><li>'Pop'</li><li>'Rock'</li><li>'Other'</li></ol>




```R
length(music_genre)
```


8



```R
music_genre[3]
```


Classic
<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Classic'</li><li>'Jazz'</li><li>'Pop'</li><li>'Rock'</li><li>'Other'</li></ol>
</details>



```R
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"))

music_genre[3] <- "Pop"

music_genre[3]
```


Pop
<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Classic'</li><li>'Jazz'</li><li>'Pop'</li><li>'Rock'</li></ol>
</details>


Note that you cannot change the value of a specific item if it is not already specified in the factor. The following example will produce an error:

```
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"))

music_genre[3] <- "Opera"

music_genre[3]
```

However, if you have already specified it inside the levels argument, it will work:


```R
music_genre <- factor(c("Jazz", "Rock", "Classic", "Classic", "Pop", "Jazz", "Rock", "Jazz"), levels = c("Classic", "Jazz", "Pop", "Rock", "Opera"))

music_genre[3] <- "Opera"

music_genre[3]
```


Opera
<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Classic'</li><li>'Jazz'</li><li>'Pop'</li><li>'Rock'</li><li>'Opera'</li></ol>
</details>


# GRAPHIC AND DATA VISUALIZATION

## Simple plot


```R
plot(1,3)
plot(c(1, 8), c(3, 10))
plot(c(1, 2, 3, 4, 5), c(3, 7, 8, 9, 12))
plot(1:10)
```


    
![png](basic_r_files/basic_r_171_0.png)
    



    
![png](basic_r_files/basic_r_171_1.png)
    



    
![png](basic_r_files/basic_r_171_2.png)
    



    
![png](basic_r_files/basic_r_171_3.png)
    



```R
x <- c(1, 2, 3, 4, 5)
y <- c(3, 7, 8, 9, 12)

plot(x, y)
```


    
![png](basic_r_files/basic_r_172_0.png)
    



```R
plot(1:10, type="l")
```


    
![png](basic_r_files/basic_r_173_0.png)
    



```R
plot(x,y, main="My Graph", col="red", pch=25, cex=2, xlab="The x-axis", ylab="The y axis")
```


    
![png](basic_r_files/basic_r_174_0.png)
    


## Line


```R
plot(1:10, type="l", col="blue", lwd=5, lty = 6)
```


    
![png](basic_r_files/basic_r_176_0.png)
    



```R
line1 <- c(1,2,3,4,5,10)
line2 <- c(2,5,7,8,9,10)

plot(line1, type = "l", col = "blue", lwd=5, lty =4)
lines(line2, type="l", col = "red", lwd=2, lty = 2)
```


    
![png](basic_r_files/basic_r_177_0.png)
    



```R
# Load the required library
library(ggplot2)

# Customizing the ggplot
ggplot(data = mtcars, aes(x = wt, y = mpg)) +
  geom_point() +
  ggtitle("Car Weight vs. MPG") +
  xlab("Weight") +
  ylab("Miles Per Gallon")
```


    
![png](basic_r_files/basic_r_178_0.png)
    


## Scatter plots


```R
# day one, the age and speed of 12 cars:
x1 <- c(5,7,8,7,2,2,9,4,11,12,9,6)
y1 <- c(99,86,87,88,111,103,87,94,78,77,85,86)

# day two, the age and speed of 15 cars:
x2 <- c(2,2,8,1,15,8,12,9,7,3,11,4,7,14,12)
y2 <- c(100,105,84,105,90,99,90,95,94,100,79,112,91,80,85)

plot(x1, y1, main="Observation of Cars", xlab="Car age", ylab="Car speed", col="red", cex=2)
points(x2, y2, col="blue", cex=2)
```


    
![png](basic_r_files/basic_r_180_0.png)
    


## Pie Charts


```R
# Create a vector of pies
x <- c(10,20,30,40)

# Display the pie chart and start the first pie at 90 degrees
pie(x, init.angle = 90)
```


    
![png](basic_r_files/basic_r_182_0.png)
    



```R
# Create a vector of pies
x <- c(10,20,30,40)

# Create a vector of labels
mylabel <- c("Apples", "Bananas", "Cherries", "Dates")

# Display the pie chart with labels
pie(x, label = mylabel, main = "Fruits")
```


    
![png](basic_r_files/basic_r_183_0.png)
    



```R
# Create a vector of colors
colors <- c("blue", "yellow", "green", "violet")

# Display the pie chart with colors
pie(x, label = mylabel, main = "Fruits", col = colors)
```


    
![png](basic_r_files/basic_r_184_0.png)
    


The legend can be positioned as either:

`bottomright`, `bottom`, `bottomleft`, `left`, `topleft`, `top`, `topright`, `right`, `center`


```R
# Create a vector of labels
mylabel <- c("Apples", "Bananas", "Cherries", "Dates")

# Create a vector of colors
colors <- c("blue", "yellow", "green", "black")

# Display the pie chart with colors
pie(x, label = mylabel, main = "Pie Chart", col = colors)

# Display the explanation box
legend("bottomright", mylabel, fill = colors)
```


    
![png](basic_r_files/basic_r_186_0.png)
    


## Bars


```R
# x-axis values
x <- c("A", "B", "C", "D")

# y-axis values
y <- c(2, 4, 6, 8)

barplot(y, names.arg = x, col = "red", density = 10, width = c(1,2,3,4), horiz=TRUE)
```


    
![png](basic_r_files/basic_r_188_0.png)
    


# BASIC STATISTICS

The R language was developed by two statisticians. It has many built-in functionalities, in addition to libraries for the exact purpose of statistical analysis.

Statistics is the science of analyzing, reviewing and conclude data.

Some basic statistical numbers include:

* Mean, median and mode
* Minimum and maximum value
* Percentiles
* Variance and Standard Devation
* Covariance and Correlation
* Probability distributions

### Dataset

There is a popular built-in data set in R called `mtcars` (*Motor Trend Car Road Tests*), which is retrieved from the 1974 Motor Trend US Magazine.

In the examples below, we will use the `mtcars` data set, for statistical purposes:


```R
# Print the mtcars data set
mtcars
```


<table class="dataframe">
<caption>A data.frame: 32 × 11</caption>
<thead>
	<tr><th></th><th scope=col>mpg</th><th scope=col>cyl</th><th scope=col>disp</th><th scope=col>hp</th><th scope=col>drat</th><th scope=col>wt</th><th scope=col>qsec</th><th scope=col>vs</th><th scope=col>am</th><th scope=col>gear</th><th scope=col>carb</th></tr>
	<tr><th></th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><th scope=row>Mazda RX4</th><td>21.0</td><td>6</td><td>160.0</td><td>110</td><td>3.90</td><td>2.620</td><td>16.46</td><td>0</td><td>1</td><td>4</td><td>4</td></tr>
	<tr><th scope=row>Mazda RX4 Wag</th><td>21.0</td><td>6</td><td>160.0</td><td>110</td><td>3.90</td><td>2.875</td><td>17.02</td><td>0</td><td>1</td><td>4</td><td>4</td></tr>
	<tr><th scope=row>Datsun 710</th><td>22.8</td><td>4</td><td>108.0</td><td> 93</td><td>3.85</td><td>2.320</td><td>18.61</td><td>1</td><td>1</td><td>4</td><td>1</td></tr>
	<tr><th scope=row>Hornet 4 Drive</th><td>21.4</td><td>6</td><td>258.0</td><td>110</td><td>3.08</td><td>3.215</td><td>19.44</td><td>1</td><td>0</td><td>3</td><td>1</td></tr>
	<tr><th scope=row>Hornet Sportabout</th><td>18.7</td><td>8</td><td>360.0</td><td>175</td><td>3.15</td><td>3.440</td><td>17.02</td><td>0</td><td>0</td><td>3</td><td>2</td></tr>
	<tr><th scope=row>Valiant</th><td>18.1</td><td>6</td><td>225.0</td><td>105</td><td>2.76</td><td>3.460</td><td>20.22</td><td>1</td><td>0</td><td>3</td><td>1</td></tr>
	<tr><th scope=row>Duster 360</th><td>14.3</td><td>8</td><td>360.0</td><td>245</td><td>3.21</td><td>3.570</td><td>15.84</td><td>0</td><td>0</td><td>3</td><td>4</td></tr>
	<tr><th scope=row>Merc 240D</th><td>24.4</td><td>4</td><td>146.7</td><td> 62</td><td>3.69</td><td>3.190</td><td>20.00</td><td>1</td><td>0</td><td>4</td><td>2</td></tr>
	<tr><th scope=row>Merc 230</th><td>22.8</td><td>4</td><td>140.8</td><td> 95</td><td>3.92</td><td>3.150</td><td>22.90</td><td>1</td><td>0</td><td>4</td><td>2</td></tr>
	<tr><th scope=row>Merc 280</th><td>19.2</td><td>6</td><td>167.6</td><td>123</td><td>3.92</td><td>3.440</td><td>18.30</td><td>1</td><td>0</td><td>4</td><td>4</td></tr>
	<tr><th scope=row>Merc 280C</th><td>17.8</td><td>6</td><td>167.6</td><td>123</td><td>3.92</td><td>3.440</td><td>18.90</td><td>1</td><td>0</td><td>4</td><td>4</td></tr>
	<tr><th scope=row>Merc 450SE</th><td>16.4</td><td>8</td><td>275.8</td><td>180</td><td>3.07</td><td>4.070</td><td>17.40</td><td>0</td><td>0</td><td>3</td><td>3</td></tr>
	<tr><th scope=row>Merc 450SL</th><td>17.3</td><td>8</td><td>275.8</td><td>180</td><td>3.07</td><td>3.730</td><td>17.60</td><td>0</td><td>0</td><td>3</td><td>3</td></tr>
	<tr><th scope=row>Merc 450SLC</th><td>15.2</td><td>8</td><td>275.8</td><td>180</td><td>3.07</td><td>3.780</td><td>18.00</td><td>0</td><td>0</td><td>3</td><td>3</td></tr>
	<tr><th scope=row>Cadillac Fleetwood</th><td>10.4</td><td>8</td><td>472.0</td><td>205</td><td>2.93</td><td>5.250</td><td>17.98</td><td>0</td><td>0</td><td>3</td><td>4</td></tr>
	<tr><th scope=row>Lincoln Continental</th><td>10.4</td><td>8</td><td>460.0</td><td>215</td><td>3.00</td><td>5.424</td><td>17.82</td><td>0</td><td>0</td><td>3</td><td>4</td></tr>
	<tr><th scope=row>Chrysler Imperial</th><td>14.7</td><td>8</td><td>440.0</td><td>230</td><td>3.23</td><td>5.345</td><td>17.42</td><td>0</td><td>0</td><td>3</td><td>4</td></tr>
	<tr><th scope=row>Fiat 128</th><td>32.4</td><td>4</td><td> 78.7</td><td> 66</td><td>4.08</td><td>2.200</td><td>19.47</td><td>1</td><td>1</td><td>4</td><td>1</td></tr>
	<tr><th scope=row>Honda Civic</th><td>30.4</td><td>4</td><td> 75.7</td><td> 52</td><td>4.93</td><td>1.615</td><td>18.52</td><td>1</td><td>1</td><td>4</td><td>2</td></tr>
	<tr><th scope=row>Toyota Corolla</th><td>33.9</td><td>4</td><td> 71.1</td><td> 65</td><td>4.22</td><td>1.835</td><td>19.90</td><td>1</td><td>1</td><td>4</td><td>1</td></tr>
	<tr><th scope=row>Toyota Corona</th><td>21.5</td><td>4</td><td>120.1</td><td> 97</td><td>3.70</td><td>2.465</td><td>20.01</td><td>1</td><td>0</td><td>3</td><td>1</td></tr>
	<tr><th scope=row>Dodge Challenger</th><td>15.5</td><td>8</td><td>318.0</td><td>150</td><td>2.76</td><td>3.520</td><td>16.87</td><td>0</td><td>0</td><td>3</td><td>2</td></tr>
	<tr><th scope=row>AMC Javelin</th><td>15.2</td><td>8</td><td>304.0</td><td>150</td><td>3.15</td><td>3.435</td><td>17.30</td><td>0</td><td>0</td><td>3</td><td>2</td></tr>
	<tr><th scope=row>Camaro Z28</th><td>13.3</td><td>8</td><td>350.0</td><td>245</td><td>3.73</td><td>3.840</td><td>15.41</td><td>0</td><td>0</td><td>3</td><td>4</td></tr>
	<tr><th scope=row>Pontiac Firebird</th><td>19.2</td><td>8</td><td>400.0</td><td>175</td><td>3.08</td><td>3.845</td><td>17.05</td><td>0</td><td>0</td><td>3</td><td>2</td></tr>
	<tr><th scope=row>Fiat X1-9</th><td>27.3</td><td>4</td><td> 79.0</td><td> 66</td><td>4.08</td><td>1.935</td><td>18.90</td><td>1</td><td>1</td><td>4</td><td>1</td></tr>
	<tr><th scope=row>Porsche 914-2</th><td>26.0</td><td>4</td><td>120.3</td><td> 91</td><td>4.43</td><td>2.140</td><td>16.70</td><td>0</td><td>1</td><td>5</td><td>2</td></tr>
	<tr><th scope=row>Lotus Europa</th><td>30.4</td><td>4</td><td> 95.1</td><td>113</td><td>3.77</td><td>1.513</td><td>16.90</td><td>1</td><td>1</td><td>5</td><td>2</td></tr>
	<tr><th scope=row>Ford Pantera L</th><td>15.8</td><td>8</td><td>351.0</td><td>264</td><td>4.22</td><td>3.170</td><td>14.50</td><td>0</td><td>1</td><td>5</td><td>4</td></tr>
	<tr><th scope=row>Ferrari Dino</th><td>19.7</td><td>6</td><td>145.0</td><td>175</td><td>3.62</td><td>2.770</td><td>15.50</td><td>0</td><td>1</td><td>5</td><td>6</td></tr>
	<tr><th scope=row>Maserati Bora</th><td>15.0</td><td>8</td><td>301.0</td><td>335</td><td>3.54</td><td>3.570</td><td>14.60</td><td>0</td><td>1</td><td>5</td><td>8</td></tr>
	<tr><th scope=row>Volvo 142E</th><td>21.4</td><td>4</td><td>121.0</td><td>109</td><td>4.11</td><td>2.780</td><td>18.60</td><td>1</td><td>1</td><td>4</td><td>2</td></tr>
</tbody>
</table>




```R
# Use the question mark to get information about the data set

?mtcars
```

    mtcars                package:datasets                 R Documentation
    
    _M_o_t_o_r _T_r_e_n_d _C_a_r _R_o_a_d _T_e_s_t_s
    
    _D_e_s_c_r_i_p_t_i_o_n:
    
         The data was extracted from the 1974 _Motor Trend_ US magazine,
         and comprises fuel consumption and 10 aspects of automobile design
         and performance for 32 automobiles (1973-74 models).
    
    _U_s_a_g_e:
    
         mtcars
         
    _F_o_r_m_a_t:
    
         A data frame with 32 observations on 11 (numeric) variables.
    
           [, 1]  mpg   Miles/(US) gallon                        
           [, 2]  cyl   Number of cylinders                      
           [, 3]  disp  Displacement (cu.in.)                    
           [, 4]  hp    Gross horsepower                         
           [, 5]  drat  Rear axle ratio                          
           [, 6]  wt    Weight (1000 lbs)                        
           [, 7]  qsec  1/4 mile time                            
           [, 8]  vs    Engine (0 = V-shaped, 1 = straight)      
           [, 9]  am    Transmission (0 = automatic, 1 = manual) 
           [,10]  gear  Number of forward gears                  
           [,11]  carb  Number of carburetors                    
          
    _N_o_t_e:
    
         Henderson and Velleman (1981) comment in a footnote to Table 1:
         'Hocking [original transcriber]'s noncrucial coding of the Mazda's
         rotary engine as a straight six-cylinder engine and the Porsche's
         flat engine as a V engine, as well as the inclusion of the diesel
         Mercedes 240D, have been retained to enable direct comparisons to
         be made with previous analyses.'
    
    _S_o_u_r_c_e:
    
         Henderson and Velleman (1981), Building multiple regression models
         interactively.  _Biometrics_, *37*, 391-411.
    
    _E_x_a_m_p_l_e_s:
    
         require(graphics)
         pairs(mtcars, main = "mtcars data", gap = 1/4)
         coplot(mpg ~ disp | as.factor(cyl), data = mtcars,
                panel = panel.smooth, rows = 1)
         ## possibly more meaningful, e.g., for summary() or bivariate plots:
         mtcars2 <- within(mtcars, {
            vs <- factor(vs, labels = c("V", "S"))
            am <- factor(am, labels = c("automatic", "manual"))
            cyl  <- ordered(cyl)
            gear <- ordered(gear)
            carb <- ordered(carb)
         })
         summary(mtcars2)
         


```R
Data_Cars <- mtcars # create a variable of the mtcars data set for better organization

# Use dim() to find the dimension of the data set
dim(Data_Cars)

# Use names() to find the names of the variables from the data set
names(Data_Cars)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>32</li><li>11</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'mpg'</li><li>'cyl'</li><li>'disp'</li><li>'hp'</li><li>'drat'</li><li>'wt'</li><li>'qsec'</li><li>'vs'</li><li>'am'</li><li>'gear'</li><li>'carb'</li></ol>



Use the rownames() function to get the name of each row in the first column, which is the name of each car:


```R
Data_Cars <- mtcars

rownames(Data_Cars)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'Mazda RX4'</li><li>'Mazda RX4 Wag'</li><li>'Datsun 710'</li><li>'Hornet 4 Drive'</li><li>'Hornet Sportabout'</li><li>'Valiant'</li><li>'Duster 360'</li><li>'Merc 240D'</li><li>'Merc 230'</li><li>'Merc 280'</li><li>'Merc 280C'</li><li>'Merc 450SE'</li><li>'Merc 450SL'</li><li>'Merc 450SLC'</li><li>'Cadillac Fleetwood'</li><li>'Lincoln Continental'</li><li>'Chrysler Imperial'</li><li>'Fiat 128'</li><li>'Honda Civic'</li><li>'Toyota Corolla'</li><li>'Toyota Corona'</li><li>'Dodge Challenger'</li><li>'AMC Javelin'</li><li>'Camaro Z28'</li><li>'Pontiac Firebird'</li><li>'Fiat X1-9'</li><li>'Porsche 914-2'</li><li>'Lotus Europa'</li><li>'Ford Pantera L'</li><li>'Ferrari Dino'</li><li>'Maserati Bora'</li><li>'Volvo 142E'</li></ol>



From the examples above, we have found out that the data set has 32 observations (Mazda RX4, Mazda RX4 Wag, Datsun 710, etc) and 11 variables (mpg, cyl, disp, etc).

A variable is defined as something that can be measured or counted.

Here is a brief explanation of the variables from the mtcars data set:


| Variable Name | Description |
|:-------|------:|
|mpg|Miles/(US) Gallon|
|cyl|Number of cylinders|
|disp|Displacement|
|hp|Gross horsepower|
|drat|Rear axle ratio|
|wt|Weight (1000 lbs)|
|qsec|1/4 mile time|
|vs|Engine (0 = V-shaped, 1 = straight)|
|am|Transmission (0 = automatic, 1 = manual)|
|gear|Number of forward gears|
|carb|Number of carburetors|

#### Print Variable Values
If you want to print all values that belong to a variable, access the data frame by using the `$` sign, and the name of the variable (for example `cyl` (cylinders)):

From the examples above, we have found out that the data set has 32 observations (Mazda RX4, Mazda RX4 Wag, Datsun 710, etc) and 11 variables (mpg, cyl, disp, etc).

A variable is defined as something that can be measured or counted.

Here is a brief explanation of the variables from the mtcars data set:


| Variable Name|Description|
|:--------|---------:|
|mpg|Miles/(US) Gallon|
cyl	Number of cylinders
disp	Displacement
hp	Gross horsepower
drat	Rear axle ratio
wt	Weight (1000 lbs)
qsec	1/4 mile time
vs	Engine (0 = V-shaped, 1 = straight)
am	Transmission (0 = automatic, 1 = manual)
gear	Number of forward gears
carb	Number of carburetors


```R
Data_Cars <- mtcars

Data_Cars$cyl
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>6</li><li>6</li><li>4</li><li>6</li><li>8</li><li>6</li><li>8</li><li>4</li><li>4</li><li>6</li><li>6</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>4</li><li>4</li><li>4</li><li>4</li><li>8</li><li>8</li><li>8</li><li>8</li><li>4</li><li>4</li><li>4</li><li>8</li><li>6</li><li>8</li><li>4</li></ol>




```R
sort(Data_Cars$cyl)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>4</li><li>4</li><li>4</li><li>4</li><li>4</li><li>4</li><li>4</li><li>4</li><li>4</li><li>4</li><li>4</li><li>6</li><li>6</li><li>6</li><li>6</li><li>6</li><li>6</li><li>6</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li><li>8</li></ol>



### Analyzing the data


```R
summary(Data_Cars)
```


          mpg             cyl             disp             hp       
     Min.   :10.40   Min.   :4.000   Min.   : 71.1   Min.   : 52.0  
     1st Qu.:15.43   1st Qu.:4.000   1st Qu.:120.8   1st Qu.: 96.5  
     Median :19.20   Median :6.000   Median :196.3   Median :123.0  
     Mean   :20.09   Mean   :6.188   Mean   :230.7   Mean   :146.7  
     3rd Qu.:22.80   3rd Qu.:8.000   3rd Qu.:326.0   3rd Qu.:180.0  
     Max.   :33.90   Max.   :8.000   Max.   :472.0   Max.   :335.0  
          drat             wt             qsec             vs        
     Min.   :2.760   Min.   :1.513   Min.   :14.50   Min.   :0.0000  
     1st Qu.:3.080   1st Qu.:2.581   1st Qu.:16.89   1st Qu.:0.0000  
     Median :3.695   Median :3.325   Median :17.71   Median :0.0000  
     Mean   :3.597   Mean   :3.217   Mean   :17.85   Mean   :0.4375  
     3rd Qu.:3.920   3rd Qu.:3.610   3rd Qu.:18.90   3rd Qu.:1.0000  
     Max.   :4.930   Max.   :5.424   Max.   :22.90   Max.   :1.0000  
           am              gear            carb      
     Min.   :0.0000   Min.   :3.000   Min.   :1.000  
     1st Qu.:0.0000   1st Qu.:3.000   1st Qu.:2.000  
     Median :0.0000   Median :4.000   Median :2.000  
     Mean   :0.4062   Mean   :3.688   Mean   :2.812  
     3rd Qu.:1.0000   3rd Qu.:4.000   3rd Qu.:4.000  
     Max.   :1.0000   Max.   :5.000   Max.   :8.000  


The `summary()` function returns six statistical numbers for each variable:

* Min
* First quantile (percentile)
* Median - The middle value
* Mean - The average value
* Third quantile (percentile)
* Max

You can explore also:
* Mode - The most common value

### max and min


```R
# max and min

Data_Cars <- mtcars
max(Data_Cars$hp)
min(Data_Cars$hp)

#  find the index position of the max and min value in the table:
which.max(Data_Cars$hp)
which.min(Data_Cars$hp)

rownames(Data_Cars)[which.max(Data_Cars$hp)]
rownames(Data_Cars)[which.min(Data_Cars$hp)]

```


335



52



31



19



'Maserati Bora'



'Honda Civic'


### mean, mode, median


```R
# find the sum of all values, and divide the sum by the number of values.
mean(Data_Cars$wt)

# If there are two numbers in the middle, you must divide the sum of those numbers by two, to find the median.

# Luckily, R has a function that does all of that for you: 
# Just use the median() function to find the middle value:
median(Data_Cars$wt)

# R does not have a function to calculate the mode. 
# However, we can create our own function to find it.
names(sort(-table(Data_Cars$wt)))[1]
```


3.21725



3.325



'3.44'


### Percentiles

Quartiles are data divided into four parts, when sorted in an ascending order:

* The value of the first quartile cuts off the first 25% of the data
* The value of the second quartile cuts off the first 50% of the data
* The value of the third quartile cuts off the first 75% of the data
* The value of the fourth quartile cuts off the 100% of the data


```R
# c() specifies which percentile you want
quantile(Data_Cars$wt, c(0.75))

quantile(Data_Cars$wt)
```


<strong>75%:</strong> 3.61



<style>
.dl-inline {width: auto; margin:0; padding: 0}
.dl-inline>dt, .dl-inline>dd {float: none; width: auto; display: inline-block}
.dl-inline>dt::after {content: ":\0020"; padding-right: .5ex}
.dl-inline>dt:not(:first-of-type) {padding-left: .5ex}
</style><dl class=dl-inline><dt>0%</dt><dd>1.513</dd><dt>25%</dt><dd>2.58125</dd><dt>50%</dt><dd>3.325</dd><dt>75%</dt><dd>3.61</dd><dt>100%</dt><dd>5.424</dd></dl>



# EXERCISES & QUIZ
you can do some more R exercises [here](https://www.w3schools.com/r/r_exercises.asp)

you also can do a simple R quiz [here](https://www.w3schools.com/r/r_quiz.asp)

or, ìf you want, get a [R certificate](https://www.w3schools.com/r/r_exam.asp)
