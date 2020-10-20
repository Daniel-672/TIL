

# 분석Day05

>  데이터 수집 & pandas

### - 교육내용

```python
# 예제 2-1
# 라이브러리 불러오기
import pandas as pd

# 파일경로를 찾고, 변수 file_path에 저장
file_path = './data/read_csv_sample.csv'

# read_csv() 함수로 데이터프레임 변환. 변수 df1에 저장
df1 = pd.read_csv(file_path)
print(df1)
display(df1)
print('\n')

# read_csv() 함수로 데이터프레임 변환. 변수 df2에 저장. header=None 옵션
df2 = pd.read_csv(file_path, header=None)
print(df2)
display(df2)
print('\n')

# read_csv() 함수로 데이터프레임 변환. 변수 df3에 저장. index_col=None 옵션
df3 = pd.read_csv(file_path, index_col=None)
print(df3)
display(df3)
print('\n')

# read_csv() 함수로 데이터프레임 변환. 변수 df4에 저장. index_col='c0' 옵션
df4 = pd.read_csv(file_path, index_col='c0')
print(df4)
display(df4)
```

       c0  c1  c2  c3
    0   0   1   4   7
    1   1   2   5   8
    2   2   3   6   9



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

</div>


​    
​    

        0   1   2   3
    0  c0  c1  c2  c3
    1   0   1   4   7
    2   1   2   5   8
    3   2   3   6   9



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>c0</td>
      <td>c1</td>
      <td>c2</td>
      <td>c3</td>
    </tr>
    <tr>
      <th>1</th>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>2</th>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

</div>


​    
​    

       c0  c1  c2  c3
    0   0   1   4   7
    1   1   2   5   8
    2   2   3   6   9



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>c0</th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>0</td>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>1</td>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2</td>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

</div>


​    
​    

        c1  c2  c3
    c0            
    0    1   4   7
    1    2   5   8
    2    3   6   9



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>c1</th>
      <th>c2</th>
      <th>c3</th>
    </tr>
    <tr>
      <th>c0</th>
      <th></th>
      <th></th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>1</td>
      <td>4</td>
      <td>7</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2</td>
      <td>5</td>
      <td>8</td>
    </tr>
    <tr>
      <th>2</th>
      <td>3</td>
      <td>6</td>
      <td>9</td>
    </tr>
  </tbody>
</table>

</div>



```python
# 예제 2-2
import pandas as pd

# read_excel() 함수로 데이터프레임 변환 
df1 = pd.read_excel('./data/남북한발전전력량.xlsx')            # header=0 (default 옵션)
df2 = pd.read_excel('./data/남북한발전전력량.xlsx', header=None)  # header=None 옵션

# 데이터프레임 출력
print(df1)
display(df1)
print(df2)
display(df2)
pd.get_option('display.max_columns')
```

      전력량 (억㎾h) 발전 전력별  1990  1991  1992  1993  1994  1995  1996  1997  ...  2007  \
    0        남한     합계  1077  1186  1310  1444  1650  1847  2055  2244  ...  4031   
    1       NaN     수력    64    51    49    60    41    55    52    54  ...    50   
    2       NaN     화력   484   573   696   803  1022  1122  1264  1420  ...  2551   
    3       NaN    원자력   529   563   565   581   587   670   739   771  ...  1429   
    4       NaN    신재생     -     -     -     -     -     -     -     -  ...     -   
    5        북한     합계   277   263   247   221   231   230   213   193  ...   236   
    6       NaN     수력   156   150   142   133   138   142   125   107  ...   133   
    7       NaN     화력   121   113   105    88    93    88    88    86  ...   103   
    8       NaN    원자력     -     -     -     -     -     -     -     -  ...     -   
    
       2008  2009  2010  2011  2012  2013  2014  2015  2016  
    0  4224  4336  4747  4969  5096  5171  5220  5281  5404  
    1    56    56    65    78    77    84    78    58    66  
    2  2658  2802  3196  3343  3430  3581  3427  3402  3523  
    3  1510  1478  1486  1547  1503  1388  1564  1648  1620  
    4     -     -     -     -    86   118   151   173   195  
    5   255   235   237   211   215   221   216   190   239  
    6   141   125   134   132   135   139   130   100   128  
    7   114   110   103    79    80    82    86    90   111  
    8     -     -     -     -     -     -     -     -     -  
    
    [9 rows x 29 columns]



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>전력량 (억㎾h)</th>
      <th>발전 전력별</th>
      <th>1990</th>
      <th>1991</th>
      <th>1992</th>
      <th>1993</th>
      <th>1994</th>
      <th>1995</th>
      <th>1996</th>
      <th>1997</th>
      <th>...</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>남한</td>
      <td>합계</td>
      <td>1077</td>
      <td>1186</td>
      <td>1310</td>
      <td>1444</td>
      <td>1650</td>
      <td>1847</td>
      <td>2055</td>
      <td>2244</td>
      <td>...</td>
      <td>4031</td>
      <td>4224</td>
      <td>4336</td>
      <td>4747</td>
      <td>4969</td>
      <td>5096</td>
      <td>5171</td>
      <td>5220</td>
      <td>5281</td>
      <td>5404</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>수력</td>
      <td>64</td>
      <td>51</td>
      <td>49</td>
      <td>60</td>
      <td>41</td>
      <td>55</td>
      <td>52</td>
      <td>54</td>
      <td>...</td>
      <td>50</td>
      <td>56</td>
      <td>56</td>
      <td>65</td>
      <td>78</td>
      <td>77</td>
      <td>84</td>
      <td>78</td>
      <td>58</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>화력</td>
      <td>484</td>
      <td>573</td>
      <td>696</td>
      <td>803</td>
      <td>1022</td>
      <td>1122</td>
      <td>1264</td>
      <td>1420</td>
      <td>...</td>
      <td>2551</td>
      <td>2658</td>
      <td>2802</td>
      <td>3196</td>
      <td>3343</td>
      <td>3430</td>
      <td>3581</td>
      <td>3427</td>
      <td>3402</td>
      <td>3523</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>529</td>
      <td>563</td>
      <td>565</td>
      <td>581</td>
      <td>587</td>
      <td>670</td>
      <td>739</td>
      <td>771</td>
      <td>...</td>
      <td>1429</td>
      <td>1510</td>
      <td>1478</td>
      <td>1486</td>
      <td>1547</td>
      <td>1503</td>
      <td>1388</td>
      <td>1564</td>
      <td>1648</td>
      <td>1620</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>신재생</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>...</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>86</td>
      <td>118</td>
      <td>151</td>
      <td>173</td>
      <td>195</td>
    </tr>
    <tr>
      <th>5</th>
      <td>북한</td>
      <td>합계</td>
      <td>277</td>
      <td>263</td>
      <td>247</td>
      <td>221</td>
      <td>231</td>
      <td>230</td>
      <td>213</td>
      <td>193</td>
      <td>...</td>
      <td>236</td>
      <td>255</td>
      <td>235</td>
      <td>237</td>
      <td>211</td>
      <td>215</td>
      <td>221</td>
      <td>216</td>
      <td>190</td>
      <td>239</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>수력</td>
      <td>156</td>
      <td>150</td>
      <td>142</td>
      <td>133</td>
      <td>138</td>
      <td>142</td>
      <td>125</td>
      <td>107</td>
      <td>...</td>
      <td>133</td>
      <td>141</td>
      <td>125</td>
      <td>134</td>
      <td>132</td>
      <td>135</td>
      <td>139</td>
      <td>130</td>
      <td>100</td>
      <td>128</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>화력</td>
      <td>121</td>
      <td>113</td>
      <td>105</td>
      <td>88</td>
      <td>93</td>
      <td>88</td>
      <td>88</td>
      <td>86</td>
      <td>...</td>
      <td>103</td>
      <td>114</td>
      <td>110</td>
      <td>103</td>
      <td>79</td>
      <td>80</td>
      <td>82</td>
      <td>86</td>
      <td>90</td>
      <td>111</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>...</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>
