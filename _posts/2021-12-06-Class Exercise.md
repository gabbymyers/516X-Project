---
layout: post
title: Class Exercise
subtitle: Linear regression exercise
thumbnail-img: /assets/img/download.png
comments: true
---

We will use a couple of the variables we measured, soil moisture content and aggregate stability to see if there is any relationship between them. The data is located [here](https://github.com/gabbymyers/516X-Project/blob/master/_data/Class%20Exercise%20Data.xlsx).

Completed notebook: [nb viewer](https://nbviewer.org/github/gabbymyers/516X-Project/blob/master/_data/ClassExercise_Completed.ipynb)     
Download the not completed notebook here:      

Soil moisture content refers to the moisture in the soil. We determine this by collecting a sample from each of our 36 plots at the Northeast Iowa Research Farm. The sample is taken back to the lab and the moisture content is determined by weighing the soil before and after drying.

Aggregate stability is a measure of how the soil aggregates (groups of soil particles) fall apart when wet. We use the SLAKES app to get the aggregate stability numbers for our samples. The SLAKES app take continuous images of soil aggregates as they are submerged in water and returns aggregate stability values on a range of 0-14. The lower the number, the more stable the aggregates are. Stable aggregates indicate the soil likely has better water infiltration, reducing the risk of runoff. Cover crops are known to increase aggreagate stability, so I would expect our cover crop treatments to have lower aggregate stability values from the SLAKES app.

We have different 12 different treatments in triplicate on our 36 plots. I have these listed below.    

* 1C: Corn (on corn/soy rotation) with spring UAN    
* 1S: Soy (on corn/soy rotation) with spring UAN     
* 2C: Corn (on corn/soy rotation) with spring manure     
* 2S: Soy (on corn/soy rotation) with spring manure     
* 3.1: Continuous Corn     
* 3.2: Continuous Corn + Interseeded Cover crop (30 inch row)    
* 4.1: Continuous Corn + Perennial Groundcover    
* 4.2: Continuous Corn + Interseeded Cover crop (60 inch row)     
* 5C: Corn (on corn/soy rotation) + cereal rye     
* 5S: Soy (on corn/soy rotation) + cereal rye     
* 6C: Corn (on corn/soy rotation) + fall manure     
* 6S: Soy (on corn/soy rotation) + fall manure    

### Research Question    
Is there any relationship between aggregate stability and moisture content?
