---
layout: post
title: Soil Moisture Content Analysis
subtitle: 2021 Soil Moisture 
comments: true
---

Soil samples were collected roughly every 2 weeks to get 12 soil samples.

### Data Visualizations

<p align="center">
  <img alt="Treatment Bar" src="https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/MC_bar_trt.jpg" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Date Bar" src="https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/MC_bar_date.jpg" width="30%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Block Bar" src="https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/MC_bar_block.jpg" width="30%">
</p>

**Sample code**

~~~
trt_means = pd.DataFrame(soil_moisture.groupby('Treatment')['MC'].describe()['mean'])
trt_means = trt_means.reset_index()
trt_means['mean'] = 100 * trt_means['mean']

ax = sns.barplot(x = 'Treatment', y = 'mean', data = trt_means)
ax.set_title('2021 Mean Soil Moisture Content')
ax.set(xlabel='Treatment', ylabel='Mean MC %')

#for annotating 
for p in ax.patches:
             ax.annotate("%.1f" % p.get_height(), (p.get_x() + p.get_width() / 2., p.get_height()),
                 ha='center', va='center', fontsize=10, color='black', xytext=(0, 5),
                 textcoords='offset points')
        
plt.savefig('MC_bar_trt.jpg', bbox_inches='tight')
~~~

<p align="center">
  <img alt="Treatment Box" src="https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/trt_mc_box.jpg" width="45%">
&nbsp; &nbsp; &nbsp; &nbsp;
  <img alt="Date Box" src="https://raw.githubusercontent.com/gabbymyers/516X-Project/master/assets/img/date_bc_box.jpg" width="45%">
</p>

**Code**

~~~
ax = sns.boxplot(x = "Treatment", y = "MC", data = soil_moisture, hue = 'Short Trt Description', dodge = False)
plt.legend(bbox_to_anchor=(1.05, 1), loc=2, borderaxespad=0.)
plt.savefig('trt_mc_box.jpg', bbox_inches='tight')

ax = sns.boxplot(x = "Date", y = "MC", data = soil_moisture)
plt.savefig('date_bc_box.jpg', bbox_inches='tight')
~~~

I wrote a function to make box plots for each date, but won't incldude them on this post. You can see them in the jupyter notebook here [Link](https://github.com/gabbymyers/516X-Project/blob/master/_data/Soil%20Moisture%20Analysis.ipynb)

~~~
def filterbydate (sampledate):
    sample_date_df = pd.DataFrame(soil_moisture[soil_moisture.Date == sampledate])
    return sample_date_df

sample_date = 1 
while sample_date <= max(soil_moisture.Date):
    date_df = filterbydate(sample_date)
    date_df.boxplot('MC', by = 'Treatment')
    plt.title('Moisture Content by Trt on Date {}'.format(sample_date))
    plt.suptitle("")
    plt.ylabel("Moisture Content, DB")
    sample_date = sample_date + 1
~~~

