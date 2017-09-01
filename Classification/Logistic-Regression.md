# Logistic Regression

Logistic Regression is a class of generalized linear model. The odjective of a logistic regression is to model the probability of occurrence of a determinated outcome. This kind of models have some advantages over more complex methodologies. Some of theirs are the following

- Easy to fit.
- Transparent box, you can understand why the model take that desition
- Base for more complex methods.
- The weights have an interpretation as "odds ratio"
- statistical inference asociated to the weights
- Confidence intervals and those statistical stuff

### Introduction
To introduce the logistic regression model, let start with the linear regression model. The clasic linear regresion model is defined like

<a href="http://www.codecogs.com/eqnedit.php?latex=$$y_i=\beta_0&plus;\beta_1x_{i1}&plus;\beta_2x_{i2}&plus;\ldots&plus;\beta_kx_{ik}&plus;\varepsilon_i,~~~\varepsilon\sim&space;N(0,\sigma^2)$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$y_i=\beta_0&plus;\beta_1x_{i1}&plus;\beta_2x_{i2}&plus;\ldots&plus;\beta_kx_{ik}&plus;\varepsilon_i,~~~\varepsilon\sim&space;N(0,\sigma^2)$$" title="$$y_i=\beta_0+\beta_1x_{i1}+\beta_2x_{i2}+\ldots+\beta_kx_{ik}+\varepsilon_i,~~~\varepsilon\sim N(0,\sigma^2)$$" /></a>

But, using properties of expected values, variance and normal distibution, is easy to show that

<a href="http://www.codecogs.com/eqnedit.php?latex=$$y_i\sim&space;N(\beta_0&plus;\beta_1x_{i1}&plus;\beta_2x_{i2}&plus;\ldots&plus;\beta_kx_{ik},\sigma^2)$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$y_i\sim&space;N(\beta_0&plus;\beta_1x_{i1}&plus;\beta_2x_{i2}&plus;\ldots&plus;\beta_kx_{ik},\sigma^2)$$" title="$$y_i\sim N(\beta_0+\beta_1x_{i1}+\beta_2x_{i2}+\ldots+\beta_kx_{ik},\sigma^2)$$" /></a>

So, what's the point here? simple, here we can notice that a linear regression model is simple a normal, changing their mean for a linear function of data.

Backing to the logistic regression, that kind of regression is the same concep, but the models isn't a normal but it's a Bernoulli.
To remember

<a href="http://www.codecogs.com/eqnedit.php?latex=$$Y&space;\sim&space;Bernoulli(p),~&space;p&space;\in&space;[0,1]~~&space;\Rightarrow&space;~~&space;P(Y&space;=&space;y)&space;=&space;p^y(1-p)^{1-y},&space;~&space;y&space;\in&space;\{0,&space;1\}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$Y&space;\sim&space;Bernoulli(p),~&space;p&space;\in&space;[0,1]~~&space;\Rightarrow&space;~~&space;P(Y&space;=&space;y)&space;=&space;p^y(1-p)^{1-y},&space;~&space;y&space;\in&space;\{0,&space;1\}$$" title="$$Y \sim Bernoulli(p),~ p \in [0,1]~~ \Rightarrow ~~ P(Y = y) = p^y(1-p)^{1-y}, ~ y \in \{0, 1\}$$" /></a>

and
<a href="http://www.codecogs.com/eqnedit.php?latex=$$E(y)&space;=&space;p$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$E(y)&space;=&space;p$$" title="$$E(y) = p$$" /></a>

so, what if we say that the mean of a Bernoulli is not a fixed value but a linear function of the data, as we did in the normal case? short answer: we can't. why? 

imagine that we can, so we will have that

<a href="http://www.codecogs.com/eqnedit.php?latex=$$P(Y&space;=&space;y_i)&space;=&space;y_i^{\beta_0&space;&plus;&space;\beta_1x_{i1}&space;&plus;&space;\beta_2x_{i2}&space;&plus;&space;\ldots}(1-y)^{1&space;-&space;\beta_0&space;&plus;&space;\beta_1x_{i1}&space;&plus;&space;\beta_2x_{i2}&space;&plus;&space;\ldots}$$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$$P(Y&space;=&space;y_i)&space;=&space;y_i^{\beta_0&space;&plus;&space;\beta_1x_{i1}&space;&plus;&space;\beta_2x_{i2}&space;&plus;&space;\ldots}(1-y)^{1&space;-&space;\beta_0&space;&plus;&space;\beta_1x_{i1}&space;&plus;&space;\beta_2x_{i2}&space;&plus;&space;\ldots}$$" title="$$P(Y = y_i) = y_i^{\beta_0 + \beta_1x_{i1} + \beta_2x_{i2} + \ldots}(1-y)^{1 - \beta_0 + \beta_1x_{i1} + \beta_2x_{i2} + \ldots}$$" /></a>

Now I want you to imagine that you have <a href="http://www.codecogs.com/eqnedit.php?latex=$\beta_0&space;=&space;2$" target="_blank"><img src="http://latex.codecogs.com/gif.latex?$\beta_0&space;=&space;2$" title="$\beta_0 = 2.67$" /></a> and all your other variables are 0, then you are saying that the mean of a Bernoulli a.k.a probability of ocurrence is greater than one?!.
so, how we deal with that problem? a simple way is to scale the linear function to make us sure that we will never have a value over than one or under zero.
With that spirit we will use a function that we will known as **link function**. 
Please notice that if   

<a href="http://www.codecogs.com/eqnedit.php?latex=-\infty&space;<&space;x&space;<&space;\infty&space;\Rightarrow&space;\frac{\exp(x)&space;}{\exp(x)&space;&plus;1&space;}&space;\in&space;[0,&space;1]" target="_blank"><img src="http://latex.codecogs.com/gif.latex?-\infty&space;<&space;x&space;<&space;\infty&space;\Rightarrow&space;\frac{\exp(x)&space;}{\exp(x)&space;&plus;1&space;}&space;\in&space;[0,&space;1]" title="-\infty < x < \infty \Rightarrow \frac{\exp(x) }{\exp(x) +1 } \in [0, 1]" /></a>

