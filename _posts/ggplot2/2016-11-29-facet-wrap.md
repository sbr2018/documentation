---
title: ggplot2 facet_wrap | Examples | Plotly
name: facet_wrap
permalink: ggplot2/facet_wrap/
description: How to make subplots with facet_wrap in ggplot2 and R.
layout: base
thumbnail: thumbnail/facet_wrap.jpg
language: ggplot2
page_type: example_index
has_thumbnail: true
display_as: layout_opt
output:
  html_document:
    keep_md: true
---



### New to Plotly?

Plotly's R library is free and open source!<br>
[Get started](https://plot.ly/r/getting-started/) by downloading the client and [reading the primer](https://plot.ly/r/getting-started/).<br>
You can set up Plotly to work in [online](https://plot.ly/r/getting-started/#hosting-graphs-in-your-online-plotly-account) or [offline](https://plot.ly/r/offline/) mode.<br>
We also have a quick-reference [cheatsheet](https://images.plot.ly/plotly-documentation/images/r_cheat_sheet.pdf) (new!) to help you get started!

### Version Check

Version 4 of Plotly's R package is now [available](https://plot.ly/r/getting-started/#installation)!<br>
Check out [this post](http://moderndata.plot.ly/upgrading-to-plotly-4-0-and-above/) for more information on breaking changes and new features available in this version.


```r
library(plotly)
packageVersion('plotly')
```

```
## [1] '4.5.6.9000'
```

### Basic Columns


```r
library(reshape2)
library(plotly)

p <- ggplot(tips, aes(x=total_bill, y=tip/total_bill)) + geom_point(shape=1)

# Divide by day, going horizontally and wrapping with 2 columns
p <- p + facet_wrap( ~ day, ncol=2)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetwrap/basic")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4244.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://www.cookbook-r.com/Graphs/Scatterplots_(ggplot2)/">Cookbook for R</a>

### Add Unique Curves


```r
library(plotly)

## read in data set (tolerance data from the ALDA book)
tolerance <- read.table("http://www.ats.ucla.edu/stat/r/examples/alda/data/tolerance1_pp.txt",
    sep = ",", header = TRUE)

## change id and male to factor variables
tolerance <- within(tolerance, {
    id <- factor(id)
    male <- factor(male, levels = 0:1, labels = c("female", "male"))
})


p <- ggplot(data = tolerance, aes(x = time, y = tolerance)) + geom_point() +
    stat_smooth(method = "lm", se = FALSE) + facet_wrap(~id)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetwrap/curves")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4246.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://www.ats.ucla.edu/stat/r/faq/growth.htm">The IDRE at UCLA</a>

### Add Stat_Smooth


```r
library(plotly)

p <- ggplot(mpg, aes(displ, hwy))+
  geom_point()+
  stat_smooth()+
  facet_wrap(~year)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetwrap/stat_smooth")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4248.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://www.ling.upenn.edu/~joseff/rstudy/summer2010_ggplot2_intro.html">R Study Group</a>

### Labels


```r
library(plotly)
set.seed(123)

df <- diamonds[sample(1:nrow(diamonds), size = 1000), ]

# Create labels
labs <- c("Best","Second best","Third best","Average", "Average","Third Worst","Second Worst","Worst")
levels(df$clarity) <- rev(labs)

p <- ggplot(df, aes(carat, price)) + 
  geom_point() + 
  facet_wrap(~ clarity)

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetwrap/labels")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4250.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://stackoverflow.com/questions/3472980/ggplot-how-to-change-facet-labels">Stack Overflow</a>

### Titles


```r
library(plotly)
set.seed(123)

df <- diamonds[sample(1:nrow(diamonds), size = 1000), ]

# Create labels
labs <- c("Best","Second best","Third best","Average", "Average","Third Worst","Second Worst","Worst")
levels(df$clarity) <- rev(labs)

p <- ggplot(df, aes(carat, price)) + 
  geom_point() + 
  facet_wrap(~ clarity) + 
  ggtitle("Diamonds dataset facetted by clarity")

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetwrap/titles")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4252.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://docs.ggplot2.org/current/">ggplot2 Documentation</a>

### Ordered Facets


```r
library(plotly)
set.seed(123)

df <- diamonds[sample(1:nrow(diamonds), size = 1000), ]

# Reorer levels

levels(df$clarity) <- c("VS2", "VS1", "VVS2", "I1", "SI2", "IF", "VVS1", "SI1")

p <- ggplot(df, aes(carat, price)) + 
  geom_point() + 
  facet_wrap(~ clarity) + 
  ggtitle("Diamonds dataset facetted by clarity")

p <- ggplotly(p)

# Create a shareable link to your chart
# Set up API credentials: https://plot.ly/r/getting-started
chart_link = plotly_POST(p, filename="facetwrap/ordered")
chart_link
```

<iframe src="https://plot.ly/~RPlotBot/4254.embed" width="800" height="600" id="igraph" scrolling="no" seamless="seamless" frameBorder="0"> </iframe>
Inspired by <a href="http://stackoverflow.com/questions/3311901/how-do-i-get-ggplot-to-order-facets-correctly">Stack Overflow</a>
