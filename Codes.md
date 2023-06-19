# Sources to get data
- Journal of Statistics Education Data Archive https://jse.amstat.org/jse_data_archive.htm  
each dataset is accompanied by a peer-review paper
- R datasets pakcage  
   explanations and example codes: https://stat.ethz.ch/R-manual/R-devel/library/datasets/html/00Index.html
- Data in Brief   
hotel bookings:https://www.sciencedirect.com/science/article/pii/S2352340918315191
```
data() # R built-in datasets
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
 
 # combine columns
 bookings_df %>%
  select(arrival_date_year, arrival_date_month) %>% 
  unite(arrival_month_year, c(arrival_date_month, arrival_date_year), sep = " ")

# cobmine columns and change the format to data
cleaned <- bookings_df %>% 
  select(arrival_date_year, arrival_date_month, arrival_date_day_of_month) %>% 
  unite(new_date, c(arrival_date_year, arrival_date_month,arrival_date_day_of_month), sep = " ") %>% 
  mutate(new_date = ymd(new_date))

# make a new column
bookings_df %>%
  mutate(guests = adults + children + babies)

penguins %>% 
  mutate(body_mass_kg = body_mass_g/1000,
         flipper_length_m = flipper_length_mm/1000)
 
  
# separate a column into two columns
separate(employee, name, into = c("first_name", "last_name"), sep = " ")

# join columns
unite(employee, "name", first_name, last_name, sep = " ")

```
# Bias data
```
# this example shows that four different sets of data can have similar mean, sd, and correlation but very different shapes
library(Tmisc)
View(quartet)

quartet %>% 
  group_by(set) %>% 
  summarise(mean(x), sd(x), mean(y), sd(y), cor(x,y))

ggplot(quartet, aes(x,y))+
  geom_point()+
  geom_smooth(method = lm)+
  facet_wrap(~set)

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
# Journals
Quantitative Methods for Psychology https://www.tqmp.org/ 

# Theoritical Issues
Data Science Ethics: https://datasciencebox.org/02-ethics.html


    
# Data Visualization
choose the appropriate type of graph: https://www.data-to-viz.com/
```
ggplot(data = penguins)+
  geom_point(mapping = aes(x = flipper_length_mm, y = body_mass_g))
  
# add more aesthetics 
ggplot(penguins)+
  geom_point(mapping = aes(x = flipper_length_mm,y = body_mass_g,
                           color = species, shape = species,
                           size = species))
# if there are a lot of data points which overlap, use geom_jitter instead of geom_point()
  
# if you don't want to map variables to aesthetics, put them outside aes()
```
