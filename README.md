# Ex-08-Data-Visualization-

## AIM
To Perform Data Visualization on a complex dataset and save the data to a file. 

# Explanation
Data visualization is the graphical representation of information and data. By using visual elements like charts, graphs, and maps, data visualization tools provide an accessible way to see and understand trends, outliers, and patterns in data.

# ALGORITHM
### STEP 1
Read the given Data
### STEP 2
Clean the Data Set using Data Cleaning Process
### STEP 3
Apply Feature generation and selection techniques to all the features of the data set
### STEP 4
Apply data visualization techniques to identify the patterns of the data.
# PROGRAM:
Developed by: Thanika sree B
Register no: 212222100055

# CODE
# loading the dataset
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
df=pd.read_csv("Superstore.csv")
df
```
# removing unnecessary data variables
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

df.isnull().sum()
```

# detecting and removing outliers in current numeric data
```
plt.figure(figsize=(12,10))
plt.title("Data with outliers")
df.boxplot()
plt.show()

plt.figure(figsize=(12,10))
cols = ['Sales','Quantity','Discount','Profit']
Q1 = df[cols].quantile(0.25)
Q3 = df[cols].quantile(0.75)
IQR = Q3 - Q1
df = df[~((df[cols] < (Q1 - 1.5 * IQR)) |(df[cols] > (Q3 + 1.5 * IQR))).any(axis=1)]
plt.title("Dataset after removing outliers")
df.boxplot()
plt.show()
```

# data visualization
# line plots
# import seaborn as sns
```
sns.lineplot(x="Sub-Category",y="Sales",data=df,marker='o')
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.lineplot(x="Category",y="Profit",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Categories vs Profit")
plt.show()

sns.lineplot(x="Region",y="Sales",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Region area vs Sales")
plt.show()

sns.lineplot(x="Category",y="Discount",data=df,marker='o')
plt.title("Categories vs Discount")
plt.show()

sns.lineplot(x="Sub-Category",y="Quantity",data=df,marker='o')
plt.xticks(rotation = 90)
plt.title("Sub Categories vs Quantity")
plt.show()
## bar plots
sns.barplot(x="Sub-Category",y="Sales",data=df)
plt.title("Sub Categories vs Sales")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Profit",data=df)
plt.title("Categories vs Profit")
plt.show()

sns.barplot(x="Sub-Category",y="Quantity",data=df)
plt.title("Sub Categories vs Quantity")
plt.xticks(rotation = 90)
plt.show()

sns.barplot(x="Category",y="Discount",data=df)
plt.title("Categories vs Discount")
plt.show()

plt.figure(figsize=(12,7))
sns.barplot(x="State",y="Sales",data=df)
plt.title("States vs Sales")
plt.xticks(rotation = 90)
plt.show()

plt.figure(figsize=(25,8))
sns.barplot(x="State",y="Sales",hue="Region",data=df)
plt.title("State vs Sales based on Region")
plt.xticks(rotation = 90)
plt.show()
```
# Histogram
```
sns.histplot(data = df,x = 'Region',hue='Ship Mode')
sns.histplot(data = df,x = 'Category',hue='Quantity')
sns.histplot(data = df,x = 'Sub-Category',hue='Category')
plt.xticks(rotation = 90)
plt.show()
sns.histplot(data = df,x = 'Quantity',hue='Segment')
plt.hist(data = df,x = 'Profit')
plt.show()
```

# count plot
```
plt.figure(figsize=(10,7))
sns.countplot(x ='Segment', data = df,hue = 'Sub-Category')
sns.countplot(x ='Region', data = df,hue = 'Segment')
sns.countplot(x ='Category', data = df,hue='Discount')
sns.countplot(x ='Ship Mode', data = df,hue = 'Quantity')
```

