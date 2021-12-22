# Data-Analysis
## Basic EDA
Let us look at the dimensions to know number of rows and columns in the data
```{r}
library(rstatix)
library(nortest)
library(knitr)
nycTaxi <- read.csv("C:\\Users\\Manoja\\Downloads\\nyc-taxi.csv")
dim(nycTaxi)
```

There are 100000 observations and 16 variables in the imported data set

Following code will allow us to understand the summary of data
```{r}
summary(nycTaxi)
```
Let us look into the trip duration of this dataset.
The variable Trip duration is right skewed with very long tail. we will therefore take the log to normalise the Trip Duration distribution.


```{r}
library(ggplot2)
g <- ggplot(data=nycTaxi,aes(nycTaxi$trip_duration))
g + geom_histogram(col="blue",bins=100) + 
  labs(title="Histogram of Trip Duration")+ xlab("Trip Duration") 
```


Let us check the new plot. The log of the trip duration is normally distributed, although with a high peak.

```{r}
g <- ggplot(data=nycTaxi,aes(log(nycTaxi$trip_duration+1))) + geom_histogram(col="blue",bins=100) + 
  labs(title="Histogram of Trip Duration") + xlab("Trip Duration") 
g
```

Let us see how the tip amounts and total amounts are spread across the vendors 

```{r}
library(ggplot2)
ggplot(nycTaxi, aes(x = nycTaxi$tip_amount, y = nycTaxi$total_amount, colour = nycTaxi$Vendor)) +
  geom_point() + xlab("Tip Amount") + ylab("Total Amount") +
  facet_wrap( ~ nycTaxi$Vendor)+ labs(fill = "Vendor")
```

We can see that among the two types of vendors, VeriFone Inc has received the most tips and has earned few highest Total Amounts compared to Creative Mobile Technologies LLC.
