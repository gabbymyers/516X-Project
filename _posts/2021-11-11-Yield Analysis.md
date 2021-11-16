---
layout: post
title: Yield Analysis
subtitle: 2021 Yield Analysis 
comments: true
---
Link to Jupyter Notebook at the end of this post.   

The 2021 yield data from all of the treatments is housed in an excel file called "2021 Yield". 

### Importing the data
~~~
yield_data = pd.read_excel("2021 Yield.xlsx")
~~~

### Visualizing the data

**Box Plots**

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


**Legend Explanation** 

|Code|Explanation|
|:---|:---:|
|CS, SUAN|Corn/Soy Rotation with Spring UAN|
|CC|Continuous Corn|
|CC + PGC |Continuous Corn with Perennial Groundcover|
|CC + 30ISC |Continuous Corn with 30 inch rows and Interseeded Cover Crop|
|CS, SM|Corn/Soy Rotation with Spring Manure|
|CS + R|Corn/Soy Rotation with Cereal Rye Cover Crop|
|CC + 60ISC |Continuous Corn with 60 inch rows and Interseeded Cover Crop|
|CS, FM|Corn/Soy Rotation with Fall Manure|

**Soy**

~~~
ax = sns.boxplot(x = "Treatment", y = "Yield (avg; bu/ac)", data = soy_only, hue = 'Short Trt Description', dodge = False)
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
plt.savefig('soy_yield_box.jpg', bbox_inches='tight')
~~~

![Box plot of soy yield by treatment](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/_posts/soy_yield_box.jpg)


**Bar Plots**

**Corn Yield by Treatment**

 ~~~
corn_means = pd.DataFrame(corn_only.groupby('Treatment')['Yield'].describe()['mean'])
corn_means = corn_means.reset_index()

ax = sns.barplot(x = 'Treatment', y = 'mean', data = corn_means)
ax.set_title('2021 Yield of Corn Treatments')
ax.set(xlabel='Treatment', ylabel='Mean Yield (bu/ac)')

#for annotating 
for p in ax.patches:
             ax.annotate("%.0f" % p.get_height(), (p.get_x() + p.get_width() / 2., p.get_height()),
                 ha='center', va='center', fontsize=10, color='black', xytext=(0, 5),
                 textcoords='offset points')
        
plt.savefig('corn_bar.jpg', bbox_inches='tight')
~~~

![Bar plot of mean corn yields](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/corn_bar.jpg)

**Corn Yield by block**
~~~
corn_block_means = pd.DataFrame(corn_only.groupby('Block')['Yield'].describe()['mean'])
corn_block_means = corn_block_means.reset_index()
ax = sns.barplot(x = 'Block', y = 'mean', data = corn_block_means)
ax.set_title('2021 Corn Yield of Blocks')
ax.set(xlabel='Block', ylabel='Mean Yield (bu/ac)')

#for annotating 
for p in ax.patches:
             ax.annotate("%.1f" % p.get_height(), (p.get_x() + p.get_width() / 2., p.get_height()),
                 ha='center', va='center', fontsize=10, color='black', xytext=(0, 5),
                 textcoords='offset points')
        
plt.savefig('corn_block_bar.jpg', bbox_inches='tight')
~~~

![Bar plot of mean corn yields blocks](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/corn_block_bar.jpg)

**Soy Yield by Treatment**

~~~
soy_means = pd.DataFrame(soy_only.groupby('Treatment')['Yield'].describe()['mean'])
soy_means = soy_means.reset_index()

ax = sns.barplot(x = 'Treatment', y = 'mean', data = soy_means)
ax.set_title('2021 Yield of Soy Treatments')
ax.set(xlabel='Treatment', ylabel='Mean Yield (bu/ac)')

#for annotating 
for p in ax.patches:
             ax.annotate("%.0f" % p.get_height(), (p.get_x() + p.get_width() / 2., p.get_height()),
                 ha='center', va='center', fontsize=10, color='black', xytext=(0, 5),
                 textcoords='offset points')
        
plt.savefig('soy_bar.jpg', bbox_inches='tight')
~~~

![Bar plot of mean soy yields by trt](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/soy_bar.jpg)


**Soy Yield by Block**

~~~
soy_block_means = pd.DataFrame(soy_only.groupby('Block')['Yield'].describe()['mean'])
soy_block_means = soy_block_means.reset_index()

ax = sns.barplot(x = 'Block', y = 'mean', data = soy_block_means)
ax.set_title('2021 Soy Yield of Blocks')
ax.set(xlabel='Block', ylabel='Mean Yield (bu/ac)')

#for annotating 
for p in ax.patches:
             ax.annotate("%.1f" % p.get_height(), (p.get_x() + p.get_width() / 2., p.get_height()),
                 ha='center', va='center', fontsize=10, color='black', xytext=(0, 5),
                 textcoords='offset points')
        
plt.savefig('soy_block_bar.jpg', bbox_inches='tight')
~~~

![Bar plot of mean soy yields by block](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/soy_block_bar.jpg)



## Corn ANOVA 

I first need to test that the assumptions for ANOVA are satisfied.

**Treatment Summary**

![Corn Treatment Summary Stats](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/Corn_Stats.JPG)

**Checking for Normality**

~~~
plt.hist(x='Yield', bins = 'auto', data = corn_only)
plt.title("Corn Yields 2021")
plt.xlabel('Yield (bu/ac)')
plt.ylabel('Frequency')
plt.savefig('Corn Histogram.jpg', bbox_inches='tight')
~~~
![Corn Yield Histogram](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/Corn%20Histogram.jpg)

