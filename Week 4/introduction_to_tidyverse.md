# Introduction to R and Tidyverse

Data visualization and manipulation are essential tools for
understanding and communicating complex information in data analysis. R,
a powerful programming language for data analysis, offers a variety of
packages for creating visually appealing plots and manipulating data.
One of the most popular and user-friendly collections of packages for
data visualization and manipulation in R is Tidyverse created by Hadley
Wickham, the Chief Scientist at RStudio. The Tidyverse is a collection
of packages that covers all common tasks, it can be installed using
`install.packages("tidyverse")` and activated with
l`ibrary("tidyverse")`. In this introduction, we will explore the basics
of using Tidyverse, we will use `readr` to read data, `tidyr` to tidy,
`dplyr` to manipulate, and `ggplot2` to visualize. To learn more about
the Tidyverse check out their website <https://www.tidyverse.org/>.

## Basics

Let us start with some basic concepts! We can use R as a basic
calculator

    # This is a comment use "#" to comment something!
    2+2

    ## [1] 4

    2*4 

    ## [1] 8

    2^8

    ## [1] 256

    (1+3)/(3+5)

    ## [1] 0.5

    log(10) # This takes a natural log of 10! 

    ## [1] 2.302585

We can define variables and perform operations on them. R uses `=` or
`<-` to assign values to a variable name. It is stylistically preffered
to use `<-` to avoid confusion and some errors.

    x <- 2 # same as x = 2
    x * 4

    ## [1] 8

`x <- 2` stored `2` in `x`. Later when we wrote `x * 4` R substituted
`x` for `2` evaluating `2 * 4` to get `8`. We can update value of `x` as
much as we want using `=` or `<-`. Keep in mind R is case sensitive so
`X` and `x` are different.

    x

    ## [1] 2

    x <- x * 5

### Data Types

R has a number of different data types and classes such as data.frames,
which are similar to excel spreadsheets with columns and rows. We will
first look at vectors. Vectors can hold multiple values of the same
types. Most basic ones are numeric, character and logical.

    x

    ## [1] 10

    class(x)

    ## [1] "numeric"

    (name <- "Parsa Rahimi") # wrapping with (...) will print the variable

    ## [1] "Parsa Rahimi"

    class(name)

    ## [1] "character"

    (true_or_false <- TRUE)

    ## [1] TRUE

    class(true_or_false)

    ## [1] "logical"

Note that `name` is stored as a single character string. What if we want
store name and surname separately in the same object? We can use
concatenate `c()` to combine objects of similar class into a vector!

    (name_surname <- c("Parsa","Rahimi"))

    ## [1] "Parsa"  "Rahimi"

    length(name) 

    ## [1] 1

    length(name_surname)

    ## [1] 2

Notice how length of the `name` is 1 and length of the `name_surname` is
2! Let’s make a numeric vector and do some operations on it!

    (i <- c(1, 2, 3, 4))

    ## [1] 1 2 3 4

    i + 10 # add 10 to each elements

    ## [1] 11 12 13 14

    i * 10 # multiply each element by 10

    ## [1] 10 20 30 40

    i + c(2, 4, 6, 8) # add elements together in matching positions

    ## [1]  3  6  9 12

we haven’t modified `i` with any of those operations. The results are
just printed and not stored. If we want to preserve the results we have
to store them in a variable.

    name

    ## [1] "Parsa Rahimi"

    name <- i + c(5,4,2,1)
    name

    ## [1] 6 6 5 5

Notice that `name` is no longer “Parsa Rahimi”. It has been overwritten
by assigning a numeric vector instead of a character string. But be
careful we can perform numeric operations only on numeric objects
otherwise we will receive an error. You can use `str()` to get structure
of the object such as type, length and other.

    name_surname + 2

    ## Error in name_surname + 2: non-numeric argument to binary operator

    str(name_surname)

    ##  chr [1:2] "Parsa" "Rahimi"

## Downloading Data

If you are familiar with Base R (functions that come with the R on
installation) you know about read.csv(). `readr` provides a number of
function that solve common issues of base R read function. `read_csv`
loads data 10 time faster and produces a tibble instead of a data frame
while avoiding inconsistencies of the `read.csv`. ‘Wait what is tibble?’
you might ask. Tibbles is special type of data frame. There are superior
to regular data frames as they load faster, maintain input types, permit
columns as lists, allow non-standard variable names, and never create
row names. Okay you have your data lets load it! First, you need to know
the path to your data. You can go find you file and check its location
and then copy paste it. If you are windows user your path might have
“\\”, which is an escape character. To fix that replace “\\” with “/”.
By copying the path you are getting absolute path
“/Users/User/Documents/your\_project/data/file.csv” alternatively you
can use local a local path from the folder of the project
“/data/file.csv”. Let’s read the data! `readr::` specifies which
packages to use. Replace the text between “…” to your path.

### Example Data

I will be using a sample of experiment’s results from Climate and
Cooperation Experiment from Mexico. During the experiments, subjects
were asked to complete three series of ravens matrices, four dictator
games, and a single lottery game. Sessions below 30 Celsius are labeled
as control, and sessions above 30 Celsius as treatment. We will be
primarily using results from Raven’s matrices games: 3 sets of 12
matrices. First set, `pr_`, is piece-rate round where participants
received points for each correctly solved matrix. Second set, `tr_`, is
tournament round where participants competed againts a random opponent
and the winner received double point and the loser received nothing.
Third set, `ch_`, is choice round. Participants were asked to decide
whether they want to play piece-rate or tournament againts a different
opponent’s score from tournament round.

You can find data in the `data` in GitHub repository. We will need
`tidyverse`.

    library(tidyverse)

    data <- readr::read_csv("https://raw.githubusercontent.com/nikitoshina/ECON-623-Lab-2023/main/data/mexico_sample_data.csv?token=GHSAT0AAAAAAB5WTPULI26TZP545VNUFQE6Y6O4XVA") #Download data from git hub

    ## Rows: 114 Columns: 70
    ## ── Column specification ───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────
    ## Delimiter: ","
    ## chr   (7): id, country_city, start_time, end_time, gender, version, f_last_meal_time
    ## dbl  (61): mean_temp_celsius, incentive_local, exchange_usd_local, incentive_usd, point_value, site_id, session_n, subject_n, tr_opponet_n, ch_opponent_n, treatment, d...
    ## lgl   (1): comment
    ## date  (1): date
    ## 
    ## ℹ Use `spec()` to retrieve the full column specification for this data.
    ## ℹ Specify the column types or set `show_col_types = FALSE` to quiet this message.

