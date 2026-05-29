# Airbnb
## Description
## Data Cleaning - Python

Import pandas library
```python
import pandas as pd
```
Load the csv dataset to use
```python
df = pd.read_csv('Airbnb_Open_Data.csv')
```
Check the columns and their datatypes
```python
print(df.info())
```
Check if any columns contain null values
```python
print(df.isnull().any())
```
Check if there exists duplicate data entry and remove them
```python
print(df.duplicated().any())
df = df.drop_duplicates()
```
### ID
Id is an unique number representing each airbnb listing.
Check if all ids are different to each other by determining the number of unique id values and the total number of id entries. If these 2 numbers match it will mean that all id entries are unique.  
```python
print(df['id'].nunique())
print(len(df['id']))
```

### neighbourhood group
The neighbourhood group names needs to be fixed as they are not all consistent. 
```python
neighbourhood_group_map = {
    'brookln': 'Brooklyn',
    'manhatan': 'Manhattan'
}

df['neighbourhood group'] = df['neighbourhood group'].replace(neighbourhood_group_map)
```

### country & country code
Although the open dataset only contains the airbnb listings in New York US there exists null values. So we can just replace all null values with 'United States' and 'US' for the country and country code columns respectively.
```python
df['country'] = df['country'].fillna('United States')
df['country code'] = df['country code'].fillna('US')
```

### price
Since the datatype for the price and service fee columns are both string and contains the dollar sign, we will need to remove the dollar sign and convert the datatype to integer or float. 
```python
df['price'] = df['price'].str.replace(r'[^\d.]','', regex=True)
df['price'] = pd.to_numeric(df['price'])
df['service fee'] = df['service fee'].str.replace(r'[^\d.]','', regex=True)
df['service fee'] = pd.to_numeric(df['service fee'])
```

## SQL
## Data Visualisation - PowerBI
