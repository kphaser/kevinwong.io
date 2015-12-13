---
layout: post
title: Movie data with Pandas
tags:
- python
- pandas
- movies
---

I love movies so I thought it would be fun to analyze some movie data and show off what pandas can do. In this post I explore a crowdsourced dataset of Blockbuster movies from 1975 to 2014.

<pre><code>import os
import pandas as pd
import numpy as np
import matplotlib
from pandas import DataFrame, Series

blockbusters = pd.read_csv('top_ten_movies_per_year_DFE.csv')
</pre></code>


Dataset retrieved from: http://www.crowdflower.com/data-for-everyone