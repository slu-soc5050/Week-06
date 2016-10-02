Lab-06-Replication
==================

-   SOC 5050: Quantitative Analysis
-   02 Oct 2016
-   CHRIS

### Part 1: Random Variables

```stata
.  display (25-21)/3 // calculate z
1.3333333

. display normal(1.3333333) // calculate z's probability
.90878877
```  

1. The probability of drawing an individual with a score of 25 is relatively low (p=.909) . The probability value reported indicates that approximately 90% of values in this distribution of test scores fall at or below 25.

Note that you could embed the first display command within the second: `display normal((25 -21)/3)`. Also note that the normal distribution is appropriate because of the text of the question, which gives you evidence to suggest its use.

```stata
.  display (19-21)/3 // calculate z
-.66666667

. display normal(-.66666667) // calculate z's probability
.25249254
```

2. The probability of drawing an individual with a score of 19 is p=.252. This means that approximately 25% of values in this distribution of test score fall at or below 19.

```stata
.  display binomialtail(250,25,.08)
.14739275
```

3. The probability of seeing 25 or more successes in a series of 250 independent trials w here the probability of success is p=.08 is relatively low (p=.147). There is only a 14. 7% chance of this occurring. Another way to think about it is that, if the series of trials were repeated multiple times, we would expect this outcome to occur only 14.7% of the time.

Note that the binomial distribution is appropriate because this question indicates that you meet all four conditions of BINS: a binary outcome, independence, a fixed sample size , and a stable probability.

```stata
.  display binomial(250,25,.08)
.89710124
```

4. The probability of seeing 25 or fewer successes in a series of 250 independent trials where the probability of success is p=.08 is very high (p=.897). We would expect to see this outcome occur almost 90% of the time.

```stata
.  display binomialp(250,25,.08)
.04449399
```

5. The probability of seeing exactly 25 successes in a series of 250 independent trials w here the probability of success is p=.08 is very low (p=.044). We would expect to see this outcome only about 4% of the time.

```stata
.  display 800*.025 // calculate lambda
20

. display poissontail(20,5) // calculate poisson probability
.99998306
```

6. The probability of seeing 5 or more failures over the course of 800 rocket launches where the probability of failure is p=.025 (i.e. a failure occurs in 2.5% of launches) is very, very high (p=.999). It is almost certain that 5 or more failures would be observed over this period.

Note that the Poisson distribution is appropriate because of the large number of events combined with the small probability.

```stata
.  display poissonp(20,18) // note - using lambda from line 109
.08439355
```

7. The probability of seeing exactly 18 failures over the course of 800 rocket launches w here the probability of failure is p=.025 is quite low (p=.084). There is about an 8.5% chance that exactly 18 failures are observed.

```stata
.  display binomialtail(50,40,.3)
3.933e-13
```

8. The probability of seeing 40 or more successes in a series of 50 independent trials where the probability of success is p=.03 is basically 0 (p=3.933e-13). This outcome is exceptionally unlikely.

Note that the binomial distribution is appropriate because this question indicates that you meet all four conditions of BINS: a binary outcome, independence, a fixed sample size , and a stable probability.

```stata
.  display binomialp(50,40,.8)
.13981901
```

9.  The probability of seeing exactly 40 successes in a series of 50 independent trials where the probability of success is p=.08 is somewhat likely (p=.140). There is a 14% chance of this occurring. This outcome seems small, but if you graph the binomial distribution with the parameters n=50 and p=.08, you will see that k=40 actually has the highest likelihood of occurring. You can do this easily in Stata:

```stata
. set obs 50 number of observations (\_N) was 0, now 50

. generate k = \_n-1

. gen b = binomialp(50,k,.8)

. scatter b k
```

Graphing probability mass functions can be incredibly helpful for understanding the context of individual probabilities.

Note that the binomial distribution is appropriate because this question indicates that you meet all four conditions of BINS: a binary outcome, independence, a fixed sample size , and a stable probability.

```stata
.  display 3000*.01 // calculate lambda
30

. display poissonp(30,24) // calculate poisson probability
.04259611
```

10. The probability of seeing exactly 24 infections in a village of 3,000 where the probability of infection is p=.01 is quite low (p=.043). There is only about a 4% chance of seeing this outcome.

Note that the Poisson distribution is appropriate because of the large number of events combined with the small probability.

```stata
.  display poisson(30,12)
.0001677
```

11. The probability of seeing 12 or fewer infections in a village of 3,000 where the prob ability of infection is p=.01 is very, very low (p=.0002).

Note that the Poisson distribution is appropriate because of the large number of events combined with the small probability.

```stata
.  display poissontail(30,40)
.04625304
```

12. The probability of seeing 40 or more infections in a village of 3,000 where the probability of infection is p=.01 is very low (p=.0426). This indicates that there is only a 4.26% chance of seeing 40 or more infections.

