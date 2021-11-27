###### tags : `tutorial` `machine learning` `python`

# Machine Learning Cheat Sheet

## 1. Preprocessing
### 1.1 Model Selection

```
from sklearn.model_selection import train_test_split

# Split data with 80% train data, 20% test 
X_train, X_test, y_train, y_test = train_test_split(
    X, 
    y, 
    # 
    test_size=<test_size_val:float>,
    # set it if you want to generate pseudorandom
    random_state = <seed:int>  
)

#evaluate model
model.score(X_test, y_test)
```
### 1.2 Convert Categorical into Number
#### a. Pandas Dummy Variables

```
dummies = pd.get_dummies(<df["choosen_column"]>)
merged = pd.concat([df, dummies], axis='columns')
```
- get_dummies will create n columns. For instance if we generate dummies variabel for sex, it will generate 2 columns: male and female. The male person will have a value like this : male : 1, female: 0.   
- It also necessary to remove a column to simplify a datafame. For example we can remove male or female feature. 


#### b. Sklearn Label Encoder
```
from sklearn.preprocessing import LabelEncoder, OneHotEncoder

le = LabelEncoder()

# convert male, female into : 0 or 1
sex_encoded = le.fit_transform(df.sex)
# array([0, 0, 0, 0, 0, 1, 1, 1, 1], dtype=int64)

# rehsape array
sex_encoded = sex_encoded.reshape(-1,1)

# convert 0,1 into 2 columns
ohe = OneHotEncoder(sparse=False)
sex_ohe = ohe.fit_transform(sex_encoded)
# array([[1., 0.],
#       [1., 0.],
#       [1., 0.],
#       [1., 0.],
#       [1., 0.],
#       [0., 1.],
#       [0., 1.],
#       [0., 1.],
#       [0., 1.]])
```

### 1.3 Normalization
```
import numpy as np
from sklearn.preprocessing import MinMaxScaler

scaler = MinMaxScaler()
scaler.fit(df[['Income']])
df['Income'] = scaler.transform(df[['Income']]))

```

## 2. Supervised Learning
### 2.1 Linear Regression

Linear regression uses the relationship between the data-points to draw a straight line through all them. This line can be used to predict future values.

![](https://i.imgur.com/aadHcgi.png)

```
from sklearn.linear_model import LinearRegression

model = LinearRegression()
model.fit(df.X, df.y)
model.predict(df.X_test)

# Get model coef
model.coef_ 
# Get model y-axis interception
model.intercept_


```

### 2.2 Logistic Regression

Logistic regression is a classification algorithm, used when the value of the target variable is categorical in nature. Logistic regression is most commonly used when the data in question has binary output, so when it belongs to one class or another, or is either a 0 or 1.

![](https://i.imgur.com/ajD4vT6.jpg)

```
from sklearn.linear_model import LogisticRegression

model = LogisticRegression()
model.fit(df.X, df.y)
model.predict(df.X_test)

# Get model coef?
model.coef_ 
# Get model y-axis interception?
model.intercept_

```

### 2.3 Polinomial Regression

```
from sklearn.preprocessing import PolynomialFeatures
from sklearn.linear_model import LinearRegression

poly_reg = PolynomialFeatures(degree=2)
X_poly = poly_reg.fit_transform(X_train)

model = LinearRegression()  
model.fit(X_poly, y_train)

```

### 2.4 Support Vector Machine


### 2.5 Naive Bayes
### 2.6 Decision Tree

A decision tree is a tree where each node represents a feature(attribute), each link(branch) represents a decision(rule) and each leaf represents an outcome(categorical or continues value)


### 2.7 K-nearest neighbour

```
from sklearn.neighbour import KNeighborsClassifier

KNN = KNeighborsClassifier()
KNN.fit(X_train, y_train)

pred = KNN.predict(X_test)
```




## 3. Unsupervised Learning

### 3.1 Kmeans Clustering

k-means clustering is a method of vector quantization, originally from signal processing, that is popular for cluster analysis in data mining. k-means clustering aims to partition n observations into k clusters in which each observation belongs to the cluster with the nearest mean, serving as a prototype of the cluster

#### a. Create a Cluster
```
from sklearn.cluster import KMeans

km = KMeans(n_cluster=3)
df['cluster'] = km.fit_predict(df[['Age', 'Income']])

# get array center of cluster
km.cluster_centers_
```

#### b. Evaluate Cluster
- Elbow Method
```

sse = [] # square error
clusters = [i for i in range(n_cluster)]
for k in clusters:
  km = KMenas(n_clusters=k)
  km.fit(df[['Age', 'Income']])
  sse.append(km.inertia_)

plt.plot(clusters, sse)
```
- Silhoutte Method


### 3.2 Hierarchical Clustering
### 3.3 DBSCAN
### 3.4 Fuzzy C-Means

## 4. Model Evaluation
### 4.1 Use score method
Mostly the model already has a score method to verify used algorithm is good enough for predicting data. The value between 0 and 1. The higher the score, the better result. 

```
model.score(X_test, y_tes)

```

### 4.2 K Fold Cross Validation
```
from sklearn.model_selection import cross_val_score

scores = cross_val_score(LogisticRegression(), df.X, df.y)
print(scores.mean())
```

### 4.3 Confussion Matrix
```
from sklearn.metrics import confussion_matrix
import seaborn as sns

cm = confussion_matrix(y_test, y_predicted)
sns.heatmap(cm, annot=True)
plt.xlabel('Predicted')
plt.ylabel('Truth')

```
