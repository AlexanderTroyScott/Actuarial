:memo: Note: I had initially summarized the PA study material as a away to organize review material for a coworker and myself. I was surprised to learn that others were finding the material useful and it had continued to generate hits even years after I had passed the exam. Unfortunately I have not had the time to go back and make additions; therefore, I decided to copy everything over to this github repository so that it could be better maintained by the community and put a link to directing you here.

# Misc.
### Data exploration
Number of elements in Dataset - Before and after modification

Create a summary of the data
> dataset %>% summary()  or dataset %>% glimpse()

Discuss Target Variable 
Mention what the flag means and ratio the number in each class

> dataset %>% count(target_variable)

If the responses do not appear equally distributed then the classes would appear to be **imbalanced**

### Issue Resolution

Some candidates may find it easier to manipulate the data in Excel and then import the adjusted file into R. 
*Note: Many excel features, such as Pivot Tables, are disabled which prevents Excel being a good tool for Data Exploration*

Delete Values
Subset using set operators
> dataset <- dataset[dataset$variable!=0,] 

Replace Character Variables with Factors
If any show character as a class replace them with factors:
> dataset <- dataset %>% modify_if(is.character, as.factor) 
Alternatively, you can convert characters to releveled factors in one step:
> dataset <- dataset %>% mutate_if(is.character, fct_infreq)

### Pre-Modeling

**Level Reduction**
Consider both **n** and **mean** of the target variable before combining groups.
> dataset <- dataset %>% mutate(variable_bucket = case_when(variable < 50 ~ 0,variable <= 70 ~ 1,variable > 70 ~ 2))

**Set Reference Levels**

This **does not** effect predictions nor any measures of model fit

This *does* effect decisions if hypothesis tests are conducted to consider removing specific factor levels.
    * This is because the test compares each factor level to the base level

Explicitly set a reference level - If you want to be testing other variables against one in particular
> dataset <- relevel(dataset$variable, ref = "newBaseLevel")

Set a reference level to have the most observations - If there are no obvious choices
Displays the number of observations at each level
> dataset$column %>% as.factor() %>% summary() 
Set the highest frequency "column" to be the base level (Tidyverse Required)
> dataset <- dataset %>% mutate(column = fct_infreq(column))

**Train/Test Datasets**
Verify the mean of the target variable is similar between training and testing datasets

### Decision Trees
### General Linear Models

**Regularized Regression (Penalized Regression)**
Standardize units - Coefficients are penalized the larger they are; therefore, if a variable is measuring Units consider changing to Dollars. 

### Post-Modeling
Confusion Matrices
* Sensitivity - True Positive Rate = True Positives / (True Positives + False Negatives)
* Specificity - True Negative Rate = True Negatives / (False Positives + True Negatives)
* Precision - True Positives / (True Positives + False Positives)
* Recall - Sensitivity

Predictions
Including response will adjust the output to be probabilities; otherwise, the output will be curtailed to the specified distribution.
> sample.data %>% mutate(predicted_profit = predict(glm,sample.data,type="response"))

### Useful Links
http://uc-r.github.io/predictive 

https://exampa.net/study-guide/

https://www.casact.org/pubs/monographs/papers/05-Goldburd-Khare-Tevet.pdf

# 6. Generalized Linear Models