We can use `glimpse()` to get a glimpse at the data. It will give us a
sample and type of the column. Another very common way is to use
`head()` to get a slice of the top rows or `tail()` to get a slice of
bottom rows. You can also view the entire data set with `View()`

    data %>% glimpse()

    ## Rows: 114
    ## Columns: 70
    ## $ id                 <chr> "001018001", "001018002", "001018005", "001018009", "001018010", "001018013", "001018014", "001018015", "001019001", "001019002", "001019003",…
    ## $ country_city       <chr> "mexico_chapingo", "mexico_chapingo", "mexico_chapingo", "mexico_chapingo", "mexico_chapingo", "mexico_chapingo", "mexico_chapingo", "mexico_c…
    ## $ start_time         <chr> "12H 16M 0S", "12H 16M 0S", "12H 16M 0S", "12H 16M 0S", "12H 16M 0S", "12H 16M 0S", "12H 16M 0S", "12H 16M 0S", "14H 8M 0S", "14H 8M 0S", "14H…
    ## $ end_time           <chr> "13H 14M 0S", "13H 14M 0S", "13H 14M 0S", "13H 14M 0S", "13H 14M 0S", "13H 14M 0S", "13H 14M 0S", "13H 14M 0S", "15H 17M 0S", "15H 17M 0S", "1…
    ## $ date               <date> 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-20, 2022-06-2…
    ## $ mean_temp_celsius  <dbl> 28.58772, 28.58772, 28.58772, 28.58772, 28.58772, 28.58772, 28.58772, 28.58772, 30.69091, 30.69091, 30.69091, 30.69091, 30.69091, 30.69091, 30…
    ## $ incentive_local    <dbl> 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 100, 10…
    ## $ exchange_usd_local <dbl> 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20…
    ## $ incentive_usd      <dbl> 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5…
    ## $ gender             <chr> "Female", "Male", "Male", "Male", "Male", "Female", "Female", "Female", "Female", "Male", "Female", "Female", "Female", "Female", "Female", "M…
    ## $ point_value        <dbl> 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10, 10…
    ## $ site_id            <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ session_n          <dbl> 18, 18, 18, 18, 18, 18, 18, 18, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 20, 21…
    ## $ subject_n          <dbl> 1, 2, 5, 9, 10, 13, 14, 15, 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12, 13, 14, 15, 16, 1, 2, 3, 5, 6, 8, 9, 10, 13, 14, 15, 1, 5, 6, 9, 10, 13, 14…
    ## $ tr_opponet_n       <dbl> 2, 1, 9, 5, 13, 10, 15, 14, 2, 1, 4, 3, 5, 4, 8, 7, 10, 9, 12, 11, 14, 13, 16, 15, 2, 1, 5, 3, 8, 6, 10, 9, 14, 13, 1, 5, 1, 9, 6, 13, 10, 1, …
    ## $ ch_opponent_n      <dbl> 9, NA, NA, 1, 9, NA, NA, NA, NA, 3, 2, NA, NA, 8, NA, 6, 11, NA, 9, 13, 12, NA, 13, NA, NA, 3, 2, NA, NA, 10, 8, 8, NA, NA, NA, 13, 13, NA, NA…
    ## $ version            <chr> "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A", "A…
    ## $ treatment          <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 0, 0, 0, 0, 0, 0…
    ## $ dc_cl_ps           <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 2, 1, 1, 1, 1, 1, 2, 1, 1, 1, 1, 1…
    ## $ dc_cl_envy         <dbl> 2, 2, 2, 2, 1, 1, 2, 1, 2, 2, 2, 1, 1, 1, 1, 2, 2, 1, 2, 2, 1, 2, 2, 2, 1, 2, 2, 1, 2, 2, 2, 1, 2, 2, 1, 2, 1, 1, 2, 1, 1, 2, 1, 2, 1, 2, 1, 1…
    ## $ dc_c_ps            <dbl> 1, 1, 1, 1, 1, 2, 1, 1, 1, 2, 1, 2, 1, 2, 2, 2, 2, 2, 1, 2, 1, 1, 1, 1, 2, 2, 1, 2, 1, 1, 1, 1, 2, 1, 2, 2, 2, 1, 1, 1, 1, 1, 2, 2, 1, 1, 2, 2…
    ## $ dc_c_envy          <dbl> 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 1, 2, 2, 2, 2, 2, 1, 1, 1, 1, 2, 2, 2, 2, 2, 2, 2, 2, 2, 2, 1, 1, 2, 1, 2, 1, 2, 2, 2, 1, 2, 2, 2, 2, 2, 2, 2…
    ## $ dc_cl_ps_points    <dbl> 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 16, 12…
    ## $ dc_cl_envy_points  <dbl> 20, 20, 20, 20, 16, 16, 16, 20, 20, 20, 16, 20, 16, 16, 20, 16, 16, 20, 20, 20, 20, 16, 20, 20, 20, 16, 16, 20, 20, 20, 16, 20, 20, 20, 16, 16…
    ## $ dc_c_ps_points     <dbl> 16, 16, 16, 16, 12, 20, 16, 16, 12, 20, 12, 20, 16, 16, 16, 16, 16, 16, 12, 20, 16, 16, 16, 16, 16, 16, 12, 20, 16, 16, 16, 16, 20, 12, 16, 16…
    ## $ dc_c_envy_points   <dbl> 23, 23, 23, 23, 21, 18, 23, 23, 23, 23, 18, 21, 23, 18, 23, 23, 18, 21, 16, 16, 21, 18, 23, 23, 23, 23, 23, 23, 23, 23, 18, 21, 21, 18, 21, 18…
    ## $ pr_correct         <dbl> 7, 5, 6, 1, 7, 2, 6, 7, 5, 6, 8, 2, 2, 5, 6, 5, 2, 6, 7, 4, 4, 5, 5, 3, 7, 8, 7, 3, 5, 6, 7, 5, 8, 5, 5, 7, 5, 8, 7, 6, 2, 5, 5, 7, 5, 5, 5, 5…
    ## $ pr_wrong           <dbl> 0, 1, 0, 0, 0, 0, 0, 0, 0, 2, 0, 1, 1, 1, 0, 1, 0, 0, 0, 0, 0, 0, 0, 1, 0, 0, 5, 1, 1, 0, 0, 0, 1, 0, 2, 0, 1, 0, 1, 1, 1, 1, 1, 0, 1, 1, 3, 0…
    ## $ pr_not_attempted   <dbl> 5, 6, 6, 11, 5, 10, 6, 5, 7, 4, 4, 9, 9, 6, 6, 6, 10, 6, 5, 8, 8, 7, 7, 8, 5, 4, 0, 8, 6, 6, 5, 7, 3, 7, 5, 5, 6, 4, 4, 5, 9, 6, 6, 5, 6, 6, 4…
    ## $ tr_correct         <dbl> 3, 6, 7, 5, 9, 7, 6, 7, 4, 7, 6, 3, 6, 7, 8, 6, 6, 8, 7, 5, 4, 6, 6, 7, 6, 6, 6, 4, 8, 9, 7, 7, 7, 3, 6, 7, 7, 4, 7, 5, 3, 3, 6, 6, 4, 6, 4, 5…
    ## $ tr_wrong           <dbl> 1, 1, 1, 4, 0, 0, 2, 1, 2, 2, 2, 0, 3, 1, 1, 4, 1, 3, 1, 5, 0, 0, 3, 0, 2, 5, 2, 1, 1, 1, 3, 0, 1, 0, 0, 2, 1, 5, 2, 1, 1, 0, 1, 1, 0, 1, 8, 1…
    ## $ tr_not_attempted   <dbl> 8, 5, 4, 3, 3, 5, 4, 4, 6, 3, 4, 9, 3, 4, 3, 2, 5, 1, 4, 2, 8, 6, 3, 5, 4, 1, 4, 7, 3, 2, 2, 5, 4, 9, 6, 3, 4, 3, 3, 6, 8, 9, 5, 5, 8, 5, 0, 6…
    ## $ tr_die             <dbl> 2, 5, 2, 6, 6, 2, 2, 6, 2, 4, 5, 3, 6, 6, 3, 6, 1, 3, 1, 5, 6, 4, 6, 2, 3, 6, 4, 4, 5, 4, 3, 3, 2, 1, 5, 4, 5, 5, 5, 1, 3, 5, 3, 4, 2, 6, 6, 3…
    ## $ tr_total           <dbl> 5, 11, 9, 11, 15, 9, 8, 13, 6, 11, 11, 6, 12, 13, 11, 12, 7, 11, 8, 10, 10, 10, 12, 9, 9, 12, 10, 8, 13, 13, 10, 10, 9, 4, 11, 11, 12, 9, 12, …
    ## $ tr_guess_correct   <dbl> 5, 7, 8, 6, 11, 5, 8, 5, 5, 6, 8, 5, 5, 8, 8, 7, 3, 8, 9, 6, 5, 7, 5, 6, 7, 8, 10, 5, 8, 8, 6, 9, 12, 1, 6, 8, 4, 6, 12, 7, 7, 10, 5, 5, 5, 5,…
    ## $ tr_guess_die       <dbl> 3, 4, 1, 4, 2, 2, 5, 5, 4, 3, 4, 2, 4, 2, 3, 1, 2, 5, 5, 4, 4, 3, 4, 3, 4, 3, 2, 2, 6, 5, 2, 4, 4, 1, 4, 3, 5, 4, 6, 4, 6, 3, 4, 3, 4, 3, 3, 6…
    ## $ tr_guess_total     <dbl> 8, 11, 9, 10, 13, 7, 13, 10, 9, 9, 12, 7, 9, 10, 11, 8, 5, 13, 14, 10, 9, 10, 9, 9, 11, 11, 12, 7, 14, 13, 8, 13, 16, 4, 10, 11, 9, 10, 18, 11…
    ## $ tr_other_correct   <dbl> 6, 3, 5, 7, 7, 9, 7, 6, 7, 4, 3, 6, 6, 3, 6, 8, 8, 6, 5, 7, 6, 4, 7, 6, 6, 6, 4, 6, 9, 8, 7, 7, 3, 7, 6, 7, 7, 7, 4, 3, 5, 7, 6, 6, 6, 4, 5, 4…
    ## $ tr_other_die       <dbl> 5, 2, 6, 2, 2, 6, 6, 2, 4, 2, 3, 5, 6, 3, 6, 3, 3, 1, 5, 1, 4, 6, 2, 6, 6, 3, 4, 4, 4, 5, 3, 3, 1, 2, 3, 5, 4, 5, 5, 3, 1, 4, 4, 3, 6, 2, 3, 6…
    ## $ tr_other_total     <dbl> 11, 5, 11, 9, 9, 15, 13, 8, 11, 6, 6, 11, 12, 6, 12, 11, 11, 7, 10, 8, 10, 10, 9, 12, 12, 9, 8, 10, 13, 13, 10, 10, 4, 9, 9, 12, 11, 12, 9, 6,…
    ## $ tr_result          <dbl> 0, 2, 0, 2, 2, 0, 0, 2, 0, 2, 2, 0, 1, 2, 0, 2, 0, 2, 0, 2, 1, 1, 2, 0, 0, 2, 2, 0, 1, 1, 1, 1, 2, 0, 2, 0, 2, 0, 2, 1, 1, 0, 0, 2, 0, 2, 2, 0…
    ## $ tr_points          <dbl> 0, 22, 0, 22, 30, 0, 0, 26, 0, 22, 22, 0, 12, 26, 0, 24, 0, 22, 0, 20, 10, 10, 24, 0, 0, 24, 20, 0, 13, 13, 10, 10, 18, 0, 22, 0, 24, 0, 24, 6…
    ## $ f_happy            <dbl> 5, 9, 8, 4, 8, 8, 3, 7, 6, 10, 8, 9, 4, 5, 9, 8, 6, 6, 9, 6, 10, 5, 8, 8, 7, 9, 6, 5, 9, 9, 6, 10, 6, 10, 8, 7, 9, 8, 8, 8, 10, 9, 7, 6, 7, 8,…
    ## $ f_energetic        <dbl> 7, 8, 7, 3, 10, 9, 3, 5, 7, 10, 9, 8, 5, 6, 9, 6, 8, 8, 9, 7, 9, 10, 7, 10, 5, 8, 7, 3, 7, 9, 7, 7, 4, 10, 9, 8, 9, 7, 8, 8, 10, 8, 9, 7, 7, 1…
    ## $ f_frustrated       <dbl> 8, 3, 3, 0, 4, 8, 8, 2, 7, 0, 3, 0, 5, 0, 1, 2, 0, 2, 2, 5, 0, 5, 2, 0, 0, 1, 1, 8, 8, 0, 5, 0, 5, 6, 2, 4, 1, 6, 1, 2, 0, 0, 8, 2, 2, 5, 0, 7…
    ## $ f_last_meal_min    <dbl> 180, 240, 240, 90, 30, 120, 90, 120, 30, 120, 30, 30, 60, 120, 60, 300, 900, 60, 30, 120, 300, 720, 120, 240, 240, 300, 180, 300, 240, 360, 90…
    ## $ ch_correct         <dbl> 9, 4, 7, 7, 10, 5, 7, 6, 4, 4, 8, 6, 5, 6, 6, 6, 5, 8, 7, 6, 5, 7, 8, 8, 7, 5, 6, 7, 7, 7, 5, 7, 7, 7, 7, 8, 5, 7, 7, 8, 2, 3, 6, 5, 6, 6, 3, …
    ## $ ch_wrong           <dbl> 0, 0, 0, 5, 0, 2, 1, 2, 4, 2, 3, 0, 1, 2, 2, 2, 0, 3, 1, 1, 0, 0, 3, 0, 0, 7, 2, 2, 1, 3, 6, 1, 5, 0, 0, 0, 2, 2, 3, 1, 4, 9, 1, 3, 0, 0, 7, 0…
    ## $ ch_not_attempted   <dbl> 3, 8, 5, 0, 2, 5, 4, 4, 4, 6, 1, 6, 6, 4, 4, 4, 7, 1, 4, 5, 7, 5, 1, 4, 5, 0, 4, 3, 4, 2, 1, 4, 0, 5, 5, 4, 5, 3, 2, 3, 6, 0, 5, 4, 6, 6, 2, 5…
    ## $ ch_die             <dbl> 3, 3, 5, 6, 2, 4, 1, 3, 6, 1, 5, 4, 3, 2, 4, 2, 6, 3, 1, 1, 4, 5, 3, 6, 1, 5, 2, 4, 5, 3, 4, 2, 3, 5, 2, 1, 4, 5, 5, 2, 5, 6, 5, 6, 3, 1, 1, 6…
    ## $ ch_total           <dbl> 12, 7, 12, 13, 12, 9, 8, 9, 10, 5, 13, 10, 8, 8, 10, 8, 11, 11, 8, 7, 9, 12, 11, 14, 8, 10, 8, 11, 12, 10, 9, 9, 10, 12, 9, 9, 9, 12, 12, 10, …
    ## $ ch_tournament      <dbl> 1, 0, 0, 1, 1, 0, 0, 0, 0, 1, 1, 0, 0, 1, 0, 1, 1, 0, 1, 1, 1, 0, 1, 0, 0, 1, 1, 0, 0, 1, 1, 1, 0, 0, 0, 1, 1, 0, 0, 0, 1, 0, 1, 1, 0, 1, 1, 0…
    ## $ ch_other_correct   <dbl> 9, 4, 4, 7, 9, 4, 4, 4, 4, 4, 8, 4, 4, 6, 4, 6, 5, 4, 7, 6, 5, 4, 6, 4, 7, 5, 6, 7, 7, 7, 5, 5, 7, 7, 7, 8, 8, 7, 7, 7, 2, 7, 6, 5, 6, 6, 3, 6…
    ## $ ch_other_die       <dbl> 3, 3, 3, 6, 3, 3, 3, 3, 6, 1, 5, 6, 6, 2, 6, 2, 6, 6, 1, 1, 4, 6, 1, 6, 1, 5, 2, 1, 1, 3, 4, 4, 1, 1, 1, 1, 1, 5, 5, 5, 5, 5, 5, 6, 3, 1, 1, 3…
    ## $ ch_other_total     <dbl> 12, 7, 7, 13, 12, 7, 7, 7, 10, 5, 13, 10, 10, 8, 10, 8, 11, 10, 8, 7, 9, 10, 7, 10, 8, 10, 8, 8, 8, 10, 9, 9, 8, 8, 8, 9, 9, 12, 12, 12, 7, 12…
    ## $ ch_result          <dbl> 1, NA, NA, 1, 1, NA, NA, NA, NA, 1, 1, NA, NA, 1, NA, 1, 1, NA, 1, 1, 1, NA, 2, NA, NA, 1, 1, NA, NA, 1, 1, 1, NA, NA, NA, 1, 1, NA, NA, NA, 1…
    ## $ ch_points          <dbl> 12, 7, 12, 13, 12, 9, 8, 9, 10, 5, 13, 10, 8, 8, 10, 8, 11, 11, 8, 7, 9, 12, 22, 14, 8, 10, 8, 11, 12, 10, 9, 9, 10, 12, 9, 9, 9, 12, 12, 10, …
    ## $ ct_selected        <dbl> 2, 2, 3, 6, 6, 2, 1, 1, 1, 6, 2, 1, 1, 1, 6, 6, 6, 3, 2, 2, 1, 4, 6, 4, 4, 6, 5, 4, 6, 6, 6, 1, 6, 6, 1, 2, 1, 1, 1, 4, 1, 3, 1, 6, 2, 4, 1, 1…
    ## $ ct_tails           <dbl> 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ ct_points          <dbl> 9.5, 9.5, 8.0, 1.0, 1.0, 9.5, 11.0, 11.0, 11.0, 1.0, 9.5, 11.0, 11.0, 11.0, 1.0, 1.0, 1.0, 8.0, 9.5, 9.5, 11.0, 6.5, 1.0, 6.5, 6.5, 1.0, 5.0, …
    ## $ task_paid          <dbl> 4, 4, 4, 4, 4, 4, 4, 4, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 5, 2, 2, 2, 2, 2, 2, 2, 7, 7, 7, 7, 7, 7…
    ## $ complete           <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ total_points       <dbl> 23, 23, 23, 23, 21, 18, 23, 23, 0, 22, 22, 0, 12, 26, 0, 24, 0, 22, 0, 20, 10, 10, 24, 0, 7, 8, 7, 3, 5, 6, 7, 5, 8, 5, 5, 16, 20, 20, 16, 16,…
    ## $ total_local_paid   <dbl> 330, 330, 330, 330, 310, 280, 330, 330, 100, 320, 320, 100, 220, 360, 100, 340, 100, 320, 100, 300, 200, 200, 340, 100, 170, 180, 170, 130, 15…
    ## $ total_usd_paid     <dbl> 16.5, 16.5, 16.5, 16.5, 15.5, 14.0, 16.5, 16.5, 5.0, 16.0, 16.0, 5.0, 11.0, 18.0, 5.0, 17.0, 5.0, 16.0, 5.0, 15.0, 10.0, 10.0, 17.0, 5.0, 8.5,…
    ## $ final_version      <dbl> 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1…
    ## $ comment            <lgl> NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA, NA…
    ## $ f_last_meal_time   <chr> "3 0", "4 0", "4 0", "1 30", "0 30", "2 0", "1 30", "2 0", "0 30", "2 0", "0 30", "0 30", "1 0", "2 0", "1 0", "5 0", "15 0", "1 0", "0 30", "…
    ## $ start_time_h       <dbl> 12, 12, 12, 12, 12, 12, 12, 12, 14, 14, 14, 14, 14, 14, 14, 14, 14, 14, 14, 14, 14, 14, 14, 14, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 18, 10…
    ## $ end_time_h         <dbl> 13, 13, 13, 13, 13, 13, 13, 13, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 15, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 19, 11…

