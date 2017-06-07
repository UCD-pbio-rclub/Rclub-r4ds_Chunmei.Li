# data import
Chunmei Li  
2017年6月6日  

```r
library(tidyverse)
```

```
## Warning: package 'tidyverse' was built under R version 3.3.3
```

```
## Loading tidyverse: ggplot2
## Loading tidyverse: tibble
## Loading tidyverse: tidyr
## Loading tidyverse: readr
## Loading tidyverse: purrr
## Loading tidyverse: dplyr
```

```
## Warning: package 'ggplot2' was built under R version 3.3.3
```

```
## Warning: package 'tidyr' was built under R version 3.3.3
```

```
## Warning: package 'readr' was built under R version 3.3.3
```

```
## Warning: package 'purrr' was built under R version 3.3.3
```

```
## Warning: package 'dplyr' was built under R version 3.3.3
```

```
## Conflicts with tidy packages ----------------------------------------------
```

```
## filter(): dplyr, stats
## lag():    dplyr, stats
```


```r
#no path
#heights <- read_csv("data/heights.csv")
```


```r
read_csv("a,b,c
1,2,3
4,5,6")
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```

```r
read_csv("The first line of metadata
  The second line of metadata
  x,y,z
  1,2,3", skip = 2)
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```


```r
read_csv("# A comment I want to skip 
x,y,z
  1,2,3", comment = "#")
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
```


```r
read_csv("1,2,3\n4,5,6", col_names = FALSE)
```

```
## # A tibble: 2 × 3
##      X1    X2    X3
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```


```r
read_csv("1,2,3\n4,5,6", col_names = c("x", "y", "z"))
```

```
## # A tibble: 2 × 3
##       x     y     z
##   <int> <int> <int>
## 1     1     2     3
## 2     4     5     6
```


```r
read_csv("a,b,c\n1,2,.", na = ".")
```

```
## # A tibble: 1 × 3
##       a     b     c
##   <int> <int> <chr>
## 1     1     2  <NA>
```


read_csv() reads comma delimited files, read_csv2() reads semicolon separated files (common in countries where , is used as the decimal place), read_tsv() reads tab delimited files, and read_delim() reads in files with any delimiter.

read_fwf() reads fixed width files. You can specify fields either by their widths with fwf_widths() or their position with fwf_positions(). read_table() reads a common variation of fixed width files where columns are separated by white space.

read_log() reads Apache style log files. (But also check out webreadr which is built on top of read_log() and provides many more helpful tools.)

11.2.2 Exercise

1.
read_delim

2.


```r
?read_csv
```

```
## starting httpd help server ...
```

```
##  done
```
col_names, col_types, locale, na, quoted_na, quote, trim_ws, n_max, guess_max, progress

3.


```r
?read_fwf
```

fwf_widths

4.


```r
read_delim("x,y\n1,'a,b'", delim=",", quote="\'")
```

```
## # A tibble: 1 × 2
##       x     y
##   <int> <chr>
## 1     1   a,b
```

5.


```r
read_csv("a,b\n1,2,3\n4,5,6") #lost the third element
```

```
## Warning: 2 parsing failures.
## row col  expected    actual         file
##   1  -- 2 columns 3 columns literal data
##   2  -- 2 columns 3 columns literal data
```

```
## # A tibble: 2 × 2
##       a     b
##   <int> <int>
## 1     1     2
## 2     4     5
```

```r
read_csv("a,b,c\n1,2\n1,2,3,4") #add NA to 1st row, and lost the 4th element in 2nd row
```

```
## Warning: 2 parsing failures.
## row col  expected    actual         file
##   1  -- 3 columns 2 columns literal data
##   2  -- 3 columns 4 columns literal data
```

```
## # A tibble: 2 × 3
##       a     b     c
##   <int> <int> <int>
## 1     1     2    NA
## 2     1     2     3
```

```r
read_csv("a,b\n\"1") #double-quote
```

```
## Warning: 2 parsing failures.
## row col                     expected    actual         file
##   1  a  closing quote at end of file           literal data
##   1  -- 2 columns                    1 columns literal data
```

```
## # A tibble: 1 × 2
##       a     b
##   <int> <chr>
## 1     1  <NA>
```

```r
read_csv("a,b\n1,2\na,b") # integer 1 and 2 become character.
```

```
## # A tibble: 2 × 2
##       a     b
##   <chr> <chr>
## 1     1     2
## 2     a     b
```

```r
read_csv("a;b\n1;3") # 1 element, a;b is column name, 1;3 is value
```

```
## # A tibble: 1 × 1
##   `a;b`
##   <chr>
## 1   1;3
```



```r
str(parse_logical(c("TRUE", "FALSE", "NA")))
```

```
##  logi [1:3] TRUE FALSE NA
```

```r
str(parse_integer(c("1", "2", "3")))
```

```
##  int [1:3] 1 2 3
```

