# Ex.No:1  Data Cleaning and Outlier Detection & Removal
## Aim:
To read the given data and perform data cleaning and save the cleaned data to a file.

## Explanation:
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

## Algorithm:
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

## Coding and Output:
## Data cleaning:

```
import pandas as pd
df=pd.read_csv("ex-1.1.csv")
df
```
![image](https://github.com/user-attachments/assets/fc482989-09ea-4d80-9f69-f60b50975709)

```
df.isnull().sum()
```
![image](https://github.com/user-attachments/assets/a5faa84e-5552-46c0-b72b-4bbb82567b34)

```
df.isnull().any()
```
![image](https://github.com/user-attachments/assets/cffeb597-cec4-46df-a1b6-1ce2961cc068)

```
df.dropna()
```
![image](https://github.com/user-attachments/assets/f71813a6-7ed2-4ce1-9113-78f19dddb758)

```
df.fillna(0)
```
![image](https://github.com/user-attachments/assets/c2ac14a8-af26-4444-9fc5-2a7818a2d982)

```
df.fillna(method = 'ffill')
```
![image](https://github.com/user-attachments/assets/989543f4-f3c1-4072-8e69-92a78fcc829d)

```
df.fillna(method = 'bfill')
```
![image](https://github.com/user-attachments/assets/04ea924f-0a3e-4875-9689-eedb9a407fbf)

```
df_dropped=df.dropna()
df_dropped
```
![image](https://github.com/user-attachments/assets/d134e65f-230c-46d4-acb2-93699cfb4247)

```
df.fillna({'GENDER':'MALE','NAME':'SRI','ADDRESS':'POONAMALEE','M1':98,'M2':87,'M3':76,'M4':92,'TOTAL':305,'AVG':89.999999})
```
![image](https://github.com/user-attachments/assets/49edde14-08a1-499f-9883-74c1239425b2)

## IQR(Inter Quartile Range):

```
import pandas as pd
ir=pd.read_csv('ex-1.2.csv')
ir
```
![image](https://github.com/user-attachments/assets/d0e22b10-a49f-4fc4-8690-fa0b2115c4a3)

```
ir.describe()
```
![image](https://github.com/user-attachments/assets/bd6a4081-57b5-4c76-ac6d-5b4146ece6e9)

```
import seaborn as sns
sns.boxplot(x='sepal_width',data=ir)
```
![image](https://github.com/user-attachments/assets/c83debb2-f85e-4c30-87ad-3825a634552a)

```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
print(c3)
```
![image](https://github.com/user-attachments/assets/33aed715-1ba8-4fe8-b9a3-c5ad05313218)

```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```
![image](https://github.com/user-attachments/assets/cbbdc38c-e225-462f-a60d-139c1bd80ad2)

```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```
![image](https://github.com/user-attachments/assets/896179de-0727-440a-8bce-407dd944158b)

```
sns.boxplot(x='sepal_width',data=delid)
```
![image](https://github.com/user-attachments/assets/f009f213-357b-4b31-be4c-9c380aea4059)


## Z-Score:
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dataset=pd.read_csv("ex-1.3.csv")
dataset
```
![image](https://github.com/user-attachments/assets/435661f1-5ed3-4c95-a2f5-68973c5c3a5c)

```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```
![image](https://github.com/user-attachments/assets/da7dcf61-cf5e-44b4-ad05-78bfbef77702)

```
low = q1 - 1.5*iqr
low
```
![image](https://github.com/user-attachments/assets/bafd1459-9eef-4410-ae6c-2097eff08a89)

```
high = q3 + 1.5*iqr
high
```
![image](https://github.com/user-attachments/assets/e280b1bb-6e13-4bde-bdc2-1eb332124674)

```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```
![image](https://github.com/user-attachments/assets/ac5560f4-fff8-477b-a9b7-82c8281f8b84)

```
z = np.abs(stats.zscore(df['height']))
z
```
![image](https://github.com/user-attachments/assets/089c3519-8c3f-4b7f-b7e1-25bd116bd31e)

```
df1 = df[z<3]
df1
```
![image](https://github.com/user-attachments/assets/4248a786-a0c6-41b9-aaaf-01c31b9c22b2)


## Result:
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
