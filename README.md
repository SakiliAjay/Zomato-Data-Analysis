# Zomato-Data-Analysis

## Project Overview

**Project Title**: Zomato Data Analysis

## Project Structure

### 1. Importing Libraries
pandas is used for data manipulation and analysis
numpy is used for numerical operations
matplotlib.pyplot and seaborn are used for data visualisation

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
  **Conclusion: Majority of the restaurant falls in DINING category**

2. **How many votes has each type of restaurant received from customers ?**
```
dataframe.head()
grouped_data = dataframe.groupby('listed_in(type)')['votes'].sum()
result = pd.DataFrame({'votes': grouped_data})
plt.plot(result, c = "green", marker = "o")
plt.xlabel("Type of restaurant", c = "red", size = 20)
plt.ylabel("Votes", c = "red", size = 20)
```
  **Conclusion: DINING restaurant has recieved maximum votes**

3. **What are the ratings that the majority of restaurants have received ?**
```
dataframe.head()
plt.hist(dataframe['rate'],bins = 4)
plt.title("ratings distribution")
plt.show()
```
  **Conclusion: The majority restaurants recieved ratings from 3.5 to 4**

4. 






