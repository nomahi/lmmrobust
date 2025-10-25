
# lmmrobust package


## Robust Variance Estimators for Linear Mixed-Effects Models

Implements bias-corrected robust variance estimators for linear mixed-effects models, addressing the small-sample downward bias in standard sandwich-type estimators. Also provides tools to compute confidence intervals and hypothesis tests using t-approximations based on the effective sample size determined by the cluster structure.



## Installation

Please download "lmmrobust_1.1-1.tar.gz" and install it by R menu: "packages" -> "Install package(s) from local files...".

Download: [please click this link](https://github.com/nomahi/lmmrobust/raw/main/lmmrobust_1.1-1.tar.gz)

Manual: [please click this link](https://github.com/nomahi/lmmrobust/raw/main/lmmrobust_1.1-1.pdf)



```r

#  R example code for implementing the linear mixed-effects model analysis for clustered binary outcome data

# The "lmmrobust" package
# GitHub webpage: https://github.com/nomahi/lmmrobust/

###

# Download the R package file from the following URL:
# https://github.com/nomahi/lmmrobust/raw/main/lmmrobust_1.1-1.tar.gz

# Then, install the package (tar.gz format) by R menu: "packages" -> "Install package(s) from local files...".

###

library("lme4")							# load the "lme4" package
library("lmmrobust")					# load the "lmmrobust" package

##

# Analyzing the example dataset "mch" using the linear mixed-effects model analysis

data(mch)

mch$medu.i <- as.numeric(mch$medu<=2)
mch$mmarry.i <- as.numeric(mch$mmarry==2)

mch2 <- mch[mch$ses==2,]				# Specify the 2nd quintile subgroup

lmm1 <- lmer(y ~ x + (1|SOUM), data=mch2)			# Univariate analysis
lmmrobust(lmm1, type="RO", inference="z")
lmmrobust(lmm1, type="MD", inference="z")
lmmrobust(lmm1, type="FG", inference="t")
lmmrobust(lmm1, type="MB", inference="t")


lmm2 <- lmer(y ~ x + mage + medu.i + mmarry.i + mprig1 + time + (1|SOUM), data=mch2)			# Multivariate analysis
lmmrobust(lmm2, type="RO", inference="z")
lmmrobust(lmm2, type="MD", inference="z")
lmmrobust(lmm2, type="FG", inference="t")
lmmrobust(lmm2, type="MB", inference="t")

##

data(epil)

lmm3 <- lmer(y ~ trt + lbase + lage + (1|subject), data=epil)
lmmrobust(lmm3, type="RO", inference="z")
lmmrobust(lmm3, type="MD", inference="z")
lmmrobust(lmm3, type="FG", inference="t")
lmmrobust(lmm3, type="MB", inference="t")