## Basic Data Management

dplyr uses a collection of verbs to manipulate data that are piped
(chained) into each other with a piping operator `%>%` from `magrittr`
package. The way you use functions in base R is you wrap new function
over the previous one such as `k(g(f(x)))` this will become impossible
to read very quickly as you stack up functions and their arguments. To
solve this we will use pipes `x %>% f() %>% g() %>% k()`! Now you can
clearly see that we take x and apply f() then g() then k(). Note: base R
now also has its own pipe `|>`, but we will stick to `%>%` for
compatibility across packages. \### `select()` `select()` selects only
the columns that you want, removing all other columns. You can use
column position (with numbers) or name. The columns will be displayed in
the order you list them. We will select subject\_id, temperature, gender
and results of raven’s matrices games.

-   `id` is a unique subject identification number, where
    site\_id.session\_n.subject\_n (001.001.001).
-   `mean_temp_celsius` is mean temperature through the session
-   `gender` is gender of the subject.
-   `pr_correct` is number of correct answers in *piece-rate* round.
-   `tr_correct` is number of correct answers in *tournament* round.
-   `ch_correct` is number of correct answers in *choice* round.
-   `ch_tournament` is 1 if participant decided to play tournament and 0
    if choice.

<!-- -->

    data_raven <- data %>% select(id, mean_temp_celsius,gender, pr_correct, tr_correct, ch_tournament, ch_correct) 
    head(data_raven)

    ## # A tibble: 6 × 7
    ##   id        mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct
    ##   <chr>                 <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>
    ## 1 001018001              28.6 Female          7          3             1          9
    ## 2 001018002              28.6 Male            5          6             0          4
    ## 3 001018005              28.6 Male            6          7             0          7
    ## 4 001018009              28.6 Male            1          5             1          7
    ## 5 001018010              28.6 Male            7          9             1         10
    ## 6 001018013              28.6 Female          2          7             0          5

