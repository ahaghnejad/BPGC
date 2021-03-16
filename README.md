# BPGC
This repository contains the Matlab code for implementing the bootstrap panel Granger causality procedure proposed by Kónya (Kónya, L. Exports and growth: Granger causality analysis on OECD countries with a panel data approach. Economic Modelling, 23(6), 978-992, 2006), which is based on the seemingly unrelated regressions (SUR) systems and the Wald tests with individual-specific bootstrap critical values, and accounts for both cross-sectional error dependence and slope heterogeneity across individual units.
1. Description
This repository contains the Matlab code for implementing the bootstrap panel Granger causality procedure proposed by Kónya (2006), which is based on the seemingly unrelated regressions (SUR) systems and the Wald tests with individual-specific bootstrap critical values, and accounts for both cross-sectional error dependence and slope heterogeneity across individual units. 

2. Usage
Download the Bootstrap_Panel_Causality.rar file and unzip it in a directory of your choice. Within the unzipped folder Bootstrap_Panel_Causality, you will find two files and one subfolder. The files are:
	causality.m: a Matlab script file for implementing the bootstrap panel Granger causality procedure proposed by Kónya, L. (2006).
	data.xlsx: an excel file containing the sample data.
In addition, the subfolder is Functions, which contains four Matlab routines (m-files) required by the causality.m script.

3. Citation
This code is provided as supplementary material for our paper:
Haghnejad, A., Samadi, S., Nasrollahi, K., Azarbayjani, K., & Kazemi, I. (2020). Market power and efficiency in the Iranian banking industry. Emerging Markets Finance and Trade, 56(13), 3217-3234. 
Please cite this paper if you are using the code in your research.

4. The bootstrap panel Granger causality test
Kónya (2006) proposes a panel Granger causality test based on the seemingly unrelated regressions (SUR) systems and the Wald tests with individual-specific bootstrap critical values, which accounts for both cross-sectional error dependence and slope heterogeneity across individual units. In the framework of the bootstrap panel causality approach, Granger causality from x to y can be tested using the following set of equations:
	y_(1,t)=α_1+∑_(j=1)^ly▒β_(1,j)  y_(1,t-j)+∑_(j=1)^lx▒γ_(1,j)  x_(1,t-j)+ε_(1,t),	
	y_(2,t)=α_2+∑_(j=1)^ly▒β_(2,j)  y_(2,t-j)+∑_(j=1)^lx▒γ_(2,j)  x_(2,t-j)+ε_(2,t),	
	⋮          ⋮                                ⋮                               ⋮	
	y_(N,t)=α_N+∑_(j=1)^ly▒β_(N,j)  y_(N,t-j)+∑_(j=1)^lx▒γ_(N,j)  x_(N,t-j)+ε_(N,t),                         (1) 
where N refers to the number of cross-sections in the panel, t to the time period (t=1,…,T), lx and ly to the optimal lag lengths, and ε_(i,t) to the idiosyncratic error terms. The individual regressions may be related through the contemporaneous correlation across individuals. In this context, the set of equations (1) is a SUR system, rather than a vector autoregressive (VAR) model. Therefore, this system cannot be efficiently estimated equation‐by‐equation using the OLS estimator. Instead, as mentioned previously, Kónya (2006) suggests the more efficient estimation of the parameters with the SUR approach. 
In general, a test of Granger causality from x to y for each individual i can be carried out by testing the joint hypothesis that all the coefficients on the lagged x_i are zero (H_0:γ_(i,1)=⋯=γ_(i,lx)=0) . If the null hypothesis cannot be rejected, there is no Granger causality from x to y for individual i. On the other hand, rejection of the null hypothesis (not all γ_i’s are zero) implies that there is Granger causality running from x to y for individual i. 
Since the results of the causality analysis may be sensitive to the lag structure, the number of optimal lags must be specified before proceeding to the next step. Following the Kónya (2006), the optimal lags are allowed to vary across series but not across equations. In this context, the set of equations (1) is estimated for each possible pair of ly and lx. Then, the combination that minimizes the Akaike information criterion (AIC) or Schwarz-Bayesian criterion (SBC) is selected as the optimal lags. The procedure proposed by Kónya (2006) for testing Granger causality from x to y in a bivariate framework may proceed in several steps, as follows: 
Step 1: Estimate the set of equations (1) in a SUR framework, implement the Wald procedure for testing the null hypothesis of no Granger causality from x to y for each cross‐section (γ_(i,j)=0 for all i and j), and then calculate the individual Wald statistics.
Step 2: Re-estimate the set of equations (1) under the null hypothesis of no Granger causality from x to y (i.e., imposing the γ_(i,j) =0 for all i and j), obtain the corresponding residuals as
	e_(H_0,i,t)=y_(i,t)-α ̂_i-∑_(j=1)^ly▒〖β ̂_(i,j) y_(i,t-j) 〗,                                        (2)  
and, then construct the [e_(H_0,i,t) ]_(N×T) matrix from the residuals.
Step 3: Re-sample the residuals. In order to preserve the contemporaneous correlation structure of the errors in the set of equations (1), a full column from the [e_(H_0,i,t)] matrix at a time is randomly selected (i.e., the residuals for each individual unit should not be drawn one‐by‐one). The selected bootstrap residuals are denoted as e_(H_0,i,t)^*, where i=1,…,N and t=1,…,T^* and T^* can be greater than T.
Step 4: Generate the bootstrap samples of y under the null hypothesis of no Granger causality from x to y, recursively, based on the following formula:
	y_(i,t)^*=α ̂_i+∑_(j=1)^ly▒β ̂_(i,j)  y_(i,t-j)^*+e_(H_0,i,t)^*,      t=1,⋯,T^*,                          (3)
where α ̂_i and β ̂_(i,j) are the estimates of the parameters in step 2. 
Step 5: Substitute y_(i,t)^* for y_(i,t) and estimate the set of equations (1) without imposing any restrictions on the parameters, and then calculate the individual Wald statistics by testing for the non-causality null hypothesis for each of the cross-sectional units. 
Step 6: Obtain the empirical distribution of the individual Wald statistics by repeating steps 3‐5 many times, calculate the appropriate percentiles of the bootstrap distributions (bootstrap critical values), and then compare the Wald statistics corresponding to the original data set (step 1) with the empirical critical values for each cross‐section.

References
Haghnejad, A., Samadi, S., Nasrollahi, K., Azarbayjani, K., & Kazemi, I. (2020). Market power and efficiency in the Iranian banking industry. Emerging Markets Finance and Trade, 56(13), 3217-3234. 
Kónya, L. (2006). Exports and growth: Granger causality analysis on OECD countries with a panel data approach. Economic Modelling, 23(6), 978-992. 
