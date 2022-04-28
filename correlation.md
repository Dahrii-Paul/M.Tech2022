# Correlation 
#### Defines the relationship between two variables that is how the two variables are linked with each other

```R
setwd("/home/paul/Downloads/R")
getwd()
list.files()
# "header=F" take 1st row as part of the observation
countMatrix=read.csv("gene_exp.csv",head=T,row.names=1,sep=",")
head(countMatrix )
dim(countMatrix)
rownames(countMatrix)
colnames(countMatrix)

## Filter out lowly expressed genes
# in this case keep genes expressed more than 5 in at least 3 samples. 
# But could be too strict
use = rowSums(countMatrix > 5) >=3
head(use)
countMatrixFiltered = countMatrix[use, ]
dim(countMatrixFiltered)

#example
mat<-matrix(c(1:12), nrow = 3, byrow=T)
mat
mat[2:3,]

#log2 transform (x+1 to avoid zeroes)
log2countMatrix = log2(countMatrixFiltered+1)
class(log2countMatrix)
t_countMat<-t(log2countMatrix)
head(t_countMat)
corr_expr<-cor(t_countMat,method="pearson")

# Get p-value
install.packages('psych')
library(psych)
p_value<-corr.test(corr_expr)$p 

### Heatmap
install.packages("corrplot")
library(corrplot)
corrplot(corr_expr)
corrplot(corr_expr, order = 'hclust', addrect = 4)
corrplot(corr_expr, method="pie")
palette = colorRampPalette(c("green", "white", "red")) (20)
heatmap(x = corr_expr, col = palette, symm = TRUE)

corrplot(corr_expr, type="upper", order="hclust", 
         p.mat = p_value, sig.level = 0.01)

corrplot(corr_expr, type="upper", order="hclust", 
         p.mat = p_value, sig.level = 0.01,insig = "blank" )
corrplot(corr_expr, type="full", order="hclust", 
         p.mat = p_value, sig.level = 0.01,insig = "blank" )
```
