# R-notes

## Read csv file with ";" as a separator
tabA <- read.csv(file=<path_to_file_A>,head=TRUE,sep=";")
tabB <- read.csv(file=<path_to_file_B>,head=TRUE,sep=";")

In Windows the path syntax is: <path_to_file_A>="C:\\path\\to\\file\\A.

## Remove columns with constant values. They can be shifted to meta-data table. 
tabA2 <- tabA[sapply(tabA, function(x) length(unique(x))>1)]
tabB2 <- tabB[sapply(tabB, function(x) length(unique(x))>1)]