# Barplot
```
sns.boxplot(x="Sub-Category",y="Discount",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot( x="Profit", y="Category",data=df)
plt.xticks(rotation = 90)
plt.show()
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Profit",data=df)
sns.boxplot(x="Region",y="Sales",data=df)
plt.figure(figsize=(10,7))
sns.boxplot(x="Sub-Category",y="Quantity",data=df)
plt.xticks(rotation = 90)
plt.show()
sns.boxplot(x="Category",y="Discount",data=df)
plt.figure(figsize=(15,7))
sns.boxplot(x="State",y="Sales",data=df)
plt.xticks(rotation = 90)
plt.show()
```
# KDE plot
```
sns.kdeplot(x="Profit", data = df,hue='Category')
sns.kdeplot(x="Sales", data = df,hue='Region')
sns.kdeplot(x="Quantity", data = df,hue='Segment')
sns.kdeplot(x="Discount", data = df,hue='Segment')
```
# violin plot
```
sns.violinplot(x="Profit",data=df)
sns.violinplot(x="Discount",y="Ship Mode",data=df)
sns.violinplot(x="Quantity",y="Ship Mode",data=df)
```
# point plot
```
sns.pointplot(x=df["Quantity"],y=df["Discount"])
sns.pointplot(x=df["Quantity"],y=df["Category"])
sns.pointplot(x=df["Sales"],y=df["Sub-Category"])
```
# Pie Chart
```
df.groupby(['Category']).sum().plot(kind='pie', y='Discount',figsize=(6,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Sub-Category']).sum().plot(kind='pie', y='Sales',figsize=(10,10),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Region']).sum().plot(kind='pie', y='Profit',figsize=(6,9),pctdistance=1.7,labeldistance=1.2)
df.groupby(['Ship Mode']).sum().plot(kind='pie', y='Quantity',figsize=(8,11),pctdistance=1.7,labeldistance=1.2)

df1=df.groupby(by=["Category"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)  
plt.figure(figsize=(8,8))
colors = sns.color_palette('pastel')
plt.pie(df1["Profit"],colors = colors,labels=labels, autopct = '%0.0f%%')
plt.show()

df1=df.groupby(by=["Ship Mode"]).sum()
labels=[]
for i in df1.index:
    labels.append(i)
colors=sns.color_palette("bright")
plt.pie(df1["Sales"],labels=labels,autopct="%0.0f%%")
plt.show()

# HeatMap
```
df4=df.copy()
```
# encoding
```
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
```
# scaling
from sklearn.preprocessing import RobustScaler
sc=RobustScaler()
df5=pd.DataFrame(sc.fit_transform(df4),columns=['Ship Mode', 'Segment', 'City', 'State','Region',
                                               'Category','Sub-Category','Sales','Quantity','Discount','Profit'])
```
# Heatmap
```
plt.subplots(figsize=(12,7))
sns.heatmap(df5.corr(),cmap="PuBu",annot=True)
plt.show()
```

# OUPUT
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/049d6d12-7f74-4460-a0e9-14b8987a0c6b)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/d1d33105-f4e2-4529-8f9f-c6c67619a46c)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/0eb43364-3179-4379-886d-5e9a76dcdf1d)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/0a2355e8-c6b7-49b6-bed0-c5618d8feef8)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/a96b09c0-c1c8-4f20-9983-7d76af10012c)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/8065bcc9-ab08-4f26-9c16-d62ae23a0cca)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/e6930d8d-83fa-4f65-b007-228034470ff4)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/4430efff-374d-48d1-9bc3-e213f03acce8)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/3c1149ef-a992-4f28-b1ce-2cac9e7e5a23)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/cccd7645-291a-4e8e-be57-5e28e0c8c2d8)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/c7f69c6c-2b2e-4aee-b358-0af2178c4153)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/53ad4f0d-7616-492c-a81e-405d0240c94e)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/be02d375-ed5d-469d-91ac-bc0877bcbdeb)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/c6943abb-7dc7-451b-b00f-4d3c0368c7d5)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/1239e93e-d695-48fd-a4a4-d53e802f6bd5)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/f5668b4e-85cb-453a-b295-48e35978bb6e)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/fd0e29a9-7bec-48f8-b888-a29da4d41d7f)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/6264eebf-8fde-43c6-beaa-8d9d75ca3747)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/c6971a2b-6464-430c-95ba-00e67571adae)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/86669f20-2aa1-41b0-b89c-f389f2719e84)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/568953af-ab15-4f2c-b3a5-101f180c9e44)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/99d77b59-bfc8-4f92-b61a-3c7b45089daf)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/cfb91408-4c09-4a74-898d-68de05d5b735)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/2485d314-cc73-4dd4-922f-0113a7e1d1ba)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/b129514d-78d8-483b-8036-d791f00bc339)
![image](https://github.com/Thanikasreeb/Ex-08-Data-Visualization_1/assets/119557910/b23d3e43-44f0-44c0-95ce-365293ef51fd)

# Result:
Hence,Data Visualization is applied on the complex dataset using libraries like Seaborn and Matplotlib successfully and the data is saved to file






















