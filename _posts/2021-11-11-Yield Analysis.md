---
layout: post
title: Yield Analysis
subtitle: 2021 Yield Analysis 
comments: true
---
**The notebook for this analysis can be found here:**     
https://raw.githubusercontent.com/gabbymyers/516X-Project/master/_posts/Yield%20Analysis.ipynb      
or  "_posts/Yield Analysis.ipynb" within the directory


The 2021 yield data from all of the treatments is housed in an excel file called "2021 Yield". 

**Importing the data**
~~~
yield_data = pd.read_excel("2021 Yield.xlsx")
~~~

**Visualizing the data**

~~~
ax = sns.boxplot(x = "Treatment", y = "Yield (avg; bu/ac)", data = yield_data)
plt.savefig('all_yield_box.png')
~~~
![box plot of yield by treatment](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/_posts/all_yield_box.png)

I realized it doesn't work to have all the yields on the same plots because some treatments are soybeans and others are corn, so yields are very different.

**Subsetting the data**
~~~
corn_only = yield_data[yield_data['Treatment'].str.contains('1C|2C|3.1|3.2|4.1|4.2|5C|6C')]
ax = sns.boxplot(x = "Treatment", y = "Yield (avg; bu/ac)", data = corn_only, hue = 'Short Trt Description', dodge = False)
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
plt.savefig('corn_yield_box.jpg', bbox_inches='tight')
~~~
![box plot of yield by treatment, corn only](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/_posts/corn_yield_box.jpg)


**Full Notebook**
[Link to Yield Analysis Jupyter Notebook](https://nbviewer.org/github/gabbymyers/516X-Project/blob/master/_posts/Yield%20Analysis.ipynb)
