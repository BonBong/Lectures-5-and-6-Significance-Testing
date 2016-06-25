#Lectures 5 & 6 - Testing for Significance

##**Parametric tests**
###Experimental groups may differ for 2 reasons:
* real effect of intervention
* random variation between samples drawn from the same population 
* I must decide whether: _1_ is large enough relative to _2_ to conclude that a treatment had an effect.

###Calculate the ratio of variances
* between-group variance
* within-group variance 
* If samples are from the same population, the variances will be similar, and have a quotient of 1. 
* **Degrees of Freedom** determine the critical value the ratio (_test statistic_) must reach for the null hypothesis to be rejected. 

###Assumptions for parametric tests
* Gaussian distribution
* equal variance amongst groups
* the errors are independent (_the 'error' refers to the differnce between each value and the mean.
* data are unmatched (_for unpaired data_)/matched (_for repeasted measures data_)

###Student's t-test
* First I should have a lok at the data:
	+ data(_data.set.name_)
	+ head(_data.set.name_)
	+ boxplot(_variable_~_variable_, data = _data.set.name_)
* Secondly, run the t-test:
	+remember that the default for whether or not data is paired is "FALSE".

###Analysis of Variance (ANOVA)
* Use when the grouping factor is equal to or greater than 3 levels.
* R does not make it easy to run an ANOVA - use the **aov()** function set to a suitable variable (_foo_ and _bar_ are used below). Then I must use the _summary()_ function to see the output.
* One-way ANOVA:
	+ foo <- aov(_variable_ ~ _variable_, data = _dataframe_)
	+ summary(_foo_)
* One-way repeated-measures ANOVA:
	+ bar <- aov(_variable_ ~ _variable_ + Error(""), data = _dataframe_)
	+ summary(_bar_)
	+ in R, the "Error" argument points to the variable you  do not want as an input.
* Two-way ANOVA
	+ This test looks at the effect of two independent variables on the effect of an outcome.

###Post-hoc tests
* the p value needs to be corrected for multiple comparisons so as to avoid inflation of type 1 error
* two such tests are used:
	+ Bonferroni= _target p value_ / _number of comparisons_
	+ Holm= _target p value_ / _n - rank no# in terms of degree of significance + 1
* pairwise post-hoc tests:
	+ pairwise.t.test(_outcome_ $ _variable_ , _outcome_ $ _other.variable_, p.adjust.method = 'bonferroni', paired = FALSE)
	+the bonferroni post-hoc test is the easiest to use. It is, however, limited to 4 comparisons. 
	+ if I do not have to compare all pairs, then I can make a vector of p values from each of the planned comparisons. Then adjust the p values accordingly using the _p.adjust()_ funtion. 
		* p.adjust(_pvalue.vector_, method = 'bonferroni')

##**Non-parametric Tests**
###Assumptions
* Like the parametric test, the errors are independent 
* data are unmatched (_for unpaired data_)/ matching is effective (_for repeated measures data_).
* samples are drawn from populations with the same _shape distributions_

###Comparing 2 groups
* paired data
	+ wilcox.test(_value_ ~ _group_, data = _dataframe_, paired = **TRUE**)
* for unpaired data, I must use FALSE

###Comparing more than two groups
* kruskal.test(_value_ ~ _group_, data = _dataframe_)
* friedman.test(_value_ ~ _group_ | _subjectID_, data = _dataframe_)








