# Business-Analysis-Template
Using Bayesian Approach to answer Business questions
Tools -Pymc3, Python

Every Business has to answer a lot of business questions every day; from simple questions like Are we profiting? Is our new campaign engaging new-fans or just our old-fans? to questions like Is Strategy A really working or is it just the effect of Strategy B?
Depending upon the variables collected, data collection process and some expertise we can easily answer such questions. Some of us may already predict the answers without even analyzing from instinct and experience which comes from domain expertise and some of us has to map every single possibility to make reasons with numbers. In this example we are using Bayesian statistic as it helps to incorporate both instinct and data.

## Business Question
Are Marketing Expense and R&D expenses really affecting our profit or is it just one causing another?
To answer this question, we will be using multivariable regression model because its good at knocking out spurious association which is what the question is all about; we will talk a lot about this later. The first and foremost thing in our workflow is to set our prior. A prior is just our prior belief; i.e. what do we know about our parameters before we see the data so that we don’t have to look for everything. Therefore, a prior is just a way of telling our model what is infinity and what is not.
A prior can be improved and narrowed with right domain knowledge and expertise.

![Intercept-		a~ Normal(0,0.5)
	Beta(marketing)-	bM~Normal(0,0.5)
	Beta(R&D)-		bRD~ Normal(0,0.5)
Mean-			mu =a+bM*M_std+bA*RD_std
](http://www.sciweavers.org/tex2img.php?eq=1%2Bsin%28mc%5E2%29&bc=White&fc=Black&im=jpg&fs=12&ff=arev&edit=)

