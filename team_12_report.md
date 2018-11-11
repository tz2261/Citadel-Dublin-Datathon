<div tabindex="-1" id="notebook" class="border-box-sizing">

<div class="container" id="notebook-container">

<form action="javascript:code_toggle()"><input type="submit" id="toggleButton" value="Show Code"></form>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

# Citadel Datathon Dublin Team 12[¶](#Citadel-Datathon-Dublin-Team-12)

## The role of inspections in health and saftey of food establishments in New York[¶](#The-role-of-inspections-in-health-and-saftey-of-food-establishments-in-New-York)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

* * *

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## 1\. Executive Summary[¶](#1.-Executive-Summary)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### Question[¶](#Question)

All over the US, State and Federal governments are doubling down on efforts to improve public health. Despite advances in technology, public health standards are still below desired levels. In their [‘Prevention Agenda 2013-2018’](https://www.health.ny.gov/prevention/prevention_agenda/2013-2017/), the New York State Health Department has listed promoting healthy and safe environments as a key focus area; ensuring good food safety practices is one action point under this heading. This report examines the following question:

**How does locality and inspection history influence the quality of food establishments in New York state and how does this relate to the quality of New York resident's lives?**

We investigate the locality and inspection history data in conjuntion with socio-economic and health indicators acting as measures of quality of life.

### The Findings[¶](#The-Findings)

Our exploratory research suggests that the number of average food violations per inspection of a food establishment may have increased over time, across the state. We have found that an increase in number of inspections reduces the average critical violation count, but that these inspections are typically more frequent in areas with higher household earnings. This may suggest that efforts to increase inspections are effective and should be replicated in counties with lower household earnings to achieve parity of food establishment quality across the earnings scale.

### The Model[¶](#The-Model)

We create a model that predicts whether an establishment will incur a critical violation given the average previous critical violations per inspection and the time passes since the last inspection. It achieves reasonable performance with an a 0.68 AUC ROC. We are able to insightfully correate both features with the value we try to predict.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## 2 Data Exploration[¶](#2-Data-Exploration)

### 2.1 Data transformation:[¶](#2.1-Data-transformation:)

### Criticality of a violation[¶](#Criticality-of-a-violation)

We decided to focus on violations that were deemed 'critical' (see grading system [here](https://www.ehagroup.com/food-safety/new-york-abc-restaurant-grading/)), as they related to food temperature, sources, protection, facility design and personal hygiene of staff. These were factors we decided were more likely to impact the health of New York State citizens.

### The concept of an inspection[¶](#The-concept-of-an-inspection)

Each row in the primary dataset was a single type of violation, meaning for a single inspection, multiple rows could occur for different violation types. Since we decided not to focus on the violation types, we transformed the data to get a single row per inspection, which summed the total number of violations over all types.

This gives **406616** inspections.

### 2.2 Analysis:[¶](#2.2-Analysis:)

The following questions show our exploratory analysis into how frequency of inspections, number of violations, health and socio-economic factors of the community intertwine.

#### How does number of inspections impact the average violation count per inspection?[¶](#How-does-number-of-inspections-impact-the-average-violation-count-per-inspection?)

We explored how the number of inspections impact the average violation count per inspection with the following scatterplot.

![](https://image.ibb.co/iPkKTV/average-violations-per-inspection-over-num-inspections.png)

This shows that for more frequently inspected establishments, the average incidence of violations decreases. This is likely in part due to re-inspections to establish previous critical violations are resolved.

#### How does the earnings of a county impact the frequency of inspections?[¶](#How-does-the-earnings-of-a-county-impact-the-frequency-of-inspections?)

We decided to investigate if certain counties in New York State received a higher frequency of inspections per restaurant. The following plot shows there is a correlation between the two, with a $R^2$ value of 0.59\. This shows there is a potential bias towards inspecting establishments in more affluent neighbourhoods. Since we have seen that establishments with more inspections typically exhibit lower number of critical violations, socio-economic factors can be a factor in the quality of food establishments.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [1]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="o">%%</span><span class="k">HTML</span>
<div>
    <a href="https://plot.ly/~karthikuwc/65/?share_key=49wkewBX1wZ60beLpkkWz2" target="_blank" title="Plot 65" style="display: block; text-align: center;"><img src="https://plot.ly/~karthikuwc/65.png?share_key=49wkewBX1wZ60beLpkkWz2" alt="Plot 65" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="karthikuwc:65" sharekey-plotly="49wkewBX1wZ60beLpkkWz2" src="https://plot.ly/embed.js" async></script>
</div>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_html rendered_html output_subarea ">

<div>[![Plot 65](https://plot.ly/~karthikuwc/65.png?share_key=49wkewBX1wZ60beLpkkWz2)](https://plot.ly/~karthikuwc/65/?share_key=49wkewBX1wZ60beLpkkWz2 "Plot 65") </div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

#### How number and effectives of inspections changed over time?[¶](#How-number-and-effectives-of-inspections-changed-over-time?)

With the next three plots, we attempt to explore how number of inspections and their effectiveness have changed over time.

![](https://image.ibb.co/mSjchq/explore-over-time.png)

The first graph shows that the number of inspections have generally increased over time. Despite this, the number of average inspections per establishment (the second graph) has remained relatively stable. This shows the health department is currently keeping up with vetting the number of food establishments approximately once a year as they increase.

The third graph shows the average number of violations over time, which increase over time. Considering the Prevention Agenda commenced in 2013, we might have expected a decline in average violation count between 2013 and 2018\. This suggests that the current strategies for improving food and health safety in the state of New York are not working.

#### What areas typically have low/high numbers of average violation counts per inspection?[¶](#What-areas-typically-have-low/high-numbers-of-average-violation-counts-per-inspection?)

The following visualisation show the average critical violation count per county over time. We identify particular counties of concern that repeatedly have high average violation counts as Warren and Saratoga. These are areas the State of New York could focus on improving food and health safety.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [2]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="o">%%</span><span class="k">HTML</span>
<div class='tableauPlaceholder' id='viz1541843239667' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;9M&#47;9MHDTQ5QC&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='path' value='shared&#47;9MHDTQ5QC' /> <param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;9M&#47;9MHDTQ5QC&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1541843239667');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_html rendered_html output_subarea ">

<div class="tableauPlaceholder" id="viz1541843239667" style="position: relative">

<noscript>[![ ](https://public.tableau.com/static/images/9M/9MHDTQ5QC/1_rss.png)](#)</noscript>

<object class="tableauViz" style="display:none;"><param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F"> <param name="embed_code_version" value="3"> <param name="path" value="shared/9MHDTQ5QC"> <param name="toolbar" value="yes"><param name="static_image" value="https://public.tableau.com/static/images/9M/9MHDTQ5QC/1.png"> <param name="animate_transition" value="yes"><param name="display_static_image" value="yes"><param name="display_spinner" value="yes"><param name="display_overlay" value="yes"><param name="display_count" value="yes"><param name="filter" value="publish=yes"></object></div>

<script type="text/javascript">var divElement = document.getElementById('viz1541843239667'); var vizElement = divElement.getElementsByTagName('object')[0]; vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px'; var scriptElement = document.createElement('script'); scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js'; vizElement.parentNode.insertBefore(scriptElement, vizElement);</script></div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

#### How does average violation count impact on Salmonella incidence rate?[¶](#How-does-average-violation-count-impact-on-Salmonella-incidence-rate?)

We attempted to find health indicators in the community health data set that might identify areas of poor food health and safety of eating establishments. We found a health indicator for 'Salmonella incidence rate per 100,000 people' between 2012 and 2014\. We also found an indicator for gastroenteritis, a subset of which called bacterial gastroenteritis is commonly caused by "food poisoning". Unfortunately, this data was for children under the age of 4, an unlikely target audience of food establishments.

The following visualisation shows the relative rates of Salmonella incidence across the counties of the State of New York.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [3]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="o">%%</span><span class="k">HTML</span>
<div class='tableauPlaceholder' id='viz1541856398129' style='position: relative'><noscript><a href='#'><img alt=' ' src='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;sa&#47;salmonella&#47;Sheet22&#47;1_rss.png' style='border: none' /></a></noscript><object class='tableauViz'  style='display:none;'><param name='host_url' value='https%3A%2F%2Fpublic.tableau.com%2F' /> <param name='embed_code_version' value='3' /> <param name='site_root' value='' /><param name='name' value='salmonella&#47;Sheet22' /><param name='tabs' value='no' /><param name='toolbar' value='yes' /><param name='static_image' value='https:&#47;&#47;public.tableau.com&#47;static&#47;images&#47;sa&#47;salmonella&#47;Sheet22&#47;1.png' /> <param name='animate_transition' value='yes' /><param name='display_static_image' value='yes' /><param name='display_spinner' value='yes' /><param name='display_overlay' value='yes' /><param name='display_count' value='yes' /><param name='filter' value='publish=yes' /></object></div>                <script type='text/javascript'>                    var divElement = document.getElementById('viz1541856398129');                    var vizElement = divElement.getElementsByTagName('object')[0];                    vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px';                    var scriptElement = document.createElement('script');                    scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js';                    vizElement.parentNode.insertBefore(scriptElement, vizElement);                </script>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_html rendered_html output_subarea ">

<div class="tableauPlaceholder" id="viz1541856398129" style="position: relative">

<noscript>[![ ](https://public.tableau.com/static/images/sa/salmonella/Sheet22/1_rss.png)](#)</noscript>

<object class="tableauViz" style="display:none;"><param name="host_url" value="https%3A%2F%2Fpublic.tableau.com%2F"> <param name="embed_code_version" value="3"> <param name="site_root" value=""><param name="name" value="salmonella/Sheet22"><param name="tabs" value="no"><param name="toolbar" value="yes"><param name="static_image" value="https://public.tableau.com/static/images/sa/salmonella/Sheet22/1.png"> <param name="animate_transition" value="yes"><param name="display_static_image" value="yes"><param name="display_spinner" value="yes"><param name="display_overlay" value="yes"><param name="display_count" value="yes"><param name="filter" value="publish=yes"></object></div>

<script type="text/javascript">var divElement = document.getElementById('viz1541856398129'); var vizElement = divElement.getElementsByTagName('object')[0]; vizElement.style.width='100%';vizElement.style.height=(divElement.offsetWidth*0.75)+'px'; var scriptElement = document.createElement('script'); scriptElement.src = 'https://public.tableau.com/javascripts/api/viz_v1.js'; vizElement.parentNode.insertBefore(scriptElement, vizElement);</script></div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

The following plot shows the incidence rate of Salmonella incidence rate per 100,000 people and the average violation count per county between 2012 and 2014\. It has no significant correlation with an $R^2$ value of 0.038\. The reason for this could explained in a variety of ways including citizens giving themselves Salmonella at a higher rate than food establishments. We currently do not have the data to separate these two different events.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [4]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span><span class="o">%%</span><span class="k">HTML</span>
<div>
    <a href="https://plot.ly/~karthikuwc/63/?share_key=zZYMRLMcSMF9sTKemsp47c" target="_blank" title="Plot 63" style="display: block; text-align: center;"><img src="https://plot.ly/~karthikuwc/63.png?share_key=zZYMRLMcSMF9sTKemsp47c" alt="Plot 63" style="max-width: 100%;width: 600px;"  width="600" onerror="this.onerror=null;this.src='https://plot.ly/404.png';" /></a>
    <script data-plotly="karthikuwc:63" sharekey-plotly="zZYMRLMcSMF9sTKemsp47c" src="https://plot.ly/embed.js" async></script>
</div>
</pre>

</div>

</div>

</div>

</div>

<div class="output_wrapper">

<div class="output">

<div class="output_area">

<div class="output_html rendered_html output_subarea ">

<div>[![Plot 63](https://plot.ly/~karthikuwc/63.png?share_key=zZYMRLMcSMF9sTKemsp47c)](https://plot.ly/~karthikuwc/63/?share_key=zZYMRLMcSMF9sTKemsp47c "Plot 63") </div>

</div>

</div>

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

* * *

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## 3\. Technical Modeling and Prediction[¶](#3.-Technical-Modeling-and-Prediction)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### 3.1 Modeling[¶](#3.1-Modeling)

We are interested in finding the relationship of variables that could negatively influence outcome of the latest inspection.

Specifically, we are interested in the outcome of the latest inspection solely as binary value: 'any critical violations' and 'no critical violations'. We want to test the influence of prior average violations per inspection (i.e. level of previous consideration of food safety guidelines) and the time between just the prior and the last inspection (which could cause negligence over time).

Features:

*   (num: #) avg_violations
*   (num: # days) days_since_last_inspection

Target Variable:

*   (bin) any_violations_in_latest_inspection

The binary value 'any/no critical violations' will be modeled as a Bernoulli distribution. As such, we find the effects of our features by performing logistical regression.

Because we base our model partly on histroric averages, we limit out training set to only restaurants, that have $N > threshold$ inspections, as considering lower numbers of inspections do not give representative averages. Below, the reduction in dataset size depending on $threshold$

![alt text](https://image.ibb.co/b1iZTV/restaurant-inspection-frequency.png)

Through visualtion and exploration of deviations from the averages we calculated, we chose $threshold=5$ to strike a balance between representative data and size of the reduced dataset.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### 3.2 Model Evaluation[¶](#3.2-Model-Evaluation)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

The binary classification model was evaluated using the area under the reciever operating characteristic curve metric. The ROC-AUC score evaluates the performance of the model on each class individually, and is useful in the event of class-imbalance. It is a plot of false-positive rate (FPR) agaist true positive rate over all discrimination thresholds. The area under the ROC curve is an indication of how well the model performs, as it represents the probabilitiy that the model classifies data points correctly.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### 3.3 Model Training[¶](#3.3-Model-Training)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

#### 3.3.1 Data Preprocessing[¶](#3.3.1-Data-Preprocessing)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

Initially, the classes were imbalanced with a negative:positive class ratio of ~ 6:1\. In the case that the class imbalance is left undealt with, and accuracy is used as a performance metric, the classification will be biased towards the majority class, resulting in a higher misclassification rate for the minority class instances.

When preprocessing, the decision was made to downsample the majority, such that the number of instances of each class become equal. Although this significantly reduces the size of the training data, it is an important step in ensuring decent model performace.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

#### 3.3.2 Cross-Validation[¶](#3.3.2-Cross-Validation)

We validate our model using 10-fold cross-validation, to ensure that we are not overfitting, and to evaluate the model's performance. This also allows us to perform hyperparameter tuning. The overall performance of our model is presented in terms of the mean and standard deviation of the ROC AUC scores of each cross-validation fold.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

#### 3.3.3 Data Leak[¶](#3.3.3-Data-Leak)

Data leak occurs when information from the training set leaks into the validation set. Although the model will perform well on the validation set, when deployed into the real-world, it is likely to perform poorly. To this end, we deal with this problem by performing data preprocessing within the cross-validation folds. Within each fold, a new sklearn RobustScaler object is created, and the training data of is fitted and transformed using this scaler. This is followed by a transformation of the test data in that fold. The result of this is that the scaler is fitted to only the training data of that fold, and is used to transform the test data of that fold.

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

### 3.4 Results[¶](#3.4-Results)

The ROC score average for each fold was ~0.6772 with a standard deviation of ~0.0223.

We use the coefficients computed by the logistic regression to calculate the odds ratios for an increase in any particular feature $i$:

$oddsratio = e^{\beta_i\Delta}$

The resulting odds ratios are:

*   avg_violations ~ 1.3033
*   days_since_last_inspection ~ 1.0013

### 3.5 Interpretation[¶](#3.5-Interpretation)

Our model achieves reasonable performance.

This means:

1.  increasing the average of previous critical violations per inspection by 1 (other variables fixed) increases the odds of the latest inspection finding a critical violation by ~30.33%

2.  any month passing without inspection, inscreases the odds of the latest inspection finding a critical violation by ~4.3% (half a year translates to a ~ 27.5% increase in odds)

</div>

</div>

</div>

<div class="cell border-box-sizing text_cell rendered">

<div class="inner_cell">

<div class="text_cell_render border-box-sizing rendered_html">

## 4 Conclusions, insights and future research[¶](#4-Conclusions,-insights-and-future-research)

Inspections in the State of New York serve as a great way to not only evaluate the quality of food estblashiment health and safety practices, but also to improve them. We find that as number of inspections per restaurant increases, the lower the average critical violations per inspection is. However, inpsections are bised towards more affluent areas.

Two actions the State of New York could undertake from the results of this investigation are to inspect in areas of low household earnings as frequently as they do in more affluent areas and to perform a more thorough investigation into the two states identified as areas of concern.

The model we devised was able to successfully correlate two engineered features. We can see a correlation between the number of critical violations in previous inspections and a critical violation being found in the latest one. We also can also postulate that frequent inspections are important, as failure to frequently inspect quickly increases the odds of a critical violations. In the future, we would like to take into account more parameters in the dataset (i.e. approaching permit expiration dates) to try and schedule inspections in a proactive manner.

</div>

</div>

</div>

<div class="cell border-box-sizing code_cell rendered">

<div class="input">

<div class="prompt input_prompt">In [ ]:</div>

<div class="inner_cell">

<div class="input_area">

<div class=" highlight hl-ipython3">

<pre><span></span>
</pre>

</div>

</div>

</div>

</div>

</div>

</div>

</div>
