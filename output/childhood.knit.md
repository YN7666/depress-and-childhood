---
title: " Is there an association between early childhood adversity and higher depression scores in US adults?"
author: "Vincent Yu"
date: "2024-6-18"
output:
  pdf_document:
    latex_engine: xelatex
---


``` r
#needed questionnaires
#install.packages("haven")
#install.packages("nhanesA")
library(haven)
library(tidyverse)
```

```
## -- Attaching core tidyverse packages ------------------------ tidyverse 2.0.0 --
## v dplyr     1.1.4     v readr     2.1.5
## v forcats   1.0.0     v stringr   1.5.1
## v ggplot2   3.5.1     v tibble    3.2.1
## v lubridate 1.9.3     v tidyr     1.3.1
## v purrr     1.0.2     
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
## i Use the conflicted package (<http://conflicted.r-lib.org/>) to force all conflicts to become errors
```

``` r
#library(nhanesA)
depress <- read_xpt("D:/_uoft_1/5硕士1/depress-and-childhood/data/DPQ_J.XPT")
#depress <- nhanes("DPQ_J")
child <- read_xpt("D:/_uoft_1/5硕士1/depress-and-childhood/data/ECQ_J.XPT")
#depress <- nhanes("ECQ_J")
```


``` r
# merge 2 datasets
clean_data_T <- merge(depress, child, by = "SEQN", all.x =T, all.y =T)
clean_data_F <- merge(depress, child, by = "SEQN", all=FALSE)
head(clean_data_T)
```

```
##    SEQN DPQ010 DPQ020 DPQ030 DPQ040 DPQ050 DPQ060 DPQ070 DPQ080 DPQ090 DPQ100
## 1 93703     NA     NA     NA     NA     NA     NA     NA     NA     NA     NA
## 2 93704     NA     NA     NA     NA     NA     NA     NA     NA     NA     NA
## 3 93705      0      0      0      0      0      0      0      0      0     NA
## 4 93706      0      0      0      0      0      0      0      0      0     NA
## 5 93707     NA     NA     NA     NA     NA     NA     NA     NA     NA     NA
## 6 93708      0      0      0      0      0      0      0      0      0     NA
##   ECD010 ECQ020 ECD070A ECD070B ECQ080 ECQ090 WHQ030E MCQ080E ECQ150
## 1     35      2       8      11     NA     NA       3       2     NA
## 2     29      2       7       9     NA     NA       3       2     NA
## 3     NA     NA      NA      NA     NA     NA      NA      NA     NA
## 4     NA     NA      NA      NA     NA     NA      NA      NA     NA
## 5     34      2       7       2     NA     NA       3       2     NA
## 6     NA     NA      NA      NA     NA     NA      NA      NA     NA
```

``` r
head(clean_data_F)
```

```
##  [1] SEQN    DPQ010  DPQ020  DPQ030  DPQ040  DPQ050  DPQ060  DPQ070  DPQ080 
## [10] DPQ090  DPQ100  ECD010  ECQ020  ECD070A ECD070B ECQ080  ECQ090  WHQ030E
## [19] MCQ080E ECQ150 
## <0 行> (或0-长度的row.names)
```

``` r
# filter missing and refused
```

According to the previous article, participants who scored 10 or more were considered to have clinically significant depressive symptoms (Jackson et al., 2019)
