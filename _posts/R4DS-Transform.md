# C12. Logical Vectors


```R
library(tidyverse)
library(nycflights13)
library(dplyr)
```

## 12.2. Comparisions


```R
x <- c(1, 2, 3, 5, 7, 11, 13)
x * 2

df <- tibble(x)
df |> 
  mutate(y = x * 2)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>2</li><li>4</li><li>6</li><li>10</li><li>14</li><li>22</li><li>26</li></ol>




<table class="dataframe">
<caption>A tibble: 7 x 2</caption>
<thead>
	<tr><th scope=col>x</th><th scope=col>y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td> 1</td><td> 2</td></tr>
	<tr><td> 2</td><td> 4</td></tr>
	<tr><td> 3</td><td> 6</td></tr>
	<tr><td> 5</td><td>10</td></tr>
	<tr><td> 7</td><td>14</td></tr>
	<tr><td>11</td><td>22</td></tr>
	<tr><td>13</td><td>26</td></tr>
</tbody>
</table>




```R
flights |> 
  mutate(
    daytime = dep_time > 600 & dep_time < 2000,
    approx_ontime = abs(arr_delay) < 20,
    .keep = "used"
  )
```


<table class="dataframe">
<caption>A tibble: 336776 x 4</caption>
<thead>
	<tr><th scope=col>dep_time</th><th scope=col>arr_delay</th><th scope=col>daytime</th><th scope=col>approx_ontime</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;lgl&gt;</th><th scope=col>&lt;lgl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>517</td><td> 11</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>533</td><td> 20</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>542</td><td> 33</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>544</td><td>-18</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>554</td><td>-25</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>554</td><td> 12</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>555</td><td> 19</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>557</td><td>-14</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>557</td><td> -8</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>558</td><td>  8</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>558</td><td> -2</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>558</td><td> -3</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>558</td><td>  7</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>558</td><td>-14</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>559</td><td> 31</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>559</td><td> -4</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>559</td><td> -8</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>600</td><td> -7</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>600</td><td> 12</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>601</td><td> -6</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>602</td><td> -8</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>602</td><td> 16</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>606</td><td>-12</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>606</td><td> -8</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>607</td><td>-17</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>608</td><td> 32</td><td> TRUE</td><td>FALSE</td></tr>
	<tr><td>611</td><td> 14</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>613</td><td>  4</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>615</td><td>-21</td><td> TRUE</td><td>FALSE</td></tr>
	<tr><td>615</td><td> -9</td><td> TRUE</td><td> TRUE</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2123</td><td>-24</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2127</td><td> -9</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2128</td><td>-31</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2129</td><td> -2</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2131</td><td>-30</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2140</td><td>-30</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2142</td><td> 11</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2145</td><td>-25</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2147</td><td>  3</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2149</td><td>-23</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2150</td><td>-16</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2159</td><td>194</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2203</td><td>  8</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2207</td><td>  7</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2211</td><td> 57</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2231</td><td>-21</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2233</td><td> 42</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2235</td><td>130</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2237</td><td> -8</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2240</td><td>-17</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2240</td><td>-20</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>2241</td><td>-16</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2307</td><td>  1</td><td>FALSE</td><td> TRUE</td></tr>
	<tr><td>2349</td><td>-25</td><td>FALSE</td><td>FALSE</td></tr>
	<tr><td>  NA</td><td> NA</td><td>   NA</td><td>   NA</td></tr>
	<tr><td>  NA</td><td> NA</td><td>   NA</td><td>   NA</td></tr>
	<tr><td>  NA</td><td> NA</td><td>   NA</td><td>   NA</td></tr>
	<tr><td>  NA</td><td> NA</td><td>   NA</td><td>   NA</td></tr>
	<tr><td>  NA</td><td> NA</td><td>   NA</td><td>   NA</td></tr>
	<tr><td>  NA</td><td> NA</td><td>   NA</td><td>   NA</td></tr>
</tbody>
</table>




```R
flights |> 
  mutate(
    daytime = dep_time > 600 & dep_time < 2000,
    approx_ontime = abs(arr_delay) < 20,
  ) |> 
  filter(daytime & approx_ontime)
```


<table class="dataframe">
<caption>A tibble: 172286 x 21</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>...</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th><th scope=col>daytime</th><th scope=col>approx_ontime</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>...</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;lgl&gt;</th><th scope=col>&lt;lgl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td>...</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>...</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>...</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>...</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>...</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>...</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td>...</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td>...</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td>...</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>622</td><td>630</td><td>-8</td><td>1017</td><td>1014</td><td>  3</td><td>US</td><td>...</td><td>N807AW</td><td>EWR</td><td>PHX</td><td>342</td><td>2133</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>623</td><td>610</td><td>13</td><td> 920</td><td> 915</td><td>  5</td><td>AA</td><td>...</td><td>N3EMAA</td><td>LGA</td><td>MIA</td><td>153</td><td>1096</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>623</td><td>627</td><td>-4</td><td> 933</td><td> 932</td><td>  1</td><td>UA</td><td>...</td><td>N459UA</td><td>LGA</td><td>IAH</td><td>229</td><td>1416</td><td>6</td><td>27</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>624</td><td>630</td><td>-6</td><td> 840</td><td> 830</td><td> 10</td><td>MQ</td><td>...</td><td>N518MQ</td><td>LGA</td><td>MSP</td><td>166</td><td>1020</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>627</td><td>630</td><td>-3</td><td>1018</td><td>1018</td><td>  0</td><td>US</td><td>...</td><td>N535UW</td><td>JFK</td><td>PHX</td><td>330</td><td>2153</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>628</td><td>630</td><td>-2</td><td>1137</td><td>1140</td><td> -3</td><td>AA</td><td>...</td><td>N3BAAA</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>629</td><td>630</td><td>-1</td><td> 824</td><td> 810</td><td> 14</td><td>AA</td><td>...</td><td>N3CYAA</td><td>LGA</td><td>ORD</td><td>140</td><td> 733</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>629</td><td>630</td><td>-1</td><td> 721</td><td> 740</td><td>-19</td><td>WN</td><td>...</td><td>N273WN</td><td>LGA</td><td>BWI</td><td> 40</td><td> 185</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>629</td><td>630</td><td>-1</td><td> 824</td><td> 833</td><td> -9</td><td>US</td><td>...</td><td>N426US</td><td>EWR</td><td>CLT</td><td> 91</td><td> 529</td><td>6</td><td>30</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>632</td><td>608</td><td>24</td><td> 740</td><td> 728</td><td> 12</td><td>EV</td><td>...</td><td>N13553</td><td>EWR</td><td>IAD</td><td> 52</td><td> 212</td><td>6</td><td> 8</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>637</td><td>645</td><td>-8</td><td> 930</td><td> 935</td><td> -5</td><td>B6</td><td>...</td><td>N709JB</td><td>LGA</td><td>MCO</td><td>144</td><td> 950</td><td>6</td><td>45</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>639</td><td>640</td><td>-1</td><td> 739</td><td> 749</td><td>-10</td><td>B6</td><td>...</td><td>N805JB</td><td>JFK</td><td>BOS</td><td> 41</td><td> 187</td><td>6</td><td>40</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>643</td><td>646</td><td>-3</td><td> 922</td><td> 940</td><td>-18</td><td>UA</td><td>...</td><td>N497UA</td><td>EWR</td><td>PBI</td><td>146</td><td>1023</td><td>6</td><td>46</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>643</td><td>645</td><td>-2</td><td> 837</td><td> 848</td><td>-11</td><td>US</td><td>...</td><td>N178US</td><td>EWR</td><td>CLT</td><td> 91</td><td> 529</td><td>6</td><td>45</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>644</td><td>636</td><td> 8</td><td> 931</td><td> 940</td><td> -9</td><td>UA</td><td>...</td><td>N75435</td><td>EWR</td><td>FLL</td><td>151</td><td>1065</td><td>6</td><td>36</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>645</td><td>647</td><td>-2</td><td> 815</td><td> 810</td><td>  5</td><td>B6</td><td>...</td><td>N796JB</td><td>JFK</td><td>BUF</td><td> 63</td><td> 301</td><td>6</td><td>47</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>646</td><td>645</td><td> 1</td><td> 910</td><td> 916</td><td> -6</td><td>UA</td><td>...</td><td>N569UA</td><td>LGA</td><td>DEN</td><td>243</td><td>1620</td><td>6</td><td>45</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>646</td><td>645</td><td> 1</td><td>1023</td><td>1030</td><td> -7</td><td>UA</td><td>...</td><td>N38727</td><td>EWR</td><td>SNA</td><td>380</td><td>2434</td><td>6</td><td>45</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>651</td><td>655</td><td>-4</td><td> 936</td><td> 942</td><td> -6</td><td>B6</td><td>...</td><td>N558JB</td><td>JFK</td><td>LAS</td><td>323</td><td>2248</td><td>6</td><td>55</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>652</td><td>655</td><td>-3</td><td> 932</td><td> 921</td><td> 11</td><td>B6</td><td>...</td><td>N178JB</td><td>JFK</td><td>MSY</td><td>191</td><td>1182</td><td>6</td><td>55</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>655</td><td>655</td><td> 0</td><td>1021</td><td>1030</td><td> -9</td><td>DL</td><td>...</td><td>N3763D</td><td>JFK</td><td>SLC</td><td>294</td><td>1990</td><td>6</td><td>55</td><td>2013-01-01 06:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td></td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1908</td><td>1911</td><td> -3</td><td>2107</td><td>2110</td><td> -3</td><td>EV</td><td>...</td><td>N16987</td><td>EWR</td><td>CLT</td><td> 74</td><td> 529</td><td>19</td><td>11</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1909</td><td>1905</td><td>  4</td><td>2055</td><td>2057</td><td> -2</td><td>9E</td><td>...</td><td>N937XJ</td><td>JFK</td><td>ORD</td><td>108</td><td> 740</td><td>19</td><td> 5</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1909</td><td>1901</td><td>  8</td><td>2212</td><td>2211</td><td>  1</td><td>UA</td><td>...</td><td>N513UA</td><td>EWR</td><td>SFO</td><td>307</td><td>2565</td><td>19</td><td> 1</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1915</td><td>1900</td><td> 15</td><td>2138</td><td>2151</td><td>-13</td><td>B6</td><td>...</td><td>N563JB</td><td>JFK</td><td>MCO</td><td>120</td><td> 944</td><td>19</td><td> 0</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1915</td><td>1900</td><td> 15</td><td>2025</td><td>2015</td><td> 10</td><td>WN</td><td>...</td><td>N719SW</td><td>LGA</td><td>MKE</td><td>104</td><td> 738</td><td>19</td><td> 0</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1917</td><td>1920</td><td> -3</td><td>2053</td><td>2055</td><td> -2</td><td>9E</td><td>...</td><td>N600LR</td><td>LGA</td><td>BUF</td><td> 50</td><td> 292</td><td>19</td><td>20</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1925</td><td>1930</td><td> -5</td><td>2033</td><td>2049</td><td>-16</td><td>EV</td><td>...</td><td>N825AS</td><td>LGA</td><td>IAD</td><td> 43</td><td> 229</td><td>19</td><td>30</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1926</td><td>1930</td><td> -4</td><td>2146</td><td>2201</td><td>-15</td><td>DL</td><td>...</td><td>N303DQ</td><td>EWR</td><td>ATL</td><td> 95</td><td> 746</td><td>19</td><td>30</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1927</td><td>1930</td><td> -3</td><td>2054</td><td>2056</td><td> -2</td><td>EV</td><td>...</td><td>N13956</td><td>EWR</td><td>MKE</td><td>110</td><td> 725</td><td>19</td><td>30</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1928</td><td>1932</td><td> -4</td><td>2137</td><td>2143</td><td> -6</td><td>EV</td><td>...</td><td>N18556</td><td>EWR</td><td>TYS</td><td> 82</td><td> 631</td><td>19</td><td>32</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1929</td><td>1934</td><td> -5</td><td>2146</td><td>2136</td><td> 10</td><td>EV</td><td>...</td><td>N18557</td><td>EWR</td><td>CHS</td><td> 92</td><td> 628</td><td>19</td><td>34</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1930</td><td>1930</td><td>  0</td><td>2217</td><td>2231</td><td>-14</td><td>DL</td><td>...</td><td>N365NB</td><td>LGA</td><td>TPA</td><td>133</td><td>1010</td><td>19</td><td>30</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1930</td><td>1940</td><td>-10</td><td>2120</td><td>2125</td><td> -5</td><td>MQ</td><td>...</td><td>N839MQ</td><td>JFK</td><td>RDU</td><td> 70</td><td> 427</td><td>19</td><td>40</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1931</td><td>1905</td><td> 26</td><td>2049</td><td>2033</td><td> 16</td><td>EV</td><td>...</td><td>N748EV</td><td>LGA</td><td>ROC</td><td> 41</td><td> 254</td><td>19</td><td> 5</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1932</td><td>1935</td><td> -3</td><td>2221</td><td>2232</td><td>-11</td><td>DL</td><td>...</td><td>N927DA</td><td>LGA</td><td>MCO</td><td>132</td><td> 950</td><td>19</td><td>35</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1934</td><td>1930</td><td>  4</td><td>2236</td><td>2250</td><td>-14</td><td>AA</td><td>...</td><td>N3EXAA</td><td>JFK</td><td>SEA</td><td>340</td><td>2422</td><td>19</td><td>30</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1934</td><td>1935</td><td> -1</td><td>2238</td><td>2250</td><td>-12</td><td>AA</td><td>...</td><td>N3JFAA</td><td>LGA</td><td>MIA</td><td>150</td><td>1096</td><td>19</td><td>35</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1935</td><td>1935</td><td>  0</td><td>2211</td><td>2229</td><td>-18</td><td>B6</td><td>...</td><td>N589JB</td><td>JFK</td><td>TPA</td><td>132</td><td>1005</td><td>19</td><td>35</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1935</td><td>1930</td><td>  5</td><td>2230</td><td>2233</td><td> -3</td><td>UA</td><td>...</td><td>N38446</td><td>EWR</td><td>TPA</td><td>132</td><td> 997</td><td>19</td><td>30</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1936</td><td>1910</td><td> 26</td><td>2204</td><td>2203</td><td>  1</td><td>DL</td><td>...</td><td>N905DL</td><td>JFK</td><td>MCO</td><td>126</td><td> 944</td><td>19</td><td>10</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1939</td><td>1940</td><td> -1</td><td>2041</td><td>2100</td><td>-19</td><td>EV</td><td>...</td><td>N829AS</td><td>JFK</td><td>IAD</td><td> 42</td><td> 228</td><td>19</td><td>40</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1939</td><td>1950</td><td>-11</td><td>2129</td><td>2140</td><td>-11</td><td>MQ</td><td>...</td><td>N735MQ</td><td>LGA</td><td>CMH</td><td> 73</td><td> 479</td><td>19</td><td>50</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1940</td><td>1900</td><td> 40</td><td>2228</td><td>2232</td><td> -4</td><td>DL</td><td>...</td><td>N723TW</td><td>JFK</td><td>SFO</td><td>323</td><td>2586</td><td>19</td><td> 0</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1944</td><td>1950</td><td> -6</td><td>2208</td><td>2215</td><td> -7</td><td>MQ</td><td>...</td><td>N507MQ</td><td>LGA</td><td>ATL</td><td>100</td><td> 762</td><td>19</td><td>50</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1953</td><td>2000</td><td> -7</td><td>2119</td><td>2132</td><td>-13</td><td>UA</td><td>...</td><td>N853UA</td><td>LGA</td><td>ORD</td><td>107</td><td> 733</td><td>20</td><td> 0</td><td>2013-09-30 20:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1955</td><td>2000</td><td> -5</td><td>2219</td><td>2230</td><td>-11</td><td>DL</td><td>...</td><td>N992DL</td><td>LGA</td><td>ATL</td><td> 99</td><td> 762</td><td>20</td><td> 0</td><td>2013-09-30 20:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1955</td><td>1935</td><td> 20</td><td>2141</td><td>2159</td><td>-18</td><td>9E</td><td>...</td><td>N928XJ</td><td>JFK</td><td>CVG</td><td> 86</td><td> 589</td><td>19</td><td>35</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1955</td><td>1942</td><td> 13</td><td>2300</td><td>2250</td><td> 10</td><td>B6</td><td>...</td><td>N623JB</td><td>LGA</td><td>FLL</td><td>141</td><td>1076</td><td>19</td><td>42</td><td>2013-09-30 19:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1955</td><td>2000</td><td> -5</td><td>2112</td><td>2114</td><td> -2</td><td>US</td><td>...</td><td>N957UW</td><td>LGA</td><td>BOS</td><td> 35</td><td> 184</td><td>20</td><td> 0</td><td>2013-09-30 20:00:00</td><td>TRUE</td><td>TRUE</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>1958</td><td>2005</td><td> -7</td><td>2119</td><td>2130</td><td>-11</td><td>MQ</td><td>...</td><td>N511MQ</td><td>EWR</td><td>ORD</td><td>102</td><td> 719</td><td>20</td><td> 5</td><td>2013-09-30 20:00:00</td><td>TRUE</td><td>TRUE</td></tr>
</tbody>
</table>



### Floating point comparision


```R
x <- c(1 / 49 * 49, sqrt(2) ^ 2)
x
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>2</li></ol>




```R
x == c(1, 2)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>FALSE</li><li>FALSE</li></ol>




```R
print(x, digits = 16)
```

    [1] 0.9999999999999999 2.0000000000000004



```R
near(x, c(1, 2))
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>TRUE</li><li>TRUE</li></ol>



### Missing values


```R
NA > 5
10 == NA

NA == NA
```


&lt;NA&gt;



&lt;NA&gt;



&lt;NA&gt;



```R
# so this code doesn't work
flights |> 
  filter(dep_time == NA)
```


<table class="dataframe">
<caption>A tibble: 0 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>



### `is.na()`


```R
flights |> 
  filter(is.na(dep_time))
```


<table class="dataframe">
<caption>A tibble: 8255 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>NA</td><td>1630</td><td>NA</td><td>NA</td><td>1815</td><td>NA</td><td>EV</td><td>4308</td><td>N18120</td><td>EWR</td><td>RDU</td><td>NA</td><td> 416</td><td>16</td><td>30</td><td>2013-01-01 16:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>NA</td><td>1935</td><td>NA</td><td>NA</td><td>2240</td><td>NA</td><td>AA</td><td> 791</td><td>N3EHAA</td><td>LGA</td><td>DFW</td><td>NA</td><td>1389</td><td>19</td><td>35</td><td>2013-01-01 19:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>NA</td><td>1500</td><td>NA</td><td>NA</td><td>1825</td><td>NA</td><td>AA</td><td>1925</td><td>N3EVAA</td><td>LGA</td><td>MIA</td><td>NA</td><td>1096</td><td>15</td><td> 0</td><td>2013-01-01 15:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>NA</td><td> 600</td><td>NA</td><td>NA</td><td> 901</td><td>NA</td><td>B6</td><td> 125</td><td>N618JB</td><td>JFK</td><td>FLL</td><td>NA</td><td>1069</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1540</td><td>NA</td><td>NA</td><td>1747</td><td>NA</td><td>EV</td><td>4352</td><td>N10575</td><td>EWR</td><td>CVG</td><td>NA</td><td> 569</td><td>15</td><td>40</td><td>2013-01-02 15:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1620</td><td>NA</td><td>NA</td><td>1746</td><td>NA</td><td>EV</td><td>4406</td><td>N13949</td><td>EWR</td><td>PIT</td><td>NA</td><td> 319</td><td>16</td><td>20</td><td>2013-01-02 16:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1355</td><td>NA</td><td>NA</td><td>1459</td><td>NA</td><td>EV</td><td>4434</td><td>N10575</td><td>EWR</td><td>MHT</td><td>NA</td><td> 209</td><td>13</td><td>55</td><td>2013-01-02 13:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1420</td><td>NA</td><td>NA</td><td>1644</td><td>NA</td><td>EV</td><td>4935</td><td>N759EV</td><td>EWR</td><td>ATL</td><td>NA</td><td> 746</td><td>14</td><td>20</td><td>2013-01-02 14:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1321</td><td>NA</td><td>NA</td><td>1536</td><td>NA</td><td>EV</td><td>3849</td><td>N13550</td><td>EWR</td><td>IND</td><td>NA</td><td> 645</td><td>13</td><td>21</td><td>2013-01-02 13:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1545</td><td>NA</td><td>NA</td><td>1910</td><td>NA</td><td>AA</td><td> 133</td><td>NA    </td><td>JFK</td><td>LAX</td><td>NA</td><td>2475</td><td>15</td><td>45</td><td>2013-01-02 15:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1330</td><td>NA</td><td>NA</td><td>1640</td><td>NA</td><td>AA</td><td> 753</td><td>N3FBAA</td><td>LGA</td><td>DFW</td><td>NA</td><td>1389</td><td>13</td><td>30</td><td>2013-01-02 13:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>2</td><td>NA</td><td>1601</td><td>NA</td><td>NA</td><td>1735</td><td>NA</td><td>UA</td><td> 623</td><td>NA    </td><td>EWR</td><td>ORD</td><td>NA</td><td> 719</td><td>16</td><td> 1</td><td>2013-01-02 16:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td> 645</td><td>NA</td><td>NA</td><td> 757</td><td>NA</td><td>EV</td><td>4241</td><td>N14972</td><td>EWR</td><td>DCA</td><td>NA</td><td> 199</td><td> 6</td><td>45</td><td>2013-01-03 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td>1030</td><td>NA</td><td>NA</td><td>1210</td><td>NA</td><td>AA</td><td> 321</td><td>N487AA</td><td>LGA</td><td>ORD</td><td>NA</td><td> 733</td><td>10</td><td>30</td><td>2013-01-03 10:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td>1125</td><td>NA</td><td>NA</td><td>1305</td><td>NA</td><td>AA</td><td> 327</td><td>N3AMAA</td><td>LGA</td><td>ORD</td><td>NA</td><td> 733</td><td>11</td><td>25</td><td>2013-01-03 11:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td> 835</td><td>NA</td><td>NA</td><td>1150</td><td>NA</td><td>AA</td><td> 717</td><td>N3GXAA</td><td>LGA</td><td>DFW</td><td>NA</td><td>1389</td><td> 8</td><td>35</td><td>2013-01-03 08:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td> 920</td><td>NA</td><td>NA</td><td>1245</td><td>NA</td><td>AA</td><td> 721</td><td>N201AA</td><td>LGA</td><td>DFW</td><td>NA</td><td>1389</td><td> 9</td><td>20</td><td>2013-01-03 09:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td>1020</td><td>NA</td><td>NA</td><td>1330</td><td>NA</td><td>AA</td><td> 731</td><td>N3FVAA</td><td>LGA</td><td>DFW</td><td>NA</td><td>1389</td><td>10</td><td>20</td><td>2013-01-03 10:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td>1220</td><td>NA</td><td>NA</td><td>1415</td><td>NA</td><td>AA</td><td>1757</td><td>N573AA</td><td>LGA</td><td>STL</td><td>NA</td><td> 888</td><td>12</td><td>20</td><td>2013-01-03 12:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td> 630</td><td>NA</td><td>NA</td><td> 830</td><td>NA</td><td>MQ</td><td>4599</td><td>N500MQ</td><td>LGA</td><td>MSP</td><td>NA</td><td>1020</td><td> 6</td><td>30</td><td>2013-01-03 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td> 857</td><td>NA</td><td>NA</td><td>1209</td><td>NA</td><td>UA</td><td> 714</td><td>NA    </td><td>EWR</td><td>MIA</td><td>NA</td><td>1085</td><td> 8</td><td>57</td><td>2013-01-03 08:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>3</td><td>NA</td><td> 645</td><td>NA</td><td>NA</td><td> 952</td><td>NA</td><td>UA</td><td> 719</td><td>NA    </td><td>EWR</td><td>DFW</td><td>NA</td><td>1372</td><td> 6</td><td>45</td><td>2013-01-03 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>4</td><td>NA</td><td> 845</td><td>NA</td><td>NA</td><td>1015</td><td>NA</td><td>9E</td><td>3405</td><td>NA    </td><td>JFK</td><td>DCA</td><td>NA</td><td> 213</td><td> 8</td><td>45</td><td>2013-01-04 08:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>4</td><td>NA</td><td>1830</td><td>NA</td><td>NA</td><td>2044</td><td>NA</td><td>9E</td><td>3716</td><td>NA    </td><td>EWR</td><td>DTW</td><td>NA</td><td> 488</td><td>18</td><td>30</td><td>2013-01-04 18:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>4</td><td>NA</td><td> 920</td><td>NA</td><td>NA</td><td>1245</td><td>NA</td><td>AA</td><td> 721</td><td>N541AA</td><td>LGA</td><td>DFW</td><td>NA</td><td>1389</td><td> 9</td><td>20</td><td>2013-01-04 09:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>4</td><td>NA</td><td>1245</td><td>NA</td><td>NA</td><td>1550</td><td>NA</td><td>AA</td><td> 745</td><td>N3BGAA</td><td>LGA</td><td>DFW</td><td>NA</td><td>1389</td><td>12</td><td>45</td><td>2013-01-04 12:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>4</td><td>NA</td><td>1430</td><td>NA</td><td>NA</td><td>1735</td><td>NA</td><td>AA</td><td> 883</td><td>N200AA</td><td>EWR</td><td>DFW</td><td>NA</td><td>1372</td><td>14</td><td>30</td><td>2013-01-04 14:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>4</td><td>NA</td><td>1530</td><td>NA</td><td>NA</td><td>1725</td><td>NA</td><td>AA</td><td>2223</td><td>N569AA</td><td>LGA</td><td>STL</td><td>NA</td><td> 888</td><td>15</td><td>30</td><td>2013-01-04 15:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>5</td><td>NA</td><td>1400</td><td>NA</td><td>NA</td><td>1518</td><td>NA</td><td>EV</td><td>5712</td><td>N827AS</td><td>JFK</td><td>IAD</td><td>NA</td><td> 228</td><td>14</td><td> 0</td><td>2013-01-05 14:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>5</td><td>NA</td><td> 840</td><td>NA</td><td>NA</td><td>1001</td><td>NA</td><td>9E</td><td>3422</td><td>NA    </td><td>JFK</td><td>BOS</td><td>NA</td><td> 187</td><td> 8</td><td>40</td><td>2013-01-05 08:00:00</td></tr>
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




```R
flights |> 
  filter(month == 1, day == 1) |> 
  arrange(desc(is.na(dep_time)), dep_time)
```


