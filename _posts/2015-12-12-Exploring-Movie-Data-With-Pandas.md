
# Exploring Blockbuster Movies With Pandas
Dataset retrieved from: http://www.crowdflower.com/data-for-everyoneI love movies so I thought it would be fun to analyze some movie data and show off what pandas can do. In this notebook I explore a crowdsourced dataset of Blockbuster movies from 1975 to 2014.

```python
%matplotlib inline
import os
import pandas as pd
import numpy as np
import matplotlib
from pandas import DataFrame, Series
```


```python
blockbusters = pd.read_csv('C:/Users/kphas_000/Desktop/Data Science/Website/top_ten_movies_per_year_DFE.csv')
```


```python
blockbusters.dtypes
```




    audience_freshness    float64
    poster_url             object
    rt_audience_score     float64
    rt_freshness          float64
    rt_score              float64
    2015_inflation         object
    adjusted               object
    genres                 object
    Genre_1                object
    Genre_2                object
    Genre_3                object
    imdb_rating           float64
    length                float64
    rank_in_year          float64
    rating                 object
    release_date           object
    studio                 object
    title                  object
    worldwide_gross        object
    year                  float64
    dtype: object




```python
len(blockbusters)
```




    399




```python
blockbusters.columns
```




    Index([u'audience_freshness', u'poster_url', u'rt_audience_score',
           u'rt_freshness', u'rt_score', u'2015_inflation', u'adjusted', u'genres',
           u'Genre_1', u'Genre_2', u'Genre_3', u'imdb_rating', u'length',
           u'rank_in_year', u'rating', u'release_date', u'studio', u'title',
           u'worldwide_gross', u'year'],
          dtype='object')