```r
str(parse_date(c("2010-01-01", "1979-10-14")))
```

```
##  Date[1:2], format: "2010-01-01" "1979-10-14"
```


```r
parse_integer(c("1", "231", ".", "456"), na = ".")
```

```
## [1]   1 231  NA 456
```


```r
x <- parse_integer(c("123", "345", "abc", "123.45"))
```

```
## Warning: 2 parsing failures.
## row col               expected actual
##   3  -- an integer                abc
##   4  -- no trailing characters    .45
```

```r
x
```

```
## [1] 123 345  NA  NA
## attr(,"problems")
## # A tibble: 2 × 4
##     row   col               expected actual
##   <int> <int>                  <chr>  <chr>
## 1     3    NA             an integer    abc
## 2     4    NA no trailing characters    .45
```

```r
problems(x)
```

```
## # A tibble: 2 × 4
##     row   col               expected actual
##   <int> <int>                  <chr>  <chr>
## 1     3    NA             an integer    abc
## 2     4    NA no trailing characters    .45
```

```r
parse_double("1.23")
```

```
## [1] 1.23
```


```r
parse_double("1,23", locale = locale(decimal_mark = ","))
```

```
## [1] 1.23
```


```r
parse_number("$100")
```

```
## [1] 100
```

```r
parse_number("20%")
```

```
## [1] 20
```

```r
parse_number("It cost $123.45") #different output from book
```

```
## [1] 123.45
```


```r
# Used in America
parse_number("$123,456,789")
```

```
## [1] 123456789
```

```r
# Used in many parts of Europe
parse_number("123.456.789", locale = locale(grouping_mark = "."))
```

```
## [1] 123456789
```

```r
# Used in Switzerland
parse_number("123'456'789", locale = locale(grouping_mark = "'"))
```

```
## [1] 123456789
```


```r
charToRaw("Hadley")
```

```
## [1] 48 61 64 6c 65 79
```


```r
x1 <- "El Ni\xf1o was particularly bad this year"
x2 <- "\x82\xb1\x82\xf1\x82\xc9\x82\xbf\x82\xcd"

x1
```

```
## [1] "El Ni駉 was particularly bad this year"
```

```r
x2
```

```
## [1] "偙傫偵偪偼"
```

```r
#???
```


```r
parse_character(x1, locale = locale(encoding = "Latin1"))
```

```
## [1] "El Ni<U+00F1>o was particularly bad this year"
```

```r
parse_character(x2, locale = locale(encoding = "Shift-JIS"))
```

```
## [1] "こんにちは"
```


```r
guess_encoding(charToRaw(x1))
```

```
## # A tibble: 2 × 2
##     encoding confidence
##        <chr>      <dbl>
## 1 ISO-8859-1       0.46
## 2 ISO-8859-9       0.23
```

```r
guess_encoding(charToRaw(x2))
```

```
## # A tibble: 1 × 2
##   encoding confidence
##      <chr>      <dbl>
## 1   KOI8-R       0.42
```


```r
fruit <- c("apple", "banana")
parse_factor(c("apple", "banana", "bananana"), levels = fruit)
```

```
## Warning: 1 parsing failure.
## row col           expected   actual
##   3  -- value in level set bananana
```

```
## [1] apple  banana <NA>  
## attr(,"problems")
## # A tibble: 1 × 4
##     row   col           expected   actual
##   <int> <int>              <chr>    <chr>
## 1     3    NA value in level set bananana
## Levels: apple banana
```


```r
parse_datetime("2010-10-01T2010")
```

```
## [1] "2010-10-01 20:10:00 UTC"
```

```r
parse_datetime("20101010")
```

```
## [1] "2010-10-10 UTC"
```


```r
parse_date("2010-10-01")
```

```
## [1] "2010-10-01"
```


```r
library(hms)
```

```
## Warning: package 'hms' was built under R version 3.3.3
```

```r
parse_time("01:10 am")
```

```
## 01:10:00
```

```r
parse_time("20:10:01")
```

```
## 20:10:01
```


```r
parse_date("01/02/15", "%m/%d/%y")
```

```
## [1] "2015-01-02"
```

```r
parse_date("01/02/15", "%d/%m/%y")
```

```
## [1] "2015-02-01"
```

```r
parse_date("01/02/15", "%y/%m/%d")
```

```
## [1] "2001-02-15"
```


```r
parse_date("1 janvier 2015", "%d %B %Y", locale = locale("fr"))
```

```
## [1] "2015-01-01"
```

```r
date_names_langs()
```