<table class="dataframe">
<caption>A tibble: 842 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td> NA</td><td>1630</td><td>NA</td><td>  NA</td><td>1815</td><td> NA</td><td>EV</td><td>4308</td><td>N18120</td><td>EWR</td><td>RDU</td><td> NA</td><td> 416</td><td>16</td><td>30</td><td>2013-01-01 16:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> NA</td><td>1935</td><td>NA</td><td>  NA</td><td>2240</td><td> NA</td><td>AA</td><td> 791</td><td>N3EHAA</td><td>LGA</td><td>DFW</td><td> NA</td><td>1389</td><td>19</td><td>35</td><td>2013-01-01 19:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> NA</td><td>1500</td><td>NA</td><td>  NA</td><td>1825</td><td> NA</td><td>AA</td><td>1925</td><td>N3EVAA</td><td>LGA</td><td>MIA</td><td> NA</td><td>1096</td><td>15</td><td> 0</td><td>2013-01-01 15:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td> NA</td><td> 600</td><td>NA</td><td>  NA</td><td> 901</td><td> NA</td><td>B6</td><td> 125</td><td>N618JB</td><td>JFK</td><td>FLL</td><td> NA</td><td>1069</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>517</td><td> 515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td> 5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>533</td><td> 529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td> 5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>542</td><td> 540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td> 5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>544</td><td> 545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td> 5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td> 600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>554</td><td> 558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td> 5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>555</td><td> 600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td> 600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>557</td><td> 600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td> 600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td> 600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td> 600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td> 600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>558</td><td> 600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td> 600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td> 559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td> 5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>559</td><td> 600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td> 600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>600</td><td> 600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>601</td><td> 600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td> 610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td> 6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>602</td><td> 605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td> 6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td> 610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td> 6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>606</td><td> 610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td> 6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>607</td><td> 607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td> 6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>608</td><td> 600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td> 6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2128</td><td>2125</td><td>  3</td><td>2243</td><td>2240</td><td>  3</td><td>MQ</td><td>4449</td><td>N810MQ</td><td>JFK</td><td>DCA</td><td> 54</td><td> 213</td><td>21</td><td>25</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2129</td><td>2120</td><td>  9</td><td>2342</td><td>2351</td><td> -9</td><td>B6</td><td>  97</td><td>N625JB</td><td>JFK</td><td>DEN</td><td>223</td><td>1626</td><td>21</td><td>20</td><td>2013-01-01 21:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2134</td><td>2045</td><td> 49</td><td>  20</td><td>2352</td><td> 28</td><td>UA</td><td>1106</td><td>N27733</td><td>EWR</td><td>FLL</td><td>152</td><td>1065</td><td>20</td><td>45</td><td>2013-01-01 20:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>2136</td><td>2145</td><td> -9</td><td>  25</td><td>  39</td><td>-14</td><td>B6</td><td> 515</td><td>N198JB</td><td>EWR</td><td>FLL</td><td>154</td><td>1065</td><td>21</td><td>45</td><td>2013-01-01 21:00:00</td></tr>
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
</tbody>
</table>



### Exercises:
1. Use mutate(), is.na(), and count() together to describe how the missing values in dep_time, sched_dep_time and dep_delay are connected.

## 12.3 Boolean Algebra
`!, &, xor, |`


```R
df <- tibble(x = c(TRUE, FALSE, NA))

df |> 
  mutate(
    and = x & NA,
    or = x | NA
  )
```


<table class="dataframe">
<caption>A tibble: 3 x 3</caption>
<thead>
	<tr><th scope=col>x</th><th scope=col>and</th><th scope=col>or</th></tr>
	<tr><th scope=col>&lt;lgl&gt;</th><th scope=col>&lt;lgl&gt;</th><th scope=col>&lt;lgl&gt;</th></tr>
</thead>
<tbody>
	<tr><td> TRUE</td><td>   NA</td><td>TRUE</td></tr>
	<tr><td>FALSE</td><td>FALSE</td><td>  NA</td></tr>
	<tr><td>   NA</td><td>   NA</td><td>  NA</td></tr>
</tbody>
</table>




```R
flights |> 
  filter(month %in% c(11, 12))
```


<table class="dataframe">
<caption>A tibble: 55403 x 19</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>11</td><td>1</td><td>  5</td><td>2359</td><td>  6</td><td>352</td><td> 345</td><td>  7</td><td>B6</td><td> 745</td><td>N568JB</td><td>JFK</td><td>PSE</td><td>205</td><td>1617</td><td>23</td><td>59</td><td>2013-11-01 23:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td> 35</td><td>2250</td><td>105</td><td>123</td><td>2356</td><td> 87</td><td>B6</td><td>1816</td><td>N353JB</td><td>JFK</td><td>SYR</td><td> 36</td><td> 209</td><td>22</td><td>50</td><td>2013-11-01 22:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>455</td><td> 500</td><td> -5</td><td>641</td><td> 651</td><td>-10</td><td>US</td><td>1895</td><td>N192UW</td><td>EWR</td><td>CLT</td><td> 88</td><td> 529</td><td> 5</td><td> 0</td><td>2013-11-01 05:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>539</td><td> 545</td><td> -6</td><td>856</td><td> 827</td><td> 29</td><td>UA</td><td>1714</td><td>N38727</td><td>LGA</td><td>IAH</td><td>229</td><td>1416</td><td> 5</td><td>45</td><td>2013-11-01 05:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>542</td><td> 545</td><td> -3</td><td>831</td><td> 855</td><td>-24</td><td>AA</td><td>2243</td><td>N5CLAA</td><td>JFK</td><td>MIA</td><td>147</td><td>1089</td><td> 5</td><td>45</td><td>2013-11-01 05:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>549</td><td> 600</td><td>-11</td><td>912</td><td> 923</td><td>-11</td><td>UA</td><td> 303</td><td>N595UA</td><td>JFK</td><td>SFO</td><td>359</td><td>2586</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>550</td><td> 600</td><td>-10</td><td>705</td><td> 659</td><td>  6</td><td>US</td><td>2167</td><td>N748UW</td><td>LGA</td><td>DCA</td><td> 57</td><td> 214</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>554</td><td> 600</td><td> -6</td><td>659</td><td> 701</td><td> -2</td><td>US</td><td>2134</td><td>N742PS</td><td>LGA</td><td>BOS</td><td> 40</td><td> 184</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>554</td><td> 600</td><td> -6</td><td>826</td><td> 827</td><td> -1</td><td>DL</td><td> 563</td><td>N912DE</td><td>LGA</td><td>ATL</td><td>126</td><td> 762</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>554</td><td> 600</td><td> -6</td><td>749</td><td> 751</td><td> -2</td><td>DL</td><td> 731</td><td>N315NB</td><td>LGA</td><td>DTW</td><td> 93</td><td> 502</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>555</td><td> 600</td><td> -5</td><td>847</td><td> 854</td><td> -7</td><td>B6</td><td> 605</td><td>N640JB</td><td>EWR</td><td>FLL</td><td>149</td><td>1065</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>555</td><td> 600</td><td> -5</td><td>839</td><td> 846</td><td> -7</td><td>B6</td><td> 583</td><td>N661JB</td><td>JFK</td><td>MCO</td><td>136</td><td> 944</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>555</td><td> 600</td><td> -5</td><td>929</td><td> 943</td><td>-14</td><td>B6</td><td>1403</td><td>N746JB</td><td>JFK</td><td>SJU</td><td>196</td><td>1598</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>556</td><td> 600</td><td> -4</td><td>834</td><td> 851</td><td>-17</td><td>UA</td><td> 407</td><td>N834UA</td><td>EWR</td><td>TPA</td><td>142</td><td> 997</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>558</td><td> 600</td><td> -2</td><td>727</td><td> 730</td><td> -3</td><td>UA</td><td> 279</td><td>N459UA</td><td>EWR</td><td>ORD</td><td>118</td><td> 719</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>558</td><td> 600</td><td> -2</td><td>650</td><td> 658</td><td> -8</td><td>US</td><td>1909</td><td>N950UW</td><td>LGA</td><td>PHL</td><td> 38</td><td>  96</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>558</td><td> 600</td><td> -2</td><td>914</td><td> 905</td><td>  9</td><td>AA</td><td>1175</td><td>N3GHAA</td><td>LGA</td><td>MIA</td><td>155</td><td>1096</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>558</td><td> 600</td><td> -2</td><td>720</td><td> 715</td><td>  5</td><td>WN</td><td> 464</td><td>N390SW</td><td>EWR</td><td>MDW</td><td>117</td><td> 711</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>559</td><td> 600</td><td> -1</td><td>756</td><td> 730</td><td> 26</td><td>AA</td><td> 301</td><td>N4YHAA</td><td>LGA</td><td>ORD</td><td>119</td><td> 733</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>600</td><td> 600</td><td>  0</td><td>709</td><td> 716</td><td> -7</td><td>EV</td><td>5716</td><td>N820AS</td><td>JFK</td><td>IAD</td><td> 49</td><td> 228</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>600</td><td> 600</td><td>  0</td><td>725</td><td> 721</td><td>  4</td><td>UA</td><td>1198</td><td>N23707</td><td>LGA</td><td>ORD</td><td>121</td><td> 733</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>601</td><td> 600</td><td>  1</td><td>853</td><td> 856</td><td> -3</td><td>B6</td><td> 371</td><td>N570JB</td><td>LGA</td><td>FLL</td><td>150</td><td>1076</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>601</td><td> 610</td><td> -9</td><td>803</td><td> 813</td><td>-10</td><td>DL</td><td>1919</td><td>N922DL</td><td>LGA</td><td>MSP</td><td>153</td><td>1020</td><td> 6</td><td>10</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>602</td><td> 600</td><td>  2</td><td>843</td><td> 815</td><td> 28</td><td>FL</td><td> 345</td><td>N353AT</td><td>LGA</td><td>ATL</td><td>131</td><td> 762</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>603</td><td> 600</td><td>  3</td><td>717</td><td> 711</td><td>  6</td><td>EV</td><td>4533</td><td>N11109</td><td>EWR</td><td>BUF</td><td> 53</td><td> 282</td><td> 6</td><td> 0</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>604</td><td> 610</td><td> -6</td><td>855</td><td> 855</td><td>  0</td><td>AA</td><td>1103</td><td>N3FTAA</td><td>LGA</td><td>DFW</td><td>205</td><td>1389</td><td> 6</td><td>10</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>606</td><td> 615</td><td> -9</td><td>746</td><td> 750</td><td> -4</td><td>MQ</td><td>3525</td><td>N834MQ</td><td>LGA</td><td>RDU</td><td> 74</td><td> 431</td><td> 6</td><td>15</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>606</td><td> 615</td><td> -9</td><td>807</td><td> 817</td><td>-10</td><td>US</td><td>1899</td><td>N199UW</td><td>JFK</td><td>CLT</td><td> 93</td><td> 541</td><td> 6</td><td>15</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>606</td><td> 610</td><td> -4</td><td>752</td><td> 745</td><td>  7</td><td>WN</td><td>2609</td><td>N440LV</td><td>LGA</td><td>STL</td><td>142</td><td> 888</td><td> 6</td><td>10</td><td>2013-11-01 06:00:00</td></tr>
	<tr><td>2013</td><td>11</td><td>1</td><td>607</td><td> 611</td><td> -4</td><td>857</td><td> 912</td><td>-15</td><td>B6</td><td> 601</td><td>N597JB</td><td>JFK</td><td>FLL</td><td>149</td><td>1069</td><td> 6</td><td>11</td><td>2013-11-01 06:00:00</td></tr>
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



### Exercises
1. Find all flights where `arr_delay` is missing but dep_delay is not. Find all flights where neither `arr_time` nor `sched_arr_time` are missing, but arr_delay is.
2. How many flights have a missing `dep_time`? What other variables are missing in these rows? What might these rows represent?
3. Assuming that a missing dep_time implies that a flight is cancelled, look at the number of cancelled flights per day. Is there a pattern? Is there a connection between the proportion of cancelled flights and the average delay of non-cancelled flights?

## 12.4 Summarizes
### Logical summarizes

### Nummeric summaries of logical vectors

### Logical subsetting

### Exercises

## 12.5 Conditional transformations

### `if_else()`

### `case_when()`

### Compatible types

### Exercises

## 12.6 Summary

# C13. Numbers

## 13.2 Making numbers

## 13.3 Counts

## 13.4 Numeric transformations

## 13.5 General transformations

## 13.6 Numeric summaries

## 13.7 Summary

# C14. Strings

## 14.2 Creating a string

## 14.3 Creating many strings from data

## 14.4 Extracting data from strings


## 14.5 Letters

## 14.6 Non-English text

## 14.7 Summary

# C15 Regular Expressions


```R
library(tidyverse)
library(babynames)
```

## 15.2 Pattern basics

## 15.3 Key functions

## 15.4 Pattern details

## 15.5 Pattern control

## 15.6 Practice

## 15.7 Regular expressions in other places

## 15.8 Summary

# C16. Factors
## 16.2 Factor basics


```R
month_levels <- c(
  "Jan", "Feb", "Mar", "Apr", "May", "Jun", 
  "Jul", "Aug", "Sep", "Oct", "Nov", "Dec"
)
```


```R
x1 <- c("Dec", "Apr", "Jan", "Mar")

y1 <- factor(x1, levels = month_levels)
y1

sort(y1)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>Dec</li><li>Apr</li><li>Jan</li><li>Mar</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Jan'</li><li>'Feb'</li><li>'Mar'</li><li>'Apr'</li><li>'May'</li><li>'Jun'</li><li>'Jul'</li><li>'Aug'</li><li>'Sep'</li><li>'Oct'</li><li>'Nov'</li><li>'Dec'</li></ol>
</details>



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>Jan</li><li>Mar</li><li>Apr</li><li>Dec</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Jan'</li><li>'Feb'</li><li>'Mar'</li><li>'Apr'</li><li>'May'</li><li>'Jun'</li><li>'Jul'</li><li>'Aug'</li><li>'Sep'</li><li>'Oct'</li><li>'Nov'</li><li>'Dec'</li></ol>
</details>



```R
x2 <- c("Dec", "Apr", "Jam", "Mar")
y2 <- factor(x2, levels = month_levels)
y2

sort(y2)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>Dec</li><li>Apr</li><li>&lt;NA&gt;</li><li>Mar</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Jan'</li><li>'Feb'</li><li>'Mar'</li><li>'Apr'</li><li>'May'</li><li>'Jun'</li><li>'Jul'</li><li>'Aug'</li><li>'Sep'</li><li>'Oct'</li><li>'Nov'</li><li>'Dec'</li></ol>
</details>



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>Mar</li><li>Apr</li><li>Dec</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Jan'</li><li>'Feb'</li><li>'Mar'</li><li>'Apr'</li><li>'May'</li><li>'Jun'</li><li>'Jul'</li><li>'Aug'</li><li>'Sep'</li><li>'Oct'</li><li>'Nov'</li><li>'Dec'</li></ol>
</details>



```R
levels(y2)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'Jan'</li><li>'Feb'</li><li>'Mar'</li><li>'Apr'</li><li>'May'</li><li>'Jun'</li><li>'Jul'</li><li>'Aug'</li><li>'Sep'</li><li>'Oct'</li><li>'Nov'</li><li>'Dec'</li></ol>




```R
library(readr)
csv <- "
month,value
Jan,12
Feb,56
Mar,12"

df <- read_csv(csv, col_types = cols(month = col_factor(month_levels)))
df$month
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>Jan</li><li>Feb</li><li>Mar</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'Jan'</li><li>'Feb'</li><li>'Mar'</li><li>'Apr'</li><li>'May'</li><li>'Jun'</li><li>'Jul'</li><li>'Aug'</li><li>'Sep'</li><li>'Oct'</li><li>'Nov'</li><li>'Dec'</li></ol>
</details>


## 16.3 General Social Survey


```R
library(tidyverse)
library(gridExtra)
gss_cat
```


<table class="dataframe">
<caption>A tibble: 21483 x 9</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>marital</th><th scope=col>age</th><th scope=col>race</th><th scope=col>rincome</th><th scope=col>partyid</th><th scope=col>relig</th><th scope=col>denom</th><th scope=col>tvhours</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2000</td><td>Never married</td><td>26</td><td>White</td><td>$8000 to 9999 </td><td>Ind,near rep      </td><td>Protestant        </td><td>Southern baptist </td><td>12</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>48</td><td>White</td><td>$8000 to 9999 </td><td>Not str republican</td><td>Protestant        </td><td>Baptist-dk which </td><td>NA</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>67</td><td>White</td><td>Not applicable</td><td>Independent       </td><td>Protestant        </td><td>No denomination  </td><td> 2</td></tr>
	<tr><td>2000</td><td>Never married</td><td>39</td><td>White</td><td>Not applicable</td><td>Ind,near rep      </td><td>Orthodox-christian</td><td>Not applicable   </td><td> 4</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>25</td><td>White</td><td>Not applicable</td><td>Not str democrat  </td><td>None              </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>25</td><td>White</td><td>$20000 - 24999</td><td>Strong democrat   </td><td>Protestant        </td><td>Southern baptist </td><td>NA</td></tr>
	<tr><td>2000</td><td>Never married</td><td>36</td><td>White</td><td>$25000 or more</td><td>Not str republican</td><td>Christian         </td><td>Not applicable   </td><td> 3</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>44</td><td>White</td><td>$7000 to 7999 </td><td>Ind,near dem      </td><td>Protestant        </td><td>Lutheran-mo synod</td><td>NA</td></tr>
	<tr><td>2000</td><td>Married      </td><td>44</td><td>White</td><td>$25000 or more</td><td>Not str democrat  </td><td>Protestant        </td><td>Other            </td><td> 0</td></tr>
	<tr><td>2000</td><td>Married      </td><td>47</td><td>White</td><td>$25000 or more</td><td>Strong republican </td><td>Protestant        </td><td>Southern baptist </td><td> 3</td></tr>
	<tr><td>2000</td><td>Married      </td><td>53</td><td>White</td><td>$25000 or more</td><td>Not str democrat  </td><td>Protestant        </td><td>Other            </td><td> 2</td></tr>
	<tr><td>2000</td><td>Married      </td><td>52</td><td>White</td><td>$25000 or more</td><td>Ind,near rep      </td><td>None              </td><td>Not applicable   </td><td>NA</td></tr>
	<tr><td>2000</td><td>Married      </td><td>52</td><td>White</td><td>$25000 or more</td><td>Strong democrat   </td><td>Protestant        </td><td>Southern baptist </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>51</td><td>White</td><td>$25000 or more</td><td>Strong republican </td><td>Protestant        </td><td>United methodist </td><td>NA</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>52</td><td>White</td><td>$25000 or more</td><td>Ind,near dem      </td><td>None              </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>40</td><td>Black</td><td>$25000 or more</td><td>Strong democrat   </td><td>Protestant        </td><td>Baptist-dk which </td><td> 7</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>77</td><td>White</td><td>Not applicable</td><td>Strong republican </td><td>Jewish            </td><td>Not applicable   </td><td>NA</td></tr>
	<tr><td>2000</td><td>Never married</td><td>44</td><td>White</td><td>$25000 or more</td><td>Independent       </td><td>None              </td><td>Not applicable   </td><td> 3</td></tr>
	<tr><td>2000</td><td>Married      </td><td>40</td><td>White</td><td>$10000 - 14999</td><td>Not str democrat  </td><td>Catholic          </td><td>Not applicable   </td><td> 3</td></tr>
	<tr><td>2000</td><td>Married      </td><td>45</td><td>Black</td><td>Not applicable</td><td>Independent       </td><td>Protestant        </td><td>United methodist </td><td>NA</td></tr>
	<tr><td>2000</td><td>Married      </td><td>48</td><td>White</td><td>$25000 or more</td><td>Ind,near dem      </td><td>Catholic          </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>49</td><td>White</td><td>Refused       </td><td>Strong republican </td><td>Protestant        </td><td>United methodist </td><td> 2</td></tr>
	<tr><td>2000</td><td>Never married</td><td>19</td><td>White</td><td>Not applicable</td><td>Independent       </td><td>None              </td><td>Not applicable   </td><td> 2</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>54</td><td>White</td><td>$25000 or more</td><td>Ind,near rep      </td><td>Christian         </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>82</td><td>White</td><td>Not applicable</td><td>Not str democrat  </td><td>Protestant        </td><td>Other            </td><td> 3</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>83</td><td>White</td><td>Not applicable</td><td>Strong democrat   </td><td>Protestant        </td><td>Episcopal        </td><td>NA</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>89</td><td>White</td><td>Not applicable</td><td>Not str democrat  </td><td>Protestant        </td><td>Other lutheran   </td><td> 4</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>88</td><td>White</td><td>Not applicable</td><td>Strong republican </td><td>Protestant        </td><td>Afr meth ep zion </td><td>NA</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>72</td><td>White</td><td>Not applicable</td><td>Strong democrat   </td><td>Protestant        </td><td>Southern baptist </td><td> 7</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>82</td><td>White</td><td>Not applicable</td><td>Independent       </td><td>Protestant        </td><td>Am bapt ch in usa</td><td>NA</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>38</td><td>White</td><td>$3000 to 3999 </td><td>Not str republican</td><td>Protestant</td><td>Other           </td><td> 1</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>46</td><td>White</td><td>$25000 or more</td><td>Strong democrat   </td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>49</td><td>White</td><td>Not applicable</td><td>Ind,near rep      </td><td>Protestant</td><td>Other           </td><td> 6</td></tr>
	<tr><td>2014</td><td>Never married</td><td>34</td><td>White</td><td>$25000 or more</td><td>Independent       </td><td>Protestant</td><td>United methodist</td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>54</td><td>White</td><td>Not applicable</td><td>Independent       </td><td>Protestant</td><td>Other           </td><td>NA</td></tr>
	<tr><td>2014</td><td>Married      </td><td>34</td><td>White</td><td>$15000 - 19999</td><td>Ind,near dem      </td><td>Buddhism  </td><td>Not applicable  </td><td> 1</td></tr>
	<tr><td>2014</td><td>Married      </td><td>69</td><td>White</td><td>Not applicable</td><td>Ind,near dem      </td><td>Jewish    </td><td>Not applicable  </td><td> 3</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>36</td><td>White</td><td>Not applicable</td><td>Independent       </td><td>None      </td><td>Not applicable  </td><td> 0</td></tr>
	<tr><td>2014</td><td>Married      </td><td>65</td><td>White</td><td>$25000 or more</td><td>Not str democrat  </td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>48</td><td>White</td><td>$20000 - 24999</td><td>Strong democrat   </td><td>Protestant</td><td>Other           </td><td> 0</td></tr>
	<tr><td>2014</td><td>Married      </td><td>38</td><td>White</td><td>$10000 - 14999</td><td>Not str democrat  </td><td>Protestant</td><td>No denomination </td><td> 2</td></tr>
	<tr><td>2014</td><td>Never married</td><td>30</td><td>White</td><td>$4000 to 4999 </td><td>Ind,near dem      </td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>48</td><td>White</td><td>$8000 to 9999 </td><td>Not str republican</td><td>Catholic  </td><td>Not applicable  </td><td> 0</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>49</td><td>White</td><td>$25000 or more</td><td>Ind,near rep      </td><td>Other     </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>54</td><td>White</td><td>$25000 or more</td><td>Ind,near dem      </td><td>Protestant</td><td>Other           </td><td>NA</td></tr>
	<tr><td>2014</td><td>Married      </td><td>49</td><td>White</td><td>$25000 or more</td><td>Not str republican</td><td>Catholic  </td><td>Not applicable  </td><td>NA</td></tr>
	<tr><td>2014</td><td>Married      </td><td>53</td><td>White</td><td>$25000 or more</td><td>Not str democrat  </td><td>None      </td><td>Not applicable  </td><td> 0</td></tr>
	<tr><td>2014</td><td>Married      </td><td>52</td><td>White</td><td>$25000 or more</td><td>Not str democrat  </td><td>None      </td><td>Not applicable  </td><td> 1</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>82</td><td>White</td><td>Not applicable</td><td>Strong democrat   </td><td>Protestant</td><td>Other           </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>63</td><td>White</td><td>Not applicable</td><td>Ind,near dem      </td><td>No answer </td><td>No answer       </td><td> 2</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>54</td><td>White</td><td>$25000 or more</td><td>Ind,near rep      </td><td>Catholic  </td><td>Not applicable  </td><td> 3</td></tr>
	<tr><td>2014</td><td>Married      </td><td>62</td><td>White</td><td>$25000 or more</td><td>Ind,near rep      </td><td>Protestant</td><td>Other           </td><td>NA</td></tr>
	<tr><td>2014</td><td>Never married</td><td>40</td><td>White</td><td>$1000 to 2999 </td><td>Not str republican</td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>33</td><td>White</td><td>Not applicable</td><td>Independent       </td><td>Christian </td><td>No denomination </td><td> 0</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>75</td><td>White</td><td>Don't know    </td><td>Strong republican </td><td>Protestant</td><td>Baptist-dk which</td><td> 4</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>89</td><td>White</td><td>Not applicable</td><td>Not str republican</td><td>Protestant</td><td>United methodist</td><td> 3</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>56</td><td>White</td><td>$25000 or more</td><td>Independent       </td><td>None      </td><td>Not applicable  </td><td> 4</td></tr>
	<tr><td>2014</td><td>Never married</td><td>24</td><td>White</td><td>$10000 - 14999</td><td>Ind,near dem      </td><td>None      </td><td>Not applicable  </td><td> 4</td></tr>
	<tr><td>2014</td><td>Never married</td><td>27</td><td>White</td><td>$25000 or more</td><td>Not str democrat  </td><td>Catholic  </td><td>Not applicable  </td><td>NA</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>71</td><td>White</td><td>$20000 - 24999</td><td>Ind,near rep      </td><td>Protestant</td><td>Other           </td><td> 2</td></tr>
</tbody>
</table>




```R
gss_cat |>
  count(race)

```


<table class="dataframe">
<caption>A tibble: 3 x 2</caption>
<thead>
	<tr><th scope=col>race</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Other</td><td> 1959</td></tr>
	<tr><td>Black</td><td> 3129</td></tr>
	<tr><td>White</td><td>16395</td></tr>
</tbody>
</table>



### Exercises
1. Explore the distribution of rincome (reported income). What makes the default bar chart hard to understand? How could you improve the plot?

2. What is the most common relig in this survey? What’s the most common partyid?

3. Which relig does denom (denomination) apply to? How can you find out with a table? How can you find out with a visualization?

## 16.4 Modifying factor order


```R
relig_summary <- gss_cat |>
  group_by(relig) |>
  summarize(
    tvhours = mean(tvhours, na.rm = TRUE),
    n = n()
  )

ggplot(relig_summary, aes(x = tvhours, y = relig)) + 
  geom_point()
```


    
![png](R4DS-Transform_files/R4DS-Transform_66_0.png)
    



```R
ggplot(relig_summary, aes(x = tvhours, y = fct_reorder(relig, tvhours))) +
  geom_point()
```


    
![png](R4DS-Transform_files/R4DS-Transform_67_0.png)
    



```R
relig_summary |>
  mutate(
    relig = fct_reorder(relig, tvhours)
  ) |>
  ggplot(aes(x = tvhours, y = relig)) +
  geom_point()
```


    
![png](R4DS-Transform_files/R4DS-Transform_68_0.png)
    



```R
rincome_summary <- gss_cat |>
  group_by(rincome) |>
  summarize(
    age = mean(age, na.rm = TRUE),
    n = n()
  )

ggplot(rincome_summary, aes(x = age, y = fct_reorder(rincome, age))) + 
  geom_point()
```


    
![png](R4DS-Transform_files/R4DS-Transform_69_0.png)
    



```R
ggplot(rincome_summary, aes(x = age, y = fct_relevel(rincome, "Not applicable"))) +
  geom_point()
```


    
![png](R4DS-Transform_files/R4DS-Transform_70_0.png)
    



```R
by_age <- gss_cat |>
  filter(!is.na(age)) |> 
  count(age, marital) |>
  group_by(age) |>
  mutate(
    prop = n / sum(n)
  )

p1 <- ggplot(by_age, aes(x = age, y = prop, color = marital)) +
  geom_line(linewidth = 1) + 
  scale_color_brewer(palette = "Set1")

p2 <- ggplot(by_age, aes(x = age, y = prop, color = fct_reorder2(marital, age, prop))) +
  geom_line(linewidth = 1) +
  scale_color_brewer(palette = "Set1") + 
  labs(color = "marital") 

options(repr.plot.width = 20, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)

```


    
![png](R4DS-Transform_files/R4DS-Transform_71_0.png)
    



```R
gss_cat |>
  mutate(marital = marital |> fct_infreq() |> fct_rev()) |>
  ggplot(aes(x = marital)) +
  geom_bar()
  options(repr.plot.width = 10, repr.plot.height = 5)

```


    
![png](R4DS-Transform_files/R4DS-Transform_72_0.png)
    


1. There are some suspiciously high numbers in tvhours. Is the mean a good summary?

2. For each factor in gss_cat identify whether the order of the levels is arbitrary or principled.

3. Why did moving “Not applicable” to the front of the levels move it to the bottom of the plot?

## 16.5 Modifying factor levels


```R
gss_cat |> count(partyid)
```


