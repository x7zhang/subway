#<h1>Analyze New Yorker transportation preference base on weather</h1>
![image](https://github.com/x7zhang/subway/blob/master/graphs/subway-wireless-nyc.jpg?raw=true)

<h2>Introduction</h2>
The ultimate goal of the analysis is to see whether NYC subway ridership is higher on rainy days vs non-rainy days. Python (NumPy, Pandas, ggplot) is used for the analysis and visualizations respectively.

Sample of MTA New York City Subway dataset containing hourly entries and exits to turnstiles(UNIT) by day in the subway system. Weather data from Weather Underground containing features [ barometric pressure, wind speed, temperature, the total amount of precipitation, and the indicidence of rain, fog, and thunder ] is joined to Subway data.

```python
#import liberaries we need
import numpy as np
import pandas as pd
import matplotlib as plt
%matplotlib inline
from ggplot import *
import scipy
from scipy.stats import kstest
```


```python
#load the csv file into Pandas dataframe named turnstile_weather
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

plt.figure()

entries_without_rain = turnstile_weather[turnstile_weather['rain'] == 0]['ENTRIESn_hourly']
entries_with_rain = turnstile_weather[turnstile_weather['rain'] == 1]['ENTRIESn_hourly']

entries_without_rain.hist(range = [0, 6000], bins = 25, label='No Rain')
entries_with_rain.hist(range = [0, 6000], bins = 20, label='Rain')

plt.title('Histogram of ENTRIESn_hourly')
plt.xlabel('ENTRIESn_hourly')
plt.ylabel('Frequency')
plt.legend()

plt.figure()
```

![png](https://github.com/x7zhang/subway/blob/master/graphs/output_21_1.png?raw=true)

"Histogram of ENTRIESn_hourly" graph illustrates Subway data is not located in any specific propability distribution. 
 "Mann-Whitney Test" is a good method to analysis it.

