# Get the seasonally adjusted model from a workspace

Generic functions to retrieve seasonally adjusted model(s) from
`workspace`, `multiprocessing` or `sa_item` object. `get_model` returns
a `"SA"` object while `get_jmodel` returns the Java objects of the
models.

## Usage

``` r
get_jmodel(
  x,
  workspace,
  userdefined = NULL,
  progress_bar = TRUE,
  type = c("Domain", "Estimation", "Point")
)

get_model(
  x,
  workspace,
  userdefined = NULL,
  progress_bar = TRUE,
  type = c("Domain", "Estimation", "Point")
)
```

## Arguments

- x:

  the object from which to retrieve the seasonally adjusted model.

- workspace:

  the workspace object where models are stored. If `x` is a `workspace`
  object, this parameter is not used.

- userdefined:

  a vector containing the names of additional output variables. (see
  [`x13`](x13.md) or [`tramoseats`](tramoseats.md)).

- progress_bar:

  Boolean: if `TRUE`, a progress bar is printed.

- type:

  a `character` indicating the type of model to retrieve: \`"Domain"\`
  (initial specification), \`"Estimation"\` (specification used for the
  current estimation) or "Point" (specification corresponding to the
  results of the current estimation: fully identified model).

## Value

`get_model()` returns a seasonally adjusted object (class
`c("SA", "X13")` or `c("SA", "TRAMO_SEATS"`) or a list of seasonally
adjusted objects:

- if `x` is a `sa_item` object, `get_model(x)` returns a `"SA"` object
  (or a [`jSA`](jSA.md) object with `get_jmodel(x)`);

- if `x` is a `multiprocessing` object, `get_ts(x)` returns a list of
  length the number of sa_items, each element containing a `"SA"` object
  (or a [`jSA`](jSA.md) object with `get_jmodel(x)`);

- if `x` is a `workspace` object, `get_ts(x)` returns list of length the
  number of multiprocessings, each element containing a list of `"SA"`
  object(s) (or [`jSA`](jSA.md) object's) with `get_jmodel(x)`).

## See also

Other functions to retrieve information from a workspace,
multiprocessing or sa_item: [`count`](count.md),
[`get_name`](get_name.md), [`get_ts`](get_ts.md).

[`compute`](compute.md)

## Examples

``` r
# \donttest{
spec_x13 <- x13_spec(spec = "RSA5c", easter.enabled = FALSE)
sa_x13 <- x13(ipi_c_eu[, "FR"], spec = spec_x13)
spec_ts <- tramoseats_spec(spec = "RSA5")
sa_ts <- tramoseats(ipi_c_eu[, "FR"], spec = spec_ts)

wk <- new_workspace()
mp <- new_multiprocessing(wk, "sap1")
add_sa_item(wk, "sap1", sa_x13, "X13")
add_sa_item(wk, "sap1", sa_ts, "TramoSeats")

compute(wk) # It's important to compute the workspace before retrieving the SA model
sa_item1 <- get_object(mp, 1)

get_model(sa_item1, wk) # To extract the model of the sa_item1: its the object sa_x13
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     0.02043      0.107
#> Phi(2)     0.11093      0.077
#> Theta(1)  -0.58663      0.098
#> BTheta(1) -0.69921      0.041
#> 
#>              Estimate Std. Error
#> Monday         0.6788      0.244
#> Tuesday        0.9500      0.245
#> Wednesday      1.0053      0.246
#> Thursday      -0.0656      0.245
#> Friday         1.0304      0.245
#> Saturday      -1.5721      0.245
#> Leap year      2.1513      0.753
#> TC (4-2020)  -36.1532      2.193
#> AO (3-2020)  -20.2213      2.255
#> AO (5-2011)   13.2210      1.970
#> LS (11-2008) -12.7459      1.663
#> 
#> 
#> Residual standard error: 2.294 on 343 degrees of freedom
#> Log likelihood = -811.8, aic =  1656 aicc =  1657, bic(corrected for length) = 1.907
#> 
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.127
#> M(2)    0.076
#> M(3)    1.139
#> M(4)    0.080
#> M(5)    1.072
#> M(6)    0.030
#> M(7)    0.084
#> M(8)    0.244
#> M(9)    0.063
#> M(10)   0.254
#> M(11)   0.239
#> Q       0.319
#> Q-M2    0.349
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s           i
#> Jan 2020 101.0 102.92412 102.8147  -1.9241199   0.1094395
#> Feb 2020 100.1 103.50547 102.8976  -3.4054722   0.6078825
#> Mar 2020  91.8  83.00218 103.1831   8.7978221 -20.1809275
#> Apr 2020  66.7  65.83747 103.6570   0.8625259 -37.8194996
#> May 2020  73.7  78.73548 104.1282  -5.0354792 -25.3926864
#> Jun 2020  98.2  87.26580 104.5188  10.9342001 -17.2529628
#> Jul 2020  97.4  92.53528 104.7033   4.8647224 -12.1679796
#> Aug 2020  71.7  97.64618 104.5690 -25.9461813  -6.9227978
#> Sep 2020 104.7  97.34380 104.1405   7.3562012  -6.7967236
#> Oct 2020 106.7  98.78451 103.5511   7.9154948  -4.7665946
#> Nov 2020 101.6 100.50933 103.0298   1.0906693  -2.5204281
#> Dec 2020  96.6  99.74645 102.7263  -3.1464483  -2.9798265
#> 
#> Forecasts:
#>                y_f     sa_f      t_f         s_f         i_f
#> Jan 2021  94.82712 101.3420 102.6158  -6.5148928 -1.27380795
#> Feb 2021  98.00197 101.8372 102.5826  -3.8352640 -0.74540432
#> Mar 2021 113.62540 101.9088 102.5235  11.7165747 -0.61463800
#> Apr 2021 103.28588 102.3855 102.3987   0.9004327 -0.01326784
#> May 2021  96.23640 101.5938 102.2898  -5.3574428 -0.69592946
#> Jun 2021 113.04727 101.6902 102.2365  11.3570720 -0.54632230
#> Jul 2021 104.27161 101.8281 102.2910   2.4435091 -0.46291753
#> Aug 2021  79.29357 102.6462 102.4831 -23.3526340  0.16311885
#> Sep 2021 109.23197 102.7863 102.7326   6.4456639  0.05371199
#> Oct 2021 108.79200 102.9386 102.9781   5.8533505 -0.03947210
#> Nov 2021 106.90616 102.9549 103.2017   3.9512094 -0.24675320
#> Dec 2021 100.22813 103.5456 103.3775  -3.3174206  0.16802658
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         2.238
#>  Seasonal     59.768
#>  Irregular     1.203
#>  TD & Hol.     2.436
#>  Others       34.383
#>  Total       100.028
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.059
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          1.000
#>  qs test on i                           0.985
#>  f-test on sa (seasonal dummies)        0.916
#>  f-test on i (seasonal dummies)         0.812
#>  Residual seasonality (entire series)   0.902
#>  Residual seasonality (last 3 years)    0.966
#>  f-test on sa (td)                      0.983
#>  f-test on i (td)                       0.998
#> 
#> 
#> Additional output variables

# To get all models from the multiprocessing mp:
get_model(mp, wk)
#>   |                                                                              |                                                                      |   0%  |                                                                              |===================================                                   |  50%  |                                                                              |======================================================================| 100%
#> $X13
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     0.02043      0.107
#> Phi(2)     0.11093      0.077
#> Theta(1)  -0.58663      0.098
#> BTheta(1) -0.69921      0.041
#> 
#>              Estimate Std. Error
#> Monday         0.6788      0.244
#> Tuesday        0.9500      0.245
#> Wednesday      1.0053      0.246
#> Thursday      -0.0656      0.245
#> Friday         1.0304      0.245
#> Saturday      -1.5721      0.245
#> Leap year      2.1513      0.753
#> TC (4-2020)  -36.1532      2.193
#> AO (3-2020)  -20.2213      2.255
#> AO (5-2011)   13.2210      1.970
#> LS (11-2008) -12.7459      1.663
#> 
#> 
#> Residual standard error: 2.294 on 343 degrees of freedom
#> Log likelihood = -811.8, aic =  1656 aicc =  1657, bic(corrected for length) = 1.907
#> 
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.127
#> M(2)    0.076
#> M(3)    1.139
#> M(4)    0.080
#> M(5)    1.072
#> M(6)    0.030
#> M(7)    0.084
#> M(8)    0.244
#> M(9)    0.063
#> M(10)   0.254
#> M(11)   0.239
#> Q       0.319
#> Q-M2    0.349
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s           i
#> Jan 2020 101.0 102.92412 102.8147  -1.9241199   0.1094395
#> Feb 2020 100.1 103.50547 102.8976  -3.4054722   0.6078825
#> Mar 2020  91.8  83.00218 103.1831   8.7978221 -20.1809275
#> Apr 2020  66.7  65.83747 103.6570   0.8625259 -37.8194996
#> May 2020  73.7  78.73548 104.1282  -5.0354792 -25.3926864
#> Jun 2020  98.2  87.26580 104.5188  10.9342001 -17.2529628
#> Jul 2020  97.4  92.53528 104.7033   4.8647224 -12.1679796
#> Aug 2020  71.7  97.64618 104.5690 -25.9461813  -6.9227978
#> Sep 2020 104.7  97.34380 104.1405   7.3562012  -6.7967236
#> Oct 2020 106.7  98.78451 103.5511   7.9154948  -4.7665946
#> Nov 2020 101.6 100.50933 103.0298   1.0906693  -2.5204281
#> Dec 2020  96.6  99.74645 102.7263  -3.1464483  -2.9798265
#> 
#> Forecasts:
#>                y_f     sa_f      t_f         s_f         i_f
#> Jan 2021  94.82712 101.3420 102.6158  -6.5148928 -1.27380795
#> Feb 2021  98.00197 101.8372 102.5826  -3.8352640 -0.74540432
#> Mar 2021 113.62540 101.9088 102.5235  11.7165747 -0.61463800
#> Apr 2021 103.28588 102.3855 102.3987   0.9004327 -0.01326784
#> May 2021  96.23640 101.5938 102.2898  -5.3574428 -0.69592946
#> Jun 2021 113.04727 101.6902 102.2365  11.3570720 -0.54632230
#> Jul 2021 104.27161 101.8281 102.2910   2.4435091 -0.46291753
#> Aug 2021  79.29357 102.6462 102.4831 -23.3526340  0.16311885
#> Sep 2021 109.23197 102.7863 102.7326   6.4456639  0.05371199
#> Oct 2021 108.79200 102.9386 102.9781   5.8533505 -0.03947210
#> Nov 2021 106.90616 102.9549 103.2017   3.9512094 -0.24675320
#> Dec 2021 100.22813 103.5456 103.3775  -3.3174206  0.16802658
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         2.238
#>  Seasonal     59.768
#>  Irregular     1.203
#>  TD & Hol.     2.436
#>  Others       34.383
#>  Total       100.028
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.059
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          1.000
#>  qs test on i                           0.985
#>  f-test on sa (seasonal dummies)        0.916
#>  f-test on i (seasonal dummies)         0.812
#>  Residual seasonality (entire series)   0.902
#>  Residual seasonality (last 3 years)    0.966
#>  f-test on sa (td)                      0.983
#>  f-test on i (td)                       0.998
#> 
#> 
#> Additional output variables
#> 
#> $TramoSeats
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     0.02572      0.108
#> Phi(2)     0.16988      0.075
#> Theta(1)  -0.53992      0.102
#> BTheta(1) -0.67459      0.042
#> 
#>               Estimate Std. Error
#> Monday         0.56114      0.231
#> Tuesday        0.89966      0.231
#> Wednesday      1.06703      0.232
#> Thursday       0.02403      0.232
#> Friday         0.86378      0.234
#> Saturday      -1.55222      0.231
#> Leap year      2.19751      0.712
#> Easter [6]    -2.31734      0.461
#> TC (4-2020)  -20.83317      2.183
#> TC (3-2020)  -20.98304      2.183
#> AO (5-2011)   13.28128      1.872
#> LS (11-2008) -12.57486      1.631
#> 
#> 
#> Residual standard error: 2.221 on 342 degrees of freedom
#> Log likelihood = -799.8, aic =  1634 aicc =  1635, bic(corrected for length) = 1.858
#> 
#> 
#> 
#> Decomposition
#> Model
#> AR :  1 + 0.025720 B + 0.169879 B^2 
#> D :  1 - B - B^12 + B^13 
#> MA :  1 - 0.539919 B - 0.674594 B^12 + 0.364227 B^13 
#> 
#> 
#> SA
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 1.531766 B + 0.545834 B^2 
#> Innovation variance:  0.5502022 
#> 
#> Trend
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 + 0.032214 B - 0.967786 B^2 
#> Innovation variance:  0.02623268 
#> 
#> Seasonal
#> AR :  1 + 0.025720 B + 0.169879 B^2 
#> D :  1 + B + B^2 + B^3 + B^4 + B^5 + B^6 + B^7 + B^8 + B^9 + B^10 + B^11 
#> MA :  1 + 1.245052 B + 0.658623 B^2 + 0.593270 B^3 + 0.481574 B^4 + 0.366624 B^5 + 0.304938 B^6 + 0.184553 B^7 + 0.190108 B^8 + 0.095090 B^9 + 0.221559 B^10 + 0.186281 B^11 - 0.207005 B^12 - 0.348481 B^13 
#> Innovation variance:  0.1464012 
#> 
#> Irregular
#> Innovation variance:  0.3257068 
#> 
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s           i
#> Jan 2020 101.0 102.72726 103.1221  -1.7272634  -0.3948220
#> Feb 2020 100.1 102.95124 103.1797  -2.8512352  -0.2284534
#> Mar 2020  91.8  82.31999 103.3030   9.4800115 -20.9830366
#> Apr 2020  66.7  66.85029 103.5340  -0.1502858 -36.6836970
#> May 2020  73.7  79.46771 103.9124  -5.7677083 -24.4446419
#> Jun 2020  98.2  87.82311 104.2371  10.3768872 -16.4139594
#> Jul 2020  97.4  92.74114 104.3260   4.6588650 -11.5848433
#> Aug 2020  71.7  97.04194 104.1300 -25.3419376  -7.0880934
#> Sep 2020 104.7  97.32774 103.6918   7.3722629  -6.3640867
#> Oct 2020 106.7  98.66536 103.2317   8.0346351  -4.5663227
#> Nov 2020 101.6 100.05441 102.8519   1.5455901  -2.7974884
#> Dec 2020  96.6  99.35191 102.5735  -2.7519144  -3.2215659
#> 
#> Forecasts:
#>                y_f     sa_f      t_f        s_f         i_f
#> Jan 2021  94.55690 101.0346 102.4680  -6.477689 -1.43341231
#> Feb 2021  97.86506 101.4506 102.4540  -3.585540 -1.00338862
#> Mar 2021 113.01303 101.7376 102.4400  11.275402 -0.70237203
#> Apr 2021 103.19842 101.9344 102.4260   1.264068 -0.49166042
#> May 2021  96.00309 102.0679 102.4120  -6.064764 -0.34416230
#> Jun 2021 112.77599 102.1571 102.3980  10.618882 -0.24091361
#> Jul 2021 104.03135 102.2154 102.3840   1.815959 -0.16863953
#> Aug 2021  79.09787 102.2520 102.3700 -23.154116 -0.11804767
#> Sep 2021 109.04546 102.2734 102.3560   6.772048 -0.08263337
#> Oct 2021 108.59337 102.2842 102.3421   6.309157 -0.05784336
#> Nov 2021 106.47776 102.2876 102.3281   4.190193 -0.04049035
#> Dec 2021  99.77303 102.2857 102.3141  -2.512692 -0.02834325
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         1.887
#>  Seasonal     58.928
#>  Irregular     0.509
#>  TD & Hol.     2.598
#>  Others       33.908
#>  Total        97.830
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.064
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          1.000
#>  qs test on i                           1.000
#>  f-test on sa (seasonal dummies)        1.000
#>  f-test on i (seasonal dummies)         1.000
#>  Residual seasonality (entire series)   1.000
#>  Residual seasonality (last 3 years)    0.968
#>  f-test on sa (td)                      0.984
#>  f-test on i (td)                       1.000
#> 
#> 
#> Additional output variables
#> 

# To get all models from the workspace wk:
get_model(wk)
#> Multiprocessing 1 on 1:
#>   |                                                                              |                                                                      |   0%  |                                                                              |===================================                                   |  50%  |                                                                              |======================================================================| 100%
#> $sap1
#> $sap1$X13
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     0.02043      0.107
#> Phi(2)     0.11093      0.077
#> Theta(1)  -0.58663      0.098
#> BTheta(1) -0.69921      0.041
#> 
#>              Estimate Std. Error
#> Monday         0.6788      0.244
#> Tuesday        0.9500      0.245
#> Wednesday      1.0053      0.246
#> Thursday      -0.0656      0.245
#> Friday         1.0304      0.245
#> Saturday      -1.5721      0.245
#> Leap year      2.1513      0.753
#> TC (4-2020)  -36.1532      2.193
#> AO (3-2020)  -20.2213      2.255
#> AO (5-2011)   13.2210      1.970
#> LS (11-2008) -12.7459      1.663
#> 
#> 
#> Residual standard error: 2.294 on 343 degrees of freedom
#> Log likelihood = -811.8, aic =  1656 aicc =  1657, bic(corrected for length) = 1.907
#> 
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.127
#> M(2)    0.076
#> M(3)    1.139
#> M(4)    0.080
#> M(5)    1.072
#> M(6)    0.030
#> M(7)    0.084
#> M(8)    0.244
#> M(9)    0.063
#> M(10)   0.254
#> M(11)   0.239
#> Q       0.319
#> Q-M2    0.349
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s           i
#> Jan 2020 101.0 102.92412 102.8147  -1.9241199   0.1094395
#> Feb 2020 100.1 103.50547 102.8976  -3.4054722   0.6078825
#> Mar 2020  91.8  83.00218 103.1831   8.7978221 -20.1809275
#> Apr 2020  66.7  65.83747 103.6570   0.8625259 -37.8194996
#> May 2020  73.7  78.73548 104.1282  -5.0354792 -25.3926864
#> Jun 2020  98.2  87.26580 104.5188  10.9342001 -17.2529628
#> Jul 2020  97.4  92.53528 104.7033   4.8647224 -12.1679796
#> Aug 2020  71.7  97.64618 104.5690 -25.9461813  -6.9227978
#> Sep 2020 104.7  97.34380 104.1405   7.3562012  -6.7967236
#> Oct 2020 106.7  98.78451 103.5511   7.9154948  -4.7665946
#> Nov 2020 101.6 100.50933 103.0298   1.0906693  -2.5204281
#> Dec 2020  96.6  99.74645 102.7263  -3.1464483  -2.9798265
#> 
#> Forecasts:
#>                y_f     sa_f      t_f         s_f         i_f
#> Jan 2021  94.82712 101.3420 102.6158  -6.5148928 -1.27380795
#> Feb 2021  98.00197 101.8372 102.5826  -3.8352640 -0.74540432
#> Mar 2021 113.62540 101.9088 102.5235  11.7165747 -0.61463800
#> Apr 2021 103.28588 102.3855 102.3987   0.9004327 -0.01326784
#> May 2021  96.23640 101.5938 102.2898  -5.3574428 -0.69592946
#> Jun 2021 113.04727 101.6902 102.2365  11.3570720 -0.54632230
#> Jul 2021 104.27161 101.8281 102.2910   2.4435091 -0.46291753
#> Aug 2021  79.29357 102.6462 102.4831 -23.3526340  0.16311885
#> Sep 2021 109.23197 102.7863 102.7326   6.4456639  0.05371199
#> Oct 2021 108.79200 102.9386 102.9781   5.8533505 -0.03947210
#> Nov 2021 106.90616 102.9549 103.2017   3.9512094 -0.24675320
#> Dec 2021 100.22813 103.5456 103.3775  -3.3174206  0.16802658
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         2.238
#>  Seasonal     59.768
#>  Irregular     1.203
#>  TD & Hol.     2.436
#>  Others       34.383
#>  Total       100.028
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.059
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          1.000
#>  qs test on i                           0.985
#>  f-test on sa (seasonal dummies)        0.916
#>  f-test on i (seasonal dummies)         0.812
#>  Residual seasonality (entire series)   0.902
#>  Residual seasonality (last 3 years)    0.966
#>  f-test on sa (td)                      0.983
#>  f-test on i (td)                       0.998
#> 
#> 
#> Additional output variables
#> 
#> $sap1$TramoSeats
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     0.02572      0.108
#> Phi(2)     0.16988      0.075
#> Theta(1)  -0.53992      0.102
#> BTheta(1) -0.67459      0.042
#> 
#>               Estimate Std. Error
#> Monday         0.56114      0.231
#> Tuesday        0.89966      0.231
#> Wednesday      1.06703      0.232
#> Thursday       0.02403      0.232
#> Friday         0.86378      0.234
#> Saturday      -1.55222      0.231
#> Leap year      2.19751      0.712
#> Easter [6]    -2.31734      0.461
#> TC (4-2020)  -20.83317      2.183
#> TC (3-2020)  -20.98304      2.183
#> AO (5-2011)   13.28128      1.872
#> LS (11-2008) -12.57486      1.631
#> 
#> 
#> Residual standard error: 2.221 on 342 degrees of freedom
#> Log likelihood = -799.8, aic =  1634 aicc =  1635, bic(corrected for length) = 1.858
#> 
#> 
#> 
#> Decomposition
#> Model
#> AR :  1 + 0.025720 B + 0.169879 B^2 
#> D :  1 - B - B^12 + B^13 
#> MA :  1 - 0.539919 B - 0.674594 B^12 + 0.364227 B^13 
#> 
#> 
#> SA
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 1.531766 B + 0.545834 B^2 
#> Innovation variance:  0.5502022 
#> 
#> Trend
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 + 0.032214 B - 0.967786 B^2 
#> Innovation variance:  0.02623268 
#> 
#> Seasonal
#> AR :  1 + 0.025720 B + 0.169879 B^2 
#> D :  1 + B + B^2 + B^3 + B^4 + B^5 + B^6 + B^7 + B^8 + B^9 + B^10 + B^11 
#> MA :  1 + 1.245052 B + 0.658623 B^2 + 0.593270 B^3 + 0.481574 B^4 + 0.366624 B^5 + 0.304938 B^6 + 0.184553 B^7 + 0.190108 B^8 + 0.095090 B^9 + 0.221559 B^10 + 0.186281 B^11 - 0.207005 B^12 - 0.348481 B^13 
#> Innovation variance:  0.1464012 
#> 
#> Irregular
#> Innovation variance:  0.3257068 
#> 
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s           i
#> Jan 2020 101.0 102.72726 103.1221  -1.7272634  -0.3948220
#> Feb 2020 100.1 102.95124 103.1797  -2.8512352  -0.2284534
#> Mar 2020  91.8  82.31999 103.3030   9.4800115 -20.9830366
#> Apr 2020  66.7  66.85029 103.5340  -0.1502858 -36.6836970
#> May 2020  73.7  79.46771 103.9124  -5.7677083 -24.4446419
#> Jun 2020  98.2  87.82311 104.2371  10.3768872 -16.4139594
#> Jul 2020  97.4  92.74114 104.3260   4.6588650 -11.5848433
#> Aug 2020  71.7  97.04194 104.1300 -25.3419376  -7.0880934
#> Sep 2020 104.7  97.32774 103.6918   7.3722629  -6.3640867
#> Oct 2020 106.7  98.66536 103.2317   8.0346351  -4.5663227
#> Nov 2020 101.6 100.05441 102.8519   1.5455901  -2.7974884
#> Dec 2020  96.6  99.35191 102.5735  -2.7519144  -3.2215659
#> 
#> Forecasts:
#>                y_f     sa_f      t_f        s_f         i_f
#> Jan 2021  94.55690 101.0346 102.4680  -6.477689 -1.43341231
#> Feb 2021  97.86506 101.4506 102.4540  -3.585540 -1.00338862
#> Mar 2021 113.01303 101.7376 102.4400  11.275402 -0.70237203
#> Apr 2021 103.19842 101.9344 102.4260   1.264068 -0.49166042
#> May 2021  96.00309 102.0679 102.4120  -6.064764 -0.34416230
#> Jun 2021 112.77599 102.1571 102.3980  10.618882 -0.24091361
#> Jul 2021 104.03135 102.2154 102.3840   1.815959 -0.16863953
#> Aug 2021  79.09787 102.2520 102.3700 -23.154116 -0.11804767
#> Sep 2021 109.04546 102.2734 102.3560   6.772048 -0.08263337
#> Oct 2021 108.59337 102.2842 102.3421   6.309157 -0.05784336
#> Nov 2021 106.47776 102.2876 102.3281   4.190193 -0.04049035
#> Dec 2021  99.77303 102.2857 102.3141  -2.512692 -0.02834325
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         1.887
#>  Seasonal     58.928
#>  Irregular     0.509
#>  TD & Hol.     2.598
#>  Others       33.908
#>  Total        97.830
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.064
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          1.000
#>  qs test on i                           1.000
#>  f-test on sa (seasonal dummies)        1.000
#>  f-test on i (seasonal dummies)         1.000
#>  Residual seasonality (entire series)   1.000
#>  Residual seasonality (last 3 years)    0.968
#>  f-test on sa (td)                      0.984
#>  f-test on i (td)                       1.000
#> 
#> 
#> Additional output variables
#> 
#> 
# }
```