### Part 2: Skew and Kurtosis by Hand

13. As calculated by hand, the skew of the distribution is sk=-0.289. This indicates a sl ight amount of negative, left skew. There is a small amount of asymmetry in the distribution relative to the standard normal but, because the value for skew is less than 2, the variable's distribution is not considered problematic in terms of its skew.

As calculated by hand, the kurtosis of the distribution is k=1.761. This indicates a platykurtic distribution where there are more observations in the tails (i.e. "heavier" tail s) than in a standard normal distribution. Since the value for kurtosis is less than 5, the variable's distribution is not considered problematic in terms of its kurtosis.

These calculations are included by hand, and can also be checked using the included spreadsheet. If you are still not convinced, I've included in a Stata dataset as well. Simply use the `summarize` command with the `detail` option and you can check your own work twice!

### Part 3: Normality Testing in Stata

```stata
.  use "$projName/$newData"
(Current Population Survey, December 2011: Food Security Supplement)

. summarize HRNUMHOU, detail

                          HRNUMHOU
-------------------------------------------------------------
      Percentiles      Smallest
 1%            0              0
 5%            0              0
10%            1              0       Obs             151,308
25%            2              0       Sum of Wgt.     151,308

50%            3                      Mean           2.977001
                        Largest       Std. Dev.      1.893407
75%            4             16
90%            5             16       Variance       3.584989
95%            6             16       Skewness       .7163182
99%            8             16       Kurtosis       4.316437
```

14a. The variable's skew is s=.716. This indicates a slight amount of positive, right skew. There is a small amount of asymmetry in the distribution relative to the standard normal but, because the value for skew is less than 2, the variable's distribution is not considered problematic in terms of its skew.

14b. The variable's kurtosis is k=4.316. This indicates a leptokurtic distribution where there are are fewer observations in the tails (i.e. "lighter" tails) than in a standard normal distribution. Since the value for kurtosis is less than 5, the variable's distribution is not considered problematic in terms of its kurtosis.

```stata
.  pnorm HRNUMHOU, scheme(s2mono) title(Probablity Normal Plot for HRNUMHOU) ///
   subtitle(2011 CPS) note("Produced by Christopher Prener, PhD")

. graph export "$projName/Plots/fig1.png", as(png) width(800) height(600) replace
(file Lab-06-Replication/Plots/fig1.png written in PNG format)
```

14c. The p-p plot does not indicate large shifts away from normal since the point values are laid out along the 45-degree line.

```stata
.  qnorm HRNUMHOU, scheme(s2mono) title(Quantile-Quantile Plot for HRNUMHOU) ///
   subtitle(2011 CPS) note("Produced by Christopher Prener, PhD")



. graph export "$projName/Plots/fig2.png", as(png) width(800) height(600) replace
(file Lab-06-Replication/Plots/fig2.png written in PNG format)
```

14d. The q-q plot does indicate some shifts away from normal since the point values in the tails do shift away from the 45-degree line.

14e. Given that the variable HRNUMHOU's n of 151,308 lies outside of the acceptable range for either the Shapiro-Wilk and Shapiro-Francia tests, neither test can be considered appropriate for testing normality.

```stata
.  swilk HRNUMHOU

                   Shapiro-Wilk W test for normal data

    Variable |        Obs       W           V         z       Prob>z
-------------+------------------------------------------------------
    HRNUMHOU |    151,308    0.98338    669.935    18.324    0.00000

. sfrancia HRNUMHOU

                  Shapiro-Francia W' test for normal data

    Variable |       Obs       W'          V'        z       Prob>z
-------------+-----------------------------------------------------
    HRNUMHOU |   151,308    0.98346   1225.175    22.039    0.00001

Note: The normal approximation to the sampling distribution of W'
      is valid for 10<=n<=5000 under the log transformation.
```

14f. The results of the Shapiro-Wilk test (W=0.983; p=0.000) indicate that variable `HRNUMHOU` is not normally distributed. The results of the Shapiro-Francia test (W'=0.983; p=0. 000) indicate that variable `HRNUMHOU` is not normally distributed. It is important to note that the variable `HRNUMHOU` violates the assumptions for both tests. The sample size for `HRNUMHOU` is so large that even the most minute deviations from normal will result in a statistically significant result on both tests. They should therefore not be factored into any decision about the normality of `HRNUMHOU`.

14g. This question was not asked, but if you were asked to weight all of the information before you about the normality of the variable `HRNUMHOU`, you would disregard the information from the Shapiro-Wilk and Shapiro-Francia tests. Instead, you would focus on the bulk of the evidence (the skew, kurtosis, and the p-p plot), all of which point to a variable that is approximately normally distributed. On the whole, these could be argued to outweigh the evidence of the q-q plot, which does suggest some deviations from normal.
