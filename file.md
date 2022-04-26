# File handling
getwd()
setwd("/cloud/project/data")
sepsis<-read.csv(file="Sepsis.csv", header=T)
head(sepsis,2)
colnames(sepsis)
x<-read.
delim("clipboard")

sepsis$Shock<-factor(sepsis$Shock,
                     label=c("no","yes"))
sepsis$Alcoholism <-factor(sepsis$Alcoholism, 
                           labels=c("no","yes"))
sepsis$Infarction <-factor(sepsis$Infarction, 
                           labels=c("no","yes"))
head(sepsis)
sepsis<-sepsis[-1]
