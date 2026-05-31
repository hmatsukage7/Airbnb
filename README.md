# Airbnb
## Description
## Data Cleaning - Python

- Import pandas library
```python
import pandas as pd
```
- Load the csv dataset to use
```python
df = pd.read_csv('Airbnb_Open_Data.csv')
```
- Check the columns and their datatypes
```python
print(df.dtypes)
```
<p align=center>
<img src=https://i.imgur.com/LuJYxnC.png width=30%>

`We can see that the price and service fee should display monetary value however the data type is shown as string for both. This will be fixed later on.`

- The column names are not consistently formatted as only some starts with capital letters and some contains space instead of underscores. We will fix this by making all the column names lower case and replace the space with underscore. 

```python
print(f"Before fix: {df.columns}\n")
df.columns = df.columns.str.lower().str.replace(' ', '_')
print(f"After fix: {df.columns}")
```
<p align=center>
<img src=https://i.imgur.com/Y3LLAlo.png width=60%>

- Check if any columns contain null values
```python
print(df.isnull().any())
```

- Checking for duplicated rows and removing them
```python
print(f"Before removing duplicates: {df.duplicated().any()}")
df = df.drop_duplicates()
print(f"After removing duplicates: {df.duplicated().any()}")
```
<p align=center>
<img src=https://i.imgur.com/w8oj0ov.png>
 
### ID
Id is an unique number representing each airbnb listing.
Check if all ids are different to each other by determining the number of unique id values and the total number of id entries. If these 2 numbers match it will mean that all id entries are unique. 
```python
print(f"Total unique ids: {df['id'].nunique()}")
print(f"Total number of ids:{len(df['id'])}")
```
<p align=center>
<img src=https://i.imgur.com/6614j1B.png>

`Before removing the duplicated rows in the previous step, the total number of ids and the number of unique ids did not match`

### neighbourhood group
The neighbourhood group names needs to be fixed as they are not all consistent. 

```python
print(f"Before fix: {df['neighbourhood_group'].unique()}\n")

neighbourhood_group_map = {
    'brookln': 'Brooklyn',
    'manhatan': 'Manhattan'
}

df['neighbourhood_group'] = df['neighbourhood_group'].replace(neighbourhood_group_map)

print(f"After fix: {df['neighbourhood_group'].unique()}")
```
<p align=center>
<img src=https://i.imgur.com/7HPCDNk.png>

### country & country code
Although the open dataset only contains the airbnb listings in New York US there exists null values. So we can just replace all null values with 'United States' and 'US' for the country and country code columns respectively.
```python
print(f"country before fix: {df['country'].unique()}\n")
df['country'] = df['country'].fillna('United States')
print(f"country after fix: {df['country'].unique()}")

print(f"country_code before fix: {df['country_code'].unique()}\n")
df['country_code'] = df['country_code'].fillna('US')
print(f"country_code after fix: {df['country_code'].unique()}")
```
<p align=center>
<img src=https://i.imgur.com/WxkRxvS.png width=40%>
<p align=center>
<img src=https://i.imgur.com/FsCgfPx.png width=40%>

### construction year
convert from float to integer

### price
Since the datatype for the price and service fee columns are both string and contains the dollar sign, we will need to remove the dollar sign and convert the datatype to integer or float. 
```python
print(f"price before fix: \n{df['price'].head()}\n")
df['price'] = df['price'].str.replace(r'[^\d.]','', regex=True)
df['price'] = pd.to_numeric(df['price'])
print(f"price after fix: \n{df['price'].head()}")

print(f"service_fee before fix: \n{df['service_fee'].head()}\n")
df['service_fee'] = df['service_fee'].str.replace(r'[^\d.]','', regex=True)
df['service_fee'] = pd.to_numeric(df['service_fee'])
print(f"service_fee after fix: \n{df['service_fee'].head()}")
```
<p align=center>
<img src=https://i.imgur.com/qwdqTzn.png width=30%>
<p align=center>
<img src=https://i.imgur.com/3jLIowS.png width=30%>

### minimum nights, number of reviews, review rate number, calculated host listings and availability 365
Fix from float to integer

    
## SQL
## Data Visualisation - PowerBI
