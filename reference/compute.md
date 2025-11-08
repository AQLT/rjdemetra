# Compute a workspace multi-processing(s)

Function to compute all the multiprocessings or only a given one from a
workspace. By default, the workspace only contains definitions:
computation is needed to recalculate and access the adjusted model (with
[`get_model`](get_model.md)).

## Usage

``` r
compute(workspace, i)
```

## Arguments

- workspace:

  the workspace to compute.

- i:

  a `character` or `numeric` indicating the name or the index of the
  multiprocessing to compute. By default, all multiprocessings are
  computed.

## See also

[`get_model`](get_model.md)

## Examples

``` r
# \donttest{
spec_x13 <- x13_spec(spec = "RSA5c", easter.enabled = FALSE)
sa_x13 <- x13(ipi_c_eu[, "FR"], spec = spec_x13)

wk <- new_workspace()
mp <- new_multiprocessing(wk, "sap1")
add_sa_item(wk, "sap1", sa_x13, "X13")
sa_item1 <- get_object(mp, 1)

get_model(sa_item1, wk) # Returns NULL
#> Warning: The result of the object is NULL: have you computed the workspace after importing it?
#> See ?compute for more information.
#> NULL

compute(wk)

get_model(sa_item1, wk) # Returns the SA model sa_x13
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
# }

```
