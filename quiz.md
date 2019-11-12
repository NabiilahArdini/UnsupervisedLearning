# Data Exploration
  
In this quiz, we will be using Arabica coffee beans reviews. You can get the csv file stored within the folder under `coffee.csv` file. Before we perform data clustering and principle component analysis, we will need to perform exploratory data analysis. You can glimpse the structure of our dataset! You can choose either `str()` or `glimpse()` function.

```
# your code here  
```

This dataset consisted of 13 variables and 1082 rows and contain reviews of varieties of Arabica coffee beans reviewed by Coffee Quality Institute's highly trained individuals. Take a look at the following glossary:    

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

When we are looking for information to retain in a dimentionality reduction exercise, we will need make sure we scale or normalize our data before performing a PCA. You can use `scale()` function to scaling the numeric variabel and store it under `coffee_scale`.

## Build your Principal Component

Using our scaled dataset, we will try to generate the principal component from `coffee_scale`. Recall how we use `FactoMineR` library to perform PCA. Use `PCA()` function for our scaled dataset and store it under `pca_coffee` object. Now check the `summary()` of the model.

1. Using the information from model summary, how many PCs will you use if you only tolerate no more than 20% of information loss?    
  [ ] 5 PC (PC 1 through 5)    
  [ ] 6 PC (PC 1 through 6)    
  [ ] 1 PC (PC 1 only)    
  
Other than dimension reduction, PCA is also a great tools for detecting outliers. To do that we can utilize a biplot to visualize a multidimesional dataset into a two dimensional plot. Now try to detect the outliers by passing in your `pca_coffee` in `plot.PCA()` function.  

2. Based on the visualization using biplot, which coffeee id is considered as outlier?    
  [ ] 1082, 1080, 1081    
  [ ] 1082, 993, 998    
  [ ] 1081, 308, 201    
  [ ] 1080, 1082, 998    
  
The biplot, consist of two types of biplot, if you pass in `choix` parameter when using `plot.PCA()`, you can choose either `choix="var"` or `choix="ind"` to generate a specific type of biplot. The `var` type, will give you the variables loading information within a plot. This however, is not really efficient when we are analyzing a lot of features. Some of the loading visualization (arrows), can overlapped to one another and make it harder to see.

There are of course, other method of extracting the loading information using `dimdesc()` function. Pass in our object into `dimdesc()` and try to answer the following question:
  
3. PC 1 is the most collectible PC of all variables. mention the 3 most contributing variables on PC 1!
  [ ] Aroma, Flavor, Aftertaste    
  [ ] Sweetness, Clean.cup, Uniformity    
  [ ] Balance, Flavor, Aftertaste    
  [ ] Moisture, Quakers, Clean.Cup    
  [ ] Acidity, Body, Balance     

// TODO: Create story bridging for the next question

4. Which of the following is NOT TRUE about PCA?     
  [ ] Because PCA tries to 'summarize' the covariance between variables of our data, it requires that the input variables to be scaled so they have the same range of measurement    
  [ ] A Principal Component with an eigenvalue of 0.6 is not more helpful than a Principal Component with an eigenvalue of 6.0 in terms of the variance it explains    
  [ ] We cannot fully reconstruct the original data from a PCA even if we use all the eigenvectors and eigenvalues because PCA always result in some loss of variance / information due to its dimensionality reduction process    
  
# 2. K-Means Clustering

Data clustering is a common data mining techniques to create a cluster of data that can be identify as "data with the same characteristics". To perform data clustering, you will need to remove our previously identified *outlier* using biplot on the previous step. The observation with coffeeId 1082 is a fairly extending outlier compared to the rest of the observation. Try to remove the data from our initial dataset and perform a scaling to the new data.

## 2.1 Choosing Optimum K

Next step in building a K-means clustering is to find the optimum cluster number to model our data. Use `kmeansTunning` function defined below to find the optimum K using elbow method. Use a maximum of maxK as 10 to limit the plot into 10 dinstinct cluster.

```
kmeansTunning <- function(data, maxK) {
  withinall <- NULL
  total_k <- NULL
  for (i in 2:maxK) {
    set.seed(100)
    temp <- kmeans(data,i)$tot.withinss
    withinall <- append(withinall, temp)
    total_k <- append(total_k,i)
  }
  plot(x = total_k, y = withinall, type = "o", xlab = "Number of Cluster", ylab = "Total within")
}

# kmeansTunning(your_data)

```

Based on the elbow plot generated from the function above try to answer the following question:

5. What is the optimal number of clusters ?    
  - [ ] 4    
  - [ ] 5    
  - [ ] 6   
  - [ ] 7
  
// TODO: Create story bridging for the next question

6. Which of the following is NOT TRUE about K-Means?       
  - [ ] The centroid in the first iteration is placed randomly
  - [ ] A good cluster are clusters with low `withinss` and high `betweenss`
  - [ ] Cluster with low `withinss` means the character of the data within 1 cluster are similar to each other
  - [ ] The greater the value of `betweenss`, the greater the data variance in each cluster     

## 2.2 Building Cluster

// TODO: Clue for building kmeans object and extracting the object$clust

## 2.3 Clusters Profiling

Once you are set in using the K of your choice from previous section, try to create a K-means cluster from our data. Use a `set.seed(100)` before building the model to guarantee a reproducible example.

7. For a customer who enjoy coffee with `coffeID` 929, which of the following coffee beans may be characteristically similar enough to warrant a recommendation?     
  - [ ] 1060    
  - [ ] 21    
  - [ ] 1071    
  
Recall how we can perform a cluster profiling by using a combination of `group_by()` and `summarise_all()` grouped by our previously created cluster column. After you extract the characteristics for each cluster, try to answer the following question:
  
8. which coffee cluster has the highest mean of aroma, highest mean of sweetness, and lowest mean of acidity?
  - [ ] 5, 1, 2    
  - [ ] 5, 6, 5    
  - [ ] 2, 5, 1    
  - [ ] 2, 4, 1    
