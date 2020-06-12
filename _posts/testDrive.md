---
title: "testDrive"
author: "Yong"
date: '2020 6 12 '
output: html_document
---



## R Markdown

This is an R Markdown document. Markdown is a simple formatting syntax for authoring HTML, PDF, and MS Word documents. For more details on using R Markdown see <http://rmarkdown.rstudio.com>.

When you click the **Knit** button a document will be generated that includes both content as well as the output of any embedded R code chunks within the document. You can embed an R code chunk like this:


{% highlight r %}
summary(cars)
{% endhighlight %}



{% highlight text %}
##      speed           dist       
##  Min.   : 4.0   Min.   :  2.00  
##  1st Qu.:12.0   1st Qu.: 26.00  
##  Median :15.0   Median : 36.00  
##  Mean   :15.4   Mean   : 42.98  
##  3rd Qu.:19.0   3rd Qu.: 56.00  
##  Max.   :25.0   Max.   :120.00
{% endhighlight %}

## Including Plots

You can also embed plots, for example:

![plot of chunk pressure](/assets/article_images/testDrive/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to prevent printing of the R code that generated the plot.


# jekyll ��α� ���丮 ����
base <- "C:/Users/ykun9/yongkcho.github.io"

# Rmd ������ ����� ���丮 ����
rmds <- "_Rmd"
setwd(base)

# ���� �̸� ����
filename <- "2016-01-17-test.Rmd"

# ���� ��ε�
figs.path <- "assets/article_images/"
posts.path <- "_posts/R/"

# Rmd -> md ��ȯ
require(knitr)
render_jekyll(highlight = "pygments")
opts_knit$set(base.url="/")

file <- paste0(rmds, "/", filename)

### ���� ��� ����
fig.path <- paste0(figs.path, sub(".Rmd$", "", basename(file)), "/")
opts_chunk$set(fig.path = fig.path)

### suppress messages
opts_chunk$set(cache = F, warning = F, message = F, cache.path = "_cache/", tidy = F)

### ���� ��ȯ �� ��� ����
out.file <- basename(knit(file))
file.rename(out.file, paste0(posts.path, out.file))
