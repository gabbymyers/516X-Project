---
layout: post
title: Yield Analysis
subtitle: 2021 Yield Analysis 
comments: true
---

The 2021 yield data from all of the treatments is housed in an excel file called "2021 Yield". 

**Importing the data**
~~~
yield_data = pd.read_excel("2021 Yield.xlsx")
yield_data.head()
~~~

**Visualizing the data**

~~~
ax = sns.boxplot(x = "Treatment", y = "Yield (avg; bu/ac)", data = yield_data)
plt.savefig('all_yield_box.png')
~~~
![box plot of yield by treatment hello](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/_posts/all_yield_box.png)

I realized it doesn't work to have all the yields on the same plots because some treatments are soybeans and others are corn, so yields are very different.

**Subsetting the data**
~~~
corn_only = yield_data[yield_data['Treatment'].str.contains('1C|2C|3.1|3.2|4.1|4.2|5C|6C')]
corn_only.head()
~~~

