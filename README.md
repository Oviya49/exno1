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
## Data Cleaning
```
import pandas as pd
nam=pd.read_csv("/content/Data_set.csv")
nam.head(8)
```
![image](https://github.com/user-attachments/assets/e2dd34ad-bad6-4aa0-962c-482646bfc8b7)
```
nam.tail()
```
![image](https://github.com/user-attachments/assets/547633e8-e2dc-456b-8d8c-0203199480c1)
```
nam.isnull()
```
![image](https://github.com/user-attachments/assets/e1f0177d-24d4-4898-96d2-2d5d299a9d21)
```
nam.isnull().sum()
```
![image](https://github.com/user-attachments/assets/3573e286-c254-4fb2-859e-fa573619888b)
```
nam.isnull().any()
```
![image](https://github.com/user-attachments/assets/43eef7fe-9c79-4586-b72f-e72bf13ee656)
```
nam.dropna()
```
![image](https://github.com/user-attachments/assets/0e5051dc-32b8-46e1-a5f5-b49f7cc536c5)
```
nam.fillna(400,inplace=True)
nam.dropna(axis=1)
```
![image](https://github.com/user-attachments/assets/0b68a6cd-d86e-4b49-98c7-4598e5803283)
```
df.fillna(0)
```
![image](https://github.com/user-attachments/assets/443dcf1e-93f5-4ca6-894b-89a82b01d1f6)
```
df.fillna(method = 'ffill')
```

![image](https://github.com/user-attachments/assets/0fa0088c-a215-44c7-b84d-59dc93606910)

```
df.fillna(method = 'bfill')
```

![image](https://github.com/user-attachments/assets/4febf8b5-3d77-497d-863b-ddb9b1e59c6c)

```
nam_dropped = nam.dropna()
nam_dropped
```

![image](https://github.com/user-attachments/assets/1a7c4d72-5f93-4466-be73-36ba56e53a01)
## IQR(Inter Quartile Range)
```
import pandas as pd
ir=pd.read_csv("/content/iris.csv")
ir
```

![image](https://github.com/user-attachments/assets/ec385fca-ddeb-404d-8cbe-829b68382240)
```
ir.describe()
```

![image](https://github.com/user-attachments/assets/3cf0c16f-396d-4126-8b39-083e43b85aa2)
```
sns.boxplot(x='sepal_width',data=ir)
```

![image](https://github.com/user-attachments/assets/8c128c6a-721d-4fb5-a5ce-75952e68f194)
```
c1=ir.sepal_width.quantile(0.25)
c3=ir.sepal_width.quantile(0.75)
iq=c3-c1
print(c3)
```

![image](https://github.com/user-attachments/assets/9271e515-0c84-48ce-8a7f-62e4f069212f)
```
rid=ir[((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
rid['sepal_width']
```

![image](https://github.com/user-attachments/assets/342c5a60-f4ce-430f-a1ee-9d095c8402da)
```
delid=ir[~((ir.sepal_width<(c1-1.5*iq))|(ir.sepal_width>(c3+1.5*iq)))]
delid
```

![image](https://github.com/user-attachments/assets/5fbbeb0f-84df-4e4f-9cd9-ecb71aaab981)
```
sns.boxplot(x='sepal_width',data=delid)
```

![image](https://github.com/user-attachments/assets/953377ca-a7a8-44fe-9cea-9d26e4c65ffc)
## Z-Score
```
import matplotlib.pyplot as plt
import pandas as pd
import numpy as np
import scipy.stats as stats
dp=pd.read_csv("/content/heights.csv")
dp
```

![image](https://github.com/user-attachments/assets/d3fbceab-6b53-4a85-9b3f-263ccd81f7b1)
```
df = pd.read_csv("heights.csv")
q1 = df['height'].quantile(0.25)
q2 = df['height'].quantile(0.5)
q3 = df['height'].quantile(0.75)
iqr = q3-q1
iqr
```

![image](https://github.com/user-attachments/assets/b8530173-dc9f-4f58-aa09-c69d4f5f3709)
```
low = q1 - 1.5*iqr
low
```

![image](https://github.com/user-attachments/assets/1a44c03e-1587-4636-b405-81b8f9964b17)
```
high = q3 + 1.5*iqr
high
```

![image](https://github.com/user-attachments/assets/0fa838f9-8205-42cf-893d-a9b252b8dd97)
```
df1 = df[((df['height'] >=low)& (df['height'] <=high))]
df1
```

![image](https://github.com/user-attachments/assets/3333683c-a8fd-46a4-a4b3-a1a8ce7c1ad4)
```
z = np.abs(stats.zscore(df['height']))
z
```

![image](https://github.com/user-attachments/assets/7976fa76-3463-4577-b65b-6380fec5e307)
```
df1 = df[z<3]
df1
```

![image](https://github.com/user-attachments/assets/9c936e36-debc-4dc5-b012-67f100e9c45f)
# Result
Thus we have cleaned the data and removed the outliers by detection using IQR and Z-score method
