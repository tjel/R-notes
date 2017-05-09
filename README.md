# R-notes

# Linear regression stuff
```R
library(lmtest)

dataset <- read.csv("C:\\Users\\tjelinski\\Pobrane\\dataset.csv",header=T)

y <- dataset$zmienna_zalezna
x1 <- dataset$zmienna_niezalezna_1
x2 <- dataset$zmienna_niezalezna_2
multi.fit <- lm(y~x1+x2+x1:x2+I(x1^2)+I(x2^2), data=dataset)
summary(multi.fit)


ynew <- dataset$
xnew <- dataset$
newfit <- lm(ynew~xnew)
res <- residuals(newfit)

shapiro.test(res)
gqtest(ynew ~ xnew)
bgtest(ynew~xnew)
bgtest(ynew~xnew,order=4)
resettest(ynew~xnew, power =2, type="regressor")

shapiro.test(rnorm(100,mean=5,sd=3))
```


#### Read csv files with `;` as a separator
```R
tabA <- read.csv(file=<path_to_file_A>, head=TRUE, sep=";")
tabB <- read.csv(file=<path_to_file_B>, head=TRUE, sep=";")
```

In Windows the path syntax is: `<path_to_file_A>="C:\\path\\to\\file\\A.csv.`

#### Remove columns with constant values. They can be shifted to meta-data table. 
```R
tabA2 <- tabA[sapply(tabA, function(x) length(unique(x))>1)]
tabB2 <- tabB[sapply(tabB, function(x) length(unique(x))>1)]
```

#### Define columns which are not very informative.
```R
tabAdrops <- c("colA1", "colA2", "colA3")
tabBdrops <- c("colB1", "colB2")
```

#### Delete not very informative columns.
```R
tabA3 <- tabA2[, !(names(tabA2) %in% tabAdrops)]
tabB3 <- tabB2[, !(names(tabB2) %in% tabBdrops)]
```

#### Full join both tables on column `colA4`
```R
tabBdane <- merge(x = tabA3, y = tabB3, by = "colA4", all = TRUE)
```

#### Write output table as a csv with `;` as a separator. Use `quote = FALSE` to get rid of `""` around each string.
```R
write.csv2(tabBdane, <path_to_output_csv_file>,quote = FALSE, row.names = FALSE)
```

#### Translate accented characters by `chartr` or by `gsub` function
```R
mydata <- c("ą", "ę")
chartr("ąęć", "aec", mydata)
mydata2 <- chartr("ąćęłńóśźżĄĆĘŁŃÓŚŹŻ", "acelnoszzACELNOSZZ", mydata)
mydata3 <- gsub("ą", "a", mydata3)
sapply(mydata, gsub, pattern="ą", replacement="a")
```

#### Convert accented characters/diacritic signs to ASCII signs using `stri_trans_general` from `stringi` library
```R
library(stringi)
tabBdane2 <- as.data.frame(lapply(tabBdane, function(x) stri_trans_general(x,"latin-ascii")))
```

#### Save converted data to a csv file
```R
write.csv2(tabBdane2, <path_to_output_csv_file>, quote = FALSE, row.names = FALSE)
```
