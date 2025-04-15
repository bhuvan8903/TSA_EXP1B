# Ex.No: 1B                     CONVERSION OF NON STATIONARY TO STATIONARY DATA
# Date: 

## AIM:
To perform regular differncing,seasonal adjustment and log transformatio on international airline passenger data
## ALGORITHM:
1. Import the required packages like pandas and numpy
2. Read the data using the pandas
3. Perform the data preprocessing if needed and apply regular differncing,seasonal adjustment,log transformation.
4. Plot the data according to need, before and after regular differncing,seasonal adjustment,log transformation.
5. Display the overall results.
## PROGRAM:
```
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.seasonal import seasonal_decompose

# Load the dataset
data = pd.read_csv('Time-Series Analysis Dataset.csv')

# Convert 'Date' to datetime and set it as the index
data['datetime_local'] = pd.to_datetime(data['datetime_local'])
data.set_index('datetime_local', inplace=True)

# Drop rows with missing values in 'USD'
data.dropna(subset=['temperature'], inplace=True)

# ---------- USD Analysis ----------
# Regular differencing
data['usd_diff'] = data['temperature'].diff()

# Seasonal decomposition of original USD
result_usd = seasonal_decompose(data['temperature'], model='additive', period=12)
data['usd_sea_diff'] = result_usd.resid

# Log transformation
data['usd_log'] = np.log(data['temperature'])

# Log transformation + regular differencing
data['usd_log_diff'] = data['usd_log'].diff().dropna()

# Seasonal decomposition after log differencing
if len(data['usd_log_diff'].dropna()) >= 12:  # Check if enough data exists for decomposition
    result_usd_log = seasonal_decompose(data['usd_log_diff'].dropna(), model='additive', period=12)
    data['usd_log_seasonal_diff'] = result_usd_log.resid
else:
    data['usd_log_seasonal_diff'] = np.nan
    print("Not enough data for seasonal decomposition after log differencing for USD.")

# Plotting results
plt.figure(figsize=(16, 12))

# Original TEMP Data
plt.subplot(2, 1, 1)
plt.plot(data['temperature'], label='Original Temperature')
plt.legend(loc='best')
plt.title('Original TEMP Data')

# TEMP Regular Differencing
plt.subplot(2, 1, 1)
plt.plot(data['usd_diff'], label='TEMP Difference')
plt.legend(loc='best')
plt.title('TEMP Regular Differencing')

# TEMP Seasonal Adjustment
plt.subplot(2, 1, 1)
plt.plot(data['usd_sea_diff'], label='TEMP Seasonal Adjustment')
plt.legend(loc='best')
plt.title('TEMP Seasonal Adjustment')

# Log Transformation of TEMP
plt.subplot(2, 1, 1)
plt.plot(data['usd_log'], label='Log Transformation (temperature)')
plt.legend(loc='best')
plt.title('Log Transformation of TEMP')

# Log Transformation and Differencing (TEMP)
plt.subplot(2, 1, 1)
plt.plot(data['usd_log_diff'], label='Log Transformation + Diff (TEMP)')
plt.legend(loc='best')
plt.title('Log Transformation and Differencing (TEMP)')

# Log, Differencing, and Seasonal Adjustment (TEMP)
plt.subplot(2, 1, 1)
plt.plot(data['usd_log_seasonal_diff'], label='Log + Diff + Seasonal Diff (TEMP)')
plt.legend(loc='best')
plt.title('Log, Differencing, and Seasonal Adjustment (TEMP)')

```

## OUTPUT:

![download](https://github.com/user-attachments/assets/fbadd3a1-7eab-4eec-9d3c-968ef5aec8fe)

### REGULAR DIFFERENCING:
![download (1)](https://github.com/user-attachments/assets/57f10fb4-1fe1-4cb7-a3d5-82746453c888)

### SEASONAL ADJUSTMENT:
![download (2)](https://github.com/user-attachments/assets/016c9544-7ea5-4f6d-9709-3a50d08dfd23)

### LOG TRANSFORMATION:
![download (3)](https://github.com/user-attachments/assets/d8603f8e-320e-4b15-a0f2-339d223f496e)

### LOG TRANSFORMATION AND DIFERENCING(TEMP)
![download (4)](https://github.com/user-attachments/assets/9cbab3d4-4b2f-4322-9590-2c02204a87e7)
### LOG,DIFFERENCING, AND SEASONAL ADJUSTMENT(TEMP)
![download (5)](https://github.com/user-attachments/assets/92ab607b-6698-4ec4-8e60-2cf16d81d4bd)


### RESULT:
Thus we have created the python code for the conversion of non stationary to stationary data on international airline passenger
data.
