#<h1>Analyze New Yorker transportation preference base on weather</h1>
![image](https://github.com/x7zhang/subway/blob/master/graphs/subway-wireless-nyc.jpg?raw=true)

<h2>Introduction</h2>
The ultimate goal of the analysis is to see whether NYC subway ridership is higher on rainy days vs non-rainy days. Python (NumPy, Pandas, ggplot) is used for the analysis and visualizations respectively.

Sample of MTA New York City Subway dataset containing hourly entries and exits to turnstiles(UNIT) by day in the subway system. Weather data from Weather Underground containing features [ barometric pressure, wind speed, temperature, the total amount of precipitation, and the indicidence of rain, fog, and thunder ] is joined to Subway data.

```python
#Import liberaries we need
import numpy as np
import pandas as pd
from ggplot import *
```


```python
#Load the csv file into Pandas dataframe named turnstile_weather
turnstile_weather = pd.read_csv('../New York Subway/turnstile_data_master_with_weather.csv')
turnstile_weather.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Unnamed: 0</th>
      <th>UNIT</th>
      <th>DATEn</th>
      <th>TIMEn</th>
      <th>Hour</th>
      <th>DESCn</th>
      <th>ENTRIESn_hourly</th>
      <th>EXITSn_hourly</th>
      <th>maxpressurei</th>
      <th>maxdewpti</th>
      <th>...</th>
      <th>meandewpti</th>
      <th>meanpressurei</th>
      <th>fog</th>
      <th>rain</th>
      <th>meanwindspdi</th>
      <th>mintempi</th>
      <th>meantempi</th>
      <th>maxtempi</th>
      <th>precipi</th>
      <th>thunder</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>R001</td>
      <td>2011-05-01</td>
      <td>01:00:00</td>
      <td>1</td>
      <td>REGULAR</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>30.31</td>
      <td>42.0</td>
      <td>...</td>
      <td>39.0</td>
      <td>30.27</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>50.0</td>
      <td>60.0</td>
      <td>69.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>R001</td>
      <td>2011-05-01</td>
      <td>05:00:00</td>
      <td>5</td>
      <td>REGULAR</td>
      <td>217.0</td>
      <td>553.0</td>
      <td>30.31</td>
      <td>42.0</td>
      <td>...</td>
      <td>39.0</td>
      <td>30.27</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>50.0</td>
      <td>60.0</td>
      <td>69.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>R001</td>
      <td>2011-05-01</td>
      <td>09:00:00</td>
      <td>9</td>
      <td>REGULAR</td>
      <td>890.0</td>
      <td>1262.0</td>
      <td>30.31</td>
      <td>42.0</td>
      <td>...</td>
      <td>39.0</td>
      <td>30.27</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>50.0</td>
      <td>60.0</td>
      <td>69.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>R001</td>
      <td>2011-05-01</td>
      <td>13:00:00</td>
      <td>13</td>
      <td>REGULAR</td>
      <td>2451.0</td>
      <td>3708.0</td>
      <td>30.31</td>
      <td>42.0</td>
      <td>...</td>
      <td>39.0</td>
      <td>30.27</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>50.0</td>
      <td>60.0</td>
      <td>69.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>R001</td>
      <td>2011-05-01</td>
      <td>17:00:00</td>
      <td>17</td>
      <td>REGULAR</td>
      <td>4400.0</td>
      <td>2501.0</td>
      <td>30.31</td>
      <td>42.0</td>
      <td>...</td>
      <td>39.0</td>
      <td>30.27</td>
      <td>0.0</td>
      <td>0.0</td>
      <td>5.0</td>
      <td>50.0</td>
      <td>60.0</td>
      <td>69.0</td>
      <td>0.0</td>
      <td>0.0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 22 columns</p>
</div>


<h2>Section 1: Statitical Test</h2>
```python
import matplotlib.pyplot as plt
%matplotlib inline

entries_without_rain = turnstile_weather[turnstile_weather['rain'] == 0]['ENTRIESn_hourly']
entries_with_rain = turnstile_weather[turnstile_weather['rain'] == 1]['ENTRIESn_hourly']

entries_without_rain.hist(range = [0, 6000], bins = 25, label='No Rain')
entries_with_rain.hist(range = [0, 6000], bins = 20, label='Rain')

plt.title('Histogram of ENTRIESn_hourly')
plt.xlabel('ENTRIESn_hourly')
plt.ylabel('Frequency')
plt.legend()


```

![png](https://github.com/x7zhang/subway/blob/master/graphs/output_21_1.png?raw=true)
<h3>1.1 Statistic Test Method</h3>
"Histogram of ENTRIESn_hourly" graph illustrates Subway data is not located in any specific propability distribution. 
<br/><strong>"Mann-Whitney U-Test"</strong> is a good method to analysis it.
<br/>Generally, in this case, I using this test to find the U-statistic and P-value to determine if the two populations(rainy and non-rainy) have equal mean based on the sample means computed from the provided data.
The P-value used in this test is 0.05 to test for significance.

<h3>1.2 Hypothesis</h3>
One-tailed-test
<p><b>Null Hypothesis:</b> There is no statistically differenece in entries population on rainy VS non-rainy days</p>
<p><b>Alternative Hypothesis:</b> There is a statistically differenece in entries population on rainy VS non-rainy days</p>

```python

import scipy
from scipy.stats import kstest

with_rain = turnstile_weather['ENTRIESn_hourly'][turnstile_weather['rain']==1]
without_rain = turnstile_weather['ENTRIESn_hourly'][turnstile_weather['rain']==0]
with_rain_mean = np.mean(with_rain)
without_rain_mean = np.mean(without_rain)
U, p = scipy.stats.mannwhitneyu(with_rain, without_rain)
```

<h3>1.3 Result</h3>
```python
U, p
```

    (1924409167.0, 0.024940392294493356)


<h3>1.4 Significance</h3>
P-value 0.0249 < 0.05, so I reject the null hypothesis and conclude the distribution of the entries is statistically different between rainy and non-rainy days.

<h2>Section 2: Linear Regression</h2>

### 2.1 Feature Selection


```python
#Select Features
features = turnstile_weather[['rain', 'precipi', 'Hour', 'meantempi']]
features.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rain</th>
      <th>precipi</th>
      <th>Hour</th>
      <th>meantempi</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>5</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>9</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>13</td>
      <td>60.0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>17</td>
      <td>60.0</td>
    </tr>
  </tbody>
</table>
</div>

The dummy variable(UNIT) taken directly from the turnstile_weather data is used as categorical features for my linear model.
```python
dummy_units = pd.get_dummies(turnstile_weather['UNIT'], prefix='unit')
features.join(dummy_units).head()

```
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>rain</th>
      <th>precipi</th>
      <th>Hour</th>
      <th>meantempi</th>
      <th>unit_R001</th>
      <th>unit_R002</th>
      <th>unit_R003</th>
      <th>unit_R004</th>
      <th>unit_R005</th>
      <th>unit_R006</th>
      <th>...</th>
      <th>unit_R543</th>
      <th>unit_R544</th>
      <th>unit_R545</th>
      <th>unit_R546</th>
      <th>unit_R547</th>
      <th>unit_R548</th>
      <th>unit_R549</th>
      <th>unit_R550</th>
      <th>unit_R551</th>
      <th>unit_R552</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>1</td>
      <td>60.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>5</td>
      <td>60.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>9</td>
      <td>60.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>3</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>13</td>
      <td>60.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
    <tr>
      <th>4</th>
      <td>0.0</td>
      <td>0.0</td>
      <td>17</td>
      <td>60.0</td>
      <td>1</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>...</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
    </tr>
  </tbody>
</table>
<p>5 rows × 469 columns</p>
</div>

### 2.2 Feature Selection Rationale

meantempi is chosen as a feature as temperature is a component of the weather that affects people’s decision making. A given temperature may affect how long and how much effort it takes to clothe in the morning. A person may simply choose to stay indoors due to discomfort with a given temperature.

Hour feature were chosen as it is easily observed how ridership varies with time of day and day of week. A phenomenon supporting the Hour feature is the daily rush hours that mass transit systems and roadways exhibit and accommodate. 

Rain and precipi features indicate if it is rain at that time and how big is the rain. If rain is too heavy, maybe will increase possible rate for people choose subway.

### 2.3 Model
#### First to stard by normalizing the features in the dataset


```python
#Values
values = turnstile_weather['ENTRIESn_hourly']
m = len(values)

#Normalize the features in the dataset
mu = features.mean()
sigma = features.std()

if(sigma == 0).any():
    raise Exception("One or more features had the same value for all samples, and thus could " + \
                     "not be normalized. Please do not include features with only a single value " + \
                     "in your model.")
features = (features - mu) / sigma

#Add a column of 1s (y intercept)
features['ones'] = np.ones(m)
```


```python
#Set the inititial coefficient vector theta to a column vector of zeros
#Convert features and values to numpy arrays

features_array = np.array(features)
values_array = np.array(values)

#Set values for alpha, number of iterations
alpha = 0.1
num_iterations =75

#Initialize theta for gradient descent
theta_gradient_descent = np.zeros(len(features.columns))
```

Perform gradient descent, building a cost history over time. 
During this process, the cost function recomputes the theta value for
a given number of iterations as a numerical approach to approximating the ideal coefficients to 
fit the linear regression model.


```python
# Perform gradient descent given a data set with an arbitrary number of features
cost_history = []

for i in range(num_iterations):
    predicted_value = np.dot(features_array, theta_gradient_descent)
    theta_gradient_descent = theta_gradient_descent + alpha/m * np.dot(values_array - predicted_value, features_array)
    
    #Compute the cost function given a set of features / values, and the values for our thetas.
    sum_of_square_errors = np.square(np.dot(features_array, theta_gradient_descent) - values_array).sum()
    cost = sum_of_square_errors / (2*m)
    
    #Add cost to history
    cost_history.append(cost)

cost_history = pd.Series(cost_history)

#Calculate predictions
predictions = np.dot(features_array, theta_gradient_descent)

```


### Goodness of Fit

After making predictions, use the coefficient of determination(R^2) to see how the model performed


```python
#Compute the coefficient of determination (R^2) given
# a list of original data points and a list of predicted data points
sg_data_predictions_diff = np.sum((values - predictions) ** 2)
mean = np.mean(values)
sg_data_mean_diff = np.sum((values - mean) ** 2)

r_squared = 1 - sg_data_predictions_diff / sg_data_mean_diff

print 'Calculated R^2 value: {0}'.format(r_squared)
```

    Calculated R^2 value: 0.45804431403
 This R^2 value is is rather low, indicating that linear regression model doesn't fit with the data too well. 
