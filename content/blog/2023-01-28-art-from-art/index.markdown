---
title: "Art from Art"
author: "Katherine"
date: '2023-01-28'
draft: false
slug: art-from-art
categories: []
tags: [art, tidytuesday]
---


I was really excited to see that the [Tidy
Tuesday](https://github.com/rfordatascience/tidytuesday) for last week
(1/17) was on Art! I haven't found a lot of great art data sets, and
definitely not a lot with numerical data, so I was pretty interested in
taking this data for a spin. The data is from the package
[arthistory](https://saralemus7.github.io/arthistory/), and was
originally collected as part of an undergraduate thesis on demographic
representation in Art History textbooks. I decided that rather than
analyzing the set of data, I was more interested in how the data could
be used to produce generative art. With that goal in mind, I dug into
exploring the data.

## Libraries and all that jazz



```r
# install.packages("arthistory")
library(arthistory)

# install.packages("MetBrewer")

# Art themed art must be art colored
library(MetBrewer)

# essentially my utilities 
library(tidyverse)
```

```
## ── Attaching packages ─────────────────────────────────────── tidyverse 1.3.2 ──
## ✔ ggplot2 3.4.0      ✔ purrr   1.0.1 
## ✔ tibble  3.1.8      ✔ dplyr   1.0.10
## ✔ tidyr   1.3.0      ✔ stringr 1.5.0 
## ✔ readr   2.1.3      ✔ forcats 0.5.2 
## ── Conflicts ────────────────────────────────────────── tidyverse_conflicts() ──
## ✖ dplyr::filter() masks stats::filter()
## ✖ dplyr::lag()    masks stats::lag()
```

```r
library(here)
```

```
## here() starts at /Users/katherine/Desktop/Projects/katherine-blog
```

```r
library(glue)
```


```r
# setting the all important seed
set.seed(9902)
# from https://www.calculatorsoup.com/calculators/statistics/random-number-generator.php
# range 1 - 10,000
```


## Initial Exploration



```r
glimpse(worksjanson)
```

```
## Rows: 1,634
## Columns: 25
## $ artist_name                      <chr> "A. R. Penck", "A. R. Penck", "Aaron …
## $ artist_unique_id                 <dbl> 1, 1, 2, 2, 2, 2, 3, 3, 4, 4, 5, 6, 6…
## $ artist_nationality               <chr> "German", "German", "American", "Amer…
## $ artist_gender                    <chr> "Male", "Male", "Male", "Male", "Male…
## $ artist_race                      <chr> "White", "White", "White", "White", "…
## $ artist_ethnicity                 <chr> "Not Hispanic or Latinx", "Not Hispan…
## $ title_of_work                    <chr> "The Demon of Curiosity", "The Demon …
## $ edition_number                   <dbl> 5, 6, 3, 4, 5, 6, 5, 6, 7, 8, 7, 7, 8…
## $ publication_year                 <dbl> 1995, 2001, 1986, 1991, 1995, 2001, 1…
## $ part_in_text                     <dbl> 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4…
## $ chapter_title                    <chr> "Post-Modernism", "Post-Modernism", "…
## $ start_date                       <dbl> 1982, 1982, 1951, 1951, 1951, 1951, 1…
## $ end_date                         <dbl> 1982, 1982, 1951, 1951, 1951, 1951, 1…
## $ circa                            <chr> "0", "0", "0", "0", "0", "0", "0", "0…
## $ medium                           <chr> "Acrylic on canvas", "Acrylic on canv…
## $ height_of_work_in_book           <dbl> 8.5725, 8.5725, 11.1125, 11.1125, 10.…
## $ width_of_work_in_book            <dbl> 8.8900, 8.8900, 8.8900, 8.8900, 8.890…
## $ height_of_text                   <dbl> 12.0650, 10.7950, 3.1750, 3.1750, 3.1…
## $ width_of_text                    <dbl> 8.890, 8.890, 8.890, 8.890, 8.890, 8.…
## $ area_actual_work                 <chr> "78419.60123", "78419.60123", "0", "0…
## $ area_of_work_in_book             <dbl> 76.20952, 76.20952, 98.79013, 98.7901…
## $ area_of_text                     <dbl> 107.25785, 95.96755, 28.22575, 28.225…
## $ work_to_figure_ratio             <chr> "1029", "1029", "0", "0", "0", "0", "…
## $ work_in_text_in_color            <dbl> 1, 1, 0, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1…
## $ location_as_catalogued_in_janson <chr> "Riverdell Collection, New York. Cour…
```


I was interested in using medium as the color for my art, however, it
looks like there are a lot of different mediums listed, let's take a
look at all of them:



```r
worksjanson |> 
  select(medium) |> 
  group_by(medium) |> 
  summarize(count = n()) |> 
  arrange(-count)
```

```
## # A tibble: 168 × 2
##    medium               count
##    <chr>                <int>
##  1 Oil on canvas          996
##  2 Photograph              72
##  3 Gelatin-silver print    64
##  4 Acrylic on canvas       28
##  5 Lithograph              27
##  6 Oil on panel            18
##  7 Collage                 15
##  8 Albumen print           12
##  9 Platinum print          11
## 10 Woodcut                 11
## # … with 158 more rows
```


hi hi moo 