```python
blockbusters.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>audience_freshness</th>
      <th>poster_url</th>
      <th>rt_audience_score</th>
      <th>rt_freshness</th>
      <th>rt_score</th>
      <th>2015_inflation</th>
      <th>adjusted</th>
      <th>genres</th>
      <th>Genre_1</th>
      <th>Genre_2</th>
      <th>Genre_3</th>
      <th>imdb_rating</th>
      <th>length</th>
      <th>rank_in_year</th>
      <th>rating</th>
      <th>release_date</th>
      <th>studio</th>
      <th>title</th>
      <th>worldwide_gross</th>
      <th>year</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>92</td>
      <td>http://resizing.flixster.com/gxRJwetP1eNIrPR6x...</td>
      <td>4.3</td>
      <td>89</td>
      <td>7.5</td>
      <td>-0.26%</td>
      <td>$712,903,691.09</td>
      <td>Sci-Fi\nAdventure\nAction</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>Action</td>
      <td>7.8</td>
      <td>136</td>
      <td>7</td>
      <td>PG-13</td>
      <td>4-Apr-14</td>
      <td>Marvel Studios</td>
      <td>Captain America: The Winter Soldier</td>
      <td>$714,766,572.00</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>1</th>
      <td>89</td>
      <td>http://resizing.flixster.com/gDtbA1iPxTYEjBZeS...</td>
      <td>4.2</td>
      <td>90</td>
      <td>7.9</td>
      <td>-0.26%</td>
      <td>$706,988,165.89</td>
      <td>Sci-Fi\nDrama\nAction</td>
      <td>Sci-Fi</td>
      <td>Drama</td>
      <td>Action</td>
      <td>7.7</td>
      <td>130</td>
      <td>9</td>
      <td>PG-13</td>
      <td>11-Jul-14</td>
      <td>20th Century Fox</td>
      <td>Dawn of the Planet of the Apes</td>
      <td>$708,835,589.00</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>2</th>
      <td>93</td>
      <td>http://resizing.flixster.com/YrF_OeTQx3bXNsMLI...</td>
      <td>4.4</td>
      <td>91</td>
      <td>7.7</td>
      <td>-0.26%</td>
      <td>$772,158,880.00</td>
      <td>Sci-Fi\nAdventure\nAction</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>Action</td>
      <td>8.1</td>
      <td>121</td>
      <td>3</td>
      <td>PG-13</td>
      <td>1-Aug-14</td>
      <td>Marvel Studios</td>
      <td>Guardians of the Galaxy</td>
      <td>$774,176,600.00</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>3</th>
      <td>86</td>
      <td>http://resizing.flixster.com/l9yjA-72sZMYECeOj...</td>
      <td>4.2</td>
      <td>72</td>
      <td>7.0</td>
      <td>-0.26%</td>
      <td>$671,220,455.10</td>
      <td>Sci-Fi\nAdventure</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>NaN</td>
      <td>8.7</td>
      <td>169</td>
      <td>10</td>
      <td>PG-13</td>
      <td>7-Nov-14</td>
      <td>Paramount Pictures / Warner Bros.</td>
      <td>Interstellar</td>
      <td>$672,974,414.00</td>
      <td>2014</td>
    </tr>
    <tr>
      <th>4</th>
      <td>71</td>
      <td>http://resizing.flixster.com/YukULOFULUesVZccN...</td>
      <td>3.8</td>
      <td>49</td>
      <td>5.7</td>
      <td>-0.26%</td>
      <td>$756,677,675.77</td>
      <td>Family\nAdventure\nAction</td>
      <td>Family</td>
      <td>Adventure</td>
      <td>Action</td>
      <td>7.1</td>
      <td>97</td>
      <td>4</td>
      <td>PG</td>
      <td>30-May-14</td>
      <td>Walt Disney Pictures</td>
      <td>Maleficent</td>
      <td>$758,654,942.00</td>
      <td>2014</td>
    </tr>
  </tbody>
</table>
</div>




```python
blockbusters['year'].value_counts()
```




    2002    11
    2014    10
    1993    10
    1991    10
    1990    10
    1989    10
    1988    10
    1987    10
    1986    10
    1985    10
    1984    10
    1983    10
    1982    10
    1981    10
    1980    10
    1979    10
    1978    10
    1977    10
    1976    10
    1992    10
    1994    10
    2013    10
    2005    10
    2012    10
    2011    10
    2010    10
    2009    10
    2008    10
    2007    10
    2006    10
    2004    10
    1995    10
    2003    10
    2001    10
    2000    10
    1999    10
    1998    10
    1997    10
    1996    10
    1975     7
    Name: year, dtype: int64



Below we answer some interesting questions:

### What are the top 10 highest rated sci-fi films?


```python
blockbusters[(blockbusters.Genre_1 == 'Sci-Fi') | (blockbusters.Genre_2 == 'Sci-Fi') | (blockbusters.Genre_3 == 'Sci-Fi')][['title','imdb_rating','Genre_1','Genre_2','Genre_3']].sort_values(by='imdb_rating',ascending=False).head(10)
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>title</th>
      <th>imdb_rating</th>
      <th>Genre_1</th>
      <th>Genre_2</th>
      <th>Genre_3</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>44</th>
      <td>Inception</td>
      <td>8.8</td>
      <td>Sci-Fi</td>
      <td>Mystery</td>
      <td>Action</td>
    </tr>
    <tr>
      <th>155</th>
      <td>The Matrix</td>
      <td>8.7</td>
      <td>Sci-Fi</td>
      <td>Action</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Interstellar</td>
      <td>8.7</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>237</th>
      <td>Terminator 2: Judgment Day</td>
      <td>8.5</td>
      <td>Sci-Fi</td>
      <td>Action</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>351</th>
      <td>Alien</td>
      <td>8.5</td>
      <td>Sci-Fi</td>
      <td>Horror</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>281</th>
      <td>Aliens</td>
      <td>8.4</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>Action</td>
    </tr>
    <tr>
      <th>25</th>
      <td>The Avengers</td>
      <td>8.2</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>Action</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Guardians of the Galaxy</td>
      <td>8.1</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>Action</td>
    </tr>
    <tr>
      <th>309</th>
      <td>The Terminator</td>
      <td>8.1</td>
      <td>Sci-Fi</td>
      <td>Action</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>9</th>
      <td>X-Men: Days of Future Past</td>
      <td>8.1</td>
      <td>Sci-Fi</td>
      <td>Adventure</td>
      <td>Action</td>
    </tr>
  </tbody>
</table>
</div>



### Which years released the highest rated movies?