```
##   [1] "af"  "agq" "ak"  "am"  "ar"  "as"  "asa" "az"  "bas" "be"  "bem"
##  [12] "bez" "bg"  "bm"  "bn"  "bo"  "br"  "brx" "bs"  "ca"  "cgg" "chr"
##  [23] "cs"  "cy"  "da"  "dav" "de"  "dje" "dsb" "dua" "dyo" "dz"  "ebu"
##  [34] "ee"  "el"  "en"  "eo"  "es"  "et"  "eu"  "ewo" "fa"  "ff"  "fi" 
##  [45] "fil" "fo"  "fr"  "fur" "fy"  "ga"  "gd"  "gl"  "gsw" "gu"  "guz"
##  [56] "gv"  "ha"  "haw" "he"  "hi"  "hr"  "hsb" "hu"  "hy"  "id"  "ig" 
##  [67] "ii"  "is"  "it"  "ja"  "jgo" "jmc" "ka"  "kab" "kam" "kde" "kea"
##  [78] "khq" "ki"  "kk"  "kkj" "kl"  "kln" "km"  "kn"  "ko"  "kok" "ks" 
##  [89] "ksb" "ksf" "ksh" "kw"  "ky"  "lag" "lb"  "lg"  "lkt" "ln"  "lo" 
## [100] "lt"  "lu"  "luo" "luy" "lv"  "mas" "mer" "mfe" "mg"  "mgh" "mgo"
## [111] "mk"  "ml"  "mn"  "mr"  "ms"  "mt"  "mua" "my"  "naq" "nb"  "nd" 
## [122] "ne"  "nl"  "nmg" "nn"  "nnh" "nus" "nyn" "om"  "or"  "os"  "pa" 
## [133] "pl"  "ps"  "pt"  "qu"  "rm"  "rn"  "ro"  "rof" "ru"  "rw"  "rwk"
## [144] "sah" "saq" "sbp" "se"  "seh" "ses" "sg"  "shi" "si"  "sk"  "sl" 
## [155] "smn" "sn"  "so"  "sq"  "sr"  "sv"  "sw"  "ta"  "te"  "teo" "th" 
## [166] "ti"  "to"  "tr"  "twq" "tzm" "ug"  "uk"  "ur"  "uz"  "vai" "vi" 
## [177] "vun" "wae" "xog" "yav" "yi"  "yo"  "zgh" "zh"  "zu"
```


```r
parse_date("2017年6月6日", "%Y %m %d", locale = locale("zh"))
```

```
## Warning: 1 parsing failure.
## row col           expected       actual
##   1  -- date like %Y %m %d 2017年6月6日
```

```
## [1] NA
```


11.3.5 Exercise

1.

```r
?locale
```
decimal_mark, grouping_mark, encoding

2.

```r
#parse_double("1,23", locale = locale(decimal_mark = ",", grouping_mark = ","))
#Error: `decimal_mark` and `grouping_mark` must be different
```


```r
parse_number("123,456", locale=locale(decimal_mark=","))
```

```
## [1] 123.456
```

```r
#"," became into decimal mark
```

```r
parse_number("123.456", locale=locale(grouping_mark="."))
```

```
## [1] 123456
```

```r
#"." became into grouping mark
```

3.


```r
parse_date("2015/02/19", locale=locale(date_format = "%Y/%m/%d"))
```

```
## [1] "2015-02-19"
```

```r
parse_time("06/24/46", locale=locale(time_format = "%H/%M/%S"))
```

```
## 06:24:46
```

4.

??

5.

read_csv() reads comma "," delimited files, read_csv2() reads semicolon ";" separated files (common in countries where , is used as the decimal place)


```r
read_csv("x,y,z\n4,5,6", col_names =T)
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     4     5     6
```

```r
read_csv2("x;y;z\n4;5;6", col_names = T)
```

```
## Using ',' as decimal and '.' as grouping mark. Use read_delim() for more control.
```

```
## # A tibble: 1 × 3
##       x     y     z
##   <int> <int> <int>
## 1     4     5     6
```

6.

d1 <- "January 1, 2010"
d2 <- "2015-Mar-07"
d3 <- "06-Jun-2017"
d4 <- c("August 19 (2015)", "July 1 (2015)")
d5 <- "12/30/14" # Dec 30, 2014
t1 <- "1705"
t2 <- "11:15:10.12 PM"


```r
d1 <- parse_date("January 1, 2010", "%B %d, %Y")
d1
```

```
## [1] "2010-01-01"
```


```r
d2 <- parse_date("2015-Mar-07", "%Y-%b-%d")
d2
```

```
## [1] "2015-03-07"
```


```r
d3 <- parse_date("06-Jun-2017", "%d-%b-%Y")
d3
```

```
## [1] "2017-06-06"
```


```r
d4 <- parse_date(c("August 19 (2015)", "July 1 (2015)"), "%B %d (%Y)")
d4
```

```
## [1] "2015-08-19" "2015-07-01"
```


```r
d5 <- parse_date("12/30/14", "%m/%d/%y")
d5
```

```
## [1] "2014-12-30"
```


```r
t1 <- parse_time("1705", "%H%M")
t1
```

```
## 17:05:00
```


```r
t2 <- parse_time("11:15:10.12 PM", "%I:%M:%OS %p")
t2
```

```
## 23:15:10.12
```

