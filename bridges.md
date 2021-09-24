Stat 433 HW1
================

``` r
library(readr)
library(magrittr) 
library(dplyr)
```

    ## 
    ## Attaching package: 'dplyr'

    ## The following objects are masked from 'package:stats':
    ## 
    ##     filter, lag

    ## The following objects are masked from 'package:base':
    ## 
    ##     intersect, setdiff, setequal, union

``` r
library(ggplot2)
library(data.table)
```

    ## 
    ## Attaching package: 'data.table'

    ## The following objects are masked from 'package:dplyr':
    ## 
    ##     between, first, last

``` r
#reading in the the date
wi_bridges2020 = fread("https://www.fhwa.dot.gov/bridge/nbi/2020/delimited/WI20.txt")
```

``` r
#change column names, select certain variables, pipe them into new data set to work with 
wi_bridges2020_select=wi_bridges2020%>% 
  rename(bridge_id=STRUCTURE_NUMBER_008,
fips_code=STATE_CODE_001,
rating_decksc=DECK_COND_058,
rating_supersc=SUPERSTRUCTURE_COND_059,
rating_subsc=SUBSTRUCTURE_COND_060,
year_built=YEAR_BUILT_027) %>% 
  select(bridge_id,fips_code,rating_decksc,rating_subsc,rating_supersc,year_built) 
wi_bridges2020_select
```

    ##              bridge_id fips_code rating_decksc rating_subsc rating_supersc
    ##     1: 00000000000F303        55             4            5              5
    ##     2: 00000000000F304        55             5            4              5
    ##     3: 00000000000F310        55             5            7              5
    ##     4: 00000000000F311        55             5            8              7
    ##     5: 00000000000F315        55             5            7              5
    ##    ---                                                                    
    ## 14267: P71094000000000        55             7            8              8
    ## 14268: P73090300000000        55             4            6              6
    ## 14269: P73090400000000        55             4            6              6
    ## 14270: P73090700000000        55             5            7              7
    ## 14271: P73091200000000        55             6            5              7
    ##        year_built
    ##     1:       1932
    ##     2:       1974
    ##     3:       1948
    ##     4:       1979
    ##     5:       1977
    ##    ---           
    ## 14267:       1992
    ## 14268:       1930
    ## 14269:       1957
    ## 14270:       1979
    ## 14271:       1970

``` r
#how many bridges built per year
ggplot(data = wi_bridges2020_select, aes(year_built)) +
  geom_histogram(color = "black", fill = "light blue") +
  xlab("Year Bridges was Built") +
  xlab("Number of Bridges Built")+
  ggtitle("How Many Bridges Built Per Year") 
```

    ## `stat_bin()` using `bins = 30`. Pick better value with `binwidth`.

![](bridges_files/figure-gfm/unnamed-chunk-4-1.png)<!-- -->