<p>9 rows × 29 columns</p>

</div>


              0       1     2     3     4     5     6     7     8     9   ...  \
    0  전력량 (억㎾h)  발전 전력별  1990  1991  1992  1993  1994  1995  1996  1997  ...   
    1         남한      합계  1077  1186  1310  1444  1650  1847  2055  2244  ...   
    2        NaN      수력    64    51    49    60    41    55    52    54  ...   
    3        NaN      화력   484   573   696   803  1022  1122  1264  1420  ...   
    4        NaN     원자력   529   563   565   581   587   670   739   771  ...   
    5        NaN     신재생     -     -     -     -     -     -     -     -  ...   
    6         북한      합계   277   263   247   221   231   230   213   193  ...   
    7        NaN      수력   156   150   142   133   138   142   125   107  ...   
    8        NaN      화력   121   113   105    88    93    88    88    86  ...   
    9        NaN     원자력     -     -     -     -     -     -     -     -  ...   
    
         19    20    21    22    23    24    25    26    27    28  
    0  2007  2008  2009  2010  2011  2012  2013  2014  2015  2016  
    1  4031  4224  4336  4747  4969  5096  5171  5220  5281  5404  
    2    50    56    56    65    78    77    84    78    58    66  
    3  2551  2658  2802  3196  3343  3430  3581  3427  3402  3523  
    4  1429  1510  1478  1486  1547  1503  1388  1564  1648  1620  
    5     -     -     -     -     -    86   118   151   173   195  
    6   236   255   235   237   211   215   221   216   190   239  
    7   133   141   125   134   132   135   139   130   100   128  
    8   103   114   110   103    79    80    82    86    90   111  
    9     -     -     -     -     -     -     -     -     -     -  
    
    [10 rows x 29 columns]



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>...</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
      <th>22</th>
      <th>23</th>
      <th>24</th>
      <th>25</th>
      <th>26</th>
      <th>27</th>
      <th>28</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>전력량 (억㎾h)</td>
      <td>발전 전력별</td>
      <td>1990</td>
      <td>1991</td>
      <td>1992</td>
      <td>1993</td>
      <td>1994</td>
      <td>1995</td>
      <td>1996</td>
      <td>1997</td>
      <td>...</td>
      <td>2007</td>
      <td>2008</td>
      <td>2009</td>
      <td>2010</td>
      <td>2011</td>
      <td>2012</td>
      <td>2013</td>
      <td>2014</td>
      <td>2015</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>1</th>
      <td>남한</td>
      <td>합계</td>
      <td>1077</td>
      <td>1186</td>
      <td>1310</td>
      <td>1444</td>
      <td>1650</td>
      <td>1847</td>
      <td>2055</td>
      <td>2244</td>
      <td>...</td>
      <td>4031</td>
      <td>4224</td>
      <td>4336</td>
      <td>4747</td>
      <td>4969</td>
      <td>5096</td>
      <td>5171</td>
      <td>5220</td>
      <td>5281</td>
      <td>5404</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>수력</td>
      <td>64</td>
      <td>51</td>
      <td>49</td>
      <td>60</td>
      <td>41</td>
      <td>55</td>
      <td>52</td>
      <td>54</td>
      <td>...</td>
      <td>50</td>
      <td>56</td>
      <td>56</td>
      <td>65</td>
      <td>78</td>
      <td>77</td>
      <td>84</td>
      <td>78</td>
      <td>58</td>
      <td>66</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>화력</td>
      <td>484</td>
      <td>573</td>
      <td>696</td>
      <td>803</td>
      <td>1022</td>
      <td>1122</td>
      <td>1264</td>
      <td>1420</td>
      <td>...</td>
      <td>2551</td>
      <td>2658</td>
      <td>2802</td>
      <td>3196</td>
      <td>3343</td>
      <td>3430</td>
      <td>3581</td>
      <td>3427</td>
      <td>3402</td>
      <td>3523</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>529</td>
      <td>563</td>
      <td>565</td>
      <td>581</td>
      <td>587</td>
      <td>670</td>
      <td>739</td>
      <td>771</td>
      <td>...</td>
      <td>1429</td>
      <td>1510</td>
      <td>1478</td>
      <td>1486</td>
      <td>1547</td>
      <td>1503</td>
      <td>1388</td>
      <td>1564</td>
      <td>1648</td>
      <td>1620</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>신재생</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>...</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>86</td>
      <td>118</td>
      <td>151</td>
      <td>173</td>
      <td>195</td>
    </tr>
    <tr>
      <th>6</th>
      <td>북한</td>
      <td>합계</td>
      <td>277</td>
      <td>263</td>
      <td>247</td>
      <td>221</td>
      <td>231</td>
      <td>230</td>
      <td>213</td>
      <td>193</td>
      <td>...</td>
      <td>236</td>
      <td>255</td>
      <td>235</td>
      <td>237</td>
      <td>211</td>
      <td>215</td>
      <td>221</td>
      <td>216</td>
      <td>190</td>
      <td>239</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>수력</td>
      <td>156</td>
      <td>150</td>
      <td>142</td>
      <td>133</td>
      <td>138</td>
      <td>142</td>
      <td>125</td>
      <td>107</td>
      <td>...</td>
      <td>133</td>
      <td>141</td>
      <td>125</td>
      <td>134</td>
      <td>132</td>
      <td>135</td>
      <td>139</td>
      <td>130</td>
      <td>100</td>
      <td>128</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>화력</td>
      <td>121</td>
      <td>113</td>
      <td>105</td>
      <td>88</td>
      <td>93</td>
      <td>88</td>
      <td>88</td>
      <td>86</td>
      <td>...</td>
      <td>103</td>
      <td>114</td>
      <td>110</td>
      <td>103</td>
      <td>79</td>
      <td>80</td>
      <td>82</td>
      <td>86</td>
      <td>90</td>
      <td>111</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>...</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>