You can also exclude columns or select everything else with select using
`-`

    data_raven %>% select(-gender) %>% head()

    ## # A tibble: 6 × 6
    ##   id        mean_temp_celsius pr_correct tr_correct ch_tournament ch_correct
    ##   <chr>                 <dbl>      <dbl>      <dbl>         <dbl>      <dbl>
    ## 1 001018001              28.6          7          3             1          9
    ## 2 001018002              28.6          5          6             0          4
    ## 3 001018005              28.6          6          7             0          7
    ## 4 001018009              28.6          1          5             1          7
    ## 5 001018010              28.6          7          9             1         10
    ## 6 001018013              28.6          2          7             0          5

### `filter()`

`filter()` keeps only rows that meet the specified criteria. Let’s
filter and make 2 data sets one for Males and one for Females.

    data_male <- data_raven %>% filter(gender == "Male") # we use == for comparison
    data_female <- data_raven %>% filter(gender == "Female")
    head(data_male)

    ## # A tibble: 6 × 7
    ##   id        mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct
    ##   <chr>                 <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>
    ## 1 001018002              28.6 Male            5          6             0          4
    ## 2 001018005              28.6 Male            6          7             0          7
    ## 3 001018009              28.6 Male            1          5             1          7
    ## 4 001018010              28.6 Male            7          9             1         10
    ## 5 001019002              30.7 Male            6          7             1          4
    ## 6 001019008              30.7 Male            5          6             1          6

    head(data_female)

    ## # A tibble: 6 × 7
    ##   id        mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct
    ##   <chr>                 <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>
    ## 1 001018001              28.6 Female          7          3             1          9
    ## 2 001018013              28.6 Female          2          7             0          5
    ## 3 001018014              28.6 Female          6          6             0          7
    ## 4 001018015              28.6 Female          7          7             0          6
    ## 5 001019001              30.7 Female          5          4             0          4
    ## 6 001019003              30.7 Female          8          6             1          8