```python
blockbusters.groupby('year').mean()[['imdb_rating']]
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>imdb_rating</th>
    </tr>
    <tr>
      <th>year</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>1975</th>
      <td>6.642857</td>
    </tr>
    <tr>
      <th>1976</th>
      <td>6.800000</td>
    </tr>
    <tr>
      <th>1977</th>
      <td>7.260000</td>
    </tr>
    <tr>
      <th>1978</th>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>1979</th>
      <td>7.160000</td>
    </tr>
    <tr>
      <th>1980</th>
      <td>6.830000</td>
    </tr>
    <tr>
      <th>1981</th>
      <td>7.120000</td>
    </tr>
    <tr>
      <th>1982</th>
      <td>6.930000</td>
    </tr>
    <tr>
      <th>1983</th>
      <td>6.730000</td>
    </tr>
    <tr>
      <th>1984</th>
      <td>7.170000</td>
    </tr>
    <tr>
      <th>1985</th>
      <td>7.080000</td>
    </tr>
    <tr>
      <th>1986</th>
      <td>6.890000</td>
    </tr>
    <tr>
      <th>1987</th>
      <td>6.860000</td>
    </tr>
    <tr>
      <th>1988</th>
      <td>7.040000</td>
    </tr>
    <tr>
      <th>1989</th>
      <td>7.220000</td>
    </tr>
    <tr>
      <th>1990</th>
      <td>7.090000</td>
    </tr>
    <tr>
      <th>1991</th>
      <td>7.420000</td>
    </tr>
    <tr>
      <th>1992</th>
      <td>6.950000</td>
    </tr>
    <tr>
      <th>1993</th>
      <td>7.150000</td>
    </tr>
    <tr>
      <th>1994</th>
      <td>7.220000</td>
    </tr>
    <tr>
      <th>1995</th>
      <td>7.030000</td>
    </tr>
    <tr>
      <th>1996</th>
      <td>6.550000</td>
    </tr>
    <tr>
      <th>1997</th>
      <td>7.000000</td>
    </tr>
    <tr>
      <th>1998</th>
      <td>6.750000</td>
    </tr>
    <tr>
      <th>1999</th>
      <td>7.400000</td>
    </tr>
    <tr>
      <th>2000</th>
      <td>6.840000</td>
    </tr>
    <tr>
      <th>2001</th>
      <td>7.070000</td>
    </tr>
    <tr>
      <th>2002</th>
      <td>7.036364</td>
    </tr>
    <tr>
      <th>2003</th>
      <td>7.390000</td>
    </tr>
    <tr>
      <th>2004</th>
      <td>6.970000</td>
    </tr>
    <tr>
      <th>2005</th>
      <td>7.110000</td>
    </tr>
    <tr>
      <th>2006</th>
      <td>6.850000</td>
    </tr>
    <tr>
      <th>2007</th>
      <td>7.090000</td>
    </tr>
    <tr>
      <th>2008</th>
      <td>7.200000</td>
    </tr>
    <tr>
      <th>2009</th>
      <td>6.920000</td>
    </tr>
    <tr>
      <th>2010</th>
      <td>7.350000</td>
    </tr>
    <tr>
      <th>2011</th>
      <td>6.630000</td>
    </tr>
    <tr>
      <th>2012</th>
      <td>7.310000</td>
    </tr>
    <tr>
      <th>2013</th>
      <td>7.500000</td>
    </tr>
    <tr>
      <th>2014</th>
      <td>7.450000</td>
    </tr>
  </tbody>
</table>
</div>



### Which genre of movie has the highest gross?


```python

```

### Which studio has grossed the most money?


```python

```

### What movie has the highest gross and highest rating on IMDB?


```python

```

### How many movies released by each studio?


```python
blockbusters.studio.value_counts()
```




    Warner Bros.                                     45
    Paramount Pictures                               30
    Universal Pictures                               22
    20th Century Fox                                 20
    Columbia Pictures                                19
    Walt Disney Pictures                             14
    United Artists                                   13
    Columbia                                         10
    Paramount / DreamWorks                            8
    TriStar Pictures                                  8
    Fox                                               8
    Universal                                         8
    Paramount                                         7
    Disney                                            7
    New Line Cinema                                   7
    Disney / Pixar                                    7
    Warner Bros. / Legendary                          6
    Walt Disney Pictures / Pixar                      6
    Touchstone Pictures                               6
    Orion Pictures                                    5
    Marvel Studios                                    5
    Universal Studios                                 5
    Touchstone                                        5
    Warner Bros. Pictures                             5
    United Artists Pictures                           4
    DreamWorks                                        4
    Universal Pictures / Amblin Entertainment         4
    Paramount Pictures / Lucasfilm                    3
    20th Century Fox / Lucasfilm                      3
    MGM / Columbia                                    3
                                                     ..
    TriStar Pictures / Carolco                        1
    DreamWorks / Fox                                  1
    Paramount / Marvel                                1
    Universal Pictures / ITC                          1
    MGM / Universal                                   1
    Walt Disney Productions                           1
    20th Century-Fox Film Corporation                 1
    Warner Bros. / Columbia                           1
    Orion Pictures / Warner Bros.                     1
    Miramax Films / Universal Pictures                1
    Warner Bros. / New Line Cinema / MGM              1
    Paramount Pictures / Orion Pictures               1
    Paramount / Lucasfilm                             1
    20th Century Fox / Golden Harvest                 1
    TriStar Pictures / Amblin Entertainment           1
    Fox Searchlight Pictures                          1
    Warner Bros / Legendary                           1
    Paramount Pictures / PolyGram                     1
    20th Century Fox / Cinergi Pictures               1
    Lionsgate / Summit                                1
    Columbia / Marvel                                 1
    Disney / Walden Media                             1
    Columbia Pictures / Castle Rock Entertainment     1
    National Air and Space Museum                     1
    American International Pictures                   1
    United Film Distribution Company                  1
    DreamWorks / Universal                            1
    Columbia Pictures / Rastar                        1
    New Line                                          1
    Summit Entertainment                              1
    Name: studio, dtype: int64



### How many movies rated higher than 7 by studio?


```python
blockbusters[]
```