<p>10 rows × 29 columns</p>

</div>



```python
pd.set_option('display.max_columns', 100)

import pandas as pd

# read_excel() 함수로 데이터프레임 변환 
df1 = pd.read_excel('./data/남북한발전전력량.xlsx')            # header=0 (default 옵션)
df2 = pd.read_excel('./data/남북한발전전력량.xlsx', header=None)  # header=None 옵션

# 데이터프레임 출력
display(df1)
display(df2)
```


<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>전력량 (억㎾h)</th>
      <th>발전 전력별</th>
      <th>1990</th>
      <th>1991</th>
      <th>1992</th>
      <th>1993</th>
      <th>1994</th>
      <th>1995</th>
      <th>1996</th>
      <th>1997</th>
      <th>1998</th>
      <th>1999</th>
      <th>2000</th>
      <th>2001</th>
      <th>2002</th>
      <th>2003</th>
      <th>2004</th>
      <th>2005</th>
      <th>2006</th>
      <th>2007</th>
      <th>2008</th>
      <th>2009</th>
      <th>2010</th>
      <th>2011</th>
      <th>2012</th>
      <th>2013</th>
      <th>2014</th>
      <th>2015</th>
      <th>2016</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>남한</td>
      <td>합계</td>
      <td>1077</td>
      <td>1186</td>
      <td>1310</td>
      <td>1444</td>
      <td>1650</td>
      <td>1847</td>
      <td>2055</td>
      <td>2244</td>
      <td>2153</td>
      <td>2393</td>
      <td>2664</td>
      <td>2852</td>
      <td>3065</td>
      <td>3225</td>
      <td>3421</td>
      <td>3646</td>
      <td>3812</td>
      <td>4031</td>
      <td>4224</td>
      <td>4336</td>
      <td>4747</td>
      <td>4969</td>
      <td>5096</td>
      <td>5171</td>
      <td>5220</td>
      <td>5281</td>
      <td>5404</td>
    </tr>
    <tr>
      <th>1</th>
      <td>NaN</td>
      <td>수력</td>
      <td>64</td>
      <td>51</td>
      <td>49</td>
      <td>60</td>
      <td>41</td>
      <td>55</td>
      <td>52</td>
      <td>54</td>
      <td>61</td>
      <td>61</td>
      <td>56</td>
      <td>42</td>
      <td>53</td>
      <td>69</td>
      <td>59</td>
      <td>52</td>
      <td>52</td>
      <td>50</td>
      <td>56</td>
      <td>56</td>
      <td>65</td>
      <td>78</td>
      <td>77</td>
      <td>84</td>
      <td>78</td>
      <td>58</td>
      <td>66</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>화력</td>
      <td>484</td>
      <td>573</td>
      <td>696</td>
      <td>803</td>
      <td>1022</td>
      <td>1122</td>
      <td>1264</td>
      <td>1420</td>
      <td>1195</td>
      <td>1302</td>
      <td>1518</td>
      <td>1689</td>
      <td>1821</td>
      <td>1859</td>
      <td>2056</td>
      <td>2127</td>
      <td>2272</td>
      <td>2551</td>
      <td>2658</td>
      <td>2802</td>
      <td>3196</td>
      <td>3343</td>
      <td>3430</td>
      <td>3581</td>
      <td>3427</td>
      <td>3402</td>
      <td>3523</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>529</td>
      <td>563</td>
      <td>565</td>
      <td>581</td>
      <td>587</td>
      <td>670</td>
      <td>739</td>
      <td>771</td>
      <td>897</td>
      <td>1031</td>
      <td>1090</td>
      <td>1121</td>
      <td>1191</td>
      <td>1297</td>
      <td>1307</td>
      <td>1468</td>
      <td>1487</td>
      <td>1429</td>
      <td>1510</td>
      <td>1478</td>
      <td>1486</td>
      <td>1547</td>
      <td>1503</td>
      <td>1388</td>
      <td>1564</td>
      <td>1648</td>
      <td>1620</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>신재생</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>86</td>
      <td>118</td>
      <td>151</td>
      <td>173</td>
      <td>195</td>
    </tr>
    <tr>
      <th>5</th>
      <td>북한</td>
      <td>합계</td>
      <td>277</td>
      <td>263</td>
      <td>247</td>
      <td>221</td>
      <td>231</td>
      <td>230</td>
      <td>213</td>
      <td>193</td>
      <td>170</td>
      <td>186</td>
      <td>194</td>
      <td>202</td>
      <td>190</td>
      <td>196</td>
      <td>206</td>
      <td>215</td>
      <td>225</td>
      <td>236</td>
      <td>255</td>
      <td>235</td>
      <td>237</td>
      <td>211</td>
      <td>215</td>
      <td>221</td>
      <td>216</td>
      <td>190</td>
      <td>239</td>
    </tr>
    <tr>
      <th>6</th>
      <td>NaN</td>
      <td>수력</td>
      <td>156</td>
      <td>150</td>
      <td>142</td>
      <td>133</td>
      <td>138</td>
      <td>142</td>
      <td>125</td>
      <td>107</td>
      <td>102</td>
      <td>103</td>
      <td>102</td>
      <td>106</td>
      <td>106</td>
      <td>117</td>
      <td>125</td>
      <td>131</td>
      <td>126</td>
      <td>133</td>
      <td>141</td>
      <td>125</td>
      <td>134</td>
      <td>132</td>
      <td>135</td>
      <td>139</td>
      <td>130</td>
      <td>100</td>
      <td>128</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>화력</td>
      <td>121</td>
      <td>113</td>
      <td>105</td>
      <td>88</td>
      <td>93</td>
      <td>88</td>
      <td>88</td>
      <td>86</td>
      <td>68</td>
      <td>83</td>
      <td>92</td>
      <td>96</td>
      <td>84</td>
      <td>79</td>
      <td>81</td>
      <td>84</td>
      <td>99</td>
      <td>103</td>
      <td>114</td>
      <td>110</td>
      <td>103</td>
      <td>79</td>
      <td>80</td>
      <td>82</td>
      <td>86</td>
      <td>90</td>
      <td>111</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

