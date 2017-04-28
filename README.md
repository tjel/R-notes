# R-notes

### Read csv file with ";" as a separator
```R
tabA <- read.csv(file=<path_to_file_A>,head=TRUE,sep=";")
tabB <- read.csv(file=<path_to_file_B>,head=TRUE,sep=";")
```

In Windows the path syntax is: `<path_to_file_A>="C:\\path\\to\\file\\A.csv.`

### Remove columns with constant values. They can be shifted to meta-data table. 
```R
tabA2 <- tabA[sapply(tabA, function(x) length(unique(x))>1)]
tabB2 <- tabB[sapply(tabB, function(x) length(unique(x))>1)]
```

### Define columns which are not very informative.
```R
tabAdrops <- c("colA1","colA2","colA3")
tabBdrops <- c("colB1", "colB2")
```

### Delete not very informative columns.
```R
tabA3 <- tabA2[,!(names(tabA2) %in% tabAdrops)]
tabB3 <- tabB2[,!(names(tabB2) %in% tabBdrops)]
```