We can chain multiple requirements. Here we will look at Males,
temperature over 30 celsius or Females, temperature below 30. Notice
that we use `&` as “and”, `|` as “or, and wrap the two conditions
into”()” to avoid confusion. It could read it as
`mean_temp_celsius > 30 | gender == "Female"`.

    data_raven %>% 
      filter( 
        (gender == "Male" & mean_temp_celsius > 30) | (gender == "Female" & mean_temp_celsius < 30)
            )

    ## # A tibble: 61 × 7
    ##    id        mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct
    ##    <chr>                 <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>
    ##  1 001018001              28.6 Female          7          3             1          9
    ##  2 001018013              28.6 Female          2          7             0          5
    ##  3 001018014              28.6 Female          6          6             0          7
    ##  4 001018015              28.6 Female          7          7             0          6
    ##  5 001019002              30.7 Male            6          7             1          4
    ##  6 001019008              30.7 Male            5          6             1          6
    ##  7 001019009              30.7 Male            2          6             1          5
    ##  8 001019010              30.7 Male            6          8             0          8
    ##  9 001019011              30.7 Male            7          7             1          7
    ## 10 001019012              30.7 Male            4          5             1          6
    ## # … with 51 more rows

### `arrange()`

`arrange()` allows you to order the table using a variable. Let’s see
which subject scored the worst in `pr_correct`.

    data_raven %>% arrange(pr_correct) %>% head()

    ## # A tibble: 6 × 7
    ##   id        mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct
    ##   <chr>                 <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>
    ## 1 001018009              28.6 Male            1          5             1          7
    ## 2 001018013              28.6 Female          2          7             0          5
    ## 3 001019004              30.7 Female          2          3             0          6
    ## 4 001019005              30.7 Female          2          6             0          5
    ## 5 001019009              30.7 Male            2          6             1          5
    ## 6 001021013              30.4 Male            2          3             1          2

We can also sort in descending order using `desc()` modifier. Let’s look
at who scored the most!

    data_raven %>% arrange(desc(pr_correct)) %>% head()

    ## # A tibble: 6 × 7
    ##   id        mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct
    ##   <chr>                 <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>
    ## 1 001019003              30.7 Female          8          6             1          8
    ## 2 001020002              31.6 Male            8          6             1          5
    ## 3 001020013              31.6 Male            8          7             0          7
    ## 4 001021006              30.4 Male            8          4             0          7
    ## 5 001025009              26.8 Male            8          9             1          9
    ## 6 001027015              32.2 Female          8          7             0          8