</div>



<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }


    .dataframe tbody tr th {
        vertical-align: top;
    }
    
    .dataframe thead th {
        text-align: right;
    }

</style>

<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
      <th>1</th>
      <th>2</th>
      <th>3</th>
      <th>4</th>
      <th>5</th>
      <th>6</th>
      <th>7</th>
      <th>8</th>
      <th>9</th>
      <th>10</th>
      <th>11</th>
      <th>12</th>
      <th>13</th>
      <th>14</th>
      <th>15</th>
      <th>16</th>
      <th>17</th>
      <th>18</th>
      <th>19</th>
      <th>20</th>
      <th>21</th>
      <th>22</th>
      <th>23</th>
      <th>24</th>
      <th>25</th>
      <th>26</th>
      <th>27</th>
      <th>28</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>전력량 (억㎾h)</td>
      <td>발전 전력별</td>
      <td>1990</td>
      <td>1991</td>
      <td>1992</td>
      <td>1993</td>
      <td>1994</td>
      <td>1995</td>
      <td>1996</td>
      <td>1997</td>
      <td>1998</td>
      <td>1999</td>
      <td>2000</td>
      <td>2001</td>
      <td>2002</td>
      <td>2003</td>
      <td>2004</td>
      <td>2005</td>
      <td>2006</td>
      <td>2007</td>
      <td>2008</td>
      <td>2009</td>
      <td>2010</td>
      <td>2011</td>
      <td>2012</td>
      <td>2013</td>
      <td>2014</td>
      <td>2015</td>
      <td>2016</td>
    </tr>
    <tr>
      <th>1</th>
      <td>남한</td>
      <td>합계</td>
      <td>1077</td>
      <td>1186</td>
      <td>1310</td>
      <td>1444</td>
      <td>1650</td>
      <td>1847</td>
      <td>2055</td>
      <td>2244</td>
      <td>2153</td>
      <td>2393</td>
      <td>2664</td>
      <td>2852</td>
      <td>3065</td>
      <td>3225</td>
      <td>3421</td>
      <td>3646</td>
      <td>3812</td>
      <td>4031</td>
      <td>4224</td>
      <td>4336</td>
      <td>4747</td>
      <td>4969</td>
      <td>5096</td>
      <td>5171</td>
      <td>5220</td>
      <td>5281</td>
      <td>5404</td>
    </tr>
    <tr>
      <th>2</th>
      <td>NaN</td>
      <td>수력</td>
      <td>64</td>
      <td>51</td>
      <td>49</td>
      <td>60</td>
      <td>41</td>
      <td>55</td>
      <td>52</td>
      <td>54</td>
      <td>61</td>
      <td>61</td>
      <td>56</td>
      <td>42</td>
      <td>53</td>
      <td>69</td>
      <td>59</td>
      <td>52</td>
      <td>52</td>
      <td>50</td>
      <td>56</td>
      <td>56</td>
      <td>65</td>
      <td>78</td>
      <td>77</td>
      <td>84</td>
      <td>78</td>
      <td>58</td>
      <td>66</td>
    </tr>
    <tr>
      <th>3</th>
      <td>NaN</td>
      <td>화력</td>
      <td>484</td>
      <td>573</td>
      <td>696</td>
      <td>803</td>
      <td>1022</td>
      <td>1122</td>
      <td>1264</td>
      <td>1420</td>
      <td>1195</td>
      <td>1302</td>
      <td>1518</td>
      <td>1689</td>
      <td>1821</td>
      <td>1859</td>
      <td>2056</td>
      <td>2127</td>
      <td>2272</td>
      <td>2551</td>
      <td>2658</td>
      <td>2802</td>
      <td>3196</td>
      <td>3343</td>
      <td>3430</td>
      <td>3581</td>
      <td>3427</td>
      <td>3402</td>
      <td>3523</td>
    </tr>
    <tr>
      <th>4</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>529</td>
      <td>563</td>
      <td>565</td>
      <td>581</td>
      <td>587</td>
      <td>670</td>
      <td>739</td>
      <td>771</td>
      <td>897</td>
      <td>1031</td>
      <td>1090</td>
      <td>1121</td>
      <td>1191</td>
      <td>1297</td>
      <td>1307</td>
      <td>1468</td>
      <td>1487</td>
      <td>1429</td>
      <td>1510</td>
      <td>1478</td>
      <td>1486</td>
      <td>1547</td>
      <td>1503</td>
      <td>1388</td>
      <td>1564</td>
      <td>1648</td>
      <td>1620</td>
    </tr>
    <tr>
      <th>5</th>
      <td>NaN</td>
      <td>신재생</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>86</td>
      <td>118</td>
      <td>151</td>
      <td>173</td>
      <td>195</td>
    </tr>
    <tr>
      <th>6</th>
      <td>북한</td>
      <td>합계</td>
      <td>277</td>
      <td>263</td>
      <td>247</td>
      <td>221</td>
      <td>231</td>
      <td>230</td>
      <td>213</td>
      <td>193</td>
      <td>170</td>
      <td>186</td>
      <td>194</td>
      <td>202</td>
      <td>190</td>
      <td>196</td>
      <td>206</td>
      <td>215</td>
      <td>225</td>
      <td>236</td>
      <td>255</td>
      <td>235</td>
      <td>237</td>
      <td>211</td>
      <td>215</td>
      <td>221</td>
      <td>216</td>
      <td>190</td>
      <td>239</td>
    </tr>
    <tr>
      <th>7</th>
      <td>NaN</td>
      <td>수력</td>
      <td>156</td>
      <td>150</td>
      <td>142</td>
      <td>133</td>
      <td>138</td>
      <td>142</td>
      <td>125</td>
      <td>107</td>
      <td>102</td>
      <td>103</td>
      <td>102</td>
      <td>106</td>
      <td>106</td>
      <td>117</td>
      <td>125</td>
      <td>131</td>
      <td>126</td>
      <td>133</td>
      <td>141</td>
      <td>125</td>
      <td>134</td>
      <td>132</td>
      <td>135</td>
      <td>139</td>
      <td>130</td>
      <td>100</td>
      <td>128</td>
    </tr>
    <tr>
      <th>8</th>
      <td>NaN</td>
      <td>화력</td>
      <td>121</td>
      <td>113</td>
      <td>105</td>
      <td>88</td>
      <td>93</td>
      <td>88</td>
      <td>88</td>
      <td>86</td>
      <td>68</td>
      <td>83</td>
      <td>92</td>
      <td>96</td>
      <td>84</td>
      <td>79</td>
      <td>81</td>
      <td>84</td>
      <td>99</td>
      <td>103</td>
      <td>114</td>
      <td>110</td>
      <td>103</td>
      <td>79</td>
      <td>80</td>
      <td>82</td>
      <td>86</td>
      <td>90</td>
      <td>111</td>
    </tr>
    <tr>
      <th>9</th>
      <td>NaN</td>
      <td>원자력</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
      <td>-</td>
    </tr>
  </tbody>
