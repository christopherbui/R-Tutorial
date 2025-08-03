# R Tutorial

Welcome 成嘉敏 to this introductory R tutorial. I hope it can give you better context when working with this `[insert adjective]` language.

Things to know:

- R fundamentally is a programming language.
- It is best suited for data analysis due to efficient methods that require less typing, allowing for faster workflows that otherwise would take longer in traditional programming language syntax structure.
- Although R syntax mostly follows fundamental structure of other programming languages, its syntax is also very R specific (Tradeoff: increased ambiguity for increased functionality).
- Because of R's syntax and it being a programming language, keep in mind:
  - There's more than 1 way to do the same thing (applies to all languages).
  - You can do something the "R" way.
  - Or, you can do it the "general programming language way".

------

How do you know if something is done in "R" way?

You have limited programming experience, so it's hard to identify something as R specific since you can't compare it to other common syntax structure of other languages. But that's ok!

You'll be working with **dataframes** (basically a data table) mostly, and in this situation, it is very easy to recognize R specific methods vs general programming methods for the same task.

Especially with dataframes, the R way generally requires less typing and allows you to get your desired results faster. An example shown below:

```R
# load packages that you need
library(dplyr)

# create a dataframe
df <- data.frame(
  ID = 1:5,
  Name = c("Alice", "Bob", "Chris", "David", "Eva"),
  Age = c(23, 19, 30, 12, 8),
  Score = c(88.5, 92.0, 0.0, 85.0, 90.5)
)
#> df
#  ID  Name Age Score
#1  1 Alice  23  88.5
#2  2   Bob  19  92.0
#3  3 Chris  30   0.0
#4  4 David  12  85.0
#5  5   Eva   8  90.5

####### TASK: FIND PEOPLE WHO ARE > 13 YEARS OLD #######

# R Way --------------------------------------------
df_filtered <- dplyr::filter(df, Age > 13)
								# OR
df_filtered <- filter(df, Age > 13)
# The above 2 lines are the same. In the 1st, it is saying, "from the dplyr package, use the filter function". In the 2nd, your Rstudio environment already knows what package the filter function is associated with, so no need to type the dplyr:: part.

# Sometimes you need to specify dplyr::filter because you might use 2 different packages that have functions with the same name, so Rstudio needs to know which one you want specifically.

#> df_filtered
#  ID  Name Age Score
#1  1 Alice  23  88.5
#2  2   Bob  19  92.0
#3  3 Chris  30   0.0


# General Programming Way --------------------------
df_filtered <- df[df$Age > 13, ]
#> df_filtered
#  ID  Name Age Score
#1  1 Alice  23  88.5
#2  2   Bob  19  92.0
#3  3 Chris  30   0.0

```

The R way has special methods like `filter`, and special syntax like `%>%` to get results conveniently. The general programming way filters information through an **indexing** perspective. Indexing will be explained in the *arrays* section.

Overall, you can use any workflow you want. It's ok to mix and match. I just want to expose you so you understand what's going on when you encounter these situations.

With that in mind, いきましょう！

# Resources

