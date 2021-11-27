###### tags : `tutorial` `python`

#  A. Pandas
Pandas is a Python library used for working with data sets.

It has functions for analyzing, cleaning, exploring, and manipulating data.

The name "Pandas" has a reference to both "Panel Data", and "Python Data Analysis" and was created by Wes McKinney in 2008.


## 1. Series and Data Frame
### 1.1 Series
A Pandas Series is like a column in a table.
a. Basic Syntax
```
# Create series from a List
a = [1, 7, 2]
sr = pd.Series(a) # default label : list indexing
print(foo[0]) # 1

a = [1, 7, 2]
sr = pd.Series(a, index = ["x", "y", "z"])
print(foo["x"]) # 1

# Create Series from a Dictionary
calories = {"day1": 420, "day2": 380, "day3": 390}
sr = pd.Series(calories) # default label : dictionary key
print(sr["day1"]) # 420

sr2 = pd.Series(calories, index = ["day1", "day2"]) # take certain key-value

# Get keys and Values
sr.keys()
sr.values
```
b. Indexing and Filter
- Indexing
- 
| method | description | example |
| -------- | -------- | -------- |
| loc     | indexing base on object's label     | `sr.loc["a":"c"]`     |
| iloc     | indexing base on object's position     | `sr.loc[:2]`     |

- Filtering
```
sr[sr>2] # filter base on values
sr[['c','d']] # filter base on index
```

### 1.2 Data Frame
Data sets in Pandas are usually multi-dimensional tables, called DataFrames.

Series is like a column, a DataFrame is the whole table.

a. Generate Data Frame
- from a Dictionary
```
# Without Indexing
data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}
df = pd.DataFrame(data)
print(df.loc[0]) # access first row
print(df.loc[0:1]) # access row 1 & 2


# With Indexing
data = {
  "calories": [420, 380, 390],
  "duration": [50, 40, 45]
}

df = pd.DataFrame(data, index = ["day1", "day2", "day3"])
print(df["day_1"]) # access "day1" row
```

- from a List
```
data = [
    ['tom', 10, "male"], 
    ['nick', 15, "male"], 
    ['juli', 14, "female"]
]

df = pd.DataFrame(data, columns = ['Name', 'Age', 'sex']) 
```

- from a file
```
df = pd.read_csv('data.csv')
df = pd.read_json('data.json')
```

b. Indexing and Filtering

| Column 1 | Column 2 | Column 3 |
| -------- | -------- | -------- |
| df[<colName>]     | Operator Index     | Text     |
| df.<colName>     | Attribute Index     | Text     |
| df.loc[<colName>]     | Access df that has "colName"     | Text     |
| df.iloc[]     | Access df in certain position     | Text     |



## 2. Viewing Data
| Method | Description | 
| -------- | -------- | 
| `head()`     | get n-first dataframe     | 
| `tail()`     | get n-last dataframe     | 
| `shape`     | get dataframe's shape     | 
| `info()`     | get dataframe's information     | 
| `describe()`     | get dataframe's statistic description     | 
| `sort_values()`     | sort dataframe     | 

```
# example sort
df_sort_val = df.sort_values("age", ascending = True)
df_sort_mul = df.sort_values(["age", "sex"], ascending = [True, False])
```

## 3. Subset Data Frame

### Subset a columns
| Method | Description | 
| -------- | -------- | 
| `df[<colName>]`     | subseting df contain `<colName>`     |
| `df[[<col1>,<col2> ]]`     | subseting df contain multiple columns     |

```
age = df["age"]
age_sex = df[["age", "sex"]]

```
### Subset(Filter) a Rows
```
ageGte50 = df[df["age"]>=50]
ageGte50AndMale = df[(df["age"]>=50) & (df["isMale"]==True)]
ageGte50OrMale = df[(df["age"]>=50) | (df["isMale"]==True)]
ageInRegion12 = df[(df["region"].isin(["region1", "region2"]))]
```