<table class="dataframe">
<caption>A tibble: 10 x 2</caption>
<thead>
	<tr><th scope=col>partyid</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>No answer         </td><td> 154</td></tr>
	<tr><td>Don't know        </td><td>   1</td></tr>
	<tr><td>Other party       </td><td> 393</td></tr>
	<tr><td>Strong republican </td><td>2314</td></tr>
	<tr><td>Not str republican</td><td>3032</td></tr>
	<tr><td>Ind,near rep      </td><td>1791</td></tr>
	<tr><td>Independent       </td><td>4119</td></tr>
	<tr><td>Ind,near dem      </td><td>2499</td></tr>
	<tr><td>Not str democrat  </td><td>3690</td></tr>
	<tr><td>Strong democrat   </td><td>3490</td></tr>
</tbody>
</table>




```R
gss_cat |>
  mutate(
    partyid = fct_recode(partyid,
      "Republican, strong"    = "Strong republican",
      "Republican, weak"      = "Not str republican",
      "Independent, near rep" = "Ind,near rep",
      "Independent, near dem" = "Ind,near dem",
      "Democrat, weak"        = "Not str democrat",
      "Democrat, strong"      = "Strong democrat"
    )
  ) |>
  count(partyid)
```


<table class="dataframe">
<caption>A tibble: 10 x 2</caption>
<thead>
	<tr><th scope=col>partyid</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>No answer            </td><td> 154</td></tr>
	<tr><td>Don't know           </td><td>   1</td></tr>
	<tr><td>Other party          </td><td> 393</td></tr>
	<tr><td>Republican, strong   </td><td>2314</td></tr>
	<tr><td>Republican, weak     </td><td>3032</td></tr>
	<tr><td>Independent, near rep</td><td>1791</td></tr>
	<tr><td>Independent          </td><td>4119</td></tr>
	<tr><td>Independent, near dem</td><td>2499</td></tr>
	<tr><td>Democrat, weak       </td><td>3690</td></tr>
	<tr><td>Democrat, strong     </td><td>3490</td></tr>
</tbody>
</table>




```R
gss_cat |>
  mutate(
    partyid = fct_recode(partyid,
      "Republican, strong"    = "Strong republican",
      "Republican, weak"      = "Not str republican",
      "Independent, near rep" = "Ind,near rep",
      "Independent, near dem" = "Ind,near dem",
      "Democrat, weak"        = "Not str democrat",
      "Democrat, strong"      = "Strong democrat",
      "Other"                 = "No answer",
      "Other"                 = "Don't know",
      "Other"                 = "Other party"
    )
  )
```


<table class="dataframe">
<caption>A tibble: 21483 x 9</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>marital</th><th scope=col>age</th><th scope=col>race</th><th scope=col>rincome</th><th scope=col>partyid</th><th scope=col>relig</th><th scope=col>denom</th><th scope=col>tvhours</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2000</td><td>Never married</td><td>26</td><td>White</td><td>$8000 to 9999 </td><td>Independent, near rep</td><td>Protestant        </td><td>Southern baptist </td><td>12</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>48</td><td>White</td><td>$8000 to 9999 </td><td>Republican, weak     </td><td>Protestant        </td><td>Baptist-dk which </td><td>NA</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>67</td><td>White</td><td>Not applicable</td><td>Independent          </td><td>Protestant        </td><td>No denomination  </td><td> 2</td></tr>
	<tr><td>2000</td><td>Never married</td><td>39</td><td>White</td><td>Not applicable</td><td>Independent, near rep</td><td>Orthodox-christian</td><td>Not applicable   </td><td> 4</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>25</td><td>White</td><td>Not applicable</td><td>Democrat, weak       </td><td>None              </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>25</td><td>White</td><td>$20000 - 24999</td><td>Democrat, strong     </td><td>Protestant        </td><td>Southern baptist </td><td>NA</td></tr>
	<tr><td>2000</td><td>Never married</td><td>36</td><td>White</td><td>$25000 or more</td><td>Republican, weak     </td><td>Christian         </td><td>Not applicable   </td><td> 3</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>44</td><td>White</td><td>$7000 to 7999 </td><td>Independent, near dem</td><td>Protestant        </td><td>Lutheran-mo synod</td><td>NA</td></tr>
	<tr><td>2000</td><td>Married      </td><td>44</td><td>White</td><td>$25000 or more</td><td>Democrat, weak       </td><td>Protestant        </td><td>Other            </td><td> 0</td></tr>
	<tr><td>2000</td><td>Married      </td><td>47</td><td>White</td><td>$25000 or more</td><td>Republican, strong   </td><td>Protestant        </td><td>Southern baptist </td><td> 3</td></tr>
	<tr><td>2000</td><td>Married      </td><td>53</td><td>White</td><td>$25000 or more</td><td>Democrat, weak       </td><td>Protestant        </td><td>Other            </td><td> 2</td></tr>
	<tr><td>2000</td><td>Married      </td><td>52</td><td>White</td><td>$25000 or more</td><td>Independent, near rep</td><td>None              </td><td>Not applicable   </td><td>NA</td></tr>
	<tr><td>2000</td><td>Married      </td><td>52</td><td>White</td><td>$25000 or more</td><td>Democrat, strong     </td><td>Protestant        </td><td>Southern baptist </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>51</td><td>White</td><td>$25000 or more</td><td>Republican, strong   </td><td>Protestant        </td><td>United methodist </td><td>NA</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>52</td><td>White</td><td>$25000 or more</td><td>Independent, near dem</td><td>None              </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>40</td><td>Black</td><td>$25000 or more</td><td>Democrat, strong     </td><td>Protestant        </td><td>Baptist-dk which </td><td> 7</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>77</td><td>White</td><td>Not applicable</td><td>Republican, strong   </td><td>Jewish            </td><td>Not applicable   </td><td>NA</td></tr>
	<tr><td>2000</td><td>Never married</td><td>44</td><td>White</td><td>$25000 or more</td><td>Independent          </td><td>None              </td><td>Not applicable   </td><td> 3</td></tr>
	<tr><td>2000</td><td>Married      </td><td>40</td><td>White</td><td>$10000 - 14999</td><td>Democrat, weak       </td><td>Catholic          </td><td>Not applicable   </td><td> 3</td></tr>
	<tr><td>2000</td><td>Married      </td><td>45</td><td>Black</td><td>Not applicable</td><td>Independent          </td><td>Protestant        </td><td>United methodist </td><td>NA</td></tr>
	<tr><td>2000</td><td>Married      </td><td>48</td><td>White</td><td>$25000 or more</td><td>Independent, near dem</td><td>Catholic          </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Married      </td><td>49</td><td>White</td><td>Refused       </td><td>Republican, strong   </td><td>Protestant        </td><td>United methodist </td><td> 2</td></tr>
	<tr><td>2000</td><td>Never married</td><td>19</td><td>White</td><td>Not applicable</td><td>Independent          </td><td>None              </td><td>Not applicable   </td><td> 2</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>54</td><td>White</td><td>$25000 or more</td><td>Independent, near rep</td><td>Christian         </td><td>Not applicable   </td><td> 1</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>82</td><td>White</td><td>Not applicable</td><td>Democrat, weak       </td><td>Protestant        </td><td>Other            </td><td> 3</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>83</td><td>White</td><td>Not applicable</td><td>Democrat, strong     </td><td>Protestant        </td><td>Episcopal        </td><td>NA</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>89</td><td>White</td><td>Not applicable</td><td>Democrat, weak       </td><td>Protestant        </td><td>Other lutheran   </td><td> 4</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>88</td><td>White</td><td>Not applicable</td><td>Republican, strong   </td><td>Protestant        </td><td>Afr meth ep zion </td><td>NA</td></tr>
	<tr><td>2000</td><td>Divorced     </td><td>72</td><td>White</td><td>Not applicable</td><td>Democrat, strong     </td><td>Protestant        </td><td>Southern baptist </td><td> 7</td></tr>
	<tr><td>2000</td><td>Widowed      </td><td>82</td><td>White</td><td>Not applicable</td><td>Independent          </td><td>Protestant        </td><td>Am bapt ch in usa</td><td>NA</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>38</td><td>White</td><td>$3000 to 3999 </td><td>Republican, weak     </td><td>Protestant</td><td>Other           </td><td> 1</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>46</td><td>White</td><td>$25000 or more</td><td>Democrat, strong     </td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>49</td><td>White</td><td>Not applicable</td><td>Independent, near rep</td><td>Protestant</td><td>Other           </td><td> 6</td></tr>
	<tr><td>2014</td><td>Never married</td><td>34</td><td>White</td><td>$25000 or more</td><td>Independent          </td><td>Protestant</td><td>United methodist</td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>54</td><td>White</td><td>Not applicable</td><td>Independent          </td><td>Protestant</td><td>Other           </td><td>NA</td></tr>
	<tr><td>2014</td><td>Married      </td><td>34</td><td>White</td><td>$15000 - 19999</td><td>Independent, near dem</td><td>Buddhism  </td><td>Not applicable  </td><td> 1</td></tr>
	<tr><td>2014</td><td>Married      </td><td>69</td><td>White</td><td>Not applicable</td><td>Independent, near dem</td><td>Jewish    </td><td>Not applicable  </td><td> 3</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>36</td><td>White</td><td>Not applicable</td><td>Independent          </td><td>None      </td><td>Not applicable  </td><td> 0</td></tr>
	<tr><td>2014</td><td>Married      </td><td>65</td><td>White</td><td>$25000 or more</td><td>Democrat, weak       </td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>48</td><td>White</td><td>$20000 - 24999</td><td>Democrat, strong     </td><td>Protestant</td><td>Other           </td><td> 0</td></tr>
	<tr><td>2014</td><td>Married      </td><td>38</td><td>White</td><td>$10000 - 14999</td><td>Democrat, weak       </td><td>Protestant</td><td>No denomination </td><td> 2</td></tr>
	<tr><td>2014</td><td>Never married</td><td>30</td><td>White</td><td>$4000 to 4999 </td><td>Independent, near dem</td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>48</td><td>White</td><td>$8000 to 9999 </td><td>Republican, weak     </td><td>Catholic  </td><td>Not applicable  </td><td> 0</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>49</td><td>White</td><td>$25000 or more</td><td>Independent, near rep</td><td>Other     </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>54</td><td>White</td><td>$25000 or more</td><td>Independent, near dem</td><td>Protestant</td><td>Other           </td><td>NA</td></tr>
	<tr><td>2014</td><td>Married      </td><td>49</td><td>White</td><td>$25000 or more</td><td>Republican, weak     </td><td>Catholic  </td><td>Not applicable  </td><td>NA</td></tr>
	<tr><td>2014</td><td>Married      </td><td>53</td><td>White</td><td>$25000 or more</td><td>Democrat, weak       </td><td>None      </td><td>Not applicable  </td><td> 0</td></tr>
	<tr><td>2014</td><td>Married      </td><td>52</td><td>White</td><td>$25000 or more</td><td>Democrat, weak       </td><td>None      </td><td>Not applicable  </td><td> 1</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>82</td><td>White</td><td>Not applicable</td><td>Democrat, strong     </td><td>Protestant</td><td>Other           </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>63</td><td>White</td><td>Not applicable</td><td>Independent, near dem</td><td>No answer </td><td>No answer       </td><td> 2</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>54</td><td>White</td><td>$25000 or more</td><td>Independent, near rep</td><td>Catholic  </td><td>Not applicable  </td><td> 3</td></tr>
	<tr><td>2014</td><td>Married      </td><td>62</td><td>White</td><td>$25000 or more</td><td>Independent, near rep</td><td>Protestant</td><td>Other           </td><td>NA</td></tr>
	<tr><td>2014</td><td>Never married</td><td>40</td><td>White</td><td>$1000 to 2999 </td><td>Republican, weak     </td><td>None      </td><td>Not applicable  </td><td> 2</td></tr>
	<tr><td>2014</td><td>Married      </td><td>33</td><td>White</td><td>Not applicable</td><td>Independent          </td><td>Christian </td><td>No denomination </td><td> 0</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>75</td><td>White</td><td>Don't know    </td><td>Republican, strong   </td><td>Protestant</td><td>Baptist-dk which</td><td> 4</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>89</td><td>White</td><td>Not applicable</td><td>Republican, weak     </td><td>Protestant</td><td>United methodist</td><td> 3</td></tr>
	<tr><td>2014</td><td>Divorced     </td><td>56</td><td>White</td><td>$25000 or more</td><td>Independent          </td><td>None      </td><td>Not applicable  </td><td> 4</td></tr>
	<tr><td>2014</td><td>Never married</td><td>24</td><td>White</td><td>$10000 - 14999</td><td>Independent, near dem</td><td>None      </td><td>Not applicable  </td><td> 4</td></tr>
	<tr><td>2014</td><td>Never married</td><td>27</td><td>White</td><td>$25000 or more</td><td>Democrat, weak       </td><td>Catholic  </td><td>Not applicable  </td><td>NA</td></tr>
	<tr><td>2014</td><td>Widowed      </td><td>71</td><td>White</td><td>$20000 - 24999</td><td>Independent, near rep</td><td>Protestant</td><td>Other           </td><td> 2</td></tr>
</tbody>
</table>




```R
gss_cat |>
  mutate(
    partyid = fct_collapse(partyid,
      "other" = c("No answer", "Don't know", "Other party"),
      "rep" = c("Strong republican", "Not str republican"),
      "ind" = c("Ind,near rep", "Independent", "Ind,near dem"),
      "dem" = c("Not str democrat", "Strong democrat")
    )
  ) |>
  count(partyid)
```


<table class="dataframe">
<caption>A tibble: 4 x 2</caption>
<thead>
	<tr><th scope=col>partyid</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>other</td><td> 548</td></tr>
	<tr><td>rep  </td><td>5346</td></tr>
	<tr><td>ind  </td><td>8409</td></tr>
	<tr><td>dem  </td><td>7180</td></tr>
</tbody>
</table>




```R
gss_cat |>
  mutate(relig = fct_lump_lowfreq(relig)) |>
  count(relig)
```


<table class="dataframe">
<caption>A tibble: 2 x 2</caption>
<thead>
	<tr><th scope=col>relig</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Protestant</td><td>10846</td></tr>
	<tr><td>Other     </td><td>10637</td></tr>
</tbody>
</table>




```R
gss_cat |>
  mutate(relig = fct_lump_n(relig, n = 10)) |>
  count(relig, sort = TRUE)
```


<table class="dataframe">
<caption>A tibble: 10 x 2</caption>
<thead>
	<tr><th scope=col>relig</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Protestant             </td><td>10846</td></tr>
	<tr><td>Catholic               </td><td> 5124</td></tr>
	<tr><td>None                   </td><td> 3523</td></tr>
	<tr><td>Christian              </td><td>  689</td></tr>
	<tr><td>Other                  </td><td>  458</td></tr>
	<tr><td>Jewish                 </td><td>  388</td></tr>
	<tr><td>Buddhism               </td><td>  147</td></tr>
	<tr><td>Inter-nondenominational</td><td>  109</td></tr>
	<tr><td>Moslem/islam           </td><td>  104</td></tr>
	<tr><td>Orthodox-christian     </td><td>   95</td></tr>
</tbody>
</table>



### Exercises
1. How have the proportions of people identifying as Democrat, Republican, and Independent changed over time?

2. How could you collapse rincome into a small set of categories?

3. Notice there are 9 groups (excluding other) in the fct_lump example above. Why not 10? (Hint: type ?fct_lump, and find the default for the argument other_level is “Other”.)



## 16.6 Ordered factors


```R
ordered(c("a", "b", "c"))
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>a</li><li>b</li><li>c</li></ol>

<details>
	<summary style=display:list-item;cursor:pointer>
		<strong>Levels</strong>:
	</summary>
	<style>
	.list-inline {list-style: none; margin:0; padding: 0}
	.list-inline>li {display: inline-block}
	.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
	</style>
	<ol class=list-inline><li>'a'</li><li>'b'</li><li>'c'</li></ol>
</details>


## 16.7 Summary

# C17. Dates and Times


```R
library(tidyverse)
library(nycflights13)
```

## 17.2 Creating date/times

**Year:** 
* `%Y`	4 digit year
* `%y`	2 digit year

**Month:**
* `%m`	Number
* `%b`	Abbreviated name
* `%B`	Full name

**Day:**
* `%d`	One or two digits
* `%e`	Two digits

**Time:**
* `%H`	24-hour hour
* `%I`	12-hour hour
* `%p`	AM/PM
* `%M`	Minutes
* `%S`	Seconds
* `%OS`	Seconds with decimal component
* `%Z`	Time zone name
* `%z`	Offset from UTC

**Others:**
* `%.`	Skip one non-digit
* `%*`	Skip any number of non-digits


```R
today()
now()
```


<time datetime="2024-03-12">2024-03-12</time>



    [1] "2024-03-12 11:34:12 AEST"


### During import


```R
csv <- "
  date
  01/02/15
"

read_csv(csv, col_types = cols(date = col_date("%m/%d/%y")))
read_csv(csv, col_types = cols(date = col_date("%d/%m/%y")))
read_csv(csv, col_types = cols(date = col_date("%y/%m/%d")))
```


<table class="dataframe">
<caption>A spec_tbl_df: 1 x 1</caption>
<thead>
	<tr><th scope=col>date</th></tr>
	<tr><th scope=col>&lt;date&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2015-01-02</td></tr>
</tbody>
</table>




<table class="dataframe">
<caption>A spec_tbl_df: 1 x 1</caption>
<thead>
	<tr><th scope=col>date</th></tr>
	<tr><th scope=col>&lt;date&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2015-02-01</td></tr>
</tbody>
</table>




<table class="dataframe">
<caption>A spec_tbl_df: 1 x 1</caption>
<thead>
	<tr><th scope=col>date</th></tr>
	<tr><th scope=col>&lt;date&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2001-02-15</td></tr>
</tbody>
</table>



### From strings


```R
ymd("2017-01-31")
mdy("January 31st, 2017")
dmy("31-Jan-2017")

ymd("2017-01-31", tz = "UTC")

```


<time datetime="2017-01-31">2017-01-31</time>



<time datetime="2017-01-31">2017-01-31</time>



<time datetime="2017-01-31">2017-01-31</time>



    [1] "2017-01-31 UTC"


### From individual components
* `make_date()`
* `make_datetime()`


```R
flights |> 
  select(year, month, day, hour, minute) |> 
  mutate(departure = make_datetime(year, month, day, hour, minute))
```


<table class="dataframe">
<caption>A tibble: 336776 x 6</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>departure</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>1</td><td>1</td><td>5</td><td>15</td><td>2013-01-01 05:15:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>5</td><td>29</td><td>2013-01-01 05:29:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>5</td><td>40</td><td>2013-01-01 05:40:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>5</td><td>45</td><td>2013-01-01 05:45:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>5</td><td>58</td><td>2013-01-01 05:58:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>5</td><td>59</td><td>2013-01-01 05:59:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td>10</td><td>2013-01-01 06:10:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 5</td><td>2013-01-01 06:05:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td>10</td><td>2013-01-01 06:10:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td>10</td><td>2013-01-01 06:10:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 7</td><td>2013-01-01 06:07:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td>10</td><td>2013-01-01 06:10:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td>15</td><td>2013-01-01 06:15:00</td></tr>
	<tr><td>2013</td><td>1</td><td>1</td><td>6</td><td>15</td><td>2013-01-01 06:15:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>25</td><td>2013-09-30 21:25:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>29</td><td>2013-09-30 21:29:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>30</td><td>2013-09-30 21:30:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>20</td><td>59</td><td>2013-09-30 20:59:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>40</td><td>2013-09-30 21:40:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>40</td><td>2013-09-30 21:40:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>29</td><td>2013-09-30 21:29:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>45</td><td>2013-09-30 21:45:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>37</td><td>2013-09-30 21:37:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>56</td><td>2013-09-30 21:56:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>59</td><td>2013-09-30 21:59:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>18</td><td>45</td><td>2013-09-30 18:45:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td> 5</td><td>2013-09-30 22:05:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>40</td><td>2013-09-30 21:40:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>20</td><td>59</td><td>2013-09-30 20:59:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td>45</td><td>2013-09-30 22:45:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>21</td><td>13</td><td>2013-09-30 21:13:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>20</td><td> 1</td><td>2013-09-30 20:01:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td>45</td><td>2013-09-30 22:45:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td>45</td><td>2013-09-30 22:45:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td>50</td><td>2013-09-30 22:50:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td>46</td><td>2013-09-30 22:46:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td>55</td><td>2013-09-30 22:55:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>23</td><td>59</td><td>2013-09-30 23:59:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>18</td><td>42</td><td>2013-09-30 18:42:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>14</td><td>55</td><td>2013-09-30 14:55:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>12</td><td>10</td><td>2013-09-30 12:10:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td>11</td><td>59</td><td>2013-09-30 11:59:00</td></tr>
	<tr><td>2013</td><td>9</td><td>30</td><td> 8</td><td>40</td><td>2013-09-30 08:40:00</td></tr>
</tbody>
</table>




```R
make_datetime_100 <- function(year, month, day, time) {
  make_datetime(year, month, day, time %/% 100, time %% 100)
}

flights_dt <- flights |> 
  filter(!is.na(dep_time), !is.na(arr_time)) |> 
  mutate(
    dep_time = make_datetime_100(year, month, day, dep_time),
    arr_time = make_datetime_100(year, month, day, arr_time),
    sched_dep_time = make_datetime_100(year, month, day, sched_dep_time),
    sched_arr_time = make_datetime_100(year, month, day, sched_arr_time)
  ) |> 
  select(origin, dest, ends_with("delay"), ends_with("time"))

