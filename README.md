# Zomato-Data-Analysis

## Project Overview

**Project Title**: Zomato Data Analysis

## Project Structure

### 1. Importing Libraries
pandas is used for data manipulation and analysis, numpy is used for numerical operations ,matplotlib.pyplot and seaborn are used for data visualisation

```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

### 2. Create the data frame

```
dataframe = pd.read_csv("Zomato data .csv")
print(dataframe)
```

### 3.Convert the data type of column - rate
The values in rate column are as (for example 4.1/5) so we have to remove the /5 so we will get only the rating i.e a float value 

```
def handleRate(value):
    value = str(value).split('/')
    value = value[0];
    return float(value)

dataframe['rate'] = dataframe['rate'].apply(handleRate)
print(dataframe.head())
```

### 4. Check for any Null Value

```
dataframe.info()
```

### Data Analysis & Findings

1. **Which type of restaurant do the majority of customers order from ?**:
```
dataframe.head()
sns.countplot(x=dataframe['listed_in(type)'])
plt.xlabel("type of restaurant")
```
  **Answer: Majority of the restaurant falls in DINING category**
  

2. **How many votes has each type of restaurant received from customers ?**
```
dataframe.head()
grouped_data = dataframe.groupby('listed_in(type)')['votes'].sum()
result = pd.DataFrame({'votes': grouped_data})
plt.plot(result, c = "green", marker = "o")
plt.xlabel("Type of restaurant", c = "red", size = 20)
plt.ylabel("Votes", c = "red", size = 20)
```
  **Answer: DINING restaurant has recieved maximum votes**
  

3. **What are the ratings that the majority of restaurants have received ?**
```
dataframe.head()
plt.hist(dataframe['rate'],bins = 4)
plt.title("ratings distribution")
plt.show()
```
  **Answer: The majority restaurants recieved ratings from 3.5 to 4**
  

4. **Zomato has observed that most couples order most of their food online. What is the average spending on each other ?**
```
dataframe.head()
couple_data = dataframe['approx_cost(for two people)']
sns.countplot(x = couple_data)
```
**Answer: The majority of Couples prefer restaurants with an approximate cost of 300 RS.**

5. **Which mode (online or offline) has received the maximum rating ?**
```
dataframe.head()
plt.figure(figsize = (6,6))
sns.boxplot(x = 'online_order', y = 'rate', data = dataframe)
```
**Answer: Offline order recieved Lower ratings Compared to Online order.**

6. **Which type of Restaurant recieved more offline orders, So that Zomato can provide customers with some good offers**
```
dataframe.head()
pivot_table = dataframe.pivot_table(index = 'listed_in(type)', columns = 'online_order', aggfunc = 'size', fill_value = 0)
sns.heatmap(pivot_table, annot = True, cmap = "YlGnBu", fmt = 'd')
plt.title("Heatmap")
plt.xlabel("Online Order")
plt.ylabel("Listed in (Type)")
plt.show()
```
**Answer: DINING restaurants primarily accept Offline orders. Whereas CAFES primarily receive Online orders.**

## Author - SAKILI AJAY
This project is part of my portfolio


