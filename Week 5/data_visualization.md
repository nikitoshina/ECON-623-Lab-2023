# Data Visualization

Data visualization is an essential tool for understanding and
communicating complex information. R, a powerful programming language
for data analysis, offers a variety of packages for creating visually
appealing and informative plots. One of the most popular and versatile
packages for data visualization in R is `ggplot2`. In this introduction,
we will explore the basics of using `ggplot2` to create different types
of plots and customize them to suit your needs. We can load it
separately `libary(ggplot2)` or with `libary(tidyverse)`.

    library(tidyverse)

We will continue using the example from the previous vignette. If you
used R before then you are familiar with the default graphing function
`plot`,`hist`, etc. `ggplot2` has it own version of quickly making a
graph `qplot()`. To learn about `qplot()` check out [this
vignette](http://www.sthda.com/english/wiki/qplot-quick-plot-with-ggplot2-r-software-and-data-visualization).

    data_raven %>% pull(pr_correct) %>% hist() 

![](../Week%205/data_visualization_files/figure-markdown_strict/unnamed-chunk-2-1.png)

    data_raven %>% qplot(pr_correct, data = ., geom = 'histogram', bins = length(unique(data_raven$pr_correct)))

![](../Week%205/data_visualization_files/figure-markdown_strict/unnamed-chunk-2-2.png)

## `ggplot()`

The ggplot() function sets up the basic structure of a plot, and
additional layers, such as points, lines, and facets, can be added using
`+` operator (like `%>%`, but for `+`). This makes it easy to
understand, modify the code, and build complex plots by adding layers.
This allows for easy creation of plots that reveal patterns in the data.
In contrast, the basic R plotting functions and qplot() have a simpler
and less expressive syntax, making it harder to create complex and
multi-layered plots. Mastering ggplot() is well worth your time and
effort as it will teach you how to think about graphs and what goes into
building them. For example, let’s improve the histogram from earlier!

    data_raven %>% 
      count(pr_correct) %>% # I prefer calculating statistics myself
      ggplot(aes(x = as.factor(pr_correct), y = n)) + # We use aes to set x and y
      geom_col(fill = "steelblue") +
      theme_minimal(base_size = 15) + 
      theme(panel.grid = element_blank(), 
            panel.grid.major.y = element_line(size = 0.5, linetype = 2, color = "grey")) +
      labs(x = "Number of Correct Answers", 
           y = "Subject Count", 
           title = "Distribution of Correct Answers in Piece-rate Game")

    ## Warning: The `size` argument of `element_line()` is deprecated as of ggplot2 3.4.0.
    ## ℹ Please use the `linewidth` argument instead.

![](../Week%205/data_visualization_files/figure-markdown_strict/unnamed-chunk-3-1.png)
Ah much better! We added labels, removed unnecessary grid lines, and
added some color. If you want to learn more about ggplot check out
[ggplot2: Elegant Graphics for Data Analysis](https://ggplot2-book.org))
and [the
cheatsheet](https://posit.co/wp-content/uploads/2022/10/data-visualization-1.pdf).

We will use an amazing package `esquisse` to build our plots with
drag-and-drop!

    install.packages('esquisse')

    ## 
    ## The downloaded binary packages are in
    ##  /var/folders/_h/1k95hxk12j77hrrss_n49_zw0000gn/T//RtmpEWO53Z/downloaded_packages

    library(esquisse)

You can access `esquisse` by going to “Addins” in the top panel or with
`esquisser(your_data)`. Now go learn more about this package
[here](https://cran.r-project.org/web/packages/esquisse/vignettes/get-started.html).

### 
