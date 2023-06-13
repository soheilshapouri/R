# Sources to get data
- Journal of Statistics Education Data Archive https://jse.amstat.org/jse_data_archive.htm  
each dataset is accompanied by a peer-review paper
- R datasets pakcage   
```
data() # explanations and example codes: https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/00Index.html
```

# Data Import
```
# read csv files 
library(readr) 
readr_example() #sample datasets from readr package 
read_csv(readr_example("chickens.csv"))

# read excel files
library(readxl)
readxl_example() #sample xls and xlsx files

read_excel(readxl_example("datasets.xls"))
read_excel(readxl_example("type-me.xlsx"))

# to get the list of sheets in excel files 
excel_sheets(readxl_example("type-me.xlsx"))

# to read a particular sheet by number 
read_excel(readxl_example("type-me.xlsx"), sheet = 1)

# to read a particular sheet by its name 
read_excel(readxl_example("type-me.xlsx"), sheet = "date_coercion")
```
# Data Inspection
```
View()
glimpse()
skim_without_charts(penguins)
```
# Data Cleaning
```
colnames(penguins)

# select columns
mtcars %>% 
  select(-mpg)

penguins %>% 
  filter(species == "Adelie")
 
subset(penguins, select = c("species"))

# rename columns
df %>% 
  rename(new_name = old_name)
  
rename_with(penguins,toupper) # make all columns uppercase
rename_with(penguins,tolower) # make all columns lowercase

# arrange 
penguins %>% 
  arrange(bill_length_mm)

penguins %>% 
  arrange(desc(bill_length_mm))

penguins %>% 
  arrange(-bill_length_mm)
  
# grouping 
penguins %>% 
  group_by(island) %>% 
  drop_na() %>% 
  summarise(mean = mean(bill_length_mm))

penguins %>% 
  group_by(species, island) %>% 
  drop_na() %>% 
  summarise(min(bill_length_mm),
            max(bill_length_mm))
            

```


# Files and Folders
```
# creating new folder
dir.create("averynewfolder") 

# create new files 
file.create("soso.txt")

file.create("soso.docx")

file.create("sos.csv")

#delete files 
unlink("soso.docx")


```

# Data Structures
most common structures: vectors, lists, data frames, matrices, and arrays

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

#name elements of a vector, method 1
x <- c(1,2,3)
names(x) <- c('a','b','c')
x 

#name elements of a vector, method 2
y <- c("a" = 1, "b" = 2, "c"=3)


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
```
## DataFrames
```
data.frame(x=c(1,2,3), y = c("a", "b", "a"))
```
## Matrices
```
matrix(nrow = 2, ncol = 2)
matrix(c(3:8), nrow = 2)
matrix(c(3:8), ncol = 2)

```


# Time and Date 
time and date data in R has three different formats:  
date, time, and date-time  
date: 2016-08-16  
time: 20:11:59 UTC  
daye-time: 2018-03-31 18:15:48 UTC  

```
library(lubridate)

# to get the time
today() 
date()
timestamp()
now()

# convert strings to dates and time
x <- "2021-01-20" 
typeof(x)         #x is a string
x <- ymd(x)
typeof(x)         #retruns double 

x <- "2021-20-01"
ydm(x)

x <- 19850923
ymd(x) # will return date in yy, mm, dd format 

x <- "2021-01-20 20:11:59"
ymd_hms(x)

x <-"2023, 04, 13, 12:45"
ymd_hm(x)

now() #returns date_time
as.Date(now()) #change it to only date with base 
as_date(now()) #change it to only date with lubridate 
```

# Logical Operators
& and   
| or   
! NOT  
```  
TRUE & TRUE     #returns TRUE   
TRUE & FALSE    #returns FALSE  
FALSE & FALSE   #returns FALSE  
  
TRUE | TRUE  #returns TRUE  
TRUE | FALSE #returns TRUE  
FALSE| FALSE #retruns FALSE  

! not   
# zero means FALSE, non-zero menas TRUE  
x= 1 # x is TRUE cause it is non-zero  
!x   # NOT TRUE so retruns false   
  
airquality[airquality$Solar.R >150 & airquality$Wind > 10,]  
# the opposite should have | instead of &   
airquality[!(airquality$Solar.R >150 | airquality$Wind > 10),]  
```
# Packages
```
# update packages
tidyverse_update()
install.packages()

# tolearn about a package
browseVignettes("ggplot2")
```

# Nested functions vs. Pipes
```
filtered_tg <- filter(ToothGrowth, dose == 0.5)
arrange(filtered_tg, len)

# nested functions
arrange(filter(ToothGrowth, dose ==0.5),len)

# pipes
ToothGrowth %>% 
  filter(dose== 0.5) %>% 
  arrange(len)
```
# Tidyverse
```
ToothGrowth %>% 
  filter(dose == 0.5) %>% 
  group_by(supp) %>% 
  summarise(mean_len = mean(len, na.rm = T))
```