flights_dt
```


<table class="dataframe">
<caption>A tibble: 328063 x 9</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>dest</th><th scope=col>dep_delay</th><th scope=col>arr_delay</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>air_time</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>EWR</td><td>IAH</td><td> 2</td><td> 11</td><td>2013-01-01 05:17:00</td><td>2013-01-01 05:15:00</td><td>2013-01-01 08:30:00</td><td>2013-01-01 08:19:00</td><td>227</td></tr>
	<tr><td>LGA</td><td>IAH</td><td> 4</td><td> 20</td><td>2013-01-01 05:33:00</td><td>2013-01-01 05:29:00</td><td>2013-01-01 08:50:00</td><td>2013-01-01 08:30:00</td><td>227</td></tr>
	<tr><td>JFK</td><td>MIA</td><td> 2</td><td> 33</td><td>2013-01-01 05:42:00</td><td>2013-01-01 05:40:00</td><td>2013-01-01 09:23:00</td><td>2013-01-01 08:50:00</td><td>160</td></tr>
	<tr><td>JFK</td><td>BQN</td><td>-1</td><td>-18</td><td>2013-01-01 05:44:00</td><td>2013-01-01 05:45:00</td><td>2013-01-01 10:04:00</td><td>2013-01-01 10:22:00</td><td>183</td></tr>
	<tr><td>LGA</td><td>ATL</td><td>-6</td><td>-25</td><td>2013-01-01 05:54:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:12:00</td><td>2013-01-01 08:37:00</td><td>116</td></tr>
	<tr><td>EWR</td><td>ORD</td><td>-4</td><td> 12</td><td>2013-01-01 05:54:00</td><td>2013-01-01 05:58:00</td><td>2013-01-01 07:40:00</td><td>2013-01-01 07:28:00</td><td>150</td></tr>
	<tr><td>EWR</td><td>FLL</td><td>-5</td><td> 19</td><td>2013-01-01 05:55:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 09:13:00</td><td>2013-01-01 08:54:00</td><td>158</td></tr>
	<tr><td>LGA</td><td>IAD</td><td>-3</td><td>-14</td><td>2013-01-01 05:57:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 07:09:00</td><td>2013-01-01 07:23:00</td><td> 53</td></tr>
	<tr><td>JFK</td><td>MCO</td><td>-3</td><td> -8</td><td>2013-01-01 05:57:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:38:00</td><td>2013-01-01 08:46:00</td><td>140</td></tr>
	<tr><td>LGA</td><td>ORD</td><td>-2</td><td>  8</td><td>2013-01-01 05:58:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 07:53:00</td><td>2013-01-01 07:45:00</td><td>138</td></tr>
	<tr><td>JFK</td><td>PBI</td><td>-2</td><td> -2</td><td>2013-01-01 05:58:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:49:00</td><td>2013-01-01 08:51:00</td><td>149</td></tr>
	<tr><td>JFK</td><td>TPA</td><td>-2</td><td> -3</td><td>2013-01-01 05:58:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:53:00</td><td>2013-01-01 08:56:00</td><td>158</td></tr>
	<tr><td>JFK</td><td>LAX</td><td>-2</td><td>  7</td><td>2013-01-01 05:58:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 09:24:00</td><td>2013-01-01 09:17:00</td><td>345</td></tr>
	<tr><td>EWR</td><td>SFO</td><td>-2</td><td>-14</td><td>2013-01-01 05:58:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 09:23:00</td><td>2013-01-01 09:37:00</td><td>361</td></tr>
	<tr><td>LGA</td><td>DFW</td><td>-1</td><td> 31</td><td>2013-01-01 05:59:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 09:41:00</td><td>2013-01-01 09:10:00</td><td>257</td></tr>
	<tr><td>JFK</td><td>BOS</td><td> 0</td><td> -4</td><td>2013-01-01 05:59:00</td><td>2013-01-01 05:59:00</td><td>2013-01-01 07:02:00</td><td>2013-01-01 07:06:00</td><td> 44</td></tr>
	<tr><td>EWR</td><td>LAS</td><td>-1</td><td> -8</td><td>2013-01-01 05:59:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:54:00</td><td>2013-01-01 09:02:00</td><td>337</td></tr>
	<tr><td>LGA</td><td>FLL</td><td> 0</td><td> -7</td><td>2013-01-01 06:00:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:51:00</td><td>2013-01-01 08:58:00</td><td>152</td></tr>
	<tr><td>LGA</td><td>ATL</td><td> 0</td><td> 12</td><td>2013-01-01 06:00:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:37:00</td><td>2013-01-01 08:25:00</td><td>134</td></tr>
	<tr><td>EWR</td><td>PBI</td><td> 1</td><td> -6</td><td>2013-01-01 06:01:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:44:00</td><td>2013-01-01 08:50:00</td><td>147</td></tr>
	<tr><td>LGA</td><td>MSP</td><td>-8</td><td> -8</td><td>2013-01-01 06:02:00</td><td>2013-01-01 06:10:00</td><td>2013-01-01 08:12:00</td><td>2013-01-01 08:20:00</td><td>170</td></tr>
	<tr><td>LGA</td><td>DTW</td><td>-3</td><td> 16</td><td>2013-01-01 06:02:00</td><td>2013-01-01 06:05:00</td><td>2013-01-01 08:21:00</td><td>2013-01-01 08:05:00</td><td>105</td></tr>
	<tr><td>EWR</td><td>MIA</td><td>-4</td><td>-12</td><td>2013-01-01 06:06:00</td><td>2013-01-01 06:10:00</td><td>2013-01-01 08:58:00</td><td>2013-01-01 09:10:00</td><td>152</td></tr>
	<tr><td>JFK</td><td>ATL</td><td>-4</td><td> -8</td><td>2013-01-01 06:06:00</td><td>2013-01-01 06:10:00</td><td>2013-01-01 08:37:00</td><td>2013-01-01 08:45:00</td><td>128</td></tr>
	<tr><td>EWR</td><td>MIA</td><td> 0</td><td>-17</td><td>2013-01-01 06:07:00</td><td>2013-01-01 06:07:00</td><td>2013-01-01 08:58:00</td><td>2013-01-01 09:15:00</td><td>157</td></tr>
	<tr><td>EWR</td><td>ORD</td><td> 8</td><td> 32</td><td>2013-01-01 06:08:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 08:07:00</td><td>2013-01-01 07:35:00</td><td>139</td></tr>
	<tr><td>JFK</td><td>SFO</td><td>11</td><td> 14</td><td>2013-01-01 06:11:00</td><td>2013-01-01 06:00:00</td><td>2013-01-01 09:45:00</td><td>2013-01-01 09:31:00</td><td>366</td></tr>
	<tr><td>JFK</td><td>RSW</td><td> 3</td><td>  4</td><td>2013-01-01 06:13:00</td><td>2013-01-01 06:10:00</td><td>2013-01-01 09:25:00</td><td>2013-01-01 09:21:00</td><td>175</td></tr>
	<tr><td>JFK</td><td>SJU</td><td> 0</td><td>-21</td><td>2013-01-01 06:15:00</td><td>2013-01-01 06:15:00</td><td>2013-01-01 10:39:00</td><td>2013-01-01 11:00:00</td><td>182</td></tr>
	<tr><td>EWR</td><td>ATL</td><td> 0</td><td> -9</td><td>2013-01-01 06:15:00</td><td>2013-01-01 06:15:00</td><td>2013-01-01 08:33:00</td><td>2013-01-01 08:42:00</td><td>120</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>LGA</td><td>DTW</td><td>  5</td><td> -9</td><td>2013-09-30 21:15:00</td><td>2013-09-30 21:10:00</td><td>2013-09-30 22:46:00</td><td>2013-09-30 22:55:00</td><td> 72</td></tr>
	<tr><td>EWR</td><td>SDF</td><td> -8</td><td>-20</td><td>2013-09-30 21:16:00</td><td>2013-09-30 21:24:00</td><td>2013-09-30 23:17:00</td><td>2013-09-30 23:37:00</td><td> 94</td></tr>
	<tr><td>EWR</td><td>MCI</td><td> 74</td><td> 58</td><td>2013-09-30 21:19:00</td><td>2013-09-30 20:05:00</td><td>2013-09-30 23:10:00</td><td>2013-09-30 22:12:00</td><td>147</td></tr>
	<tr><td>JFK</td><td>JAX</td><td> -1</td><td>-24</td><td>2013-09-30 21:19:00</td><td>2013-09-30 21:20:00</td><td>2013-09-30 23:30:00</td><td>2013-09-30 23:54:00</td><td>113</td></tr>
	<tr><td>JFK</td><td>LAX</td><td> 21</td><td>-25</td><td>2013-09-30 21:21:00</td><td>2013-09-30 21:00:00</td><td>2013-09-30 23:49:00</td><td>2013-09-30 00:14:00</td><td>296</td></tr>
	<tr><td>EWR</td><td>DCA</td><td> -5</td><td>-11</td><td>2013-09-30 21:22:00</td><td>2013-09-30 21:27:00</td><td>2013-09-30 22:26:00</td><td>2013-09-30 22:37:00</td><td> 35</td></tr>
	<tr><td>LGA</td><td>CHO</td><td> -2</td><td>-24</td><td>2013-09-30 21:23:00</td><td>2013-09-30 21:25:00</td><td>2013-09-30 22:23:00</td><td>2013-09-30 22:47:00</td><td> 45</td></tr>
	<tr><td>EWR</td><td>CLT</td><td> -2</td><td> -9</td><td>2013-09-30 21:27:00</td><td>2013-09-30 21:29:00</td><td>2013-09-30 23:14:00</td><td>2013-09-30 23:23:00</td><td> 72</td></tr>
	<tr><td>JFK</td><td>DEN</td><td> -2</td><td>-31</td><td>2013-09-30 21:28:00</td><td>2013-09-30 21:30:00</td><td>2013-09-30 23:28:00</td><td>2013-09-30 23:59:00</td><td>213</td></tr>
	<tr><td>LGA</td><td>RIC</td><td> 30</td><td> -2</td><td>2013-09-30 21:29:00</td><td>2013-09-30 20:59:00</td><td>2013-09-30 22:30:00</td><td>2013-09-30 22:32:00</td><td> 45</td></tr>
	<tr><td>JFK</td><td>DCA</td><td> -9</td><td>-30</td><td>2013-09-30 21:31:00</td><td>2013-09-30 21:40:00</td><td>2013-09-30 22:25:00</td><td>2013-09-30 22:55:00</td><td> 36</td></tr>
	<tr><td>JFK</td><td>LAX</td><td>  0</td><td>-30</td><td>2013-09-30 21:40:00</td><td>2013-09-30 21:40:00</td><td>2013-09-30 00:10:00</td><td>2013-09-30 00:40:00</td><td>298</td></tr>
	<tr><td>EWR</td><td>PWM</td><td> 13</td><td> 11</td><td>2013-09-30 21:42:00</td><td>2013-09-30 21:29:00</td><td>2013-09-30 22:50:00</td><td>2013-09-30 22:39:00</td><td> 47</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>  0</td><td>-25</td><td>2013-09-30 21:45:00</td><td>2013-09-30 21:45:00</td><td>2013-09-30 01:15:00</td><td>2013-09-30 01:40:00</td><td>192</td></tr>
	<tr><td>LGA</td><td>FLL</td><td> 10</td><td>  3</td><td>2013-09-30 21:47:00</td><td>2013-09-30 21:37:00</td><td>2013-09-30 00:30:00</td><td>2013-09-30 00:27:00</td><td>139</td></tr>
	<tr><td>EWR</td><td>BOS</td><td> -7</td><td>-23</td><td>2013-09-30 21:49:00</td><td>2013-09-30 21:56:00</td><td>2013-09-30 22:45:00</td><td>2013-09-30 23:08:00</td><td> 37</td></tr>
	<tr><td>EWR</td><td>MHT</td><td> -9</td><td>-16</td><td>2013-09-30 21:50:00</td><td>2013-09-30 21:59:00</td><td>2013-09-30 22:50:00</td><td>2013-09-30 23:06:00</td><td> 39</td></tr>
	<tr><td>JFK</td><td>BUF</td><td>194</td><td>194</td><td>2013-09-30 21:59:00</td><td>2013-09-30 18:45:00</td><td>2013-09-30 23:44:00</td><td>2013-09-30 20:30:00</td><td> 50</td></tr>
	<tr><td>LGA</td><td>BGR</td><td> -2</td><td>  8</td><td>2013-09-30 22:03:00</td><td>2013-09-30 22:05:00</td><td>2013-09-30 23:39:00</td><td>2013-09-30 23:31:00</td><td> 61</td></tr>
	<tr><td>LGA</td><td>BNA</td><td> 27</td><td>  7</td><td>2013-09-30 22:07:00</td><td>2013-09-30 21:40:00</td><td>2013-09-30 22:57:00</td><td>2013-09-30 22:50:00</td><td> 97</td></tr>
	<tr><td>EWR</td><td>STL</td><td> 72</td><td> 57</td><td>2013-09-30 22:11:00</td><td>2013-09-30 20:59:00</td><td>2013-09-30 23:39:00</td><td>2013-09-30 22:42:00</td><td>120</td></tr>
	<tr><td>JFK</td><td>PWM</td><td>-14</td><td>-21</td><td>2013-09-30 22:31:00</td><td>2013-09-30 22:45:00</td><td>2013-09-30 23:35:00</td><td>2013-09-30 23:56:00</td><td> 48</td></tr>
	<tr><td>EWR</td><td>SFO</td><td> 80</td><td> 42</td><td>2013-09-30 22:33:00</td><td>2013-09-30 21:13:00</td><td>2013-09-30 01:12:00</td><td>2013-09-30 00:30:00</td><td>318</td></tr>
	<tr><td>JFK</td><td>MCO</td><td>154</td><td>130</td><td>2013-09-30 22:35:00</td><td>2013-09-30 20:01:00</td><td>2013-09-30 00:59:00</td><td>2013-09-30 22:49:00</td><td>123</td></tr>
	<tr><td>JFK</td><td>BTV</td><td> -8</td><td> -8</td><td>2013-09-30 22:37:00</td><td>2013-09-30 22:45:00</td><td>2013-09-30 23:45:00</td><td>2013-09-30 23:53:00</td><td> 43</td></tr>
	<tr><td>JFK</td><td>SYR</td><td> -5</td><td>-17</td><td>2013-09-30 22:40:00</td><td>2013-09-30 22:45:00</td><td>2013-09-30 23:34:00</td><td>2013-09-30 23:51:00</td><td> 41</td></tr>
	<tr><td>JFK</td><td>BUF</td><td>-10</td><td>-20</td><td>2013-09-30 22:40:00</td><td>2013-09-30 22:50:00</td><td>2013-09-30 23:47:00</td><td>2013-09-30 00:07:00</td><td> 52</td></tr>
	<tr><td>JFK</td><td>ROC</td><td> -5</td><td>-16</td><td>2013-09-30 22:41:00</td><td>2013-09-30 22:46:00</td><td>2013-09-30 23:45:00</td><td>2013-09-30 00:01:00</td><td> 47</td></tr>
	<tr><td>JFK</td><td>BOS</td><td> 12</td><td>  1</td><td>2013-09-30 23:07:00</td><td>2013-09-30 22:55:00</td><td>2013-09-30 23:59:00</td><td>2013-09-30 23:58:00</td><td> 33</td></tr>
	<tr><td>JFK</td><td>PSE</td><td>-10</td><td>-25</td><td>2013-09-30 23:49:00</td><td>2013-09-30 23:59:00</td><td>2013-09-30 03:25:00</td><td>2013-09-30 03:50:00</td><td>196</td></tr>
</tbody>
</table>




```R
flights_dt |> 
  ggplot(aes(x = dep_time)) + 
  geom_freqpoly(binwidth = 86400) # 86400 seconds = 1 day
```


    
![png](R4DS-Transform_files/R4DS-Transform_96_0.png)
    



```R
# or within a single day
flights_dt |> 
  filter(dep_time < ymd(20130102)) |> 
  ggplot(aes(x = dep_time)) + 
  geom_freqpoly(binwidth = 600) # 600 s = 10 minutes
```


    
![png](R4DS-Transform_files/R4DS-Transform_97_0.png)
    


### From other types
* `as_date()`
* `as_datetime()`


```R
as_datetime(today())

as_date(now())
```


    [1] "2024-03-12 UTC"



<time datetime="2024-03-12">2024-03-12</time>



```R
as_datetime(86300)

as_date(365 * 10 + 2)
```


    [1] "1970-01-01 23:58:20 UTC"



<time datetime="1980-01-01">1980-01-01</time>


### Exercises


```R
today(tzone = "UTC")
```


<time datetime="2024-03-12">2024-03-12</time>


3. For each of the following date-times, show how you’d parse it using a readr column specification and a lubridate function.


```R
d1 <- "January 1, 2010"
d2 <- "2015-Mar-07"
d3 <- "06-Jun-2017"
d4 <- c("August 19 (2015)", "July 1 (2015)")
d5 <- "12/30/14" # Dec 30, 2014
t1 <- "1705"
t2 <- "11:15:10.12 PM"


mdy(d1)
as_date(d2)
dmy(d3)
mdy(d4)
mdy(d5)

as_datetime(as.numeric(t1))
hms(t2)


```


<time datetime="2010-01-01">2010-01-01</time>



<time datetime="2015-03-07">2015-03-07</time>



<time datetime="2017-06-06">2017-06-06</time>



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li><time datetime="2015-08-19">2015-08-19</time></li><li><time datetime="2015-07-01">2015-07-01</time></li></ol>




<time datetime="2014-12-30">2014-12-30</time>



    [1] "1970-01-01 00:28:25 UTC"



11H 15M 10.12S


## 17.3 Date-time components


```R
datetime <- ymd_hms(now())      # "2026-07-08 12:34:56"

year(datetime)
#> 2026
month(datetime)
#>  7
mday(datetime)
#>  8
yday(datetime)
#> 189
wday(datetime)
#> 4
```


2024



3



12



72



3



```R
flights_dt |> 
  mutate(wday = wday(dep_time, label = TRUE)) |> 
  ggplot(aes(x = wday)) +
  geom_bar()
```


    
![png](R4DS-Transform_files/R4DS-Transform_107_0.png)
    



```R
flights_dt |> 
  mutate(minute = minute(dep_time)) |> 
  group_by(minute) |> 
  summarize(
    avg_delay = mean(dep_delay, na.rm = TRUE),
    n = n()
  ) |> 
  ggplot(aes(x = minute, y = avg_delay)) +
  geom_line()
```


    
![png](R4DS-Transform_files/R4DS-Transform_108_0.png)
    



```R
sched_dep <- flights_dt |> 
  mutate(minute = minute(sched_dep_time)) |> 
  group_by(minute) |> 
  summarize(
    avg_delay = mean(arr_delay, na.rm = TRUE),
    n = n()
  )

ggplot(sched_dep, aes(x = minute, y = avg_delay)) +
  geom_line()
```


    
![png](R4DS-Transform_files/R4DS-Transform_109_0.png)
    



```R
flights_dt |> 
  mutate(dep_hour = hms::as_hms(dep_time - floor_date(dep_time, "day"))) |> 
  ggplot(aes(x = dep_hour)) +
  geom_freqpoly(binwidth = 60 * 30)
```


    
![png](R4DS-Transform_files/R4DS-Transform_110_0.png)
    


### Modify components



```R
datetime <- ymd_hms("2026-07-08 12:34:56")
datetime
year(datetime) <- 2030
datetime
month(datetime) <- 01
datetime
hour(datetime) <- hour(datetime) + 1
datetime

update(datetime, year = 2030, month = 2, mday = 2, hour = 2)
datetime
```


    [1] "2026-07-08 12:34:56 UTC"



    [1] "2030-07-08 12:34:56 UTC"



    [1] "2030-01-08 12:34:56 UTC"



    [1] "2030-01-08 13:34:56 UTC"



    [1] "2030-02-02 02:34:56 UTC"



    [1] "2030-01-08 13:34:56 UTC"


### Exercises

1. How does the distribution of flight times within a day change over the course of the year?
2. Compare dep_time, `sched_dep_time` and `dep_delay`. Are they consistent? Explain your findings.
3. Compare air_time with the duration between the departure and arrival. Explain your findings. (Hint: consider the location of the airport.)
4. How does the average delay time change over the course of a day? Should you use `dep_time` or `sched_dep_time`? Why?
5. On what day of the week should you leave if you want to minimise the chance of a delay?
6. What makes the distribution of `diamonds$carat` and `flights$sched_dep_time` similar?
7. Confirm our hypothesis that the early departures of flights in minutes 20-30 and 50-60 are caused by scheduled flights that leave early. Hint: create a binary variable that tells you whether or not a flight was delayed.



## 17.4 Time spans
* **Durations**, which represent an exact number of seconds.
* **Periods**, which represent human units like weeks and months.
* **Intervals**, which represent a starting and ending point.

### Duration


```R
# How old is Hadley?
h_age <- today() - ymd("1979-05-16")
h_age
```


    Time difference of 16372 days



```R
as.duration(h_age)
```


1414540800s (~44.82 years)



```R
dseconds(15)
dminutes(10)
dhours(c(12, 24))
ddays(0:5)
dweeks(3)
dyears(1)
```


15s



600s (~10 minutes)



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>43200s (~12 hours)</li><li>86400s (~1 days)</li></ol>




<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>0s</li><li>86400s (~1 days)</li><li>172800s (~2 days)</li><li>259200s (~3 days)</li><li>345600s (~4 days)</li><li>432000s (~5 days)</li></ol>




1814400s (~3 weeks)



31557600s (~1 years)



```R
# you can add and multiply durations:
2 * dyears(1)
dyears(1) + dweeks(12) + dhours(15)
## add and subtract durations to and from days

tomorrow <- today() + ddays(1)
last_year <- today() - dyears(1)
```


63115200s (~2 years)



38869200s (~1.23 years)



```R
one_am <- ymd_hms("2026-03-08 01:00:00", tz = "America/New_York")

one_am
# be careful with time zone (on that day timezone has changed)
one_am + ddays(1)
```


    [1] "2026-03-08 01:00:00 EST"



    [1] "2026-03-09 02:00:00 EDT"


### Periods


```R
one_am <- ymd_hms("2026-03-08 01:00:00", tz = "America/New_York")
hours(c(12, 24))

days(7)
months(1:6)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>12H 0M 0S</li><li>24H 0M 0S</li></ol>




7d 0H 0M 0S



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1m 0d 0H 0M 0S</li><li>2m 0d 0H 0M 0S</li><li>3m 0d 0H 0M 0S</li><li>4m 0d 0H 0M 0S</li><li>5m 0d 0H 0M 0S</li><li>6m 0d 0H 0M 0S</li></ol>




```R
10 * (months(6) + days(1))
days(50) + hours(25) + minutes(2)
```


60m 10d 0H 0M 0S



50d 25H 2M 0S



```R
# A leap year
ymd("2024-01-01") + dyears(1)
ymd("2024-01-01") + years(1)


# Daylight saving time
one_am + ddays(1)
one_am + days(1)

```


    [1] "2024-12-31 06:00:00 UTC"



<time datetime="2025-01-01">2025-01-01</time>



    [1] "2026-03-09 02:00:00 EDT"



    [1] "2026-03-09 01:00:00 EDT"



```R
flights_dt |> 
  filter(arr_time < dep_time) 
```


<table class="dataframe">
<caption>A tibble: 10633 x 9</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>dest</th><th scope=col>dep_delay</th><th scope=col>arr_delay</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>air_time</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>EWR</td><td>BQN</td><td>  9</td><td> -4</td><td>2013-01-01 19:29:00</td><td>2013-01-01 19:20:00</td><td>2013-01-01 00:03:00</td><td>2013-01-01 00:07:00</td><td>192</td></tr>
	<tr><td>JFK</td><td>DFW</td><td> 59</td><td> NA</td><td>2013-01-01 19:39:00</td><td>2013-01-01 18:40:00</td><td>2013-01-01 00:29:00</td><td>2013-01-01 21:51:00</td><td> NA</td></tr>
	<tr><td>EWR</td><td>TPA</td><td> -2</td><td>  9</td><td>2013-01-01 20:58:00</td><td>2013-01-01 21:00:00</td><td>2013-01-01 00:08:00</td><td>2013-01-01 23:59:00</td><td>159</td></tr>
	<tr><td>EWR</td><td>SJU</td><td> -6</td><td>-12</td><td>2013-01-01 21:02:00</td><td>2013-01-01 21:08:00</td><td>2013-01-01 01:46:00</td><td>2013-01-01 01:58:00</td><td>199</td></tr>
	<tr><td>EWR</td><td>SFO</td><td> 11</td><td>-14</td><td>2013-01-01 21:08:00</td><td>2013-01-01 20:57:00</td><td>2013-01-01 00:25:00</td><td>2013-01-01 00:39:00</td><td>354</td></tr>
	<tr><td>LGA</td><td>FLL</td><td>-10</td><td> -2</td><td>2013-01-01 21:20:00</td><td>2013-01-01 21:30:00</td><td>2013-01-01 00:16:00</td><td>2013-01-01 00:18:00</td><td>160</td></tr>
	<tr><td>EWR</td><td>MCO</td><td> 41</td><td> 43</td><td>2013-01-01 21:21:00</td><td>2013-01-01 20:40:00</td><td>2013-01-01 00:06:00</td><td>2013-01-01 23:23:00</td><td>143</td></tr>
	<tr><td>JFK</td><td>LAX</td><td> -7</td><td>-24</td><td>2013-01-01 21:28:00</td><td>2013-01-01 21:35:00</td><td>2013-01-01 00:26:00</td><td>2013-01-01 00:50:00</td><td>338</td></tr>
	<tr><td>EWR</td><td>FLL</td><td> 49</td><td> 28</td><td>2013-01-01 21:34:00</td><td>2013-01-01 20:45:00</td><td>2013-01-01 00:20:00</td><td>2013-01-01 23:52:00</td><td>152</td></tr>
	<tr><td>EWR</td><td>FLL</td><td> -9</td><td>-14</td><td>2013-01-01 21:36:00</td><td>2013-01-01 21:45:00</td><td>2013-01-01 00:25:00</td><td>2013-01-01 00:39:00</td><td>154</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>  5</td><td>-14</td><td>2013-01-01 21:40:00</td><td>2013-01-01 21:35:00</td><td>2013-01-01 02:10:00</td><td>2013-01-01 02:24:00</td><td>189</td></tr>
	<tr><td>JFK</td><td>MCO</td><td>  2</td><td>  2</td><td>2013-01-01 21:57:00</td><td>2013-01-01 21:55:00</td><td>2013-01-01 00:43:00</td><td>2013-01-01 00:41:00</td><td>140</td></tr>
	<tr><td>EWR</td><td>MIA</td><td>285</td><td>246</td><td>2013-01-01 22:05:00</td><td>2013-01-01 17:20:00</td><td>2013-01-01 00:46:00</td><td>2013-01-01 20:40:00</td><td>146</td></tr>
	<tr><td>JFK</td><td>PBI</td><td> 24</td><td> 21</td><td>2013-01-01 22:09:00</td><td>2013-01-01 21:45:00</td><td>2013-01-01 00:58:00</td><td>2013-01-01 00:37:00</td><td>143</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>-12</td><td>-26</td><td>2013-01-01 22:17:00</td><td>2013-01-01 22:29:00</td><td>2013-01-01 02:49:00</td><td>2013-01-01 03:15:00</td><td>191</td></tr>
	<tr><td>JFK</td><td>TPA</td><td> 47</td><td> 73</td><td>2013-01-01 22:17:00</td><td>2013-01-01 21:30:00</td><td>2013-01-01 01:40:00</td><td>2013-01-01 00:27:00</td><td>163</td></tr>
	<tr><td>JFK</td><td>FLL</td><td> 30</td><td> 49</td><td>2013-01-01 22:29:00</td><td>2013-01-01 21:59:00</td><td>2013-01-01 01:49:00</td><td>2013-01-01 01:00:00</td><td>153</td></tr>
	<tr><td>JFK</td><td>ROC</td><td> 21</td><td> 23</td><td>2013-01-01 23:06:00</td><td>2013-01-01 22:45:00</td><td>2013-01-01 00:28:00</td><td>2013-01-01 00:05:00</td><td> 59</td></tr>
	<tr><td>JFK</td><td>BTV</td><td> 22</td><td> 35</td><td>2013-01-01 23:07:00</td><td>2013-01-01 22:45:00</td><td>2013-01-01 00:32:00</td><td>2013-01-01 23:57:00</td><td> 59</td></tr>
	<tr><td>JFK</td><td>BUF</td><td> 15</td><td>  9</td><td>2013-01-01 23:10:00</td><td>2013-01-01 22:55:00</td><td>2013-01-01 00:24:00</td><td>2013-01-01 00:15:00</td><td> 57</td></tr>
	<tr><td>EWR</td><td>DCA</td><td>192</td><td>191</td><td>2013-01-01 23:12:00</td><td>2013-01-01 20:00:00</td><td>2013-01-01 00:21:00</td><td>2013-01-01 21:10:00</td><td> 44</td></tr>
	<tr><td>EWR</td><td>BTV</td><td> 83</td><td> 69</td><td>2013-01-01 23:23:00</td><td>2013-01-01 22:00:00</td><td>2013-01-01 00:22:00</td><td>2013-01-01 23:13:00</td><td> 44</td></tr>
	<tr><td>JFK</td><td>LAS</td><td>116</td><td> 73</td><td>2013-01-01 23:26:00</td><td>2013-01-01 21:30:00</td><td>2013-01-01 01:31:00</td><td>2013-01-01 00:18:00</td><td>290</td></tr>
	<tr><td>JFK</td><td>SYR</td><td> 37</td><td> 33</td><td>2013-01-01 23:27:00</td><td>2013-01-01 22:50:00</td><td>2013-01-01 00:32:00</td><td>2013-01-01 23:59:00</td><td> 45</td></tr>
	<tr><td>EWR</td><td>MCI</td><td>379</td><td>456</td><td>2013-01-01 23:43:00</td><td>2013-01-01 17:24:00</td><td>2013-01-01 03:14:00</td><td>2013-01-01 19:38:00</td><td>222</td></tr>
	<tr><td>JFK</td><td>PSE</td><td> -6</td><td>-20</td><td>2013-01-01 23:53:00</td><td>2013-01-01 23:59:00</td><td>2013-01-01 04:25:00</td><td>2013-01-01 04:45:00</td><td>195</td></tr>
	<tr><td>JFK</td><td>SJU</td><td> -6</td><td>-24</td><td>2013-01-01 23:53:00</td><td>2013-01-01 23:59:00</td><td>2013-01-01 04:18:00</td><td>2013-01-01 04:42:00</td><td>185</td></tr>
	<tr><td>JFK</td><td>BQN</td><td> -3</td><td>-12</td><td>2013-01-01 23:56:00</td><td>2013-01-01 23:59:00</td><td>2013-01-01 04:25:00</td><td>2013-01-01 04:37:00</td><td>186</td></tr>
	<tr><td>JFK</td><td>AUS</td><td>  5</td><td> 32</td><td>2013-01-02 20:30:00</td><td>2013-01-02 20:25:00</td><td>2013-01-02 00:13:00</td><td>2013-01-02 23:41:00</td><td>259</td></tr>
	<tr><td>EWR</td><td>AUS</td><td>  2</td><td> 17</td><td>2013-01-02 20:30:00</td><td>2013-01-02 20:28:00</td><td>2013-01-02 00:08:00</td><td>2013-01-02 23:51:00</td><td>252</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>JFK</td><td>SJU</td><td> 32</td><td> 25</td><td>2013-09-28 22:17:00</td><td>2013-09-28 21:45:00</td><td>2013-09-28 02:05:00</td><td>2013-09-28 01:40:00</td><td>213</td></tr>
	<tr><td>JFK</td><td>BTV</td><td> 10</td><td> 15</td><td>2013-09-28 22:55:00</td><td>2013-09-28 22:45:00</td><td>2013-09-28 00:08:00</td><td>2013-09-28 23:53:00</td><td> 48</td></tr>
	<tr><td>JFK</td><td>PSE</td><td> -8</td><td> 17</td><td>2013-09-28 23:51:00</td><td>2013-09-28 23:59:00</td><td>2013-09-28 04:07:00</td><td>2013-09-28 03:50:00</td><td>218</td></tr>
	<tr><td>JFK</td><td>SJU</td><td> -9</td><td>-21</td><td>2013-09-29 20:36:00</td><td>2013-09-29 20:45:00</td><td>2013-09-29 00:32:00</td><td>2013-09-29 00:53:00</td><td>212</td></tr>
	<tr><td>JFK</td><td>PDX</td><td> -1</td><td> 28</td><td>2013-09-29 20:54:00</td><td>2013-09-29 20:55:00</td><td>2013-09-29 00:27:00</td><td>2013-09-29 23:59:00</td><td>346</td></tr>
	<tr><td>JFK</td><td>LAX</td><td> -2</td><td>  3</td><td>2013-09-29 20:58:00</td><td>2013-09-29 21:00:00</td><td>2013-09-29 00:17:00</td><td>2013-09-29 00:14:00</td><td>326</td></tr>
	<tr><td>JFK</td><td>AUS</td><td>  5</td><td>  3</td><td>2013-09-29 20:59:00</td><td>2013-09-29 20:54:00</td><td>2013-09-29 00:01:00</td><td>2013-09-29 23:58:00</td><td>202</td></tr>
	<tr><td>JFK</td><td>SEA</td><td> -3</td><td>-11</td><td>2013-09-29 21:02:00</td><td>2013-09-29 21:05:00</td><td>2013-09-29 00:06:00</td><td>2013-09-29 00:17:00</td><td>336</td></tr>
	<tr><td>EWR</td><td>BQN</td><td> 37</td><td> 21</td><td>2013-09-29 21:32:00</td><td>2013-09-29 20:55:00</td><td>2013-09-29 01:17:00</td><td>2013-09-29 00:56:00</td><td>206</td></tr>
	<tr><td>JFK</td><td>LAX</td><td> -5</td><td>-34</td><td>2013-09-29 21:35:00</td><td>2013-09-29 21:40:00</td><td>2013-09-29 00:06:00</td><td>2013-09-29 00:40:00</td><td>295</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>  9</td><td> 11</td><td>2013-09-29 21:54:00</td><td>2013-09-29 21:45:00</td><td>2013-09-29 01:51:00</td><td>2013-09-29 01:40:00</td><td>208</td></tr>
	<tr><td>LGA</td><td>MCO</td><td> 64</td><td> 39</td><td>2013-09-29 22:04:00</td><td>2013-09-29 21:00:00</td><td>2013-09-29 00:23:00</td><td>2013-09-29 23:44:00</td><td>117</td></tr>
	<tr><td>JFK</td><td>DEN</td><td> 39</td><td>  3</td><td>2013-09-29 22:09:00</td><td>2013-09-29 21:30:00</td><td>2013-09-29 00:02:00</td><td>2013-09-29 23:59:00</td><td>208</td></tr>
	<tr><td>LGA</td><td>CVG</td><td> 73</td><td> 54</td><td>2013-09-29 22:23:00</td><td>2013-09-29 21:10:00</td><td>2013-09-29 00:13:00</td><td>2013-09-29 23:19:00</td><td> 87</td></tr>
	<tr><td>LGA</td><td>FLL</td><td> 47</td><td> 20</td><td>2013-09-29 22:24:00</td><td>2013-09-29 21:37:00</td><td>2013-09-29 00:47:00</td><td>2013-09-29 00:27:00</td><td>128</td></tr>
	<tr><td>EWR</td><td>MSP</td><td>131</td><td>110</td><td>2013-09-29 22:45:00</td><td>2013-09-29 20:34:00</td><td>2013-09-29 00:27:00</td><td>2013-09-29 22:37:00</td><td>141</td></tr>
	<tr><td>JFK</td><td>LAX</td><td>173</td><td>141</td><td>2013-09-29 22:53:00</td><td>2013-09-29 20:00:00</td><td>2013-09-29 01:21:00</td><td>2013-09-29 23:00:00</td><td>303</td></tr>
	<tr><td>JFK</td><td>DCA</td><td> 94</td><td> 76</td><td>2013-09-29 23:14:00</td><td>2013-09-29 21:40:00</td><td>2013-09-29 00:11:00</td><td>2013-09-29 22:55:00</td><td> 39</td></tr>
	<tr><td>JFK</td><td>PWM</td><td> 33</td><td> 19</td><td>2013-09-29 23:18:00</td><td>2013-09-29 22:45:00</td><td>2013-09-29 00:15:00</td><td>2013-09-29 23:56:00</td><td> 44</td></tr>
	<tr><td>LGA</td><td>RDU</td><td>144</td><td>124</td><td>2013-09-29 23:24:00</td><td>2013-09-29 21:00:00</td><td>2013-09-29 00:39:00</td><td>2013-09-29 22:35:00</td><td> 61</td></tr>
	<tr><td>LGA</td><td>FLL</td><td>225</td><td>183</td><td>2013-09-29 23:27:00</td><td>2013-09-29 19:42:00</td><td>2013-09-29 01:53:00</td><td>2013-09-29 22:50:00</td><td>129</td></tr>
	<tr><td>JFK</td><td>PSE</td><td> -3</td><td> -9</td><td>2013-09-29 23:56:00</td><td>2013-09-29 23:59:00</td><td>2013-09-29 03:41:00</td><td>2013-09-29 03:50:00</td><td>204</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>  5</td><td>-33</td><td>2013-09-30 20:50:00</td><td>2013-09-30 20:45:00</td><td>2013-09-30 00:20:00</td><td>2013-09-30 00:53:00</td><td>188</td></tr>
	<tr><td>JFK</td><td>PDX</td><td> 15</td><td> 52</td><td>2013-09-30 21:10:00</td><td>2013-09-30 20:55:00</td><td>2013-09-30 00:51:00</td><td>2013-09-30 23:59:00</td><td>361</td></tr>
	<tr><td>JFK</td><td>LAX</td><td>  0</td><td>-30</td><td>2013-09-30 21:40:00</td><td>2013-09-30 21:40:00</td><td>2013-09-30 00:10:00</td><td>2013-09-30 00:40:00</td><td>298</td></tr>
	<tr><td>JFK</td><td>SJU</td><td>  0</td><td>-25</td><td>2013-09-30 21:45:00</td><td>2013-09-30 21:45:00</td><td>2013-09-30 01:15:00</td><td>2013-09-30 01:40:00</td><td>192</td></tr>
	<tr><td>LGA</td><td>FLL</td><td> 10</td><td>  3</td><td>2013-09-30 21:47:00</td><td>2013-09-30 21:37:00</td><td>2013-09-30 00:30:00</td><td>2013-09-30 00:27:00</td><td>139</td></tr>
	<tr><td>EWR</td><td>SFO</td><td> 80</td><td> 42</td><td>2013-09-30 22:33:00</td><td>2013-09-30 21:13:00</td><td>2013-09-30 01:12:00</td><td>2013-09-30 00:30:00</td><td>318</td></tr>
	<tr><td>JFK</td><td>MCO</td><td>154</td><td>130</td><td>2013-09-30 22:35:00</td><td>2013-09-30 20:01:00</td><td>2013-09-30 00:59:00</td><td>2013-09-30 22:49:00</td><td>123</td></tr>
	<tr><td>JFK</td><td>PSE</td><td>-10</td><td>-25</td><td>2013-09-30 23:49:00</td><td>2013-09-30 23:59:00</td><td>2013-09-30 03:25:00</td><td>2013-09-30 03:50:00</td><td>196</td></tr>