### `mutate()`

`mutate()` adds new columns and modifies current variables in the data
set. Let’s create a dataset with 10 rows and make three new variable
columns as an example

    tibble(rows = 1:10) %>% mutate(
      One = 1,
      Comment = "Something",
      Approved = TRUE
    )

    ## # A tibble: 10 × 4
    ##     rows   One Comment   Approved
    ##    <int> <dbl> <chr>     <lgl>   
    ##  1     1     1 Something TRUE    
    ##  2     2     1 Something TRUE    
    ##  3     3     1 Something TRUE    
    ##  4     4     1 Something TRUE    
    ##  5     5     1 Something TRUE    
    ##  6     6     1 Something TRUE    
    ##  7     7     1 Something TRUE    
    ##  8     8     1 Something TRUE    
    ##  9     9     1 Something TRUE    
    ## 10    10     1 Something TRUE

`mutate()` can use existing variables from the data set to create new
ones! Lets convert Celsius to Fahrenheit, see how many point more people
scored in tournament over piece-rate round, and check how far from the
mean they scored in piece-rate round!

    data_raven %>% mutate(mean_temp_fahrenheit = (mean_temp_celsius * 9/5) + 32,
                          impovement = tr_correct - pr_correct,
                          pr_deviation = pr_correct - mean(pr_correct))

    ## # A tibble: 114 × 10
    ##    id        mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct mean_temp_fahrenheit impovement pr_deviation
    ##    <chr>                 <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>                <dbl>      <dbl>        <dbl>
    ##  1 001018001              28.6 Female          7          3             1          9                 83.5         -4        1.66 
    ##  2 001018002              28.6 Male            5          6             0          4                 83.5          1       -0.342
    ##  3 001018005              28.6 Male            6          7             0          7                 83.5          1        0.658
    ##  4 001018009              28.6 Male            1          5             1          7                 83.5          4       -4.34 
    ##  5 001018010              28.6 Male            7          9             1         10                 83.5          2        1.66 
    ##  6 001018013              28.6 Female          2          7             0          5                 83.5          5       -3.34 
    ##  7 001018014              28.6 Female          6          6             0          7                 83.5          0        0.658
    ##  8 001018015              28.6 Female          7          7             0          6                 83.5          0        1.66 
    ##  9 001019001              30.7 Female          5          4             0          4                 87.2         -1       -0.342
    ## 10 001019002              30.7 Male            6          7             1          4                 87.2          1        0.658
    ## # … with 104 more rows

Notice that we can nest functions within `mutate()`: first we took
`mean()` of the entire column and then subtracted it from `pr_correct`.

### `recode()`

`recode()` modifies the values within a variable. Here is a template:

> data %&gt;% mutate(Variable = recode(Variable, “old value” = “new
> value”))

Let’s use `recode()` to change “Male” to “M” and “Female” to “F”.

    data_raven <- data_raven %>% mutate(gender = recode(gender, "Male" = "M", "Female" = "F"))

## `summarize()`

`summarize()` collapses all rows and returns a one-row summary. We will
use summary to calculation what percentage of participant were male,
median score in piece-rate round, max score in tournament, percentage of
people choosing tournament in choice and mean score in choice round.

    data_raven %>% 
      summarize(perc_male = sum(gender == "Male", na.rm = T) / n(),
                pr_median = median(pr_correct),
                tr_max = max(tr_correct),
                ch_ratio = sum(ch_tournament) / n(),
                ch_mean = mean(ch_correct))

    ## # A tibble: 1 × 5
    ##   perc_male pr_median tr_max ch_ratio ch_mean
    ##       <dbl>     <dbl>  <dbl>    <dbl>   <dbl>
    ## 1         0         5      9    0.456    6.01

## `group_by()` and `ungroup()`

### `group_by()`

`group_by()` groups data by specific variables for future operations. We
can use `group_by()` and `summarize()` to calculate different summary
statistics for genders!

    data_raven %>% 
      drop_na(gender) %>%  # removes NA gender
      group_by(gender) %>% 
      summarize(pr_mean = mean(pr_correct),
                tr_mean = mean(tr_correct),
                ch_mean = mean(ch_correct),
                pr_sd = sd(pr_correct),
                n = n()) %>%
      ungroup()

    ## # A tibble: 2 × 6
    ##   gender pr_mean tr_mean ch_mean pr_sd     n
    ##   <chr>    <dbl>   <dbl>   <dbl> <dbl> <int>
    ## 1 F         5.22    6.17    5.93  1.58    58
    ## 2 M         5.47    6.4     6.09  1.59    55

Let’s group by gender and choice in choice round and look at points in
choice round!

    data_raven %>%
      drop_na(gender) %>%  # removes NA gender
      group_by(gender, ch_tournament) %>% 
      summarize(ch_mean = mean(ch_correct),
                pr_sd = sd(ch_correct),
                n = n()) %>%
      ungroup()

    ## `summarise()` has grouped output by 'gender'. You can override using the `.groups` argument.

    ## # A tibble: 4 × 5
    ##   gender ch_tournament ch_mean pr_sd     n
    ##   <chr>          <dbl>   <dbl> <dbl> <int>
    ## 1 F                  0    5.73  1.70    33
    ## 2 F                  1    6.2   1.73    25
    ## 3 M                  0    6.07  1.69    29
    ## 4 M                  1    6.12  2.25    26

### `ungroup()`

`ungroup()` does exactly what you think – removes the grouping! Always
ungroup your data after you are done with operation that required
grouping, else it will get messy. Look at this example

    data_raven %>%
      drop_na(gender) %>%  # removes NA gender
      group_by(gender) %>% 
      mutate(n = n()) %>%
      mutate(mean_male = mean(gender == "Male")) %>%
      ungroup() %>%
      select(id, gender, n, mean_male) %>% head(n = 5)

    ## # A tibble: 5 × 4
    ##   id        gender     n mean_male
    ##   <chr>     <chr>  <int>     <dbl>
    ## 1 001018001 F         58         0
    ## 2 001018002 M         55         0
    ## 3 001018005 M         55         0
    ## 4 001018009 M         55         0
    ## 5 001018010 M         55         0