</table>

</div>



```python
pd.reset_option("^display")
```




    20




```python
# 예제 2-3
import pandas as pd

# read_json() 함수로 데이터프레임 변환 
df = pd.read_json('./data/read_json_sample.json')  
print(df)
print('\n')
print(df.index)
```

               name  year        developer opensource
    pandas           2008    Wes Mckinneye       True
    NumPy            2006  Travis Oliphant       True
    matplotlib       2003   John D. Hunter       True


​    

    Index(['pandas', 'NumPy', 'matplotlib'], dtype='object')



```python
# 예제 2-4
import pandas as pd

# HTML 파일 경로 or 웹 페이지 주소를 url 변수에 저장
url ='./data/sample.html'

# HTML 웹페이지의 표(table)를 가져와서 데이터프레임으로 변환 
tables = pd.read_html(url)

# 표(table)의 개수 확인
print(len(tables))
print('\n')

# tables 리스트의 원소를 iteration하면서 각각 화면 출력
for i in range(len(tables)):
    print("tables[%s]" % i)
    print(tables[i])
    print('\n')

# 파이썬 패키지 정보가 들어 있는 두 번째 데이터프레임을 선택하여 df 변수에 저장
df = tables[1] 

# 'name' 열을 인덱스로 지정
df.set_index(['name'], inplace=True)
print(df)
```

    2


