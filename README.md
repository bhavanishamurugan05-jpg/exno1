# Exno:1
Data Cleaning Process
# NAME: BHAVANISHA.M
# REF NO:25018505

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
df=pd.read_csv("SAMPLEIDS.csv")
df
```
<img width="999" height="701" alt="image" src="https://github.com/user-attachments/assets/4e753d89-a3ee-42b2-8797-bd842da36931" />

```python
df.shape
```
<img width="86" height="36" alt="image" src="https://github.com/user-attachments/assets/248446fc-81f3-47bb-919e-5d65edcb0582" />

```python
df.describe()
```
<img width="925" height="352" alt="image" src="https://github.com/user-attachments/assets/c42b7250-3fcf-43ad-a4cc-87687d219bd4" />

```python
df.info()
```
<img width="404" height="429" alt="image" src="https://github.com/user-attachments/assets/79a4de03-6cb3-499e-8fa3-3d47376fcebd" />

```python
df.head(5)
```
<img width="965" height="245" alt="image" src="https://github.com/user-attachments/assets/e208a0e3-a525-4e4d-b18f-ce7059c14b29" />

```python
df.tail(2)
```
<img width="974" height="124" alt="image" src="https://github.com/user-attachments/assets/4e2a9575-b9e1-4d7b-80a0-9592f5165618" />

```python
df.dropna(how='any').shape
```
<img width="86" height="43" alt="image" src="https://github.com/user-attachments/assets/2f236362-9c22-412e-9992-b448c9ef2d13" />

```python
df.isnull().sum()
```
<img width="174" height="560" alt="image" src="https://github.com/user-attachments/assets/e55347e6-83a9-49b8-b060-a1e9cba2c2f3" />

```python
mn=df.TOTAL.mean()
df.TOTAL.fillna(mn,inplace=True)
df
```
<img width="1280" height="620" alt="image" src="https://github.com/user-attachments/assets/e5f4f574-a2d1-4e69-8e8e-5bad006ca356" />

```python
df.M1.dropna(inplace=True)
df
```
<img width="811" height="687" alt="image" src="https://github.com/user-attachments/assets/b0cd311f-8f05-4047-af2c-e031571c2bb3" />

```python
df.isna().sum()
```
<img width="139" height="559" alt="image" src="https://github.com/user-attachments/assets/43b4126b-6465-453f-8b01-211a920a2ebb" />

```python
df['M1'].fillna(method='ffill',inplace=True)
```
<img width="1280" height="157" alt="image" src="https://github.com/user-attachments/assets/a9630c5b-5b64-4c49-9b25-bb3d5e8ea7df" />

```python
df.duplicated()
```
<img width="101" height="727" alt="image" src="https://github.com/user-attachments/assets/8322103d-ba2f-4c40-88f3-a4824d87f326" />

```python
df['DOB']
```
<img width="121" height="730" alt="image" src="https://github.com/user-attachments/assets/b33decad-2e3e-416e-9461-554a6c2779f4" />

```python
import seaborn as sns
sns.heatmap(df.isnull(),yticklabels=False,annot=True)
```
<img width="505" height="504" alt="image" src="https://github.com/user-attachments/assets/026adf1c-e4aa-4c19-966d-505beb6d8484" />

```python
import pandas as pd
import seaborn as sns
import numpy as np
age=[1,3,28,27,25,92,30,39,40,50,26,24,29,94]
af=pd.DataFrame(age)
af
```
<img width="70" height="468" alt="image" src="https://github.com/user-attachments/assets/64ffe7e5-209e-4a60-9015-b36b2fcf7d23" />

```python
sns.boxplot(data=af)
```
<img width="561" height="434" alt="image" src="https://github.com/user-attachments/assets/16537c11-084c-4f20-8aef-8b887ea8eafe" />

```python
sns.scatterplot(data=af)
```
<img width="565" height="435" alt="image" src="https://github.com/user-attachments/assets/59fa4924-22f8-4d1c-a79f-f9cbea267e5b" />

```python
q1=af.quantile(0.25)
q2=af.quantile(0.5)
q3=af.quantile(0.75)
iqr=q3-q1
iqr
```
<img width="111" height="119" alt="image" src="https://github.com/user-attachments/assets/022c7dd1-4878-4181-ad2c-a33c0734addb" />

```python
Q1=np.percentile(af,25)
Q3=np.percentile(af,75)
IQR=Q3-q1
IQR
```
<img width="114" height="102" alt="image" src="https://github.com/user-attachments/assets/7e9d56e0-5799-4d45-af8d-6d0313c5c813" />

```python
lower_bound=Q1-1.5*IQR
upper_bound=Q3+1.5*IQR
lower_bound
```
<img width="117" height="112" alt="image" src="https://github.com/user-attachments/assets/773fe25c-df34-42ff-af48-2640293a2247" />

```python
upper_bound
```
<img width="110" height="106" alt="image" src="https://github.com/user-attachments/assets/45d0948a-fe77-4251-ac50-95ba2028373b" />

```python
outliers = [x for x in age if (x < lower_bound.iloc[0]) or (x > upper_bound.iloc[0])]
print("q1",q1)
print("q3",q3)
print("iqr",iqr)
print("lower bound",lower_bound)
print("upper bound",upper_bound)
print("outliers",outliers)
```
<img width="216" height="193" alt="image" src="https://github.com/user-attachments/assets/4612ec0d-6135-4c13-8cb7-be678c80233e" />

```python
af=af[((af>=lower_bound)&(af<=upper_bound))]
```
<img width="73" height="334" alt="image" src="https://github.com/user-attachments/assets/93e9fa2c-93b0-4e3a-8659-f07ee8e9c2ef" />

```python
data=[1,2,2,2,3,1,1,15,2,2,2,3,1,1,2]
mean=np.mean(data)
std=np.std(data)
print('mean of the dataset is',mean)
print('std.deviation is',std)
```
<img width="326" height="57" alt="image" src="https://github.com/user-attachments/assets/4da33897-78de-46fb-8bf8-1b20af17988c" />

```python
threshold=3
outlier=[]
for i in data:
  z=(i-mean)/std
  if z>threshold:
    outlier.append(i)
    print('Outlier in dataset is:',outlier)
```
<img width="240" height="50" alt="image" src="https://github.com/user-attachments/assets/9db23120-60ac-4b3d-ae2b-04451b0a9ab8" />

```python
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
<img width="73" height="704" alt="image" src="https://github.com/user-attachments/assets/0ce05070-cb41-4397-b5e4-5eef96f57a40" />

```python
z=np.abs(stats.zscore(df))
print(df[z['weight']>3])
```
<img width="87" height="57" alt="image" src="https://github.com/user-attachments/assets/19e6d7ca-4630-4bd7-b9f2-c4f609b51fb3" />

```python
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
<img width="72" height="28" alt="image" src="https://github.com/user-attachments/assets/2f294732-13b3-42ed-bcf4-57a74f3f670f" />

# Result
Thus we have cleaned the data and removed the outliers by detection by using IQR and Z-score method.