Notice how mean\_male (ratio of male to total) is 0 for Female and 1 for
Male. It is because the data was grouped and we performed operation on
Males and Females separately.

    data_raven %>%
      drop_na(gender) %>%  # removes NA gender
      group_by(gender) %>% 
      mutate(n = n()) %>%
      ungroup() %>%
      mutate(mean_male = mean(gender == "Male")) %>%
      select(id, gender, n, mean_male) %>% head(n = 5)

    ## # A tibble: 5 × 4
    ##   id        gender     n mean_male
    ##   <chr>     <chr>  <int>     <dbl>
    ## 1 001018001 F         58         0
    ## 2 001018002 M         55         0
    ## 3 001018005 M         55         0
    ## 4 001018009 M         55         0
    ## 5 001018010 M         55         0

This time on the other hand we ungrouped the data, correctly calculating
the ratio!

### `rowwise()`

`rowwise()` produces a row-wise grouping. Later you might want to run a
calculation row-wise instead of column-wise, but your column will be
filled with an aggregate result. This is where `rowwise()` comes in to
save the day! To demonstrate, we will make a dataframe with a column of
lists and try to find the length of each list.

    df <- tibble(
      x = list(1, 2:3, 4:6,7:11)
    )

    df %>% mutate(length = length(x))

    ## # A tibble: 4 × 2
    ##   x         length
    ##   <list>     <int>
    ## 1 <dbl [1]>      4
    ## 2 <int [2]>      4
    ## 3 <int [3]>      4
    ## 4 <int [5]>      4

Hmmm… Instead of lists’ lengths we got the total number of rows in the
data set (length of column `x`). Now let’s use `rowwise()`

    df %>% rowwise() %>%
      mutate(length = length(x))

    ## # A tibble: 4 × 2
    ## # Rowwise: 
    ##   x         length
    ##   <list>     <int>
    ## 1 <dbl [1]>      1
    ## 2 <int [2]>      2
    ## 3 <int [3]>      3
    ## 4 <int [5]>      5

Yey! Here R runs `length()` on each list separately, giving us correct
lengths!

## `count()`

`count()` is similar to `group_by()` and `summarize()` combo – it
collapses the rows and counts the number of observations per group of
values.

    data_raven %>% count(gender)

    ## # A tibble: 3 × 2
    ##   gender     n
    ##   <chr>  <int>
    ## 1 F         58
    ## 2 M         55
    ## 3 <NA>       1

Similar to `group_by()` you can select multiple columns to group.

    data_raven %>% count(gender, ch_tournament)

    ## # A tibble: 5 × 3
    ##   gender ch_tournament     n
    ##   <chr>          <dbl> <int>
    ## 1 F                  0    33
    ## 2 F                  1    25
    ## 3 M                  0    29
    ## 4 M                  1    26
    ## 5 <NA>               1     1

## `rename()`

`rename()` renames a column. Notice that the “New Name” is on the left
and “Old Name” is on the right. Let’s rename `id` to `subject_id` and
`gender` to `sex`.

    data_raven %>% rename("subject_id" = "id", "sex" = "gender") %>% head(n = 5)

    ## # A tibble: 5 × 7
    ##   subject_id mean_temp_celsius sex   pr_correct tr_correct ch_tournament ch_correct
    ##   <chr>                  <dbl> <chr>      <dbl>      <dbl>         <dbl>      <dbl>
    ## 1 001018001               28.6 F              7          3             1          9
    ## 2 001018002               28.6 M              5          6             0          4
    ## 3 001018005               28.6 M              6          7             0          7
    ## 4 001018009               28.6 M              1          5             1          7
    ## 5 001018010               28.6 M              7          9             1         10

## `row_number()`

`row_number()` fills a column with consecutive numbers. It is especially
useful if you need to create an id column. Let’s remove `id` column and
make a new one with `row_number()`.

    data_raven %>% 
      select(-id) %>%
      mutate(id = row_number()) %>% 
      relocate(id) %>% # used to move id at the beginning
      head(n = 5)

    ## # A tibble: 5 × 7
    ##      id mean_temp_celsius gender pr_correct tr_correct ch_tournament ch_correct
    ##   <int>             <dbl> <chr>       <dbl>      <dbl>         <dbl>      <dbl>
    ## 1     1              28.6 F               7          3             1          9
    ## 2     2              28.6 M               5          6             0          4
    ## 3     3              28.6 M               6          7             0          7
    ## 4     4              28.6 M               1          5             1          7
    ## 5     5              28.6 M               7          9             1         10

# `tidyr` – Wide and Long Data

Wide data and long data are two common forms of data organization.

Wide data, also known as unstacked data, is organized so that each row
represents an individual unit of observation and each column represents
a variable. This format is often used when the number of variables is
relatively small and they are not related to one another in a
hierarchical manner.

For example, a wide data table containing information about a group of
students might have one row for each student and columns for their name,
age, gender, and test scores.

On the other hand, long data, also known as stacked data, is organized
so that each row represents a single observation of a variable, and each
column represents the variable and an identifier of the unit of
observation. This format is often used when the number of variables is
large or they are related to one another in a hierarchical manner.

For example, a long data table containing information about the test
scores of a group of students might have one row for each student-test
combination, with columns for the student’s name, the test name and the
score.

Choosing between wide and long format depends on the specific analysis
and visualization needs. Wide format is more suited for simple
exploratory analysis, while long format is more suited for complex
analysis and visualization. We will take advantage of long and wide data
in visualization section.

## `pivot_longer()`

A common problem is a dataset where column names are not names of
variables, but *value* of a variable. This is true for `pr_correct`,
`tr_correct`, `ch_correct` as the column names represent name of the
`game` variable, the values in the columns represent number of correct
answers, and each row represents two observations, not one.

To tidy a dataset, we need to pivot the offending columns into a new
pair of variables. To carry out the operation we need to supply:

1.  The columns whose names are values, not variables – columns we want
    to pivot. Here `pr_correct`, `tr_correct`, `ch_correct`.
2.  The name of the variable to move the column names to. Here `game`.
    The default `name`.
3.  The name of the variable to move the column values to. Here
    `n_correct`. The default `value`.

<!-- -->

    data_raven %>% 
      pivot_longer(c(pr_correct, tr_correct, ch_correct), names_to = "game", values_to = "n_correct") %>%
      select(id,game,n_correct) %>% 
      head(n = 5)

    ## # A tibble: 5 × 3
    ##   id        game       n_correct
    ##   <chr>     <chr>          <dbl>
    ## 1 001018001 pr_correct         7
    ## 2 001018001 tr_correct         3
    ## 3 001018001 ch_correct         9
    ## 4 001018002 pr_correct         5
    ## 5 001018002 tr_correct         6

## `pivot_wider()`

