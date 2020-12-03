# Business-Analysis-Template
Using Bayesian Approach to answer Business questions<br/>
- Tools -Pymc3, Python<br/>

Every Business has to answer a lot of business questions every day; from simple questions like Are we profiting? Is our new campaign engaging new-fans or just our old-fans? to questions like Is Strategy A really working or is it just the effect of Strategy B?
Depending upon the variables collected, data collection process and some expertise we can easily answer such questions. Some of us may already predict the answers without even analyzing from instinct and experience which comes from domain expertise and some of us has to map every single possibility to make reasons with numbers. In this example we are using Bayesian statistic as it helps to incorporate both instinct and data.

## Our Business Question
Are Marketing Expense and R&D expenses really affecting our profit or is it just one causing another?
To answer this question, we will be using multivariable regression model because its good at knocking out spurious association which is what the question is all about; we will talk a lot about this later. The first and foremost thing in our workflow is to set our prior. A prior is just our prior belief; i.e. what do we know about our parameters before we see the data so that we don’t have to look for everything. Therefore, a prior is just a way of telling our model what is infinity and what is not.
A prior can be improved and narrowed with right domain knowledge and expertise.

 *Mathematically;*<br/>
&nbsp;&nbsp;&nbsp;- Intercept&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![intercept](https://latex.codecogs.com/png.latex?a%5Csim%20Normal%280%2C0.5%29)<br/>
&nbsp;&nbsp;&nbsp;- Beta(marketing)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Beta(marketing)](https://latex.codecogs.com/png.latex?bM%20%5Csim%20Normal%280%2C0.5%29)<br/>
&nbsp;&nbsp;&nbsp;- Beta(R&D)&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Beta(RD)](https://latex.codecogs.com/png.latex?bRD%20%5Csim%20Normal%280%2C0.5%29)<br/>
&nbsp;&nbsp;&nbsp;- Mean&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;![Beta(mu)](https://latex.codecogs.com/png.latex?mu%20%3Da&plus;bM*M%28std%29&plus;bRD*RD%28std%29)<br/>
*Assuming mean of profit is normally distributed*<br/>
<br/>
You can also do some prior predictive checks if you want to get the sense of your priors. However I will be skipping prior predictive here.

### Data
In this example we will be taking a slice of profit and Loss account. The following are the variables simulated. 
-M_expenses: Marketing expenses in million
-RD_expenses: Research and Development expenses in million
-Profit: Profit in million (loss in negative)
Fig: Pair Plot

We can already see some association along all the variables. We can also calculate covariance if we want relationship in numbers.

### Model-1
Our model will assume that profit will be distributed Normally:
*Mathematically
	Intercept-		a ~ Normal(0,0.5)
	Beta(marketing)-	bM~Normal(0,0.5)
	Beta(R&D)-		bRD~ Normal(0,0.5)
	Mean-			mu =a+bM*M_std+bRD*RD_std
	Sigma-			sigma~Exponential(1)
	Profit_std-		profit~ Normal(mu,sigma)


Let plot posterior predictive 


<img src="https://github.com/roesta07/Business-Analysis-Template/blob/main/img/posterior_predective_2.png" width="400" height="400">


At this point you can finalize your report; our model finds out the association of both variables with profit and gives pretty okay predictions. But wait; you still have some gut feeling of something is wrong that this is not it or you remember your boss saying something unusual is happening and you decide to look a deeper look at your data. This process is crucial. People often think statistical modelling is just about data & numbers so they often ignore information cues that is important to any model; which is why communicating to domain experts or people around the field is as much important as knowing statistics

### Digging deep into Data
Let’s take a deep look at the data yearly.

**Trend Plot 


<img src="https://github.com/roesta07/Business-Analysis-Template/blob/main/img/trend_3.png" width="1000" height="400">


### Model 2-First Seven Years
In this model we will be working with only frist seven years 
*Mathematically
	Intercept-		a ~ Normal(0,0.5)
	Beta(marketing)-	bM~Normal(0,0.5)
	Beta(R&D)-		bRD~ Normal(0,0.5)
	Mean-			mu =a+bM*M_std[:till year 7]+bRD*RD_std[:till year seven]
	Sigma-			sigma~Exponential(1)
	Profit_std-		profit~ Normal(mu,sigma)*
	

### Model 3 -Later Seven Years
In this Model we will be working with the later seven years

*Mathematically
	Intercept-		a ~ Normal(0,0.5)
	Beta(marketing)-	bM~Normal(0,0.5)
	Beta(R&D)-		bRD~ Normal(0,0.5)
	Mean-			mu =a+bM*M_std[year seven:]+bRD*RD_std[year seven:]
	Sigma-			sigma~Exponential(1)
	Profit_std-		profit~ Normal(mu,sigma)*

Best way to demonstrate the change in parameters in using forest plot:
<img src="https://github.com/roesta07/Business-Analysis-Template/blob/main/img/forest_plot_4.png" width="700" height="300">

### CounterFactuals
We have seen the change now let’s see the affect. Such affects can be seen by asking further questions like what does change in one variable and keeping the other variables constant does with the outcome? It’s basically the question about past that if we had done this what would have happened? 


<img src="https://github.com/roesta07/Business-Analysis-Template/blob/main/img/counter_1.png" width="1000" height="400">
<img src="https://github.com/roesta07/Business-Analysis-Template/blob/main/img/counter_2.png" width="1000" height="400">


### Findings 
- For first seven years Marketing was the cause of profit given only two predictor variable
- After seven years till fourteen years Marketing had minimal or no affect to profit but was mimicking the association of R&D and profit. In statistical term it’s called spurious association. 

Note: Multivariable regression does a very good thing by knocking the spurious association. It does this by looking at the association of the residuals for each variable after removing the effect of one. This all happens at the back of the algorithm so you don’t have to worry about it; well for now.


Lastly, let's lets plot the Model prediction; which will look slightly better than Model 1

<img src="https://github.com/roesta07/Business-Analysis-Template/blob/main/img/predective_posterior.png" width="1000" height="450">