​    

    tables[0]
       Unnamed: 0  c0  c1  c2  c3
    0           0   0   1   4   7
    1           1   1   2   5   8
    2           2   2   3   6   9


​    

    tables[1]
             name  year        developer  opensource
    0       NumPy  2006  Travis Oliphant        True
    1  matplotlib  2003   John D. Hunter        True
    2      pandas  2008    Wes Mckinneye        True


​    

                year        developer  opensource
    name                                         
    NumPy       2006  Travis Oliphant        True
    matplotlib  2003   John D. Hunter        True
    pandas      2008    Wes Mckinneye        True



```python
## google 지오코딩 API 통해 위도, 경도 데이터 가져오기 
# 예제 2-6
# 라이브러리 가져오기
import googlemaps
import pandas as pd

my_key = "AIzaSyDy81EbO46BRSnX1DOgg_F84bhsdbku2z4"

# 구글맵스 객체 생성하기
maps = googlemaps.Client(key=my_key)  # my key값 입력

lat = []  #위도
lng = []  #경도

# 장소(또는 주소) 리스트
places = ["서울시청", "국립국악원", "해운대해수욕장"]

i=0
for place in places:   
    i = i + 1
    try:
        print(i, place)
        # 지오코딩 API 결과값 호출하여 geo_location 변수에 저장
        geo_location = maps.geocode(place)[0].get('geometry')
        lat.append(geo_location['location']['lat'])
        lng.append(geo_location['location']['lng'])
        

    except:
        lat.append('')
        lng.append('')
        print(i)

# 데이터프레임으로 변환하기
df = pd.DataFrame({'위도':lat, '경도':lng}, index=places)
print('\n')
print(df)
```

    1 서울시청
    2 국립국악원
    3 해운대해수욕장


​    

                    위도          경도
    서울시청     37.566295  126.977945
    국립국악원    37.477759  127.008304
    해운대해수욕장  35.158698  129.160384



```python
# 예제 2-7
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
data = {'name' : [ 'Jerry', 'Riah', 'Paul'],
        'algol' : [ "A", "A+", "B"],
        'basic' : [ "C", "B", "B+"],
        'c++' : [ "B+", "C", "C+"],
        }

df = pd.DataFrame(data)
df.set_index('name', inplace=True)   #name 열을 인덱스로 지정
print(df)

# to_csv() 메소드를 사용하여 CSV 파일로 내보내기. 파열명은 df_sample.csv로 저장
df.to_csv("./output/df_sample.csv")
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+



```python
# 예제 2-8
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
data = {'name' : [ 'Jerry', 'Riah', 'Paul'],
        'algol' : [ "A", "A+", "B"],
        'basic' : [ "C", "B", "B+"],
        'c++' : [ "B+", "C", "C+"],
        }

df = pd.DataFrame(data)
df.set_index('name', inplace=True)   #name 열을 인덱스로 지정
print(df)

# to_json() 메소드를 사용하여 JSON 파일로 내보내기. 파열명은 df_sample.json로 저장
df.to_json("./output/df_sample.json")
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+



```python
# 예제 2-9
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df에 저장 
data = {'name' : [ 'Jerry', 'Riah', 'Paul'],
        'algol' : [ "A", "A+", "B"],
        'basic' : [ "C", "B", "B+"],
        'c++' : [ "B+", "C", "C+"],
        }

df = pd.DataFrame(data)
df.set_index('name', inplace=True)   #name 열을 인덱스로 지정
print(df)

# to_excel() 메소드를 사용하여 엑셀 파일로 내보내기. 파열명은 df_sample.xlsx로 저장
df.to_excel("./output/df_sample.xlsx")
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+



```python
# 예제 2-10
import pandas as pd

# 판다스 DataFrame() 함수로 데이터프레임 변환. 변수 df1, df2에 저장 
data1 = {'name' : [ 'Jerry', 'Riah', 'Paul'],
         'algol' : [ "A", "A+", "B"],
         'basic' : [ "C", "B", "B+"],
          'c++' : [ "B+", "C", "C+"]}

data2 = {'c0':[1,2,3], 
         'c1':[4,5,6], 
         'c2':[7,8,9], 
         'c3':[10,11,12], 
         'c4':[13,14,15]}

df1 = pd.DataFrame(data1)
df1.set_index('name', inplace=True)      #name 열을 인덱스로 지정
print(df1)
print('\n')

df2 = pd.DataFrame(data2)
df2.set_index('c0', inplace=True)        #c0 열을 인덱스로 지정
print(df2)

# df1을 'sheet1'으로, df2를 'sheet2'로 저장 (엑셀파일명은 "df_excelwriter.xlsx")
writer = pd.ExcelWriter("./output/df_excelwriter.xlsx")
df1.to_excel(writer, sheet_name="sheet1")
df2.to_excel(writer, sheet_name="sheet2")
writer.save()
```

          algol basic c++
    name                 
    Jerry     A     C  B+
    Riah     A+     B   C
    Paul      B    B+  C+


​    

        c1  c2  c3  c4
    c0                
    1    4   7  10  13
    2    5   8  11  14
    3    6   9  12  15



### - 실습

```python
# 함수버전
import urllib.request
import json
from bs4 import BeautifulSoup

