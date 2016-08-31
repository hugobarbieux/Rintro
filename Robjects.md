# R basics: objects for storing data

Once you've done a few things in R to see how it works, to go further you'll probably need to understand some aspects of R in more depth. Let's start with data types.

## Confusingly similar data types: vectors vs lists and matrices vs data frames

R has a confusing range of data types, many of which perform similar functions. For example you can store a data table in either a *matrix* or a *data frame*, and you can store a list of items in a *list* or a *vector*. So which do you use when?

Broadly speaking, you would use a **vector** to store a list of data (such as a column), and a **data frame** to store a whole dataset. 

This is why:

**Vectors** are lists but they *must all be the same type of item*. This makes sense in data when you tend to be dealing with a column of numbers, or a column of text entries.

In contrast a **list** can contain items of different types, and can even contain more lists.

The difference between data frames and matrices is similar: all columns in a **matrix** must be the same data type, whereas different columns can be of different types in a **data frame**. In fact, a data frame is really a *list* of *vectors* (i.e. columns) of equal length.

A good way to understand this is to manually create a table in R from a series of columns. 

## Creating a data frame from a series of vectors

Normally you create a data frame by importing data in some way. However, creating one from scratch is useful in understanding the structure.

Each column in a data frame, then, is created as a **vector**, and then those vectors are joined to form the data frame. Here's the code to do that:

`name <- c('Paul', 'Sarah', 'Joe')`

`age <- c(25, 35, 28)`

`city <- c('Birmingham', 'Brighton', 'Liverpool')`

`mynewtable <- data.frame(name, age, city)`

I'll explain these commands that create vectors and data frames below. For now I just want to focus on the structure.

So, we have 3 lines creating 3 vector objects (variables). Then the final 4th line uses those 3 variables to create a data frame and store it in a variable called `mynewtable`. 

The *name* of each vector *variable* is important, because this is used as the *column name* in the data frame. 

You can find out the column names by using `colnames()` like so:

`colnames(mynewtable)`

A data frame also has *row names*. Unless you specify them, these are normally added as automatic *indexes* (1 for row 1, 2 for row 2 and so on). You can see them by using the `rownames()` function like so:

`rownames(mynewtable)`

But you can also set the rownames like so:

`rownames(mynewtable) <- name` 

In this case, the number of items in that vector should be the same as the number of items in the data frame.

Now to dig deeper into vectors and data frames.

## Vectors: lists of items of the same type

A **vector** is a way of storing a list of items. It is created using `c()` like so:

`myvector <- c(1, 3, 5)`

You can add items to the vector like so:

`myvector <- c(myvector, 6)`

Or combine lists like so:

`myvector <- c(myvector, anothervector)`

Note that items will be added *in that order*, they will not be reordered in numeric or alphabetical order.

If the two vectors contain different types of data (for example one vector contains numbers and the other contains strings) then the resulting vector items will be changed to strings. You can find out what type of data is stored in the vector by using `class` like so:

`class(myvector)`.

You can **remove items** from a vector by index like so:

`myvector <- c(myvector[1:3])`

Or you can use a negative index to indicate you want to keep everything *but* that item. This for example will give you all items from `myvector` apart from the first one:

`myvector <- c(myvector[-1])`

## Data frames

Datasets in R are created using the `data.frame()` function as detailed above, but are also created by other functions like `read.csv()` and `read.table()`.

You can access data in a data frame like you do in Excel, using row and column references. For example: 

First row, first cell:

`mydata[1,1]`

First row:

`mydata[1,]`

First column:

`mydata[1,]`

You can access individual columns by column name by using the $ sign between the variable name and the column name like so:

`mydata$mycolumn`

## Other data types: strings, integers, numeric and boolean (logical)

As well as the data types outlined above, you can also store more basic types of data in R. For example you might want to store a URL, or a single number, or a TRUE/FALSE value.

You do that in the same way, using `<-`, like so:

`urltograb <- 'http://bbc.co.uk/story.html'`

`myage <- 23`

`temp <- 12.5`

`yesorno <- TRUE`

If you need to use a number, string or logical value (TRUE/FALSE) more than once, it may be worth storing it in a variable. The main advantage is that you can just change the variable once to affect all instances where that value is used.

Bear in mind that you can only do certain things with certain variables: for example you cannot perform calculations on strings of characters, and you cannot combine numbers in the same way that you combine strings of text.

You can find out what type a variable is by using class. For example `class(urltograb)` would return `"character"`, meaning **character**. Type `class(yesorno)` and you will get `"logical"`. `class(myage)` and `class(temp)` would both return `"numeric"`. Note that there is no distinction between whole numbers and floating decimals as there is in other languages. The [difference between numeric and integer classes is quite complicated and dull](https://stackoverflow.com/questions/23660094/whats-the-difference-between-integer-class-and-numeric-class-in-r) and not that important.
