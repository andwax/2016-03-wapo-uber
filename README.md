# 2016-03-wapo-uber

#[WaPo Title](www.wapo...) <- insert article URL
By [Jennifer A Stark](https://github.com/JAStark) and [Nick Diakopoulos](http://www.nickdiakopoulos.com)

# Supporting open source and reproducibility
This is a repository containing data analysis and visualization code for the
Washington Post article [" "](www.wapo...). <- insert article URL

Data were collected using the Uber API with config.config and gatherUberData.py -
based on scripts of the same name from our [uberpy](https://github.com/comp-journalism/uberpy)
project.

`config.config` was modified to collect every 3 minutes, provided a list of 276
locations across DC, and provided a list of Uber API keys.

`gatherUberData.py` was modified to save data with the DC local datetime.

If you have cloned this repo and downloaded the raw [data](https://drive.google.com/folderview?id=0B-mutxqHY34rblhORk9raWxQQjQ&usp=sharing),
you can follow the [notebook](https://github.com/comp-journalism/2016-03-wapo-uber/blob/master/UberSurgePricing_OSC.ipynb)

#Requirements
If you use the Anaconda distribution, you're all set.

Python 3 (does not work in python 2)
ipython notebook / Jupyter
pandas
numpy
matplotlib.pyplot
scipy.stats  (for `pearsonr`)
seaborn
statsmodels.formula.api
statsmodels.graphics.api (for `abline_plot`)

#Funding
This project was funded by a grant from the Tow Foundation to study computational
and data journalism with an emphasis on algorithmic accountability, narrative data
visualization, and social computing in the news.

#Feedback
Email Jennifer A Stark at starkja@umd.edu