def naver_search (keyword, callType = 'JSON') :
    client_key = 'izGsqP2exeThwwEUVU3x'
    client_secret = 'WrwbQ1l6ZI'
    query = keyword
    encText = urllib.parse.quote_plus(query)

    num = 5
    if callType == 'JSON' :
        urlhead = 'https://openapi.naver.com/v1/search/local.json?query='
    elif callType == 'XML' :
        urlhead = 'https://openapi.naver.com/v1/search/local.xml?query='
    else :
        print('JSON or XML only')
        return
    
    naver_url = urlhead + encText + '&display=' + str(num)

    request = urllib.request.Request(naver_url)
    request.add_header("X-Naver-Client-Id",client_key)
    request.add_header("X-Naver-Client-Secret",client_secret)
    response = urllib.request.urlopen(request)
    rescode = response.getcode()

    if(rescode == 200):
        response_body = response.read()
        count = 1        
        if callType == 'JSON' :
            dataList = json.loads(response_body)
            print(type(dataList))
            print('[' + query + '에 대한 네이버 지역 정보(JSON)]')
            for data in dataList['items'] :
                print (str(count) + ' : ' + data['title'] + ',' + data['telephone'] + ',' + data['address'])
                count += 1
        elif callType == 'XML' :
            xmlsoup = BeautifulSoup(response_body, 'xml')
            items = xmlsoup.find_all('item')
            print(type(items))
            print('[' + query + '에 대한 네이버 지역 정보(XML)]')
            for data in items:
                print (str(count) + ' : ' + data.title.string + ',' + ('없음' if data.telephone.string == None else data.telephone.string) + ',' + data.address.string)
                count += 1
    else:
        print('오류 코드 : ' + rescode)

naver_search('쌀국수', 'XML')
print('***')
naver_search('쌀국수', 'JSON')
```

```python
import pandas as pd

# 문제 1
data = {
    'name':['둘리', '또치', '도우너', '희동이'],
    'kor':[90, 80, 70, 70],
    'eng':[99, 98, 97, 46],
    'mat':[90, 70, 70, 60],
}
df = pd.DataFrame(data)
print(df)

df['class'] = [str(x) + '반' for x in range(1, 3)] * 2
print(df)
```

      name  kor  eng  mat
    0   둘리   90   99   90
    1   또치   80   98   70
    2  도우너   70   97   70
    3  희동이   70   46   60
      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반



```python
# 문제 2
print(df)

df.loc[4] = ['마이콜', 80, 80, 80, '1반']
print(df)
```

      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반
      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반
    4  마이콜   80   80   80    1반



```python
# 문제 3
print(df)

df.set_index('name', inplace=True)
df.columns=['국어', '영어', '수학', '반번호']
print(df)
```

      name  kor  eng  mat class
    0   둘리   90   99   90    1반
    1   또치   80   98   70    2반
    2  도우너   70   97   70    1반
    3  희동이   70   46   60    2반
    4  마이콜   80   80   80    1반
          국어  영어  수학 반번호
    name                
    둘리    90  99  90  1반
    또치    80  98  70  2반
    도우너   70  97  70  1반
    희동이   70  46  60  2반
    마이콜   80  80  80  1반



```python
# 문제 4
print(df)

df.loc['마이콜', '국어':'수학'] = 100
df.loc['희동이', '영어'] = 90
print(df)
```

          국어  영어  수학 반번호
    name                
    둘리    90  99  90  1반
    또치    80  98  70  2반
    도우너   70  97  70  1반
    희동이   70  46  60  2반
    마이콜   80  80  80  1반
           국어   영어   수학 반번호
    name                   
    둘리     90   99   90  1반
    또치     80   98   70  2반
    도우너    70   97   70  1반
    희동이    70   90   60  2반
    마이콜   100  100  100  1반



```python
# 문제 5
print(df)
df.reset_index(inplace=True)
print(df)
df.rename(columns={'name':'성명'}, inplace=True)
print(df)
```

           국어   영어   수학 반번호
    name                   
    둘리     90   99   90  1반
    또치     80   98   70  2반
    도우너    70   97   70  1반
    희동이    70   90   60  2반
    마이콜   100  100  100  1반
      name   국어   영어   수학 반번호
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
    4  마이콜  100  100  100  1반
        성명   국어   영어   수학 반번호
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
    4  마이콜  100  100  100  1반



```python
# 문제 6
print(df)
df1 = df.sort_values(by='국어', ascending=False)
df2 = df.sort_values(by='영어')
print(df1)
print(df2)
```

        성명   국어   영어   수학 반번호
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
    4  마이콜  100  100  100  1반
        성명   국어   영어   수학 반번호
    4  마이콜  100  100  100  1반
    0   둘리   90   99   90  1반
    1   또치   80   98   70  2반
    2  도우너   70   97   70  1반
    3  희동이   70   90   60  2반
        성명   국어   영어   수학 반번호
    3  희동이   70   90   60  2반
    2  도우너   70   97   70  1반
    1   또치   80   98   70  2반
    0   둘리   90   99   90  1반
    4  마이콜  100  100  100  1반



```python
# 문제 7
print(df)
# print(df.loc[ : , '국어':'수학'])
# print([sum(df.loc[ x , '국어':'수학']) for x in range(0, len(df))])