Not looking very normally distributed. A histogram might not be the best way to see it. I'll make a kernel density estimate plot ([Link to Doumentation](https://seaborn.pydata.org/generated/seaborn.kdeplot.html)) to look at it another way. 

~~~
sns.kdeplot(data=corn_only, x="Yield")
plt.title('Corn Yield Kernel Density Plot')
plt.savefig('corn_yield_kde.jpg', bbox_inches='tight')
~~~

![Corn Yield KDE](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/corn_yield_kde.jpg)

Clearly we have some outliers. 

~~~
stats.probplot(corn_only['Yield'], dist="norm", plot=plt)
plt.show()
plt.savefig('corn_yield_probplot', bbox_inches='tight')
~~~
![Corn Yield Prob Plot](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/corn_yield_probplot.JPG)

Certainly not the most normally distributed, but I'm going to move along. 


**Homogeneity of Variances**    

**Null**: Variances are the same across treatments       
**Alternative**: Variances are not the same across treatments  

Following this tutorial: [Barletts and Levenes Tests](https://www.marsja.se/levenes-bartletts-test-of-equality-homogeneity-of-variance-in-python/)          

**Bartlett’s Test of Homogeneity of Variances**      
~~~
from scipy.stats import bartlett

# subsetting the data:
trt1 = corn_only.query('Treatment == "1C"')['Yield']
trt2 = corn_only.query('Treatment == "2C"')['Yield']
trt31 = corn_only.query('Treatment == "3.1"')['Yield']
trt32 = corn_only.query('Treatment == "3.2"')['Yield']
trt41 = corn_only.query('Treatment == "4.1"')['Yield']
trt42 = corn_only.query('Treatment == "4.2"')['Yield']
trt5 = corn_only.query('Treatment == "5C"')['Yield']
trt6 = corn_only.query('Treatment == "6C"')['Yield']

# Bartlett's test in Python with SciPy:
stat, p = bartlett(trt1, trt2, trt31, trt32, trt41, trt42, trt5, trt6)

# Get the results:
print(stat, p)

~~~
T = 8.236102945085667     
p = 0.3122358533181093     

The p-value is high, so you can assume the variances are the same.     

**Levene’s Test of Equality of Variances**       

This is preferred for non-normal data.      

~~~
from scipy.stats import levene

# Create three arrays for each sample:
trt1 = corn_only.query('Treatment == "1C"')['Yield']
trt2 = corn_only.query('Treatment == "2C"')['Yield']
trt31 = corn_only.query('Treatment == "3.1"')['Yield']
trt32 = corn_only.query('Treatment == "3.2"')['Yield']
trt41 = corn_only.query('Treatment == "4.1"')['Yield']
trt42 = corn_only.query('Treatment == "4.2"')['Yield']
trt5 = corn_only.query('Treatment == "5C"')['Yield']
trt6 = corn_only.query('Treatment == "6C"')['Yield']

# Levene's Test in Python with Scipy:
stat, p = levene(trt1, trt2, trt31, trt32, trt41, trt42, trt5, trt6)

print(stat, p)

~~~
W = 0.6584854455470804     
p = 0.7032800804487055    

p-value is high, so you can assume the variances are the same.      


**ANOVA**

Checking to see if treatment or block had a significant effect on corn yields in 2021. 

~~~
corn_only = corn_only.rename(columns={"Simp. Treatment": "simple_treatment"})

model = ols('Yield ~ C(Block) + C(simple_treatment)', data = corn_only).fit()

aov_table = sm.stats.anova_lm(model)

print(aov_table)
~~~
    

![Corn Yield ANOVA Table](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/corn_yield_anovatable.JPG)

This matches what I get using SAS:    

~~~
proc glm data = A;
class Block Trt;
model Yield = Block Trt;
random Block/test ;
run;
~~~

![Corn Yield ANOVA Table SAS](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/sdfgfgd.PNG)

It looks like treatment definitely had an effect on corn yields in 2021 and block did not.    

**Least Significant Difference in SAS**    

To see which treatments' means are different from each other.    

~~~
proc glm data = A;
class Block Trt;
model Yield = Block Trt;
means Trt/lsd;
run;
~~~

![Corn Yield LSD](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/corn_yield_lsd.JPG)

* Treatment 4.2 is different from all other treatments, which is expected because of an error in the seeding chart for this treatment leading to a lower plant density than desired. 
* The PGC treatment (4.1) was significantly different than the control (3.1), with PGC having a 12.75 bu/ac decrease from the control.
* The corn/soy rotations with manure applied and no cover crops yielded the best (2C and 6C). 

## Soy ANOVA

Following the same steps as above.

<p align="center">
  <img alt="Soy Histogram" src="https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/Soy%20Histogram.jpg" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Soy KDE" src="https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/soy_yield_kde.jpg" width="45%">
</p>

![Soy Prob Plot](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/soy_yield_probplot.JPG)

~~~

model = ols('Yield ~ C(Block) + C(simple_treatment)', data = soy_only).fit()

aov_table = sm.stats.anova_lm(model)

print(aov_table)

~~~

![Soy ANOVA Table](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/soy_anova_table.JPG)


**In SAS**

![Soy Anova SAS](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/soy_sas_anova.JPG)

![Soy LSD](https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/soy_lsd.JPG)

* Again, the treatments with no cover crops yielded the best (6S and 2S). 
* The cereal rye treatment saw an approximately 2 bu/ac decrease in soy yield

**Full Notebook**     
[nb viewer](https://nbviewer.org/github/gabbymyers/516X-Project/blob/master/_data/Yield%20Analysis.ipynb)    

[In Gitub](https://github.com/gabbymyers/516X-Project/blob/master/_data/Yield%20Analysis.ipynb)       