</tbody>
</table>




```R
flights_dt <- flights_dt |> 
  mutate(
    overnight = arr_time < dep_time,
    arr_time = arr_time + days(overnight),
    sched_arr_time = sched_arr_time + days(overnight)
  )

flights_dt |> 
  filter(arr_time < dep_time) 
```


<table class="dataframe">
<caption>A tibble: 0 x 10</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>dest</th><th scope=col>dep_delay</th><th scope=col>arr_delay</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>air_time</th><th scope=col>overnight</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;lgl&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>



### Intervals


```R
dyears(1) / ddays(365) # 1 dyear is 365.25days
years(1) / days(1)
```


1.00068493150685



365.25



```R
y2023 <- ymd("2023-01-01") %--% ymd("2024-01-01")
y2024 <- ymd("2024-01-01") %--% ymd("2025-01-01")
```


```R
y2023 / days(1)
y2024 / days(1)
```


365



366


### Exercises
1. Explain days(!overnight) and days(overnight) to someone who has just started learning R. What is the key fact you need to know?

2. Create a vector of dates giving the first day of every month in 2015. Create a vector of dates giving the first day of every month in the current year.

3. Write a function that given your birthday (as a date), returns how old you are in years.

4. Why can’t `(today() %--% (today() + years(1))) / months(1)` work?


```R
(today() %--% (today() + years(1))) / months(1)
```


12


## 17.5 Time zones


```R
Sys.timezone()      # {area}/{location}: {continent}/{city} or {ocian}/{city}
```


'Australia/Brisbane'



```R
length(OlsonNames())
head(OlsonNames())
```


597



<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>'Africa/Abidjan'</li><li>'Africa/Accra'</li><li>'Africa/Addis_Ababa'</li><li>'Africa/Algiers'</li><li>'Africa/Asmara'</li><li>'Africa/Asmera'</li></ol>




```R
x1 <- ymd_hms("2024-06-01 12:00:00", tz = "America/New_York")
x1

x2 <- ymd_hms("2024-06-01 18:00:00", tz = "Europe/Copenhagen")
x2

x3 <- ymd_hms("2024-06-02 04:00:00", tz = "Pacific/Auckland")
x3

x1 - x2
#> Time difference of 0 secs
x1 - x3
#> Time difference of 0 secs
```


    [1] "2024-06-01 12:00:00 EDT"



    [1] "2024-06-01 18:00:00 CEST"



    [1] "2024-06-02 04:00:00 NZST"



    Time difference of 0 secs



    Time difference of 0 secs


You can change the time zone in two ways:

* Keep the instant in time the same, and change how it’s displayed. Use this when the instant is correct, but you want a more natural display.
* Change the underlying instant in time. Use this when you have an instant that has been labelled with the incorrect time zone, and you need to fix it.


```R
x4 <- c(x1, x2, x3)
x4
x4a <- with_tz(x4, tzone = "Australia/Lord_Howe")
x4a

x4a - x4
```


    [1] "2024-06-01 12:00:00 EDT" "2024-06-01 12:00:00 EDT"
    [3] "2024-06-01 12:00:00 EDT"



    [1] "2024-06-02 02:30:00 +1030" "2024-06-02 02:30:00 +1030"
    [3] "2024-06-02 02:30:00 +1030"



    Time differences in secs
    [1] 0 0 0



```R
x4b <- force_tz(x4, tzone = "Australia/Lord_Howe")
x4b

x4b - x4
```


    [1] "2024-06-01 12:00:00 +1030" "2024-06-01 12:00:00 +1030"
    [3] "2024-06-01 12:00:00 +1030"



    Time differences in hours
    [1] -14.5 -14.5 -14.5


# C18. Missing Values


```R
library(tidyverse)
```

## 18.2 Explicit missing values

* Last observation carried forward (repeated)
* Fixed values


```R
treatment <- tribble(
  ~person,           ~treatment, ~response,
  "Derrick Whitmore", 1,         7,
  NA,                 2,         10,
  NA,                 3,         NA,
  "Katherine Burke",  1,         4
)
```


```R
treatment |>
  fill(everything())        # method: last observation carried forward!

```


<table class="dataframe">
<caption>A tibble: 4 x 3</caption>
<thead>
	<tr><th scope=col>person</th><th scope=col>treatment</th><th scope=col>response</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Derrick Whitmore</td><td>1</td><td> 7</td></tr>
	<tr><td>Derrick Whitmore</td><td>2</td><td>10</td></tr>
	<tr><td>Derrick Whitmore</td><td>3</td><td>10</td></tr>
	<tr><td>Katherine Burke </td><td>1</td><td> 4</td></tr>
</tbody>
</table>




```R
x <- c(1, 4, 5, 7, NA)
coalesce(x, 0)
```


<style>
.list-inline {list-style: none; margin:0; padding: 0}
.list-inline>li {display: inline-block}
.list-inline>li:not(:last-child)::after {content: "\00b7"; padding: 0 .5ex}
</style>
<ol class=list-inline><li>1</li><li>4</li><li>5</li><li>7</li><li>0</li></ol>



## 18.3 Implicit missing values
An explicit missing value is the presence of an absence.

An implicit missing value is the absence of a presence.


```R
stocks <- tibble(
  year  = c(2020, 2020, 2020, 2020, 2021, 2021, 2021),
  qtr   = c(   1,    2,    3,    4,    2,    3,    4),
  price = c(1.88, 0.59, 0.35,   NA, 0.92, 0.17, 2.66)
)
```

### Pivoting
Making data wider can make implicit missing values explicit because every combination of the rows and new columns must have some value. 


```R
stocks |>
  pivot_wider(
    names_from = qtr, 
    values_from = price
  )
```


<table class="dataframe">
<caption>A tibble: 2 x 5</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>1</th><th scope=col>2</th><th scope=col>3</th><th scope=col>4</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2020</td><td>1.88</td><td>0.59</td><td>0.35</td><td>  NA</td></tr>
	<tr><td>2021</td><td>  NA</td><td>0.92</td><td>0.17</td><td>2.66</td></tr>
</tbody>
</table>



### Complete

tidyr::complete() allows you to generate explicit missing values by providing a set of variables that define the combination of rows that should exist. 


```R
stocks |>
  complete(year, qtr)
```


<table class="dataframe">
<caption>A tibble: 8 x 3</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>qtr</th><th scope=col>price</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2020</td><td>1</td><td>1.88</td></tr>
	<tr><td>2020</td><td>2</td><td>0.59</td></tr>
	<tr><td>2020</td><td>3</td><td>0.35</td></tr>
	<tr><td>2020</td><td>4</td><td>  NA</td></tr>
	<tr><td>2021</td><td>1</td><td>  NA</td></tr>
	<tr><td>2021</td><td>2</td><td>0.92</td></tr>
	<tr><td>2021</td><td>3</td><td>0.17</td></tr>
	<tr><td>2021</td><td>4</td><td>2.66</td></tr>
</tbody>
</table>




```R
stocks |>
  complete(year = 2019:2021, qtr)
```


<table class="dataframe">
<caption>A tibble: 12 x 3</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>qtr</th><th scope=col>price</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2019</td><td>1</td><td>  NA</td></tr>
	<tr><td>2019</td><td>2</td><td>  NA</td></tr>
	<tr><td>2019</td><td>3</td><td>  NA</td></tr>
	<tr><td>2019</td><td>4</td><td>  NA</td></tr>
	<tr><td>2020</td><td>1</td><td>1.88</td></tr>
	<tr><td>2020</td><td>2</td><td>0.59</td></tr>
	<tr><td>2020</td><td>3</td><td>0.35</td></tr>
	<tr><td>2020</td><td>4</td><td>  NA</td></tr>
	<tr><td>2021</td><td>1</td><td>  NA</td></tr>
	<tr><td>2021</td><td>2</td><td>0.92</td></tr>
	<tr><td>2021</td><td>3</td><td>0.17</td></tr>
	<tr><td>2021</td><td>4</td><td>2.66</td></tr>
</tbody>
</table>



### Joins
In some cases, the complete set of observations can’t be generated by a simple combination of variables. In that case, you can do manually what complete() does for you: create a data frame that contains all the rows that should exist (using whatever combination of techniques you need), then combine it with your original dataset with `dplyr::full_join()`.

`dplyr::anti_join(x, y)` is a particularly useful tool , it selects only the rows in x that don’t have a match in y