##### a) Implement ordinary least squares regression in R and understand model assumptions.
[![Alt text](https://img.youtube.com/vi/PaFPbb66DxQ/0.jpg)](https://www.youtube.com/watch?v=PaFPbb66DxQ)

[![Alt text](https://img.youtube.com/vi/nk2CQITm_eo/0.jpg)](https://www.youtube.com/watch?v=nk2CQITm_eo)

[![Alt text](https://img.youtube.com/vi/u1cc1r_Y7M0/0.jpg)](https://www.youtube.com/watch?v=u1cc1r_Y7M0)

##### b) Understand the specifications of the GLM and the model assumptions. 
1. Linear Regression (Ordinary Least Squares Regression)
2. Logistic Regression
3. Regularized Regression 
    * Ridge
    * Lasso
    * Elastic Net

###### Logistic Regression

[![Alt text](https://img.youtube.com/vi/yIYKR4sgzI8/0.jpg)](https://www.youtube.com/watch?v=yIYKR4sgzI8)

[![Alt text](https://img.youtube.com/vi/vN5cNN2-HWE/0.jpg)](https://www.youtube.com/watch?v=vN5cNN2-HWE)

[![Alt text](https://img.youtube.com/vi/BfKanl1aSG0/0.jpg)](https://www.youtube.com/watch?v=BfKanl1aSG0)

[![Alt text](https://img.youtube.com/vi/xxFYro8QuXA/0.jpg)](https://www.youtube.com/watch?v=xxFYro8QuXA)

[![Alt text](https://img.youtube.com/vi/9T0wlKdew6I/0.jpg)](https://www.youtube.com/watch?v=9T0wlKdew6I)

[![Alt text](https://img.youtube.com/vi/JC56jS2gVUE/0.jpg)](https://www.youtube.com/watch?v=JC56jS2gVUE)

[![Alt text](https://img.youtube.com/vi/C4N3_XJJ-jU/0.jpg)](https://www.youtube.com/watch?v=C4N3_XJJ-jU)

###### Regularized Regression

[![Alt text](https://img.youtube.com/vi/Q81RR3yKn30/0.jpg)](https://www.youtube.com/watch?v=Q81RR3yKn30)

[![Alt text](https://img.youtube.com/vi/NGf0voTMlcs/0.jpg)](https://www.youtube.com/watch?v=NGf0voTMlcs)

[![Alt text](https://img.youtube.com/vi/1dKRdX9bfIo/0.jpg)](https://www.youtube.com/watch?v=1dKRdX9bfIo)

[![Alt text](https://img.youtube.com/vi/ctmNq7FgbvI/0.jpg)](https://www.youtube.com/watch?v=ctmNq7FgbvI)

###### Regularized Regression

##### c) Create new features appropriate for GLMs. 



##### d) Interpret model coefficients, interaction terms, offsets, and weights. 

See casact article

##### e) Select and validate a GLM appropriately. 

[![Alt text](https://img.youtube.com/vi/fSytzGwwBVw/0.jpg)](https://www.youtube.com/watch?v=fSytzGwwBVw)

[![Alt text](https://img.youtube.com/vi/Kdsp6soqA7o/0.jpg)](https://www.youtube.com/watch?v=Kdsp6soqA7o)

[![Alt text](https://img.youtube.com/vi/vP06aMoz4v8/0.jpg)](https://www.youtube.com/watch?v=vP06aMoz4v8)

[![Alt text](https://img.youtube.com/vi/4jRBRDbJemM/0.jpg)](https://www.youtube.com/watch?v=4jRBRDbJemM)

[![Alt text](https://img.youtube.com/vi/qcvAqAH60Yw/0.jpg)](https://www.youtube.com/watch?v=qcvAqAH60Yw)

##### f) Explain the concepts of bias, variance, model complexity, and the bias-variance trade-off. 

The more fit the model is to the training data, the less bias there will be; however, this tends to result in more variance in the testing data.

**Overfitting** - "Overfitting" to the training data resulting in **low bias, but high variance**

**Underfitting** - "Underfitting" to the training data resulting in **high bias, but low variance**

[![Alt text](https://img.youtube.com/vi/EuBBz3bI-aA/0.jpg)](https://www.youtube.com/watch?v=EuBBz3bI-aA)

##### g) Select appropriate hyperparameters for regularized regression 

# 7. Decision Trees 

## a) Understand the basic motivation behind decision trees. 

[![Alt text](https://img.youtube.com/vi/7VeUPuFGJHk/0.jpg)](https://www.youtube.com/watch?v=7VeUPuFGJHk)

[![Alt text](https://img.youtube.com/vi/wpNl-JwwplA/0.jpg)](https://www.youtube.com/watch?v=wpNl-JwwplA)

## b) Construct regression and classification trees. 

[![Alt text](https://img.youtube.com/vi/g9c66TUylZ4/0.jpg)](https://www.youtube.com/watch?v=g9c66TUylZ4)

[![Alt text](https://img.youtube.com/vi/D0efHEJsfHo/0.jpg)](https://www.youtube.com/watch?v=D0efHEJsfHo)

## c) Use bagging and random forests to improve accuracy. 

[![Alt text](https://img.youtube.com/vi/J4Wdy0Wc_xQ/0.jpg)](https://www.youtube.com/watch?v=J4Wdy0Wc_xQ)

[![Alt text](https://img.youtube.com/vi/nyxTdL_4Q-Q/0.jpg)](https://www.youtube.com/watch?v=nyxTdL_4Q-Q)

[![Alt text](https://img.youtube.com/vi/6EXPYzbfLCE/0.jpg)](https://www.youtube.com/watch?v=6EXPYzbfLCE)

## d) Use boosting to improve accuracy. 

[![Alt text](https://img.youtube.com/vi/LsK-xG1cLYA/0.jpg)](https://www.youtube.com/watch?v=LsK-xG1cLYA)

[![Alt text](https://img.youtube.com/vi/3CC4N4z3GJc/0.jpg)](https://www.youtube.com/watch?v=3CC4N4z3GJc)

[![Alt text](https://img.youtube.com/vi/2xudPOBz-vs/0.jpg)](https://www.youtube.com/watch?v=2xudPOBz-vs)

[![Alt text](https://img.youtube.com/vi/jxuNLH5dXCs/0.jpg)](https://www.youtube.com/watch?v=jxuNLH5dXCs)

[![Alt text](https://img.youtube.com/vi/StWY5QWMXCw/0.jpg)](https://www.youtube.com/watch?v=StWY5QWMXCw)

## e) Select appropriate hyperparameters for decision trees and related techniques. 

**Random Forest Hyperparameters**
1. Impurity measure - In most cases there is not much difference between selecting one method over the other. 
    * Gini - Default
    * Entropy - More computationally intensive since it uses the logarithmic function
2. Splitter - How a split is determined at each node. 
    * Best - Default - chooses the one based on the impurity measures and is computationally intensive
    * Random - Chooses a random feature and generally ends up with longer and less precise trees, but can reduce overfitting
3. Max_Depth - Controlling this is the main way to combat overfitting
    * None - Default
4. ntree - Number of trees in the forest
5. mtry - Number of variables compared in the trees

**GBM Hyperparameters**

# 8. Cluster and Principal Component Analyses

## a) Understand and apply K-means clustering. 

**Summary of K-means clustering**
1. Pick k points randomly, these are the clusters
2. Group each other points to the nearest cluster
3. Calculate mean of each cluster
4. Repeat steps 2 and 3 until the mean does not move
--- Repeat Steps 1-4 ----
5. The result of each repitition are compared based on the *variance* in the distance between each observation and the cluster mean. The clustering with the **smallest variance** is the best clustering for a given *k*.

The higher *k* is, the lower the total variance will be. The ideal *k* would tend to be when there is less reduction in variance by the addition of additional clusters. This is graphically shown in a elbow plot.  

**K-means vs hierarchical clustering**

[![Alt text](https://img.youtube.com/vi/4b5d3muPQmA/0.jpg)](https://www.youtube.com/watch?v=4b5d3muPQmA)

## b) Understand and apply hierarchical clustering.

Start with one observation and find the most similar one to it, then repeat for all observations, the most similar observations become the first cluster. Repeat, but treat the first cluster as a combined unit and use it to compare. Keep repeating until there is only one cluster.

Dendrograms show similarities and the order which clusters were formed.

Similarity needs to be defined:
* Commonly Euclidean Distance. 

> ?dist - Can show other methods along with calculations

Compare also needs to be defined:
* Centroid - Average of each cluster
    * "Ward" - Like centroid, but also takes into account the variance within each cluster
* Single-linkage - closest point in the cluster
* Complete-linkage - furthest point in each cluster

> ?hclust - Can show other methods, but knowing the above helps significantly

Hierarchical clustering can be agglomerative (bottomup) or divisive (top-down) and they should give similar results. K-means clustering can simulate the divisive technique and is computationally much faster.

Pro:
* Shows all possible linkages between clusters
* Understand how much clusters differ based on dendrogram length
* No hyperparameters, the analyst can select the appropriate number of clusters for the business need 
* Many methods to test and select which fits data best

Con:
* scalability, increasing observations will prevent interpretation
* computationally intensive

[![Alt text](https://img.youtube.com/vi/7xHsRkOdVwo/0.jpg)](https://www.youtube.com/watch?v=7xHsRkOdVwo)

## c) Understand and apply principal component analysis. 

**Summary of PCA Method**
1. Two variables are graphically compared
2. The average point is then calculated and plotted
3. The graph is shifted so that this average point is at the origin
4. PCA finds the best fitting line by **maximizing the sum of the squared distances from the projected points to the origin**
    * This is computationally easier than finding the minimum distances between each point and the line
    * Sum of squared distances are also called "eingenvalues"
5. This is repeated for all variables
6. Line with the largest eigenvalue becomes PC1

[![Alt text](https://img.youtube.com/vi/0Jp4gsfOLMs/0.jpg)](https://www.youtube.com/watch?v=0Jp4gsfOLMs)