## 4. Data Transformation
```
def transform(x):
    return x+10

df["val_"] = df["val"].apply(transform)
```
## 5. Reshaping
1. Pivotting
- Pandas pivot() function is used to change the DataFrame format from long to wide.
- Syntax : `df.pivot()` or `pd.pivot(df)`  
- `pivot` : can't work with duplicate data
- `pivot_table` : can apply aggregation

```
df.pivot(index, columns, values)
df.pivot_table(
    index, 
    columns, 
    values, 
    aggFunc
)   

# example
df.pivot_table(
    index="kota", 
    columns='barang', 
    values="harga", 
    aggfunc="sum"
)
    
def add10(x):
    return x+10

df.pivot_table(
    index="kota", 
    columns='barang', 
    values="harga", 
    aggfunc=add10
)
```
    
2. Melt
- melt() is the complete opposite of pivot()
- Syntax : `df.melt()` or `pd.melt(df)`
```
df.melt(
    id_vars, 
    value_vars, 
    var_name, 
    value_name
)

# example
df.melt(
    id_vars="kota", 
    value_vars=["beras", "telur"], 
    var_name="barang", 
    value_name="harga"
)
```
    
<!-- 
## 5. Cleaning Data

### 5.1 Handle Empty Values

| Column 1 | Column 2 | 
| -------- | -------- | 
| `df.dropna()`     | Remove row with empty cells     |
| `df.dropna(subset=['<col>'], inplace = True)`     | Remove row with empty cells in column <col>     |
| `df.fillna(<val>, inplace=True)`     | replace empty values with `<val>`     |
| `df.<col>.fillna(100, inplace=True)`     | replace empty values with `<val>` in column <col>     |

```
#replace empty values by median
df = pd.read_csv('data.csv')

x = df["Calories"].median()

df["Calories"].fillna(x, inplace = True)
```

### 5.2 Handle Wrong Format
- Case : Convert string date into correct format

```
# convert string into date format
df['Date'] = pd.to_datetime(df['Date'])
# delete row that has invalid date format
df.dropna(subset=['Date'], inplace = True)
```
### 5.3 Fixing Wrong Data

```
# Set Duration = 45 in row 7
df.loc[7, 'Duration'] = 45

#Loop through all values in the "Duration" column.
#If the value is higher than 120, set it to 120:
for x in df.index:
  if df.loc[x, "Duration"] > 120:
    df.loc[x, "Duration"] = 120
    
# Delete rows where "Duration" is higher than 120:
for x in df.index:
  if df.loc[x, "Duration"] > 120:
    df.drop(x, inplace = True)
```
### 5.4 Removing Duplicates
```
# find duplicate data
df.duplicated()
# Remove Duplicates
df.drop_duplicates(inplace = True)
``` -->

#  B. Matplotlib
## 1. Basic Syntax

```
# import matplotlib
import matplotlib as plt

# data
x = [0,1,2,3,4,5]
y = [0,1,4,9,16,25]

# plot data
plt.<plot_method>(x,y)

# show plot
plt.show()
```

## 2. Plot Method

| Method | Syntax | Column 3 |
| -------- | -------- | -------- |
| Line Plot     | plot(x,y)     | Text     |
| Scatter Plot     | scatter(x,y, [s:<size:number[]>,c:<color:string[]>, alpha:<color_opacity:float>])     | Text     |
| Histogram Plot     | hist(x,y, [bin:<number_bin:int>])     | Text     |

## 3. Customization
| Method | Description | Column 3 |
| -------- | -------- | -------- |
| xlabel(<xlabel:string>)     | Add label on x/y axis     | Text     |
| title(<title:string>)     | Add title     | Text     |
| xticks(<val:[]>, <label:[]>)     | Add x/y ticks     | Text     |
| grid(<grid_status:bool>)     | Enable/disable grid     | Text     |
| text(<x:val>, <y:val>, <text:string>)     | Add text on specific coordinat     | Text     |

