---
layout: post
title: Tự học ngôn ngữ R trong 7 ngày
subtitle: Day 3. Data Transformation
tags: [R, Data Science, Data Transformation]
comments: true
categories: R DataScience DataAnalysis
author: Chí Trung HÀ
---

# R for Data Science (2e)

# Day 3. Data Transformation

## Introduction

This [chapter](https://r4ds.hadley.nz/data-transform) will introduce you to data transformation using the dplyr package and a new dataset on flights that departed from New York City in 2013.

### Prerequisites


```R
# install.packages("nycflights13")
```


```R
library(nycflights13)
library(tidyverse)
```

### nycflights13

This dataset contains all *336,776 flights that departed from New York City in 2013*. The data comes from the US Bureau of Transportation Statistics, and is documented in `?flights`. For short:

     Data frame with columns year, month, day Date of departure.

     dep_time, arr_time Actual departure and arrival times (format HHMM or HMM), local tz.

     sched_dep_time, sched_arr_time Scheduled departure and arrival times (format HHMM or HMM), local tz.


```R
flights
```


<table class="dataframe">
<caption>A tibble: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>




```R
glimpse(flights)
```

    Rows: 336,776
    Columns: 19
    $ year           [3m[90m<int>[39m[23m 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2013, 2~
    $ month          [3m[90m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1~
    $ day            [3m[90m<int>[39m[23m 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1, 1~
    $ dep_time       [3m[90m<int>[39m[23m 517, 533, 542, 544, 554, 554, 555, 557, 557, 558, 558, ~
    $ sched_dep_time [3m[90m<int>[39m[23m 515, 529, 540, 545, 600, 558, 600, 600, 600, 600, 600, ~
    $ dep_delay      [3m[90m<dbl>[39m[23m 2, 4, 2, -1, -6, -4, -5, -3, -3, -2, -2, -2, -2, -2, -1~
    $ arr_time       [3m[90m<int>[39m[23m 830, 850, 923, 1004, 812, 740, 913, 709, 838, 753, 849,~
    $ sched_arr_time [3m[90m<int>[39m[23m 819, 830, 850, 1022, 837, 728, 854, 723, 846, 745, 851,~
    $ arr_delay      [3m[90m<dbl>[39m[23m 11, 20, 33, -18, -25, 12, 19, -14, -8, 8, -2, -3, 7, -1~
    $ carrier        [3m[90m<chr>[39m[23m "UA", "UA", "AA", "B6", "DL", "UA", "B6", "EV", "B6", "~
    $ flight         [3m[90m<int>[39m[23m 1545, 1714, 1141, 725, 461, 1696, 507, 5708, 79, 301, 4~
    $ tailnum        [3m[90m<chr>[39m[23m "N14228", "N24211", "N619AA", "N804JB", "N668DN", "N394~
    $ origin         [3m[90m<chr>[39m[23m "EWR", "LGA", "JFK", "JFK", "LGA", "EWR", "EWR", "LGA",~
    $ dest           [3m[90m<chr>[39m[23m "IAH", "IAH", "MIA", "BQN", "ATL", "ORD", "FLL", "IAD",~
    $ air_time       [3m[90m<dbl>[39m[23m 227, 227, 160, 183, 116, 150, 158, 53, 140, 138, 149, 1~
    $ distance       [3m[90m<dbl>[39m[23m 1400, 1416, 1089, 1576, 762, 719, 1065, 229, 944, 733, ~
    $ hour           [3m[90m<dbl>[39m[23m 5, 5, 5, 5, 6, 5, 6, 6, 6, 6, 6, 6, 6, 6, 6, 5, 6, 6, 6~
    $ minute         [3m[90m<dbl>[39m[23m 15, 29, 40, 45, 0, 58, 0, 0, 0, 0, 0, 0, 0, 0, 0, 59, 0~
    $ time_hour      [3m[90m<dttm>[39m[23m 2013-01-01 05:00:00, 2013-01-01 05:00:00, 2013-01-01 0~


### `dplyr` basics

1. The first argument is always a data frame.
2. The subsequent arguments typically describe which columns to operate on, using the variable names (without quotes).
3. The output is always a new data frame.

`|>`: the pipe to combining multiple verbs (functions): the pipe takes the thing on its left and passes it along to the function on its right so that `x |> f(y)` is equivalent to `f(x, y)`, and `x |> f(y) |> g(z)` is equivalent to `g(f(x, y), z)`. The easiest way to pronounce the pipe is *“then”*. 

`dplyr`’s verbs are organized into four groups based on what they operate on: **rows**, **columns**, **groups**, or **tables**. In the following sections you’ll learn the most important verbs for rows, columns, and groups, then we’ll come back to the join verbs that work on tables in Chapter 19.


```R
# |>: the pipe to combining multiple verbs (functions)
flights |>
  filter(dest == "IAH") |> 
  group_by(year, month, day) |> 
  summarize(
    arr_delay = mean(arr_delay, na.rm = TRUE)
  )
```

    [1m[22m`summarise()` has grouped output by 'year', 'month'. You can override using the
    `.groups` argument.



<table class="dataframe">
<caption>A grouped_df: 365 x 4</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>arr_delay</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td> 1</td><td> 17.850000</td></tr>
	<tr><td>2013</td><td>1</td><td> 2</td><td>  7.000000</td></tr>
	<tr><td>2013</td><td>1</td><td> 3</td><td> 18.315789</td></tr>
	<tr><td>2013</td><td>1</td><td> 4</td><td> -3.200000</td></tr>
	<tr><td>2013</td><td>1</td><td> 5</td><td> 20.230769</td></tr>
	<tr><td>2013</td><td>1</td><td> 6</td><td>  9.277778</td></tr>
	<tr><td>2013</td><td>1</td><td> 7</td><td> -7.736842</td></tr>
	<tr><td>2013</td><td>1</td><td> 8</td><td>  7.789474</td></tr>
	<tr><td>2013</td><td>1</td><td> 9</td><td> 18.055556</td></tr>
	<tr><td>2013</td><td>1</td><td>10</td><td>  6.684211</td></tr>
	<tr><td>2013</td><td>1</td><td>11</td><td>-22.526316</td></tr>
	<tr><td>2013</td><td>1</td><td>12</td><td>-19.923077</td></tr>
	<tr><td>2013</td><td>1</td><td>13</td><td> 14.833333</td></tr>
	<tr><td>2013</td><td>1</td><td>14</td><td> 17.421053</td></tr>
	<tr><td>2013</td><td>1</td><td>15</td><td> 26.105263</td></tr>
	<tr><td>2013</td><td>1</td><td>16</td><td> 40.105263</td></tr>
	<tr><td>2013</td><td>1</td><td>17</td><td> -7.894737</td></tr>
	<tr><td>2013</td><td>1</td><td>18</td><td> -5.210526</td></tr>
	<tr><td>2013</td><td>1</td><td>19</td><td>  2.153846</td></tr>
	<tr><td>2013</td><td>1</td><td>20</td><td> 10.352941</td></tr>
	<tr><td>2013</td><td>1</td><td>21</td><td> 19.789474</td></tr>
	<tr><td>2013</td><td>1</td><td>22</td><td> -5.055556</td></tr>
	<tr><td>2013</td><td>1</td><td>23</td><td> -6.947368</td></tr>
	<tr><td>2013</td><td>1</td><td>24</td><td>-15.894737</td></tr>
	<tr><td>2013</td><td>1</td><td>25</td><td>-10.368421</td></tr>
	<tr><td>2013</td><td>1</td><td>26</td><td> -8.384615</td></tr>
	<tr><td>2013</td><td>1</td><td>27</td><td>-16.055556</td></tr>
	<tr><td>2013</td><td>1</td><td>28</td><td>-15.157895</td></tr>
	<tr><td>2013</td><td>1</td><td>29</td><td>-20.842105</td></tr>
	<tr><td>2013</td><td>1</td><td>30</td><td> 20.842105</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>12</td><td> 2</td><td>-6.5000000</td></tr>
	<tr><td>2013</td><td>12</td><td> 3</td><td>-8.4545455</td></tr>
	<tr><td>2013</td><td>12</td><td> 4</td><td>-3.1363636</td></tr>
	<tr><td>2013</td><td>12</td><td> 5</td><td>51.7142857</td></tr>
	<tr><td>2013</td><td>12</td><td> 6</td><td>14.8181818</td></tr>
	<tr><td>2013</td><td>12</td><td> 7</td><td>18.8666667</td></tr>
	<tr><td>2013</td><td>12</td><td> 8</td><td>29.4705882</td></tr>
	<tr><td>2013</td><td>12</td><td> 9</td><td>34.5454545</td></tr>
	<tr><td>2013</td><td>12</td><td>10</td><td>60.3529412</td></tr>
	<tr><td>2013</td><td>12</td><td>11</td><td> 3.4090909</td></tr>
	<tr><td>2013</td><td>12</td><td>12</td><td> 5.3333333</td></tr>
	<tr><td>2013</td><td>12</td><td>13</td><td>-3.0000000</td></tr>
	<tr><td>2013</td><td>12</td><td>14</td><td>54.6666667</td></tr>
	<tr><td>2013</td><td>12</td><td>15</td><td> 6.6470588</td></tr>
	<tr><td>2013</td><td>12</td><td>16</td><td>-8.1818182</td></tr>
	<tr><td>2013</td><td>12</td><td>17</td><td>33.4500000</td></tr>
	<tr><td>2013</td><td>12</td><td>18</td><td> 8.4090909</td></tr>
	<tr><td>2013</td><td>12</td><td>19</td><td>-6.6190476</td></tr>
	<tr><td>2013</td><td>12</td><td>20</td><td>20.1000000</td></tr>
	<tr><td>2013</td><td>12</td><td>21</td><td>50.1250000</td></tr>
	<tr><td>2013</td><td>12</td><td>22</td><td>28.3333333</td></tr>
	<tr><td>2013</td><td>12</td><td>23</td><td>28.8181818</td></tr>
	<tr><td>2013</td><td>12</td><td>24</td><td> 2.3125000</td></tr>
	<tr><td>2013</td><td>12</td><td>25</td><td> 7.5833333</td></tr>
	<tr><td>2013</td><td>12</td><td>26</td><td>-0.4444444</td></tr>
	<tr><td>2013</td><td>12</td><td>27</td><td> 6.1666667</td></tr>
	<tr><td>2013</td><td>12</td><td>28</td><td> 9.5000000</td></tr>
	<tr><td>2013</td><td>12</td><td>29</td><td>23.6111111</td></tr>
	<tr><td>2013</td><td>12</td><td>30</td><td>23.6842105</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>-4.9333333</td></tr>
</tbody>
</table>



## Rows

Some important verbs that operate on rows:
* `filter()`: allows you to keep rows based on the values of the columns without changing their order
* `arrange()`: changes the order of the rows based on the value of the columns (without changing which are present)

Both functions only affect the rows, and the columns are left unchanged.
* `distinct()` which finds rows with unique values but unlike `arrange()` and `filter()` it can also optionally modify the columns.

### `filter()`


```R
flights |> filter(dep_delay > 1000)
```


<table class="dataframe">
<caption>A tibble: 5 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td> 9</td><td> 641</td><td> 900</td><td>1301</td><td>1242</td><td>1530</td><td>1272</td><td>HA</td><td>  51</td><td>N384HA</td><td>JFK</td><td>HNL</td><td>640</td><td>4983</td><td> 9</td><td> 0</td><td>2013-01-09 09:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>10</td><td>1121</td><td>1635</td><td>1126</td><td>1239</td><td>1810</td><td>1109</td><td>MQ</td><td>3695</td><td>N517MQ</td><td>EWR</td><td>ORD</td><td>111</td><td> 719</td><td>16</td><td>35</td><td>2013-01-10 16:00:00</td></tr>
	<tr><td>2013</td><td>6</td><td>15</td><td>1432</td><td>1935</td><td>1137</td><td>1607</td><td>2120</td><td>1127</td><td>MQ</td><td>3535</td><td>N504MQ</td><td>JFK</td><td>CMH</td><td> 74</td><td> 483</td><td>19</td><td>35</td><td>2013-06-15 19:00:00</td></tr>
	<tr><td>2013</td><td>7</td><td>22</td><td> 845</td><td>1600</td><td>1005</td><td>1044</td><td>1815</td><td> 989</td><td>MQ</td><td>3075</td><td>N665MQ</td><td>JFK</td><td>CVG</td><td> 96</td><td> 589</td><td>16</td><td> 0</td><td>2013-07-22 16:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>20</td><td>1139</td><td>1845</td><td>1014</td><td>1457</td><td>2210</td><td>1007</td><td>AA</td><td> 177</td><td>N338AA</td><td>JFK</td><td>SFO</td><td>354</td><td>2586</td><td>18</td><td>45</td><td>2013-09-20 18:00:00</td></tr>
</tbody>
</table>




```R
# Flights that departed on January 1
flights |> filter(month==1 & day==1)
```


<table class="dataframe">
<caption>A tibble: 842 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2140</td><td>2135</td><td>  5</td><td> 210</td><td> 224</td><td>-14</td><td>B6</td><td> 701</td><td>N284JB</td><td>JFK</td><td>SJU</td><td>189</td><td>1598</td><td>21</td><td>35</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2157</td><td>2155</td><td>  2</td><td>  43</td><td>  41</td><td>  2</td><td>B6</td><td>  43</td><td>N537JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>21</td><td>55</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2158</td><td>2200</td><td> -2</td><td>2254</td><td>2307</td><td>-13</td><td>EV</td><td>4103</td><td>N14998</td><td>EWR</td><td>BWI</td><td> 36</td><td> 169</td><td>22</td><td> 0</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2205</td><td>1720</td><td>285</td><td>  46</td><td>2040</td><td>246</td><td>AA</td><td>1999</td><td>N5DNAA</td><td>EWR</td><td>MIA</td><td>146</td><td>1085</td><td>17</td><td>20</td><td>2013-01-01 17:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2209</td><td>2145</td><td> 24</td><td>  58</td><td>  37</td><td> 21</td><td>B6</td><td>  35</td><td>N608JB</td><td>JFK</td><td>PBI</td><td>143</td><td>1028</td><td>21</td><td>45</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2209</td><td>2155</td><td> 14</td><td>2400</td><td>2337</td><td> 23</td><td>B6</td><td>1109</td><td>N216JB</td><td>JFK</td><td>RDU</td><td> 86</td><td> 427</td><td>21</td><td>55</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2211</td><td>2145</td><td> 26</td><td>2339</td><td>2311</td><td> 28</td><td>B6</td><td> 104</td><td>N228JB</td><td>JFK</td><td>BUF</td><td> 64</td><td> 301</td><td>21</td><td>45</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2217</td><td>2229</td><td>-12</td><td> 249</td><td> 315</td><td>-26</td><td>B6</td><td> 713</td><td>N547JB</td><td>JFK</td><td>SJU</td><td>191</td><td>1598</td><td>22</td><td>29</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2217</td><td>2130</td><td> 47</td><td> 140</td><td>  27</td><td> 73</td><td>B6</td><td>  21</td><td>N516JB</td><td>JFK</td><td>TPA</td><td>163</td><td>1005</td><td>21</td><td>30</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2221</td><td>2000</td><td>141</td><td>2331</td><td>2124</td><td>127</td><td>EV</td><td>4462</td><td>N13566</td><td>EWR</td><td>BUF</td><td> 56</td><td> 282</td><td>20</td><td> 0</td><td>2013-01-01 20:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2224</td><td>2200</td><td> 24</td><td>2324</td><td>2316</td><td>  8</td><td>EV</td><td>4206</td><td>N16561</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>22</td><td> 0</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2229</td><td>2159</td><td> 30</td><td> 149</td><td> 100</td><td> 49</td><td>B6</td><td>  11</td><td>N531JB</td><td>JFK</td><td>FLL</td><td>153</td><td>1069</td><td>21</td><td>59</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2240</td><td>2245</td><td> -5</td><td>2340</td><td>2356</td><td>-16</td><td>B6</td><td> 608</td><td>N279JB</td><td>JFK</td><td>PWM</td><td> 44</td><td> 273</td><td>22</td><td>45</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2250</td><td>2255</td><td> -5</td><td>2352</td><td>2359</td><td> -7</td><td>B6</td><td>1018</td><td>N521JB</td><td>JFK</td><td>BOS</td><td> 37</td><td> 187</td><td>22</td><td>55</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2302</td><td>2200</td><td> 62</td><td>2342</td><td>2253</td><td> 49</td><td>EV</td><td>4276</td><td>N13903</td><td>EWR</td><td>BDL</td><td> 24</td><td> 116</td><td>22</td><td> 0</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2306</td><td>2245</td><td> 21</td><td>  28</td><td>   5</td><td> 23</td><td>B6</td><td>  30</td><td>N281JB</td><td>JFK</td><td>ROC</td><td> 59</td><td> 264</td><td>22</td><td>45</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2307</td><td>2245</td><td> 22</td><td>  32</td><td>2357</td><td> 35</td><td>B6</td><td> 128</td><td>N178JB</td><td>JFK</td><td>BTV</td><td> 59</td><td> 266</td><td>22</td><td>45</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2310</td><td>2255</td><td> 15</td><td>  24</td><td>  15</td><td>  9</td><td>B6</td><td> 112</td><td>N646JB</td><td>JFK</td><td>BUF</td><td> 57</td><td> 301</td><td>22</td><td>55</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2312</td><td>2000</td><td>192</td><td>  21</td><td>2110</td><td>191</td><td>EV</td><td>4312</td><td>N13958</td><td>EWR</td><td>DCA</td><td> 44</td><td> 199</td><td>20</td><td> 0</td><td>2013-01-01 20:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2323</td><td>2200</td><td> 83</td><td>  22</td><td>2313</td><td> 69</td><td>EV</td><td>4257</td><td>N13538</td><td>EWR</td><td>BTV</td><td> 44</td><td> 266</td><td>22</td><td> 0</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2326</td><td>2130</td><td>116</td><td> 131</td><td>  18</td><td> 73</td><td>B6</td><td> 199</td><td>N594JB</td><td>JFK</td><td>LAS</td><td>290</td><td>2248</td><td>21</td><td>30</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2327</td><td>2250</td><td> 37</td><td>  32</td><td>2359</td><td> 33</td><td>B6</td><td>  22</td><td>N639JB</td><td>JFK</td><td>SYR</td><td> 45</td><td> 209</td><td>22</td><td>50</td><td>2013-01-01 22:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2343</td><td>1724</td><td>379</td><td> 314</td><td>1938</td><td>456</td><td>EV</td><td>4321</td><td>N21197</td><td>EWR</td><td>MCI</td><td>222</td><td>1092</td><td>17</td><td>24</td><td>2013-01-01 17:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2353</td><td>2359</td><td> -6</td><td> 425</td><td> 445</td><td>-20</td><td>B6</td><td> 739</td><td>N591JB</td><td>JFK</td><td>PSE</td><td>195</td><td>1617</td><td>23</td><td>59</td><td>2013-01-01 23:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2353</td><td>2359</td><td> -6</td><td> 418</td><td> 442</td><td>-24</td><td>B6</td><td> 707</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>185</td><td>1598</td><td>23</td><td>59</td><td>2013-01-01 23:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2356</td><td>2359</td><td> -3</td><td> 425</td><td> 437</td><td>-12</td><td>B6</td><td> 727</td><td>N588JB</td><td>JFK</td><td>BQN</td><td>186</td><td>1576</td><td>23</td><td>59</td><td>2013-01-01 23:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  NA</td><td>1630</td><td> NA</td><td>  NA</td><td>1815</td><td> NA</td><td>EV</td><td>4308</td><td>N18120</td><td>EWR</td><td>RDU</td><td> NA</td><td> 416</td><td>16</td><td>30</td><td>2013-01-01 16:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  NA</td><td>1935</td><td> NA</td><td>  NA</td><td>2240</td><td> NA</td><td>AA</td><td> 791</td><td>N3EHAA</td><td>LGA</td><td>DFW</td><td> NA</td><td>1389</td><td>19</td><td>35</td><td>2013-01-01 19:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  NA</td><td>1500</td><td> NA</td><td>  NA</td><td>1825</td><td> NA</td><td>AA</td><td>1925</td><td>N3EVAA</td><td>LGA</td><td>MIA</td><td> NA</td><td>1096</td><td>15</td><td> 0</td><td>2013-01-01 15:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  NA</td><td> 600</td><td> NA</td><td>  NA</td><td> 901</td><td> NA</td><td>B6</td><td> 125</td><td>N618JB</td><td>JFK</td><td>FLL</td><td> NA</td><td>1069</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
</tbody>
</table>




```R
# A shorter way to select flights that departed in January or February
flights |> 
  filter(month %in% c(1, 2))
  # the same as filter(month==1 | month==2)
  # but not filter(month == 1 | 2) - error!
```


<table class="dataframe">
<caption>A tibble: 51955 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2157</td><td>2007</td><td>110</td><td>2344</td><td>2206</td><td> 98</td><td>EV</td><td>4572</td><td>N29906</td><td>EWR</td><td>GSP</td><td> 93</td><td> 594</td><td>20</td><td> 7</td><td>2013-02-28 20:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2158</td><td>1910</td><td>168</td><td>  19</td><td>2215</td><td>124</td><td>AA</td><td>2075</td><td>N4YSAA</td><td>EWR</td><td>DFW</td><td>182</td><td>1372</td><td>19</td><td>10</td><td>2013-02-28 19:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2158</td><td>2145</td><td> 13</td><td>  49</td><td>  34</td><td> 15</td><td>B6</td><td>  35</td><td>N708JB</td><td>JFK</td><td>PBI</td><td>151</td><td>1028</td><td>21</td><td>45</td><td>2013-02-28 21:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2201</td><td>2155</td><td>  6</td><td>  59</td><td>  41</td><td> 18</td><td>B6</td><td>  43</td><td>N579JB</td><td>JFK</td><td>MCO</td><td>149</td><td> 944</td><td>21</td><td>55</td><td>2013-02-28 21:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2205</td><td>2045</td><td> 80</td><td>2304</td><td>2216</td><td> 48</td><td>9E</td><td>3395</td><td>N916XJ</td><td>JFK</td><td>DCA</td><td> 38</td><td> 213</td><td>20</td><td>45</td><td>2013-02-28 20:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2205</td><td>2159</td><td>  6</td><td> 106</td><td>  56</td><td> 10</td><td>B6</td><td>  11</td><td>N554JB</td><td>JFK</td><td>FLL</td><td>158</td><td>1069</td><td>21</td><td>59</td><td>2013-02-28 21:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2218</td><td>2150</td><td> 28</td><td> 115</td><td>  42</td><td> 33</td><td>B6</td><td> 325</td><td>N504JB</td><td>JFK</td><td>TPA</td><td>154</td><td>1005</td><td>21</td><td>50</td><td>2013-02-28 21:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2223</td><td>2023</td><td>120</td><td> 252</td><td> 114</td><td> 98</td><td>UA</td><td>1071</td><td>N37298</td><td>EWR</td><td>BQN</td><td>188</td><td>1585</td><td>20</td><td>23</td><td>2013-02-28 20:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2226</td><td>2029</td><td>117</td><td> 115</td><td>2333</td><td>102</td><td>UA</td><td> 771</td><td>N560UA</td><td>JFK</td><td>LAX</td><td>313</td><td>2475</td><td>20</td><td>29</td><td>2013-02-28 20:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2229</td><td>2230</td><td> -1</td><td> 258</td><td> 312</td><td>-14</td><td>B6</td><td> 713</td><td>N523JB</td><td>JFK</td><td>SJU</td><td>193</td><td>1598</td><td>22</td><td>30</td><td>2013-02-28 22:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2239</td><td>2245</td><td> -6</td><td>2339</td><td>2354</td><td>-15</td><td>B6</td><td> 608</td><td>N197JB</td><td>JFK</td><td>PWM</td><td> 44</td><td> 273</td><td>22</td><td>45</td><td>2013-02-28 22:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2242</td><td>2250</td><td> -8</td><td>2350</td><td>   5</td><td>-15</td><td>B6</td><td>  30</td><td>N351JB</td><td>JFK</td><td>ROC</td><td> 51</td><td> 264</td><td>22</td><td>50</td><td>2013-02-28 22:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2245</td><td>2245</td><td>  0</td><td>   5</td><td>2356</td><td>  9</td><td>B6</td><td> 128</td><td>N184JB</td><td>JFK</td><td>BTV</td><td> 48</td><td> 266</td><td>22</td><td>45</td><td>2013-02-28 22:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2254</td><td>2258</td><td> -4</td><td>  10</td><td>  19</td><td> -9</td><td>B6</td><td> 112</td><td>N655JB</td><td>JFK</td><td>BUF</td><td> 53</td><td> 301</td><td>22</td><td>58</td><td>2013-02-28 22:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2257</td><td>2140</td><td> 77</td><td>2338</td><td>2241</td><td> 57</td><td>EV</td><td>4276</td><td>N12567</td><td>EWR</td><td>BDL</td><td> 24</td><td> 116</td><td>21</td><td>40</td><td>2013-02-28 21:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2257</td><td>2255</td><td>  2</td><td>2400</td><td>2357</td><td>  3</td><td>B6</td><td>1018</td><td>N807JB</td><td>JFK</td><td>BOS</td><td> 35</td><td> 187</td><td>22</td><td>55</td><td>2013-02-28 22:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2323</td><td>2251</td><td> 32</td><td>  18</td><td>2357</td><td> 21</td><td>B6</td><td>  22</td><td>N279JB</td><td>JFK</td><td>SYR</td><td> 40</td><td> 209</td><td>22</td><td>51</td><td>2013-02-28 22:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2342</td><td>2352</td><td>-10</td><td> 413</td><td> 437</td><td>-24</td><td>B6</td><td> 739</td><td>N656JB</td><td>JFK</td><td>PSE</td><td>193</td><td>1617</td><td>23</td><td>52</td><td>2013-02-28 23:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2356</td><td>2358</td><td> -2</td><td> 423</td><td> 438</td><td>-15</td><td>B6</td><td> 707</td><td>N646JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>23</td><td>58</td><td>2013-02-28 23:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>2359</td><td>2359</td><td>  0</td><td> 443</td><td> 438</td><td>  5</td><td>B6</td><td> 727</td><td>N641JB</td><td>JFK</td><td>BQN</td><td>192</td><td>1576</td><td>23</td><td>59</td><td>2013-02-28 23:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td> 600</td><td> NA</td><td>  NA</td><td> 722</td><td> NA</td><td>EV</td><td>5739</td><td>N833AS</td><td>LGA</td><td>IAD</td><td> NA</td><td> 229</td><td> 6</td><td> 0</td><td>2013-02-28 06:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td>1820</td><td> NA</td><td>  NA</td><td>2003</td><td> NA</td><td>EV</td><td>5409</td><td>N740EV</td><td>LGA</td><td>MSN</td><td> NA</td><td> 812</td><td>18</td><td>20</td><td>2013-02-28 18:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td>1154</td><td> NA</td><td>  NA</td><td>1447</td><td> NA</td><td>B6</td><td>  27</td><td>N274JB</td><td>JFK</td><td>TPA</td><td> NA</td><td>1005</td><td>11</td><td>54</td><td>2013-02-28 11:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td> 900</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>US</td><td>2120</td><td>NA    </td><td>LGA</td><td>BOS</td><td> NA</td><td> 184</td><td> 9</td><td> 0</td><td>2013-02-28 09:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td> 605</td><td> NA</td><td>  NA</td><td> 805</td><td> NA</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td> NA</td><td> 502</td><td> 6</td><td> 5</td><td>2013-02-28 06:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td> 850</td><td> NA</td><td>  NA</td><td>1035</td><td> NA</td><td>MQ</td><td>4558</td><td>N737MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td> 8</td><td>50</td><td>2013-02-28 08:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td> 905</td><td> NA</td><td>  NA</td><td>1115</td><td> NA</td><td>MQ</td><td>4478</td><td>N722MQ</td><td>LGA</td><td>DTW</td><td> NA</td><td> 502</td><td> 9</td><td> 5</td><td>2013-02-28 09:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td>1115</td><td> NA</td><td>  NA</td><td>1310</td><td> NA</td><td>MQ</td><td>4485</td><td>N725MQ</td><td>LGA</td><td>CMH</td><td> NA</td><td> 479</td><td>11</td><td>15</td><td>2013-02-28 11:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td> 830</td><td> NA</td><td>  NA</td><td>1205</td><td> NA</td><td>UA</td><td>1480</td><td>NA    </td><td>EWR</td><td>SFO</td><td> NA</td><td>2565</td><td> 8</td><td>30</td><td>2013-02-28 08:00:00</td></tr>
	<tr><td>2013</td><td>2</td><td>28</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1147</td><td> NA</td><td>UA</td><td> 443</td><td>NA    </td><td>JFK</td><td>LAX</td><td> NA</td><td>2475</td><td> 8</td><td>40</td><td>2013-02-28 08:00:00</td></tr>
</tbody>
</table>



### `arrange()`


```R
flights |> arrange(year, month, day, dep_time)
```


<table class="dataframe">
<caption>A tibble: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2155</td><td>2039</td><td> 76</td><td> 253</td><td>2355</td><td> NA</td><td>B6</td><td>1205</td><td>N627JB</td><td>JFK</td><td>PDX</td><td> NA</td><td>2454</td><td>20</td><td>39</td><td>2013-12-31 20:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2155</td><td>2150</td><td>  5</td><td> 110</td><td>  51</td><td> 19</td><td>B6</td><td>1901</td><td>N729JB</td><td>JFK</td><td>FLL</td><td>164</td><td>1069</td><td>21</td><td>50</td><td>2013-12-31 21:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2159</td><td>2155</td><td>  4</td><td>  55</td><td>  46</td><td>  9</td><td>B6</td><td>2053</td><td>N593JB</td><td>JFK</td><td>PBI</td><td>155</td><td>1028</td><td>21</td><td>55</td><td>2013-12-31 21:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2206</td><td>2110</td><td> 56</td><td>  44</td><td>2339</td><td> 65</td><td>B6</td><td> 775</td><td>N184JB</td><td>JFK</td><td>MSY</td><td>195</td><td>1182</td><td>21</td><td>10</td><td>2013-12-31 21:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2211</td><td>2159</td><td> 12</td><td> 100</td><td>  45</td><td> 15</td><td>B6</td><td>1183</td><td>N715JB</td><td>JFK</td><td>MCO</td><td>148</td><td> 944</td><td>21</td><td>59</td><td>2013-12-31 21:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2218</td><td>2219</td><td> -1</td><td> 315</td><td> 304</td><td> 11</td><td>B6</td><td>1203</td><td>N625JB</td><td>JFK</td><td>SJU</td><td>202</td><td>1598</td><td>22</td><td>19</td><td>2013-12-31 22:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2235</td><td>2245</td><td>-10</td><td>2351</td><td>2355</td><td> -4</td><td>B6</td><td> 234</td><td>N355JB</td><td>JFK</td><td>BTV</td><td> 49</td><td> 266</td><td>22</td><td>45</td><td>2013-12-31 22:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2245</td><td>2250</td><td> -5</td><td>2359</td><td>2356</td><td>  3</td><td>B6</td><td>1816</td><td>N318JB</td><td>JFK</td><td>SYR</td><td> 51</td><td> 209</td><td>22</td><td>50</td><td>2013-12-31 22:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2310</td><td>2255</td><td> 15</td><td>   7</td><td>2356</td><td> 11</td><td>B6</td><td> 718</td><td>N279JB</td><td>JFK</td><td>BOS</td><td> 40</td><td> 187</td><td>22</td><td>55</td><td>2013-12-31 22:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2321</td><td>2250</td><td> 31</td><td>  46</td><td>   8</td><td> 38</td><td>B6</td><td>2002</td><td>N179JB</td><td>JFK</td><td>BUF</td><td> 66</td><td> 301</td><td>22</td><td>50</td><td>2013-12-31 22:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2328</td><td>2330</td><td> -2</td><td> 412</td><td> 409</td><td>  3</td><td>B6</td><td>1389</td><td>N651JB</td><td>EWR</td><td>SJU</td><td>198</td><td>1608</td><td>23</td><td>30</td><td>2013-12-31 23:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2332</td><td>2245</td><td> 47</td><td>  58</td><td>   3</td><td> 55</td><td>B6</td><td> 486</td><td>N334JB</td><td>JFK</td><td>ROC</td><td> 60</td><td> 264</td><td>22</td><td>45</td><td>2013-12-31 22:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2355</td><td>2359</td><td> -4</td><td> 430</td><td> 440</td><td>-10</td><td>B6</td><td>1503</td><td>N509JB</td><td>JFK</td><td>SJU</td><td>195</td><td>1598</td><td>23</td><td>59</td><td>2013-12-31 23:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>2356</td><td>2359</td><td> -3</td><td> 436</td><td> 445</td><td> -9</td><td>B6</td><td> 745</td><td>N665JB</td><td>JFK</td><td>PSE</td><td>200</td><td>1617</td><td>23</td><td>59</td><td>2013-12-31 23:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>1520</td><td> NA</td><td>  NA</td><td>1705</td><td> NA</td><td>AA</td><td> 341</td><td>N568AA</td><td>LGA</td><td>ORD</td><td> NA</td><td> 733</td><td>15</td><td>20</td><td>2013-12-31 15:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>2025</td><td> NA</td><td>  NA</td><td>2205</td><td> NA</td><td>AA</td><td> 371</td><td>N482AA</td><td>LGA</td><td>ORD</td><td> NA</td><td> 733</td><td>20</td><td>25</td><td>2013-12-31 20:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>1932</td><td> NA</td><td>  NA</td><td>2305</td><td> NA</td><td>B6</td><td> 161</td><td>N516JB</td><td>JFK</td><td>SMF</td><td> NA</td><td>2521</td><td>19</td><td>32</td><td>2013-12-31 19:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>1505</td><td> NA</td><td>  NA</td><td>1725</td><td> NA</td><td>EV</td><td>4181</td><td>N24103</td><td>EWR</td><td>MCI</td><td> NA</td><td>1092</td><td>15</td><td> 5</td><td>2013-12-31 15:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>1000</td><td> NA</td><td>  NA</td><td>1252</td><td> NA</td><td>UA</td><td>1124</td><td>NA    </td><td>EWR</td><td>EGE</td><td> NA</td><td>1725</td><td>10</td><td> 0</td><td>2013-12-31 10:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1205</td><td> NA</td><td>UA</td><td>1151</td><td>NA    </td><td>EWR</td><td>SEA</td><td> NA</td><td>2402</td><td> 8</td><td>40</td><td>2013-12-31 08:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td> 754</td><td> NA</td><td>  NA</td><td>1118</td><td> NA</td><td>UA</td><td>1455</td><td>NA    </td><td>EWR</td><td>LAX</td><td> NA</td><td>2454</td><td> 7</td><td>54</td><td>2013-12-31 07:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>2000</td><td> NA</td><td>  NA</td><td>2146</td><td> NA</td><td>UA</td><td>1482</td><td>NA    </td><td>EWR</td><td>ORD</td><td> NA</td><td> 719</td><td>20</td><td> 0</td><td>2013-12-31 20:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>1500</td><td> NA</td><td>  NA</td><td>1817</td><td> NA</td><td>UA</td><td>1483</td><td>NA    </td><td>EWR</td><td>AUS</td><td> NA</td><td>1504</td><td>15</td><td> 0</td><td>2013-12-31 15:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>1430</td><td> NA</td><td>  NA</td><td>1750</td><td> NA</td><td>UA</td><td>1493</td><td>NA    </td><td>EWR</td><td>LAX</td><td> NA</td><td>2454</td><td>14</td><td>30</td><td>2013-12-31 14:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td> 855</td><td> NA</td><td>  NA</td><td>1142</td><td> NA</td><td>UA</td><td>1506</td><td>NA    </td><td>EWR</td><td>JAC</td><td> NA</td><td>1874</td><td> 8</td><td>55</td><td>2013-12-31 08:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td> 705</td><td> NA</td><td>  NA</td><td> 931</td><td> NA</td><td>UA</td><td>1729</td><td>NA    </td><td>EWR</td><td>DEN</td><td> NA</td><td>1605</td><td> 7</td><td> 5</td><td>2013-12-31 07:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td> 825</td><td> NA</td><td>  NA</td><td>1029</td><td> NA</td><td>US</td><td>1831</td><td>NA    </td><td>JFK</td><td>CLT</td><td> NA</td><td> 541</td><td> 8</td><td>25</td><td>2013-12-31 08:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td>1615</td><td> NA</td><td>  NA</td><td>1800</td><td> NA</td><td>MQ</td><td>3301</td><td>N844MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td>16</td><td>15</td><td>2013-12-31 16:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td> 600</td><td> NA</td><td>  NA</td><td> 735</td><td> NA</td><td>UA</td><td> 219</td><td>NA    </td><td>EWR</td><td>ORD</td><td> NA</td><td> 719</td><td> 6</td><td> 0</td><td>2013-12-31 06:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>31</td><td>  NA</td><td> 830</td><td> NA</td><td>  NA</td><td>1154</td><td> NA</td><td>UA</td><td> 443</td><td>NA    </td><td>JFK</td><td>LAX</td><td> NA</td><td>2475</td><td> 8</td><td>30</td><td>2013-12-31 08:00:00</td></tr>
</tbody>
</table>




```R
flights |> arrange(desc(dep_delay))
```


<table class="dataframe">
<caption>A tibble: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td> 1</td><td> 9</td><td> 641</td><td> 900</td><td>1301</td><td>1242</td><td>1530</td><td>1272</td><td>HA</td><td>  51</td><td>N384HA</td><td>JFK</td><td>HNL</td><td>640</td><td>4983</td><td> 9</td><td> 0</td><td>2013-01-09 09:00:00</td></tr>
	<tr><td>2013</td><td> 6</td><td>15</td><td>1432</td><td>1935</td><td>1137</td><td>1607</td><td>2120</td><td>1127</td><td>MQ</td><td>3535</td><td>N504MQ</td><td>JFK</td><td>CMH</td><td> 74</td><td> 483</td><td>19</td><td>35</td><td>2013-06-15 19:00:00</td></tr>
	<tr><td>2013</td><td> 1</td><td>10</td><td>1121</td><td>1635</td><td>1126</td><td>1239</td><td>1810</td><td>1109</td><td>MQ</td><td>3695</td><td>N517MQ</td><td>EWR</td><td>ORD</td><td>111</td><td> 719</td><td>16</td><td>35</td><td>2013-01-10 16:00:00</td></tr>
	<tr><td>2013</td><td> 9</td><td>20</td><td>1139</td><td>1845</td><td>1014</td><td>1457</td><td>2210</td><td>1007</td><td>AA</td><td> 177</td><td>N338AA</td><td>JFK</td><td>SFO</td><td>354</td><td>2586</td><td>18</td><td>45</td><td>2013-09-20 18:00:00</td></tr>
	<tr><td>2013</td><td> 7</td><td>22</td><td> 845</td><td>1600</td><td>1005</td><td>1044</td><td>1815</td><td> 989</td><td>MQ</td><td>3075</td><td>N665MQ</td><td>JFK</td><td>CVG</td><td> 96</td><td> 589</td><td>16</td><td> 0</td><td>2013-07-22 16:00:00</td></tr>
	<tr><td>2013</td><td> 4</td><td>10</td><td>1100</td><td>1900</td><td> 960</td><td>1342</td><td>2211</td><td> 931</td><td>DL</td><td>2391</td><td>N959DL</td><td>JFK</td><td>TPA</td><td>139</td><td>1005</td><td>19</td><td> 0</td><td>2013-04-10 19:00:00</td></tr>
	<tr><td>2013</td><td> 3</td><td>17</td><td>2321</td><td> 810</td><td> 911</td><td> 135</td><td>1020</td><td> 915</td><td>DL</td><td>2119</td><td>N927DA</td><td>LGA</td><td>MSP</td><td>167</td><td>1020</td><td> 8</td><td>10</td><td>2013-03-17 08:00:00</td></tr>
	<tr><td>2013</td><td> 6</td><td>27</td><td> 959</td><td>1900</td><td> 899</td><td>1236</td><td>2226</td><td> 850</td><td>DL</td><td>2007</td><td>N3762Y</td><td>JFK</td><td>PDX</td><td>313</td><td>2454</td><td>19</td><td> 0</td><td>2013-06-27 19:00:00</td></tr>
	<tr><td>2013</td><td> 7</td><td>22</td><td>2257</td><td> 759</td><td> 898</td><td> 121</td><td>1026</td><td> 895</td><td>DL</td><td>2047</td><td>N6716C</td><td>LGA</td><td>ATL</td><td>109</td><td> 762</td><td> 7</td><td>59</td><td>2013-07-22 07:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td> 5</td><td> 756</td><td>1700</td><td> 896</td><td>1058</td><td>2020</td><td> 878</td><td>AA</td><td> 172</td><td>N5DMAA</td><td>EWR</td><td>MIA</td><td>149</td><td>1085</td><td>17</td><td> 0</td><td>2013-12-05 17:00:00</td></tr>
	<tr><td>2013</td><td> 5</td><td> 3</td><td>1133</td><td>2055</td><td> 878</td><td>1250</td><td>2215</td><td> 875</td><td>MQ</td><td>3744</td><td>N523MQ</td><td>EWR</td><td>ORD</td><td>112</td><td> 719</td><td>20</td><td>55</td><td>2013-05-03 20:00:00</td></tr>
	<tr><td>2013</td><td> 1</td><td> 1</td><td> 848</td><td>1835</td><td> 853</td><td>1001</td><td>1950</td><td> 851</td><td>MQ</td><td>3944</td><td>N942MQ</td><td>JFK</td><td>BWI</td><td> 41</td><td> 184</td><td>18</td><td>35</td><td>2013-01-01 18:00:00</td></tr>
	<tr><td>2013</td><td> 2</td><td>10</td><td>2243</td><td> 830</td><td> 853</td><td> 100</td><td>1106</td><td> 834</td><td>F9</td><td> 835</td><td>N203FR</td><td>LGA</td><td>DEN</td><td>233</td><td>1620</td><td> 8</td><td>30</td><td>2013-02-10 08:00:00</td></tr>
	<tr><td>2013</td><td> 5</td><td>19</td><td> 713</td><td>1700</td><td> 853</td><td>1007</td><td>1955</td><td> 852</td><td>AA</td><td> 257</td><td>N3HEAA</td><td>JFK</td><td>LAS</td><td>323</td><td>2248</td><td>17</td><td> 0</td><td>2013-05-19 17:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>19</td><td> 734</td><td>1725</td><td> 849</td><td>1046</td><td>2039</td><td> 847</td><td>DL</td><td>1223</td><td>N375NC</td><td>EWR</td><td>SLC</td><td>290</td><td>1969</td><td>17</td><td>25</td><td>2013-12-19 17:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>17</td><td> 705</td><td>1700</td><td> 845</td><td>1026</td><td>2020</td><td> 846</td><td>AA</td><td> 172</td><td>N5EMAA</td><td>EWR</td><td>MIA</td><td>145</td><td>1085</td><td>17</td><td> 0</td><td>2013-12-17 17:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>14</td><td> 830</td><td>1845</td><td> 825</td><td>1210</td><td>2154</td><td> 856</td><td>DL</td><td>2391</td><td>N939DL</td><td>JFK</td><td>TPA</td><td>173</td><td>1005</td><td>18</td><td>45</td><td>2013-12-14 18:00:00</td></tr>
	<tr><td>2013</td><td> 4</td><td>19</td><td> 912</td><td>1940</td><td> 812</td><td>1228</td><td>2247</td><td> 821</td><td>DL</td><td>1435</td><td>N900DE</td><td>LGA</td><td>TPA</td><td>174</td><td>1010</td><td>19</td><td>40</td><td>2013-04-19 19:00:00</td></tr>
	<tr><td>2013</td><td> 6</td><td>27</td><td> 753</td><td>1830</td><td> 803</td><td> 937</td><td>2015</td><td> 802</td><td>AA</td><td>2019</td><td>N571AA</td><td>LGA</td><td>STL</td><td>134</td><td> 888</td><td>18</td><td>30</td><td>2013-06-27 18:00:00</td></tr>
	<tr><td>2013</td><td> 3</td><td>18</td><td>1020</td><td>2100</td><td> 800</td><td>1336</td><td>  32</td><td> 784</td><td>DL</td><td>2363</td><td>N624AG</td><td>JFK</td><td>LAX</td><td>335</td><td>2475</td><td>21</td><td> 0</td><td>2013-03-18 21:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td> 3</td><td> 603</td><td>1645</td><td> 798</td><td> 829</td><td>1913</td><td> 796</td><td>DL</td><td>2042</td><td>N990AT</td><td>EWR</td><td>ATL</td><td>109</td><td> 746</td><td>16</td><td>45</td><td>2013-11-03 16:00:00</td></tr>
	<tr><td>2013</td><td> 4</td><td>19</td><td> 617</td><td>1700</td><td> 797</td><td> 858</td><td>1955</td><td> 783</td><td>AA</td><td> 257</td><td>N3GJAA</td><td>JFK</td><td>LAS</td><td>313</td><td>2248</td><td>17</td><td> 0</td><td>2013-04-19 17:00:00</td></tr>
	<tr><td>2013</td><td> 6</td><td>27</td><td> 615</td><td>1705</td><td> 790</td><td> 853</td><td>2004</td><td> 769</td><td>DL</td><td> 503</td><td>N372DA</td><td>JFK</td><td>SAN</td><td>312</td><td>2446</td><td>17</td><td> 5</td><td>2013-06-27 17:00:00</td></tr>
	<tr><td>2013</td><td> 2</td><td>19</td><td>2324</td><td>1016</td><td> 788</td><td> 114</td><td>1227</td><td> 767</td><td>DL</td><td>2319</td><td>N324US</td><td>LGA</td><td>MSP</td><td>136</td><td>1020</td><td>10</td><td>16</td><td>2013-02-19 10:00:00</td></tr>
	<tr><td>2013</td><td> 6</td><td>27</td><td> 732</td><td>1825</td><td> 787</td><td> 932</td><td>2032</td><td> 780</td><td>DL</td><td>1715</td><td>N335NB</td><td>LGA</td><td>MSY</td><td>160</td><td>1183</td><td>18</td><td>25</td><td>2013-06-27 18:00:00</td></tr>
	<tr><td>2013</td><td> 2</td><td>24</td><td>1921</td><td> 615</td><td> 786</td><td>2135</td><td> 842</td><td> 773</td><td>DL</td><td> 575</td><td>N348NW</td><td>EWR</td><td>ATL</td><td>111</td><td> 746</td><td> 6</td><td>15</td><td>2013-02-24 06:00:00</td></tr>
	<tr><td>2013</td><td> 4</td><td>19</td><td> 606</td><td>1725</td><td> 761</td><td> 923</td><td>2020</td><td> 783</td><td>AA</td><td>1901</td><td>N3DGAA</td><td>JFK</td><td>IAH</td><td>222</td><td>1417</td><td>17</td><td>25</td><td>2013-04-19 17:00:00</td></tr>
	<tr><td>2013</td><td> 4</td><td>19</td><td> 758</td><td>1925</td><td> 753</td><td>1049</td><td>2225</td><td> 744</td><td>DL</td><td>1485</td><td>N927DA</td><td>LGA</td><td>MCO</td><td>149</td><td> 950</td><td>19</td><td>25</td><td>2013-04-19 19:00:00</td></tr>
	<tr><td>2013</td><td> 2</td><td>16</td><td> 757</td><td>1930</td><td> 747</td><td>1013</td><td>2149</td><td> 744</td><td>9E</td><td>3798</td><td>N8940E</td><td>JFK</td><td>CLT</td><td> 85</td><td> 541</td><td>19</td><td>30</td><td>2013-02-16 19:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td>14</td><td>2042</td><td> 900</td><td> 702</td><td>2255</td><td>1127</td><td> 688</td><td>DL</td><td> 502</td><td>N943DL</td><td>EWR</td><td>ATL</td><td> 98</td><td> 746</td><td> 9</td><td> 0</td><td>2013-10-14 09:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>24</td><td>NA</td><td>1625</td><td>NA</td><td>NA</td><td>1750</td><td>NA</td><td>MQ</td><td>3622</td><td>N524MQ</td><td>LGA</td><td>BNA</td><td>NA</td><td> 764</td><td>16</td><td>25</td><td>2013-09-24 16:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td>1259</td><td>NA</td><td>NA</td><td>1507</td><td>NA</td><td>EV</td><td>5207</td><td>N615QX</td><td>LGA</td><td>CLT</td><td>NA</td><td> 544</td><td>12</td><td>59</td><td>2013-09-25 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td> 845</td><td>NA</td><td>NA</td><td>1018</td><td>NA</td><td>EV</td><td>5286</td><td>N615QX</td><td>LGA</td><td>BTV</td><td>NA</td><td> 258</td><td> 8</td><td>45</td><td>2013-09-25 08:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td>1755</td><td>NA</td><td>NA</td><td>1932</td><td>NA</td><td>EV</td><td>5287</td><td>N722EV</td><td>LGA</td><td>MSN</td><td>NA</td><td> 812</td><td>17</td><td>55</td><td>2013-09-25 17:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td> 600</td><td>NA</td><td>NA</td><td> 716</td><td>NA</td><td>EV</td><td>5716</td><td>N877AS</td><td>JFK</td><td>IAD</td><td>NA</td><td> 228</td><td> 6</td><td> 0</td><td>2013-09-25 06:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td> 836</td><td>NA</td><td>NA</td><td> 944</td><td>NA</td><td>B6</td><td>2280</td><td>N258JB</td><td>EWR</td><td>BOS</td><td>NA</td><td> 200</td><td> 8</td><td>36</td><td>2013-09-25 08:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td>1300</td><td>NA</td><td>NA</td><td>1409</td><td>NA</td><td>US</td><td>2148</td><td>NA    </td><td>LGA</td><td>BOS</td><td>NA</td><td> 184</td><td>13</td><td> 0</td><td>2013-09-25 13:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td>1900</td><td>NA</td><td>NA</td><td>2014</td><td>NA</td><td>US</td><td>2160</td><td>NA    </td><td>LGA</td><td>BOS</td><td>NA</td><td> 184</td><td>19</td><td> 0</td><td>2013-09-25 19:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td>1300</td><td>NA</td><td>NA</td><td>1450</td><td>NA</td><td>MQ</td><td>3388</td><td>N817MQ</td><td>LGA</td><td>CMH</td><td>NA</td><td> 479</td><td>13</td><td> 0</td><td>2013-09-25 13:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td>1655</td><td>NA</td><td>NA</td><td>1840</td><td>NA</td><td>MQ</td><td>3411</td><td>N735MQ</td><td>LGA</td><td>RDU</td><td>NA</td><td> 431</td><td>16</td><td>55</td><td>2013-09-25 16:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>25</td><td>NA</td><td>1559</td><td>NA</td><td>NA</td><td>1719</td><td>NA</td><td>MQ</td><td>3748</td><td>N530MQ</td><td>EWR</td><td>ORD</td><td>NA</td><td> 719</td><td>15</td><td>59</td><td>2013-09-25 15:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>26</td><td>NA</td><td> 915</td><td>NA</td><td>NA</td><td>1141</td><td>NA</td><td>EV</td><td>5109</td><td>N748EV</td><td>LGA</td><td>CHS</td><td>NA</td><td> 641</td><td> 9</td><td>15</td><td>2013-09-26 09:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>26</td><td>NA</td><td>1400</td><td>NA</td><td>NA</td><td>1512</td><td>NA</td><td>US</td><td>2183</td><td>NA    </td><td>LGA</td><td>DCA</td><td>NA</td><td> 214</td><td>14</td><td> 0</td><td>2013-09-26 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>26</td><td>NA</td><td>1240</td><td>NA</td><td>NA</td><td>1525</td><td>NA</td><td>WN</td><td>4720</td><td>N691WN</td><td>EWR</td><td>HOU</td><td>NA</td><td>1411</td><td>12</td><td>40</td><td>2013-09-26 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td>NA</td><td> 600</td><td>NA</td><td>NA</td><td> 730</td><td>NA</td><td>AA</td><td> 301</td><td>N584AA</td><td>LGA</td><td>ORD</td><td>NA</td><td> 733</td><td> 6</td><td> 0</td><td>2013-09-27 06:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td>NA</td><td>2100</td><td>NA</td><td>NA</td><td>2211</td><td>NA</td><td>US</td><td>2164</td><td>NA    </td><td>LGA</td><td>BOS</td><td>NA</td><td> 184</td><td>21</td><td> 0</td><td>2013-09-27 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td>NA</td><td>1329</td><td>NA</td><td>NA</td><td>1444</td><td>NA</td><td>MQ</td><td>3760</td><td>N505MQ</td><td>EWR</td><td>ORD</td><td>NA</td><td> 719</td><td>13</td><td>29</td><td>2013-09-27 13:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td>NA</td><td>1600</td><td>NA</td><td>NA</td><td>1739</td><td>NA</td><td>UA</td><td> 269</td><td>NA    </td><td>LGA</td><td>ORD</td><td>NA</td><td> 733</td><td>16</td><td> 0</td><td>2013-09-27 16:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>28</td><td>NA</td><td>1803</td><td>NA</td><td>NA</td><td>1927</td><td>NA</td><td>EV</td><td>5563</td><td>N724EV</td><td>LGA</td><td>BTV</td><td>NA</td><td> 258</td><td>18</td><td> 3</td><td>2013-09-28 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>28</td><td>NA</td><td> 910</td><td>NA</td><td>NA</td><td>1220</td><td>NA</td><td>AA</td><td>   1</td><td>N320AA</td><td>JFK</td><td>LAX</td><td>NA</td><td>2475</td><td> 9</td><td>10</td><td>2013-09-28 09:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>28</td><td>NA</td><td>1635</td><td>NA</td><td>NA</td><td>1827</td><td>NA</td><td>US</td><td> 581</td><td>NA    </td><td>EWR</td><td>CLT</td><td>NA</td><td> 529</td><td>16</td><td>35</td><td>2013-09-28 16:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>29</td><td>NA</td><td>2054</td><td>NA</td><td>NA</td><td>2302</td><td>NA</td><td>EV</td><td>4536</td><td>N13988</td><td>EWR</td><td>CVG</td><td>NA</td><td> 569</td><td>20</td><td>54</td><td>2013-09-29 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>29</td><td>NA</td><td>1830</td><td>NA</td><td>NA</td><td>2010</td><td>NA</td><td>MQ</td><td>3134</td><td>N508MQ</td><td>EWR</td><td>ORD</td><td>NA</td><td> 719</td><td>18</td><td>30</td><td>2013-09-29 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>29</td><td>NA</td><td> 700</td><td>NA</td><td>NA</td><td> 833</td><td>NA</td><td>UA</td><td> 331</td><td>NA    </td><td>LGA</td><td>ORD</td><td>NA</td><td> 733</td><td> 7</td><td> 0</td><td>2013-09-29 07:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>NA</td><td>1842</td><td>NA</td><td>NA</td><td>2019</td><td>NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td>NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>NA</td><td>1455</td><td>NA</td><td>NA</td><td>1634</td><td>NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td>NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>NA</td><td>2200</td><td>NA</td><td>NA</td><td>2312</td><td>NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td>NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>NA</td><td>1210</td><td>NA</td><td>NA</td><td>1330</td><td>NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td>NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>NA</td><td>1159</td><td>NA</td><td>NA</td><td>1344</td><td>NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td>NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>NA</td><td> 840</td><td>NA</td><td>NA</td><td>1020</td><td>NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td>NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>



### `distinct()`


```R
# Remove duplicate rows, if any
flights |> 
  distinct()
```


<table class="dataframe">
<caption>A tibble: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>




```R
# # Find all unique origin and destination pairs
flights |> 
  distinct(origin, dest)
```


<table class="dataframe">
<caption>A tibble: 224 x 2</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>dest</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>EWR</td><td>IAH</td></tr>
	<tr><td>LGA</td><td>IAH</td></tr>
	<tr><td>JFK</td><td>MIA</td></tr>
	<tr><td>JFK</td><td>BQN</td></tr>
	<tr><td>LGA</td><td>ATL</td></tr>
	<tr><td>EWR</td><td>ORD</td></tr>
	<tr><td>EWR</td><td>FLL</td></tr>
	<tr><td>LGA</td><td>IAD</td></tr>
	<tr><td>JFK</td><td>MCO</td></tr>
	<tr><td>LGA</td><td>ORD</td></tr>
	<tr><td>JFK</td><td>PBI</td></tr>
	<tr><td>JFK</td><td>TPA</td></tr>
	<tr><td>JFK</td><td>LAX</td></tr>
	<tr><td>EWR</td><td>SFO</td></tr>
	<tr><td>LGA</td><td>DFW</td></tr>
	<tr><td>JFK</td><td>BOS</td></tr>
	<tr><td>EWR</td><td>LAS</td></tr>
	<tr><td>LGA</td><td>FLL</td></tr>
	<tr><td>EWR</td><td>PBI</td></tr>
	<tr><td>LGA</td><td>MSP</td></tr>
	<tr><td>LGA</td><td>DTW</td></tr>
	<tr><td>EWR</td><td>MIA</td></tr>
	<tr><td>JFK</td><td>ATL</td></tr>
	<tr><td>JFK</td><td>SFO</td></tr>
	<tr><td>JFK</td><td>RSW</td></tr>
	<tr><td>JFK</td><td>SJU</td></tr>
	<tr><td>EWR</td><td>ATL</td></tr>
	<tr><td>EWR</td><td>PHX</td></tr>
	<tr><td>LGA</td><td>MIA</td></tr>
	<tr><td>EWR</td><td>MSP</td></tr>
	<tr><td>...</td><td>...</td></tr>
	<tr><td>JFK</td><td>ACK</td></tr>
	<tr><td>LGA</td><td>BGR</td></tr>
	<tr><td>LGA</td><td>MSN</td></tr>
	<tr><td>LGA</td><td>ORF</td></tr>
	<tr><td>JFK</td><td>IAH</td></tr>
	<tr><td>JFK</td><td>MCI</td></tr>
	<tr><td>LGA</td><td>OMA</td></tr>
	<tr><td>LGA</td><td>DSM</td></tr>
	<tr><td>LGA</td><td>GSP</td></tr>
	<tr><td>JFK</td><td>ABQ</td></tr>
	<tr><td>LGA</td><td>ILM</td></tr>
	<tr><td>LGA</td><td>SYR</td></tr>
	<tr><td>JFK</td><td>MVY</td></tr>
	<tr><td>LGA</td><td>SBN</td></tr>
	<tr><td>JFK</td><td>STL</td></tr>
	<tr><td>LGA</td><td>LEX</td></tr>
	<tr><td>EWR</td><td>SBN</td></tr>
	<tr><td>LGA</td><td>MHT</td></tr>
	<tr><td>LGA</td><td>CAE</td></tr>
	<tr><td>JFK</td><td>JAC</td></tr>
	<tr><td>JFK</td><td>SDF</td></tr>
	<tr><td>LGA</td><td>CHO</td></tr>
	<tr><td>JFK</td><td>MKE</td></tr>
	<tr><td>LGA</td><td>AVL</td></tr>
	<tr><td>JFK</td><td>BHM</td></tr>
	<tr><td>LGA</td><td>TVC</td></tr>
	<tr><td>LGA</td><td>MYR</td></tr>
	<tr><td>EWR</td><td>TVC</td></tr>
	<tr><td>EWR</td><td>ANC</td></tr>
	<tr><td>EWR</td><td>LGA</td></tr>
</tbody>
</table>




```R
# keep other columns when filtering for unique rows
flights |> 
  distinct(origin, dest, .keep_all = TRUE)
```


<table class="dataframe">
<caption>A tibble: 224 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>622</td><td>630</td><td>-8</td><td>1017</td><td>1014</td><td>  3</td><td>US</td><td> 245</td><td>N807AW</td><td>EWR</td><td>PHX</td><td>342</td><td>2133</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>623</td><td>610</td><td>13</td><td> 920</td><td> 915</td><td>  5</td><td>AA</td><td>1837</td><td>N3EMAA</td><td>LGA</td><td>MIA</td><td>153</td><td>1096</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>624</td><td>630</td><td>-6</td><td> 909</td><td> 840</td><td> 29</td><td>EV</td><td>4626</td><td>N11107</td><td>EWR</td><td>MSP</td><td>190</td><td>1008</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1149</td><td>1159</td><td>-10</td><td>1245</td><td>1259</td><td>-14</td><td>B6</td><td>1191</td><td>N346JB</td><td>JFK</td><td>ACK</td><td> 39</td><td> 199</td><td>11</td><td>59</td><td>2013-10-01 11:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1338</td><td>1105</td><td>153</td><td>1446</td><td>1245</td><td>121</td><td>EV</td><td>5309</td><td>N713EV</td><td>LGA</td><td>BGR</td><td> 57</td><td> 378</td><td>11</td><td> 5</td><td>2013-10-01 11:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1345</td><td>1350</td><td> -5</td><td>1457</td><td>1526</td><td>-29</td><td>EV</td><td>5181</td><td>N612QX</td><td>LGA</td><td>MSN</td><td>115</td><td> 812</td><td>13</td><td>50</td><td>2013-10-01 13:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1543</td><td>1545</td><td> -2</td><td>1702</td><td>1721</td><td>-19</td><td>EV</td><td>5293</td><td>N398CA</td><td>LGA</td><td>ORF</td><td> 46</td><td> 296</td><td>15</td><td>45</td><td>2013-10-01 15:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1658</td><td>1700</td><td> -2</td><td>2002</td><td>1955</td><td>  7</td><td>AA</td><td> 211</td><td>N3FVAA</td><td>JFK</td><td>IAH</td><td>214</td><td>1417</td><td>17</td><td> 0</td><td>2013-10-01 17:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1728</td><td>1736</td><td> -8</td><td>1910</td><td>2006</td><td>-56</td><td>9E</td><td>3310</td><td>N907XJ</td><td>JFK</td><td>MCI</td><td>143</td><td>1113</td><td>17</td><td>36</td><td>2013-10-01 17:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1732</td><td>1730</td><td>  2</td><td>1925</td><td>1953</td><td>-28</td><td>EV</td><td>5298</td><td>N709EV</td><td>LGA</td><td>OMA</td><td>153</td><td>1148</td><td>17</td><td>30</td><td>2013-10-01 17:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1857</td><td>1900</td><td> -3</td><td>2044</td><td>2117</td><td>-33</td><td>9E</td><td>3445</td><td>N906XJ</td><td>LGA</td><td>DSM</td><td>146</td><td>1031</td><td>19</td><td> 0</td><td>2013-10-01 19:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1930</td><td>1900</td><td> 30</td><td>2129</td><td>2119</td><td> 10</td><td>9E</td><td>3854</td><td>N8884E</td><td>LGA</td><td>GSP</td><td> 86</td><td> 610</td><td>19</td><td> 0</td><td>2013-10-01 19:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>1955</td><td>2001</td><td> -6</td><td>2213</td><td>2248</td><td>-35</td><td>B6</td><td>  65</td><td>N554JB</td><td>JFK</td><td>ABQ</td><td>230</td><td>1826</td><td>20</td><td> 1</td><td>2013-10-01 20:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>2051</td><td>2110</td><td>-19</td><td>2219</td><td>2306</td><td>-47</td><td>EV</td><td>4885</td><td>N752EV</td><td>LGA</td><td>ILM</td><td> 66</td><td> 500</td><td>21</td><td>10</td><td>2013-10-01 21:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 1</td><td>2150</td><td>2159</td><td> -9</td><td>2246</td><td>2308</td><td>-22</td><td>9E</td><td>3525</td><td>N922XJ</td><td>LGA</td><td>SYR</td><td> 34</td><td> 198</td><td>21</td><td>59</td><td>2013-10-01 21:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td> 3</td><td>1414</td><td>1350</td><td> 24</td><td>1514</td><td>1453</td><td> 21</td><td>B6</td><td>1338</td><td>N368JB</td><td>JFK</td><td>MVY</td><td> 36</td><td> 173</td><td>13</td><td>50</td><td>2013-10-03 13:00:00</td></tr>
	<tr><td>2013</td><td>10</td><td>18</td><td>1820</td><td>1745</td><td> 35</td><td>2030</td><td>2011</td><td> 19</td><td>EV</td><td>5624</td><td>N748EV</td><td>LGA</td><td>SBN</td><td>104</td><td> 651</td><td>17</td><td>45</td><td>2013-10-18 17:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td> 2</td><td>1519</td><td>1459</td><td> 20</td><td>1654</td><td>1702</td><td> -8</td><td>DL</td><td> 567</td><td>N329NB</td><td>JFK</td><td>STL</td><td>129</td><td> 892</td><td>14</td><td>59</td><td>2013-11-02 14:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>24</td><td>2026</td><td>2035</td><td> -9</td><td>2227</td><td>2249</td><td>-22</td><td>9E</td><td>3669</td><td>N8604C</td><td>LGA</td><td>LEX</td><td> 90</td><td> 604</td><td>20</td><td>35</td><td>2013-11-24 20:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td> 1</td><td>1241</td><td>1215</td><td> 26</td><td>1431</td><td>1431</td><td>  0</td><td>EV</td><td>3264</td><td>N16976</td><td>EWR</td><td>SBN</td><td> 94</td><td> 637</td><td>12</td><td>15</td><td>2013-12-01 12:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>19</td><td>1056</td><td>1103</td><td> -7</td><td>1210</td><td>1219</td><td> -9</td><td>EV</td><td>5252</td><td>N848AS</td><td>LGA</td><td>MHT</td><td> 39</td><td> 195</td><td>11</td><td> 3</td><td>2013-12-19 11:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>19</td><td>1914</td><td>1915</td><td> -1</td><td>2130</td><td>2144</td><td>-14</td><td>EV</td><td>5567</td><td>N848AS</td><td>LGA</td><td>CAE</td><td> 97</td><td> 617</td><td>19</td><td>15</td><td>2013-12-19 19:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>21</td><td> 802</td><td> 800</td><td>  2</td><td>1115</td><td>1102</td><td> 13</td><td>DL</td><td>2379</td><td>N6705Y</td><td>JFK</td><td>JAC</td><td>281</td><td>1894</td><td> 8</td><td> 0</td><td>2013-12-21 08:00:00</td></tr>
	<tr><td>2013</td><td>12</td><td>21</td><td>1610</td><td>1610</td><td>  0</td><td>1839</td><td>1855</td><td>-16</td><td>9E</td><td>2941</td><td>N8930E</td><td>JFK</td><td>SDF</td><td>114</td><td> 662</td><td>16</td><td>10</td><td>2013-12-21 16:00:00</td></tr>
	<tr><td>2013</td><td> 3</td><td> 1</td><td>2046</td><td>2045</td><td>  1</td><td>2206</td><td>2220</td><td>-14</td><td>EV</td><td>5343</td><td>N197PQ</td><td>LGA</td><td>CHO</td><td> 48</td><td> 305</td><td>20</td><td>45</td><td>2013-03-01 20:00:00</td></tr>
	<tr><td>2013</td><td> 3</td><td> 2</td><td>1606</td><td>1610</td><td> -4</td><td>1723</td><td>1758</td><td>-35</td><td>9E</td><td>3437</td><td>N927XJ</td><td>JFK</td><td>MKE</td><td>109</td><td> 745</td><td>16</td><td>10</td><td>2013-03-02 16:00:00</td></tr>
	<tr><td>2013</td><td> 4</td><td>14</td><td> 937</td><td> 945</td><td> -8</td><td>1130</td><td>1159</td><td>-29</td><td>9E</td><td>3632</td><td>N8936A</td><td>LGA</td><td>AVL</td><td> 93</td><td> 599</td><td> 9</td><td>45</td><td>2013-04-14 09:00:00</td></tr>
	<tr><td>2013</td><td> 5</td><td>25</td><td>1007</td><td>1000</td><td>  7</td><td>1129</td><td>1148</td><td>-19</td><td>EV</td><td>5621</td><td>N751EV</td><td>JFK</td><td>BHM</td><td>117</td><td> 865</td><td>10</td><td> 0</td><td>2013-05-25 10:00:00</td></tr>
	<tr><td>2013</td><td> 6</td><td>14</td><td>1756</td><td>1800</td><td> -4</td><td>2004</td><td>2005</td><td> -1</td><td>MQ</td><td>3402</td><td>N722MQ</td><td>LGA</td><td>TVC</td><td>101</td><td> 655</td><td>18</td><td> 0</td><td>2013-06-14 18:00:00</td></tr>
	<tr><td>2013</td><td> 6</td><td>15</td><td>1517</td><td>1520</td><td> -3</td><td>1656</td><td>1730</td><td>-34</td><td>EV</td><td>5163</td><td>N605QX</td><td>LGA</td><td>MYR</td><td> 74</td><td> 563</td><td>15</td><td>20</td><td>2013-06-15 15:00:00</td></tr>
	<tr><td>2013</td><td> 7</td><td> 5</td><td>1355</td><td>1400</td><td> -5</td><td>1550</td><td>1620</td><td>-30</td><td>EV</td><td>4137</td><td>N11164</td><td>EWR</td><td>TVC</td><td> 93</td><td> 644</td><td>14</td><td> 0</td><td>2013-07-05 14:00:00</td></tr>
	<tr><td>2013</td><td> 7</td><td> 6</td><td>1629</td><td>1615</td><td> 14</td><td>1954</td><td>1953</td><td>  1</td><td>UA</td><td> 887</td><td>N587UA</td><td>EWR</td><td>ANC</td><td>418</td><td>3370</td><td>16</td><td>15</td><td>2013-07-06 16:00:00</td></tr>
	<tr><td>2013</td><td> 7</td><td>27</td><td>  NA</td><td> 106</td><td> NA</td><td>  NA</td><td> 245</td><td> NA</td><td>US</td><td>1632</td><td>NA    </td><td>EWR</td><td>LGA</td><td> NA</td><td>  17</td><td> 1</td><td> 6</td><td>2013-07-27 01:00:00</td></tr>
</tbody>
</table>



If you want to find the number of occurrences instead, you’re better off swapping `distinct()` for `count()`, and with the `sort = TRUE` argument you can arrange them in descending order of number of occurrences. 


```R
flights |>
  count(origin, dest, sort = TRUE)
```


<table class="dataframe">
<caption>A tibble: 224 x 3</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>dest</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>JFK</td><td>LAX</td><td>11262</td></tr>
	<tr><td>LGA</td><td>ATL</td><td>10263</td></tr>
	<tr><td>LGA</td><td>ORD</td><td> 8857</td></tr>
	<tr><td>JFK</td><td>SFO</td><td> 8204</td></tr>
	<tr><td>LGA</td><td>CLT</td><td> 6168</td></tr>
	<tr><td>EWR</td><td>ORD</td><td> 6100</td></tr>
	<tr><td>JFK</td><td>BOS</td><td> 5898</td></tr>
	<tr><td>LGA</td><td>MIA</td><td> 5781</td></tr>
	<tr><td>JFK</td><td>MCO</td><td> 5464</td></tr>
	<tr><td>EWR</td><td>BOS</td><td> 5327</td></tr>
	<tr><td>EWR</td><td>SFO</td><td> 5127</td></tr>
	<tr><td>LGA</td><td>DTW</td><td> 5040</td></tr>
	<tr><td>EWR</td><td>CLT</td><td> 5026</td></tr>
	<tr><td>EWR</td><td>ATL</td><td> 5022</td></tr>
	<tr><td>EWR</td><td>MCO</td><td> 4941</td></tr>
	<tr><td>EWR</td><td>LAX</td><td> 4912</td></tr>
	<tr><td>LGA</td><td>DFW</td><td> 4858</td></tr>
	<tr><td>JFK</td><td>SJU</td><td> 4752</td></tr>
	<tr><td>LGA</td><td>DCA</td><td> 4716</td></tr>
	<tr><td>LGA</td><td>BOS</td><td> 4283</td></tr>
	<tr><td>JFK</td><td>FLL</td><td> 4254</td></tr>
	<tr><td>LGA</td><td>FLL</td><td> 4008</td></tr>
	<tr><td>JFK</td><td>LAS</td><td> 3987</td></tr>
	<tr><td>EWR</td><td>IAH</td><td> 3973</td></tr>
	<tr><td>EWR</td><td>FLL</td><td> 3793</td></tr>
	<tr><td>LGA</td><td>MSP</td><td> 3713</td></tr>
	<tr><td>LGA</td><td>DEN</td><td> 3704</td></tr>
	<tr><td>LGA</td><td>MCO</td><td> 3677</td></tr>
	<tr><td>JFK</td><td>BUF</td><td> 3582</td></tr>
	<tr><td>LGA</td><td>RDU</td><td> 3581</td></tr>
	<tr><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>JFK</td><td>EGE</td><td>103</td></tr>
	<tr><td>LGA</td><td>OMA</td><td> 95</td></tr>
	<tr><td>LGA</td><td>IND</td><td> 87</td></tr>
	<tr><td>LGA</td><td>TVC</td><td> 77</td></tr>
	<tr><td>LGA</td><td>SAV</td><td> 68</td></tr>
	<tr><td>EWR</td><td>MYR</td><td> 56</td></tr>
	<tr><td>LGA</td><td>CHO</td><td> 52</td></tr>
	<tr><td>EWR</td><td>PHL</td><td> 49</td></tr>
	<tr><td>JFK</td><td>SDF</td><td> 46</td></tr>
	<tr><td>LGA</td><td>GRR</td><td> 46</td></tr>
	<tr><td>EWR</td><td>BZN</td><td> 36</td></tr>
	<tr><td>EWR</td><td>TVC</td><td> 24</td></tr>
	<tr><td>EWR</td><td>JAC</td><td> 23</td></tr>
	<tr><td>JFK</td><td>PSP</td><td> 19</td></tr>
	<tr><td>LGA</td><td>EYW</td><td> 17</td></tr>
	<tr><td>EWR</td><td>HDN</td><td> 15</td></tr>
	<tr><td>EWR</td><td>MTJ</td><td> 15</td></tr>
	<tr><td>LGA</td><td>BWI</td><td> 15</td></tr>
	<tr><td>LGA</td><td>CAE</td><td> 12</td></tr>
	<tr><td>LGA</td><td>AVL</td><td> 10</td></tr>
	<tr><td>EWR</td><td>ANC</td><td>  8</td></tr>
	<tr><td>LGA</td><td>SBN</td><td>  6</td></tr>
	<tr><td>EWR</td><td>SBN</td><td>  4</td></tr>
	<tr><td>LGA</td><td>MYR</td><td>  3</td></tr>
	<tr><td>JFK</td><td>JAC</td><td>  2</td></tr>
	<tr><td>EWR</td><td>LGA</td><td>  1</td></tr>
	<tr><td>JFK</td><td>BHM</td><td>  1</td></tr>
	<tr><td>JFK</td><td>MEM</td><td>  1</td></tr>
	<tr><td>JFK</td><td>STL</td><td>  1</td></tr>
	<tr><td>LGA</td><td>LEX</td><td>  1</td></tr>
</tbody>
</table>



### Exercises

3.2.1. Single pipeline:
* Had an arrival delay of two or more hours
* Flew to Houston (IAH or HOU)
* Were operated by United, American, or Delta
* Departed in summer (July, August, and September)
* Arrived more than two hours late, but didn’t leave late
* Were delayed by at least an hour, but made up over 30 minutes in flight

3.2.2. Sort flights to find the flights with longest departure delays. Find the flights that left earliest in the morning.

3.2.3. Sort flights to find the fastest flights. (Hint: Try including a math calculation inside of your function.)

3.2.4. Was there a flight on every day of 2013?

3.2.5. Which flights traveled the farthest distance? Which traveled the least distance?

3.2.6. Does it matter what order you used filter() and arrange() if you’re using both? Why/why not? Think about the results and how much work the functions would have to do.


```R
#3.2.1. Had an arrival delay of two or more hours

```


```R
#3.2.1. Flew to Houston (IAH or HOU)

```


```R
#3.2.1. Were operated by United, American, or Delta
#
```


```R
#3.2.1. Departed in summer (July, August, and September)

```


```R
#3.2.1. Arrived more than two hours late, but didn’t leave late

```


```R
#3.2.1. Were delayed by at least an hour, but made up over 30 minutes in flight


```


```R
#3.2.2. Sort flights to find the flights with longest departure delays. Find the flights that left earliest in the morning.


```


```R
#3.2.3. Sort flights to find the fastest flights. (Hint: Try including a math calculation inside of your function.)


```


```R
#3.2.4. Was there a flight on every day of 2013?

#
```


```R
#3.2.5. Which flights traveled the farthest distance? Which traveled the least distance?


```


```R
#3.2.6. Does it matter what order you used filter() and arrange() if you’re using both? Why/why not? 
# Think about the results and how much work the functions would have to do.
```

## Columns

There are four important verbs that affect the columns without changing the rows:
* `mutate()` creates new columns that are derived from the existing columns
* `select()` changes which columns are present
* `rename()` changes the names of the columns
* `relocate()` changes the positions of the columns.

### `mutate()`
By default, `mutate()` adds new columns on the right hand side of your dataset, which makes it difficult to see what’s happening here. We can use the `.before` argument to instead add the variables to the left hand side.


```R
flights |> 
  mutate(
    gain = dep_delay - arr_delay,       # gain, how much time a delayed flight made up in the air
    speed = distance / air_time * 60,   # the speed in miles per hour
    .after = day                         # try: .before = 1
  )
```


<table class="dataframe">
<caption>A tibble: 336776 x 21</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>gain</th><th scope=col>speed</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>...</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>...</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td> -9</td><td>370.0441</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td>...</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-16</td><td>374.2731</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td>...</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-31</td><td>408.3750</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td>...</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> 17</td><td>516.7213</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>...</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> 19</td><td>394.1379</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>...</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-16</td><td>287.6000</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td>...</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-24</td><td>404.4304</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td>...</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> 11</td><td>259.2453</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>...</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  5</td><td>404.5714</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td>...</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-10</td><td>318.6957</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>...</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  0</td><td>413.9597</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td>...</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  1</td><td>381.6456</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td>...</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> -9</td><td>430.4348</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>...</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> 12</td><td>426.3158</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>...</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-32</td><td>324.2802</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td>...</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  4</td><td>255.0000</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td>...</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  7</td><td>396.4985</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td>...</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  7</td><td>424.7368</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td>...</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-12</td><td>341.1940</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td>...</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  7</td><td>417.5510</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td>...</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  0</td><td>360.0000</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td>...</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-19</td><td>286.8571</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td>...</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  8</td><td>428.2895</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>...</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  4</td><td>356.2500</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td>...</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> 17</td><td>414.6497</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>...</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>-24</td><td>310.3597</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td>...</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> -3</td><td>423.9344</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td>...</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> -1</td><td>368.2286</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>...</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> 21</td><td>526.8132</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>...</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>  9</td><td>373.0000</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td>...</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td></td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 22</td><td>406.6667</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>...</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  7</td><td>440.8333</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td>...</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 29</td><td>458.0282</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>...</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 32</td><td>389.3333</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td>...</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 21</td><td>355.0000</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>...</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 30</td><td>498.3221</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>...</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  2</td><td>362.5532</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td>...</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 25</td><td>499.3750</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>...</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  7</td><td>464.4604</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>...</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 16</td><td>324.3243</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>...</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  7</td><td>321.5385</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>...</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  0</td><td>361.2000</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>...</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>-10</td><td>371.8033</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>...</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 20</td><td>472.5773</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>...</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 15</td><td>436.0000</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td>...</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  7</td><td>341.2500</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>...</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 38</td><td>483.9623</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td>...</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 24</td><td>460.4878</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>...</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  0</td><td>371.1628</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td>...</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 12</td><td>305.8537</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>...</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 10</td><td>347.3077</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>...</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 11</td><td>337.0213</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>...</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 11</td><td>340.0000</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>...</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 15</td><td>495.0000</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>...</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> NA</td><td>      NA</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td>...</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> NA</td><td>      NA</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td>...</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> NA</td><td>      NA</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td>...</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> NA</td><td>      NA</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td>...</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> NA</td><td>      NA</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td>...</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> NA</td><td>      NA</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td>...</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>




```R
flights |> 
  mutate(
    gain = dep_delay - arr_delay,
    hours = air_time / 60,
    gain_per_hour = gain / hours,
    .keep = "used"
  )
```


<table class="dataframe">
<caption>A tibble: 336776 x 6</caption>
<thead>
	<tr><th scope=col>dep_delay</th><th scope=col>arr_delay</th><th scope=col>air_time</th><th scope=col>gain</th><th scope=col>hours</th><th scope=col>gain_per_hour</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td> 2</td><td> 11</td><td>227</td><td> -9</td><td>3.7833333</td><td> -2.3788546</td></tr>
	<tr><td> 4</td><td> 20</td><td>227</td><td>-16</td><td>3.7833333</td><td> -4.2290749</td></tr>
	<tr><td> 2</td><td> 33</td><td>160</td><td>-31</td><td>2.6666667</td><td>-11.6250000</td></tr>
	<tr><td>-1</td><td>-18</td><td>183</td><td> 17</td><td>3.0500000</td><td>  5.5737705</td></tr>
	<tr><td>-6</td><td>-25</td><td>116</td><td> 19</td><td>1.9333333</td><td>  9.8275862</td></tr>
	<tr><td>-4</td><td> 12</td><td>150</td><td>-16</td><td>2.5000000</td><td> -6.4000000</td></tr>
	<tr><td>-5</td><td> 19</td><td>158</td><td>-24</td><td>2.6333333</td><td> -9.1139241</td></tr>
	<tr><td>-3</td><td>-14</td><td> 53</td><td> 11</td><td>0.8833333</td><td> 12.4528302</td></tr>
	<tr><td>-3</td><td> -8</td><td>140</td><td>  5</td><td>2.3333333</td><td>  2.1428571</td></tr>
	<tr><td>-2</td><td>  8</td><td>138</td><td>-10</td><td>2.3000000</td><td> -4.3478261</td></tr>
	<tr><td>-2</td><td> -2</td><td>149</td><td>  0</td><td>2.4833333</td><td>  0.0000000</td></tr>
	<tr><td>-2</td><td> -3</td><td>158</td><td>  1</td><td>2.6333333</td><td>  0.3797468</td></tr>
	<tr><td>-2</td><td>  7</td><td>345</td><td> -9</td><td>5.7500000</td><td> -1.5652174</td></tr>
	<tr><td>-2</td><td>-14</td><td>361</td><td> 12</td><td>6.0166667</td><td>  1.9944598</td></tr>
	<tr><td>-1</td><td> 31</td><td>257</td><td>-32</td><td>4.2833333</td><td> -7.4708171</td></tr>
	<tr><td> 0</td><td> -4</td><td> 44</td><td>  4</td><td>0.7333333</td><td>  5.4545455</td></tr>
	<tr><td>-1</td><td> -8</td><td>337</td><td>  7</td><td>5.6166667</td><td>  1.2462908</td></tr>
	<tr><td> 0</td><td> -7</td><td>152</td><td>  7</td><td>2.5333333</td><td>  2.7631579</td></tr>
	<tr><td> 0</td><td> 12</td><td>134</td><td>-12</td><td>2.2333333</td><td> -5.3731343</td></tr>
	<tr><td> 1</td><td> -6</td><td>147</td><td>  7</td><td>2.4500000</td><td>  2.8571429</td></tr>
	<tr><td>-8</td><td> -8</td><td>170</td><td>  0</td><td>2.8333333</td><td>  0.0000000</td></tr>
	<tr><td>-3</td><td> 16</td><td>105</td><td>-19</td><td>1.7500000</td><td>-10.8571429</td></tr>
	<tr><td>-4</td><td>-12</td><td>152</td><td>  8</td><td>2.5333333</td><td>  3.1578947</td></tr>
	<tr><td>-4</td><td> -8</td><td>128</td><td>  4</td><td>2.1333333</td><td>  1.8750000</td></tr>
	<tr><td> 0</td><td>-17</td><td>157</td><td> 17</td><td>2.6166667</td><td>  6.4968153</td></tr>
	<tr><td> 8</td><td> 32</td><td>139</td><td>-24</td><td>2.3166667</td><td>-10.3597122</td></tr>
	<tr><td>11</td><td> 14</td><td>366</td><td> -3</td><td>6.1000000</td><td> -0.4918033</td></tr>
	<tr><td> 3</td><td>  4</td><td>175</td><td> -1</td><td>2.9166667</td><td> -0.3428571</td></tr>
	<tr><td> 0</td><td>-21</td><td>182</td><td> 21</td><td>3.0333333</td><td>  6.9230769</td></tr>
	<tr><td> 0</td><td> -9</td><td>120</td><td>  9</td><td>2.0000000</td><td>  4.5000000</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td> -2</td><td>-24</td><td> 45</td><td> 22</td><td>0.7500000</td><td>29.333333</td></tr>
	<tr><td> -2</td><td> -9</td><td> 72</td><td>  7</td><td>1.2000000</td><td> 5.833333</td></tr>
	<tr><td> -2</td><td>-31</td><td>213</td><td> 29</td><td>3.5500000</td><td> 8.169014</td></tr>
	<tr><td> 30</td><td> -2</td><td> 45</td><td> 32</td><td>0.7500000</td><td>42.666667</td></tr>
	<tr><td> -9</td><td>-30</td><td> 36</td><td> 21</td><td>0.6000000</td><td>35.000000</td></tr>
	<tr><td>  0</td><td>-30</td><td>298</td><td> 30</td><td>4.9666667</td><td> 6.040268</td></tr>
	<tr><td> 13</td><td> 11</td><td> 47</td><td>  2</td><td>0.7833333</td><td> 2.553191</td></tr>
	<tr><td>  0</td><td>-25</td><td>192</td><td> 25</td><td>3.2000000</td><td> 7.812500</td></tr>
	<tr><td> 10</td><td>  3</td><td>139</td><td>  7</td><td>2.3166667</td><td> 3.021583</td></tr>
	<tr><td> -7</td><td>-23</td><td> 37</td><td> 16</td><td>0.6166667</td><td>25.945946</td></tr>
	<tr><td> -9</td><td>-16</td><td> 39</td><td>  7</td><td>0.6500000</td><td>10.769231</td></tr>
	<tr><td>194</td><td>194</td><td> 50</td><td>  0</td><td>0.8333333</td><td> 0.000000</td></tr>
	<tr><td> -2</td><td>  8</td><td> 61</td><td>-10</td><td>1.0166667</td><td>-9.836066</td></tr>
	<tr><td> 27</td><td>  7</td><td> 97</td><td> 20</td><td>1.6166667</td><td>12.371134</td></tr>
	<tr><td> 72</td><td> 57</td><td>120</td><td> 15</td><td>2.0000000</td><td> 7.500000</td></tr>
	<tr><td>-14</td><td>-21</td><td> 48</td><td>  7</td><td>0.8000000</td><td> 8.750000</td></tr>
	<tr><td> 80</td><td> 42</td><td>318</td><td> 38</td><td>5.3000000</td><td> 7.169811</td></tr>
	<tr><td>154</td><td>130</td><td>123</td><td> 24</td><td>2.0500000</td><td>11.707317</td></tr>
	<tr><td> -8</td><td> -8</td><td> 43</td><td>  0</td><td>0.7166667</td><td> 0.000000</td></tr>
	<tr><td> -5</td><td>-17</td><td> 41</td><td> 12</td><td>0.6833333</td><td>17.560976</td></tr>
	<tr><td>-10</td><td>-20</td><td> 52</td><td> 10</td><td>0.8666667</td><td>11.538462</td></tr>
	<tr><td> -5</td><td>-16</td><td> 47</td><td> 11</td><td>0.7833333</td><td>14.042553</td></tr>
	<tr><td> 12</td><td>  1</td><td> 33</td><td> 11</td><td>0.5500000</td><td>20.000000</td></tr>
	<tr><td>-10</td><td>-25</td><td>196</td><td> 15</td><td>3.2666667</td><td> 4.591837</td></tr>
	<tr><td> NA</td><td> NA</td><td> NA</td><td> NA</td><td>       NA</td><td>       NA</td></tr>
	<tr><td> NA</td><td> NA</td><td> NA</td><td> NA</td><td>       NA</td><td>       NA</td></tr>
	<tr><td> NA</td><td> NA</td><td> NA</td><td> NA</td><td>       NA</td><td>       NA</td></tr>
	<tr><td> NA</td><td> NA</td><td> NA</td><td> NA</td><td>       NA</td><td>       NA</td></tr>
	<tr><td> NA</td><td> NA</td><td> NA</td><td> NA</td><td>       NA</td><td>       NA</td></tr>
	<tr><td> NA</td><td> NA</td><td> NA</td><td> NA</td><td>       NA</td><td>       NA</td></tr>
</tbody>
</table>



### `select()`

There are a number of helper functions you can use within `select()`:

* `starts_with("abc")`: matches names that begin with “abc”.
* `ends_with("xyz")`: matches names that end with “xyz”.
* `contains("ijk")`: matches names that contain “ijk”.
* `num_range("x", 1:3)`: matches x1, x2 and x3.

See `?select` for more details



```R
flights |> 
  select(year, month, day)
```


<table class="dataframe">
<caption>A tibble: 336776 x 3</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
</tbody>
</table>




```R
flights |> 
  select(year:day)
```


<table class="dataframe">
<caption>A tibble: 336776 x 3</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td></tr>
	<tr><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td></tr>
</tbody>
</table>




```R
flights |> 
  select(!year:day)
```


<table class="dataframe">
<caption>A tibble: 336776 x 16</caption>
<thead>
	<tr><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>




```R
#Select all columns that are characters:

flights |> 
  select(!where(is.character))
```


<table class="dataframe">
<caption>A tibble: 336776 x 15</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>flight</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>1545</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>1714</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>1141</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td> 725</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td> 461</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>1696</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td> 507</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>5708</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>  79</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td> 301</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>  49</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>  71</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td> 194</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>1124</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td> 707</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>1806</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>1187</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td> 371</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>4650</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td> 343</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>1919</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>4401</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>1895</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>1743</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>1077</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>3768</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td> 303</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td> 135</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td> 709</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td> 575</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>5489</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>3833</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>  97</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>5048</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>3621</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td> 185</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>4509</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>1103</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>1371</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td> 523</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>3842</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>3320</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>5311</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>3660</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>4672</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td> 108</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td> 471</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>1083</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td> 234</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>1816</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>2002</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td> 486</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td> 718</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td> 745</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>5274</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>3393</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>3525</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>3461</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>3572</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>3531</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>




```R
# rename variable while select
flights |> 
  select(tail_num = tailnum)
```


<table class="dataframe">
<caption>A tibble: 336776 x 1</caption>
<thead>
	<tr><th scope=col>tail_num</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>N14228</td></tr>
	<tr><td>N24211</td></tr>
	<tr><td>N619AA</td></tr>
	<tr><td>N804JB</td></tr>
	<tr><td>N668DN</td></tr>
	<tr><td>N39463</td></tr>
	<tr><td>N516JB</td></tr>
	<tr><td>N829AS</td></tr>
	<tr><td>N593JB</td></tr>
	<tr><td>N3ALAA</td></tr>
	<tr><td>N793JB</td></tr>
	<tr><td>N657JB</td></tr>
	<tr><td>N29129</td></tr>
	<tr><td>N53441</td></tr>
	<tr><td>N3DUAA</td></tr>
	<tr><td>N708JB</td></tr>
	<tr><td>N76515</td></tr>
	<tr><td>N595JB</td></tr>
	<tr><td>N542MQ</td></tr>
	<tr><td>N644JB</td></tr>
	<tr><td>N971DL</td></tr>
	<tr><td>N730MQ</td></tr>
	<tr><td>N633AA</td></tr>
	<tr><td>N3739P</td></tr>
	<tr><td>N53442</td></tr>
	<tr><td>N9EAMQ</td></tr>
	<tr><td>N532UA</td></tr>
	<tr><td>N635JB</td></tr>
	<tr><td>N794JB</td></tr>
	<tr><td>N326NB</td></tr>
	<tr><td>...</td></tr>
	<tr><td>N712EV</td></tr>
	<tr><td>N16546</td></tr>
	<tr><td>N807JB</td></tr>
	<tr><td>N751EV</td></tr>
	<tr><td>N807MQ</td></tr>
	<tr><td>N335AA</td></tr>
	<tr><td>N12957</td></tr>
	<tr><td>N633JB</td></tr>
	<tr><td>N627JB</td></tr>
	<tr><td>N813UA</td></tr>
	<tr><td>N10575</td></tr>
	<tr><td>N906XJ</td></tr>
	<tr><td>N722EV</td></tr>
	<tr><td>N532MQ</td></tr>
	<tr><td>N12145</td></tr>
	<tr><td>N193JB</td></tr>
	<tr><td>N578UA</td></tr>
	<tr><td>N804JB</td></tr>
	<tr><td>N318JB</td></tr>
	<tr><td>N354JB</td></tr>
	<tr><td>N281JB</td></tr>
	<tr><td>N346JB</td></tr>
	<tr><td>N565JB</td></tr>
	<tr><td>N516JB</td></tr>
	<tr><td>N740EV</td></tr>
	<tr><td>NA    </td></tr>
	<tr><td>NA    </td></tr>
	<tr><td>N535MQ</td></tr>
	<tr><td>N511MQ</td></tr>
	<tr><td>N839MQ</td></tr>
</tbody>
</table>




### `rename()`

If you want to keep all the existing variables and just want to rename a few, you can use `rename()` instead of `select()`:

also try: janitor::clean_names()


```R
flights |> 
  rename(tail_num = tailnum)
```


<table class="dataframe">
<caption>A tibble: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tail_num</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>



### `relocate()`
By default `relocate()` moves variables to the front:


```R
flights |> 
  relocate(time_hour, air_time)

# flights |> 
#   relocate(year:dep_time, .after = time_hour)
# flights |> 
#   relocate(starts_with("arr"), .before = dep_time)
```


<table class="dataframe">
<caption>A tibble: 336776 x 19</caption>
<thead>
	<tr><th scope=col>time_hour</th><th scope=col>air_time</th><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th></tr>
	<tr><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013-01-01 05:00:00</td><td>227</td><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>1400</td><td>5</td><td>15</td></tr>
	<tr><td>2013-01-01 05:00:00</td><td>227</td><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>1416</td><td>5</td><td>29</td></tr>
	<tr><td>2013-01-01 05:00:00</td><td>160</td><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>1089</td><td>5</td><td>40</td></tr>
	<tr><td>2013-01-01 05:00:00</td><td>183</td><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>1576</td><td>5</td><td>45</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>116</td><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td> 762</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 05:00:00</td><td>150</td><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td> 719</td><td>5</td><td>58</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>158</td><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>1065</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td> 53</td><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 229</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>140</td><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td> 944</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>138</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td> 733</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>149</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>1028</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>158</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>1005</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>345</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>2475</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>361</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>2565</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>257</td><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>1389</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 05:00:00</td><td> 44</td><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 187</td><td>5</td><td>59</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>337</td><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>2227</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>152</td><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>1076</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>134</td><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td> 762</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>147</td><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>1023</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>170</td><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>1020</td><td>6</td><td>10</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>105</td><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td> 502</td><td>6</td><td> 5</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>152</td><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>1085</td><td>6</td><td>10</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>128</td><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td> 760</td><td>6</td><td>10</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>157</td><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>1085</td><td>6</td><td> 7</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>139</td><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td> 719</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>366</td><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>2586</td><td>6</td><td> 0</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>175</td><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>1074</td><td>6</td><td>10</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>182</td><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>1598</td><td>6</td><td>15</td></tr>
	<tr><td>2013-01-01 06:00:00</td><td>120</td><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td> 746</td><td>6</td><td>15</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td> 45</td><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 305</td><td>21</td><td>25</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td> 72</td><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 529</td><td>21</td><td>29</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td>213</td><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>1626</td><td>21</td><td>30</td></tr>
	<tr><td>2013-09-30 20:00:00</td><td> 45</td><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 292</td><td>20</td><td>59</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td> 36</td><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 213</td><td>21</td><td>40</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td>298</td><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>2475</td><td>21</td><td>40</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td> 47</td><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 284</td><td>21</td><td>29</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td>192</td><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>1598</td><td>21</td><td>45</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td>139</td><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>1076</td><td>21</td><td>37</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td> 37</td><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 200</td><td>21</td><td>56</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td> 39</td><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 209</td><td>21</td><td>59</td></tr>
	<tr><td>2013-09-30 18:00:00</td><td> 50</td><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 301</td><td>18</td><td>45</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> 61</td><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 378</td><td>22</td><td> 5</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td> 97</td><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 764</td><td>21</td><td>40</td></tr>
	<tr><td>2013-09-30 20:00:00</td><td>120</td><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td> 872</td><td>20</td><td>59</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> 48</td><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 273</td><td>22</td><td>45</td></tr>
	<tr><td>2013-09-30 21:00:00</td><td>318</td><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>2565</td><td>21</td><td>13</td></tr>
	<tr><td>2013-09-30 20:00:00</td><td>123</td><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td> 944</td><td>20</td><td> 1</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> 43</td><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 266</td><td>22</td><td>45</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> 41</td><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 209</td><td>22</td><td>45</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> 52</td><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 301</td><td>22</td><td>50</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> 47</td><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 264</td><td>22</td><td>46</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> 33</td><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 187</td><td>22</td><td>55</td></tr>
	<tr><td>2013-09-30 23:00:00</td><td>196</td><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>1617</td><td>23</td><td>59</td></tr>
	<tr><td>2013-09-30 18:00:00</td><td> NA</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> 764</td><td>18</td><td>42</td></tr>
	<tr><td>2013-09-30 14:00:00</td><td> NA</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> 213</td><td>14</td><td>55</td></tr>
	<tr><td>2013-09-30 22:00:00</td><td> NA</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> 198</td><td>22</td><td> 0</td></tr>
	<tr><td>2013-09-30 12:00:00</td><td> NA</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> 764</td><td>12</td><td>10</td></tr>
	<tr><td>2013-09-30 11:00:00</td><td> NA</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> 419</td><td>11</td><td>59</td></tr>
	<tr><td>2013-09-30 08:00:00</td><td> NA</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> 431</td><td> 8</td><td>40</td></tr>
</tbody>
</table>



### 3.3. Exercises 

3.3.1 Compare dep_time, sched_dep_time, and dep_delay. How would you expect those three numbers to be related?


```R

```


3.3.2. Brainstorm as many ways as possible to select dep_time, dep_delay, arr_time, and arr_delay from flights.



```R

```

3.3.3. What happens if you specify the name of the same variable multiple times in a select() call?


```R

```

3.3.4. What does the any_of() function do? Why might it be helpful in conjunction with this vector?


```R
variables <- c("year", "month", "day", "dep_delay", "arr_delay")
```

3.3.5. Does the result of running the following code surprise you? How do the select helpers deal with upper and lower case by default? How can you change that default?


```R
flights |> select(contains("TIME"))
```


<table class="dataframe">
<caption>A tibble: 336776 x 6</caption>
<thead>
	<tr><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>air_time</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>517</td><td>515</td><td> 830</td><td> 819</td><td>227</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>533</td><td>529</td><td> 850</td><td> 830</td><td>227</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>542</td><td>540</td><td> 923</td><td> 850</td><td>160</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>544</td><td>545</td><td>1004</td><td>1022</td><td>183</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>554</td><td>600</td><td> 812</td><td> 837</td><td>116</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>554</td><td>558</td><td> 740</td><td> 728</td><td>150</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>555</td><td>600</td><td> 913</td><td> 854</td><td>158</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>557</td><td>600</td><td> 709</td><td> 723</td><td> 53</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>557</td><td>600</td><td> 838</td><td> 846</td><td>140</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td> 753</td><td> 745</td><td>138</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td> 849</td><td> 851</td><td>149</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td> 853</td><td> 856</td><td>158</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td> 924</td><td> 917</td><td>345</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>558</td><td>600</td><td> 923</td><td> 937</td><td>361</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>559</td><td>600</td><td> 941</td><td> 910</td><td>257</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>559</td><td>559</td><td> 702</td><td> 706</td><td> 44</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>559</td><td>600</td><td> 854</td><td> 902</td><td>337</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>600</td><td>600</td><td> 851</td><td> 858</td><td>152</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>600</td><td>600</td><td> 837</td><td> 825</td><td>134</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>601</td><td>600</td><td> 844</td><td> 850</td><td>147</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>602</td><td>610</td><td> 812</td><td> 820</td><td>170</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>602</td><td>605</td><td> 821</td><td> 805</td><td>105</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>606</td><td>610</td><td> 858</td><td> 910</td><td>152</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>606</td><td>610</td><td> 837</td><td> 845</td><td>128</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>607</td><td>607</td><td> 858</td><td> 915</td><td>157</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>608</td><td>600</td><td> 807</td><td> 735</td><td>139</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>611</td><td>600</td><td> 945</td><td> 931</td><td>366</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>613</td><td>610</td><td> 925</td><td> 921</td><td>175</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>615</td><td>615</td><td>1039</td><td>1100</td><td>182</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>615</td><td>615</td><td> 833</td><td> 842</td><td>120</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2123</td><td>2125</td><td>2223</td><td>2247</td><td> 45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2127</td><td>2129</td><td>2314</td><td>2323</td><td> 72</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2128</td><td>2130</td><td>2328</td><td>2359</td><td>213</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2129</td><td>2059</td><td>2230</td><td>2232</td><td> 45</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2131</td><td>2140</td><td>2225</td><td>2255</td><td> 36</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2140</td><td>2140</td><td>  10</td><td>  40</td><td>298</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2142</td><td>2129</td><td>2250</td><td>2239</td><td> 47</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2145</td><td>2145</td><td> 115</td><td> 140</td><td>192</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2147</td><td>2137</td><td>  30</td><td>  27</td><td>139</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2149</td><td>2156</td><td>2245</td><td>2308</td><td> 37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2150</td><td>2159</td><td>2250</td><td>2306</td><td> 39</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2159</td><td>1845</td><td>2344</td><td>2030</td><td> 50</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2203</td><td>2205</td><td>2339</td><td>2331</td><td> 61</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2207</td><td>2140</td><td>2257</td><td>2250</td><td> 97</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2211</td><td>2059</td><td>2339</td><td>2242</td><td>120</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2231</td><td>2245</td><td>2335</td><td>2356</td><td> 48</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2233</td><td>2113</td><td> 112</td><td>  30</td><td>318</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2235</td><td>2001</td><td>  59</td><td>2249</td><td>123</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2237</td><td>2245</td><td>2345</td><td>2353</td><td> 43</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2240</td><td>2245</td><td>2334</td><td>2351</td><td> 41</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2240</td><td>2250</td><td>2347</td><td>   7</td><td> 52</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2241</td><td>2246</td><td>2345</td><td>   1</td><td> 47</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2307</td><td>2255</td><td>2359</td><td>2358</td><td> 33</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2349</td><td>2359</td><td> 325</td><td> 350</td><td>196</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>  NA</td><td>1842</td><td>  NA</td><td>2019</td><td> NA</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>  NA</td><td>1455</td><td>  NA</td><td>1634</td><td> NA</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>  NA</td><td>2200</td><td>  NA</td><td>2312</td><td> NA</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>  NA</td><td>1210</td><td>  NA</td><td>1330</td><td> NA</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>  NA</td><td>1159</td><td>  NA</td><td>1344</td><td> NA</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>  NA</td><td> 840</td><td>  NA</td><td>1020</td><td> NA</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>



3.3.6. Rename air_time to air_time_min to indicate units of measurement and move it to the beginning of the data frame.


```R

```

3.3.7. Why doesn’t the following work, and what does the error mean?


```R
flights |> 
  select(tailnum) |> 
  arrange(arr_delay)
```


    Error in `arrange()`:
    i In argument: `..1 = arr_delay`.
    Caused by error:
    ! object 'arr_delay' not found
    Traceback:


    1. arrange(select(flights, tailnum), arr_delay)

    2. arrange.data.frame(select(flights, tailnum), arr_delay)

    3. arrange_rows(.data, dots = dots, locale = .locale)

    4. mutate(data, `:=`("{name}", !!dot), .keep = "none")

    5. mutate.data.frame(data, `:=`("{name}", !!dot), .keep = "none")

    6. mutate_cols(.data, dplyr_quosures(...), by)

    7. withCallingHandlers(for (i in seq_along(dots)) {
     .     poke_error_context(dots, i, mask = mask)
     .     context_poke("column", old_current_column)
     .     new_columns <- mutate_col(dots[[i]], data, mask, new_columns)
     . }, error = dplyr_error_handler(dots = dots, mask = mask, bullets = mutate_bullets, 
     .     error_call = error_call, error_class = "dplyr:::mutate_error"), 
     .     warning = dplyr_warning_handler(state = warnings_state, mask = mask, 
     .         error_call = error_call))

    8. mutate_col(dots[[i]], data, mask, new_columns)

    9. mask$eval_all_mutate(quo)

    10. eval()

    11. .handleSimpleError(function (cnd) 
      . {
      .     local_error_context(dots, i = frame[[i_sym]], mask = mask)
      .     if (inherits(cnd, "dplyr:::internal_error")) {
      .         parent <- error_cnd(message = bullets(cnd))
      .     }
      .     else {
      .         parent <- cnd
      .     }
      .     message <- c(cnd_bullet_header(action), i = if (has_active_group_context(mask)) cnd_bullet_cur_group_label())
      .     abort(message, class = error_class, parent = parent, call = error_call)
      . }, "object 'arr_delay' not found", base::quote(NULL))

    12. h(simpleError(msg, call))

    13. abort(message, class = error_class, parent = parent, call = error_call)

    14. signal_abort(cnd, .file)


## The pipe


```R
flights |> 
  filter(dest == "IAH") |> 
  mutate(speed = distance / air_time * 60) |> 
  select(year:day, dep_time, carrier, flight, speed) |> 
  arrange(desc(speed))
```


<table class="dataframe">
<caption>A tibble: 7198 x 7</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>speed</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>7</td><td> 9</td><td> 707</td><td>UA</td><td> 226</td><td>521.7391</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1850</td><td>UA</td><td>1128</td><td>521.2270</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td> 902</td><td>UA</td><td>1711</td><td>518.5185</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td>2122</td><td>UA</td><td>1022</td><td>518.5185</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>1628</td><td>UA</td><td>1178</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1017</td><td>UA</td><td> 333</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1205</td><td>UA</td><td>1421</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1758</td><td>UA</td><td> 302</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td> 521</td><td>UA</td><td> 252</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td> 625</td><td>UA</td><td> 559</td><td>514.9091</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td>1505</td><td>UA</td><td>1695</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>9</td><td> 7</td><td>2025</td><td>UA</td><td>1022</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>9</td><td> 8</td><td>1830</td><td>UA</td><td> 404</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1651</td><td>UA</td><td> 525</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 4</td><td> 542</td><td>UA</td><td>1714</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 6</td><td>2006</td><td>UA</td><td>1128</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 8</td><td>1849</td><td>UA</td><td>1128</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>2017</td><td>UA</td><td> 350</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td> 8</td><td>2131</td><td>UA</td><td> 260</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td> 8</td><td>2213</td><td>UA</td><td>1740</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td>12</td><td>1718</td><td>UA</td><td> 268</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td>19</td><td> 634</td><td>UA</td><td> 226</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td>2003</td><td>UA</td><td>1712</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1854</td><td>UA</td><td> 315</td><td>508.7425</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>1517</td><td>UA</td><td>1611</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>6</td><td>15</td><td> 852</td><td>UA</td><td> 215</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 7</td><td>1649</td><td>UA</td><td>1254</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td> 851</td><td>UA</td><td>1711</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td>2001</td><td>UA</td><td> 299</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td>2331</td><td>UA</td><td>1178</td><td>506.0241</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>6</td><td>10</td><td>  NA</td><td>UA</td><td> 318</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>15</td><td>2037</td><td>UA</td><td>1611</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>17</td><td>  NA</td><td>UA</td><td> 318</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>17</td><td>  NA</td><td>UA</td><td>1178</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>19</td><td>  NA</td><td>UA</td><td> 430</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>19</td><td>  NA</td><td>UA</td><td> 531</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>20</td><td>1256</td><td>UA</td><td> 636</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>22</td><td>  NA</td><td>UA</td><td> 251</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>25</td><td>  NA</td><td>UA</td><td> 453</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>27</td><td>1951</td><td>UA</td><td>1611</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>28</td><td>  NA</td><td>UA</td><td> 768</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>10</td><td>1905</td><td>AA</td><td>1901</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>10</td><td>  NA</td><td>UA</td><td>1661</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>11</td><td>  NA</td><td>UA</td><td> 508</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>16</td><td>1302</td><td>UA</td><td> 824</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>17</td><td>  NA</td><td>UA</td><td> 226</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>22</td><td>  NA</td><td>UA</td><td>1259</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>22</td><td>  NA</td><td>UA</td><td>1661</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>23</td><td>  NA</td><td>UA</td><td>1454</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>28</td><td>  NA</td><td>UA</td><td> 408</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td> 2</td><td>  NA</td><td>UA</td><td> 349</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>13</td><td>  NA</td><td>UA</td><td> 220</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>14</td><td>1537</td><td>UA</td><td>1178</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>16</td><td>1456</td><td>UA</td><td>1257</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td> 2</td><td>  NA</td><td>UA</td><td>1128</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>1815</td><td>UA</td><td>1695</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td> 404</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td> 525</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td>1128</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>20</td><td> 752</td><td>UA</td><td>1591</td><td>NA</td></tr>
</tbody>
</table>



What would happen if we didn’t have the pipe? We could nest each function call inside the previous call:


```R
arrange(
  select(
    mutate(
      filter(
        flights, 
        dest == "IAH"
      ),
      speed = distance / air_time * 60
    ),
    year:day, dep_time, carrier, flight, speed
  ),
  desc(speed)
)
```


<table class="dataframe">
<caption>A tibble: 7198 x 7</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>speed</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>7</td><td> 9</td><td> 707</td><td>UA</td><td> 226</td><td>521.7391</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1850</td><td>UA</td><td>1128</td><td>521.2270</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td> 902</td><td>UA</td><td>1711</td><td>518.5185</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td>2122</td><td>UA</td><td>1022</td><td>518.5185</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>1628</td><td>UA</td><td>1178</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1017</td><td>UA</td><td> 333</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1205</td><td>UA</td><td>1421</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1758</td><td>UA</td><td> 302</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td> 521</td><td>UA</td><td> 252</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td> 625</td><td>UA</td><td> 559</td><td>514.9091</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td>1505</td><td>UA</td><td>1695</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>9</td><td> 7</td><td>2025</td><td>UA</td><td>1022</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>9</td><td> 8</td><td>1830</td><td>UA</td><td> 404</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1651</td><td>UA</td><td> 525</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 4</td><td> 542</td><td>UA</td><td>1714</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 6</td><td>2006</td><td>UA</td><td>1128</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 8</td><td>1849</td><td>UA</td><td>1128</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>2017</td><td>UA</td><td> 350</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td> 8</td><td>2131</td><td>UA</td><td> 260</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td> 8</td><td>2213</td><td>UA</td><td>1740</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td>12</td><td>1718</td><td>UA</td><td> 268</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td>19</td><td> 634</td><td>UA</td><td> 226</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td>2003</td><td>UA</td><td>1712</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1854</td><td>UA</td><td> 315</td><td>508.7425</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>1517</td><td>UA</td><td>1611</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>6</td><td>15</td><td> 852</td><td>UA</td><td> 215</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 7</td><td>1649</td><td>UA</td><td>1254</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td> 851</td><td>UA</td><td>1711</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td>2001</td><td>UA</td><td> 299</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td>2331</td><td>UA</td><td>1178</td><td>506.0241</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>6</td><td>10</td><td>  NA</td><td>UA</td><td> 318</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>15</td><td>2037</td><td>UA</td><td>1611</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>17</td><td>  NA</td><td>UA</td><td> 318</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>17</td><td>  NA</td><td>UA</td><td>1178</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>19</td><td>  NA</td><td>UA</td><td> 430</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>19</td><td>  NA</td><td>UA</td><td> 531</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>20</td><td>1256</td><td>UA</td><td> 636</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>22</td><td>  NA</td><td>UA</td><td> 251</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>25</td><td>  NA</td><td>UA</td><td> 453</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>27</td><td>1951</td><td>UA</td><td>1611</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>28</td><td>  NA</td><td>UA</td><td> 768</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>10</td><td>1905</td><td>AA</td><td>1901</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>10</td><td>  NA</td><td>UA</td><td>1661</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>11</td><td>  NA</td><td>UA</td><td> 508</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>16</td><td>1302</td><td>UA</td><td> 824</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>17</td><td>  NA</td><td>UA</td><td> 226</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>22</td><td>  NA</td><td>UA</td><td>1259</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>22</td><td>  NA</td><td>UA</td><td>1661</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>23</td><td>  NA</td><td>UA</td><td>1454</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>28</td><td>  NA</td><td>UA</td><td> 408</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td> 2</td><td>  NA</td><td>UA</td><td> 349</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>13</td><td>  NA</td><td>UA</td><td> 220</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>14</td><td>1537</td><td>UA</td><td>1178</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>16</td><td>1456</td><td>UA</td><td>1257</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td> 2</td><td>  NA</td><td>UA</td><td>1128</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>1815</td><td>UA</td><td>1695</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td> 404</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td> 525</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td>1128</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>20</td><td> 752</td><td>UA</td><td>1591</td><td>NA</td></tr>
</tbody>
</table>



Or we could use a bunch of intermediate objects:


```R
flights1 <- filter(flights, dest == "IAH")
flights2 <- mutate(flights1, speed = distance / air_time * 60)
flights3 <- select(flights2, year:day, dep_time, carrier, flight, speed)
arrange(flights3, desc(speed))
```


<table class="dataframe">
<caption>A tibble: 7198 x 7</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>speed</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>7</td><td> 9</td><td> 707</td><td>UA</td><td> 226</td><td>521.7391</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1850</td><td>UA</td><td>1128</td><td>521.2270</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td> 902</td><td>UA</td><td>1711</td><td>518.5185</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td>2122</td><td>UA</td><td>1022</td><td>518.5185</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>1628</td><td>UA</td><td>1178</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1017</td><td>UA</td><td> 333</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1205</td><td>UA</td><td>1421</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1758</td><td>UA</td><td> 302</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td> 521</td><td>UA</td><td> 252</td><td>515.3374</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td> 625</td><td>UA</td><td> 559</td><td>514.9091</td></tr>
	<tr><td>2013</td><td>8</td><td>28</td><td>1505</td><td>UA</td><td>1695</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>9</td><td> 7</td><td>2025</td><td>UA</td><td>1022</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>9</td><td> 8</td><td>1830</td><td>UA</td><td> 404</td><td>512.1951</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1651</td><td>UA</td><td> 525</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 4</td><td> 542</td><td>UA</td><td>1714</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 6</td><td>2006</td><td>UA</td><td>1128</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>9</td><td> 8</td><td>1849</td><td>UA</td><td>1128</td><td>511.8072</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>2017</td><td>UA</td><td> 350</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td> 8</td><td>2131</td><td>UA</td><td> 260</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td> 8</td><td>2213</td><td>UA</td><td>1740</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td>12</td><td>1718</td><td>UA</td><td> 268</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>7</td><td>19</td><td> 634</td><td>UA</td><td> 226</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>9</td><td>27</td><td>2003</td><td>UA</td><td>1712</td><td>509.0909</td></tr>
	<tr><td>2013</td><td>8</td><td>27</td><td>1854</td><td>UA</td><td> 315</td><td>508.7425</td></tr>
	<tr><td>2013</td><td>6</td><td>11</td><td>1517</td><td>UA</td><td>1611</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>6</td><td>15</td><td> 852</td><td>UA</td><td> 215</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 7</td><td>1649</td><td>UA</td><td>1254</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td> 851</td><td>UA</td><td>1711</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td>2001</td><td>UA</td><td> 299</td><td>506.0241</td></tr>
	<tr><td>2013</td><td>7</td><td> 9</td><td>2331</td><td>UA</td><td>1178</td><td>506.0241</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>6</td><td>10</td><td>  NA</td><td>UA</td><td> 318</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>15</td><td>2037</td><td>UA</td><td>1611</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>17</td><td>  NA</td><td>UA</td><td> 318</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>17</td><td>  NA</td><td>UA</td><td>1178</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>19</td><td>  NA</td><td>UA</td><td> 430</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>19</td><td>  NA</td><td>UA</td><td> 531</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>20</td><td>1256</td><td>UA</td><td> 636</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>22</td><td>  NA</td><td>UA</td><td> 251</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>25</td><td>  NA</td><td>UA</td><td> 453</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>27</td><td>1951</td><td>UA</td><td>1611</td><td>NA</td></tr>
	<tr><td>2013</td><td>6</td><td>28</td><td>  NA</td><td>UA</td><td> 768</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>10</td><td>1905</td><td>AA</td><td>1901</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>10</td><td>  NA</td><td>UA</td><td>1661</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>11</td><td>  NA</td><td>UA</td><td> 508</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>16</td><td>1302</td><td>UA</td><td> 824</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>17</td><td>  NA</td><td>UA</td><td> 226</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>22</td><td>  NA</td><td>UA</td><td>1259</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>22</td><td>  NA</td><td>UA</td><td>1661</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>23</td><td>  NA</td><td>UA</td><td>1454</td><td>NA</td></tr>
	<tr><td>2013</td><td>7</td><td>28</td><td>  NA</td><td>UA</td><td> 408</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td> 2</td><td>  NA</td><td>UA</td><td> 349</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>13</td><td>  NA</td><td>UA</td><td> 220</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>14</td><td>1537</td><td>UA</td><td>1178</td><td>NA</td></tr>
	<tr><td>2013</td><td>8</td><td>16</td><td>1456</td><td>UA</td><td>1257</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td> 2</td><td>  NA</td><td>UA</td><td>1128</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>1815</td><td>UA</td><td>1695</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td> 404</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td> 525</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>12</td><td>  NA</td><td>UA</td><td>1128</td><td>NA</td></tr>
	<tr><td>2013</td><td>9</td><td>20</td><td> 752</td><td>UA</td><td>1591</td><td>NA</td></tr>
</tbody>
</table>



## Groups

### `group_by()`  
divide your dataset into groups meaningful for your analysis:


```R
flights |> 
  group_by(month)
```


<table class="dataframe">
<caption>A grouped_df: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>



### `summarize()`
The most important grouped operation is a summary, which, if being used to calculate a single summary statistic, reduces the data frame to have a single row for each group.


```R
flights |> 
  group_by(month) |> 
  summarize(
    avg_delay = mean(dep_delay)
  )
```


<table class="dataframe">
<caption>A tibble: 12 x 2</caption>
<thead>
	<tr><th scope=col>month</th><th scope=col>avg_delay</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td> 1</td><td>NA</td></tr>
	<tr><td> 2</td><td>NA</td></tr>
	<tr><td> 3</td><td>NA</td></tr>
	<tr><td> 4</td><td>NA</td></tr>
	<tr><td> 5</td><td>NA</td></tr>
	<tr><td> 6</td><td>NA</td></tr>
	<tr><td> 7</td><td>NA</td></tr>
	<tr><td> 8</td><td>NA</td></tr>
	<tr><td> 9</td><td>NA</td></tr>
	<tr><td>10</td><td>NA</td></tr>
	<tr><td>11</td><td>NA</td></tr>
	<tr><td>12</td><td>NA</td></tr>
</tbody>
</table>




```R
flights |> 
  group_by(month) |> 
  summarize(
    avg_delay = mean(dep_delay, na.rm = TRUE)
  )
```


<table class="dataframe">
<caption>A tibble: 12 x 2</caption>
<thead>
	<tr><th scope=col>month</th><th scope=col>avg_delay</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td> 1</td><td>10.036665</td></tr>
	<tr><td> 2</td><td>10.816843</td></tr>
	<tr><td> 3</td><td>13.227076</td></tr>
	<tr><td> 4</td><td>13.938038</td></tr>
	<tr><td> 5</td><td>12.986859</td></tr>
	<tr><td> 6</td><td>20.846332</td></tr>
	<tr><td> 7</td><td>21.727787</td></tr>
	<tr><td> 8</td><td>12.611040</td></tr>
	<tr><td> 9</td><td> 6.722476</td></tr>
	<tr><td>10</td><td> 6.243988</td></tr>
	<tr><td>11</td><td> 5.435362</td></tr>
	<tr><td>12</td><td>16.576688</td></tr>
</tbody>
</table>




```R
flights |> 
  group_by(month) |> 
  summarize(
    avg_delay = mean(dep_delay, na.rm = TRUE), 
    n = n()
  )
```


<table class="dataframe">
<caption>A tibble: 12 x 3</caption>
<thead>
	<tr><th scope=col>month</th><th scope=col>avg_delay</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td> 1</td><td>10.036665</td><td>27004</td></tr>
	<tr><td> 2</td><td>10.816843</td><td>24951</td></tr>
	<tr><td> 3</td><td>13.227076</td><td>28834</td></tr>
	<tr><td> 4</td><td>13.938038</td><td>28330</td></tr>
	<tr><td> 5</td><td>12.986859</td><td>28796</td></tr>
	<tr><td> 6</td><td>20.846332</td><td>28243</td></tr>
	<tr><td> 7</td><td>21.727787</td><td>29425</td></tr>
	<tr><td> 8</td><td>12.611040</td><td>29327</td></tr>
	<tr><td> 9</td><td> 6.722476</td><td>27574</td></tr>
	<tr><td>10</td><td> 6.243988</td><td>28889</td></tr>
	<tr><td>11</td><td> 5.435362</td><td>27268</td></tr>
	<tr><td>12</td><td>16.576688</td><td>28135</td></tr>
</tbody>
</table>



### The `slice_` functions
* `df |> slice_head(n = 1)` takes the first row from each group.
* `df |> slice_tail(n = 1)` takes the last row in each group.
* `df |> slice_min(x, n = 1)` takes the row with the smallest value of column x.
* `df |> slice_max(x, n = 1)` takes the row with the largest value of column x.
* `df |> slice_sample(n = 1)` takes one random row.

You can vary n to select more than one row, or instead of n =, you can use prop = 0.1 to select (e.g.) 10% of the rows in each group


```R
flights |> 
  group_by(dest) |> 
  slice_max(arr_delay, with_ties = FALSE, n = 1) |>
  relocate(dest)
```


<table class="dataframe">
<caption>A grouped_df: 105 x 19</caption>
<thead>
	<tr><th scope=col>dest</th><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>ABQ</td><td>2013</td><td> 7</td><td>22</td><td>2145</td><td>2007</td><td>  98</td><td> 132</td><td>2259</td><td> 153</td><td>B6</td><td>1505</td><td>N784JB</td><td>JFK</td><td>259</td><td>1826</td><td>20</td><td> 7</td><td>2013-07-22 20:00:00</td></tr>
	<tr><td>ACK</td><td>2013</td><td> 7</td><td>23</td><td>1139</td><td> 800</td><td> 219</td><td>1250</td><td> 909</td><td> 221</td><td>B6</td><td>1491</td><td>N192JB</td><td>JFK</td><td> 44</td><td> 199</td><td> 8</td><td> 0</td><td>2013-07-23 08:00:00</td></tr>
	<tr><td>ALB</td><td>2013</td><td> 1</td><td>25</td><td> 123</td><td>2000</td><td> 323</td><td> 229</td><td>2101</td><td> 328</td><td>EV</td><td>4309</td><td>N13908</td><td>EWR</td><td> 30</td><td> 143</td><td>20</td><td> 0</td><td>2013-01-25 20:00:00</td></tr>
	<tr><td>ANC</td><td>2013</td><td> 8</td><td>17</td><td>1740</td><td>1625</td><td>  75</td><td>2042</td><td>2003</td><td>  39</td><td>UA</td><td> 887</td><td>N528UA</td><td>EWR</td><td>404</td><td>3370</td><td>16</td><td>25</td><td>2013-08-17 16:00:00</td></tr>
	<tr><td>ATL</td><td>2013</td><td> 7</td><td>22</td><td>2257</td><td> 759</td><td> 898</td><td> 121</td><td>1026</td><td> 895</td><td>DL</td><td>2047</td><td>N6716C</td><td>LGA</td><td>109</td><td> 762</td><td> 7</td><td>59</td><td>2013-07-22 07:00:00</td></tr>
	<tr><td>AUS</td><td>2013</td><td> 7</td><td>10</td><td>2056</td><td>1505</td><td> 351</td><td>2347</td><td>1758</td><td> 349</td><td>UA</td><td> 503</td><td>N803UA</td><td>EWR</td><td>192</td><td>1504</td><td>15</td><td> 5</td><td>2013-07-10 15:00:00</td></tr>
	<tr><td>AVL</td><td>2013</td><td> 8</td><td>13</td><td>1156</td><td> 832</td><td> 204</td><td>1417</td><td>1029</td><td> 228</td><td>EV</td><td>4175</td><td>N13538</td><td>EWR</td><td>108</td><td> 583</td><td> 8</td><td>32</td><td>2013-08-13 08:00:00</td></tr>
	<tr><td>BDL</td><td>2013</td><td> 2</td><td>21</td><td>1728</td><td>1316</td><td> 252</td><td>1839</td><td>1413</td><td> 266</td><td>EV</td><td>4103</td><td>N16976</td><td>EWR</td><td> 26</td><td> 116</td><td>13</td><td>16</td><td>2013-02-21 13:00:00</td></tr>
	<tr><td>BGR</td><td>2013</td><td>12</td><td> 1</td><td>1504</td><td>1056</td><td> 248</td><td>1628</td><td>1230</td><td> 238</td><td>EV</td><td>5309</td><td>N615QX</td><td>LGA</td><td> 57</td><td> 378</td><td>10</td><td>56</td><td>2013-12-01 10:00:00</td></tr>
	<tr><td>BHM</td><td>2013</td><td> 4</td><td>10</td><td>  25</td><td>1900</td><td> 325</td><td> 136</td><td>2045</td><td> 291</td><td>EV</td><td>5038</td><td>N713EV</td><td>LGA</td><td>115</td><td> 866</td><td>19</td><td> 0</td><td>2013-04-10 19:00:00</td></tr>
	<tr><td>BNA</td><td>2013</td><td> 1</td><td>25</td><td>2020</td><td>1527</td><td> 293</td><td>2304</td><td>1700</td><td> 364</td><td>EV</td><td>3835</td><td>N14920</td><td>EWR</td><td>124</td><td> 748</td><td>15</td><td>27</td><td>2013-01-25 15:00:00</td></tr>
	<tr><td>BOS</td><td>2013</td><td> 3</td><td> 8</td><td>1819</td><td>1200</td><td> 379</td><td>2005</td><td>1303</td><td> 422</td><td>B6</td><td>1174</td><td>N329JB</td><td>EWR</td><td> 47</td><td> 200</td><td>12</td><td> 0</td><td>2013-03-08 12:00:00</td></tr>
	<tr><td>BQN</td><td>2013</td><td> 6</td><td>13</td><td>   6</td><td>2034</td><td> 212</td><td> 358</td><td>  30</td><td> 208</td><td>UA</td><td>1071</td><td>N77296</td><td>EWR</td><td>216</td><td>1585</td><td>20</td><td>34</td><td>2013-06-13 20:00:00</td></tr>
	<tr><td>BTV</td><td>2013</td><td> 9</td><td>12</td><td>2125</td><td>1459</td><td> 386</td><td>2258</td><td>1622</td><td> 396</td><td>B6</td><td>1734</td><td>N178JB</td><td>JFK</td><td> 52</td><td> 266</td><td>14</td><td>59</td><td>2013-09-12 14:00:00</td></tr>
	<tr><td>BUF</td><td>2013</td><td>11</td><td>27</td><td>1503</td><td> 815</td><td> 408</td><td>1628</td><td> 952</td><td> 396</td><td>9E</td><td>2906</td><td>N930XJ</td><td>JFK</td><td> 56</td><td> 301</td><td> 8</td><td>15</td><td>2013-11-27 08:00:00</td></tr>
	<tr><td>BUR</td><td>2013</td><td> 6</td><td>27</td><td>2146</td><td>1800</td><td> 226</td><td> 109</td><td>2102</td><td> 247</td><td>B6</td><td> 359</td><td>N635JB</td><td>JFK</td><td>321</td><td>2465</td><td>18</td><td> 0</td><td>2013-06-27 18:00:00</td></tr>
	<tr><td>BWI</td><td>2013</td><td> 1</td><td> 1</td><td> 848</td><td>1835</td><td> 853</td><td>1001</td><td>1950</td><td> 851</td><td>MQ</td><td>3944</td><td>N942MQ</td><td>JFK</td><td> 41</td><td> 184</td><td>18</td><td>35</td><td>2013-01-01 18:00:00</td></tr>
	<tr><td>BZN</td><td>2013</td><td>12</td><td>28</td><td>1104</td><td> 819</td><td> 165</td><td>1353</td><td>1119</td><td> 154</td><td>UA</td><td> 568</td><td>N436UA</td><td>EWR</td><td>267</td><td>1882</td><td> 8</td><td>19</td><td>2013-12-28 08:00:00</td></tr>
	<tr><td>CAE</td><td>2013</td><td> 4</td><td>14</td><td>2148</td><td>1846</td><td> 182</td><td>2400</td><td>2016</td><td> 224</td><td>EV</td><td>4471</td><td>N15983</td><td>EWR</td><td>100</td><td> 602</td><td>18</td><td>46</td><td>2013-04-14 18:00:00</td></tr>
	<tr><td>CAK</td><td>2013</td><td>12</td><td>18</td><td>1702</td><td> 950</td><td> 432</td><td>1836</td><td>1123</td><td> 433</td><td>FL</td><td> 160</td><td>N972AT</td><td>LGA</td><td> 70</td><td> 397</td><td> 9</td><td>50</td><td>2013-12-18 09:00:00</td></tr>
	<tr><td>CHO</td><td>2013</td><td> 3</td><td> 8</td><td>2355</td><td>1940</td><td> 255</td><td> 109</td><td>2121</td><td> 228</td><td>EV</td><td>5325</td><td>N611QX</td><td>LGA</td><td> 42</td><td> 305</td><td>19</td><td>40</td><td>2013-03-08 19:00:00</td></tr>
	<tr><td>CHS</td><td>2013</td><td> 3</td><td> 8</td><td>1202</td><td> 751</td><td> 251</td><td>1530</td><td> 959</td><td> 331</td><td>EV</td><td>4532</td><td>N15555</td><td>EWR</td><td> 88</td><td> 628</td><td> 7</td><td>51</td><td>2013-03-08 07:00:00</td></tr>
	<tr><td>CLE</td><td>2013</td><td>12</td><td>22</td><td>2236</td><td>1430</td><td> 486</td><td>  15</td><td>1626</td><td> 469</td><td>EV</td><td>4159</td><td>N15912</td><td>LGA</td><td> 71</td><td> 419</td><td>14</td><td>30</td><td>2013-12-22 14:00:00</td></tr>
	<tr><td>CLT</td><td>2013</td><td> 2</td><td>16</td><td> 757</td><td>1930</td><td> 747</td><td>1013</td><td>2149</td><td> 744</td><td>9E</td><td>3798</td><td>N8940E</td><td>JFK</td><td> 85</td><td> 541</td><td>19</td><td>30</td><td>2013-02-16 19:00:00</td></tr>
	<tr><td>CMH</td><td>2013</td><td> 6</td><td>15</td><td>1432</td><td>1935</td><td>1137</td><td>1607</td><td>2120</td><td>1127</td><td>MQ</td><td>3535</td><td>N504MQ</td><td>JFK</td><td> 74</td><td> 483</td><td>19</td><td>35</td><td>2013-06-15 19:00:00</td></tr>
	<tr><td>CRW</td><td>2013</td><td> 4</td><td>18</td><td>2158</td><td>1845</td><td> 193</td><td>2339</td><td>2030</td><td> 189</td><td>MQ</td><td>4517</td><td>N713MQ</td><td>LGA</td><td> 73</td><td> 444</td><td>18</td><td>45</td><td>2013-04-18 18:00:00</td></tr>
	<tr><td>CVG</td><td>2013</td><td> 7</td><td>22</td><td> 845</td><td>1600</td><td>1005</td><td>1044</td><td>1815</td><td> 989</td><td>MQ</td><td>3075</td><td>N665MQ</td><td>JFK</td><td> 96</td><td> 589</td><td>16</td><td> 0</td><td>2013-07-22 16:00:00</td></tr>
	<tr><td>DAY</td><td>2013</td><td>12</td><td> 5</td><td>1504</td><td> 955</td><td> 309</td><td>1709</td><td>1217</td><td> 292</td><td>9E</td><td>4060</td><td>N8877A</td><td>LGA</td><td> 96</td><td> 549</td><td> 9</td><td>55</td><td>2013-12-05 09:00:00</td></tr>
	<tr><td>DCA</td><td>2013</td><td> 2</td><td>27</td><td>1529</td><td> 845</td><td> 404</td><td>1639</td><td>1015</td><td> 384</td><td>9E</td><td>3405</td><td>N922XJ</td><td>JFK</td><td> 49</td><td> 213</td><td> 8</td><td>45</td><td>2013-02-27 08:00:00</td></tr>
	<tr><td>DEN</td><td>2013</td><td> 2</td><td>10</td><td>2243</td><td> 830</td><td> 853</td><td> 100</td><td>1106</td><td> 834</td><td>F9</td><td> 835</td><td>N203FR</td><td>LGA</td><td>233</td><td>1620</td><td> 8</td><td>30</td><td>2013-02-10 08:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>PIT</td><td>2013</td><td> 6</td><td>25</td><td>1421</td><td> 805</td><td> 376</td><td>1602</td><td> 950</td><td> 372</td><td>9E</td><td>3611</td><td>N8458A</td><td>JFK</td><td> 64</td><td> 340</td><td> 8</td><td> 5</td><td>2013-06-25 08:00:00</td></tr>
	<tr><td>PSE</td><td>2013</td><td> 6</td><td>28</td><td> 317</td><td>2359</td><td> 198</td><td> 652</td><td> 350</td><td> 182</td><td>B6</td><td> 745</td><td>N568JB</td><td>JFK</td><td>199</td><td>1617</td><td>23</td><td>59</td><td>2013-06-28 23:00:00</td></tr>
	<tr><td>PSP</td><td>2013</td><td> 3</td><td>16</td><td>1046</td><td>1055</td><td>  -9</td><td>1412</td><td>1355</td><td>  17</td><td>VX</td><td>  55</td><td>N839VA</td><td>JFK</td><td>365</td><td>2378</td><td>10</td><td>55</td><td>2013-03-16 10:00:00</td></tr>
	<tr><td>PVD</td><td>2013</td><td> 3</td><td>18</td><td> 200</td><td>2115</td><td> 285</td><td> 259</td><td>2214</td><td> 285</td><td>EV</td><td>4404</td><td>N11547</td><td>EWR</td><td> 27</td><td> 160</td><td>21</td><td>15</td><td>2013-03-18 21:00:00</td></tr>
	<tr><td>PWM</td><td>2013</td><td> 3</td><td> 8</td><td>1300</td><td> 829</td><td> 271</td><td>1505</td><td> 955</td><td> 310</td><td>EV</td><td>4224</td><td>N12540</td><td>EWR</td><td> 52</td><td> 284</td><td> 8</td><td>29</td><td>2013-03-08 08:00:00</td></tr>
	<tr><td>RDU</td><td>2013</td><td> 6</td><td>13</td><td>1833</td><td>1250</td><td> 343</td><td>2135</td><td>1425</td><td> 430</td><td>MQ</td><td>3361</td><td>N804MQ</td><td>JFK</td><td> 76</td><td> 427</td><td>12</td><td>50</td><td>2013-06-13 12:00:00</td></tr>
	<tr><td>RIC</td><td>2013</td><td> 7</td><td>22</td><td>  41</td><td>1638</td><td> 483</td><td> 154</td><td>1811</td><td> 463</td><td>EV</td><td>4300</td><td>N13970</td><td>EWR</td><td> 47</td><td> 277</td><td>16</td><td>38</td><td>2013-07-22 16:00:00</td></tr>
	<tr><td>ROC</td><td>2013</td><td> 6</td><td>27</td><td>2334</td><td>1635</td><td> 419</td><td>  32</td><td>1805</td><td> 387</td><td>EV</td><td>4322</td><td>N11191</td><td>EWR</td><td> 40</td><td> 246</td><td>16</td><td>35</td><td>2013-06-27 16:00:00</td></tr>
	<tr><td>RSW</td><td>2013</td><td> 2</td><td>27</td><td>2138</td><td>1658</td><td> 280</td><td>  39</td><td>2007</td><td> 272</td><td>B6</td><td> 139</td><td>N228JB</td><td>JFK</td><td>162</td><td>1074</td><td>16</td><td>58</td><td>2013-02-27 16:00:00</td></tr>
	<tr><td>SAN</td><td>2013</td><td> 6</td><td>27</td><td> 615</td><td>1705</td><td> 790</td><td> 853</td><td>2004</td><td> 769</td><td>DL</td><td> 503</td><td>N372DA</td><td>JFK</td><td>312</td><td>2446</td><td>17</td><td> 5</td><td>2013-06-27 17:00:00</td></tr>
	<tr><td>SAT</td><td>2013</td><td>12</td><td> 1</td><td> 657</td><td>1930</td><td> 687</td><td>1010</td><td>2249</td><td> 681</td><td>DL</td><td>1091</td><td>N342NW</td><td>JFK</td><td>211</td><td>1587</td><td>19</td><td>30</td><td>2013-12-01 19:00:00</td></tr>
	<tr><td>SAV</td><td>2013</td><td>12</td><td> 5</td><td>1735</td><td>1024</td><td> 431</td><td>2009</td><td>1246</td><td> 443</td><td>EV</td><td>4495</td><td>N14977</td><td>EWR</td><td>111</td><td> 708</td><td>10</td><td>24</td><td>2013-12-05 10:00:00</td></tr>
	<tr><td>SBN</td><td>2013</td><td>11</td><td>22</td><td>2013</td><td>1905</td><td>  68</td><td>2224</td><td>2131</td><td>  53</td><td>EV</td><td>5383</td><td>N398CA</td><td>LGA</td><td>110</td><td> 651</td><td>19</td><td> 5</td><td>2013-11-22 19:00:00</td></tr>
	<tr><td>SDF</td><td>2013</td><td> 7</td><td>10</td><td>2111</td><td>1615</td><td> 296</td><td>  57</td><td>1900</td><td> 357</td><td>9E</td><td>3926</td><td>N800AY</td><td>JFK</td><td>110</td><td> 662</td><td>16</td><td>15</td><td>2013-07-10 16:00:00</td></tr>
	<tr><td>SEA</td><td>2013</td><td> 6</td><td>24</td><td> 159</td><td>1735</td><td> 504</td><td> 432</td><td>2108</td><td> 444</td><td>DL</td><td>1543</td><td>N727TW</td><td>JFK</td><td>307</td><td>2422</td><td>17</td><td>35</td><td>2013-06-24 17:00:00</td></tr>
	<tr><td>SFO</td><td>2013</td><td> 9</td><td>20</td><td>1139</td><td>1845</td><td>1014</td><td>1457</td><td>2210</td><td>1007</td><td>AA</td><td> 177</td><td>N338AA</td><td>JFK</td><td>354</td><td>2586</td><td>18</td><td>45</td><td>2013-09-20 18:00:00</td></tr>
	<tr><td>SJC</td><td>2013</td><td> 7</td><td>10</td><td>2227</td><td>1855</td><td> 212</td><td> 202</td><td>2216</td><td> 226</td><td>B6</td><td> 669</td><td>N621JB</td><td>JFK</td><td>338</td><td>2569</td><td>18</td><td>55</td><td>2013-07-10 18:00:00</td></tr>
	<tr><td>SJU</td><td>2013</td><td> 7</td><td>18</td><td>2131</td><td>1455</td><td> 396</td><td> 116</td><td>1905</td><td> 371</td><td>AA</td><td>1635</td><td>N5FNAA</td><td>JFK</td><td>198</td><td>1598</td><td>14</td><td>55</td><td>2013-07-18 14:00:00</td></tr>
	<tr><td>SLC</td><td>2013</td><td>12</td><td>19</td><td> 734</td><td>1725</td><td> 849</td><td>1046</td><td>2039</td><td> 847</td><td>DL</td><td>1223</td><td>N375NC</td><td>EWR</td><td>290</td><td>1969</td><td>17</td><td>25</td><td>2013-12-19 17:00:00</td></tr>
	<tr><td>SMF</td><td>2013</td><td> 4</td><td>19</td><td>2346</td><td>1845</td><td> 301</td><td> 248</td><td>2217</td><td> 271</td><td>B6</td><td> 171</td><td>N706JB</td><td>JFK</td><td>335</td><td>2521</td><td>18</td><td>45</td><td>2013-04-19 18:00:00</td></tr>
	<tr><td>SNA</td><td>2013</td><td> 7</td><td>23</td><td>1034</td><td> 715</td><td> 199</td><td>1307</td><td> 958</td><td> 189</td><td>UA</td><td> 288</td><td>N514UA</td><td>EWR</td><td>307</td><td>2434</td><td> 7</td><td>15</td><td>2013-07-23 07:00:00</td></tr>
	<tr><td>SRQ</td><td>2013</td><td> 6</td><td>24</td><td>1713</td><td>1055</td><td> 378</td><td>2205</td><td>1411</td><td> 474</td><td>DL</td><td>1903</td><td>N345NB</td><td>LGA</td><td>154</td><td>1047</td><td>10</td><td>55</td><td>2013-06-24 10:00:00</td></tr>
	<tr><td>STL</td><td>2013</td><td> 6</td><td>27</td><td> 753</td><td>1830</td><td> 803</td><td> 937</td><td>2015</td><td> 802</td><td>AA</td><td>2019</td><td>N571AA</td><td>LGA</td><td>134</td><td> 888</td><td>18</td><td>30</td><td>2013-06-27 18:00:00</td></tr>
	<tr><td>STT</td><td>2013</td><td> 2</td><td>11</td><td>1416</td><td> 810</td><td> 366</td><td>1845</td><td>1315</td><td> 330</td><td>AA</td><td> 655</td><td>N625AA</td><td>JFK</td><td>180</td><td>1623</td><td> 8</td><td>10</td><td>2013-02-11 08:00:00</td></tr>
	<tr><td>SYR</td><td>2013</td><td> 7</td><td>10</td><td>2257</td><td>1705</td><td> 352</td><td> 116</td><td>1845</td><td> 391</td><td>B6</td><td>1516</td><td>N238JB</td><td>JFK</td><td> 42</td><td> 209</td><td>17</td><td> 5</td><td>2013-07-10 17:00:00</td></tr>
	<tr><td>TPA</td><td>2013</td><td> 4</td><td>10</td><td>1100</td><td>1900</td><td> 960</td><td>1342</td><td>2211</td><td> 931</td><td>DL</td><td>2391</td><td>N959DL</td><td>JFK</td><td>139</td><td>1005</td><td>19</td><td> 0</td><td>2013-04-10 19:00:00</td></tr>
	<tr><td>TUL</td><td>2013</td><td> 1</td><td>20</td><td>2347</td><td>1936</td><td> 251</td><td> 230</td><td>2208</td><td> 262</td><td>EV</td><td>4333</td><td>N14177</td><td>EWR</td><td>208</td><td>1215</td><td>19</td><td>36</td><td>2013-01-20 19:00:00</td></tr>
	<tr><td>TVC</td><td>2013</td><td> 8</td><td>10</td><td>1120</td><td> 730</td><td> 230</td><td>1323</td><td> 943</td><td> 220</td><td>EV</td><td>5144</td><td>N718EV</td><td>LGA</td><td> 96</td><td> 655</td><td> 7</td><td>30</td><td>2013-08-10 07:00:00</td></tr>
	<tr><td>TYS</td><td>2013</td><td> 4</td><td>12</td><td>  51</td><td>2000</td><td> 291</td><td> 250</td><td>2209</td><td> 281</td><td>EV</td><td>3826</td><td>N15986</td><td>EWR</td><td>103</td><td> 631</td><td>20</td><td> 0</td><td>2013-04-12 20:00:00</td></tr>
	<tr><td>XNA</td><td>2013</td><td> 3</td><td> 8</td><td>1311</td><td> 822</td><td> 289</td><td>1615</td><td>1045</td><td> 330</td><td>EV</td><td>4140</td><td>N18556</td><td>EWR</td><td>168</td><td>1131</td><td> 8</td><td>22</td><td>2013-03-08 08:00:00</td></tr>
</tbody>
</table>



### Grouping by multiple variables


```R
daily <- flights |>  
  group_by(year, month, day)
daily
```


<table class="dataframe">
<caption>A grouped_df: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>




```R
# daily_flights <- daily |> 
#   summarize(n = n())
#> `summarise()` has grouped output by 'year', 'month'. You can override using
#> the `.groups` argument.
daily_flights <- daily |> 
  summarize(
    n = n(), 
    .groups = "drop_last"
  )
```

### Ungrouping
You might also want to remove grouping from a data frame without using `summarize()`. You can do this with `ungroup()`


```R
daily |> 
  ungroup()
```


<table class="dataframe">
<caption>A tibble: 336776 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>




```R
daily |> 
  ungroup() |>
  summarize(
    avg_delay = mean(dep_delay, na.rm = TRUE), 
    flights = n()
  )
```


<table class="dataframe">
<caption>A tibble: 1 x 2</caption>
<thead>
	<tr><th scope=col>avg_delay</th><th scope=col>flights</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>12.63907</td><td>336776</td></tr>
</tbody>
</table>



### `.by`
Instead of using `group_by()` and `ungroup()`


```R
flights |> 
  summarize(
    delay = mean(dep_delay, na.rm = TRUE), 
    n = n(),
    .by = c(origin, dest)
  )
```


<table class="dataframe">
<caption>A tibble: 224 x 4</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>dest</th><th scope=col>delay</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>EWR</td><td>IAH</td><td>11.826551</td><td> 3973</td></tr>
	<tr><td>LGA</td><td>IAH</td><td> 9.058986</td><td> 2951</td></tr>
	<tr><td>JFK</td><td>MIA</td><td> 9.336571</td><td> 3314</td></tr>
	<tr><td>JFK</td><td>BQN</td><td> 6.665546</td><td>  599</td></tr>
	<tr><td>LGA</td><td>ATL</td><td>11.448621</td><td>10263</td></tr>
	<tr><td>EWR</td><td>ORD</td><td>14.644163</td><td> 6100</td></tr>
	<tr><td>EWR</td><td>FLL</td><td>13.532606</td><td> 3793</td></tr>
	<tr><td>LGA</td><td>IAD</td><td>16.650421</td><td> 1803</td></tr>
	<tr><td>JFK</td><td>MCO</td><td>10.601583</td><td> 5464</td></tr>
	<tr><td>LGA</td><td>ORD</td><td>10.740758</td><td> 8857</td></tr>
	<tr><td>JFK</td><td>PBI</td><td>14.420290</td><td> 1739</td></tr>
	<tr><td>JFK</td><td>TPA</td><td>12.012855</td><td> 2987</td></tr>
	<tr><td>JFK</td><td>LAX</td><td> 8.522508</td><td>11262</td></tr>
	<tr><td>EWR</td><td>SFO</td><td>14.326394</td><td> 5127</td></tr>
	<tr><td>LGA</td><td>DFW</td><td> 5.806151</td><td> 4858</td></tr>
	<tr><td>JFK</td><td>BOS</td><td>11.694953</td><td> 5898</td></tr>
	<tr><td>EWR</td><td>LAS</td><td>11.230075</td><td> 2010</td></tr>
	<tr><td>LGA</td><td>FLL</td><td>12.876453</td><td> 4008</td></tr>
	<tr><td>EWR</td><td>PBI</td><td>13.962329</td><td> 2351</td></tr>
	<tr><td>LGA</td><td>MSP</td><td> 9.752957</td><td> 3713</td></tr>
	<tr><td>LGA</td><td>DTW</td><td> 7.770528</td><td> 5040</td></tr>
	<tr><td>EWR</td><td>MIA</td><td>11.615385</td><td> 2633</td></tr>
	<tr><td>JFK</td><td>ATL</td><td>10.465974</td><td> 1930</td></tr>
	<tr><td>JFK</td><td>SFO</td><td>11.952691</td><td> 8204</td></tr>
	<tr><td>JFK</td><td>RSW</td><td>10.082017</td><td> 1339</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>10.334039</td><td> 4752</td></tr>
	<tr><td>EWR</td><td>ATL</td><td>15.501738</td><td> 5022</td></tr>
	<tr><td>EWR</td><td>PHX</td><td>10.635789</td><td> 2723</td></tr>
	<tr><td>LGA</td><td>MIA</td><td> 7.361747</td><td> 5781</td></tr>
	<tr><td>EWR</td><td>MSP</td><td>15.313163</td><td> 2377</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>JFK</td><td>ACK</td><td> 6.4566038</td><td>265</td></tr>
	<tr><td>LGA</td><td>BGR</td><td>19.4750000</td><td>375</td></tr>
	<tr><td>LGA</td><td>MSN</td><td>27.1179245</td><td>218</td></tr>
	<tr><td>LGA</td><td>ORF</td><td>16.5538462</td><td>206</td></tr>
	<tr><td>JFK</td><td>IAH</td><td>15.6176471</td><td>274</td></tr>
	<tr><td>JFK</td><td>MCI</td><td>23.0859375</td><td>276</td></tr>
	<tr><td>LGA</td><td>OMA</td><td>27.3695652</td><td> 95</td></tr>
	<tr><td>LGA</td><td>DSM</td><td>17.2222222</td><td>158</td></tr>
	<tr><td>LGA</td><td>GSP</td><td> 8.2346939</td><td>104</td></tr>
	<tr><td>JFK</td><td>ABQ</td><td>13.7401575</td><td>254</td></tr>
	<tr><td>LGA</td><td>ILM</td><td>19.4166667</td><td>110</td></tr>
	<tr><td>LGA</td><td>SYR</td><td>19.1107011</td><td>293</td></tr>
	<tr><td>JFK</td><td>MVY</td><td> 7.0516432</td><td>221</td></tr>
	<tr><td>LGA</td><td>SBN</td><td>31.3333333</td><td>  6</td></tr>
	<tr><td>JFK</td><td>STL</td><td>20.0000000</td><td>  1</td></tr>
	<tr><td>LGA</td><td>LEX</td><td>-9.0000000</td><td>  1</td></tr>
	<tr><td>EWR</td><td>SBN</td><td> 5.7500000</td><td>  4</td></tr>
	<tr><td>LGA</td><td>MHT</td><td>24.0370370</td><td>142</td></tr>
	<tr><td>LGA</td><td>CAE</td><td>29.5000000</td><td> 12</td></tr>
	<tr><td>JFK</td><td>JAC</td><td> 5.0000000</td><td>  2</td></tr>
	<tr><td>JFK</td><td>SDF</td><td>23.9767442</td><td> 46</td></tr>
	<tr><td>LGA</td><td>CHO</td><td>21.3913043</td><td> 52</td></tr>
	<tr><td>JFK</td><td>MKE</td><td>19.8604651</td><td>183</td></tr>
	<tr><td>LGA</td><td>AVL</td><td>-2.6000000</td><td> 10</td></tr>
	<tr><td>JFK</td><td>BHM</td><td> 7.0000000</td><td>  1</td></tr>
	<tr><td>LGA</td><td>TVC</td><td>23.4109589</td><td> 77</td></tr>
	<tr><td>LGA</td><td>MYR</td><td> 0.6666667</td><td>  3</td></tr>
	<tr><td>EWR</td><td>TVC</td><td>17.8695652</td><td> 24</td></tr>
	<tr><td>EWR</td><td>ANC</td><td>12.8750000</td><td>  8</td></tr>
	<tr><td>EWR</td><td>LGA</td><td>       NaN</td><td>  1</td></tr>
</tbody>
</table>




```R
# group by multiple variables
flights |> 
  summarize(
    delay = mean(dep_delay, na.rm = TRUE), 
    n = n(),
    .by = c(origin, dest)
  )
```


<table class="dataframe">
<caption>A tibble: 224 x 4</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>dest</th><th scope=col>delay</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>EWR</td><td>IAH</td><td>11.826551</td><td> 3973</td></tr>
	<tr><td>LGA</td><td>IAH</td><td> 9.058986</td><td> 2951</td></tr>
	<tr><td>JFK</td><td>MIA</td><td> 9.336571</td><td> 3314</td></tr>
	<tr><td>JFK</td><td>BQN</td><td> 6.665546</td><td>  599</td></tr>
	<tr><td>LGA</td><td>ATL</td><td>11.448621</td><td>10263</td></tr>
	<tr><td>EWR</td><td>ORD</td><td>14.644163</td><td> 6100</td></tr>
	<tr><td>EWR</td><td>FLL</td><td>13.532606</td><td> 3793</td></tr>
	<tr><td>LGA</td><td>IAD</td><td>16.650421</td><td> 1803</td></tr>
	<tr><td>JFK</td><td>MCO</td><td>10.601583</td><td> 5464</td></tr>
	<tr><td>LGA</td><td>ORD</td><td>10.740758</td><td> 8857</td></tr>
	<tr><td>JFK</td><td>PBI</td><td>14.420290</td><td> 1739</td></tr>
	<tr><td>JFK</td><td>TPA</td><td>12.012855</td><td> 2987</td></tr>
	<tr><td>JFK</td><td>LAX</td><td> 8.522508</td><td>11262</td></tr>
	<tr><td>EWR</td><td>SFO</td><td>14.326394</td><td> 5127</td></tr>
	<tr><td>LGA</td><td>DFW</td><td> 5.806151</td><td> 4858</td></tr>
	<tr><td>JFK</td><td>BOS</td><td>11.694953</td><td> 5898</td></tr>
	<tr><td>EWR</td><td>LAS</td><td>11.230075</td><td> 2010</td></tr>
	<tr><td>LGA</td><td>FLL</td><td>12.876453</td><td> 4008</td></tr>
	<tr><td>EWR</td><td>PBI</td><td>13.962329</td><td> 2351</td></tr>
	<tr><td>LGA</td><td>MSP</td><td> 9.752957</td><td> 3713</td></tr>
	<tr><td>LGA</td><td>DTW</td><td> 7.770528</td><td> 5040</td></tr>
	<tr><td>EWR</td><td>MIA</td><td>11.615385</td><td> 2633</td></tr>
	<tr><td>JFK</td><td>ATL</td><td>10.465974</td><td> 1930</td></tr>
	<tr><td>JFK</td><td>SFO</td><td>11.952691</td><td> 8204</td></tr>
	<tr><td>JFK</td><td>RSW</td><td>10.082017</td><td> 1339</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>10.334039</td><td> 4752</td></tr>
	<tr><td>EWR</td><td>ATL</td><td>15.501738</td><td> 5022</td></tr>
	<tr><td>EWR</td><td>PHX</td><td>10.635789</td><td> 2723</td></tr>
	<tr><td>LGA</td><td>MIA</td><td> 7.361747</td><td> 5781</td></tr>
	<tr><td>EWR</td><td>MSP</td><td>15.313163</td><td> 2377</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>JFK</td><td>ACK</td><td> 6.4566038</td><td>265</td></tr>
	<tr><td>LGA</td><td>BGR</td><td>19.4750000</td><td>375</td></tr>
	<tr><td>LGA</td><td>MSN</td><td>27.1179245</td><td>218</td></tr>
	<tr><td>LGA</td><td>ORF</td><td>16.5538462</td><td>206</td></tr>
	<tr><td>JFK</td><td>IAH</td><td>15.6176471</td><td>274</td></tr>
	<tr><td>JFK</td><td>MCI</td><td>23.0859375</td><td>276</td></tr>
	<tr><td>LGA</td><td>OMA</td><td>27.3695652</td><td> 95</td></tr>
	<tr><td>LGA</td><td>DSM</td><td>17.2222222</td><td>158</td></tr>
	<tr><td>LGA</td><td>GSP</td><td> 8.2346939</td><td>104</td></tr>
	<tr><td>JFK</td><td>ABQ</td><td>13.7401575</td><td>254</td></tr>
	<tr><td>LGA</td><td>ILM</td><td>19.4166667</td><td>110</td></tr>
	<tr><td>LGA</td><td>SYR</td><td>19.1107011</td><td>293</td></tr>
	<tr><td>JFK</td><td>MVY</td><td> 7.0516432</td><td>221</td></tr>
	<tr><td>LGA</td><td>SBN</td><td>31.3333333</td><td>  6</td></tr>
	<tr><td>JFK</td><td>STL</td><td>20.0000000</td><td>  1</td></tr>
	<tr><td>LGA</td><td>LEX</td><td>-9.0000000</td><td>  1</td></tr>
	<tr><td>EWR</td><td>SBN</td><td> 5.7500000</td><td>  4</td></tr>
	<tr><td>LGA</td><td>MHT</td><td>24.0370370</td><td>142</td></tr>
	<tr><td>LGA</td><td>CAE</td><td>29.5000000</td><td> 12</td></tr>
	<tr><td>JFK</td><td>JAC</td><td> 5.0000000</td><td>  2</td></tr>
	<tr><td>JFK</td><td>SDF</td><td>23.9767442</td><td> 46</td></tr>
	<tr><td>LGA</td><td>CHO</td><td>21.3913043</td><td> 52</td></tr>
	<tr><td>JFK</td><td>MKE</td><td>19.8604651</td><td>183</td></tr>
	<tr><td>LGA</td><td>AVL</td><td>-2.6000000</td><td> 10</td></tr>
	<tr><td>JFK</td><td>BHM</td><td> 7.0000000</td><td>  1</td></tr>
	<tr><td>LGA</td><td>TVC</td><td>23.4109589</td><td> 77</td></tr>
	<tr><td>LGA</td><td>MYR</td><td> 0.6666667</td><td>  3</td></tr>
	<tr><td>EWR</td><td>TVC</td><td>17.8695652</td><td> 24</td></tr>
	<tr><td>EWR</td><td>ANC</td><td>12.8750000</td><td>  8</td></tr>
	<tr><td>EWR</td><td>LGA</td><td>       NaN</td><td>  1</td></tr>
</tbody>
</table>



# Exercises
3.5.1. Which carrier has the worst average delays? Challenge: can you disentangle the effects of bad airports vs. bad carriers? Why/why not? (Hint: think about `flights |> group_by(carrier, dest) |> summarize(n())`)


3.5.2. Find the flights that are most delayed upon departure from each destination.

3.5.3. How do delays vary over the course of the day. Illustrate your answer with a plot.

3.5.4. What happens if you supply a negative n to slice_min() and friends?

3.5.5. Explain what count() does in terms of the dplyr verbs you just learned. What does the sort argument to count() do?

3.5.6. Suppose we have the following tiny data frame:


```R
df <- tibble(
  x = 1:5,
  y = c("a", "b", "a", "a", "b"),
  z = c("K", "K", "L", "L", "K")
)
```

a. Write down what you think the output will look like, then check if you were correct, and describe what group_by() does.


```R
df |>
  group_by(y)
```


<table class="dataframe">
<caption>A grouped_df: 5 x 3</caption>
<thead>
	<tr><th scope=col>x</th><th scope=col>y</th><th scope=col>z</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>a</td><td>K</td></tr>
	<tr><td>2</td><td>b</td><td>K</td></tr>
	<tr><td>3</td><td>a</td><td>L</td></tr>
	<tr><td>4</td><td>a</td><td>L</td></tr>
	<tr><td>5</td><td>b</td><td>K</td></tr>
</tbody>
</table>



b. Write down what you think the output will look like, then check if you were correct, and describe what arrange() does. Also comment on how it’s different from the group_by() in part (a)?


```R
df |>
  arrange(y)
```


<table class="dataframe">
<caption>A tibble: 5 x 3</caption>
<thead>
	<tr><th scope=col>x</th><th scope=col>y</th><th scope=col>z</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>a</td><td>K</td></tr>
	<tr><td>3</td><td>a</td><td>L</td></tr>
	<tr><td>4</td><td>a</td><td>L</td></tr>
	<tr><td>2</td><td>b</td><td>K</td></tr>
	<tr><td>5</td><td>b</td><td>K</td></tr>
</tbody>
</table>



c. Write down what you think the output will look like, then check if you were correct, and describe what the pipeline does.


```R
df |>
  group_by(y) |>
  summarize(mean_x = mean(x))
```


<table class="dataframe">
<caption>A tibble: 2 x 2</caption>
<thead>
	<tr><th scope=col>y</th><th scope=col>mean_x</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>a</td><td>2.666667</td></tr>
	<tr><td>b</td><td>3.500000</td></tr>
</tbody>
</table>



d. Write down what you think the output will look like, then check if you were correct, and describe what the pipeline does. Then, comment on what the message says.



```R
df |>
  group_by(y, z) |>
  summarize(mean_x = mean(x))
```

    [1m[22m`summarise()` has grouped output by 'y'. You can override using the `.groups`
    argument.



<table class="dataframe">
<caption>A grouped_df: 3 x 3</caption>
<thead>
	<tr><th scope=col>y</th><th scope=col>z</th><th scope=col>mean_x</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>a</td><td>K</td><td>1.0</td></tr>
	<tr><td>a</td><td>L</td><td>3.5</td></tr>
	<tr><td>b</td><td>K</td><td>3.5</td></tr>
</tbody>
</table>



e. Write down what you think the output will look like, then check if you were correct, and describe what the pipeline does. How is the output different from the one in part (d).


```R
df |>
  group_by(y, z) |>
  summarize(mean_x = mean(x), .groups = "drop")
```


<table class="dataframe">
<caption>A tibble: 3 x 3</caption>
<thead>
	<tr><th scope=col>y</th><th scope=col>z</th><th scope=col>mean_x</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>a</td><td>K</td><td>1.0</td></tr>
	<tr><td>a</td><td>L</td><td>3.5</td></tr>
	<tr><td>b</td><td>K</td><td>3.5</td></tr>
</tbody>
</table>



f. Write down what you think the outputs will look like, then check if you were correct, and describe what each pipeline does. How are the outputs of the two pipelines different?


```R
df |>
  group_by(y, z) |>
  summarize(mean_x = mean(x))
df |>
  group_by(y, z) |>
  mutate(mean_x = mean(x))
```

    [1m[22m`summarise()` has grouped output by 'y'. You can override using the `.groups`
    argument.



<table class="dataframe">
<caption>A grouped_df: 3 x 3</caption>
<thead>
	<tr><th scope=col>y</th><th scope=col>z</th><th scope=col>mean_x</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>a</td><td>K</td><td>1.0</td></tr>
	<tr><td>a</td><td>L</td><td>3.5</td></tr>
	<tr><td>b</td><td>K</td><td>3.5</td></tr>
</tbody>
</table>




<table class="dataframe">
<caption>A grouped_df: 5 x 4</caption>
<thead>
	<tr><th scope=col>x</th><th scope=col>y</th><th scope=col>z</th><th scope=col>mean_x</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>a</td><td>K</td><td>1.0</td></tr>
	<tr><td>2</td><td>b</td><td>K</td><td>3.5</td></tr>
	<tr><td>3</td><td>a</td><td>L</td><td>3.5</td></tr>
	<tr><td>4</td><td>a</td><td>L</td><td>3.5</td></tr>
	<tr><td>5</td><td>b</td><td>K</td><td>3.5</td></tr>
</tbody>
</table>



## Case study: aggregates and sample size
Whenever you do any aggregation, it’s always a good idea to include a count (`n()`). That way, you can ensure that you’re not drawing conclusions based on very small amounts of data. We’ll demonstrate this with some baseball data from the **Lahman** package. Specifically, we will compare what proportion of times a player gets a hit (`H`) vs. the number of times they try to put the ball in play (`AB`):




```R
batters <- Lahman::Batting |> 
  group_by(playerID) |> 
  summarize(
    performance = sum(H, na.rm = TRUE) / sum(AB, na.rm = TRUE),
    n = sum(AB, na.rm = TRUE)
  )
batters
```


<table class="dataframe">
<caption>A tibble: 20469 x 3</caption>
<thead>
	<tr><th scope=col>playerID</th><th scope=col>performance</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>aardsda01</td><td>0.00000000</td><td>    4</td></tr>
	<tr><td>aaronha01</td><td>0.30499838</td><td>12364</td></tr>
	<tr><td>aaronto01</td><td>0.22881356</td><td>  944</td></tr>
	<tr><td>aasedo01 </td><td>0.00000000</td><td>    5</td></tr>
	<tr><td>abadan01 </td><td>0.09523810</td><td>   21</td></tr>
	<tr><td>abadfe01 </td><td>0.11111111</td><td>    9</td></tr>
	<tr><td>abadijo01</td><td>0.22448980</td><td>   49</td></tr>
	<tr><td>abbated01</td><td>0.25361367</td><td> 3044</td></tr>
	<tr><td>abbeybe01</td><td>0.16888889</td><td>  225</td></tr>
	<tr><td>abbeych01</td><td>0.28075171</td><td> 1756</td></tr>
	<tr><td>abbotco01</td><td>0.33333333</td><td>    3</td></tr>
	<tr><td>abbotda01</td><td>0.14285714</td><td>    7</td></tr>
	<tr><td>abbotfr01</td><td>0.20857700</td><td>  513</td></tr>
	<tr><td>abbotgl01</td><td>       NaN</td><td>    0</td></tr>
	<tr><td>abbotje01</td><td>0.26342282</td><td>  596</td></tr>
	<tr><td>abbotji01</td><td>0.09523810</td><td>   21</td></tr>
	<tr><td>abbotku01</td><td>0.25587084</td><td> 2044</td></tr>
	<tr><td>abbotky01</td><td>0.09677419</td><td>   31</td></tr>
	<tr><td>abbotod01</td><td>0.18571429</td><td>   70</td></tr>
	<tr><td>abbotpa01</td><td>0.25000000</td><td>   20</td></tr>
	<tr><td>aberal01 </td><td>0.14000000</td><td>  100</td></tr>
	<tr><td>abercda01</td><td>0.00000000</td><td>    4</td></tr>
	<tr><td>abercre01</td><td>0.22279793</td><td>  386</td></tr>
	<tr><td>abernbi01</td><td>0.00000000</td><td>    1</td></tr>
	<tr><td>abernbr01</td><td>0.24423963</td><td>  868</td></tr>
	<tr><td>abernte01</td><td>0.20000000</td><td>    5</td></tr>
	<tr><td>abernte02</td><td>0.13812155</td><td>  181</td></tr>
	<tr><td>abernwo01</td><td>0.00000000</td><td>    8</td></tr>
	<tr><td>aberscl01</td><td>0.25139665</td><td>  179</td></tr>
	<tr><td>ablesha01</td><td>0.00000000</td><td>   26</td></tr>
	<tr><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>zimmero01</td><td>0.27551020</td><td>  98</td></tr>
	<tr><td>zimmery01</td><td>0.27742711</td><td>6654</td></tr>
	<tr><td>zinkch01 </td><td>       NaN</td><td>   0</td></tr>
	<tr><td>zinkwa01 </td><td>0.00000000</td><td>   1</td></tr>
	<tr><td>zinnfr01 </td><td>0.00000000</td><td>   7</td></tr>
	<tr><td>zinngu01 </td><td>0.26926564</td><td>1103</td></tr>
	<tr><td>zinnji01 </td><td>0.28333333</td><td> 120</td></tr>
	<tr><td>zinsebi01</td><td>       NaN</td><td>   0</td></tr>
	<tr><td>zinteal01</td><td>0.16666667</td><td>  78</td></tr>
	<tr><td>zipfebu01</td><td>0.22033898</td><td> 354</td></tr>
	<tr><td>ziskri01 </td><td>0.28713064</td><td>5144</td></tr>
	<tr><td>zitoba01 </td><td>0.10174419</td><td> 344</td></tr>
	<tr><td>zitzmbi01</td><td>0.26693227</td><td>1004</td></tr>
	<tr><td>zmiched01</td><td>0.05882353</td><td>  17</td></tr>
	<tr><td>zobribe01</td><td>0.26632653</td><td>5880</td></tr>
	<tr><td>zoccope01</td><td>0.10810811</td><td>  37</td></tr>
	<tr><td>zoldasa01</td><td>0.17482517</td><td> 286</td></tr>
	<tr><td>zoskyed01</td><td>0.16000000</td><td>  50</td></tr>
	<tr><td>zuberbi01</td><td>0.13537118</td><td> 229</td></tr>
	<tr><td>zuberjo01</td><td>0.25000000</td><td> 136</td></tr>
	<tr><td>zuberty01</td><td>0.00000000</td><td>   1</td></tr>
	<tr><td>zuletju01</td><td>0.24712644</td><td> 174</td></tr>
	<tr><td>zumayjo01</td><td>       NaN</td><td>   0</td></tr>
	<tr><td>zuninmi01</td><td>0.20007479</td><td>2674</td></tr>
	<tr><td>zupcibo01</td><td>0.25031447</td><td> 795</td></tr>
	<tr><td>zupofr01 </td><td>0.16666667</td><td>  18</td></tr>
	<tr><td>zuvelpa01</td><td>0.22199593</td><td> 491</td></tr>
	<tr><td>zuverge01</td><td>0.14788732</td><td> 142</td></tr>
	<tr><td>zwilldu01</td><td>0.28437500</td><td>1280</td></tr>
	<tr><td>zychto01 </td><td>       NaN</td><td>   0</td></tr>
</tbody>
</table>




```R
batters |> 
  filter(n > 100) |> 
  ggplot(aes(x = n, y = performance)) +
  geom_point(alpha = 1 / 10) + 
  geom_smooth(se = FALSE)
```

    [1m[22m`geom_smooth()` using method = 'gam' and formula = 'y ~ s(x, bs = "cs")'



    
![png](R4DS_Workflow_files/R4DS_Workflow_109_1.png)
    



```R
batters |> 
  arrange(desc(performance))
```


<table class="dataframe">
<caption>A tibble: 20469 x 3</caption>
<thead>
	<tr><th scope=col>playerID</th><th scope=col>performance</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>abramge01</td><td>1</td><td>1</td></tr>
	<tr><td>alberan01</td><td>1</td><td>1</td></tr>
	<tr><td>banisje01</td><td>1</td><td>1</td></tr>
	<tr><td>bartocl01</td><td>1</td><td>1</td></tr>
	<tr><td>bassdo01 </td><td>1</td><td>1</td></tr>
	<tr><td>birasst01</td><td>1</td><td>2</td></tr>
	<tr><td>bruneju01</td><td>1</td><td>1</td></tr>
	<tr><td>burnscb01</td><td>1</td><td>1</td></tr>
	<tr><td>cammaer01</td><td>1</td><td>1</td></tr>
	<tr><td>campsh01 </td><td>1</td><td>1</td></tr>
	<tr><td>crockcl01</td><td>1</td><td>1</td></tr>
	<tr><td>davenjo01</td><td>1</td><td>1</td></tr>
	<tr><td>davidda01</td><td>1</td><td>1</td></tr>
	<tr><td>devinha01</td><td>1</td><td>2</td></tr>
	<tr><td>dupremi01</td><td>1</td><td>1</td></tr>
	<tr><td>eddydo01 </td><td>1</td><td>1</td></tr>
	<tr><td>egeco01  </td><td>1</td><td>1</td></tr>
	<tr><td>eubanue01</td><td>1</td><td>1</td></tr>
	<tr><td>fryjo01  </td><td>1</td><td>1</td></tr>
	<tr><td>gallaja01</td><td>1</td><td>1</td></tr>
	<tr><td>garcimi02</td><td>1</td><td>1</td></tr>
	<tr><td>garcira01</td><td>1</td><td>1</td></tr>
	<tr><td>gideobr01</td><td>1</td><td>1</td></tr>
	<tr><td>gleasro01</td><td>1</td><td>1</td></tr>
	<tr><td>gowella01</td><td>1</td><td>1</td></tr>
	<tr><td>grasmlo01</td><td>1</td><td>1</td></tr>
	<tr><td>grayda01 </td><td>1</td><td>1</td></tr>
	<tr><td>hancory01</td><td>1</td><td>1</td></tr>
	<tr><td>hesslke01</td><td>1</td><td>1</td></tr>
	<tr><td>holloji01</td><td>1</td><td>1</td></tr>
	<tr><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>yardler01</td><td>NaN</td><td>0</td></tr>
	<tr><td>yarnaed01</td><td>NaN</td><td>0</td></tr>
	<tr><td>yeabsbe01</td><td>NaN</td><td>0</td></tr>
	<tr><td>yettri01 </td><td>NaN</td><td>0</td></tr>
	<tr><td>ynoami01 </td><td>NaN</td><td>0</td></tr>
	<tr><td>yochira01</td><td>NaN</td><td>0</td></tr>
	<tr><td>youngcl01</td><td>NaN</td><td>0</td></tr>
	<tr><td>youngda01</td><td>NaN</td><td>0</td></tr>
	<tr><td>youngda02</td><td>NaN</td><td>0</td></tr>
	<tr><td>youngki01</td><td>NaN</td><td>0</td></tr>
	<tr><td>youngma03</td><td>NaN</td><td>0</td></tr>
	<tr><td>youngti01</td><td>NaN</td><td>0</td></tr>
	<tr><td>yountla01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zabalan01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zagurmi01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zamorda01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zaratma01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zaskeje01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zavadcl01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zavarcl01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zelleba01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zerpaan01</td><td>NaN</td><td>0</td></tr>
	<tr><td>ziemst01 </td><td>NaN</td><td>0</td></tr>
	<tr><td>zimmeje02</td><td>NaN</td><td>0</td></tr>
	<tr><td>zimmejo01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zimmeky01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zinkch01 </td><td>NaN</td><td>0</td></tr>
	<tr><td>zinsebi01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zumayjo01</td><td>NaN</td><td>0</td></tr>
	<tr><td>zychto01 </td><td>NaN</td><td>0</td></tr>
</tbody>
</table>



## Summary

In this chapter, you’ve learned the tools that dplyr provides for working with data frames. The tools are roughly grouped into three categories: those that manipulate the rows (like `filter()` and `arrange()`), those that manipulate the columns (like `select()` and `mutate()`), and those that manipulate groups (like group_by() and summarize()). In this chapter, we’ve focused on these “*whole data frame*” tools, but you haven’t yet learned much about what you can do with the *individual variable*. 
