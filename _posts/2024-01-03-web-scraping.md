---
layout: post
title: "R for Web Data: Mining Insights from Websites"
subtitle: "Extract Movie Data from IMDB: A Guide with rvest"
background: '/img/posts/web-scrape/comedy movies.jpg'

---

## Intro of the post

We are searching data from IMDB Comedy TV series that have 5.0 or above ratings. This post gives you an insight baout how scarping the names, years and synopsis of the top 100 comedy movies at the IMDB. Web scraping provides a convenient method for retrieving information from websites lacking an API or offering direct data access. This guide will explain the process of extracting details such as names, years, ratings, and synopses from the top 100 adventure movies on IMDb.

## Install required packages

```
install.packages("rvest")
install.packages("dplyr")
```

## The Web page of IMDB

![IMDB Page](/img/posts/web-scrape/IMDB-page.png)

## Load libraries
```
library(rvest)
library(dplyr)
```

## Read the web page
```
link = "https://www.imdb.com/search/title/?title=Comedy&title_type=tv_series&user_rating=5,"
page = read_html(link)
```

## Scrape the data
```
name = page %>% html_nodes(".lister-item-header a") %>% html_text()
year = page %>% html_nodes(".text-muted.unbold") %>% html_text()
rating = page %>% html_nodes(".ratings-imdb-rating strong") %>% html_text()
synopsis = page %>% html_nodes(".ratings-bar+ .text-muted") %>% html_text()
```

## Convert data to a data frame
movies = data.frame(name, year, rating, synopsis, stringsAsFactors = FALSE)

## Write to CSV
write.csv(movies, "movies.csv", row.names = FALSE)