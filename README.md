<h1>Analyze New Yorker transportation preference base on weather</h1>
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
turnstile_weather = pd.read_csv('../New York Subway/turnstile_weather_v2.csv')
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

<h3>2.1 Ordinary Least Squares Using Statsmodels</h3>
I choose OLS for linear regression, then select different features to get highest "rsqured".

```python
import statsmodels.api as sm 

def linear_regression(features, values):
    features = sm.add_constant(features)
    model = sm.OLS(values, features)
    results = model.fit()
    return results


#Given arbitrary number of features to perform linear regression
values = turnstile_weather['ENTRIESn_hourly']
#1
features = pd.get_dummies(turnstile_weather['UNIT'], prefix='unit')
print "R square for model that only contain UNIT as feature:", linear_regression(features, values).rsquared
#2
features = pd.get_dummies(turnstile_weather['station'], prefix='station')
print "R square for model that only contain station as feature:", linear_regression(features, values).rsquared
#3 regression without cond
numerics = ['precipi', 'pressurei','tempi', 'wspdi',
            'meanprecipi', 'meanpressurei', 'meantempi', 'meanwspdi']
dummies = ['fog', 'rain']
features = turnstile_weather[numerics + dummies]
dummy_units = pd.get_dummies(turnstile_weather['UNIT'], prefix='unit')
features = features.join(dummy_units)
dummy_units = pd.get_dummies(turnstile_weather['datetime'])
features = features.join(dummy_units)
print "R square for model that does not contain cond as dummy feature:", linear_regression(features, values).rsquared
#4 add cond
dummy_units = pd.get_dummies(turnstile_weather['conds'])
features = features.join(dummy_units)
model_results = linear_regression(features, values) # This is my final model, so I would like to keep it
print "R square for model that add cond as dummy feature:", model_results.rsquared
#5 add weather_lat and weather_lon
features.add(turnstile_weather[['weather_lat', 'weather_lon']])
print "R square for model that add weather_lat and weather_lon:", linear_regression(features, values).rsquared
```

    R square for model that only contain UNIT as feature: 0.37521567404
    R square for model that only contain station as feature: 0.324263055724
    R square for model that does not contain cond as dummy feature: 0.574630122068
    R square for model that add cond as dummy feature: 0.575449558588
    R square for model that add weather_lat and weather_lon: 0.575449558588


<h3>2.2 Visulization for the model</h3>


```python
intercept = model_results.params[0]
params = model_results.params[1:]
predictions = intercept + np.dot(features, params)
values_and_predictions = pd.DataFrame({'entries':values, 'predictions':predictions})
ggplot(aes(x='entries', y='predictions'), data=values_and_predictions) + geom_point() + geom_abline(slope=1, intercept=0, color='red') +  ggtitle('Predictions vs. Real Entries')
```
![png](https://github.com/x7zhang/subway/blob/master/graphs/output_11_1.png?raw=true)
<br>This model seem not good for data.

<h2>Section 3: Visualization</h2>

### ENTRIESn_hourly for rainy days and non-rainy days




```python
ggplot(aes(x='ENTRIESn_hourly'), data=turnstile_weather[turnstile_weather['rain'] == 0]) +\
geom_histogram(fill='blue', binwidth=1000) + ylim(0, 20000) + ggtitle('Non-rainy Day Subway Entries') + ylab('frequency')
```


![png](https://github.com/x7zhang/subway/blob/master/graphs/png-24.png?raw=true)

```python
ggplot(aes(x='ENTRIESn_hourly'), data=turnstile_weather[turnstile_weather['rain'] == 1]) +\
geom_histogram(fill='blue', binwidth=1000) + ylim(0, 20000) + ggtitle('Rainy Day Subway Entries') + ylab('frequency')
```


![png](https://github.com/x7zhang/subway/blob/master/graphs/png-23.png?raw=true)

<br>
There is a big differents betweent rainy-day amount and non-rainy-day amount. 33064 for non-rainy datas, and only 9585 for rainy datas. 
We can find, both plots are right-skewed, we can hypothesis if the days for rainy equals to non-rainy day, maybe their result are quiet similar.

```python
from datetime import datetime

df = turnstile_weather[['DATEn', 'ENTRIESn_hourly', 'rain']]
df.is_copy = False

# get the weekday as a string
f = lambda x: datetime.strptime(x, "%Y-%m-%d").strftime('%A')

df['weekday'] = df['DATEn'].apply(f)



print ggplot(df, aes(x = 'ENTRIESn_hourly', colour='factor(rain)')) \
        + geom_density() \
        + xlim(0,2500) \
        + facet_wrap('weekday')
```


![png](https://github.com/x7zhang/subway/blob/master/graphs/output_36_0.png?raw=true)
<br>
Result shows similar in density plot.
<h2>Section 4: Conclusion</h2>
From Mann-Whitney U test, we get the results that more people on average do ride the subway in New York when it is raining. However, the different is not enough to say there is any practical differnece or enough to predict higher or lower ridership based on the presence of rain. If I delete "rain" feature, it did have a large impact on rsquares. 
Due to the rsquares for linear regression is 57.4%, this model is not very good to fit the data.