- [W3 Schools](https://www.w3schools.com/r/)

------

# Data Types

In programming, anything that you interact with is considered a general **object**. There are different **types of objects**, or **classes**. Objects of different types have different capabilities.

Fundamental Data Types:

| General Term | R Term                    | Example                         | Description                                                  |
| ------------ | ------------------------- | ------------------------------- | ------------------------------------------------------------ |
| Integer      | Integer                   | 1, 9, 28                        | Whole numbers                                                |
| Float        | Numeric                   | 0.5, 3.14, 99.0                 | Decimal numbers                                              |
| String       | Character                 | "Hello", 'world', 'x'           | Text                                                         |
| Array        | Vector / List             | c(1, 2, 3), c("hello", "world") | A list-like object that holds other objects (i.e. numeric, string, or any other type) |
| Dictionary   | Named Vector / Named List | list(student="chris", age="24") | A list-like object, but has a **key** associated with a **value** |
| Boolean      | Logical                   | TRUE, T, FALSE, F               | True or false values                                         |

**Note:** 

- The table provides the common names of data types across most programming languages and their names in R.
- In R when working with dataframes, you might have column labels that specify the data type for that column. Most likely it is a **tibble** dataframe. This is still a normal dataframe, but some guy wanted to add extra functionality to a normal dataframe, and his version grew in popularity.

However you interact with a default dataframe, you can do the same with a tibble. The only difference is how information is displayed. Notice for the tibble, it specifies the column data type for "easier" interpretation. These types are not part of the dataframe itself. They only show up in the console when you view it. `<int>` is *integer*. `<chr>` is *character*, or *string*. `<dbl>` is *double*, or *numeric* in R (decimal numbers).

- *Double* is the general term for a float (decimal number) with certain precision (i.e. 17 decimal places). You just need to know float overall, but now you know what *double* is if it appears.

```R
# Example of a tibble dataframe vs default dataframe
library(tibble)

df_tib <- tibble(
  ID = 1:5,
  Name = c("Alice", "Bob", "Chris", "David", "Eva"),
  Age = c(23, 19, 30, 12, 8),
  Score = c(88.5, 92.0, 0.0, 85.0, 90.5)
)
df <- data.frame(
  ID = 1:5,
  Name = c("Alice", "Bob", "Chris", "David", "Eva"),
  Age = c(23, 19, 30, 12, 8),
  Score = c(88.5, 92.0, 0.0, 85.0, 90.5)
)

#> df_tib
# A tibble: 5 × 4
#     ID Name    Age Score
#  <int> <chr> <dbl> <dbl>
#1     1 Alice    23  88.5
#2     2 Bob      19  92  
#3     3 Chris    30   0  
#4     4 David    12  85  
#5     5 Eva       8  90.5

#> df
#  ID  Name Age Score
#1  1 Alice  23  88.5
#2  2   Bob  19  92.0
#3  3 Chris  30   0.0
#4  4 David  12  85.0
#5  5   Eva   8  90.5
```

## Integer

Whole numbers.

- 1, 9, 28, etc.

## Float

Decimal numbers.

- 0.5, 3.14, 99.0
- Can also be referenced as a *double*, which is just a decimal with a certain precision of 17 decimal places.
- Called *numeric* in R.

## String

Text.

- It can be one character "a", or a whole word, "apple".
- **For strings in R, double quotes "", or single quotes '' is ok.** I note this because in other languages, strings usually are only allowed to be double "". You can use either double or single quotes, or use them interchangeably. Just use what's best for your situation.
- In R, strings of any length is just called *character*. 👎

## Boolean

Booleans are simply `TRUE` or `FALSE`.

- Code will run if conditions are `TRUE`.
- Booleans help set what code is run in certain scenarios.
  - *"If condition is TRUE, do something. If it's FALSE, do something else."*

- "true" is represented as:  `TRUE` , `T`, any non-zero number (1, 23, -4, etc.).
- "false" is represented as:  `FALSE`,  `F`, zero (0).

## Array

A list-like object that holds other objects.

This is where R is different from other languages 👎, making things more confusing for no reason, so I'll try to explain clearly.

### Vector

In R, a basic array can be a **VECTOR**, created with `c()`. The *c* means *combine*.

- It's called a vector because in mathematics, vectors are 1-Dimensional (flat).

```R
# create an array using a vector
fruits <- c("apple", "orange", "banana")
scores <- c(82, 75, 95)
```

**Items in a VECTOR need to all be the same type.** If you define a vector with mixed types, R will auto convert them to be the same type. Example:

```R
# R converting integer 8 to string "8" to meet vector's requirements of
# all items in the vector to be the same type.
x <- c(8, "hi")
print(x)
[1] "8"  "hi"

# R converts integers to floats (called numeric in R) because of the 3.1
y <- c(1, 2, 3.1)
print(y)
[1] 1.0 2.0 3.1
```

### List

In R, a basic array can also be a **LIST**, created with `list()`.

**The difference between VECTOR and LIST is that list can have mixed types.**

```R
# create an array using a list
fruits <- list("apple", "orange", "banana", 9)
scores <- list(82, 75, 95, "hello")

# the [[1]], [[2]], [[3]], [[4]] is just the index, or each item's position in the list
# Note: The list has both string (character) & integer items.
print(fruits)
#[[1]]
#[1] "apple"
#
#[[2]]
#[1] "orange"
#
#[[3]]
#[1] "banana"
#
#[[4]]
#[1] 9

# verify item type (class).
class(fruits[[1]])
#[1] "character"
class(fruits[[4]])
#[1] "numeric"
```

**🛑⚠️🚧 SKIP TO THE INDEXING SECTION, THEN RETURN TO THE DICTIONARY SECTION FOR BETTER UNDERSTANDING**

## Dictionary

A dictionary is a list-like object that has `key : value` pairs.

Just like how a list can be created with a vector `c()`, or list `list()` in R, a dictionary can be made with a `named vector` or a `named list`.

Each item in a dictionary is the **value**.

Each item has a **unique "name"** associated with it. This is the **key**.

Ideally, all keys *should* be unique. Values can be duplicates. 

- A key is like a person's unique ID or home address.
- When I go to a specific key in a dictionary, I get the value paired with that key. This is like saying: If I go to Raymond (key), I expect to get Jiamin (value).
- **Minor Note:** R dictionaries can have duplicate keys, but it will only return the value paired with the first key.

### Dictionary Using Vector

```R
# Create a dictionary with vector, c()
# One dictionary uses quotes for the keys. Both are the same.
# Use what you prefer.
my_dict <- c(
  chris = 13,
  jiamin = 13,
  joe = 5,
  chandelle = 20
)
my_dict <- c(
  "chris" = 13,
  "jiamin" = 13,
  "joe" = 5,
  "chandelle" = 20
)
# my_dict
#    chris    jiamin       joe chandelle 
#       13        13         5        20 

# get value using key
jiamin_score <- my_dict[["jiamin"]]
# jiamin_score
# [1] 13

# get value using index
joe_score <- my_dict[[3]]
# joe_score
# [1] 5
```

Each key is associated with a value. Values can be the same. What matters for a functional dictionary is that the keys are unique.

**Note:** Above `dict[[key]]` is used to get the value. Note the double `[[ ]]` gives you the actual value as we learned in the *Indexing* section. Single `[ ]` instead will return a list containing the value.

To get a list of the keys, you can use the `names()` function.

```R
# get list of keys from dictionary above
my_keys <- names(my_dict)
# my_keys
# [1] "chris"     "jiamin"    "joe"       "chandelle"
```

### Dictionary Using `list()`

We learned in *Array* section that a vector and a `list()` can both be used to make a list. Similarly, we can use both to make a dictionary. Above, we used a *named vector*. Now, we'll use a *named list*.

```R
# Create a dictionary with list()
# One dictionary uses quotes for the keys. Both are the same.
# Use what you prefer.
my_dict <- list(
  chris = 13,
  jiamin = 13,
  joe = "5",
  chandelle = "20"
)
my_dict <- list(
  "chris" = 13,
  "jiamin" = 13,
  "joe" = "5",
  "chandelle" = "20"
)

# get value using key
jiamin_score <- my_dict[["jiamin"]]
# jiamin_score
# [1] 13

# get value using index
joe_score <- my_dict[[3]]
# joe_score
# [1] "5"

# get list of keys from dictionary
names(my_dict)
# [1] "chris"     "jiamin"    "joe"       "chandelle"
```

**Note:** 

- Remember for lists made with `c()`, all items must be (or will be converted to) the same type (i.e. integer/float/string). But a list made with `list()`, it can hold items of different types.
- Similarly, for dictionaries made with `c()`, the values must be the same type. Dictionaries made with `list()` can hold values of different types as seen above.
- In the 1st dictionary made with vector `c()`, Joe's score is integer 5. In the 2nd dictionary made with `list()`, Joe's score is string 5. 
- **You can get values by the specific key or index. Which to use will depend on your own need and situation.**

# Indexing

An **index** is a number that specifies the **position** of an item in a list-like object.

R is a **1-based index language**, meaning the first position starts with **1**.

- 99% of all other programming languages is 0-based index, meaning the first item position is 0.

To get an item from a list-like object, we use the syntax: `object[index]`.

To get a range of items, we do: `object[index_1:index_2]`

```R
# create a vector list of scores
scores <- c(23, 17, 55, 98)

# get the 1st & 3rd item
scores[1]	# 23
scores[3]	# 55
```

Above, we indexed a vector. This is the simplest form of accessing a list-like object, and is most similar to other languages.

Below, we will index from R's `list()` object. **Indexing from R's `list()` object returns either a `list()` or a specific item**.

- `[ ]` --> returns a list containing the item
- `[[ ]]` --> returns the actual item



**Get a list containing the item:**

```R
# create a list() list of scores
scores <- list(23, 17, 55, 98)

# returns a list() with the one item at the 1st index
# the displayed [[1]] below is just the index of the item in the returned list
# since you passed in one index, your returned list has one item, so the displayed index is always [[1]]
scores[1]
#[[1]]
#[1] 23
scores[3]
#[[1]]
#[1] 55

# get list containing 2nd to 4th item
> scores[2:4]
#[[1]]
#[1] 17
#
#[[2]]
#[1] 55
#
#[[3]]
#[1] 98

# NOTE: all results above are lists, not the actual item
```

**Get the actual item in list:**

```R
# get the actual item in the list() list
# note how the results don't have the [[1]] above, because you are getting the actual item, and not returning a list with one item in it
scores <- list(23, 17, 55, 98)

# get the 1st item
scores[[1]]
#[1] 23

# get the 3rd item
scores[[3]]
#[1] 55
```

# Variables

Variables are names we use to store data, or reference an object (i.e. a list, a dataframe, etc.)

**In R, we use `<-` to assign data to a variable.**

```R
# assign string to variable
name <- "chris"

# assign list to variable
my_list <- c("apple", "orange", "grape")

# assign value in list to variable
favorite_food <- my_list[[2]]
```

Variables allow us to reference data and interact with it more efficiently, and not needing to type the same thing repeatedly.

If data needs updating, then we simply change the value in the variable assignment, without having to change the rest of the code.

```R
user_id <- "oxford8888"
password <- "ja84$@%97"

# BAD
# this is not efficient, especially if information is long
# if password changes, we would have to manually change the print statement
print("user id: oxford8888 has password: ja84$@%97")


# GOOD
# variables allow efficient referencing and changes

# uses paste0()
print(paste0("user id: ", user_id, " has password: ", password))
#[1] "user id: oxford8888 has password: ja84$@%97"

# uses glue()
print(glue("user id: {user_id} has password: {password}"))
# user id: oxford8888 has password: ja84$@%97
```

**Note:**

- `paste0()` is the default way to combine variables and strings. You pass in variables or type your own strings, and each part is separated with a comma `,` to produce 1 final string.
- `glue()` also produces 1 final string, but I prefer this way since you use `{variable_name}` to pass in variables. This is more like Python, and just my preference, but use what you feel is best.



 ## Operators

Operators manage **boolean** (`TRUE`, `FALSE`) values, and depending on the boolean, it drives the logic of the code.

**The result of a statement using operators is a boolean.**

## Comparison Operators

Comparison operators compare 2 *values*. If the statement is true, then the output of the statement is `TRUE`. Otherwise, it is `FALSE`.

| **Operator** | **Meaning**              |
| ------------ | ------------------------ |
| ==           | equal                    |
| !=           | not equal                |
| >            | greater than             |
| <            | less than                |
| >=           | greater than or equal to |
| <=           | less than or equal to    |

```R
# Example 1
4.0 < 16	# TRUE

# Example 2
2 != 2	# FALSE

# Example 3
"fujikaze" == "fujikaze"	# TRUE

# Example 4
a <- 2
b <- a
a == b	# TRUE
b == a 	# TRUE

# Example 5
a <- 2
b <- a
a <- 5
a == b	# FALSE
a != b	# TRUE

```

