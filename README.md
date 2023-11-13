# Ex-08-Data-Visualization-
# AIM
To Perform Data Visualization on a complex dataset and save the data to a file.

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
## STEP 1
Read the given Data

## STEP 2
Clean the Data Set using Data Cleaning Process

## STEP 3
Apply Feature generation and selection techniques to all the features of the data set

## STEP 4
Apply data visualization techniques to identify the patterns of the data.

# CODE
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
from google.colab import files
uploaded = files.upload()
df=pd.read_csv("SuperStore.csv",encoding='unicode_escape')
df
```
<img width="574" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/9490e216-c4fe-416b-a747-95c535e6917a">

```
df.isnull().sum()
```

<img width="191" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/18de36c6-05fc-425e-80df-1d7b5923645c">

```
df.drop('Row ID',axis=1,inplace=True)
df.drop('Order ID',axis=1,inplace=True)
df.drop('Customer ID',axis=1,inplace=True)
df.drop('Customer Name',axis=1,inplace=True)
df.drop('Country',axis=1,inplace=True)
df.drop('Postal Code',axis=1,inplace=True)
df.drop('Product ID',axis=1,inplace=True)
df.drop('Product Name',axis=1,inplace=True)
df.drop('Order Date',axis=1,inplace=True)
df.drop('Ship Date',axis=1,inplace=True)
print("Updated dataset")
df
```

<img width="571" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/7944c9f6-3326-41e9-b1e7-d0bbc88d495e">

```
#detecting and removing outliers in current numeric data
plt.figure(figsize=(8,8))
plt.title("Data with outliers")
df.boxplot()
plt.show()
```
<img width="415" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/0ea30f8a-3119-40ff-a38b-344406ec680d">

```
plt.figure(figsize=(8,8))
cols = ['Sales','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```
<img width="431" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/9795e16d-194c-45f2-8e82-4760a0ee9863">

# Which Segment has Highest sales?
```
sns.lineplot(x="Segment",y="Sales",data=df,marker='o')
plt.title("Segment vs Sales")
plt.xticks(rotation = 90)
plt.show()
```

<img width="513" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/7a4c3972-2758-42da-999c-2138d229c706">
```
sns.barplot(x="Segment",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```

<img width="509" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/f7c2a67a-a643-4585-bb66-c6848603f72a">


# Which City has Highest profit?

```
df.shape
df1 = df[(df.Profit >= 60)]
df1.shape
```

<img width="90" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/fc5cd50b-2237-456e-9524-dc6a4985f2c2">


```
plt.figure(figsize=(30,8))
states=df1.loc[:,["City","Profit"]]
states=states.groupby(by=["City"]).sum().sort_values(by="Profit")
sns.barplot(x=states.index,y="Profit",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("City")
plt.ylabel=("Profit")
plt.show()
```

<img width="569" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/1662b498-7696-4713-b99c-4b88e5d9d2c7">

# Which ship mode is profitable?
```
sns.barplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```

<img width="484" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/57973bea-a362-430a-978f-bccca66d65cb">

```
sns.lineplot(x="Ship Mode",y="Profit",data=df)
plt.show()
```
<img width="524" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/855593e9-e22a-4a65-90de-a9cf47eaebbe">


sns.violinplot(x="Profit",y="Ship Mode",data=df)

<img width="530" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/cc59aa29-9691-400d-ada5-0501d5cf2f24">


sns.pointplot(x=df["Profit"],y=df["Ship Mode"])


<img width="548" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/705df777-4f52-4c43-aebf-4b3361768a4c">


# Sales of the product based on region.

```
states=df.loc[:,["Region","Sales"]]
states=states.groupby(by=["Region"]).sum().sort_values(by="Sales")
sns.barplot(x=states.index,y="Sales",data=states)
plt.xticks(rotation = 90)
plt.xlabel=("Region")
plt.ylabel=("Sales")
plt.show()
```

<img width="500" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/58e97a4b-d077-46c9-bf0b-e07ca1154661">
```
df.groupby(['Region']).sum().plot(kind='pie', y='Sales',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
```

<img width="572" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/da8a4dbe-785d-4ec9-999a-f1765fc5224b">


# Find the relation between sales and profit.

```
df["Sales"].corr(df["Profit"])
```

<img width="145" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/16a2f394-5b14-4f3a-981c-4318b511c916">

```
df_corr = df.copy()
df_corr = df_corr[["Sales","Profit"]]
df_corr.corr()
```
<img width="229" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/f916e756-b755-4d79-93d9-771390b08818">

```
sns.pairplot(df_corr, kind="scatter")
plt.show()
```

<img width="434" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/f3f67ba3-f56c-45c9-ab64-dddd08be4a12">


# Heatmap

```
df4=df.copy()

#encoding
from sklearn.preprocessing import LabelEncoder,OrdinalEncoder,OneHotEncoder
le=LabelEncoder()
ohe=OneHotEncoder
oe=OrdinalEncoder()

df4["Ship Mode"]=oe.fit_transform(df[["Ship Mode"]])
df4["Segment"]=oe.fit_transform(df[["Segment"]])
df4["City"]=le.fit_transform(df[["City"]])
df4["State"]=le.fit_transform(df[["State"]])
df4['Region'] = oe.fit_transform(df[['Region']])
df4["Category"]=oe.fit_transform(df[["Category"]])
df4["Sub-Category"]=le.fit_transform(df[["Sub-Category"]])

#scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])

#Heatmap
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```


<img width="572" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/e8dc4869-b30c-4260-93b7-a0f4c628b15c">


# Find the relation between sales and profit based on the following category.
# Segment
```
grouped_data = df.groupby('Segment')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```

<img width="490" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/ea584914-7349-4425-9375-e20e77b368ea">


# City

```
grouped_data = df.groupby('City')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('City')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
<img width="503" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/f53f342a-17e0-4973-af3e-e30c46ef396c">

# States

```
grouped_data = df.groupby('State')[['Sales', 'Profit']].mean()
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
ax.bar(grouped_data.index, grouped_data['Sales'], label='Sales')
ax.bar(grouped_data.index, grouped_data['Profit'], bottom=grouped_data['Sales'], label='Profit')
ax.set_xlabel('State')
ax.set_ylabel('Value')
ax.legend()
plt.show()
```
<img width="529" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/c3e54a3d-f1cc-4851-bc10-3dfd37ebc153">


# Segment and Ship Mode

```
grouped_data = df.groupby(['Segment', 'Ship Mode'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index='Segment', columns='Ship Mode', values=['Sales', 'Profit'])
# Create a bar chart of the grouped data
fig, ax = plt.subplots()
pivot_data.plot(kind='bar', ax=ax)
ax.set_xlabel('Segment')
ax.set_ylabel('Value')
plt.legend(title='Ship Mode')
plt.show()
```
<img width="491" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/ac705227-8b1c-4122-b5e2-aec9d7e59fb7">


# Segment, Ship mode and Region
```
grouped_data = df.groupby(['Segment', 'Ship Mode','Region'])[['Sales', 'Profit']].mean()
pivot_data = grouped_data.reset_index().pivot(index=['Segment', 'Ship Mode'], columns='Region', values=['Sales', 'Profit'])
sns.set_style("whitegrid")
sns.set_palette("Set1")
pivot_data.plot(kind='bar', stacked=True, figsize=(10, 5))
plt.xlabel('Segment-Ship Mode')
plt.ylabel('Value')
plt.legend(title='Region')
plt.show()
```
<img width="553" alt="image" src="https://github.com/Vineesha29031970/ODD2023-Datascience-Ex-08/assets/133136880/b497841d-91a5-49a6-8b6d-60d88ea19e07">

# RESULT:
Thus, Data Visualization is performed on the given dataset and save the data to a file.
