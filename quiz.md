# Data Exploration
  
In this quiz, we will be using Arabica coffee beans reviewed. You can get the csv file from this repository, which is `coffee.csv`. Before we do clustering the data or reduction the dimension using principal component, we need to perform an exploratory analysis to be able to understand the data. Tou can glimpse the structure of our coffee beans reviewed data! You can choose either `str()` or `glimpse()` function.

```
# your code here  
```

Coffee data is consist of 13 variables and 1082 row. coffee dataset is reviews of Arabica coffee beans reviewed by Coffee Quality Institute's highly trained individuals. This is more information about variable in the dataset:    

- `coffeId` : id of coffee    
- `Aroma` : the smell of coffee after adding hot water (e.g.floral, spicy, fruity, winery, sweety, earthy or nutty etc.).    
- `Flavor` : the taste characteristics (e.g. fruity, sour, bitter, rich or balanced etc.).    
- `Aftertaste` : overall impression of the coffee remains in the month.    
- `Acidity` : the sharpness and liveliness of the acidity (e.g. sharp, thin, flat, mild, or neutral etc.).    
- `Body` : the tactile feeling of the coffee in the month (e.g. full, thick, balanced, buttery or thin etc.).    
- `Balance` : no single flavor dominates the other.    
- `Uniformity` : how similarly sized the ground coffee particles are.    
- `Clean cup` : no flavor defects present.    
- `Sweetness` : mild, smooth taste sensation with no harsh flavors.    
- `Cupper points` : points earned from a Cupper (a person who objectively review over the taste and aroma of a brewed coffee, to know whether it’s a Specialty Grade Coffee).    
- `Moisture` : any amount of liquid diffused in small quantities within a green coffee beans, if humidity is stable, the coffee beans will retain that moisture until roasting.    
- `Quakers`: unripened coffee beans, often with a wrinkled surface, not darken well when roasted.    

# 1. Principal Component Analysis (PCA)

## Data Pre-Processing

When we’re looking for features to retain in a dimentionality reduction exercise, we need make sure we scale or normalize our data before running PCA. You can use `scale()` function to scaling the numeric variabel and store it under `coffee_scale`.

```
# Your code
```


## Build your Principal Component
After we have done pre-processing, now we will build the principal component from `coffee_scale`. Then let's see it summary

```
# your code
```

1. With that summary, How many PCs will you take if you only want a PC that gives information above 5%?    
  [ ] 5 PC (PC 1 through 5)    
  [ ] 4 PC (PC 1 through 4)    
  [ ] 1 PC (PC 5 only)    
  

Beside reducing the dimension remember that PCA also good at detecting outlier which we will use biplot to help us to do so, now let's detect the outlier from data using biplot.    
```
# your code
```

2. Based on the visualization using biplot, which coffeee id is the outlier?    
  [ ] 1082, 1080, 1081    
  [ ] 1082, 993, 998    
  [ ] 1081, 308, 201    
  [ ] 1080. 1082, 998    
  
3. PC one is the most collectible PC of all variables. mention the 3 most contributing variables on PC 1!
  [ ] Aroma, Flavor, Aftertaste    
  [ ] Sweetness, Clean.cup, Uniformity    
  [ ] Balance, Flavor, Aftertaste    
  [ ] Moisture, Quakers, Clean.Cup    
  [ ] Acidity, Body, Balance     


4. Which of the following is NOT TRUE about PCA?     
  [ ] Because PCA tries to 'summarize' the covariance between variables of our data, it requires that the input variables to be scaled so they have the same range of measurement    
  [ ] A Principal Component with an eigenvalue of 0.6 is not more helpful than a Principal Component with an eigenvalue of 6.0 in terms of the variance it explains    
  [ ] We cannot fully reconstruct the original data from a PCA even if we use all the eigenvectors and eigenvalues because PCA always result in some loss of variance / information due to its dimensionality reduction process    
  
# 2. K- Means Clustering

Before clustering the data, first you need to remove the data with coffeeId 1082 because the coffee is a fairly extending outlier. After removing the data, do a scaling again on the coffe dataset.    

```
# your code here

```

## 2.1 Choosing Optimum K
after scaling coffee data you need to find the optimum cluster number in k-means. use `kmeansTunning` function to find the optimum K. you can use 100 on set.seed and 10 on maxK.    

```
kmeansTunning <- function(data, maxK) {
  withinall <- NULL
  total_k <- NULL
  for (i in 2:maxK) {
    temp <- kmeans(data,i)$tot.withinss
    withinall <- append(withinall, temp)
    total_k <- append(total_k,i)
  }
  plot(x = total_k, y = withinall, type = "o", xlab = "Number of Cluster", ylab = "Total within")
}

set.seed(100)
kmeansTunning( )

```

5. What is the optimal number of clusters ?    
  - [ ] 4    
  - [ ] 5    
  - [ ] 6   
  - [ ] 7


6. Which of the following is NOT TRUE about K-Means?       
  - [ ] choosing centroid in the first iteration is done randomly
  - [ ] good clusters are clusters with low withinss and high betweenss
  - [ ] cluster with low withinss means characteristics of data in cluster are similar
  - [ ] the greater the value of betweenss, the greater the data variance in each cluster     
  

## 2.2 Clusters Profiling
After finding the optimum number of K, now let's make cluster using the k you chose in the question number five with `set.seed` 100.

```
# your code here
```

7. For a customer who enjoy coffee with `coffeID` 929, which of the following coffee beans may be characteristically similar enough to warrant a recommendation?     
  - [ ] 1060    
  - [ ] 21    
  - [ ] 1071    
  
8. which coffee cluster has the highest mean of aroma, highest mean of sweetness, and lowest mean of acidity?
  - [ ] 5, 1, 2    
  - [ ] 5, 6, 5    
  - [ ] 2, 5, 1    
  - [ ] 2, 4, 1    