# df['총점'] = [sum(df.loc[ x , '국어':'수학']) for x in range(0, len(df))]
df['총점'] = df['국어'] + df['수학'] + df['영어']
df.sort_values(by='총점', ascending=False, inplace=True )
print(df)
```

           국어   영어   수학 반번호
    name                   
    둘리     90   99   90  1반
    또치     80   98   70  2반
    도우너    70   97   70  1반
    희동이    70   90   60  2반
    마이콜   100  100  100  1반
           국어   영어   수학 반번호   총점
    name                        
    마이콜   100  100  100  1반  300
    둘리     90   99   90  1반  279
    또치     80   98   70  2반  248
    도우너    70   97   70  1반  237
    희동이    70   90   60  2반  220



```python
# 문제 8
df3 = df.drop('반번호', axis=1)
print(df3)
print(df)
```

        성명   국어   영어   수학   총점
    4  마이콜  100  100  100  300
    0   둘리   90   99   90  279
    1   또치   80   98   70  248
    2  도우너   70   97   70  237
    3  희동이   70   90   60  220
        성명   국어   영어   수학 반번호   총점
    4  마이콜  100  100  100  1반  300
    0   둘리   90   99   90  1반  279
    1   또치   80   98   70  2반  248
    2  도우너   70   97   70  1반  237
    3  희동이   70   90   60  2반  220



```python
# 문제 9
df4 = df.drop(4)
print(df4)
print(df)
```

        성명  국어  영어  수학 반번호   총점
    0   둘리  90  99  90  1반  279
    1   또치  80  98  70  2반  248
    2  도우너  70  97  70  1반  237
    3  희동이  70  90  60  2반  220
        성명   국어   영어   수학 반번호   총점
    4  마이콜  100  100  100  1반  300
    0   둘리   90   99   90  1반  279
    1   또치   80   98   70  2반  248
    2  도우너   70   97   70  1반  237
    3  희동이   70   90   60  2반  220



```python
# 문제 10
data1 = {'kor':90, 'mat':80}
data2 = {'kor':90, 'eng':70}
data3 = {'kor':90, 'eng':70, 'mat':80}
series1 = pd.Series( data1 )
series2 = pd.Series( data2 )
series3 = pd.Series( data3 )
result = series1 + series2 + series3
print(result)

result2 = series1.add(series2, fill_value=0).add(series3, fill_value=0)
print(result2)
```

    eng      NaN
    kor    270.0
    mat      NaN
    dtype: float64
    eng    140.0
    kor    270.0
    mat    160.0
    dtype: float64



```python
# 문제 11
data = {
    'X1':[2.9, 2.4, 2, 2.3, 3.2],
    'X2':[9.2, 8.7, 7.2, 8.5, 9.6],
    'X3':[13.2, 11.5, 10.8, 12.3, 12.6],
    'X4':[2, 3, 4, 3, 2]
} 
df = pd.DataFrame(data, index=['Y1','Y2','Y3', 'Y4', 'Y5'])
print(df)
print('=======================================')
df.loc['Y6'] = [x for x in range(10, 50, 10)]
print(df)
df10 = df + 10
print(df10)
# print([sum(df10.loc[ 'Y' + str(x) , 'X1':'X4']) for x in range(1, len(df)+1)])
# df10['total'] = [sum(df10.loc[ 'Y' + str(x) , 'X1':'X4']) for x in range(1, len(df)+1)]
df10['total'] = df10.sum(axis=1)
print(df10)
print(df10.T)
tdf10 = df10.transpose()
print(tdf10)
```

         X1   X2    X3  X4
    Y1  2.9  9.2  13.2   2
    Y2  2.4  8.7  11.5   3
    Y3  2.0  7.2  10.8   4
    Y4  2.3  8.5  12.3   3
    Y5  3.2  9.6  12.6   2
    =======================================
          X1    X2    X3  X4
    Y1   2.9   9.2  13.2   2
    Y2   2.4   8.7  11.5   3
    Y3   2.0   7.2  10.8   4
    Y4   2.3   8.5  12.3   3
    Y5   3.2   9.6  12.6   2
    Y6  10.0  20.0  30.0  40
          X1    X2    X3  X4
    Y1  12.9  19.2  23.2  12
    Y2  12.4  18.7  21.5  13
    Y3  12.0  17.2  20.8  14
    Y4  12.3  18.5  22.3  13
    Y5  13.2  19.6  22.6  12
    Y6  20.0  30.0  40.0  50
          X1    X2    X3  X4  total
    Y1  12.9  19.2  23.2  12   67.3
    Y2  12.4  18.7  21.5  13   65.6
    Y3  12.0  17.2  20.8  14   64.0
    Y4  12.3  18.5  22.3  13   66.1
    Y5  13.2  19.6  22.6  12   67.4
    Y6  20.0  30.0  40.0  50  140.0
             Y1    Y2    Y3    Y4    Y5     Y6
    X1     12.9  12.4  12.0  12.3  13.2   20.0
    X2     19.2  18.7  17.2  18.5  19.6   30.0
    X3     23.2  21.5  20.8  22.3  22.6   40.0
    X4     12.0  13.0  14.0  13.0  12.0   50.0
    total  67.3  65.6  64.0  66.1  67.4  140.0
             Y1    Y2    Y3    Y4    Y5     Y6
    X1     12.9  12.4  12.0  12.3  13.2   20.0
    X2     19.2  18.7  17.2  18.5  19.6   30.0
    X3     23.2  21.5  20.8  22.3  22.6   40.0
    X4     12.0  13.0  14.0  13.0  12.0   50.0
    total  67.3  65.6  64.0  66.1  67.4  140.0



```python

```