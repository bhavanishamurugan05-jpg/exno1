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
import numpy as np
from scipy import stats

# Function to display initial information about the dataset
def initial_data_info(df):
    print("Info:")
    print(df.info())
    print("\nDescribe:")
    print(df.describe())
    print("\nNull values per column:")
    print(df.isnull().sum())
    print('=' * 40)

# Function to remove null values
def remove_nulls(df):
    return df.dropna()

# Function to remove outliers using the IQR method
def remove_outliers_iqr(df, columns):
    for col in columns:
        Q1 = df[col].quantile(0.25)
        Q3 = df[col].quantile(0.75)
        IQR = Q3 - Q1
        lower = Q1 - 1.5 * IQR
        upper = Q3 + 1.5 * IQR
        df = df[(df[col] >= lower) & (df[col] <= upper)]
    return df

# Function to remove outliers using the Z-score method
def remove_outliers_zscore(df, columns, thresh=3):
    for col in columns:
        z = np.abs(stats.zscore(df[col].dropna()))
        filtered_entries = (z < thresh)
        valid_indices = df[col].dropna().index[filtered_entries]
        df = df.loc[valid_indices]
    return df

# List of dataset filenames
file_names = [
    "Data_set.csv",
    "heights.csv",
    "iris.csv",
    "Loan_data.csv",
    "SAMPLEIDS (1).csv"
]

# Process each file one by one
for file in file_names:
    print(f'Processing file: {file}')
    df = pd.read_csv(file)
    
    print("Initial Info")
    initial_data_info(df)
    
    # Remove nulls
    df_no_nulls = remove_nulls(df)
    print("After Removing Nulls:")
    print(df_no_nulls.shape)
    
    # Select numeric columns
    numeric_cols = df_no_nulls.select_dtypes(include=[np.number]).columns.tolist()
    
    # Remove outliers using IQR method
    df_iqr = remove_outliers_iqr(df_no_nulls.copy(), numeric_cols)
    print("After Removing Outliers (IQR method):", df_iqr.shape)
    
    # Remove outliers using Z-score method
    df_z = remove_outliers_zscore(df_no_nulls.copy(), numeric_cols)
    print("After Removing Outliers (Z-score method):", df_z.shape)
    
    print('=' * 80)
```
<img width="1371" height="706" alt="Screenshot 2025-10-09 130228" src="https://github.com/user-attachments/assets/e132e63d-8357-47df-8b4a-90f49c0a36c5" />
<img width="1341" height="721" alt="Screenshot 2025-10-09 130241" src="https://github.com/user-attachments/assets/d8b63e03-59a3-4135-a5b9-221dbefba14d" />
<img width="901" height="755" alt="Screenshot 2025-10-09 130259" src="https://github.com/user-attachments/assets/1bf5376e-64ca-4fb1-bf25-a4fd09a47e64" />
<img width="738" height="638" alt="Screenshot 2025-10-09 130311" src="https://github.com/user-attachments/assets/afbe17e0-a4fb-47e6-b10a-9e0be7c15db2" />
<img width="981" height="785" alt="Screenshot 2025-10-09 130321" src="https://github.com/user-attachments/assets/8bc74e71-5116-428f-bfff-4af7b6b0522f" />
<img width="874" height="635" alt="Screenshot 2025-10-09 130333" src="https://github.com/user-attachments/assets/cc29c20f-6069-4881-9623-299fac406835" />
<img width="976" height="770" alt="Screenshot 2025-10-09 130342" src="https://github.com/user-attachments/assets/acd6c3cf-5be4-4ba6-8ffe-bb1569ede97b" />
<img width="1068" height="673" alt="Screenshot 2025-10-09 130354" src="https://github.com/user-attachments/assets/3718a185-56f6-42b3-a628-277d36dcaf15" />

# Result
Thus we have cleaned the data and removed the outliers by detection by using IQR and Z-score method.
