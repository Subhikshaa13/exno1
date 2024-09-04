# Exno:1
Data Cleaning Process

# AIM
To read the given data and perform data cleaning and save the cleaned data to a file.

# Explanation
Data cleaning is the process of preparing data for analysis by removing or modifying data that is incorrect ,incompleted , irrelevant , duplicated or improperly formatted. Data cleaning is not simply about erasing data ,but rather finding a way to maximize datasets accuracy without necessarily deleting the information.

# Algorithm
STEP 1: Read the given Data

STEP 2: Get the information about the data

STEP 3: Remove the null values from the data

STEP 4: Save the Clean data to the file

STEP 5: Remove outliers using IQR

STEP 6: Use zscore of to remove outliers

# Coding and Output
```
   import pandas as pd
   df=pd.read_csv("/content/Data_set.csv")
   df
```
![ds1](https://github.com/user-attachments/assets/a24f52ea-1693-4b5f-b214-4da2eb588e7a)
```
   df.dropna(axis=1)
```
![image](https://github.com/user-attachments/assets/82af7c37-71a1-4b99-95b6-84297de8709f)

```
  dfs=df[df['current_overall_rank']> 270]
  dfs
```
![image](https://github.com/user-attachments/assets/4aa2baa1-d6ed-4589-9875-d697db6c83c1)

```
   df.iloc[:4]
```
![image](https://github.com/user-attachments/assets/5b03e943-0b34-4f39-96cd-9100c1e71295)
```
  df.iloc[0:4,1:4]
```
![image](https://github.com/user-attachments/assets/2e978343-0054-415d-a1e1-322115df6eeb)
```
  df.iloc[[1,3,5],[1,3]]
```
![image](https://github.com/user-attachments/assets/4dfa1f5d-c3d7-4353-95c6-af5b38217491)
```
   dff=df.fillna(0)
   dff
```
![image](https://github.com/user-attachments/assets/8d599deb-18a2-461c-b2d0-4ac49cc32560)
```
 df['TOTAL'].fillna(value=df['TOTAL'].mean())
```
![image](https://github.com/user-attachments/assets/15bedb63-569e-4a5f-bcac-a245bdcf6685)

### OUTLIER DETECTION AND REMOVAL USING IQR:
```
  import pandas as pd
  import seaborn as sns
  import numpy as np
  age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
  af=pd.DataFrame(age)
  af
```
![image](https://github.com/user-attachments/assets/301577c3-8236-49e3-a8f8-1b4ee5448d9c)

```
 sns.boxplot(data=af)
```
![image](https://github.com/user-attachments/assets/8611117d-29a4-4e94-88e6-bb9d4e8c1cc2)
```
 sns.scatterplot(data=af)
```
![image](https://github.com/user-attachments/assets/dad0d6d4-cbb9-4948-a3bd-047ca468c84c)
```
  q1=af.quantile(0.25)
  q2=af.quantile(0.5)
  q3=af.quantile(0.75)
  iqr=q3-q1
  iqr
```
![image](https://github.com/user-attachments/assets/ac2b01d9-cd58-41ff-aedb-6c3b7dbbde3f)
```
 Q1=np.percentile(af,25)
 Q3=np.percentile(af,75)
 IQR=Q3-q1
 IQR
```
![image](https://github.com/user-attachments/assets/49008872-5f8a-4750-aa73-84ce29ae358a)
```
 lower_bound=Q1-1.5*IQR
 upper_bound=Q3+1.5*IQR
 lower_bound
```
![image](https://github.com/user-attachments/assets/216698b4-6f18-42d9-bf73-f35cfb1dca6d)
```
 upper_bound
```
![image](https://github.com/user-attachments/assets/ab2323e2-308b-411b-86cb-7bafb4ea5fd8)
```
 outliers = [x for x in age if (x < lower_bound.iloc[0]) or (x > upper_bound.iloc[0])]
 print("q1",q1)
 print("q3",q3)
 print("iqr",iqr)
 print("lower bound",lower_bound)
 print("upper bound",upper_bound)
 print("outliers",outliers)
```
![image](https://github.com/user-attachments/assets/0384af31-7930-4c41-a455-321c10aeb49b)
```
 af=af[((af>=lower_bound)&(af<=upper_bound))]
 af
```
![image](https://github.com/user-attachments/assets/51ab019a-2a32-4a36-aee1-8c15ce000913)
```
 af.dropna()
```
![image](https://github.com/user-attachments/assets/cc34893d-283e-4c62-bd8a-1d809b8af84e)
```
  data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
  mean=np.mean(data)
  std=np.std(data)
  print('mean of the dataset is',mean)
  print('std.deviation is',std)
```
![image](https://github.com/user-attachments/assets/90d220b8-aa51-4865-aed1-7a897419dca1)
```
 threshold=3
 outlier=[]
 for i in data:
   z=(i-mean)/std
   if z>threshold:
     outlier.append(i)
     print('Outlier in dataset is:',outlier)
```
![image](https://github.com/user-attachments/assets/4a4287a3-82a8-4bc5-bbbd-6cd5b2bda2b2)
```
 import pandas as pd
 import numpy as np
 import seaborn as sns
 import pandas as pd
 from scipy import stats
 data={'weight':[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]}

 df=pd.DataFrame(data)
 df
```
![image](https://github.com/user-attachments/assets/eb6b22f5-9304-4a8a-81de-7b50df14aa44)
```
 z=np.abs(stats.zscore(df))
 print(df[z['weight']>3])
```
![image](https://github.com/user-attachments/assets/e99428c8-9599-485a-89c2-d7da4df01ee4)
```
 val=[12,15,18,21,24,27,30,33,36,39,42,45,48,51,54,57,60,63,
                66,69,202,72,75,78,81,84,232,87,90,93,96,99,258]


 import numpy as np
 out=[]
 def d_o(val):
   ts=3
   m=np.mean(val)
   sd=np.std(val)
   for i in val:
     z=(i-m)/sd
     if np.abs(z)>ts:
       out.append(i)
   return out

 op=d_o(val)
 op
```
![image](https://github.com/user-attachments/assets/8a4d7a4f-946d-471c-a300-487a71eae766)

# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method.