```R
flights |> 
  distinct(faa = dest) |> 
  anti_join(airports)
```

    [1m[22mJoining with `by = join_by(faa)`



<table class="dataframe">
<caption>A tibble: 4 x 1</caption>
<thead>
	<tr><th scope=col>faa</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>BQN</td></tr>
	<tr><td>SJU</td></tr>
	<tr><td>STT</td></tr>
	<tr><td>PSE</td></tr>
</tbody>
</table>




```R
flights |> 
  distinct(tailnum) |> 
  anti_join(planes)
```

    [1m[22mJoining with `by = join_by(tailnum)`



<table class="dataframe">
<caption>A tibble: 722 x 1</caption>
<thead>
	<tr><th scope=col>tailnum</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>N3ALAA</td></tr>
	<tr><td>N3DUAA</td></tr>
	<tr><td>N542MQ</td></tr>
	<tr><td>N730MQ</td></tr>
	<tr><td>N9EAMQ</td></tr>
	<tr><td>N532UA</td></tr>
	<tr><td>N3EMAA</td></tr>
	<tr><td>N518MQ</td></tr>
	<tr><td>N3BAAA</td></tr>
	<tr><td>N3CYAA</td></tr>
	<tr><td>N426US</td></tr>
	<tr><td>N3GKAA</td></tr>
	<tr><td>N4WNAA</td></tr>
	<tr><td>N5FMAA</td></tr>
	<tr><td>N722MQ</td></tr>
	<tr><td>N3EKAA</td></tr>
	<tr><td>N3ETAA</td></tr>
	<tr><td>N541AA</td></tr>
	<tr><td>N4WRAA</td></tr>
	<tr><td>N4WPAA</td></tr>
	<tr><td>N508MQ</td></tr>
	<tr><td>N3HMAA</td></tr>
	<tr><td>N828MQ</td></tr>
	<tr><td>N3GEAA</td></tr>
	<tr><td>N739MQ</td></tr>
	<tr><td>N531MQ</td></tr>
	<tr><td>N527JB</td></tr>
	<tr><td>N846MQ</td></tr>
	<tr><td>N3GVAA</td></tr>
	<tr><td>N4YCAA</td></tr>
	<tr><td>...</td></tr>
	<tr><td>N7BAAA</td></tr>
	<tr><td>N7BVAA</td></tr>
	<tr><td>N626MQ</td></tr>
	<tr><td>N675MQ</td></tr>
	<tr><td>N580AA</td></tr>
	<tr><td>N717MQ</td></tr>
	<tr><td>N738MQ</td></tr>
	<tr><td>N720MQ</td></tr>
	<tr><td>N7ASAA</td></tr>
	<tr><td>N328AT</td></tr>
	<tr><td>N735MQ</td></tr>
	<tr><td>N5EDAA</td></tr>
	<tr><td>N5DJAA</td></tr>
	<tr><td>N7ALAA</td></tr>
	<tr><td>N721MQ</td></tr>
	<tr><td>N7BGAA</td></tr>
	<tr><td>N5ESAA</td></tr>
	<tr><td>N456UW</td></tr>
	<tr><td>N838MQ</td></tr>
	<tr><td>N442US</td></tr>
	<tr><td>N502SW</td></tr>
	<tr><td>N451UW</td></tr>
	<tr><td>N7BKAA</td></tr>
	<tr><td>N800MQ</td></tr>
	<tr><td>N7CAAA</td></tr>
	<tr><td>N823MQ</td></tr>
	<tr><td>N5FCAA</td></tr>
	<tr><td>N5ERAA</td></tr>
	<tr><td>N654MQ</td></tr>
	<tr><td>N647MQ</td></tr>
</tbody>
</table>



### Exercises

1. Can you find any relationship between the carrier and the rows that appear to be missing from planes?

## 18.4 Factors and empty groups


```R
health <- tibble(
  name   = c("Ikaia", "Oletta", "Leriah", "Dashay", "Tresaun"),
  smoker = factor(c("no", "no", "no", "no", "no"), levels = c("yes", "no")),
  age    = c(34, 88, 75, 47, 56),
)
```


```R
health |> count(smoker)
```


<table class="dataframe">
<caption>A tibble: 1 x 2</caption>
<thead>
	<tr><th scope=col>smoker</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>no</td><td>5</td></tr>
</tbody>
</table>




```R
# We can request count() to keep all the groups, even those not seen in the data by using .drop = FALSE:
health |> count(smoker, .drop = FALSE)
```


<table class="dataframe">
<caption>A tibble: 2 x 2</caption>
<thead>
	<tr><th scope=col>smoker</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>yes</td><td>0</td></tr>
	<tr><td>no </td><td>5</td></tr>
</tbody>
</table>




```R
p1 <- ggplot(health, aes(x = smoker)) +
  geom_bar() +
  scale_x_discrete()

p2 <- ggplot(health, aes(x = smoker)) +
  geom_bar() +
  scale_x_discrete(drop = FALSE)

options(repr.plot.width = 10, repr.plot.height = 5)
grid.arrange(p1, p2, ncol=2)

```


    
![png](R4DS-Transform_files/R4DS-Transform_160_0.png)
    



```R
health |> 
  group_by(smoker, .drop = FALSE) |> 
  summarize(
    n = n(),
    mean_age = mean(age),
    min_age = min(age),
    max_age = max(age),
    sd_age = sd(age)
  )
```

    Warning message:
    "[1m[22mThere were 2 warnings in `summarize()`.
    The first warning was:
    [1m[22m[36mi[39m In argument: `min_age = min(age)`.
    [36mi[39m In group 1: `smoker = yes`.
    Caused by warning in `min()`:
    [33m![39m no non-missing arguments to min; returning Inf
    [1m[22m[36mi[39m Run `dplyr::last_dplyr_warnings()` to see the 1 remaining warning."



<table class="dataframe">
<caption>A tibble: 2 x 6</caption>
<thead>
	<tr><th scope=col>smoker</th><th scope=col>n</th><th scope=col>mean_age</th><th scope=col>min_age</th><th scope=col>max_age</th><th scope=col>sd_age</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>yes</td><td>0</td><td>NaN</td><td>Inf</td><td>-Inf</td><td>      NA</td></tr>
	<tr><td>no </td><td>5</td><td> 60</td><td> 34</td><td>  88</td><td>21.62175</td></tr>
</tbody>
</table>




```R
health |> 
  group_by(smoker) |> 
  summarize(
    n = n(),
    mean_age = mean(age),
    min_age = min(age),
    max_age = max(age),
    sd_age = sd(age)
  ) |> 
  complete(smoker)
```


<table class="dataframe">
<caption>A tibble: 2 x 6</caption>
<thead>
	<tr><th scope=col>smoker</th><th scope=col>n</th><th scope=col>mean_age</th><th scope=col>min_age</th><th scope=col>max_age</th><th scope=col>sd_age</th></tr>
	<tr><th scope=col>&lt;fct&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>yes</td><td>NA</td><td>NA</td><td>NA</td><td>NA</td><td>      NA</td></tr>
	<tr><td>no </td><td> 5</td><td>60</td><td>34</td><td>88</td><td>21.62175</td></tr>
</tbody>
</table>



# C19. Joins

Typically you have many data frames, and you must join them together to answer the questions that you’re interested in. This chapter will introduce you to two important types of joins:

1. **Mutating joins**, which add new variables to one data frame from matching observations in another.
2. **Filtering joins**, which filter observations from one data frame based on whether or not they match an observation in another.


```R
library(tidyverse)
library(nycflights13)
```

## 19.2 Keys

### Primary and foreign keys
* A primary key is a variable or set of variables that uniquely identifies each observation. When more than one variable is needed, the key is called a compound key. 
* A foreign key is a variable (or set of variables) that corresponds to a primary key in another table.

For examples:
 * `carrier` and `faa`, `tailnum` are primary key of corresponding tables `airlines`, `airports`, `planes`
 * `origin` and `time_hour `are the compound primary key of the table `weather`
* `flights$tailnum `is a foreign key that corresponds to the primary key `planes$tailnum`.
* `flights$carrier `is a foreign key that corresponds to the primary key `airlines$carrier`.
* `flights$origin `is a foreign key that corresponds to the primary key `airports$faa`.
* `flights$dest `is a foreign key that corresponds to the primary key `airports$faa`.
* `flights$origin-flights$time_hour` is a compound foreign key that corresponds to the compound primary key `weather$origin-weather$time_hour`.



```R
airlines
```


<table class="dataframe">
<caption>A tibble: 16 x 2</caption>
<thead>
	<tr><th scope=col>carrier</th><th scope=col>name</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>9E</td><td>Endeavor Air Inc.          </td></tr>
	<tr><td>AA</td><td>American Airlines Inc.     </td></tr>
	<tr><td>AS</td><td>Alaska Airlines Inc.       </td></tr>
	<tr><td>B6</td><td>JetBlue Airways            </td></tr>
	<tr><td>DL</td><td>Delta Air Lines Inc.       </td></tr>
	<tr><td>EV</td><td>ExpressJet Airlines Inc.   </td></tr>
	<tr><td>F9</td><td>Frontier Airlines Inc.     </td></tr>
	<tr><td>FL</td><td>AirTran Airways Corporation</td></tr>
	<tr><td>HA</td><td>Hawaiian Airlines Inc.     </td></tr>
	<tr><td>MQ</td><td>Envoy Air                  </td></tr>
	<tr><td>OO</td><td>SkyWest Airlines Inc.      </td></tr>
	<tr><td>UA</td><td>United Air Lines Inc.      </td></tr>
	<tr><td>US</td><td>US Airways Inc.            </td></tr>
	<tr><td>VX</td><td>Virgin America             </td></tr>
	<tr><td>WN</td><td>Southwest Airlines Co.     </td></tr>
	<tr><td>YV</td><td>Mesa Airlines Inc.         </td></tr>
</tbody>
</table>




```R
airports
```


<table class="dataframe">
<caption>A tibble: 1458 x 8</caption>
<thead>
	<tr><th scope=col>faa</th><th scope=col>name</th><th scope=col>lat</th><th scope=col>lon</th><th scope=col>alt</th><th scope=col>tz</th><th scope=col>dst</th><th scope=col>tzone</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>04G</td><td>Lansdowne Airport                   </td><td>41.13047</td><td> -80.61958</td><td>1044</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>06A</td><td>Moton Field Municipal Airport       </td><td>32.46057</td><td> -85.68003</td><td> 264</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>06C</td><td>Schaumburg Regional                 </td><td>41.98934</td><td> -88.10124</td><td> 801</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>06N</td><td>Randall Airport                     </td><td>41.43191</td><td> -74.39156</td><td> 523</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>09J</td><td>Jekyll Island Airport               </td><td>31.07447</td><td> -81.42778</td><td>  11</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>0A9</td><td>Elizabethton Municipal Airport      </td><td>36.37122</td><td> -82.17342</td><td>1593</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>0G6</td><td>Williams County Airport             </td><td>41.46731</td><td> -84.50678</td><td> 730</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>0G7</td><td>Finger Lakes Regional Airport       </td><td>42.88356</td><td> -76.78123</td><td> 492</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>0P2</td><td>Shoestring Aviation Airfield        </td><td>39.79482</td><td> -76.64719</td><td>1000</td><td>-5</td><td>U</td><td>America/New_York   </td></tr>
	<tr><td>0S9</td><td>Jefferson County Intl               </td><td>48.05381</td><td>-122.81064</td><td> 108</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>0W3</td><td>Harford County Airport              </td><td>39.56684</td><td> -76.20240</td><td> 409</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>10C</td><td>Galt Field Airport                  </td><td>42.40289</td><td> -88.37511</td><td> 875</td><td>-6</td><td>U</td><td>America/Chicago    </td></tr>
	<tr><td>17G</td><td>Port Bucyrus-Crawford County Airport</td><td>40.78156</td><td> -82.97481</td><td>1003</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>19A</td><td>Jackson County Airport              </td><td>34.17586</td><td> -83.56160</td><td> 951</td><td>-5</td><td>U</td><td>America/New_York   </td></tr>
	<tr><td>1A3</td><td>Martin Campbell Field Airport       </td><td>35.01581</td><td> -84.34683</td><td>1789</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>1B9</td><td>Mansfield Municipal                 </td><td>42.00013</td><td> -71.19677</td><td> 122</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>1C9</td><td>Frazier Lake Airpark                </td><td>54.01333</td><td>-124.76833</td><td> 152</td><td>-8</td><td>A</td><td>America/Vancouver  </td></tr>
	<tr><td>1CS</td><td>Clow International Airport          </td><td>41.69597</td><td> -88.12923</td><td> 670</td><td>-6</td><td>U</td><td>America/Chicago    </td></tr>
	<tr><td>1G3</td><td>Kent State Airport                  </td><td>41.15139</td><td> -81.41511</td><td>1134</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>1G4</td><td>Grand Canyon West Airport           </td><td>35.89990</td><td>-113.81567</td><td>4813</td><td>-7</td><td>A</td><td>America/Phoenix    </td></tr>
	<tr><td>1H2</td><td>Effingham Memorial Airport          </td><td>39.07000</td><td> -88.53400</td><td> 585</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>1OH</td><td>Fortman Airport                     </td><td>40.55533</td><td> -84.38662</td><td> 885</td><td>-5</td><td>U</td><td>America/New_York   </td></tr>
	<tr><td>1RL</td><td>Point Roberts Airpark               </td><td>48.97972</td><td>-123.07889</td><td>  10</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>23M</td><td>Clarke CO                           </td><td>32.05170</td><td> -88.44340</td><td> 320</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>24C</td><td>Lowell City Airport                 </td><td>42.95392</td><td> -85.34391</td><td> 681</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>24J</td><td>Suwannee County Airport             </td><td>30.30013</td><td> -83.02469</td><td> 104</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>25D</td><td>Forest Lake Airport                 </td><td>45.24775</td><td> -92.99439</td><td> 925</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>29D</td><td>Grove City Airport                  </td><td>41.14603</td><td> -80.16775</td><td>1371</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>2A0</td><td>Mark Anton Airport                  </td><td>35.48625</td><td> -84.93108</td><td> 718</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>2B2</td><td>Plum Island Airport                 </td><td>42.79536</td><td> -70.83944</td><td>  11</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>X59</td><td>Valkaria Municipal                  </td><td>27.96086</td><td> -80.55833</td><td>  26</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>XFL</td><td>Flagler County Airport              </td><td>29.28210</td><td> -81.12120</td><td>  33</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>XNA</td><td>NW Arkansas Regional                </td><td>36.28187</td><td> -94.30681</td><td>1287</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>XZK</td><td>Amherst Amtrak Station AMM          </td><td>42.37500</td><td> -72.51139</td><td> 258</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>Y51</td><td>Municipal Airport                   </td><td>43.57936</td><td> -90.89647</td><td>1292</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>Y72</td><td>Bloyer Field                        </td><td>43.97622</td><td> -90.48061</td><td> 966</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>YAK</td><td>Yakutat                             </td><td>59.30120</td><td>-139.39370</td><td>  33</td><td>-9</td><td>A</td><td>NA                 </td></tr>
	<tr><td>YIP</td><td>Willow Run                          </td><td>42.23793</td><td> -83.53041</td><td> 716</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>YKM</td><td>Yakima Air Terminal McAllister Field</td><td>46.56820</td><td>-120.54400</td><td>1095</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>YKN</td><td>Chan Gurney                         </td><td>42.87110</td><td> -97.39690</td><td>1200</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>YNG</td><td>Youngstown Warren Rgnl              </td><td>41.26074</td><td> -80.67910</td><td>1196</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>YUM</td><td>Yuma Mcas Yuma Intl                 </td><td>32.65658</td><td>-114.60598</td><td> 216</td><td>-7</td><td>N</td><td>America/Phoenix    </td></tr>
	<tr><td>Z84</td><td>Clear                               </td><td>64.30120</td><td>-149.12014</td><td> 552</td><td>-9</td><td>A</td><td>America/Anchorage  </td></tr>
	<tr><td>ZBP</td><td>Penn Station                        </td><td>39.30722</td><td> -76.61556</td><td>  66</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZFV</td><td>Philadelphia 30th St Station        </td><td>39.95570</td><td> -75.18200</td><td>   0</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZPH</td><td>Municipal Airport                   </td><td>28.22806</td><td> -82.15583</td><td>  90</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZRA</td><td>Atlantic City Rail Terminal         </td><td>39.36650</td><td> -74.44200</td><td>   8</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZRD</td><td>Train Station                       </td><td>37.53430</td><td> -77.42945</td><td>  26</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZRP</td><td>Newark Penn Station                 </td><td>40.73472</td><td> -74.16417</td><td>   0</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZRT</td><td>Hartford Union Station              </td><td>41.76888</td><td> -72.68150</td><td>   0</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZRZ</td><td>New Carrollton Rail Station         </td><td>38.94800</td><td> -76.87190</td><td>  39</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZSF</td><td>Springfield Amtrak Station          </td><td>42.10600</td><td> -72.59305</td><td>  65</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZSY</td><td>Scottsdale Airport                  </td><td>33.62289</td><td>-111.91053</td><td>1519</td><td>-7</td><td>A</td><td>America/Phoenix    </td></tr>
	<tr><td>ZTF</td><td>Stamford Amtrak Station             </td><td>41.04694</td><td> -73.54149</td><td>   0</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZTY</td><td>Boston Back Bay Station             </td><td>42.34780</td><td> -71.07500</td><td>  20</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZUN</td><td>Black Rock                          </td><td>35.08323</td><td>-108.79178</td><td>6454</td><td>-7</td><td>A</td><td>America/Denver     </td></tr>
	<tr><td>ZVE</td><td>New Haven Rail Station              </td><td>41.29867</td><td> -72.92599</td><td>   7</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZWI</td><td>Wilmington Amtrak Station           </td><td>39.73667</td><td> -75.55167</td><td>   0</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZWU</td><td>Washington Union Station            </td><td>38.89746</td><td> -77.00643</td><td>  76</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ZYP</td><td>Penn Station                        </td><td>40.75050</td><td> -73.99350</td><td>  35</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
</tbody>
</table>




```R
planes
```


<table class="dataframe">
<caption>A tibble: 3322 x 9</caption>
<thead>
	<tr><th scope=col>tailnum</th><th scope=col>year</th><th scope=col>type</th><th scope=col>manufacturer</th><th scope=col>model</th><th scope=col>engines</th><th scope=col>seats</th><th scope=col>speed</th><th scope=col>engine</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>N10156</td><td>2004</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N102UW</td><td>1998</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N103US</td><td>1999</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N104UW</td><td>1999</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N10575</td><td>2002</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145LR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N105UW</td><td>1999</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N107US</td><td>1999</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N108UW</td><td>1999</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N109UW</td><td>1999</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N110UW</td><td>1999</td><td>Fixed wing multi engine</td><td>AIRBUS INDUSTRIE</td><td>A320-214 </td><td>2</td><td>182</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11106</td><td>2002</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11107</td><td>2002</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11109</td><td>2002</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11113</td><td>2002</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11119</td><td>2002</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11121</td><td>2003</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11127</td><td>2003</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11137</td><td>2003</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11140</td><td>2003</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11150</td><td>2003</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11155</td><td>2004</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11164</td><td>2004</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11165</td><td>2004</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11176</td><td>2004</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11181</td><td>2005</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11184</td><td>2005</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11187</td><td>2005</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11189</td><td>2005</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11191</td><td>2005</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N11192</td><td>2005</td><td>Fixed wing multi engine</td><td>EMBRAER         </td><td>EMB-145XR</td><td>2</td><td> 55</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>N984DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N985AT</td><td>2001</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N985DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N986AT</td><td>2001</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N986DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N987AT</td><td>2001</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N987DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N988AT</td><td>2001</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N988DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N989AT</td><td>2001</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N989DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N990AT</td><td>2001</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N990DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N991AT</td><td>  NA</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N991DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N992AT</td><td>2002</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N992DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N993AT</td><td>2002</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N993DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N994AT</td><td>2002</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N994DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS CORPORATION</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-jet</td></tr>
	<tr><td>N995AT</td><td>2002</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N995DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N996AT</td><td>2002</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N996DL</td><td>1991</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N997AT</td><td>2002</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N997DL</td><td>1992</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS AIRCRAFT CO</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N998AT</td><td>2002</td><td>Fixed wing multi engine</td><td>BOEING                       </td><td>717-200</td><td>2</td><td>100</td><td>NA</td><td>Turbo-fan</td></tr>
	<tr><td>N998DL</td><td>1992</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS CORPORATION</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-jet</td></tr>
	<tr><td>N999DN</td><td>1992</td><td>Fixed wing multi engine</td><td>MCDONNELL DOUGLAS CORPORATION</td><td>MD-88  </td><td>2</td><td>142</td><td>NA</td><td>Turbo-jet</td></tr>
</tbody>
</table>



![The data relationships](https://r4ds.hadley.nz/diagrams/relational.png){width=75%}

### Checking primary keys


```R
planes |> 
  count(tailnum) |> 
  filter(n > 1)

weather |> 
  count(time_hour, origin) |> 
  filter(n > 1)
```


<table class="dataframe">
<caption>A tibble: 0 x 2</caption>
<thead>
	<tr><th scope=col>tailnum</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>




<table class="dataframe">
<caption>A tibble: 0 x 3</caption>
<thead>
	<tr><th scope=col>time_hour</th><th scope=col>origin</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>




```R
planes |> 
  filter(is.na(tailnum))

weather |> 
  filter(is.na(time_hour) | is.na(origin))
```


<table class="dataframe">
<caption>A tibble: 0 x 9</caption>
<thead>
	<tr><th scope=col>tailnum</th><th scope=col>year</th><th scope=col>type</th><th scope=col>manufacturer</th><th scope=col>model</th><th scope=col>engines</th><th scope=col>seats</th><th scope=col>speed</th><th scope=col>engine</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>




<table class="dataframe">
<caption>A tibble: 0 x 15</caption>
<thead>
	<tr><th scope=col>origin</th><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>hour</th><th scope=col>temp</th><th scope=col>dewp</th><th scope=col>humid</th><th scope=col>wind_dir</th><th scope=col>wind_speed</th><th scope=col>wind_gust</th><th scope=col>precip</th><th scope=col>pressure</th><th scope=col>visib</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>



### Surrogate keys


```R
flights |> 
  count(time_hour, carrier, flight) |> 
  filter(n > 1)
```


<table class="dataframe">
<caption>A tibble: 0 x 4</caption>
<thead>
	<tr><th scope=col>time_hour</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>n</th></tr>
	<tr><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>




```R
flights2 <- flights |> 
  mutate(id = row_number(), .before = 1)
flights2
```


<table class="dataframe">
<caption>A tibble: 336776 x 20</caption>
<thead>
	<tr><th scope=col>id</th><th scope=col>year</th><th scope=col>month</th><th scope=col>day</th><th scope=col>dep_time</th><th scope=col>sched_dep_time</th><th scope=col>dep_delay</th><th scope=col>arr_time</th><th scope=col>sched_arr_time</th><th scope=col>arr_delay</th><th scope=col>carrier</th><th scope=col>flight</th><th scope=col>tailnum</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>air_time</th><th scope=col>distance</th><th scope=col>hour</th><th scope=col>minute</th><th scope=col>time_hour</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dttm&gt;</th></tr>
</thead>
<tbody>
	<tr><td> 1</td><td>2013</td><td>1</td><td>1</td><td>517</td><td>515</td><td> 2</td><td> 830</td><td> 819</td><td> 11</td><td>UA</td><td>1545</td><td>N14228</td><td>EWR</td><td>IAH</td><td>227</td><td>1400</td><td>5</td><td>15</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td> 2</td><td>2013</td><td>1</td><td>1</td><td>533</td><td>529</td><td> 4</td><td> 850</td><td> 830</td><td> 20</td><td>UA</td><td>1714</td><td>N24211</td><td>LGA</td><td>IAH</td><td>227</td><td>1416</td><td>5</td><td>29</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td> 3</td><td>2013</td><td>1</td><td>1</td><td>542</td><td>540</td><td> 2</td><td> 923</td><td> 850</td><td> 33</td><td>AA</td><td>1141</td><td>N619AA</td><td>JFK</td><td>MIA</td><td>160</td><td>1089</td><td>5</td><td>40</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td> 4</td><td>2013</td><td>1</td><td>1</td><td>544</td><td>545</td><td>-1</td><td>1004</td><td>1022</td><td>-18</td><td>B6</td><td> 725</td><td>N804JB</td><td>JFK</td><td>BQN</td><td>183</td><td>1576</td><td>5</td><td>45</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td> 5</td><td>2013</td><td>1</td><td>1</td><td>554</td><td>600</td><td>-6</td><td> 812</td><td> 837</td><td>-25</td><td>DL</td><td> 461</td><td>N668DN</td><td>LGA</td><td>ATL</td><td>116</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td> 6</td><td>2013</td><td>1</td><td>1</td><td>554</td><td>558</td><td>-4</td><td> 740</td><td> 728</td><td> 12</td><td>UA</td><td>1696</td><td>N39463</td><td>EWR</td><td>ORD</td><td>150</td><td> 719</td><td>5</td><td>58</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td> 7</td><td>2013</td><td>1</td><td>1</td><td>555</td><td>600</td><td>-5</td><td> 913</td><td> 854</td><td> 19</td><td>B6</td><td> 507</td><td>N516JB</td><td>EWR</td><td>FLL</td><td>158</td><td>1065</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td> 8</td><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 709</td><td> 723</td><td>-14</td><td>EV</td><td>5708</td><td>N829AS</td><td>LGA</td><td>IAD</td><td> 53</td><td> 229</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td> 9</td><td>2013</td><td>1</td><td>1</td><td>557</td><td>600</td><td>-3</td><td> 838</td><td> 846</td><td> -8</td><td>B6</td><td>  79</td><td>N593JB</td><td>JFK</td><td>MCO</td><td>140</td><td> 944</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>10</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 753</td><td> 745</td><td>  8</td><td>AA</td><td> 301</td><td>N3ALAA</td><td>LGA</td><td>ORD</td><td>138</td><td> 733</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>11</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 849</td><td> 851</td><td> -2</td><td>B6</td><td>  49</td><td>N793JB</td><td>JFK</td><td>PBI</td><td>149</td><td>1028</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>12</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 853</td><td> 856</td><td> -3</td><td>B6</td><td>  71</td><td>N657JB</td><td>JFK</td><td>TPA</td><td>158</td><td>1005</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>13</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 924</td><td> 917</td><td>  7</td><td>UA</td><td> 194</td><td>N29129</td><td>JFK</td><td>LAX</td><td>345</td><td>2475</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>14</td><td>2013</td><td>1</td><td>1</td><td>558</td><td>600</td><td>-2</td><td> 923</td><td> 937</td><td>-14</td><td>UA</td><td>1124</td><td>N53441</td><td>EWR</td><td>SFO</td><td>361</td><td>2565</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>15</td><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 941</td><td> 910</td><td> 31</td><td>AA</td><td> 707</td><td>N3DUAA</td><td>LGA</td><td>DFW</td><td>257</td><td>1389</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>16</td><td>2013</td><td>1</td><td>1</td><td>559</td><td>559</td><td> 0</td><td> 702</td><td> 706</td><td> -4</td><td>B6</td><td>1806</td><td>N708JB</td><td>JFK</td><td>BOS</td><td> 44</td><td> 187</td><td>5</td><td>59</td><td>2013-01-01 05:00:00</td></tr>
	<tr><td>17</td><td>2013</td><td>1</td><td>1</td><td>559</td><td>600</td><td>-1</td><td> 854</td><td> 902</td><td> -8</td><td>UA</td><td>1187</td><td>N76515</td><td>EWR</td><td>LAS</td><td>337</td><td>2227</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>18</td><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 851</td><td> 858</td><td> -7</td><td>B6</td><td> 371</td><td>N595JB</td><td>LGA</td><td>FLL</td><td>152</td><td>1076</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>19</td><td>2013</td><td>1</td><td>1</td><td>600</td><td>600</td><td> 0</td><td> 837</td><td> 825</td><td> 12</td><td>MQ</td><td>4650</td><td>N542MQ</td><td>LGA</td><td>ATL</td><td>134</td><td> 762</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>20</td><td>2013</td><td>1</td><td>1</td><td>601</td><td>600</td><td> 1</td><td> 844</td><td> 850</td><td> -6</td><td>B6</td><td> 343</td><td>N644JB</td><td>EWR</td><td>PBI</td><td>147</td><td>1023</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>21</td><td>2013</td><td>1</td><td>1</td><td>602</td><td>610</td><td>-8</td><td> 812</td><td> 820</td><td> -8</td><td>DL</td><td>1919</td><td>N971DL</td><td>LGA</td><td>MSP</td><td>170</td><td>1020</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>22</td><td>2013</td><td>1</td><td>1</td><td>602</td><td>605</td><td>-3</td><td> 821</td><td> 805</td><td> 16</td><td>MQ</td><td>4401</td><td>N730MQ</td><td>LGA</td><td>DTW</td><td>105</td><td> 502</td><td>6</td><td> 5</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>23</td><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 858</td><td> 910</td><td>-12</td><td>AA</td><td>1895</td><td>N633AA</td><td>EWR</td><td>MIA</td><td>152</td><td>1085</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>24</td><td>2013</td><td>1</td><td>1</td><td>606</td><td>610</td><td>-4</td><td> 837</td><td> 845</td><td> -8</td><td>DL</td><td>1743</td><td>N3739P</td><td>JFK</td><td>ATL</td><td>128</td><td> 760</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>25</td><td>2013</td><td>1</td><td>1</td><td>607</td><td>607</td><td> 0</td><td> 858</td><td> 915</td><td>-17</td><td>UA</td><td>1077</td><td>N53442</td><td>EWR</td><td>MIA</td><td>157</td><td>1085</td><td>6</td><td> 7</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>26</td><td>2013</td><td>1</td><td>1</td><td>608</td><td>600</td><td> 8</td><td> 807</td><td> 735</td><td> 32</td><td>MQ</td><td>3768</td><td>N9EAMQ</td><td>EWR</td><td>ORD</td><td>139</td><td> 719</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>27</td><td>2013</td><td>1</td><td>1</td><td>611</td><td>600</td><td>11</td><td> 945</td><td> 931</td><td> 14</td><td>UA</td><td> 303</td><td>N532UA</td><td>JFK</td><td>SFO</td><td>366</td><td>2586</td><td>6</td><td> 0</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>28</td><td>2013</td><td>1</td><td>1</td><td>613</td><td>610</td><td> 3</td><td> 925</td><td> 921</td><td>  4</td><td>B6</td><td> 135</td><td>N635JB</td><td>JFK</td><td>RSW</td><td>175</td><td>1074</td><td>6</td><td>10</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>29</td><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td>1039</td><td>1100</td><td>-21</td><td>B6</td><td> 709</td><td>N794JB</td><td>JFK</td><td>SJU</td><td>182</td><td>1598</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>30</td><td>2013</td><td>1</td><td>1</td><td>615</td><td>615</td><td> 0</td><td> 833</td><td> 842</td><td> -9</td><td>DL</td><td> 575</td><td>N326NB</td><td>EWR</td><td>ATL</td><td>120</td><td> 746</td><td>6</td><td>15</td><td>2013-01-01 06:00:00</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>336747</td><td>2013</td><td>9</td><td>30</td><td>2123</td><td>2125</td><td> -2</td><td>2223</td><td>2247</td><td>-24</td><td>EV</td><td>5489</td><td>N712EV</td><td>LGA</td><td>CHO</td><td> 45</td><td> 305</td><td>21</td><td>25</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336748</td><td>2013</td><td>9</td><td>30</td><td>2127</td><td>2129</td><td> -2</td><td>2314</td><td>2323</td><td> -9</td><td>EV</td><td>3833</td><td>N16546</td><td>EWR</td><td>CLT</td><td> 72</td><td> 529</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336749</td><td>2013</td><td>9</td><td>30</td><td>2128</td><td>2130</td><td> -2</td><td>2328</td><td>2359</td><td>-31</td><td>B6</td><td>  97</td><td>N807JB</td><td>JFK</td><td>DEN</td><td>213</td><td>1626</td><td>21</td><td>30</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336750</td><td>2013</td><td>9</td><td>30</td><td>2129</td><td>2059</td><td> 30</td><td>2230</td><td>2232</td><td> -2</td><td>EV</td><td>5048</td><td>N751EV</td><td>LGA</td><td>RIC</td><td> 45</td><td> 292</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>336751</td><td>2013</td><td>9</td><td>30</td><td>2131</td><td>2140</td><td> -9</td><td>2225</td><td>2255</td><td>-30</td><td>MQ</td><td>3621</td><td>N807MQ</td><td>JFK</td><td>DCA</td><td> 36</td><td> 213</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336752</td><td>2013</td><td>9</td><td>30</td><td>2140</td><td>2140</td><td>  0</td><td>  10</td><td>  40</td><td>-30</td><td>AA</td><td> 185</td><td>N335AA</td><td>JFK</td><td>LAX</td><td>298</td><td>2475</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336753</td><td>2013</td><td>9</td><td>30</td><td>2142</td><td>2129</td><td> 13</td><td>2250</td><td>2239</td><td> 11</td><td>EV</td><td>4509</td><td>N12957</td><td>EWR</td><td>PWM</td><td> 47</td><td> 284</td><td>21</td><td>29</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336754</td><td>2013</td><td>9</td><td>30</td><td>2145</td><td>2145</td><td>  0</td><td> 115</td><td> 140</td><td>-25</td><td>B6</td><td>1103</td><td>N633JB</td><td>JFK</td><td>SJU</td><td>192</td><td>1598</td><td>21</td><td>45</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336755</td><td>2013</td><td>9</td><td>30</td><td>2147</td><td>2137</td><td> 10</td><td>  30</td><td>  27</td><td>  3</td><td>B6</td><td>1371</td><td>N627JB</td><td>LGA</td><td>FLL</td><td>139</td><td>1076</td><td>21</td><td>37</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336756</td><td>2013</td><td>9</td><td>30</td><td>2149</td><td>2156</td><td> -7</td><td>2245</td><td>2308</td><td>-23</td><td>UA</td><td> 523</td><td>N813UA</td><td>EWR</td><td>BOS</td><td> 37</td><td> 200</td><td>21</td><td>56</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336757</td><td>2013</td><td>9</td><td>30</td><td>2150</td><td>2159</td><td> -9</td><td>2250</td><td>2306</td><td>-16</td><td>EV</td><td>3842</td><td>N10575</td><td>EWR</td><td>MHT</td><td> 39</td><td> 209</td><td>21</td><td>59</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336758</td><td>2013</td><td>9</td><td>30</td><td>2159</td><td>1845</td><td>194</td><td>2344</td><td>2030</td><td>194</td><td>9E</td><td>3320</td><td>N906XJ</td><td>JFK</td><td>BUF</td><td> 50</td><td> 301</td><td>18</td><td>45</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>336759</td><td>2013</td><td>9</td><td>30</td><td>2203</td><td>2205</td><td> -2</td><td>2339</td><td>2331</td><td>  8</td><td>EV</td><td>5311</td><td>N722EV</td><td>LGA</td><td>BGR</td><td> 61</td><td> 378</td><td>22</td><td> 5</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336760</td><td>2013</td><td>9</td><td>30</td><td>2207</td><td>2140</td><td> 27</td><td>2257</td><td>2250</td><td>  7</td><td>MQ</td><td>3660</td><td>N532MQ</td><td>LGA</td><td>BNA</td><td> 97</td><td> 764</td><td>21</td><td>40</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336761</td><td>2013</td><td>9</td><td>30</td><td>2211</td><td>2059</td><td> 72</td><td>2339</td><td>2242</td><td> 57</td><td>EV</td><td>4672</td><td>N12145</td><td>EWR</td><td>STL</td><td>120</td><td> 872</td><td>20</td><td>59</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>336762</td><td>2013</td><td>9</td><td>30</td><td>2231</td><td>2245</td><td>-14</td><td>2335</td><td>2356</td><td>-21</td><td>B6</td><td> 108</td><td>N193JB</td><td>JFK</td><td>PWM</td><td> 48</td><td> 273</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336763</td><td>2013</td><td>9</td><td>30</td><td>2233</td><td>2113</td><td> 80</td><td> 112</td><td>  30</td><td> 42</td><td>UA</td><td> 471</td><td>N578UA</td><td>EWR</td><td>SFO</td><td>318</td><td>2565</td><td>21</td><td>13</td><td>2013-09-30 21:00:00</td></tr>
	<tr><td>336764</td><td>2013</td><td>9</td><td>30</td><td>2235</td><td>2001</td><td>154</td><td>  59</td><td>2249</td><td>130</td><td>B6</td><td>1083</td><td>N804JB</td><td>JFK</td><td>MCO</td><td>123</td><td> 944</td><td>20</td><td> 1</td><td>2013-09-30 20:00:00</td></tr>
	<tr><td>336765</td><td>2013</td><td>9</td><td>30</td><td>2237</td><td>2245</td><td> -8</td><td>2345</td><td>2353</td><td> -8</td><td>B6</td><td> 234</td><td>N318JB</td><td>JFK</td><td>BTV</td><td> 43</td><td> 266</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336766</td><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2245</td><td> -5</td><td>2334</td><td>2351</td><td>-17</td><td>B6</td><td>1816</td><td>N354JB</td><td>JFK</td><td>SYR</td><td> 41</td><td> 209</td><td>22</td><td>45</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336767</td><td>2013</td><td>9</td><td>30</td><td>2240</td><td>2250</td><td>-10</td><td>2347</td><td>   7</td><td>-20</td><td>B6</td><td>2002</td><td>N281JB</td><td>JFK</td><td>BUF</td><td> 52</td><td> 301</td><td>22</td><td>50</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336768</td><td>2013</td><td>9</td><td>30</td><td>2241</td><td>2246</td><td> -5</td><td>2345</td><td>   1</td><td>-16</td><td>B6</td><td> 486</td><td>N346JB</td><td>JFK</td><td>ROC</td><td> 47</td><td> 264</td><td>22</td><td>46</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336769</td><td>2013</td><td>9</td><td>30</td><td>2307</td><td>2255</td><td> 12</td><td>2359</td><td>2358</td><td>  1</td><td>B6</td><td> 718</td><td>N565JB</td><td>JFK</td><td>BOS</td><td> 33</td><td> 187</td><td>22</td><td>55</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336770</td><td>2013</td><td>9</td><td>30</td><td>2349</td><td>2359</td><td>-10</td><td> 325</td><td> 350</td><td>-25</td><td>B6</td><td> 745</td><td>N516JB</td><td>JFK</td><td>PSE</td><td>196</td><td>1617</td><td>23</td><td>59</td><td>2013-09-30 23:00:00</td></tr>
	<tr><td>336771</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1842</td><td> NA</td><td>  NA</td><td>2019</td><td> NA</td><td>EV</td><td>5274</td><td>N740EV</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>18</td><td>42</td><td>2013-09-30 18:00:00</td></tr>
	<tr><td>336772</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1455</td><td> NA</td><td>  NA</td><td>1634</td><td> NA</td><td>9E</td><td>3393</td><td>NA    </td><td>JFK</td><td>DCA</td><td> NA</td><td> 213</td><td>14</td><td>55</td><td>2013-09-30 14:00:00</td></tr>
	<tr><td>336773</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>2200</td><td> NA</td><td>  NA</td><td>2312</td><td> NA</td><td>9E</td><td>3525</td><td>NA    </td><td>LGA</td><td>SYR</td><td> NA</td><td> 198</td><td>22</td><td> 0</td><td>2013-09-30 22:00:00</td></tr>
	<tr><td>336774</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1210</td><td> NA</td><td>  NA</td><td>1330</td><td> NA</td><td>MQ</td><td>3461</td><td>N535MQ</td><td>LGA</td><td>BNA</td><td> NA</td><td> 764</td><td>12</td><td>10</td><td>2013-09-30 12:00:00</td></tr>
	<tr><td>336775</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td>1159</td><td> NA</td><td>  NA</td><td>1344</td><td> NA</td><td>MQ</td><td>3572</td><td>N511MQ</td><td>LGA</td><td>CLE</td><td> NA</td><td> 419</td><td>11</td><td>59</td><td>2013-09-30 11:00:00</td></tr>
	<tr><td>336776</td><td>2013</td><td>9</td><td>30</td><td>  NA</td><td> 840</td><td> NA</td><td>  NA</td><td>1020</td><td> NA</td><td>MQ</td><td>3531</td><td>N839MQ</td><td>LGA</td><td>RDU</td><td> NA</td><td> 431</td><td> 8</td><td>40</td><td>2013-09-30 08:00:00</td></tr>
</tbody>
</table>



### Exercises
1. We forgot to draw the relationship between weather and airports in Figure 19.1. What is the relationship and how should it appear in the diagram?

2. weather only contains information for the three origin airports in NYC. If it contained weather records for all airports in the USA, what additional connection would it make to flights?

3. The year, month, day, hour, and origin variables almost form a compound key for weather, but there’s one hour that has duplicate observations. Can you figure out what’s special about that hour?

4. We know that some days of the year are special and fewer people than usual fly on them (e.g., Christmas eve and Christmas day). How might you represent that data as a data frame? What would be the primary key? How would it connect to the existing data frames?

5. Draw a diagram illustrating the connections between the Batting, People, and Salaries data frames in the Lahman package. Draw another diagram that shows the relationship between People, Managers, AwardsManagers. How would you characterize the relationship between the Batting, Pitching, and Fielding data frames?

## 19.3 Basic joins
`dplyr` provides six join functions:
* `left_join()`,  to add in additional metadata.
* `inner_join()`, 
* `right_join()`, 
* `full_join()`, 
* `semi_join()`, 
* `anti_join()`

### Mutating joins:
A mutating join allows you to combine variables from two data frames: it first matches observations by their keys, then copies across variables from one data frame to the other.
`inner_join()`, `right_join()`, `full_join() `have the same interface as `left_join()`. The difference is which rows they keep: left join keeps all the rows in `x`, the right join keeps all rows in `y`, the full join keeps all rows in either `x` or `y`, and the inner join only keeps rows that occur in both `x` and `y`.


```R
flights2 <- flights |> 
  select(year, time_hour, origin, dest, tailnum, carrier)
flights2
```


<table class="dataframe">
<caption>A tibble: 336776 x 6</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>time_hour</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>tailnum</th><th scope=col>carrier</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>IAH</td><td>N14228</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>LGA</td><td>IAH</td><td>N24211</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>MIA</td><td>N619AA</td><td>AA</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BQN</td><td>N804JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N668DN</td><td>DL</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>ORD</td><td>N39463</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>FLL</td><td>N516JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>IAD</td><td>N829AS</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>MCO</td><td>N593JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ORD</td><td>N3ALAA</td><td>AA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>PBI</td><td>N793JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>TPA</td><td>N657JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>LAX</td><td>N29129</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>SFO</td><td>N53441</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DFW</td><td>N3DUAA</td><td>AA</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BOS</td><td>N708JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>LAS</td><td>N76515</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>FLL</td><td>N595JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N542MQ</td><td>MQ</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>PBI</td><td>N644JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>MSP</td><td>N971DL</td><td>DL</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DTW</td><td>N730MQ</td><td>MQ</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N633AA</td><td>AA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>ATL</td><td>N3739P</td><td>DL</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N53442</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ORD</td><td>N9EAMQ</td><td>MQ</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SFO</td><td>N532UA</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>RSW</td><td>N635JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SJU</td><td>N794JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ATL</td><td>N326NB</td><td>DL</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>CHO</td><td>N712EV</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>CLT</td><td>N16546</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DEN</td><td>N807JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>LGA</td><td>RIC</td><td>N751EV</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DCA</td><td>N807MQ</td><td>MQ</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>LAX</td><td>N335AA</td><td>AA</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>PWM</td><td>N12957</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>SJU</td><td>N633JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>FLL</td><td>N627JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>BOS</td><td>N813UA</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>MHT</td><td>N10575</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>JFK</td><td>BUF</td><td>N906XJ</td><td>9E</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>BGR</td><td>N722EV</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>BNA</td><td>N532MQ</td><td>MQ</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>EWR</td><td>STL</td><td>N12145</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>PWM</td><td>N193JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>SFO</td><td>N578UA</td><td>UA</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>JFK</td><td>MCO</td><td>N804JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BTV</td><td>N318JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>SYR</td><td>N354JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BUF</td><td>N281JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>ROC</td><td>N346JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BOS</td><td>N565JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 23:00:00</td><td>JFK</td><td>PSE</td><td>N516JB</td><td>B6</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>LGA</td><td>BNA</td><td>N740EV</td><td>EV</td></tr>
	<tr><td>2013</td><td>2013-09-30 14:00:00</td><td>JFK</td><td>DCA</td><td>NA    </td><td>9E</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>SYR</td><td>NA    </td><td>9E</td></tr>
	<tr><td>2013</td><td>2013-09-30 12:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td></tr>
	<tr><td>2013</td><td>2013-09-30 11:00:00</td><td>LGA</td><td>CLE</td><td>N511MQ</td><td>MQ</td></tr>
	<tr><td>2013</td><td>2013-09-30 08:00:00</td><td>LGA</td><td>RDU</td><td>N839MQ</td><td>MQ</td></tr>
</tbody>
</table>




```R
# add the full airline name to the flights2 data
flights2 |>
  left_join(airlines)
```

    [1m[22mJoining with `by = join_by(carrier)`



<table class="dataframe">
<caption>A tibble: 336776 x 7</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>time_hour</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>tailnum</th><th scope=col>carrier</th><th scope=col>name</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>IAH</td><td>N14228</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>LGA</td><td>IAH</td><td>N24211</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>MIA</td><td>N619AA</td><td>AA</td><td>American Airlines Inc.  </td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BQN</td><td>N804JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N668DN</td><td>DL</td><td>Delta Air Lines Inc.    </td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>ORD</td><td>N39463</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>FLL</td><td>N516JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>IAD</td><td>N829AS</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>MCO</td><td>N593JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ORD</td><td>N3ALAA</td><td>AA</td><td>American Airlines Inc.  </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>PBI</td><td>N793JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>TPA</td><td>N657JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>LAX</td><td>N29129</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>SFO</td><td>N53441</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DFW</td><td>N3DUAA</td><td>AA</td><td>American Airlines Inc.  </td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BOS</td><td>N708JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>LAS</td><td>N76515</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>FLL</td><td>N595JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N542MQ</td><td>MQ</td><td>Envoy Air               </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>PBI</td><td>N644JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>MSP</td><td>N971DL</td><td>DL</td><td>Delta Air Lines Inc.    </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DTW</td><td>N730MQ</td><td>MQ</td><td>Envoy Air               </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N633AA</td><td>AA</td><td>American Airlines Inc.  </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>ATL</td><td>N3739P</td><td>DL</td><td>Delta Air Lines Inc.    </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N53442</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ORD</td><td>N9EAMQ</td><td>MQ</td><td>Envoy Air               </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SFO</td><td>N532UA</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>RSW</td><td>N635JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SJU</td><td>N794JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ATL</td><td>N326NB</td><td>DL</td><td>Delta Air Lines Inc.    </td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>CHO</td><td>N712EV</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>CLT</td><td>N16546</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DEN</td><td>N807JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>LGA</td><td>RIC</td><td>N751EV</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DCA</td><td>N807MQ</td><td>MQ</td><td>Envoy Air               </td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>LAX</td><td>N335AA</td><td>AA</td><td>American Airlines Inc.  </td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>PWM</td><td>N12957</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>SJU</td><td>N633JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>FLL</td><td>N627JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>BOS</td><td>N813UA</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>MHT</td><td>N10575</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>JFK</td><td>BUF</td><td>N906XJ</td><td>9E</td><td>Endeavor Air Inc.       </td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>BGR</td><td>N722EV</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>BNA</td><td>N532MQ</td><td>MQ</td><td>Envoy Air               </td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>EWR</td><td>STL</td><td>N12145</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>PWM</td><td>N193JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>SFO</td><td>N578UA</td><td>UA</td><td>United Air Lines Inc.   </td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>JFK</td><td>MCO</td><td>N804JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BTV</td><td>N318JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>SYR</td><td>N354JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BUF</td><td>N281JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>ROC</td><td>N346JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BOS</td><td>N565JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 23:00:00</td><td>JFK</td><td>PSE</td><td>N516JB</td><td>B6</td><td>JetBlue Airways         </td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>LGA</td><td>BNA</td><td>N740EV</td><td>EV</td><td>ExpressJet Airlines Inc.</td></tr>
	<tr><td>2013</td><td>2013-09-30 14:00:00</td><td>JFK</td><td>DCA</td><td>NA    </td><td>9E</td><td>Endeavor Air Inc.       </td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>SYR</td><td>NA    </td><td>9E</td><td>Endeavor Air Inc.       </td></tr>
	<tr><td>2013</td><td>2013-09-30 12:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>Envoy Air               </td></tr>
	<tr><td>2013</td><td>2013-09-30 11:00:00</td><td>LGA</td><td>CLE</td><td>N511MQ</td><td>MQ</td><td>Envoy Air               </td></tr>
	<tr><td>2013</td><td>2013-09-30 08:00:00</td><td>LGA</td><td>RDU</td><td>N839MQ</td><td>MQ</td><td>Envoy Air               </td></tr>
</tbody>
</table>




```R
# find out the temperature and wind speed when each plane departed:
flights2 |> 
  left_join(weather |> select(origin, time_hour, temp, wind_speed))
```

    [1m[22mJoining with `by = join_by(time_hour, origin)`



<table class="dataframe">
<caption>A tibble: 336776 x 8</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>time_hour</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>tailnum</th><th scope=col>carrier</th><th scope=col>temp</th><th scope=col>wind_speed</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>IAH</td><td>N14228</td><td>UA</td><td>39.02</td><td>12.65858</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>LGA</td><td>IAH</td><td>N24211</td><td>UA</td><td>39.92</td><td>14.96014</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>MIA</td><td>N619AA</td><td>AA</td><td>39.02</td><td>14.96014</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BQN</td><td>N804JB</td><td>B6</td><td>39.02</td><td>14.96014</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N668DN</td><td>DL</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>ORD</td><td>N39463</td><td>UA</td><td>39.02</td><td>12.65858</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>FLL</td><td>N516JB</td><td>B6</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>IAD</td><td>N829AS</td><td>EV</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>MCO</td><td>N593JB</td><td>B6</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ORD</td><td>N3ALAA</td><td>AA</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>PBI</td><td>N793JB</td><td>B6</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>TPA</td><td>N657JB</td><td>B6</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>LAX</td><td>N29129</td><td>UA</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>SFO</td><td>N53441</td><td>UA</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DFW</td><td>N3DUAA</td><td>AA</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BOS</td><td>N708JB</td><td>B6</td><td>39.02</td><td>14.96014</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>LAS</td><td>N76515</td><td>UA</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>FLL</td><td>N595JB</td><td>B6</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N542MQ</td><td>MQ</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>PBI</td><td>N644JB</td><td>B6</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>MSP</td><td>N971DL</td><td>DL</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DTW</td><td>N730MQ</td><td>MQ</td><td>39.92</td><td>16.11092</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N633AA</td><td>AA</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>ATL</td><td>N3739P</td><td>DL</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N53442</td><td>UA</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ORD</td><td>N9EAMQ</td><td>MQ</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SFO</td><td>N532UA</td><td>UA</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>RSW</td><td>N635JB</td><td>B6</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SJU</td><td>N794JB</td><td>B6</td><td>37.94</td><td>13.80936</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ATL</td><td>N326NB</td><td>DL</td><td>37.94</td><td>11.50780</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>CHO</td><td>N712EV</td><td>EV</td><td>64.94</td><td> 8.05546</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>CLT</td><td>N16546</td><td>EV</td><td>62.96</td><td> 3.45234</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DEN</td><td>N807JB</td><td>B6</td><td>62.06</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>LGA</td><td>RIC</td><td>N751EV</td><td>EV</td><td>64.94</td><td> 6.90468</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DCA</td><td>N807MQ</td><td>MQ</td><td>62.06</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>LAX</td><td>N335AA</td><td>AA</td><td>62.06</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>PWM</td><td>N12957</td><td>EV</td><td>62.96</td><td> 3.45234</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>SJU</td><td>N633JB</td><td>B6</td><td>62.06</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>FLL</td><td>N627JB</td><td>B6</td><td>64.94</td><td> 8.05546</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>BOS</td><td>N813UA</td><td>UA</td><td>62.96</td><td> 3.45234</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>MHT</td><td>N10575</td><td>EV</td><td>62.96</td><td> 3.45234</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>JFK</td><td>BUF</td><td>N906XJ</td><td>9E</td><td>64.04</td><td> 6.90468</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>BGR</td><td>N722EV</td><td>EV</td><td>64.94</td><td> 6.90468</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>BNA</td><td>N532MQ</td><td>MQ</td><td>64.94</td><td> 8.05546</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>EWR</td><td>STL</td><td>N12145</td><td>EV</td><td>64.94</td><td> 3.45234</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>PWM</td><td>N193JB</td><td>B6</td><td>60.98</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>SFO</td><td>N578UA</td><td>UA</td><td>62.96</td><td> 3.45234</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>JFK</td><td>MCO</td><td>N804JB</td><td>B6</td><td>62.06</td><td> 8.05546</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BTV</td><td>N318JB</td><td>B6</td><td>60.98</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>SYR</td><td>N354JB</td><td>B6</td><td>60.98</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BUF</td><td>N281JB</td><td>B6</td><td>60.98</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>ROC</td><td>N346JB</td><td>B6</td><td>60.98</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BOS</td><td>N565JB</td><td>B6</td><td>60.98</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 23:00:00</td><td>JFK</td><td>PSE</td><td>N516JB</td><td>B6</td><td>60.08</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>LGA</td><td>BNA</td><td>N740EV</td><td>EV</td><td>66.92</td><td> 9.20624</td></tr>
	<tr><td>2013</td><td>2013-09-30 14:00:00</td><td>JFK</td><td>DCA</td><td>NA    </td><td>9E</td><td>68.00</td><td>11.50780</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>SYR</td><td>NA    </td><td>9E</td><td>64.94</td><td> 6.90468</td></tr>
	<tr><td>2013</td><td>2013-09-30 12:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>69.08</td><td> 5.75390</td></tr>
	<tr><td>2013</td><td>2013-09-30 11:00:00</td><td>LGA</td><td>CLE</td><td>N511MQ</td><td>MQ</td><td>66.92</td><td> 8.05546</td></tr>
	<tr><td>2013</td><td>2013-09-30 08:00:00</td><td>LGA</td><td>RDU</td><td>N839MQ</td><td>MQ</td><td>60.98</td><td> 5.75390</td></tr>
</tbody>
</table>




```R
# what size of plane was flying:
flights2 |> 
  left_join(planes |> select(tailnum, type, engines, seats))
```

    [1m[22mJoining with `by = join_by(tailnum)`



<table class="dataframe">
<caption>A tibble: 336776 x 9</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>time_hour</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>tailnum</th><th scope=col>carrier</th><th scope=col>type</th><th scope=col>engines</th><th scope=col>seats</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>IAH</td><td>N14228</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>149</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>LGA</td><td>IAH</td><td>N24211</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>149</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>MIA</td><td>N619AA</td><td>AA</td><td>Fixed wing multi engine</td><td> 2</td><td>178</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BQN</td><td>N804JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N668DN</td><td>DL</td><td>Fixed wing multi engine</td><td> 2</td><td>178</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>ORD</td><td>N39463</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>191</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>FLL</td><td>N516JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>IAD</td><td>N829AS</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 55</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>MCO</td><td>N593JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ORD</td><td>N3ALAA</td><td>AA</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>PBI</td><td>N793JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>TPA</td><td>N657JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>LAX</td><td>N29129</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>178</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>SFO</td><td>N53441</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>191</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DFW</td><td>N3DUAA</td><td>AA</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BOS</td><td>N708JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>LAS</td><td>N76515</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>149</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>FLL</td><td>N595JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N542MQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>PBI</td><td>N644JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>MSP</td><td>N971DL</td><td>DL</td><td>Fixed wing multi engine</td><td> 2</td><td>142</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DTW</td><td>N730MQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N633AA</td><td>AA</td><td>Fixed wing multi engine</td><td> 2</td><td>178</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>ATL</td><td>N3739P</td><td>DL</td><td>Fixed wing multi engine</td><td> 2</td><td>189</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N53442</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>191</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ORD</td><td>N9EAMQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SFO</td><td>N532UA</td><td>UA</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>RSW</td><td>N635JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SJU</td><td>N794JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ATL</td><td>N326NB</td><td>DL</td><td>Fixed wing multi engine</td><td> 2</td><td>145</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>CHO</td><td>N712EV</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 80</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>CLT</td><td>N16546</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 55</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DEN</td><td>N807JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>LGA</td><td>RIC</td><td>N751EV</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 80</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DCA</td><td>N807MQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>LAX</td><td>N335AA</td><td>AA</td><td>Fixed wing multi engine</td><td> 2</td><td>255</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>PWM</td><td>N12957</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 55</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>SJU</td><td>N633JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>FLL</td><td>N627JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>BOS</td><td>N813UA</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>179</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>MHT</td><td>N10575</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 55</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>JFK</td><td>BUF</td><td>N906XJ</td><td>9E</td><td>Fixed wing multi engine</td><td> 2</td><td> 95</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>BGR</td><td>N722EV</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 80</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>BNA</td><td>N532MQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>EWR</td><td>STL</td><td>N12145</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 55</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>PWM</td><td>N193JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td> 20</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>SFO</td><td>N578UA</td><td>UA</td><td>Fixed wing multi engine</td><td> 2</td><td>178</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>JFK</td><td>MCO</td><td>N804JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BTV</td><td>N318JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td> 20</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>SYR</td><td>N354JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td> 20</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BUF</td><td>N281JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td> 20</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>ROC</td><td>N346JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td> 20</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BOS</td><td>N565JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-09-30 23:00:00</td><td>JFK</td><td>PSE</td><td>N516JB</td><td>B6</td><td>Fixed wing multi engine</td><td> 2</td><td>200</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>LGA</td><td>BNA</td><td>N740EV</td><td>EV</td><td>Fixed wing multi engine</td><td> 2</td><td> 80</td></tr>
	<tr><td>2013</td><td>2013-09-30 14:00:00</td><td>JFK</td><td>DCA</td><td>NA    </td><td>9E</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>SYR</td><td>NA    </td><td>9E</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 12:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 11:00:00</td><td>LGA</td><td>CLE</td><td>N511MQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 08:00:00</td><td>LGA</td><td>RDU</td><td>N839MQ</td><td>MQ</td><td>NA                     </td><td>NA</td><td> NA</td></tr>
</tbody>
</table>




```R
# When left_join() fails to find a match for a row in x, it fills in the new variables with missing values. 
flights2 |> 
  filter(tailnum == "N535MQ") |> 
  left_join(planes |> select(tailnum, type, engines, seats))
```

    [1m[22mJoining with `by = join_by(tailnum)`



<table class="dataframe">
<caption>A tibble: 264 x 9</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>time_hour</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>tailnum</th><th scope=col>carrier</th><th scope=col>type</th><th scope=col>engines</th><th scope=col>seats</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;int&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>2013-01-02 16:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-03 06:00:00</td><td>LGA</td><td>CLT</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-03 11:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-03 18:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-11 16:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-12 12:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-12 18:00:00</td><td>LGA</td><td>CLE</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-13 15:00:00</td><td>LGA</td><td>CLT</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-13 20:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-14 08:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-14 20:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-18 11:00:00</td><td>JFK</td><td>DCA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-19 15:00:00</td><td>JFK</td><td>DCA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-19 19:00:00</td><td>JFK</td><td>CMH</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-20 08:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-20 14:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-20 21:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-21 09:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-23 18:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-25 06:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-26 08:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-26 15:00:00</td><td>LGA</td><td>CLT</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-27 11:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-28 09:00:00</td><td>LGA</td><td>CLT</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-28 14:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-01-31 12:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-10-01 09:00:00</td><td>LGA</td><td>CLT</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-10-01 14:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-10-01 21:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-10-02 15:00:00</td><td>LGA</td><td>CLT</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>2013-08-30 10:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-08-30 15:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-08-31 13:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-03 13:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-05 15:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-13 13:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-18 10:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-18 16:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-19 06:00:00</td><td>LGA</td><td>ATL</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-19 12:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-20 13:00:00</td><td>LGA</td><td>CLE</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-20 18:00:00</td><td>LGA</td><td>CLE</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-21 11:00:00</td><td>LGA</td><td>MSP</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-23 11:00:00</td><td>JFK</td><td>DCA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-25 06:00:00</td><td>EWR</td><td>ORD</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-25 20:00:00</td><td>JFK</td><td>CMH</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-26 11:00:00</td><td>JFK</td><td>DCA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-26 15:00:00</td><td>JFK</td><td>DCA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-27 11:00:00</td><td>LGA</td><td>CLE</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-27 15:00:00</td><td>LGA</td><td>RDU</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-27 21:00:00</td><td>LGA</td><td>CLT</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-28 11:00:00</td><td>LGA</td><td>CLE</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-29 08:00:00</td><td>LGA</td><td>DTW</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-29 13:00:00</td><td>LGA</td><td>RDU</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-29 17:00:00</td><td>LGA</td><td>RDU</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-29 21:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 11:00:00</td><td>LGA</td><td>RDU</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 15:00:00</td><td>LGA</td><td>RDU</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>RDU</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
	<tr><td>2013</td><td>2013-09-30 12:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>NA</td><td>NA</td><td>NA</td></tr>
</tbody>
</table>



### Specifying join keys

By default, left_join() will use all variables that appear in both data frames as the join key, the so called natural join. This is a useful heuristic, but it doesn’t always work, for example, both dataframes have the same column's name (but with different meanings)


```R
flights2 |> 
  left_join(airports, join_by(origin == faa))
```


<table class="dataframe">
<caption>A tibble: 336776 x 13</caption>
<thead>
	<tr><th scope=col>year</th><th scope=col>time_hour</th><th scope=col>origin</th><th scope=col>dest</th><th scope=col>tailnum</th><th scope=col>carrier</th><th scope=col>name</th><th scope=col>lat</th><th scope=col>lon</th><th scope=col>alt</th><th scope=col>tz</th><th scope=col>dst</th><th scope=col>tzone</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;dttm&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>IAH</td><td>N14228</td><td>UA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>LGA</td><td>IAH</td><td>N24211</td><td>UA</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>MIA</td><td>N619AA</td><td>AA</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BQN</td><td>N804JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N668DN</td><td>DL</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>EWR</td><td>ORD</td><td>N39463</td><td>UA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>FLL</td><td>N516JB</td><td>B6</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>IAD</td><td>N829AS</td><td>EV</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>MCO</td><td>N593JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ORD</td><td>N3ALAA</td><td>AA</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>PBI</td><td>N793JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>TPA</td><td>N657JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>LAX</td><td>N29129</td><td>UA</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>SFO</td><td>N53441</td><td>UA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DFW</td><td>N3DUAA</td><td>AA</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 05:00:00</td><td>JFK</td><td>BOS</td><td>N708JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>LAS</td><td>N76515</td><td>UA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>FLL</td><td>N595JB</td><td>B6</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>ATL</td><td>N542MQ</td><td>MQ</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>PBI</td><td>N644JB</td><td>B6</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>MSP</td><td>N971DL</td><td>DL</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>LGA</td><td>DTW</td><td>N730MQ</td><td>MQ</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N633AA</td><td>AA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>ATL</td><td>N3739P</td><td>DL</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>MIA</td><td>N53442</td><td>UA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ORD</td><td>N9EAMQ</td><td>MQ</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SFO</td><td>N532UA</td><td>UA</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>RSW</td><td>N635JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>JFK</td><td>SJU</td><td>N794JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-01-01 06:00:00</td><td>EWR</td><td>ATL</td><td>N326NB</td><td>DL</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>CHO</td><td>N712EV</td><td>EV</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>CLT</td><td>N16546</td><td>EV</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DEN</td><td>N807JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>LGA</td><td>RIC</td><td>N751EV</td><td>EV</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>DCA</td><td>N807MQ</td><td>MQ</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>LAX</td><td>N335AA</td><td>AA</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>PWM</td><td>N12957</td><td>EV</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>JFK</td><td>SJU</td><td>N633JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>FLL</td><td>N627JB</td><td>B6</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>BOS</td><td>N813UA</td><td>UA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>MHT</td><td>N10575</td><td>EV</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>JFK</td><td>BUF</td><td>N906XJ</td><td>9E</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>BGR</td><td>N722EV</td><td>EV</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>LGA</td><td>BNA</td><td>N532MQ</td><td>MQ</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>EWR</td><td>STL</td><td>N12145</td><td>EV</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>PWM</td><td>N193JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 21:00:00</td><td>EWR</td><td>SFO</td><td>N578UA</td><td>UA</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 20:00:00</td><td>JFK</td><td>MCO</td><td>N804JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BTV</td><td>N318JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>SYR</td><td>N354JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BUF</td><td>N281JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>ROC</td><td>N346JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>JFK</td><td>BOS</td><td>N565JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 23:00:00</td><td>JFK</td><td>PSE</td><td>N516JB</td><td>B6</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 18:00:00</td><td>LGA</td><td>BNA</td><td>N740EV</td><td>EV</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 14:00:00</td><td>JFK</td><td>DCA</td><td>NA    </td><td>9E</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 22:00:00</td><td>LGA</td><td>SYR</td><td>NA    </td><td>9E</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 12:00:00</td><td>LGA</td><td>BNA</td><td>N535MQ</td><td>MQ</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 11:00:00</td><td>LGA</td><td>CLE</td><td>N511MQ</td><td>MQ</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>2013</td><td>2013-09-30 08:00:00</td><td>LGA</td><td>RDU</td><td>N839MQ</td><td>MQ</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
</tbody>
</table>



### Filtering joins

The primary action of a filtering join is to *filter the rows*.

* `semi_join()` keep all rows in `x` that have a match in `y`.
* `anti_join()` return all rows in `x` that don’t have a match in `y`. They’re useful for finding missing values that are implicit in the data.


```R
airports |> 
  semi_join(flights2, join_by(faa == origin))
```


<table class="dataframe">
<caption>A tibble: 3 x 8</caption>
<thead>
	<tr><th scope=col>faa</th><th scope=col>name</th><th scope=col>lat</th><th scope=col>lon</th><th scope=col>alt</th><th scope=col>tz</th><th scope=col>dst</th><th scope=col>tzone</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>EWR</td><td>Newark Liberty Intl</td><td>40.69250</td><td>-74.16867</td><td>18</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>JFK</td><td>John F Kennedy Intl</td><td>40.63975</td><td>-73.77893</td><td>13</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
	<tr><td>LGA</td><td>La Guardia         </td><td>40.77725</td><td>-73.87261</td><td>22</td><td>-5</td><td>A</td><td>America/New_York</td></tr>
</tbody>
</table>




```R
airports |> 
  semi_join(flights2, join_by(faa == dest))
```


<table class="dataframe">
<caption>A tibble: 101 x 8</caption>
<thead>
	<tr><th scope=col>faa</th><th scope=col>name</th><th scope=col>lat</th><th scope=col>lon</th><th scope=col>alt</th><th scope=col>tz</th><th scope=col>dst</th><th scope=col>tzone</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>ABQ</td><td>Albuquerque International Sunport </td><td>35.04022</td><td>-106.60919</td><td>5355</td><td>-7</td><td>A</td><td>America/Denver     </td></tr>
	<tr><td>ACK</td><td>Nantucket Mem                     </td><td>41.25305</td><td> -70.06018</td><td>  48</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ALB</td><td>Albany Intl                       </td><td>42.74827</td><td> -73.80169</td><td> 285</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ANC</td><td>Ted Stevens Anchorage Intl        </td><td>61.17436</td><td>-149.99636</td><td> 152</td><td>-9</td><td>A</td><td>America/Anchorage  </td></tr>
	<tr><td>ATL</td><td>Hartsfield Jackson Atlanta Intl   </td><td>33.63672</td><td> -84.42807</td><td>1026</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>AUS</td><td>Austin Bergstrom Intl             </td><td>30.19453</td><td> -97.66989</td><td> 542</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>AVL</td><td>Asheville Regional Airport        </td><td>35.43619</td><td> -82.54181</td><td>2165</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>BDL</td><td>Bradley Intl                      </td><td>41.93889</td><td> -72.68322</td><td> 173</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>BGR</td><td>Bangor Intl                       </td><td>44.80744</td><td> -68.82814</td><td> 192</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>BHM</td><td>Birmingham Intl                   </td><td>33.56294</td><td> -86.75355</td><td> 644</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>BNA</td><td>Nashville Intl                    </td><td>36.12447</td><td> -86.67819</td><td> 599</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>BOS</td><td>General Edward Lawrence Logan Intl</td><td>42.36435</td><td> -71.00518</td><td>  19</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>BTV</td><td>Burlington Intl                   </td><td>44.47186</td><td> -73.15328</td><td> 335</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>BUF</td><td>Buffalo Niagara Intl              </td><td>42.94053</td><td> -78.73217</td><td> 724</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>BUR</td><td>Bob Hope                          </td><td>34.20067</td><td>-118.35867</td><td> 778</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>BWI</td><td>Baltimore Washington Intl         </td><td>39.17536</td><td> -76.66833</td><td> 146</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>BZN</td><td>Gallatin Field                    </td><td>45.77764</td><td>-111.16015</td><td>4500</td><td>-7</td><td>A</td><td>America/Denver     </td></tr>
	<tr><td>CAE</td><td>Columbia Metropolitan             </td><td>33.93883</td><td> -81.11953</td><td> 236</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CAK</td><td>Akron Canton Regional Airport     </td><td>40.91608</td><td> -81.44219</td><td>1228</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CHO</td><td>Charlottesville-Albemarle         </td><td>38.13864</td><td> -78.45286</td><td> 639</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CHS</td><td>Charleston Afb Intl               </td><td>32.89865</td><td> -80.04053</td><td>  45</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CLE</td><td>Cleveland Hopkins Intl            </td><td>41.41169</td><td> -81.84979</td><td> 791</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CLT</td><td>Charlotte Douglas Intl            </td><td>35.21400</td><td> -80.94314</td><td> 748</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CMH</td><td>Port Columbus Intl                </td><td>39.99797</td><td> -82.89189</td><td> 815</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CRW</td><td>Yeager                            </td><td>38.37315</td><td> -81.59319</td><td> 981</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>CVG</td><td>Cincinnati Northern Kentucky Intl </td><td>39.04884</td><td> -84.66782</td><td> 896</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>DAY</td><td>James M Cox Dayton Intl           </td><td>39.90237</td><td> -84.21937</td><td>1009</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>DCA</td><td>Ronald Reagan Washington Natl     </td><td>38.85208</td><td> -77.03772</td><td>  15</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>DEN</td><td>Denver Intl                       </td><td>39.86166</td><td>-104.67318</td><td>5431</td><td>-7</td><td>A</td><td>America/Denver     </td></tr>
	<tr><td>DFW</td><td>Dallas Fort Worth Intl            </td><td>32.89683</td><td> -97.03800</td><td> 607</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>PDX</td><td>Portland Intl                   </td><td>45.58872</td><td>-122.59750</td><td>  30</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>PHL</td><td>Philadelphia Intl               </td><td>39.87194</td><td> -75.24114</td><td>  36</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>PHX</td><td>Phoenix Sky Harbor Intl         </td><td>33.43428</td><td>-112.01158</td><td>1135</td><td>-7</td><td>N</td><td>America/Phoenix    </td></tr>
	<tr><td>PIT</td><td>Pittsburgh Intl                 </td><td>40.49147</td><td> -80.23287</td><td>1204</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>PSP</td><td>Palm Springs Intl               </td><td>33.82967</td><td>-116.50669</td><td> 477</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>PVD</td><td>Theodore Francis Green State    </td><td>41.73258</td><td> -71.42038</td><td>  55</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>PWM</td><td>Portland Intl Jetport           </td><td>43.64616</td><td> -70.30928</td><td>  77</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>RDU</td><td>Raleigh Durham Intl             </td><td>35.87764</td><td> -78.78747</td><td> 435</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>RIC</td><td>Richmond Intl                   </td><td>37.50517</td><td> -77.31967</td><td> 167</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>ROC</td><td>Greater Rochester Intl          </td><td>43.11887</td><td> -77.67239</td><td> 559</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>RSW</td><td>Southwest Florida Intl          </td><td>26.53617</td><td> -81.75517</td><td>  30</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>SAN</td><td>San Diego Intl                  </td><td>32.73356</td><td>-117.18967</td><td>  17</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>SAT</td><td>San Antonio Intl                </td><td>29.53369</td><td> -98.46978</td><td> 809</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>SAV</td><td>Savannah Hilton Head Intl       </td><td>32.12758</td><td> -81.20214</td><td>  51</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>SBN</td><td>South Bend Rgnl                 </td><td>41.70866</td><td> -86.31725</td><td> 799</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>SDF</td><td>Louisville International Airport</td><td>38.17409</td><td> -85.73650</td><td> 501</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>SEA</td><td>Seattle Tacoma Intl             </td><td>47.44900</td><td>-122.30931</td><td> 433</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>SFO</td><td>San Francisco Intl              </td><td>37.61897</td><td>-122.37489</td><td>  13</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>SJC</td><td>Norman Y Mineta San Jose Intl   </td><td>37.36260</td><td>-121.92902</td><td>  62</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>SLC</td><td>Salt Lake City Intl             </td><td>40.78839</td><td>-111.97777</td><td>4227</td><td>-7</td><td>A</td><td>America/Denver     </td></tr>
	<tr><td>SMF</td><td>Sacramento Intl                 </td><td>38.69542</td><td>-121.59078</td><td>  27</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>SNA</td><td>John Wayne Arpt Orange Co       </td><td>33.67567</td><td>-117.86822</td><td>  56</td><td>-8</td><td>A</td><td>America/Los_Angeles</td></tr>
	<tr><td>SRQ</td><td>Sarasota Bradenton Intl         </td><td>27.39544</td><td> -82.55439</td><td>  30</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>STL</td><td>Lambert St Louis Intl           </td><td>38.74870</td><td> -90.37003</td><td> 618</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>SYR</td><td>Syracuse Hancock Intl           </td><td>43.11119</td><td> -76.10631</td><td> 421</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>TPA</td><td>Tampa Intl                      </td><td>27.97547</td><td> -82.53325</td><td>  26</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>TUL</td><td>Tulsa Intl                      </td><td>36.19839</td><td> -95.88811</td><td> 677</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
	<tr><td>TVC</td><td>Cherry Capital Airport          </td><td>44.74144</td><td> -85.58223</td><td> 624</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>TYS</td><td>Mc Ghee Tyson                   </td><td>35.81097</td><td> -83.99403</td><td> 981</td><td>-5</td><td>A</td><td>America/New_York   </td></tr>
	<tr><td>XNA</td><td>NW Arkansas Regional            </td><td>36.28187</td><td> -94.30681</td><td>1287</td><td>-6</td><td>A</td><td>America/Chicago    </td></tr>
</tbody>
</table>




```R
# find rows that are missing from airports by looking for flights that don’t have a matching destination airport.
flights2 |> 
  anti_join(airports, join_by(dest == faa)) |> 
  distinct(dest)
```


<table class="dataframe">
<caption>A tibble: 4 x 1</caption>
<thead>
	<tr><th scope=col>dest</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>BQN</td></tr>
	<tr><td>SJU</td></tr>
	<tr><td>STT</td></tr>
	<tr><td>PSE</td></tr>
</tbody>
</table>




```R
#  find which tailnums are missing from planes
flights2 |>
  anti_join(planes, join_by(tailnum)) |> 
  distinct(tailnum)
```


<table class="dataframe">
<caption>A tibble: 722 x 1</caption>
<thead>
	<tr><th scope=col>tailnum</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>N3ALAA</td></tr>
	<tr><td>N3DUAA</td></tr>
	<tr><td>N542MQ</td></tr>
	<tr><td>N730MQ</td></tr>
	<tr><td>N9EAMQ</td></tr>
	<tr><td>N532UA</td></tr>
	<tr><td>N3EMAA</td></tr>
	<tr><td>N518MQ</td></tr>
	<tr><td>N3BAAA</td></tr>
	<tr><td>N3CYAA</td></tr>
	<tr><td>N426US</td></tr>
	<tr><td>N3GKAA</td></tr>
	<tr><td>N4WNAA</td></tr>
	<tr><td>N5FMAA</td></tr>
	<tr><td>N722MQ</td></tr>
	<tr><td>N3EKAA</td></tr>
	<tr><td>N3ETAA</td></tr>
	<tr><td>N541AA</td></tr>
	<tr><td>N4WRAA</td></tr>
	<tr><td>N4WPAA</td></tr>
	<tr><td>N508MQ</td></tr>
	<tr><td>N3HMAA</td></tr>
	<tr><td>N828MQ</td></tr>
	<tr><td>N3GEAA</td></tr>
	<tr><td>N739MQ</td></tr>
	<tr><td>N531MQ</td></tr>
	<tr><td>N527JB</td></tr>
	<tr><td>N846MQ</td></tr>
	<tr><td>N3GVAA</td></tr>
	<tr><td>N4YCAA</td></tr>
	<tr><td>...</td></tr>
	<tr><td>N7BAAA</td></tr>
	<tr><td>N7BVAA</td></tr>
	<tr><td>N626MQ</td></tr>
	<tr><td>N675MQ</td></tr>
	<tr><td>N580AA</td></tr>
	<tr><td>N717MQ</td></tr>
	<tr><td>N738MQ</td></tr>
	<tr><td>N720MQ</td></tr>
	<tr><td>N7ASAA</td></tr>
	<tr><td>N328AT</td></tr>
	<tr><td>N735MQ</td></tr>
	<tr><td>N5EDAA</td></tr>
	<tr><td>N5DJAA</td></tr>
	<tr><td>N7ALAA</td></tr>
	<tr><td>N721MQ</td></tr>
	<tr><td>N7BGAA</td></tr>
	<tr><td>N5ESAA</td></tr>
	<tr><td>N456UW</td></tr>
	<tr><td>N838MQ</td></tr>
	<tr><td>N442US</td></tr>
	<tr><td>N502SW</td></tr>
	<tr><td>N451UW</td></tr>
	<tr><td>N7BKAA</td></tr>
	<tr><td>N800MQ</td></tr>
	<tr><td>N7CAAA</td></tr>
	<tr><td>N823MQ</td></tr>
	<tr><td>N5FCAA</td></tr>
	<tr><td>N5ERAA</td></tr>
	<tr><td>N654MQ</td></tr>
	<tr><td>N647MQ</td></tr>
</tbody>
</table>



### Exercises
1. Find the 48 hours (over the course of the whole year) that have the worst delays. Cross-reference it with the weather data. Can you see any patterns?

2. Imagine you’ve found the top 10 most popular destinations using this code:

```
top_dest <- flights2 |>
  count(dest, sort = TRUE) |>
  head(10)
```

How can you find all flights to those destinations?

3. Does every departing flight have corresponding weather data for that hour?

4. What do the tail numbers that don’t have a matching record in planes have in common? (Hint: one variable explains ~90% of the problems.)

5. Add a column to planes that lists every carrier that has flown that plane. You might expect that there’s an implicit relationship between plane and airline, because each plane is flown by a single airline. Confirm or reject this hypothesis using the tools you’ve learned in previous chapters.

6. Add the latitude and the longitude of the origin and destination airport to flights. Is it easier to rename the columns before or after the join?

7. Compute the average delay by destination, then join on the airports data frame so you can show the spatial distribution of delays. Here’s an easy way to draw a map of the United States:
```
airports |>
  semi_join(flights, join_by(faa == dest)) |>
  ggplot(aes(x = lon, y = lat)) +
    borders("state") +
    geom_point() +
    coord_quickmap()
```
You might want to use the size or color of the points to display the average delay for each airport.

8. What happened on June 13 2013? Draw a map of the delays, and then use Google to cross-reference with the weather.

## 19.4 How do joins work?

![Inner join](R4DS-Transform_files/image.png){width=30%}   ![left join](R4DS-Transform_files/image-2.png){width=30%}   ![right join](R4DS-Transform_files/image-3.png){width=30%}

![full join](R4DS-Transform_files/image-4.png){width=30%}   ![Venn diagram](R4DS-Transform_files/image-5.png){width=30%}


```R
x <- tribble(
  ~key, ~val_x,
     1, "x1",
     2, "x2",
     3, "x3"
)
y <- tribble(
  ~key, ~val_y,
     1, "y1",
     2, "y2",
     4, "y3"
)
```


```R
x |>
inner_join(y)
```

    [1m[22mJoining with `by = join_by(key)`



<table class="dataframe">
<caption>A tibble: 2 x 3</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>y2</td></tr>
</tbody>
</table>




```R
x |>
left_join(y)
```

    [1m[22mJoining with `by = join_by(key)`



<table class="dataframe">
<caption>A tibble: 3 x 3</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>y2</td></tr>
	<tr><td>3</td><td>x3</td><td>NA</td></tr>
</tbody>
</table>




```R
x |> 
right_join(y)
```

    [1m[22mJoining with `by = join_by(key)`



<table class="dataframe">
<caption>A tibble: 3 x 3</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>y2</td></tr>
	<tr><td>4</td><td>NA</td><td>y3</td></tr>
</tbody>
</table>




```R
full_join(x,y)
```

    [1m[22mJoining with `by = join_by(key)`



<table class="dataframe">
<caption>A tibble: 4 x 3</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>y2</td></tr>
	<tr><td>3</td><td>x3</td><td>NA</td></tr>
	<tr><td>4</td><td>NA</td><td>y3</td></tr>
</tbody>
</table>



### Row matching
![Inner join](R4DS-Transform_files/image.png){width=30%}

one particularly dangerous case which can cause a combinatorial explosion of rows.

### Filterring joins
![semi join](R4DS-Transform_files/image.png){width=30%}       ![anti join](R4DS-Transform_files/image-2.png){width=30%}

* In a semi-join it only matters that there is a match; otherwise values in y don’t affect the output.
* An anti-join is the inverse of a semi-join, dropping rows from x that have a match in y.


```R
semi_join(x, y)
anti_join(x, y)
```

    [1m[22mJoining with `by = join_by(key)`



<table class="dataframe">
<caption>A tibble: 2 x 2</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td></tr>
	<tr><td>2</td><td>x2</td></tr>
</tbody>
</table>



    [1m[22mJoining with `by = join_by(key)`



<table class="dataframe">
<caption>A tibble: 1 x 2</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>3</td><td>x3</td></tr>
</tbody>
</table>



## 19.5 Non-equi joins

* **Cross joins** match every pair of rows.
* **Inequality joins** use <, <=, >, and >= instead of ==.
* **Rolling joins** are similar to inequality joins but only find the closest match.
* **Overlap joins** are a special type of inequality join designed to work with ranges.


```R
# equi join (where the rows match if the x key equals the y key)
x |> 
inner_join(y, join_by(key == key), keep = TRUE)
```


<table class="dataframe">
<caption>A tibble: 2 x 4</caption>
<thead>
	<tr><th scope=col>key.x</th><th scope=col>val_x</th><th scope=col>key.y</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>2</td><td>y2</td></tr>
</tbody>
</table>




```R
# non-equi join
x |> 
inner_join(y, join_by(key >= key), keep = TRUE)
```


<table class="dataframe">
<caption>A tibble: 5 x 4</caption>
<thead>
	<tr><th scope=col>key.x</th><th scope=col>val_x</th><th scope=col>key.y</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>2</td><td>y2</td></tr>
	<tr><td>3</td><td>x3</td><td>1</td><td>y1</td></tr>
	<tr><td>3</td><td>x3</td><td>2</td><td>y2</td></tr>
</tbody>
</table>



![Cross join](R4DS-Transform_files/image.png){width=30%} ![Inequality join](R4DS-Transform_files/image-2.png){width=30%} ![Rolling join](R4DS-Transform_files/image-3.png){width=30%} 


```R
cross_join(x,y)
```


<table class="dataframe">
<caption>A tibble: 9 x 4</caption>
<thead>
	<tr><th scope=col>key.x</th><th scope=col>val_x</th><th scope=col>key.y</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>1</td><td>y1</td></tr>
	<tr><td>1</td><td>x1</td><td>2</td><td>y2</td></tr>
	<tr><td>1</td><td>x1</td><td>4</td><td>y3</td></tr>
	<tr><td>2</td><td>x2</td><td>1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>2</td><td>y2</td></tr>
	<tr><td>2</td><td>x2</td><td>4</td><td>y3</td></tr>
	<tr><td>3</td><td>x3</td><td>1</td><td>y1</td></tr>
	<tr><td>3</td><td>x3</td><td>2</td><td>y2</td></tr>
	<tr><td>3</td><td>x3</td><td>4</td><td>y3</td></tr>
</tbody>
</table>




```R
inner_join(x, y, join_by(key < key))
```


<table class="dataframe">
<caption>A tibble: 4 x 4</caption>
<thead>
	<tr><th scope=col>key.x</th><th scope=col>val_x</th><th scope=col>key.y</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>2</td><td>y2</td></tr>
	<tr><td>1</td><td>x1</td><td>4</td><td>y3</td></tr>
	<tr><td>2</td><td>x2</td><td>4</td><td>y3</td></tr>
	<tr><td>3</td><td>x3</td><td>4</td><td>y3</td></tr>
</tbody>
</table>




```R
left_join(x, y, join_by(closest(key >= key)))
```


<table class="dataframe">
<caption>A tibble: 3 x 4</caption>
<thead>
	<tr><th scope=col>key.x</th><th scope=col>val_x</th><th scope=col>key.y</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>2</td><td>y2</td></tr>
	<tr><td>3</td><td>x3</td><td>2</td><td>y2</td></tr>
</tbody>
</table>




```R
anti_join(x, y, join_by(closest(key >= key)))
```


<table class="dataframe">
<caption>A tibble: 0 x 2</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
</tbody>
</table>



### Overlap join


```R
parties <- tibble(
  q = 1:4,
  party = ymd(c("2022-01-10", "2022-04-04", "2022-07-11", "2022-10-03")),
  start = ymd(c("2022-01-01", "2022-04-04", "2022-07-11", "2022-10-03")),
  end = ymd(c("2022-04-03", "2022-07-11", "2022-10-02", "2022-12-31"))
)
parties
```


<table class="dataframe">
<caption>A tibble: 4 x 4</caption>
<thead>
	<tr><th scope=col>q</th><th scope=col>party</th><th scope=col>start</th><th scope=col>end</th></tr>
	<tr><th scope=col>&lt;int&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;date&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-11</td></tr>
	<tr><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
</tbody>
</table>




```R
parties |> 
  inner_join(parties, join_by(overlaps(start, end, start, end), q < q)) |> 
  select(start.x, end.x, start.y, end.y)
```


<table class="dataframe">
<caption>A tibble: 1 x 4</caption>
<thead>
	<tr><th scope=col>start.x</th><th scope=col>end.x</th><th scope=col>start.y</th><th scope=col>end.y</th></tr>
	<tr><th scope=col>&lt;date&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;date&gt;</th></tr>
</thead>
<tbody>
	<tr><td>2022-04-04</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
</tbody>
</table>




```R
parties <- tibble(
  q = 1:4,
  party = ymd(c("2022-01-10", "2022-04-04", "2022-07-11", "2022-10-03")),
  start = ymd(c("2022-01-01", "2022-04-04", "2022-07-11", "2022-10-03")),
  end = ymd(c("2022-04-03", "2022-07-10", "2022-10-02", "2022-12-31"))
)
```


```R
set.seed(123)
employees <- tibble(
  name = sample(babynames::babynames$name, 100),
  birthday = ymd("2022-01-01") + (sample(365, 100, replace = TRUE) - 1)
)
employees
```


<table class="dataframe">
<caption>A tibble: 100 x 2</caption>
<thead>
	<tr><th scope=col>name</th><th scope=col>birthday</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;date&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Kemba    </td><td>2022-01-22</td></tr>
	<tr><td>Orean    </td><td>2022-06-26</td></tr>
	<tr><td>Kirstyn  </td><td>2022-02-11</td></tr>
	<tr><td>Amparo   </td><td>2022-11-11</td></tr>
	<tr><td>Belen    </td><td>2022-03-25</td></tr>
	<tr><td>Rayshaun </td><td>2022-01-11</td></tr>
	<tr><td>Brazil   </td><td>2022-05-01</td></tr>
	<tr><td>Chaston  </td><td>2022-10-29</td></tr>
	<tr><td>Reyn     </td><td>2022-03-26</td></tr>
	<tr><td>Ogechi   </td><td>2022-12-31</td></tr>
	<tr><td>Raylin   </td><td>2022-07-13</td></tr>
	<tr><td>Elisha   </td><td>2022-04-17</td></tr>
	<tr><td>Francico </td><td>2022-03-18</td></tr>
	<tr><td>Theoplis </td><td>2022-07-17</td></tr>
	<tr><td>Ashea    </td><td>2022-09-06</td></tr>
	<tr><td>Angela   </td><td>2022-07-19</td></tr>
	<tr><td>Essie    </td><td>2022-06-09</td></tr>
	<tr><td>Allyn    </td><td>2022-09-07</td></tr>
	<tr><td>Tanita   </td><td>2022-10-19</td></tr>
	<tr><td>Sherriann</td><td>2022-01-16</td></tr>
	<tr><td>Raven    </td><td>2022-02-02</td></tr>
	<tr><td>Glenys   </td><td>2022-02-09</td></tr>
	<tr><td>Li       </td><td>2022-01-10</td></tr>
	<tr><td>Miana    </td><td>2022-07-19</td></tr>
	<tr><td>Sewell   </td><td>2022-05-05</td></tr>
	<tr><td>Wayland  </td><td>2022-09-22</td></tr>
	<tr><td>Nadean   </td><td>2022-09-20</td></tr>
	<tr><td>Gregoria </td><td>2022-07-05</td></tr>
	<tr><td>Sumiye   </td><td>2022-03-02</td></tr>
	<tr><td>Norvell  </td><td>2022-09-09</td></tr>
	<tr><td>...</td><td>...</td></tr>
	<tr><td>Liora     </td><td>2022-07-31</td></tr>
	<tr><td>Andrina   </td><td>2022-08-10</td></tr>
	<tr><td>Gay       </td><td>2022-06-08</td></tr>
	<tr><td>Dustyn    </td><td>2022-12-15</td></tr>
	<tr><td>Nasiya    </td><td>2022-05-25</td></tr>
	<tr><td>Belma     </td><td>2022-02-26</td></tr>
	<tr><td>Thena     </td><td>2022-05-28</td></tr>
	<tr><td>Cooper    </td><td>2022-06-12</td></tr>
	<tr><td>Adele     </td><td>2022-08-26</td></tr>
	<tr><td>Atiana    </td><td>2022-06-10</td></tr>
	<tr><td>Jamil     </td><td>2022-03-07</td></tr>
	<tr><td>Nalani    </td><td>2022-01-04</td></tr>
	<tr><td>Nathalie  </td><td>2022-11-26</td></tr>
	<tr><td>Duriel    </td><td>2022-08-13</td></tr>
	<tr><td>Yesenia   </td><td>2022-04-27</td></tr>
	<tr><td>Sherlie   </td><td>2022-01-25</td></tr>
	<tr><td>Brooksley </td><td>2022-05-16</td></tr>
	<tr><td>Kristi    </td><td>2022-02-24</td></tr>
	<tr><td>Alethea   </td><td>2022-08-05</td></tr>
	<tr><td>Teandre   </td><td>2022-03-26</td></tr>
	<tr><td>Mohamedali</td><td>2022-02-14</td></tr>
	<tr><td>Audray    </td><td>2022-05-26</td></tr>
	<tr><td>Elta      </td><td>2022-06-19</td></tr>
	<tr><td>Suzannah  </td><td>2022-05-14</td></tr>
	<tr><td>Cleve     </td><td>2022-07-18</td></tr>
	<tr><td>Promise   </td><td>2022-12-27</td></tr>
	<tr><td>Ian       </td><td>2022-06-25</td></tr>
	<tr><td>Shelva    </td><td>2022-09-02</td></tr>
	<tr><td>Aedan     </td><td>2022-11-05</td></tr>
	<tr><td>Dorianna  </td><td>2022-04-14</td></tr>
</tbody>
</table>




```R
employees |> 
  inner_join(parties, join_by(between(birthday, start, end)), unmatched = "error")
```


<table class="dataframe">
<caption>A tibble: 100 x 6</caption>
<thead>
	<tr><th scope=col>name</th><th scope=col>birthday</th><th scope=col>q</th><th scope=col>party</th><th scope=col>start</th><th scope=col>end</th></tr>
	<tr><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;int&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;date&gt;</th><th scope=col>&lt;date&gt;</th></tr>
</thead>
<tbody>
	<tr><td>Kemba    </td><td>2022-01-22</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Orean    </td><td>2022-06-26</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Kirstyn  </td><td>2022-02-11</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Amparo   </td><td>2022-11-11</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Belen    </td><td>2022-03-25</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Rayshaun </td><td>2022-01-11</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Brazil   </td><td>2022-05-01</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Chaston  </td><td>2022-10-29</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Reyn     </td><td>2022-03-26</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Ogechi   </td><td>2022-12-31</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Raylin   </td><td>2022-07-13</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Elisha   </td><td>2022-04-17</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Francico </td><td>2022-03-18</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Theoplis </td><td>2022-07-17</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Ashea    </td><td>2022-09-06</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Angela   </td><td>2022-07-19</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Essie    </td><td>2022-06-09</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Allyn    </td><td>2022-09-07</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Tanita   </td><td>2022-10-19</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Sherriann</td><td>2022-01-16</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Raven    </td><td>2022-02-02</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Glenys   </td><td>2022-02-09</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Li       </td><td>2022-01-10</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Miana    </td><td>2022-07-19</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Sewell   </td><td>2022-05-05</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Wayland  </td><td>2022-09-22</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Nadean   </td><td>2022-09-20</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Gregoria </td><td>2022-07-05</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Sumiye   </td><td>2022-03-02</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Norvell  </td><td>2022-09-09</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td><td>...</td></tr>
	<tr><td>Liora     </td><td>2022-07-31</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Andrina   </td><td>2022-08-10</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Gay       </td><td>2022-06-08</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Dustyn    </td><td>2022-12-15</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Nasiya    </td><td>2022-05-25</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Belma     </td><td>2022-02-26</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Thena     </td><td>2022-05-28</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Cooper    </td><td>2022-06-12</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Adele     </td><td>2022-08-26</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Atiana    </td><td>2022-06-10</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Jamil     </td><td>2022-03-07</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Nalani    </td><td>2022-01-04</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Nathalie  </td><td>2022-11-26</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Duriel    </td><td>2022-08-13</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Yesenia   </td><td>2022-04-27</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Sherlie   </td><td>2022-01-25</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Brooksley </td><td>2022-05-16</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Kristi    </td><td>2022-02-24</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Alethea   </td><td>2022-08-05</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Teandre   </td><td>2022-03-26</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Mohamedali</td><td>2022-02-14</td><td>1</td><td>2022-01-10</td><td>2022-01-01</td><td>2022-04-03</td></tr>
	<tr><td>Audray    </td><td>2022-05-26</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Elta      </td><td>2022-06-19</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Suzannah  </td><td>2022-05-14</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Cleve     </td><td>2022-07-18</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Promise   </td><td>2022-12-27</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Ian       </td><td>2022-06-25</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
	<tr><td>Shelva    </td><td>2022-09-02</td><td>3</td><td>2022-07-11</td><td>2022-07-11</td><td>2022-10-02</td></tr>
	<tr><td>Aedan     </td><td>2022-11-05</td><td>4</td><td>2022-10-03</td><td>2022-10-03</td><td>2022-12-31</td></tr>
	<tr><td>Dorianna  </td><td>2022-04-14</td><td>2</td><td>2022-04-04</td><td>2022-04-04</td><td>2022-07-10</td></tr>
</tbody>
</table>



### Exercises


```R
x |> full_join(y, join_by(key == key))
```


<table class="dataframe">
<caption>A tibble: 4 x 3</caption>
<thead>
	<tr><th scope=col>key</th><th scope=col>val_x</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td>1</td><td>x1</td><td>y1</td></tr>
	<tr><td>2</td><td>x2</td><td>y2</td></tr>
	<tr><td>3</td><td>x3</td><td>NA</td></tr>
	<tr><td>4</td><td>NA</td><td>y3</td></tr>
</tbody>
</table>




```R
x |> full_join(y, join_by(key == key), keep = TRUE)
```


<table class="dataframe">
<caption>A tibble: 4 x 4</caption>
<thead>
	<tr><th scope=col>key.x</th><th scope=col>val_x</th><th scope=col>key.y</th><th scope=col>val_y</th></tr>
	<tr><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th><th scope=col>&lt;dbl&gt;</th><th scope=col>&lt;chr&gt;</th></tr>
</thead>
<tbody>
	<tr><td> 1</td><td>x1</td><td> 1</td><td>y1</td></tr>
	<tr><td> 2</td><td>x2</td><td> 2</td><td>y2</td></tr>
	<tr><td> 3</td><td>x3</td><td>NA</td><td>NA</td></tr>
	<tr><td>NA</td><td>NA</td><td> 4</td><td>y3</td></tr>
</tbody>
</table>



2. When finding if any party period overlapped with another party period we used q < q in the join_by()? Why? What happens if you remove this inequality?`


