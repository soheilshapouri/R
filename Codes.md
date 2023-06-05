# Data Structures
most common structures: vectors, data frames, matrices, and arrays

vectors: same elements
lists: different types of elements


## Vectors
vectors: same elements

two kind -> atomic vectors and lists

**Atomic vectors**: logical, integer, double, character (which contains strings), complex, and raw. 

### create vectors
```
c(2.3, 45, 89.7)   #creates double vector
c(13L, 14L, 15L)   #creates integer vector
```

### properties of vectors 
type, length  
name of the elements
  
```
typeof() # type of the vector
is.integer()
is.character()
is.double()

length() # length of the vector

#name elements of a vector
x <- c(1,2,3)
names(x) <- c('a','b','c')
x 

#naming is useful if you want to call a specific element later
x['a']
```  
## Lists
can have different types of data like integers, lists, etc. 
```
list("a", 2, TRUE)
list(2, "b", list("a", 4))

#choose from list
x <- list("a", 2, TRUE)
x[3]  # will retrun TRUE 

#structure of the lists 
str(x)

#name elements of a list 
cities <- list("Chicago" = 1, "Newyork" = 2, "Los Angeles" = 3)
cities[2]
cities["Newyork"]






