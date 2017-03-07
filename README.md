# subway
<!DOCTYPE html>
<html>
<head><meta charset="utf-8" />
<title>Subway Analysis</title>

<script src="https://cdnjs.cloudflare.com/ajax/libs/require.js/2.1.10/require.min.js"></script>
<script src="https://cdnjs.cloudflare.com/ajax/libs/jquery/2.0.3/jquery.min.js"></script>





<!-- Custom stylesheet, it must be in the same directory as the html file -->
</head>
<body>
  <div tabindex="-1" id="notebook" class="border-box-sizing">
    <div class="container" id="notebook-container">

<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[1]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">import</span> <span class="nn">pandas</span> <span class="kn">as</span> <span class="nn">pd</span>
<span class="kn">import</span> <span class="nn">numpy</span> <span class="kn">as</span> <span class="nn">np</span>
<span class="kn">import</span> <span class="nn">matplotlib</span> <span class="kn">as</span> <span class="nn">plt</span>
<span class="o">%</span><span class="k">matplotlib</span> inline
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[2]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">turnstile_weather</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">read_csv</span><span class="p">(</span><span class="s">&#39;turnstile_data_master_with_weather.csv&#39;</span><span class="p">)</span>
<span class="n">turnstile_weather</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[2]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
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
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Linear-Regression">Linear Regression<a class="anchor-link" href="#Linear-Regression">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Feature-Selection">Feature Selection<a class="anchor-link" href="#Feature-Selection">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[5]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="c">#Select Features</span>
<span class="n">features</span> <span class="o">=</span> <span class="n">turnstile_weather</span><span class="p">[[</span><span class="s">&#39;rain&#39;</span><span class="p">,</span> <span class="s">&#39;precipi&#39;</span><span class="p">,</span> <span class="s">&#39;Hour&#39;</span><span class="p">,</span> <span class="s">&#39;meantempi&#39;</span><span class="p">]]</span>
<span class="n">features</span><span class="o">.</span><span class="n">head</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[5]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
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
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[4]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">dummy_units</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">get_dummies</span><span class="p">(</span><span class="n">turnstile_weather</span><span class="p">[</span><span class="s">&#39;UNIT&#39;</span><span class="p">],</span> <span class="n">prefix</span><span class="o">=</span><span class="s">&#39;unit&#39;</span><span class="p">)</span>
<span class="n">features</span><span class="o">.</span><span class="n">join</span><span class="p">(</span><span class="n">dummy_units</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[4]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
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
      <td>0.00</td>
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
      <td>0.00</td>
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
      <td>0.00</td>
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
      <td>0.00</td>
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
      <td>0.00</td>
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
    <tr>
      <th>5</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>21</td>
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
      <th>6</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>1</td>
      <td>60.0</td>
      <td>0</td>
      <td>1</td>
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
      <th>7</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>5</td>
      <td>60.0</td>
      <td>0</td>
      <td>1</td>
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
      <th>8</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>9</td>
      <td>60.0</td>
      <td>0</td>
      <td>1</td>
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
      <th>9</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>13</td>
      <td>60.0</td>
      <td>0</td>
      <td>1</td>
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
      <th>10</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>17</td>
      <td>60.0</td>
      <td>0</td>
      <td>1</td>
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
      <th>11</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>21</td>
      <td>60.0</td>
      <td>0</td>
      <td>1</td>
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
      <th>12</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>13</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>4</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>14</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>12</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>15</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>16</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>16</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>20</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>17</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>18</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>4</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>19</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>8</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>20</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>12</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>21</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>16</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>22</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>20</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>23</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>24</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>4</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>25</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>12</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>26</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>16</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>27</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>20</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>28</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>0</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>29</th>
      <td>0.0</td>
      <td>0.00</td>
      <td>4</td>
      <td>60.0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>0</td>
      <td>1</td>
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
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>131921</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>17</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131922</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>18</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131923</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>18</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131924</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>18</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131925</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>18</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131926</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>19</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131927</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>19</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131928</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>19</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131929</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>19</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131930</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>19</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131931</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>19</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131932</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>19</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131933</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>20</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131934</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>20</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131935</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>20</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131936</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>20</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131937</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>20</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131938</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>20</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131939</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>21</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131940</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>21</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131941</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>22</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131942</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>22</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131943</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>22</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131944</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>22</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131945</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>22</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131946</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>23</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131947</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>23</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131948</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>23</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131949</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>23</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
    <tr>
      <th>131950</th>
      <td>1.0</td>
      <td>0.29</td>
      <td>23</td>
      <td>78.0</td>
      <td>0</td>
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
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>131951 rows × 469 columns</p>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Model-Results">Model Results<a class="anchor-link" href="#Model-Results">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h4 id="First-to-stard-by-normalizing-the-features-in-the-dataset">First to stard by normalizing the features in the dataset<a class="anchor-link" href="#First-to-stard-by-normalizing-the-features-in-the-dataset">&#182;</a></h4>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[6]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="c">#Values</span>
<span class="n">values</span> <span class="o">=</span> <span class="n">turnstile_weather</span><span class="p">[</span><span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">]</span>
<span class="n">m</span> <span class="o">=</span> <span class="nb">len</span><span class="p">(</span><span class="n">values</span><span class="p">)</span>

<span class="c">#Normalize the features in the dataset</span>
<span class="n">mu</span> <span class="o">=</span> <span class="n">features</span><span class="o">.</span><span class="n">mean</span><span class="p">()</span>
<span class="n">sigma</span> <span class="o">=</span> <span class="n">features</span><span class="o">.</span><span class="n">std</span><span class="p">()</span>

<span class="k">if</span><span class="p">(</span><span class="n">sigma</span> <span class="o">==</span> <span class="mi">0</span><span class="p">)</span><span class="o">.</span><span class="n">any</span><span class="p">():</span>
    <span class="k">raise</span> <span class="ne">Exception</span><span class="p">(</span><span class="s">&quot;One or more features had the same value for all samples, and thus could &quot;</span> <span class="o">+</span> \
                     <span class="s">&quot;not be normalized. Please do not include features with only a single value &quot;</span> <span class="o">+</span> \
                     <span class="s">&quot;in your model.&quot;</span><span class="p">)</span>
<span class="n">features</span> <span class="o">=</span> <span class="p">(</span><span class="n">features</span> <span class="o">-</span> <span class="n">mu</span><span class="p">)</span> <span class="o">/</span> <span class="n">sigma</span>

<span class="c">#Add a column of 1s (y intercept)</span>
<span class="n">features</span><span class="p">[</span><span class="s">&#39;ones&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">ones</span><span class="p">(</span><span class="n">m</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[7]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="c">#We set the inititial coefficient vector theta to a column vector of zeros</span>
<span class="c">#Convert features and values to numpy arrays</span>

<span class="n">features_array</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">features</span><span class="p">)</span>
<span class="n">values_array</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">array</span><span class="p">(</span><span class="n">values</span><span class="p">)</span>

<span class="c">#Set values for alpha, number of iterations</span>
<span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.1</span>
<span class="n">num_iterations</span> <span class="o">=</span><span class="mi">75</span>

<span class="c">#initialize theta for gradient descent</span>
<span class="n">theta_gradient_descent</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">zeros</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">features</span><span class="o">.</span><span class="n">columns</span><span class="p">))</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Perform gradient descent, building a cost history over time. 
During this process, the cost function recomputes the theta value for
a given number of iterations as a numerical approach to approximating the ideal coefficients to 
fit the linear regression model.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[8]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="c"># Perform gradient descent given a data set with an arbitrary number of features</span>
<span class="n">cost_history</span> <span class="o">=</span> <span class="p">[]</span>

<span class="k">for</span> <span class="n">i</span> <span class="ow">in</span> <span class="nb">range</span><span class="p">(</span><span class="n">num_iterations</span><span class="p">):</span>
    <span class="n">predicted_value</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">features_array</span><span class="p">,</span> <span class="n">theta_gradient_descent</span><span class="p">)</span>
    <span class="n">theta_gradient_descent</span> <span class="o">=</span> <span class="n">theta_gradient_descent</span> <span class="o">+</span> <span class="n">alpha</span><span class="o">/</span><span class="n">m</span> <span class="o">*</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">values_array</span> <span class="o">-</span> <span class="n">predicted_value</span><span class="p">,</span> <span class="n">features_array</span><span class="p">)</span>
    
    <span class="c">#Compute the cost function given a set of features / values, and the values for our thetas.</span>
    <span class="n">sum_of_square_errors</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">square</span><span class="p">(</span><span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">features_array</span><span class="p">,</span> <span class="n">theta_gradient_descent</span><span class="p">)</span> <span class="o">-</span> <span class="n">values_array</span><span class="p">)</span><span class="o">.</span><span class="n">sum</span><span class="p">()</span>
    <span class="n">cost</span> <span class="o">=</span> <span class="n">sum_of_square_errors</span> <span class="o">/</span> <span class="p">(</span><span class="mi">2</span><span class="o">*</span><span class="n">m</span><span class="p">)</span>
    
    <span class="c">#Add cost to history</span>
    <span class="n">cost_history</span><span class="o">.</span><span class="n">append</span><span class="p">(</span><span class="n">cost</span><span class="p">)</span>

<span class="n">cost_history</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">Series</span><span class="p">(</span><span class="n">cost_history</span><span class="p">)</span>

<span class="c">#Calculate predictions</span>
<span class="n">predictions</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">dot</span><span class="p">(</span><span class="n">features_array</span><span class="p">,</span> <span class="n">theta_gradient_descent</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>Let's visualize this:</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[9]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">from</span> <span class="nn">ggplot</span> <span class="kn">import</span> <span class="o">*</span>

<span class="c">#Plot cost history for viewing</span>
<span class="n">cost_df</span> <span class="o">=</span> <span class="n">pd</span><span class="o">.</span><span class="n">DataFrame</span> <span class="p">({</span>
    <span class="s">&#39;Cost_History&#39;</span><span class="p">:</span> <span class="n">cost_history</span><span class="p">,</span>
    <span class="s">&#39;Iteration&#39;</span><span class="p">:</span> <span class="nb">range</span><span class="p">(</span><span class="nb">len</span><span class="p">(</span><span class="n">cost_history</span><span class="p">))</span>
<span class="p">})</span>

<span class="n">ggplot</span><span class="p">(</span><span class="n">cost_df</span><span class="p">,</span> <span class="n">aes</span><span class="p">(</span><span class="s">&#39;Iteration&#39;</span><span class="p">,</span> <span class="s">&#39;Cost_History&#39;</span><span class="p">))</span> <span class="o">+</span> \
    <span class="n">geom_point</span><span class="p">()</span> <span class="o">+</span> <span class="n">ggtitle</span><span class="p">(</span><span class="s">&#39;Cost History for alpha = </span><span class="si">%.3f</span><span class="s">&#39;</span> <span class="o">%</span> <span class="n">alpha</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stderr output_text">
<pre>//anaconda/lib/python2.7/site-packages/ggplot/ggplot.py:192: RuntimeWarning: Setting &quot;mpl.rcParams[&apos;axes.prop_cycle&apos;]=cycler(u&apos;color&apos;, [u&apos;#333333&apos;, u&apos;#348ABD&apos;, u&apos;#7A68A6&apos;, u&apos;#A60628&apos;, u&apos;#467821&apos;, u&apos;#CF4457&apos;, u&apos;#188487&apos;, u&apos;#E24A33&apos;])&quot; raised an Exception: u&apos;axes.prop_cycle is not a valid rc parameter.See rcParams.keys() for a list of valid parameters.&apos;
  warnings.warn(msg, RuntimeWarning)
//anaconda/lib/python2.7/site-packages/matplotlib/collections.py:590: FutureWarning: elementwise comparison failed; returning scalar instead, but in the future will perform elementwise comparison
  if self._edgecolors == str(&apos;face&apos;):
</pre>
</div>
</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAuEAAAIhCAYAAADgqGQmAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzs3Xt0VPW9/vFnZjKZbMgMCSTBkHBJQki404CFWCVBgpJG
0VJz6g2kKlpKT7T212W9Uy+1th7rwYUVaa0HvJUGiBZ7o0QDWo+ikFhAaEwTMAbkFsmQ60wyvz8w
c9gGYlBmT4zv11qsldkze+/PPLhcTzbf2WMLBAIBAQAAALCMPdwDAAAAAF81lHAAAADAYpRwAAAA
wGKUcAAAAMBilHAAAADAYpRwAAAAwGKUcABfSZs3b1ZmZma4xzip7373uxo4cKCmTZsW8nMtWLBA
d9111xl/LQCge5RwACH13HPPacqUKXK73RoyZIi++c1v6vXXX/9CxxwxYoRKS0tP+fyrr76qoUOH
dtmem5ur3/72t5Kk8847T7t27frMcy1ZskTz5s37/MOeps2bN+vvf/+76urq9L//+78hP5/NZpPN
Zjvjrw2V1tZWXXvttRowYIASExP1q1/96pSv3b9/v+bMmaOkpCTZ7Xbt3bv3tI5VXl6uyZMnq3//
/poyZYoqKipC8p4AfDVRwgGEzCOPPKIf/vCHuvPOO3XgwAF98MEHWrx4sV566aUvdFybzabP8z1j
4SiR7e3tp/X6PXv2aMSIEYqKijrtc/n9/tPeR9LnyjJclixZoqqqKu3du1evvPKKfvGLX+ivf/3r
SV9rt9v1zW9+U2vWrDntY7W1temSSy7R/Pnz9fHHH+uaa67RJZdcIp/PF7L3BuCrhRIOICSOHj2q
e+65R48//rguvfRSGYYhh8OhgoICPfTQQ5KOX4m8+eablZSUpKSkJP3whz9UW1ubJOnQoUO66KKL
FBsbq0GDBmn69OkKBAKaN2+e9u7dq4svvlhut1sPP/zw55rv01fLH3roISUnJ8vj8SgzM1OlpaX6
y1/+ogcffFC///3v5Xa79bWvfU2SVFdXpzlz5mjQoEFKT0/Xb37zm+BxlixZossuu0zz5s3TgAED
9POf/1z9+/fXkSNHgq/ZunWrEhISuhT03/72t1q4cKHeeOMNud1u/fSnP5UkrVixQunp6Ro0aJAu
ueQS7du3L7iP3W7X448/rvT0dGVkZJz0vRYWFioxMVExMTHKycnRzp07T5lJcnKyHnzwQcXHxysl
JUXPPfec6TVHjhzRRRddJI/Ho2nTpunf//538LmbbrpJw4YN04ABAzRlyhS99tpr3f4dfB4rV67U
XXfdpQEDBigzM1M33HCDnn766ZO+NiEhQd/73vc0ZcqU0z7Wq6++qvb2dt10001yOp36z//8TwUC
gW7/BQYATgclHEBIvPHGG2ppadG3vvWtU77mgQce0FtvvaWKigpVVFTorbfe0v333y9J+q//+i8N
HTpUhw4d0oEDB/Tggw/KZrNp1apVGjZsmNavXy+v16v/9//+3xeedffu3Vq2bJnefvttNTQ06G9/
+5tGjBih2bNn6/bbb9fll18ur9erbdu2SZIuv/xyDRs2TPv27VNxcbFuv/12vfLKK8HjvfTSSyos
LNTRo0f1ox/9SLm5uVq9enXw+VWrVumKK66Qw+EwzXHdddfpiSeeUHZ2trxer+655x6Vlpbq9ttv
1x/+8Aft27dPw4cP1+WXX27a78UXX9SWLVtOWa4LCgr0/vvv6+DBg8rKytJVV111yiw++ugjHT58
WHV1dfqf//kf3XDDDfrXv/4l6fgV8xdeeEFLlixRfX29Ro4cqTvuuCO479e//nVVVFSovr5eV155
pQoLC4O/VH3az3/+c8XGxp70z8CBA0+6T319vfbt26eJEycGt02YMEE7duw45fs5lc861o4dOzRh
wgTTPhMnTvxc5wKAk6GEAwiJw4cPKy4uTnb7qf8389xzz+nuu+9WXFyc4uLidM8992jVqlWSpMjI
SO3bt081NTVyOBz6xje+cVrnr6ur61LuTnVl1uFwqLW1VTt27JDP59OwYcOUmpoq6XjxPHG5xgcf
fKB//OMfeuihhxQZGamJEyfq+uuv18qVK4OvOeecczRnzhxJUlRUlObPn69nnnlG0vHlKS+88MIp
15l/emnIs88+q+uuu06TJk1SZGSkHnzwQb3xxhum9c233XabYmJi5HK5TnrMBQsWqH///nI6nbrn
nntUUVEhr9d7yuzuu+8+OZ1OTZ8+XQUFBaZfIObOnaspU6bI4XDoqquuUnl5efC5q666SrGxsbLb
7brlllvU2tqq3bt3n/QcP/nJT1RfX3/SPyf+q8GJjh07JkkaMGBAcJvH4+n2vZzKZx3r2LFjpue+
yLkA4GQo4QBCYtCgQTp06JA6OjpO+Zq6ujoNHz48+HjYsGGqq6uTJP34xz/WyJEjdcEFFygtLS24
hKWnhgwZ0qXcnXvuuSd97ciRI/Xoo49qyZIlGjx4sK644grTko9Pzzxw4ED179/fNPeHH34YfJyc
nGza55JLLtHOnTtVU1OjDRs2BJdr9ETn1e9O/fv316BBg0znO9mHUDt1dHToJz/5iUaOHKkBAwYo
JSVF0vHlPicTGxsrwzCCj4cPHx7MwmazafDgwcHnDMMIlllJevjhhzVmzBjFxMQoNjZWR48ePeV5
Po/o6GhJUkNDQ3Db0aNH5Xa7z/ixoqOjTc91Pu/xeE77XABwMpRwACGRnZ0tl8uldevWnfI1Q4YM
UU1NTfDx3r17NWTIEEnHS9DDDz+sqqoqvfTSS3rkkUeCSz5C8eHKK664Qps3b9aePXtks9l06623
nvRcQ4YM0ZEjR0zlc+/evabi/el9oqKiVFhYqGeeeUbPPPOM5s+f3+O5Pp1RY2OjDh8+rKSkpFOe
70TPPvusXnrpJW3cuFFHjx5VdXW1JPMV9xP3r6+vV1NTU/Dxnj17gn8n3dm8ebN++ctf6g9/+IM+
/vhj1dfXa8CAAaf80OfPfvYzud3uk/45VdGNjY1VYmKi6ep7RUWFxo0b95nzne6xxo4dq3fffde0
z7vvvquxY8ee9rkA4GQo4QBCYsCAAbr33nu1ePFivfjii2pqapLP59Of//znYMG94oordP/99+vQ
oUM6dOiQ7r333uAyjfXr1+v9999XIBCQx+ORw+EILm0ZPHiwqqqqztis//rXv1RaWqrW1la5XC5F
RUUF12ufddZZqqmpCZbJoUOH6pxzztFtt92m1tZWvfvuu3rqqad09dVXd3uO+fPn63e/+51eeuml
07rl4RVXXKHf/e53qqioUGtrq26//XZNmzZNw4YN69H+x44dk8vl0sCBA9XY2Kjbb7/d9Pynl9tI
0j333COfz6fNmzfr5ZdfVmFhYfC1p+L1ehUREaG4uDi1tbXp3nvv7XIl+US33367vF7vSf90t9/8
+fN1//336+OPP9Z7772n3/zmN1qwYMEpX9/S0qKWlpYuP3/WsXJzc+VwOLR06VK1trZq6dKlstvt
Ov/88095LgA4HZRwACFzyy236JFHHtH999+vhIQEDRs2TI8//njww5p33nmnpkyZogkTJmjChAma
MmWK7rzzTknS+++/r1mzZsntduucc87R4sWLlZOTI+n4Guj7779fsbGxeuSRR0567p5cLe98TWtr
q2677TbFx8crMTFRhw4d0oMPPihJwQI6aNCg4BKS559/XjU1NRoyZIjmzp2re++9N1jOTnUbxG98
4xuy2+2aPHlyt8tHPr3/zJkzdd999+nb3/62hgwZourqar3wwgs9fp/z58/X8OHDlZSUpHHjxik7
O9u0z6fPd9ZZZyk2NlZDhgzRvHnztHz5co0aNeqU763z8ezZszV79myNGjVKI0aMkGEYPf5F4XT8
9Kc/VVpamoYPH64ZM2bo1ltv1QUXXBB83u12m+5D369fP3k8HtlsNmVmZpqWEXV3rMjISJWUlGjl
ypWKjY3VypUrVVJSooiIiDP+ngB8NdkCX6YbxALAl1heXp6uvPJKXXvtteEe5aReffVVzZs3Tx98
8EG4RwGAPo9f6QHAAlu2bNHWrVv14osvhnsUAEAvwHIUAAixa665RrNmzdKjjz5qWg7RG4X7a+kB
4KuC5SgAAACAxbgSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAA
AFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAA
WIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYLCLUJ/D5fHr66afl9/vV3t6uzMxM
5eXlqbS0VLt375Yk9evXT5deeqkGDBggSdq8ebO2bdsmm82m/Px8jRw5UpJUV1enkpIS+f1+paen
Kz8/X5Lk9/u1bt067du3T4ZhqLCwUDExMZKk8vJybdq0SZI0ffp0TZo0SZJUX1+v4uJiNTc3KzEx
UXPnzpXD4Qh1HAAAAIAcS5YsWRLSEzgcGj9+vKZNm6bJkyfrlVdeUVxcnMaMGaNp06bp7LPPVmtr
q7Zv367MzEwdOHBAZWVlWrRokTIyMlRcXKypU6fKZrPp+eef10UXXaRZs2bpzTfflGEYGjRokN5+
+221tbVp3rx5crlcevPNNzV27Fg1NTVp7dq1uuGGGzR58mStXbtWkyZNUkREhP74xz8qKytLF198
saqrq+X1epWUlBTKKAAAAABJFi1HiYyMlCS1t7crEAjIMAy5XK7g821tberXr58kaffu3Ro/frwc
DodiY2M1cOBA1dbWyuv1qq2tTcnJyZKkiRMnateuXcF9Oq9wjx49WtXV1ZKkqqoqpaWlyTAMGYah
1NRUVVZWKhAIqKamRmPGjOlyLAAAACDUQr4cRZI6Ojq0fPly1dfXa8qUKUpISJAkbdy4URUVFXI6
nVq4cKEkyev1Bou2JHk8Hnm9XjkcDnk8ni7bO/fpfM7hcMjlcqmpqcm0/cR9mpubFRUVJbvd3uVY
DQ0NOnbsmGn+6Oho03EAAACAL8KSEm6327Vo0SK1tLRo1apVqq6uVkpKimbOnKmZM2dq8+bN+stf
/qJLL73UinG69c4776isrMy0LScnRzNmzAjTRAAAAOhrLCnhnaKiojRq1CjV1dUpJSUluH38+PF6
9tlnJUlut1tHjx4NPtfQ0CCPxyO3262GhoYu20/cx+PxqL29Xa2trerXr5/cbrdqampM+6SkpMgw
DLW0tKijo0N2u10NDQ1yu92SpMmTJysjI8M0d3R0tOrr6+X3+894JqfD5XKptbU1rDNEREQoNjaW
PE5AJmbkYUYeZuRhRh5dkYkZeZh15tEXhLyENzY2ym63yzAM+Xw+VVVVKTc3V4cPH9agQYMkHV/T
nZiYKEnKyMjQmjVrlJ2dLa/XqyNHjigpKUk2m00ul0u1tbVKSkpSRUWFpk6dGtynoqJCQ4cO1c6d
O4MFPy0tTRs3blRzc7Ok42vE8/LyZLPZNGLECO3cuVPjxo1TeXm5MjMzJR1fmnKypScHDx6Uz+cL
dVzdioiICPsMnfx+f9hn6U15SGTyaeRhRh5m5GFGHl2RiRl59D0hL+HHjh3TunXrFAgEFAgENHHi
RKWmpur3v/+9Dh8+LJvNpoEDB6qgoECSlJCQoLFjx2rZsmWy2+0qKCiQzWaTJBUUFKikpEQ+n0/p
6elKT0+XJGVlZWnt2rVaunSpDMPQZZddJun4rQ9zcnK0YsUKSVJubq4Mw5AkzZo1S8XFxSotLVVi
YqKysrJCHQUAAAAgSbIFAoFAuIf4MugNV8INwwhe1Q8Xp9Op+Ph48jgBmZiRhxl5mJGHGXl0RSZm
5GHWmUdfwDdmAgAAABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOEAwAAABaj
hAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOE
AwAAABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QD
AAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFrMFAoFAuIfo7VpaWtTS0qJwR2W329XR0RHWGWw2myIj
I9XW1kYenyATM/IwIw8z8jAjj67IxIw8zGw2m2JiYsI6w5kSEe4BvgyioqLk9Xrl8/nCOodhGGpu
bg7rDE6nUzExMWpsbCSPT5CJGXmYkYcZeZiRR1dkYkYeZk6nM6znP5NYjgIAAABYjBIOAAAAWIwS
DgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIO
AAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4A
AABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWCwi1Cfw
+Xx6+umn5ff71d7erszMTOXl5elvf/ub/vWvf8nhcCg2NlaXXnqpoqKiJEmbN2/Wtm3bZLPZlJ+f
r5EjR0qS6urqVFJSIr/fr/T0dOXn50uS/H6/1q1bp3379skwDBUWFiomJkaSVF5erk2bNkmSpk+f
rkmTJkmS6uvrVVxcrObmZiUmJmru3LlyOByhjgMAAAAIfQl3Op265pprFBkZqfb2dj311FPas2eP
0tLSlJeXJ7vdrg0bNmjz5s2aNWuWDhw4oO3bt2vx4sVqaGjQypUrVVRUJJvNpvXr12vOnDlKTk7W
M888o8rKSqWnp2vr1q0yDENFRUXavn27NmzYoMLCQjU1NamsrEw33HCDJOnJJ59UZmamoqKitGHD
BmVnZ2vcuHFav369tm7dqrPPPjvUcXypBQIBvfDCCzpy5IjOO+88ZWZmhnskAACALyVLlqNERkZK
ktrb2xUIBGQYhtLS0mS3Hz99cnKyGhoaJEm7d+/W+PHjg1fIBw4cqNraWnm9XrW1tSk5OVmSNHHi
RO3atSu4T+cV7tGjR6u6ulqSVFVVpbS0NBmGIcMwlJqaqsrKSgUCAdXU1GjMmDFdjoVTW7JkiYqK
irRkyRIVFBRo+/bt4R4JAADgSynkV8IlqaOjQ8uXL1d9fb2mTJmihIQE0/Pbtm3TuHHjJElerzdY
tCXJ4/HI6/XK4XDI4/F02d65T+dzDodDLpdLTU1Npu0n7tPc3KyoqKjgLwEnHquhoUHHjh0zzRcd
Ha2ICEui6pbD4ZDT6Qzb+f/4xz8Gf25padHGjRv1ta99LWzzhDuPTp3/bfDfyHHkYUYeZuRhRh5d
kYkZeZj1hhzOFEveid1u16JFi9TS0qJVq1apurpaKSkpkqRNmzbJ4XBowoQJVozymd555x2VlZWZ
tuXk5GjGjBlhmqj3SEtL00cffRR8PHbsWMXHx4dxot4lNjY23CP0KuRhRh5m5GFGHl2RiRl59D2W
/joRFRWlUaNGqa6uTikpKdq2bZsqKys1f/784GvcbreOHj0afNzQ0CCPxyO32x1csnLi9hP38Xg8
am9vV2trq/r16ye3262amhrTPikpKTIMQy0tLero6JDdbldDQ4PcbrckafLkycrIyDDNHR0drfr6
evn9/lDE0mMul0utra1hO/+vfvUrFRUVqba2VnPmzNHs2bN18ODBsM0T7jw6RUREKDY2lv9GPkEe
ZuRhRh5m5NEVmZiRh1lnHn1ByEt4Y2Oj7Ha7DMOQz+dTVVWVcnNzVVlZqX/84x9asGCB6Z82MjIy
tGbNGmVnZ8vr9erIkSNKSkqSzWaTy+VSbW2tkpKSVFFRoalTpwb3qaio0NChQ7Vz587gVfa0tDRt
3LhRzc3Nko6vEc/Ly5PNZtOIESO0c+dOjRs3TuXl5cEPGXo8HtMSlk4HDx6Uz+cLdVzdioiICOsM
ycnJ+uMf/6j4+HjyOAm/3x/2eXpTJuRhRh5m5GFGHl2RiRl59D0hL+HHjh3TunXrFAgEFAgENHHi
RKWmpmrp0qVqb2/XqlWrJB0veBdddJESEhI0duxYLVu2THa7XQUFBbLZbJKkgoIClZSUyOfzKT09
Xenp6ZKkrKwsrV27VkuXLpVhGLrsssskSf369VNOTo5WrFghScrNzZVhGJKkWbNmqbi4WKWlpUpM
TFRWVlaoowAAAAAkSbZAIBAI9xBfBr3hyq9hGMGr+uHidDp7zZXw3pCHRCafRh5m5GFGHmbk0RWZ
mJGHWWcefQHfmAkAAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABY
jBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiM
Eg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwSDgAAAFiMEg4AAABYjBIOAAAAWIwS
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
hHUGm82myMhItbW1kccnyMSMPMzIw4w8zMijKzIxIw8zm82mmJiYsM5wpkSEe4Avg6ioKHm9Xvl8
vrDOYRhddw+3AAAgAElEQVSGmpubwzqD0+lUTEyMGhsbyeMTZGJGHmbkYUYeZuTRFZmYkYeZ0+kM
6/nPJJajAAAAABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMA
AAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOEAwAA
ABajhAMAAAAWo4QDAAAAFqOEAwAAABajhAMAAAAWo4QDAAAAFqOEI+S2bNmia665RgsXLlRlZWW4
xwEAAAi7iHAPgL5t//79uuqqq9TY2ChJ2rp1q1577TUZhhHmyQAAAMKHK+EIqcrKymABl46X8v37
94dxIgAAgPCjhCOkMjMzNWDAgODjoUOHasiQIWGcCAAAIPxCvhzF5/Pp6aeflt/vV3t7uzIzM5WX
l6empiYVFxfr448/VkxMjAoLC4NLFDZv3qxt27bJZrMpPz9fI0eOlCTV1dWppKREfr9f6enpys/P
lyT5/X6tW7dO+/btk2EYKiwsVExMjCSpvLxcmzZtkiRNnz5dkyZNkiTV19eruLhYzc3NSkxM1Ny5
c+VwOEIdx1dOfHy8Vq9erV//+teKjIzUzTffLJfLFe6xAAAAwirkJdzpdOqaa65RZGSk2tvb9dRT
T2nPnj3avXu3UlNTde655+q1117Ta6+9plmzZunAgQPavn27Fi9erIaGBq1cuVJFRUWy2Wxav369
5syZo+TkZD3zzDOqrKxUenq6tm7dKsMwVFRUpO3bt2vDhg0qLCxUU1OTysrKdMMNN0iSnnzySWVm
ZioqKkobNmxQdna2xo0bp/Xr12vr1q06++yzQx3HV9K4ceO0bNmycI8BAADQa1iyHCUyMlKS1N7e
rkAgIMMwtHv37uBV6YkTJ2rXrl2SpN27d2v8+PFyOByKjY3VwIEDVVtbK6/Xq7a2NiUnJ590n85j
jR49WtXV1ZKkqqoqpaWlyTAMGYah1NRUVVZWKhAIqKamRmPGjOlyLAAAACDULLk7SkdHh5YvX676
+npNmTJFCQkJamxsVHR0tCQpOjo6+OE9r9cbLNqS5PF45PV65XA45PF4umzv3KfzOYfDIZfLpaam
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
OVu2bOGyyy5j+/btNG3aFIC4uDiWLVtGUVERUDlHvEePHlgsFpo0acL27dtp06YNmzdvpmXLlkDl
COa5o5jARXEPaD8/P6/3oUp5ebnX+3Ix5QHmTJKTk9m4cSN5eXlERkZisVg80teLKRPtI2bKw0x5
mCmPmpSJmfKofS54EX7w4EG2bt1KgwYNeOeddwDo3r078fHxbNu2jTZt2ph+PioqisTERCZPnozV
auWGG27AYrEAcMMNN5CRkUFZWRnx8fHEx8cDkJSUxJw5c5g0aRJ2u52hQ4cCEBQURNeuXZk6dSoA
3bp1w263A9CzZ0/S09P54osviI6OJikp6UJHIT4mICCAqKgob3dDRERELkIWt9vt9nYnLgUXw0i4
3W43RvW95WL6dsiLIQ/49ZkcO3aMv//97zidTkaOHEmnTp3OW18uhky0j5gpDzPlYaY8alImZsrD
rCqP2qD2XGIqcom47bbbjFtifv7553z++efGFCoRERHxDfraehEPysvLM92Tvri4mK1bt3qxRyIi
IuINKsJFPCg0NJS4uDhjuU6dOiQmJnqxRyIiIuINmo4i4kEWi4WPP/6Y559/HqfTyahRo2jevLm3
uyUiIiIepiJcxMNiY2OZPHnyj7aVl5ezcuVKbDYbXbp0Me4MJCIiIrWLinCRi0R5eTm33347K1eu
BKB///7GbT1FRESkdtGccJGLxObNm40CHGD+/Pnk5OR4sUciIiJyoagIF7lIBAcHm5YtFovx5VIi
IiJSu6gIF7lItGrVigceeAAAq9XKn//8Zxo2bOjlXomIiMiFoCJc5CLy+OOPs2PHDnbu3Mm9995r
anvqqaeIi4ujU6dOfPPNN17qoYiIiJwPKsJFLjKhoaE1pqYsWrSI9957j+LiYg4dOsTYsWO91DsR
ERE5H1SEi1wCjh8/blo+efKkl3oiIiIi54OKcJFLQK9evYiIiDCWb7nlFlN7dnY27777Ll988YWn
uyYiIiK/ge4TLnIJaNSoEQsXLmTJkiVERETQr18/o+2rr77illtuoaysDIDnnnuOO++800s9FRER
kV9CI+Eil4iYmBhGjhxJ//79Td+kOXfuXKMAB5g5c6Y3uiciIiK/gkbCRS5x597GsEGDBsZjt9vN
+++/z44dO+jSpYtpBF1ERES8RyPhIpe4++67j759+xIUFERycjITJ0402l599VUmTJjAhx9+yL33
3su8efO82FMRERGpopFwkUuc3W5n6tSpxuOioiKjbfny5aafzcrKYuDAgcbytm3bOHnyJCkpKYSE
hHimwyIiIqKRcJHaLCEhwbTcokUL4/HUqVPp1asXt912G3379iU3N9fT3RMREfFZGgkXqcWeeeYZ
Kioq2L59O9deey2jR4822l599VXj8d69e5k3b55xV5XS0lLmz59PaWkp/fv31yi5iIjIeaYiXKQW
CwkJ4fXXX//RtsDAQPLz803LAC6Xi5EjR/Lll18C8K9//YvMzEzsdvsF76+IiIiv0HQUER/14osv
GoV3t27dGDJkCACHDh0yCnCA7du3s2nTJmP5/fffp2PHjlx//fWsX7/eo30WERGpLTQSLuKjevXq
xdatW8nLyyM6Otq493hoaCh16tShtLQUAIvFQv369QH49ttvmTBhAm63G4CRI0eyefNm/P39AViw
YAH/+c9/SEhIYOzYsdSpU8cL70xEROTipyJcxIcFBwcTHBxsWhcWFsZrr73Gk08+SWlpKY8++qhx
gefhw4eNAhzgzJkzOJ1OwsPDWbFiBffdd5/R/t133/HWW28Blfcrnzp1Khs2bKBDhw7cd999WK06
ESciIr5LRbiI1DBo0CAGDRpUY/1VV11Fw4YNOXbsGABXX3014eHhAGzYsMFUoH/11VfG46lTp/LM
M88AsHDhQsrKynjwwQcBOHbsGA8//DD79++nd+/ePPXUU6ZvBM3JycHpdNK6dWv8/PRfloiI1A76
RBORX6x+/fpkZmYya9YsQkJCuO2224y2du3amX62Q4cOxuNz545XX37kkUfIysoCYMqUKTRv3tzY
7jvvvMPEiRNxu9107tyZjz76yJjisn37diZPnozVauXBBx+kefPmxjaLi4vZtGkTjRo1onHjxufp
3YuIiJw/Oh8sIr9KTEwM48eP5+677zbdMaVnz568/PLLdO3aldGjRzNp0iSjrX379qZtVF/Oyckx
te3fvx+AsrIynn/+eWN0fc2aNSxduhSA3Nxcbr75ZjIyMpgzZw433XQTBQUFABQUFDBo0CCGDh1K
586deeedd4xtl5WV8dBDD9G+fXuGDh1qjOhD5V1hpk6dyoMPPsjMmTNrvO8vvviCjz/+mKNHj9Zo
2717N9nZ2aYzAVXOnj1LSUlJjfUiIuLbNBL+CxQXF+Pv7+/1U+FWq9Xrt4mzWCwUFhYqj2qUyX+N
GjWKu+++27iws6oo/cMf/gBUTlFJTk7mscceM7Lq378/b775JgB+fn7069cPu92On5+faVoKVN5G
0W638+2333L69Glj/fHjxzl+/DiJiYlkZGTw7bffGm0vv/wy48ePx2KxMHXqVKPAPnXqFH/605/4
6KOPAHjhhRd46aWXAEhPT8ff35/hw4cDMHHiROO+6hERESxbtozLLrsMgGeffda4DWS/fv2YNm2a
Md99woQJvP322/j7+/P6669z6623ApUF/6OPPsqsWbOIjY1l6tSptG7dGoCSkhIee+wx1qxZwxVX
XMErr7yCw+EAID8/nwkTJrBnzx769OljTOmpyuCvf/0rZ86c4Y477qBnz55G2969e3njjTewWCyM
GzeOuLg4o+2bb77h448/JiwsjHHjxhEaGmq0LVu2jCVLlhAfH89dd91lmsc/e/ZsNm/ezNVXX02f
Pn2M9RUVFXzwwQccPnyY/v37mw64CgsLmTp1KqWlpdx0001ER0cbbSdOnOCTTz4hICCAESNGEBQU
ZLR99913LFy4kOjoaG666SbTfrFu3TrWrl1L27Zt6d69u2l/WbJkCTt37qRbt26mMzUul4v09HR+
+OEH+vfvT2xsrNFWUFDAzJkzcblc3HTTTUb2UDl1at68edSrV4+hQ4dis9mMtp07d7J8+XKaNWtG
7969Tf346quv2LRpE1deeSUpKSmmtkWLFnH06FGuu+46mjVrZqwvLy8nPT3dOKisujgaKveD2bNn
U6dOHYYOHUpAQIDRdujQIRYvXkyDBg0YMGCA6bW+/fZb1qxZQ2JiItdcc42pbcWKFezcuZOrr76a
xMREY73b7SYzM5OTJ0+SlpZGTEyM0VZcXMzs2bMpLy9nyJAhpqxOnTpFZmYmoaGhDB482JTVnj17
WL58OU2aNDHtpwBff/01mzZtomPHjrRv3970f+rSpUvZv38/119/vWkfrqioYO7cueTn5zNgwAAi
IiKMNqfTyZw5c/Dz86uR1ZEjR1i0aBGRkZEMGDDAtF9t376dVatW0bp16xpZrV69mm3bttG5c2fa
tGljaps/fz7Hjx+nT58+pv2qpKSE2bNnU1paypAhQ0x/Z6dPn2bevHkEBwczZMgQ03vet28fy5Yt
Iy4uju7du5vaNm7cyNdff80VV1zBVVddZerH559/Tk5ODt26dSM+Pt5Y73K5mDt3Lnl5efTr14+o
qCijraCggNmzZ2O1Wrnxxht/9LPE258xQI3PhUuZxf1jQzdSw8mTJykrK/NqH879SnJv8Pf3JzIy
UnlUo0zMfm0ebrebGTNmkJOTQ48ePUwfJu+99x5/+ctfcLvddOvWjffffx8/Pz9Onz5Nly5dOHPm
DFBZGK9evZqQkBDmzp3L/fffb2wjJCSEXbt2AZVF8bRp04y21q1bG6PrgwcPNk2TGTJkiHFwkJiY
aLwWwJ///Gfuu+8+Tp06VWOUPz09ndTUVDZs2GCaV+/v7092djYhISHMmjWL8ePHG22JiYksWbIE
qDxoqH5v99/97ne88MILAIwdO5Z58+YZba+//jrDhg0DIC0tja1btxqvtXDhQlq3bo3T6aRr164c
P34cgIYNG5KVlUVISAh79+6ld+/exj6TmppKeno6UFmUDR8+3DiQuvfee3nqqaeM30vVY4DJkycb
7/Wxxx7jww8/BCoPmjIzM0lMTMTtdjN06FDjWoFGjRqxZMkSwsLCyM/Pp3fv3hw8eBCAjh07kp6e
jtVqZc+ePdxwww2cPXsWgDvvvJPnnnsOqDw7ceedd1JRUQHASy+9ZExlevfdd3n22WcBqFOnDjNn
zuTKK68E4KGHHjIOxiIiIli8eDHR0dGUlZUxZMgQNm7cCECbNm3IzMwkICCAH374gV69ehlnTwYO
HGhceJydnc3AgQMpLi4G4PHHH+eBBx4AIDMzk7Fjx+J2u7HZbPzzn/+kV69eNX7XISEhLFiwwCiY
Ro0axeLFiwFo0qQJCxcupG7duhQVFdGvXz927twJwDXXXMMnn3yC1Wrl8OHD9OnTx/j221GjRhkZ
rF27luHDhxt3PXrllVe45ZZbAPjggw94/PHHAQgICODTTz81snryySd5//33jawWLVpEo0aNqKio
4Oabb2bt2rVA5T6cmZlJYGAgubm5pKWlcejQIaDyQLvqjNSuXbvo37+/cebq0UcfNQ4mFy9ezOjR
o3G5XFitVv71r38ZRfqkSZN48cUXgcoLyufPn29cMD5mzBgyMzMBuPzyy1m4cCFhYWEUFxczcOBA
srOzgcr9+9NPP8Vms3H06FHS0tI4depUjf1qw4YN3HzzzcYZrBdffJHbb78dgBkzZhiDCnXq1OGT
Tz6hU6dOAPzlL3/hn//8JwDh4eEsWrSI2NhYXC4Xw4cPZ+XKlQC0atWK+fPnY7fbyc/PJy0tzTgD
mJaWZmxjz5499OvXD6fTCcAf//hH4/+Nzz//nLvuuouKigqsVitvv/02/fr1A+Dtt99m4sSJAAQF
BZGRkWEcWD3wwAPMmTMHqDyruXjxYsLDwyktLWXQoEFs2bIFqLz+Z9asWTUGli6mz5jaQNNRRMSr
LBYLt956K08++WSN0ZxRo0axbt06li1bxgcffGB8IISHh/PJJ5/Qp08f+vbty4wZM4xv9ezXrx/d
unUDKv+z/tvf/mZsr1+/fqYPlYEDBxqPq4/+nbscFhZmaqsalfyxEZmq0eKqD84qZWVlxod69Wkw
5y7v27fP1FZ9edu2baa2quKirKzMKMDPXc7JyTEK8KrXqtrmhg0bTB+oa9euNQ6cli1bZppe88UX
XxiPP/vsM1M/qi8vXLjQeFxcXMyyZcuAypHu6hfrHj16lG+++QaoHNGrKsChcnT7+++/BypHP6sK
cIC5c+cajzMyMowCHDCKC8A4mIDKb4CtOnhxuVzMnj3baDt16hTLly8HKs8YVBXgUJnv9u3bgcqD
kuq/p3nz5hlFd2ZmpvEY4NNPPzUez5w508ixoqLC1K8ZM2YYj8+ePcuCBQuAypHRqgIcKqdoVWW3
ceNGowAHWLVqFYcPHwYqi9iqAvzc7aenpxsFOMAnn3zyo4+rRmx/bBunTp0yDlpzcnKMAhwq982q
M1CrVq0yCnCoHB2u+h3OmzfPKMDPfe1PP/0Ul8sFVP6eqr/2xx9/bDwuKCgwiu6zZ88ajwEOHjzI
6tWrAdi6davxNwKV+3dVsbtkyRKjAD+3H+np6aYpZNXbqvejtLTU9Pus3nb69Gnj7+LQoUNGAQ6w
Y8cO47sX1qxZY/QJKs+MVP0O58+fb/p/pOrgtiqrqn3f5XKZ9rmqs3tQefapKp/i4mLT38iRI0dY
sWIFUPn7qyrAofK6nb179yIXlopwEbmoxcTE0LJlyxq3NGzXrh3vvfceU6dOpVWrVsZ6f39/Pvjg
A9asWcOOHTu48cYbjbbU1FTmzJnDI488wrvvvmsaMZ8wYQJ33nknKSkpjBs3jtGjRxttkyZNIjo6
Gj8/P4YNG2Zss379+jz88MPGzw0cONA4kOjcubPp4tRbbrnFKN7T0tKMgwbAGM0Gapyerxo1rdpm
dVdffbXxnqtPt/D39zdG6C+77DLq1q1rtNWrV8+YSpOQkGA6kIiLizPu+V79FDZguvC1adOmprbq
y+deCFu1XLduXdMpeKvVakxtaNSoken3GxwcTL169Yy26qovV5/Ocu5yw4YNTW1Vy1artcYoWoMG
DYDKg7uq9w9gs9mMqQ1VP1MlLCzMmNpQ/ZT+ua997vOqL5/7vKrlH7t1aFWfIyMjTb+zgIAAI9dz
31f15d/aVn1qR/W2sLAwU1ZWq9W4U9K578vhcBhfDHZu2//aj8DAQNM0mOpt9evXN2Xl7+9v7Ffn
9qP69s93W926dU3TYCwWi9F27nsOCgoypmKd21Z9+z+X40/1o06dOsb7P7etfv36pr9BPz+/Gj8r
55/t6aefftrbnbgUFBYWGkfo3uLv7095eblX+2Cz2QgODlYe1SgTs4shD4vFQr169QgNDa2RR6NG
jUhNTaVFixam9f7+/nTv3p1bb72Va665xvSBFB0dzT333MODDz5IWlqa6YO9c+fODB06lNtvv50R
I0YYbX5+fgwePJikpCTGjBnDyJEjjTzCw8NJS0vjsssuY/jw4aaCv1WrViQmJtKgQQPuuusu0x1o
unbtSkBAAA0bNuTBBx+kb9++RluvXr3Iy8sjNjaWp556yphOYLfb6dy5M99//z1xcXG8/PLLRtEc
HR3N5ZdfzokTJ2jVqhWTJk0yRv3btm1LaWkp+fn5XHXVVbz44otGcdCpUycOHTpESUkJffr04ckn
nzTOMHTu3Jlt27ZhtVq54447uPvuu408kpKS2LJlCyEhITz11FPGGYv69evTsGFDsrOziYiI4I03
3jAOAlq2bMnZs2fJycmhWbNm/OMf/zAKh+TkZPbu3cvJkydJSkri73//u9HHjh078s0331BQUFCj
jykpKaxduxaXy8Xo0aMZMWIEUFn8NmnShPXr1xMYGMjEiRONA5/LLrsMt9vNtm3biIqK4h//+AeX
X365kdWBAwc4cOAA8fHxvPHGG0ZBmpKSwubNmzl16hSpqan87W9/MwrSlJQU1q1bR1FRETfeeCMP
PfQQVqsVPz8/EhMTWbNmDVB5TUXVdJ/69etTr149vv76axwOBy+//LJxwJWQkMAPP/zArl27iImJ
4a233jIOCDp06MD27ds5evQobdu25dVXXzWK9yuvvJL169dz5swZunfvztNPP20U2B06dGD16tWU
lpZyxx13cM899wCVxWLjxo1Zs2YN/v7+PPXUU1x//fUAxlzozZs3U79+fd58801jvntiYiIHDhww
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
ly5dLuhrdevWjffee8+0zul00qRJkwv6uiIi8uuoCBcRucAsFst52U55ebnHXktERC4sFeEiIh6w
Y8cOxowZw9q1a3E4HISHhwNQUlLCI488QuPGjWnYsCFjxoyhuLgYgC+//JLY2FheeukloqOjGTVq
FGfOnKFfv35ERUURHh5O//79OXLkCAATJkxg5cqV3H///TgcDsaNGweA1Wpl3759AOTl5TFixAii
oqJo0qQJzz33HG63G4Bp06ZxzTXX8Mc//pHw8HCaNWvG4sWLPR2ViIhPUBEuIuIBrVu35p133iE1
NRWn08np06cBePzxx9mzZw9btmxhz549HDlyhGeffdZ43vHjx8nNzeXgwYO8++67uFwuRo0axcGD
Bzl48CB2u537778fgOeee44uXbowefJknE4nkyZNqtGPBx54AKfTSU5ODllZWUyfPp1///vfRvv6
9etp2bIlP/zwA48++iijRo26wMmIiPgmFeEiIh7gdruNEefq66ZOncqrr75KvXr1CAkJ4YknnmDG
jBnGz1itVp555hn8/f0JDAwkPDycwYMHExgYSEhICE8++SRZWVk1tvtjKioq+PTTT3n++ecJDg6m
cePG/OEPf+CDDz4wfqZx48aMGjUKi8XCiBEj+P777zlx4sR5TEJERAD8vN0BERFf8GNztU+ePElh
YSHJycnGOrfbjcvlMpYjIyOpU6eOsVxYWMhDDz3EZ599Rm5uLgBnz57F7XYbr/FT88JPnTpFWVkZ
jRs3NtZdfvnlxnQWgIYNGxqPg4KCjO1HRUX9qvcrIiI/TyPhIiIecm5xHBERgd1uZ/v27eTm5pKb
m8uZM2fIz8//yee88sorfPfdd6xfv568vDyysrJMo+w/d2FmREQE/v7+ptsVHjx4kNjY2PPw7kRE
5NdQES4i4iENGzbk8OHDlJWVAZVTTUaPHs348eM5efIkAEeOHGHJkiU/uY2zZ89it9upW7cup0+f
5plnnjG1N2jQgL179/7oc202GzfddBMTJkzg7NmzHDhwgNdee43bb7/9PL1DERH5pVSEi4h4yPXX
X09iYiINGzY0pne8+OKLNG/enE6dOlG3bl169uzJd999Zzzn3JHt8ePHU1RUREREBJ07dyYtLc30
Mw8++CDp6emEh4czfvz4Gn148803CQ4OplmzZnTp0oXbbruNkSNHGq917uvplociIheGxf1TV/CI
iIiIiMgFoZFwEREREREPUxEuIiIiIuJhKsJFRERERDxMRbiIiIiIiIepCBcRERER8TAV4SIiIiIi
HqYiXERERETEw1SEi4iIiIh42P8D+PGrn5hJ5PoAAAAASUVORK5CYII=
"
>
</div>

</div>

<div class="output_area"><div class="prompt output_prompt">Out[9]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;ggplot: (276641365)&gt;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Goodness-of-Fit">Goodness of Fit<a class="anchor-link" href="#Goodness-of-Fit">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>After making predictions, use the coefficient of determination(R^2) to see how the model performed</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[10]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="c">#Compute the coefficient of determination (R^2) given</span>
<span class="c"># a list of original data points and a list of predicted data points</span>
<span class="n">sg_data_predictions_diff</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">((</span><span class="n">values</span> <span class="o">-</span> <span class="n">predictions</span><span class="p">)</span> <span class="o">**</span> <span class="mi">2</span><span class="p">)</span>
<span class="n">mean</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">mean</span><span class="p">(</span><span class="n">values</span><span class="p">)</span>
<span class="n">sg_data_mean_diff</span> <span class="o">=</span> <span class="n">np</span><span class="o">.</span><span class="n">sum</span><span class="p">((</span><span class="n">values</span> <span class="o">-</span> <span class="n">mean</span><span class="p">)</span> <span class="o">**</span> <span class="mi">2</span><span class="p">)</span>

<span class="n">r_squared</span> <span class="o">=</span> <span class="mi">1</span> <span class="o">-</span> <span class="n">sg_data_predictions_diff</span> <span class="o">/</span> <span class="n">sg_data_mean_diff</span>

<span class="k">print</span> <span class="s">&#39;Calculated R^2 value: {0}&#39;</span><span class="o">.</span><span class="n">format</span><span class="p">(</span><span class="n">r_squared</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>Calculated R^2 value: 0.0313463012849
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Visualization">Visualization<a class="anchor-link" href="#Visualization">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="ENTRIESn_hourly-for-rainy-days-and-non-rainy-days">ENTRIESn_hourly for rainy days and non-rainy days<a class="anchor-link" href="#ENTRIESn_hourly-for-rainy-days-and-non-rainy-days">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[35]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="n">ggplot</span><span class="p">(</span><span class="n">aes</span><span class="p">(</span><span class="n">x</span><span class="o">=</span><span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">,</span>  <span class="n">color</span> <span class="o">=</span> <span class="s">&#39;factor(rain)&#39;</span><span class="p">),</span> <span class="n">data</span><span class="o">=</span><span class="n">turnstile_weather</span><span class="p">)</span> <span class="o">+</span> <span class="n">geom_density</span><span class="p">(</span><span class="n">alpha</span> <span class="o">=</span> <span class="mf">0.6</span><span class="p">)</span> <span class="o">+</span>\
<span class="n">ylab</span><span class="p">(</span><span class="s">&#39;entries density&#39;</span><span class="p">)</span> <span class="o">+</span> <span class="n">ggtitle</span><span class="p">(</span><span class="s">&#39;Subways Entries Density for Rainy Days and Non-rainy Days&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,iVBORw0KGgoAAAANSUhEUgAAAu4AAAIhCAYAAAARoz+rAAAABHNCSVQICAgIfAhkiAAAAAlwSFlz
AAALEgAACxIB0t1+/AAAIABJREFUeJzs3X18U/Xd//H3OUnapk3TplBuKjKEQVG5E7opWEFUHKII
1wAVB8VrG+pvOqabc25u4nSb13TopXPqcCpKnTq4tumw4rxFq04EhAlDbnQiFNRC70Lvm3x/f3SN
jdCSIJw09vV8PHhAcs5JPvkkKe98+z3fWMYYIwAAAABdmp3oAgAAAAAcGsEdAAAASAIEdwAAACAJ
ENwBAACAJEBwBwAAAJIAwR0AAABIAgR3IA6nn366HnjggUSX0SXccsstmj9/fqLLOGKGDRumV155
5Yjc1scff6zx48fL7/frhz/84RG5zc/jSD62L7olS5botNNOS3QZh+2L9r4EEI3gjm6ntLRU48aN
U3Z2tnr06KHCwkKtWbMmpmMty5JlWUe5ws9vyZIlcrlcyszMjPzx+/366KOPDnnsyy+/rGOPPfaQ
+/34xz/W/ffffyTKjbjxxhvl8Xjk9/vl9/uVn5+v7373uzHV/Xlt3LhR48ePj9Qxd+7cw76txYsX
q1evXqqpqdFtt932uWtr/3xmZWVpxIgR+stf/hLz8e0f25E0YMAApaeny+/3KxAI6NRTT9Xvf/97
fVG/HuSDDz6Qbds699xzo66fM2eOfv7znyeoqmhH430pJfa9CeBTBHd0KzU1NTrvvPP0ve99T5WV
lSorK9PChQuVmpqa6NKOuFNPPVXBYDDyp6amRn369Dkitx0KhY7I7XyWZVmaPXu2ampqVFlZqb/8
5S/66KOPNGbMmKQKCDt27NDxxx9/WMe2tLQc9Pq257OqqkpXXnmlLr74YlVWVn6eMj83y7K0YsUK
1dTU6MMPP9R1112nX//61/rWt76V0LqOttWrV+uNN96IXHbqA31Hrw0nfFHem0CyI7ijW9m6dass
y9KFF14oy7KUlpamSZMmafjw4ZIOHGltG2ELh8OR67Zv366TTz5ZWVlZmj59eiQ8zZs3T7fffrsk
qaysTLZt65577pEkvffee+rRo4ckqbKyUuedd5569eqlnJwcTZ06VWVlZZKkZcuWqaCgIKrm22+/
XdOnT5cklZSU6MQTT5Tf71e/fv20aNGiDh9rZ6OeAwYM0KJFizRy5EhlZ2froosuUmNjo2pra3XO
Oedo9+7dkVH6PXv26MYbb9TMmTM1d+5cZWVlacmSJQf06h//+IfGjRunQCCgUaNGadWqVZFtS5Ys
0aBBg+T3+zVw4ED98Y9/7LDmtrpdLpdOOOEEPfHEE8rNzY16rCtWrNCoUaMio7zvvPPOIR+bJO3d
u1fnnXeeAoGAevToETUKPWDAAL3wwgtauXKlbrnlFj3xxBPKzMzUSSedpOXLl3f6vLR3ySWX6JFH
HtGtt96qzMxMvfjii2pqatJVV12lY445Rsccc4yuvvpqNTU1SWr9DUe/fv106623qm/fvh2G3ra+
WJalOXPmqLGxUe+9956k1tfXGWecoZ49eyo3N1dz5sxRdXV11GN78cUXJbW+xi+44ALNmzdPfr9f
w4YN09q1ayVJt912m2bOnBl1vwsWLNBVV1110Jray8zM1NSpU/XEE0/o4Ycf1qZNmyRJTz/9tE46
6SRlZWWpf//+USPT5557ru6+++6o2xkxYoSefPJJSdLVV1+t3r17R37L0Habn/XQQw/phBNOkN/v
16BBg7R48eLItrb+3n777erdu7fy8vK0ZMmSyPZ9+/bp/PPPV1ZWlk4++eRITztz7bXX6vrrr4+6
rv377f7779fgwYPVo0cPTZs2TXv27Ilss21bv//97zVkyBAFAgFdeeWVnd5X28+RwYMHKz8/X5L0
ve99T/3791dWVpYKCgpUWloa2b/9+7Lt59cjjzyiL33pS8rNzdWvfvUrSdJHH32kjIwMVVRURI5d
t26devXqddAP5rG8N5362QZ0awboRmpqakyPHj3MvHnzzDPPPGMqKiqitt94441mzpw5kcv//ve/
jWVZJhQKGWOMmTBhgjnmmGPMpk2bTG1trZkxY0Zk/wcffNBMnTrVGGPMo48+agYNGmQuvPBCY4wx
DzzwgJk+fboxxph9+/aZP//5z6a+vt4Eg0Eza9asyLaGhgaTk5NjNm/eHKlh1KhR5s9//rMxxpg+
ffqY0tJSY4wxVVVVZt26dQd9nA899JApLCzssA8DBgwwJ598stmzZ4+pqKgwxx9/vLnvvvuMMca8
/PLLpl+/flH7L1y40Hg8HvPkk08aY4ypr6+P6tWuXbtMjx49zDPPPGOMMea5554zPXr0MHv37jX7
9+83fr/fbN261RhjzEcffWQ2bdp00LoWLlwY1f82N9xwgzn55JONMcasW7fO9OrVy6xevdqEw2Hz
8MMPmwEDBpimpqZDPrbrrrvOXH755aalpcW0tLREetl23AsvvGCMaX0dzJ07N7KtsbGx0+flsy65
5BLzs5/9LHL5Zz/7mRk7dqwpLy835eXlZty4cZHtL730knG73ea6664zTU1Npr6+/oDba/98trS0
mLvvvtsEAgFTU1NjjDFm+/bt5vnnnzdNTU2mvLzcjB8/3lx11VUHfWwLFy40aWlp5plnnjHhcNj8
+Mc/Nqeccooxxpjdu3ebjIwMU1VVZYwxprm52fTq1avD11n7222vf//+Ua+njRs3GmOM+ec//2l6
9+5t/vrXvxpjjPnTn/4UeV6NMWb9+vWmR48eprm52axcudKMGTPGVFdXG2OMeffdd82ePXsOWsfT
Tz9t3n//fWOMMatWrTLp6emRmtv6u3DhQtPS0mJKSkpMenp65DFeeOGF5sILLzR1dXVm48aN5phj
jjGnnXbaQe+n7edBMBg0xxxzjHn++eeNMcbMmTPH/PznPzfGGPPCCy+Ynj17mrfffts0Njaa7373
u2b8+PGR27Asy0ydOtVUV1ebDz/80OTm5pqVK1ce9P7a9j/77LNNZWWlaWhoMMYYU1xcbCoqKkwo
FDKLFi0yffr0MY2NjcaY6J9hbfVeeumlpqGhwWzYsMGkpqaad9991xhjzJQpU8y9994bua+rrrrK
LFiw4KB1xPLedOJnG9DdMeKObiUzM1OlpaWyLEvz589Xr169NG3aNH3yySeSOh+lllpHO4uKinTC
CScoPT1dN998s/70pz/JGKPx48ertLRUxhi9+uqruvbaa/Xaa69JklatWqUJEyZIknJycvRf//Vf
SktLk8/n009+8pPI6HRqaqouuOACFRcXS5I2bdqkHTt26LzzzpMkpaSkaNOmTaqpqVFWVpZOOumk
Dmv9xz/+oUAgEPkzePDgqO0LFixQnz59FAgENHXqVK1fv77THowbN07nn3++JCktLS1qv+LiYk2Z
MkWTJ0+WJJ111lkqKCjQ008/LcuyZNu23nnnHdXX16t379464YQTOu3zZ/Xt2zcyMrh48WJddtll
+spXvhJ5PlJTU/WPf/zjkI8tJSVFe/bs0QcffCCXy6VTTz31oPdn2o0uth3X2fPS0W20+eMf/6gb
brhBPXv2VM+ePbVw4UItXbo0st22bf385z+Xx+NRWlraQW+v7fn0er364Q9/qL/97W/KzMyUJA0a
NEhnnnmmPB6PevbsqauvvjrqNx6fddppp2ny5MmR0fsNGzZE+nzaaadp2bJlkqSVK1cqNze309fZ
weTl5UWerwkTJujEE0+UJA0fPlwXXXRRpLapU6dq69atkVHupUuX6qKLLpLb7ZbH41EwGNTmzZsV
DoeVn5/f4VSvKVOm6LjjjpMkjR8/XmeffbZeffXVyHaPx6MbbrhBLpdL55xzjnw+n7Zs2aJQKKQ/
//nPuummm+T1enXiiSdq3rx5h/w5kJ6eruuvv14//elPJUU/148++qi+9a1vadSoUUpJSdEtt9yi
N954Qx9++GFkn+uuu05+v1/HHnusJk6cGHl9duTHP/6xsrOzI1P6vvGNbygQCMi2bX3/+99XY2Oj
tmzZckAtbdqmA44YMUIjR46MPN9FRUWR13QoFNLjjz8e97kd7d+bTv1sA7ozgju6naFDh+qhhx7S
zp07tXHjRu3evTumqQBt2p+42b9/fzU3N2vv3r0aNGiQMjIytH79er366qs677zzlJeXp61bt+qV
V16JBPe6ujpddtllGjBggLKysjRhwgRVV1dH/sOdN29eZCrJ0qVLdeGFF8rj8UiS/u///k8lJSUa
MGCATj/99Kiw+lmnnHKKKisrI3+2bdsWtb19CPJ6vdq/f3+nj7tfv34dbtuxY4eWLVsW9UHhtdde
00cffaT09HQ98cQTuu+++5SXl6fzzjsvEjJiVVZWFplqtGPHDi1atCjqvnbt2qXdu3cf8rH98Ic/
1Je//GWdffbZGjRokH7961/HXENnz8uh7N69W1/60pcil/v37x9Vb25urlJSUjq9jfbP5/nnnx9V
+8cff6yLLrpI/fr1U1ZWlubOnat9+/Z1eFu9e/eO/Ds9PV0NDQ2R6WDz5s2LhKvi4uLDOkm3rKxM
OTk5kqQ333xTEydOVK9evZSdna3f//73kdrS0tJ0wQUXaOnSpTLGRAXHM844Q1deeaWuuOIK9e7d
W5dddpmCweBB7++ZZ57RKaecoh49eigQCKikpCTq8ffo0UO2/el/d+np6dq/f7/Ky8vV0tJywHs6
Ft/61rf08ccfa8WKFVHz2/fs2RP1XGdkZKhHjx6RKSNS9OszPT1dtbW1kqQTTzwxcjJ524d+SQec
LP6b3/xGJ5xwgrKzsxUIBFRdXa29e/d2WOtn76/t/TBt2jT961//0gcffKDnnnsuMvUmHu3fm079
bAO6M4I7urX8/HzNmzdPGzdulNT6n2xdXV1k+8FOumo/cvbhhx9GRjml1tHFZcuWqbm5WXl5eZow
YYKWLFmiyspKjRo1SpK0aNEibd26VatXr1Z1dbVWrVoVNcJ7yimnKCUlRa+88ooee+yxqOBUUFCg
v/71ryovL9f06dN1wQUXHPGeHOwku0OdfNe/f3/NnTs36oNCMBjUtddeK0k6++yz9fe//10fffSR
hg4d2uFydQe7j3A4rL/97W+RJfr69++v66+/Puq+9u/frwsvvPCQt+nz+fSb3/xG7733np566ind
fvvteumll2Kqo7Pn5VDy8vL0wQcfRC5/+OGHysvL6/T+OpKRkaF7771Xq1atioxm/uQnP5HL5dLG
jRtVXV2tpUuXRp2XEY9p06bpn//8pzZu3Kinn35a3/jGN+I6/q233lJZWZkKCwslSRdffLGmT5+u
Xbt2qaqqSpdffnlUbfPmzdOjjz6q559/Xunp6Tr55JMj27773e9qzZo1+te//qWtW7cedIWexsZG
zZgxQ9dee60++eQTVVZWasqUKTGtbJObmyu3233AezoWKSkpWrhwoX72s59F3ddnn+va2lrt27dP
xxxzTIe31Xb8pk2bIieTt/9tUPvXx6uvvqrbbrtNy5YtU1VVlSorK5WVlXVYK/mkpaVp1qxZKi4u
VnFxsYqKijrcN5b3Zlf/2QZ8ERDc0a1s2bJFt99+e2T0a+fOnXrsscc0duxYSdKoUaP0yiuvaOfO
naqurtYtt9wSdbwxRsXFxdq8ebPq6up0ww03aNasWZH/1CZMmKC77747ctLj6aefrrvvvlunnXZa
ZJ/9+/fL6/UqKytLFRUVB11Gbu7cubryyiuVkpKicePGSZKam5v16KOPqrq6OrI0oMvlOuI96t27
t/bt26eampqox92ZOXPm6G9/+5v+/ve/KxQKqaGhQS+//LLKysr0ySef6Mknn1Rtba08Ho8yMjI6
rLv9/bS0tGjz5s2aPXu2PvnkE33/+9+XJM2fP1/33XefVq9eLWOMamtr9fTTT3f4G4P2t7lixQpt
375dxhj5/X65XK6okdg2ffr00QcffHDA4z7Y83Ko+5Sk2bNn6xe/+IX27t2rvXv36qabbvpcy00G
AgFdeuml+p//+R9Jra+pjIwM+f1+lZWVfa4lKL1er2bMmKGLL75YJ598cqe/aZE+faw1NTVasWKF
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
lJ2drVmzZsnr9aq5uVlPPvmkPvnkE4XDYY0cOVKnnXZa5wXyzakAAABIoC4x4h4Oh1VSUqI5c+bo
iiuu0DvvvKPy8vKofbZu3aqKigotWLBAU6dO1YoVKw55bGlpqQYOHKgFCxZo4MCBKi0tlSRt3LhR
kvSd73xHl112mdauXauqqqrOi+TkVAAAACRQlwjuZWVlysnJUSAQkMvl0rBhw/Tuu+9G7bNlyxaN
GjVKktSvXz81NDQoGAx2emz7Y0aOHBm5PjMzU01NTQqHw2pqapLL5VJqamrnRVoWy0ECAAAgYbrE
VJmamhplZWVFLvv9fpWVlUXtEwwG5ff7o/YJBoMKBoMdHltbWyufzydJ8vl8qq2tlSR9+ctf1oYN
G/Sb3/xGzc3Nmjx5srxeb6SW/fv3R923z+eTy+ORbdvyeDxH8JEfXS6XK6nqbeN2u6P+TibJ2HP6
7axk7rdEz51Gv52VjP2WkrPXODxd4pm2LMvR+9iwYYNaWlp0zTXXqL6+Xg8++KAGDhyoQCCgtWvX
atWqVVHHTpgwQaePPkkhr1dZublHvVa0CgQCiS6hW6HfzqLfzqPnzqLfwJHXJYJ7ZmamqqurI5dr
amqiRtc72ycUCnV4bEZGhoLBoDIzMxUMBpWRkSFJ2rlzp4YOHSrbtpWRkaH+/ftr9+7dCgQCGjNm
jPLz86Pu2+fzqaq6Wvb+/Wr6zNz7riw1NVWNjY2JLiNubrdbgUBAlZWVamlpSXQ5cUnGntNvZyVz
vyV67jT67axk7Lf0ac/xxdclgnteXp4qKipUWVmpzMxMbdy4UTNnzozaJz8/X6tXr9bw4cO1c+dO
paWlyefzyev1dnhsfn6+NmzYoMLCQq1fv15Dhw6VJPXs2VP//ve/NXLkSDU1NWnXrl065ZRTJLVO
tfnshwZJ2ltZIYVCam5uPsrdOHLcbndS1ftZLS0tSVd/MvecfjsrGfst0XOn0W9nJXO/0T10ieDu
crk0ZcoUFRcXKxwOa/To0crNzdWaNWskSQUFBRoyZIi2bdumO++8UykpKZo2bVqnx0pSYWGhli1b
pnXr1kWWg2y7vSeffFL33HOPjDE66aST1Lt3705rNKwqAwAAgATqEsFdkgYPHqzBgwdHXVdQUBB1
+dxzz435WElKT0/XvHnzDrje7XZrxowZMdf2cV2dttXW6USCOwAAABKkSywH2dVtrqzSc3v3qong
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
LZsRdwAAADiO4B4vmxF3AAAAOI/gHieXZSnMgDsAAAAcRnCPU+tykCR3AAAAOIvgHqfWVWUSXQUA
AAC6G4J7nGxZCsvIcIIqAAAAHERwj5PlcsmSmCwDAAAARxHc42VZso1hSUgAAAA4iuAeJ2O1No0l
IQEAAOAkgnvcLLkMc9wBAADgLIJ7vCxLlhhxBwAAgLMI7vGyLNlijjsAAACcRXCPl2XJNlKI4A4A
AAAHuRNdQJtt27Zp5cqVMsZo9OjRKiwsPGCfkpISbd++XR6PR9OnT1ffvn07Pbaurk7Lly9XVVWV
srOzNWvWLHm9XlVWVup3v/udevbsKUnq16+fzjvvvNgKtezWEfcj87ABAACAmHSJ4B4Oh1VSUqKi
oiL5/X4tXrxY+fn5ys3NjeyzdetWVVRUaMGCBdq1a5dWrFih+fPnd3psaWmpBg4cqMLCQpWWlqq0
tFSTJk2SJOXk5Ojyyy+Pu1ZjWXIZMVUGAAAAjuoSU2XKysqUk5OjQCAgl8ulYcOG6d13343aZ8uW
LRo1apSk1hHyhoYGBYPBTo9tf8zIkSMPuM3DwjruAAAASIAuEdxramqUlZUVuez3+xUMBqP2CQaD
8vv9B+wTDAY7PLa2tlY+n0+S5PP5VFtbG9mvsrJS9913nx566CHt2LEj9mL/c3IqsR0AAABO6hJT
ZSzLcvQ+MjMz9f3vf19er1e7d+/W448/riuuuEKpqamqqanR/v37o471+Xxyu//TKktyWZZsl1se
j+eo1/15uFyuLl/jwbT1OtLzJJKMPaffzkrmfkv03Gn021nJ2G8pOXuNw9MlnunMzExVV1dHLtfU
1ESNrne2TygU6vDYjIwMBYNBZWZmKhgMKiMjQ1LrC7ztRZ6Xl6ecnBzt27dPeXl5Wrt2rVatWhV1
30VFRerTp49SU1OllhZ5LEtp3rTI7XVlyfpmrqurU2pqamvPk0wy9px+OyuZ+y3Rc6fRb2clY7/R
fXSJV2deXp4qKipUWVmpzMxMbdy4UTNnzozaJz8/X6tXr9bw4cO1c+dOpaWlyefzyev1dnhsfn6+
NmzYoMLCQq1fv15Dhw6V1DqFxuv1yrZtVVRUaN++fQoEApKkMWPGKD8/P+q+fT6fGhsb1dLSIoVD
MqGQauvqVauuLTU1VY2NjYkuI25ut1uBQECVlZWtPU8iydhz+u2sZO63RM+dRr+dlYz9llp7np6e
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
9fWvf11XX321GhoaDtg2Y8aMRJd72GIacb/mmmv02GOPKSsrS0VFRfrFL36hfv36RbafcsopCgQC
R63IrsaybYVDBHcAAICu4tZbb426fMcdd3S4LVnFFNwbGhr017/+VV/5ylcOut3j8eitt946ooV1
ZbZlKSy+ORUAAADOiWmqjGVZBw3tV111VeTfxx9//JGrqotz2azjDgAAAGfFFNyXLFly0OsfeeSR
I1lL0rD5AiYAAAA4rNOpMg888IAkqaWlRQ8++KCMMZG1Qt977z3l5uYe/Qq7INu2Ce4AAABwVKfB
fenSpbIsS83NzVq6dGnkesuy1Lt3bz388MNHvcAuiRF3AAAAOKzT4P7yyy9Lkq6//nr98pe/dKKe
pGBbtsjtAAAAcFKHwb39tJibbrpJ4fDBV1Gx7ZiXgv/CsC1bIb6ACQAAoEMn/99fjthtvTnjvzrd
XlNTo7POOkubN2/Wm2++qRNOOCFq+49+9CO98cYbGjBggB588EG53TF/B2mX0mHq9vv9kX97PB65
3e4D/nTXr9hlVRkAAICuIz09XSUlJZo5c6bMZzLahg0btHv3br3yyisaOnSoli9fnqAqP78OP25s
2rQp8u/333/fkWKShcuyxBenAgAAdA1ut1s9e/Y86LY33nhDX/va1yRJkydP1kMPPaSLLrrIyfKO
mA6De//+/SP/HjBgQNS2+vp62bat1NTUo1ZYV2bbLoUYcQcAAOjyKisr1bdvX0mtM0oqKioSXNHh
i2mC+g9+8AO9+eabkqSnn35aOTk5CgQCeuqpp45qcV2VbVvMcQcAAOiC2s7RbJOdna2amhpJUnV1
tXJychJR1hER08z8Rx99VDfffLMk6ec//7mKi4uVlZWlq6++Wueff/5RLbArapsq0/4EXgAAAHzq
UCeUHi2fneM+btw43X777Zo7d66effZZFRYWJqSuIyGm4F5fX6/09HTt3btX//73vzVjxgxJ0gcf
fHA0a+uyLJdLtozCklyJLgYAAACaMmWKNmzYoK1bt+rSSy/V+vXrdcstt2jkyJHq3bu3xo8fry99
6Uu69tprE13qYYspuA8ePFiPPvqotm3bpkmTJkmSysvLlZ6eflSL67IsS7YxChsjFyPuAAAACVdS
UhJ1ed68eZF/33rrrU6Xc1TEFNzvuecefe9731NKSooeeOABSdKzzz6rs88++6gW11UZy5JLUsgY
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
5fPDniHJME0F9h9QT29v/8/DIcr+PDn2PfrIBecr7PK/vUX/d/MslWNGwdkpie90JBJRR0dH9nk8
Hs85uz7YOplMZsBtQ6GQEomEIpGIEomEQqHQaY+3ZcsWbdy4MefYF1xwgT784Q9nh+OgsOLxuP77
v/9b8+bNo+cuiMfj2rJli+bNm3fS/3fIP/rtPnruLvrtvhP/3aTnI1tJXI05fvx4tbe3Z8+wNjU1
qb6+Pmed+vp6bdu2TZLU2tqqQCCgcDg86LYnbrN161ZNmzYtu7ypqUnpdFqxWEzt7e2aMGGCJGne
vHn6zGc+k31cf/312rNnz0ln4VE4nZ2d2rhxIz13Cf12F/12Hz13F/12Hz0fPUrijLtlWVq8eLFW
r14t27Y1d+5c1dTUaPPmzZKk+fPna+rUqWppadG9994rn8+n6667btBtJamhoUGPP/64Xnrppex0
kJJ03nnn6eKLL9YDDzwg0zS1ZMmS7K/9otEon1YBAABQckoiuEtSXV2d6urqcpbNnz8/5/mSJUuG
vK0kVVRUaOXKlafc5sorr9SVV155ltUCAAAA7iqJoTIAAAAABmd985vf/GaxiyhljuPI5/Np8uTJ
8vv9xS5nVKDn7qLf7qLf7qPn7qLf7qPno0fJDJUpVQcPHlRTU5O2b9+uuXPnqqGhodgllYVf/epX
amlpUSgU0uc//3lJUldXl9asWaOjR49mrzkIBoOSpOeee04vv/yyDMPQokWLtHDhQknSvn379Ktf
/UrpdFp1dXVatGiRJCmdTuvJJ5/U/v37FQwGtWLFClVWVhbnzZaIjo4OPfnkk9n7FcybN0/ve9/7
htz3SZMmZa/voO+nl0ql9MgjjyidTiuTyWjatGm6+uqr6XeB2batBx98UNFoVDfeeOMZ/Vyh32fu
7rvvlt/vz97b4jOf+Qx/xwuou7tbv/nNb3T48GFJ0rJly1RdXc3fcbzNwYAymYxzzz33OO3t7U46
nXZ++MMfOocOHSp2WWVh9+7dzr59+5wHHnggu+zpp592nnvuOcdxHOe5555zfve73zmO4zgHDx50
fvjDHzrpdNppb2937rnnHse2bcdxHOdHP/qR09ra6jiO4/zkJz9xdu7c6TiO47zwwgvOb3/7W8dx
HGf79u3OY4895tp7K1XxeNzZt2+f4ziO09PT49x3333OoUOH6HsB9fb2Oo7jOOl02nnwwQed3bt3
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
2c/0yCOP6NChQ+rr69O//uu/Sur/sHDjjTfqvvvu01tvvaXFixdr6dKlA549f+ewm4MHDyoWi+nN
N9/Uj370o5wef/zjH9f69evV0dEhqf+M/C9+8QutXLnyjPoCAKMRwR3AqOU4jpYtW6aqqqrs48c/
/nE2hM6ePVvXXHONvve9753V/s8991xVVFTosssu07e+9S0tWLBgwHX/+Mc/5tRRV1cnSYpEImps
bJRhGLr11lt13nnn6brrrtOhQ4ey215wwQXZM9s333yz9u/fn/P6qRiGoU996lO66KKLFAgE9Jd/
+ZfaunWrJOkXv/iFPvShD+kDH/iALMvS3/zN36i7u1vPP//8gPs7MZybpqlvfetb8nq9CgQCOevV
1tbqiiuu0OOPPy5JWr9+vWpqavTud7970HoBAAR3AKOYYRj69a9/rVgsln18+tOfzgmh3/72t/Vv
//Zvpw3Cp3LkyBF1dnbqzjvv1D333KN4PD7guu973/ty6mhpacm+Nm3aND388MNqbW1VU1OT9u3b
lzO0ZNy4cdmvKyoqJClnbP5ATtwuGAxmt9m3b5/OP//87GuGYWjSpElqa2sbwruWampq5PP5Bnx9
5cqVWr16tSRp9erVuummm4a0XwAY7QjuADCI+vp63XDDDfrOd75zytdPNzOLaZr6yle+osmTJ+vu
u+/OSz0rV65UU1PTsPc1kAkTJmjPnj3Z547jqLW1VRMmTJDU/+Ggq6sr+/r+/ftz+nC6nlx33XX6
05/+pKamJj311FP62Mc+lud3AAAjE8EdwKh2ugtLJen222/Xww8/fMqx7kPZXpL+4R/+Qffff39O
4B2K5uZm3XXXXdmz3a2trfr5z3+u97///We0n1MZqPYVK1boqaee0oYNG5RKpXTnnXcqEAjosssu
kyTNmTNHP/3pT5XJZLR+/Xo9++yzZ3TcYDCoD3/4w7rxxht16aWXauLEicN+LwAwGhDcAYxqS5cu
zZk//YYbbjjpYsvJkyfr5ptvPmXoHmg+9HcuW7JkicaNG6cf//jHp1z3D3/4Q04dkUhEW7ZsUSQS
0QsvvKBLL71U4XBY73//+3XJJZfozjvvHPD4Q52f/Z1nyY8/r6+v1+rVq/XFL35RNTU1euqpp/Tb
3/5WHo9HknTvvffqt7/9raqqqvSzn/1M119//WmP/85lx39rwDAZABg6wxnq6SIAAPKktbVV06ZN
08GDBxUOh4tdDgCUBc64AwBcZdu27rzzTn30ox8ltAPAGfAUuwAAQGGEw+FTDltZv369Lr/88iJU
JCWTSY0dO1YXXnjhkG8UBQDox1AZAAAAoAwwVAYAAAAoAwR3AAAAoAwQ3AEAAIAyQHAHAAAAygDB
HQAAACgD/x8lajSvEa7uIAAAAABJRU5ErkJggg==
"
>
</div>

</div>

<div class="output_area"><div class="prompt output_prompt">Out[35]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;ggplot: (297599721)&gt;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[11]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">import</span> <span class="nn">matplotlib.pyplot</span> <span class="kn">as</span> <span class="nn">plt</span>

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>

<span class="c"># your code here to plot a historgram for hourly entries when it is not raining</span>
<span class="n">non_rainy_data</span> <span class="o">=</span> <span class="n">turnstile_weather</span><span class="p">[</span><span class="n">turnstile_weather</span><span class="p">[</span><span class="s">&#39;rain&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="mi">0</span><span class="p">][</span><span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">]</span>
<span class="n">non_rainy_data</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">range</span> <span class="o">=</span> <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">6000</span><span class="p">],</span> <span class="n">bins</span> <span class="o">=</span> <span class="mi">25</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s">&#39;No Rain&#39;</span><span class="p">)</span>

<span class="c"># your code here to plot a historgram for hourly entries when it is raining</span>
<span class="n">rainy_data</span> <span class="o">=</span> <span class="n">turnstile_weather</span><span class="p">[</span><span class="n">turnstile_weather</span><span class="p">[</span><span class="s">&#39;rain&#39;</span><span class="p">]</span> <span class="o">==</span> <span class="mi">1</span><span class="p">][</span><span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">]</span>
<span class="n">rainy_data</span><span class="o">.</span><span class="n">hist</span><span class="p">(</span><span class="nb">range</span> <span class="o">=</span> <span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">6000</span><span class="p">],</span> <span class="n">bins</span> <span class="o">=</span> <span class="mi">20</span><span class="p">,</span> <span class="n">label</span><span class="o">=</span><span class="s">&#39;Rain&#39;</span><span class="p">)</span>

<span class="n">plt</span><span class="o">.</span><span class="n">title</span><span class="p">(</span><span class="s">&#39;Histogram of ENTRIESn_hourly&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">xlabel</span><span class="p">(</span><span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">ylabel</span><span class="p">(</span><span class="s">&#39;Frequency&#39;</span><span class="p">)</span>
<span class="n">plt</span><span class="o">.</span><span class="n">legend</span><span class="p">()</span>

<span class="n">plt</span><span class="o">.</span><span class="n">figure</span><span class="p">()</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[11]:</div>


<div class="output_text output_subarea output_execute_result">
<pre>&lt;matplotlib.figure.Figure at 0x10a2eaa90&gt;</pre>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_png output_subarea ">
<img src="data:image/png;base64,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
r7zyCg8//DDz5s3j29/+dk323ZP6zPDmL33prA6t39AwlFNP/WJBtamt5uZmGhsbe7oahShzbBDx
1TtJfPnLX+b8889n0qRJbLvttm9Z5/e//z2nn346ixYtYs899+TSSy/lwAMP3OS+Bw8ezLhx43j0
0UfXl02dOpUrr7yS5557jqFDh/Kd73yH8eOz50A2NTVx1VVXcd999wHQr18/rrjiCi688EKef/55
PvWpT3HZZZfVKPKO6TOJ5qKLBnVg7T+z114/rZtEE0LoOe973/tobGzkggsu4Fvf+tZGy1544QU+
8YlPcNlll3H88cczffp0PvGJT/DEE08waFDrn0mVJqylS5cyY8YMjjnmmPXL9thjD377298yZMgQ
pk+fzgknnMCTTz7J4MGDW93Xr371Kx544AFefvllxowZw5FHHtkz/Tg9fRvqbrrVtcEdeP3Be+01
1iGEnpd9TL21rGP/0x19vfWYrWloaPC9997r+fPne9ttt/Xzzz/vH//4x25sbLRtX3PNNR47duPP
kgMPPNBNTU2t7m+33XbzNtts4wEDBliSx48f77Vr17Z5/FGjRvmWW26xbV999dU+6KCD1i+T5N/9
7nfr54899lhPnTq11f20FW8q7/JncPTRhBBCF+27774cccQRTJ06daOBCs888wzDhg3baN3ddtuN
ZcuWtbofSdxyyy2sWrWK5uZmfvOb3/DAAw+sX37NNdcwevRott9+e7bffnvmz5/PypUr26zXkCFD
1k/379+fV199tbMhdkkkmhIo87UKZY4NIr4y+eY3v8mPf/zjjZLILrvswlNPPbXRek899RS77rpr
y83f4uCDD+bUU0/lrLPOWr/d5z73OX74wx/ywgsv8OKLL/Lud7+7Lu6aEIkmhBBq4F3vehfHHXfc
RiPQDj/8cB5//HGuv/561qxZww033MDChQs54ogjqtrnGWecwezZs7n//vt57bXXkMQOO+zAunXr
uPrqq5k/f37V9evJhFR4opG0maQ5km5L84Mk3SPpcUl3S9out+7ZkhZJWihpXK58jKR5admlufIt
Jd2QymdJ2q3oeHqjMo/qKXNsEPF1jQp8dc43vvENVq9evb757B3veAe33347F154ITvssAMXXHAB
t99+e5sDAVraYYcdmDhxIueddx4jR47kS1/6EgceeCBDhgxh/vz5HHTQQRvejRZ3YW55rVF33KW5
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
"
>
</div>

</div>

<div class="output_area"><div class="prompt"></div>


<div class="output_text output_subarea ">
<pre>&lt;matplotlib.figure.Figure at 0x10a2eaa90&gt;</pre>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[12]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">from</span> <span class="nn">pandasql</span> <span class="kn">import</span> <span class="n">sqldf</span>

<span class="n">q</span> <span class="o">=</span> <span class="s">&#39;&#39;&#39;</span>
<span class="s">select hour, avg(ENTRIESn_hourly) as avg_entries</span>
<span class="s">from turnstile_weather</span>
<span class="s">group by hour&#39;&#39;&#39;</span>
<span class="n">avg_entries_for_hours</span> <span class="o">=</span> <span class="n">sqldf</span><span class="p">(</span><span class="n">q</span><span class="p">,</span> <span class="nb">locals</span><span class="p">())</span>

<span class="n">avg_entries_for_hours</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">


<div class="output_area"><div class="prompt output_prompt">Out[12]:</div>

<div class="output_html rendered_html output_subarea output_execute_result">
<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Hour</th>
      <th>avg_entries</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1167.690147</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>605.048709</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>181.874257</td>
    </tr>
    <tr>
      <th>3</th>
      <td>3</td>
      <td>38.810592</td>
    </tr>
    <tr>
      <th>4</th>
      <td>4</td>
      <td>262.313576</td>
    </tr>
    <tr>
      <th>5</th>
      <td>5</td>
      <td>142.587866</td>
    </tr>
    <tr>
      <th>6</th>
      <td>6</td>
      <td>77.356750</td>
    </tr>
    <tr>
      <th>7</th>
      <td>7</td>
      <td>146.389928</td>
    </tr>
    <tr>
      <th>8</th>
      <td>8</td>
      <td>683.933781</td>
    </tr>
    <tr>
      <th>9</th>
      <td>9</td>
      <td>1315.495175</td>
    </tr>
    <tr>
      <th>10</th>
      <td>10</td>
      <td>545.392620</td>
    </tr>
    <tr>
      <th>11</th>
      <td>11</td>
      <td>292.568130</td>
    </tr>
    <tr>
      <th>12</th>
      <td>12</td>
      <td>2453.842100</td>
    </tr>
    <tr>
      <th>13</th>
      <td>13</td>
      <td>1136.670129</td>
    </tr>
    <tr>
      <th>14</th>
      <td>14</td>
      <td>411.996463</td>
    </tr>
    <tr>
      <th>15</th>
      <td>15</td>
      <td>202.954628</td>
    </tr>
    <tr>
      <th>16</th>
      <td>16</td>
      <td>1867.198923</td>
    </tr>
    <tr>
      <th>17</th>
      <td>17</td>
      <td>1552.469912</td>
    </tr>
    <tr>
      <th>18</th>
      <td>18</td>
      <td>729.480346</td>
    </tr>
    <tr>
      <th>19</th>
      <td>19</td>
      <td>386.317446</td>
    </tr>
    <tr>
      <th>20</th>
      <td>20</td>
      <td>2656.422331</td>
    </tr>
    <tr>
      <th>21</th>
      <td>21</td>
      <td>1616.284799</td>
    </tr>
    <tr>
      <th>22</th>
      <td>22</td>
      <td>510.318336</td>
    </tr>
    <tr>
      <th>23</th>
      <td>23</td>
      <td>157.985832</td>
    </tr>
  </tbody>
</table>
</div>
</div>

</div>

</div>
</div>

</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[18]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">import</span> <span class="nn">pandasql</span>

<span class="n">df</span> <span class="o">=</span> <span class="n">turnstile_weather</span><span class="p">[[</span><span class="s">&#39;Hour&#39;</span><span class="p">,</span> <span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">]]</span>

<span class="n">q</span> <span class="o">=</span> <span class="s">&quot;&quot;&quot;</span>
<span class="s">    SELECT Hour AS hour,</span>
<span class="s">           ENTRIESn_hourly AS hourlyentries</span>
<span class="s">    FROM df</span>
<span class="s">    GROUP BY hour</span>
<span class="s">    &quot;&quot;&quot;</span>

<span class="c">#Execute SQL command against the pandas frame</span>
<span class="n">rainy_days</span> <span class="o">=</span> <span class="n">pandasql</span><span class="o">.</span><span class="n">sqldf</span><span class="p">(</span><span class="n">q</span><span class="o">.</span><span class="n">lower</span><span class="p">(),</span> <span class="nb">locals</span><span class="p">())</span>

<span class="k">print</span> <span class="n">ggplot</span><span class="p">(</span><span class="n">rainy_days</span><span class="p">,</span> <span class="n">aes</span><span class="p">(</span><span class="s">&#39;hour&#39;</span><span class="p">,</span> <span class="s">&#39;hourlyentries&#39;</span><span class="p">))</span> <span class="o">+</span> \
             <span class="n">geom_path</span><span class="p">(</span><span class="n">color</span><span class="o">=</span><span class="s">&#39;red&#39;</span><span class="p">)</span> <span class="o">+</span> \
             <span class="n">scale_x_continuous</span><span class="p">(</span><span class="n">name</span><span class="o">=</span><span class="s">&#39;Hour&#39;</span><span class="p">,</span>
                                <span class="n">breaks</span><span class="o">=</span><span class="p">[</span><span class="mi">0</span><span class="p">,</span> <span class="mi">1</span><span class="p">,</span> <span class="mi">2</span><span class="p">,</span> <span class="mi">3</span><span class="p">,</span> <span class="mi">4</span><span class="p">,</span> <span class="mi">5</span><span class="p">,</span>
                                        <span class="mi">6</span><span class="p">,</span> <span class="mi">7</span><span class="p">,</span> <span class="mi">8</span><span class="p">,</span> <span class="mi">9</span><span class="p">,</span> <span class="mi">10</span><span class="p">,</span> <span class="mi">11</span><span class="p">,</span>
                                        <span class="mi">12</span><span class="p">,</span> <span class="mi">13</span><span class="p">,</span> <span class="mi">14</span><span class="p">,</span> <span class="mi">15</span><span class="p">,</span> <span class="mi">16</span><span class="p">,</span> <span class="mi">17</span><span class="p">,</span>
                                        <span class="mi">18</span><span class="p">,</span> <span class="mi">19</span><span class="p">,</span> <span class="mi">20</span><span class="p">,</span> <span class="mi">21</span><span class="p">,</span> <span class="mi">22</span><span class="p">,</span> <span class="mi">23</span><span class="p">],</span>
                                <span class="n">labels</span><span class="o">=</span><span class="p">[</span><span class="s">&#39;12AM&#39;</span><span class="p">,</span> <span class="s">&#39;1AM&#39;</span><span class="p">,</span> <span class="s">&#39;2AM&#39;</span><span class="p">,</span> <span class="s">&#39;3AM&#39;</span><span class="p">,</span> <span class="s">&#39;4AM&#39;</span><span class="p">,</span> <span class="s">&#39;5AM&#39;</span><span class="p">,</span>
                                        <span class="s">&#39;6AM&#39;</span><span class="p">,</span> <span class="s">&#39;7AM&#39;</span><span class="p">,</span> <span class="s">&#39;8AM&#39;</span><span class="p">,</span> <span class="s">&#39;9AM&#39;</span><span class="p">,</span> <span class="s">&#39;10AM&#39;</span><span class="p">,</span> <span class="s">&#39;11AM&#39;</span><span class="p">,</span>
                                        <span class="s">&#39;12PM&#39;</span><span class="p">,</span> <span class="s">&#39;1PM&#39;</span><span class="p">,</span> <span class="s">&#39;2PM&#39;</span><span class="p">,</span> <span class="s">&#39;3PM&#39;</span><span class="p">,</span> <span class="s">&#39;4PM&#39;</span><span class="p">,</span> <span class="s">&#39;5PM&#39;</span><span class="p">,</span>
                                        <span class="s">&#39;6PM&#39;</span><span class="p">,</span> <span class="s">&#39;7PM&#39;</span><span class="p">,</span> <span class="s">&#39;8PM&#39;</span><span class="p">,</span> <span class="s">&#39;9PM&#39;</span><span class="p">,</span> <span class="s">&#39;10PM&#39;</span><span class="p">,</span> <span class="s">&#39;11PM&#39;</span><span class="p">])</span> <span class="o">+</span> \
             <span class="n">ggtitle</span><span class="p">(</span><span class="s">&#39;Average ENTRIESn_hourly by Hour&#39;</span><span class="p">)</span> <span class="o">+</span> \
             <span class="n">xlab</span><span class="p">(</span><span class="s">&#39;Hour&#39;</span><span class="p">)</span> <span class="o">+</span> \
             <span class="n">ylab</span><span class="p">(</span><span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">)</span> <span class="o">+</span> \
             <span class="n">xlim</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span> <span class="mi">23</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>





<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;ggplot: (276680945)&gt;
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="For-example,-I-want-to-set-the-y-axis-to-be-from-0-to-100-with-a-tick-at-values-0,-10,-20,-30,...,100.">For example, I want to set the y-axis to be from 0 to 100 with a tick at values 0, 10, 20, 30,...,100.<a class="anchor-link" href="#For-example,-I-want-to-set-the-y-axis-to-be-from-0-to-100-with-a-tick-at-values-0,-10,-20,-30,...,100.">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">

<pre><code>ggplot(aes(x=x, y=y), data=data) + geom_point() + scale_y_continuous(limits=(0,100), breaks=range(0,100,10))
ggplot(aes(x=x, y=y), data=data) + geom_point() + scale_y_continuous(breaks=range(0,100,10)) + ylim(0,100)
ggplot(aes(x=x, y=y), data=data) + geom_point() + scale_y_continuous(breaks=range(0,100,10))</code></pre>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[26]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre><span class="kn">from</span> <span class="nn">datetime</span> <span class="kn">import</span> <span class="n">datetime</span>

<span class="n">df</span> <span class="o">=</span> <span class="n">turnstile_weather</span><span class="p">[[</span><span class="s">&#39;DATEn&#39;</span><span class="p">,</span> <span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">,</span> <span class="s">&#39;rain&#39;</span><span class="p">]]</span>
<span class="n">df</span><span class="o">.</span><span class="n">is_copy</span> <span class="o">=</span> <span class="bp">False</span>

<span class="c"># get the weekday as a string</span>
<span class="n">f</span> <span class="o">=</span> <span class="k">lambda</span> <span class="n">x</span><span class="p">:</span> <span class="n">datetime</span><span class="o">.</span><span class="n">strptime</span><span class="p">(</span><span class="n">x</span><span class="p">,</span> <span class="s">&quot;%Y-%m-</span><span class="si">%d</span><span class="s">&quot;</span><span class="p">)</span><span class="o">.</span><span class="n">strftime</span><span class="p">(</span><span class="s">&#39;%A&#39;</span><span class="p">)</span>

<span class="n">df</span><span class="p">[</span><span class="s">&#39;weekday&#39;</span><span class="p">]</span> <span class="o">=</span> <span class="n">df</span><span class="p">[</span><span class="s">&#39;DATEn&#39;</span><span class="p">]</span><span class="o">.</span><span class="n">apply</span><span class="p">(</span><span class="n">f</span><span class="p">)</span>



<span class="k">print</span> <span class="n">ggplot</span><span class="p">(</span><span class="n">df</span><span class="p">,</span> <span class="n">aes</span><span class="p">(</span><span class="n">x</span> <span class="o">=</span> <span class="s">&#39;ENTRIESn_hourly&#39;</span><span class="p">,</span> <span class="n">colour</span><span class="o">=</span><span class="s">&#39;factor(rain)&#39;</span><span class="p">))</span> \
        <span class="o">+</span> <span class="n">geom_density</span><span class="p">()</span> \
        <span class="o">+</span> <span class="n">xlim</span><span class="p">(</span><span class="mi">0</span><span class="p">,</span><span class="mi">2500</span><span class="p">)</span> \
        <span class="o">+</span> <span class="n">facet_wrap</span><span class="p">(</span><span class="s">&#39;weekday&#39;</span><span class="p">)</span>
</pre></div>

</div>
</div>
</div>

<div class="output_wrapper">
<div class="output">







<div class="output_area"><div class="prompt"></div>
<div class="output_subarea output_stream output_stdout output_text">
<pre>&lt;ggplot: (297194733)&gt;
</pre>
</div>
</div>

</div>
</div>

</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>This faceted grid shows the density functions of ENTRIESnhourly with and without rain for each day of the week. Currently legends do not work within ggplot facets. Red represents without rain, and blue represents with rain. It appears for every day, except Monday, that the distribution of ENTRIESnhourly has a fatter right tail when there is rain.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h1 id="Reflection">Reflection<a class="anchor-link" href="#Reflection">&#182;</a></h1>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<h3 id="Shortcomings-of-the-Data-Set-and-Methods-of-Analysis">Shortcomings of the Data Set and Methods of Analysis<a class="anchor-link" href="#Shortcomings-of-the-Data-Set-and-Methods-of-Analysis">&#182;</a></h3>
</div>
</div>
</div>
<div class="cell border-box-sizing text_cell rendered">
<div class="prompt input_prompt">
</div>
<div class="inner_cell">
<div class="text_cell_render border-box-sizing rendered_html">
<p>We're only working with a single month of MTA data, which is subject to effects of seasonality, as the time of year may also affect ridership. Additionally, this month contains a Monday holiday, which is reflected in the visualizations in Section 3.2 and Section 4.</p>
<p>The biggest shortcoming with this dataset is the discrepency between the units of the two joined datasets. The MTA turnstile entry data is produced on an hourly basis, whereas the weather data is produced daily. When it rains at any point in a given day, every hour of that day will reflect that it rained. This prevents a truly granular analysis of how the weather can affect ridership within a day.</p>

</div>
</div>
</div>
<div class="cell border-box-sizing code_cell rendered">
<div class="input">
<div class="prompt input_prompt">In&nbsp;[&nbsp;]:</div>
<div class="inner_cell">
    <div class="input_area">
<div class=" highlight hl-ipython2"><pre> 
</pre></div>

</div>
</div>
</div>

</div>
    </div>
  </div>
</body>
</html>