`pivot_wider()` is the opposite of `pivot_longer()`. You use it when an
observation is scattered across multiple rows. For example, let’s have a
look at `data_raven_accident`, where gnomes stacked `mean_temp_celsius`
and `ch_tournament`. Here an observation is spread across two rows.

    data_raven_accident %>% head(n=5)

    ## # A tibble: 5 × 3
    ##   id        name              value
    ##   <chr>     <chr>             <dbl>
    ## 1 001018001 mean_temp_celsius  28.6
    ## 2 001018001 ch_tournament       1  
    ## 3 001018002 mean_temp_celsius  28.6
    ## 4 001018002 ch_tournament       0  
    ## 5 001018005 mean_temp_celsius  28.6

To tidy this up, we need two parameters:

1.  The column to take variable names from. Here, it’s `name`.
2.  The column to take values from. Here it’s `value`.

<!-- -->

    data_raven_accident %>% pivot_wider(names_from = name, values_from = value) %>% head(n = 5)

    ## # A tibble: 5 × 3
    ##   id        mean_temp_celsius ch_tournament
    ##   <chr>                 <dbl>         <dbl>
    ## 1 001018001              28.6             1
    ## 2 001018002              28.6             0
    ## 3 001018005              28.6             0
    ## 4 001018009              28.6             1
    ## 5 001018010              28.6             1

It is evident from their names that pivot\_wider() and pivot\_longer()
are inverse functions. pivot\_longer() converts wide tables to a longer
and narrower format; pivot\_wider() converts long tables to a shorter
and wider format.

## `tibble()` and `tribble()`

A tibble is a special kind of data frame in R. Tibbles are a modern
re-imagining of the data frame, designed to be more friendly and
consistent than traditional data frames.

-   Tibbles are similar to data frames in that they can hold tabular
    data, but they have some key differences:

-   Tibbles display only the first 10 rows by default when printed,
    making them easier to work with large datasets.

-   Tibbles use a consistent printing format, making it easier to work
    with multiple tibbles in the same session.

-   Tibbles have a consistent subsetting behavior, making it easier to
    select columns by name. When printed, the data type of each column
    is specified.

-   Subsetting a tibble will always return a tibble. You don’t need to
    use drop = FALSE compared to traditional data.frames.

-   And most importantly, you can have column consisting of lists.

In summary, Tibbles are a more modern and consistent version of data
frames, they are less prone to errors and more readable, making them a
great choice for data manipulation and exploration tasks.

To make a tibble we can use `tibble()` similar to data.frame()

    tibble(x = c(1,2,3),
           y = c('one', 'two', 'three'))

    ## # A tibble: 3 × 2
    ##       x y    
    ##   <dbl> <chr>
    ## 1     1 one  
    ## 2     2 two  
    ## 3     3 three

You can also you `tribble()` for creating a row-wise, readable tibble in
R. This is useful for creating small tables of data. **Syntax: tribble
(~column1, ~column2)** where, Row column — represents the data in row by
row layout.

    tribble(~x, ~y,
            1, "one",
            2, "two",
            3, "three")

    ## # A tibble: 3 × 2
    ##       x y    
    ##   <dbl> <chr>
    ## 1     1 one  
    ## 2     2 two  
    ## 3     3 three

## `janitor` Clean Your Data

`janitor` is designed to make the process of cleaning and tidying data
as simple and efficient as possible. To learn more about the function
check out [this
vignette](https://cran.r-project.org/web/packages/janitor/vignettes/janitor.html)!
If you are interested in making summary tables with `janitior` check
[this
vignette](https://cran.r-project.org/web/packages/janitor/vignettes/tabyls.html)!

### `clean_names()`

`clean_names()` is used to clean variable names, particularly those that
are read in from Excel files using `readxl::read_excel()` and
`readr::read_csv()`. It parses letter cases, separators, and special
characters to a consistent format, converts certain characters like “%”
to “percent” and “\#” to “number” to retain meaning, resolves duplicate
names and empty names. It is recommended to call this function every
time data is read.

    # Create a data.frame with dirty names
    test_df <- as.data.frame(matrix(ncol = 6))
    names(test_df) <- c("camelCase", "ábc@!*", "% of respondents (2009)",
                        "Duplicate", "Duplicate", "")
    test_df

    ##   camelCase ábc@!* % of respondents (2009) Duplicate Duplicate   
    ## 1        NA     NA                      NA        NA        NA NA

    library(janitor)

    ## 
    ## Attaching package: 'janitor'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     chisq.test, fisher.test

    test_df %>% clean_names()

    ##   camel_case abc percent_of_respondents_2009 duplicate duplicate_2  x
    ## 1         NA  NA                          NA        NA          NA NA

### `remove_empty()`

`remove_empty()` removes empty row and columns, especially useful after
reading Excel files.

    test_df2 <- data.frame(numbers = c(1, NA, 3),
                           food = c(NA, NA, NA),
                           letters = c("a", NA, "c"))
    test_df2

    ##   numbers food letters
    ## 1       1   NA       a
    ## 2      NA   NA    <NA>
    ## 3       3   NA       c

    test_df2 %>%
      remove_empty(c("rows", "cols"))

    ##   numbers letters
    ## 1       1       a
    ## 3       3       c

### `remove_constant()`

`remove_constant()` drops columns from a data.frame that contain only a
single constant value (with an na.rm option to control whether NAs
should be considered as different values from the constant).

    test_df3 <- data.frame(cool_numbers = 1:3, boring = "the same")
    test_df3

    ##   cool_numbers   boring
    ## 1            1 the same
    ## 2            2 the same
    ## 3            3 the same

    test_df3 %>% remove_constant()

    ##   cool_numbers
    ## 1            1
    ## 2            2
    ## 3            3

\###`convert_to_date()` and `convert_to_datetime()` Remember loading
data from Excel and seeing `36922.75` instead of dates? Well,
`convert_to_date()` and `convert_to_datetime()` will convert this format
and other date-time formats to actual dates! If you need more
customization check `excel_numeric_to_date()`.

    convert_to_date(36922.75)

    ## [1] "2001-01-31"

    convert_to_datetime(36922.75)

    ## [1] "2001-01-31 18:00:00 UTC"

\###`row_to_names()` `row_to_names()` is a function that takes the names
of variables stored in a row of a data frame and makes them the column
names of the data frame. It can also remove the row that contained the
names, and any rows above it, if desired.

    test_df4 <- data.frame(X_1 = c(NA, "Names", 1:3),
                       X_2 = c(NA, "Value", 4:6))
    test_df4

    ##     X_1   X_2
    ## 1  <NA>  <NA>
    ## 2 Names Value
    ## 3     1     4
    ## 4     2     5
    ## 5     3     6

    row_to_names(test_df4, 2)

    ##   Names Value
    ## 3     1     4
    ## 4     2     5
    ## 5     3     6
