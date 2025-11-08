# Saving and loading a model specification, SA and pre-adjustment in X13 and TRAMO-SEATS

`save_spec` saves a SA or RegARIMA model specification. `load_spec`
loads the previously saved model specification.

## Usage

``` r
save_spec(object, file = file.path(tempdir(), "spec.RData"))

load_spec(file = "spec.RData")
```

## Arguments

- object:

  an object of one of the following classes: `c("SA_spec","X13")`,
  `c("SA_spec","TRAMO_SEATS")`, `c("SA","X13")`,
  `c("SA","TRAMO_SEATS")`, `c("regarima_spec","X13")`,
  `c("regarima_spec","TRAMO_SEATS")`, `c("regarima","X13")`,
  `c("regarima","TRAMO_SEATS")`.

- file:

  the (path and) name of the file where the model specification will
  be/has been saved.

## Value

`load_spec` returns an object of class `"SA_spec"` or `"regarima_spec"`.

## Details

`save_spec` saves the final model specification of a `"SA_spec"`,
`"SA"`, `"regarima_spec"` or `"regarima"` class object. `load_spec`
loads the previously saved model specification. It creates a
`c("SA_spec","X13")`, `c("sA_spec","TRAMO_SEATS")`,
`c("regarima_spec","X13")` or `c("regarima_spec","TRAMO_SEATS")` class
object, in line with the class of the previously saved model
specification.

## References

More information and examples related to 'JDemetra+' features in the
online documentation: <https://jdemetra-new-documentation.netlify.app/>

## Examples

``` r
# \donttest{
myseries <- ipi_c_eu[, "FR"]
myreg1 <- regarima_x13(myseries, spec = "RG5c")
myspec2 <- regarima_spec_x13(myreg1, estimate.from = "2005-10-01", outlier.from = "2010-03-01")
myreg2 <- regarima(myseries, myspec2)

myreg3 <- regarima_tramoseats(myseries, spec = "TRfull")
myspec4 <-regarima_spec_tramoseats(myreg3, tradingdays.mauto = "Unused",
                                  tradingdays.option ="WorkingDays",
                                  easter.type = "Standard",
                                  automdl.enabled = FALSE, arima.mu = TRUE)
myreg4 <-regarima(myseries, myspec4)

myspec6 <- x13_spec("RSA5c")
mysa6 <- x13(myseries, myspec6)

myspec7 <- tramoseats_spec("RSAfull")
mysa7 <- tramoseats(myseries, myspec7)

dir <- tempdir()

 # To save the model specification of a c("regarima_spec","X13") class object
save_spec(myspec2, file.path(dir, "specx13.RData"))
 # To save the model specification of a c("regarima","X13") class object
save_spec(myreg2, file.path(dir,"regx13.RData"))
 # To save the model specification of a c("regarima_spec","TRAMO_SEATS") class object
save_spec(myspec4, file.path(dir,"specTS.RData"))
 # To save the model specification of a c("regarima","TRAMO_SEATS") class object
save_spec(myreg4, file.path(dir,"regTS.RData"))
 # To save the model of a c("SA_spec","X13") class object
save_spec(myspec6, file.path(dir,"specFullx13.RData"))
 # To save the model of a c("SA","X13") class object
save_spec(mysa6, file.path(dir,"sax13.RData"))
 # To save the model of a c("SA_spec","TRAMO_SEATS") class object
save_spec(myspec7, file.path(dir,"specFullTS.RData"))
 # To save the model of a c("SA","TRAMO_SEATS") class object
save_spec(mysa7, file.path(dir,"saTS.RData"))

 # To load a model specification:
myspec2a <- load_spec(file.path(dir,"specx13.RData"))
myspec2b <- load_spec(file.path(dir,"regx13.RData"))
myspec4a <- load_spec(file.path(dir,"specTS.RData"))
myspec4b <- load_spec(file.path(dir,"regTS.RData"))
myspec6a <- load_spec(file.path(dir,"specFullx13.RData"))
myspec6b <- load_spec(file.path(dir,"sax13.RData"))
myspec7a <- load_spec(file.path(dir,"specFullTS.RData"))
myspec7b <- load_spec(file.path(dir,"saTS.RData"))

# To use the re-loaded specifications and models:
regarima(myseries, myspec2a)
#> y = regression model + arima (0, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Theta(1)   -0.2211      0.077
#> BTheta(1)  -0.6911      0.060
#> 
#>              Estimate Std. Error
#> Monday        1.32698      0.340
#> Tuesday       1.10991      0.346
#> Wednesday     0.68412      0.351
#> Thursday      0.04219      0.348
#> Friday        1.43827      0.348
#> Saturday     -1.99253      0.345
#> Leap year     2.01847      1.152
#> Easter [8]   -2.11412      0.702
#> LS (3-2020) -21.59400      2.876
#> AO (4-2020) -16.22087      2.287
#> AO (5-2011)  13.50260      2.048
#> 
#> 
#> Residual standard error: 2.656 on 156 degrees of freedom
#> Log likelihood = -411.2, aic = 850.3 aicc = 853.1, bic(corrected for length) = 2.346
#> 
x13(myseries, myspec6a)
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>             Estimate Std. Error
#> Phi(1)     0.0003269      0.108
#> Phi(2)     0.1688192      0.074
#> Theta(1)  -0.5485606      0.102
#> BTheta(1) -0.6660849      0.042
#> 
#>               Estimate Std. Error
#> Monday         0.55932      0.228
#> Tuesday        0.88221      0.228
#> Wednesday      1.03996      0.229
#> Thursday       0.04943      0.229
#> Friday         0.91132      0.230
#> Saturday      -1.57769      0.228
#> Leap year      2.15403      0.705
#> Easter [1]    -2.37950      0.454
#> TC (4-2020)  -35.59245      2.173
#> AO (3-2020)  -20.89026      2.180
#> AO (5-2011)   13.49850      1.857
#> LS (11-2008) -12.54901      1.636
#> 
#> 
#> Residual standard error: 2.218 on 342 degrees of freedom
#> Log likelihood = -799.1, aic =  1632 aicc =  1634, bic(corrected for length) = 1.855
#> 
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.163
#> M(2)    0.089
#> M(3)    1.181
#> M(4)    0.558
#> M(5)    1.020
#> M(6)    0.090
#> M(7)    0.083
#> M(8)    0.244
#> M(9)    0.062
#> M(10)   0.272
#> M(11)   0.256
#> Q       0.368
#> Q-M2    0.402
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t            s             i
#> Jan 2020 101.0 102.95613 102.9586  -1.95613209  -0.002494203
#> Feb 2020 100.1 103.50876 102.9592  -3.40875640   0.549602816
#> Mar 2020  91.8  82.87617 103.1664   8.92382800 -20.290271773
#> Apr 2020  66.7  66.65243 103.5971   0.04756625 -36.944710027
#> May 2020  73.7  78.87836 104.0393  -5.17835604 -25.160905985
#> Jun 2020  98.2  87.34544 104.3804  10.85456021 -17.034985133
#> Jul 2020  97.4  92.47436 104.5319   4.92563707 -12.057551871
#> Aug 2020  71.7  97.47245 104.3751 -25.77244698  -6.902636199
#> Sep 2020 104.7  97.37717 103.9182   7.32282919  -6.541070626
#> Oct 2020 106.7  98.24194 103.3047   8.45805540  -5.062719500
#> Nov 2020 101.6 100.26862 102.7746   1.33138152  -2.506014899
#> Dec 2020  96.6  99.66730 102.5133  -3.06729670  -2.845961796
#> 
#> Forecasts:
#>                y_f     sa_f      t_f          s_f        i_f
#> Jan 2021  94.53021 101.0902 102.4794  -6.56002888 -1.3891608
#> Feb 2021  97.90024 101.7395 102.5246  -3.83928384 -0.7850772
#> Mar 2021 114.09983 102.3065 102.5087  11.79328397 -0.2021598
#> Apr 2021 102.16781 102.2220 102.3759  -0.05422341 -0.1538967
#> May 2021  96.01612 101.5450 102.2100  -5.52888123 -0.6650098
#> Jun 2021 112.76658 101.3438 102.0725  11.42275939 -0.7286526
#> Jul 2021 104.13805 101.6681 102.0297   2.46989932 -0.3615193
#> Aug 2021  79.13003 102.3617 102.1360 -23.23171595  0.2257112
#> Sep 2021 109.06438 102.4772 102.3249   6.58713572  0.1523168
#> Oct 2021 108.64207 102.1329 102.5185   6.50921416 -0.3856588
#> Nov 2021 106.46022 102.5908 102.6996   3.86943752 -0.1088338
#> Dec 2021  99.79901 103.0831 102.8580  -3.28410831  0.2251086
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         2.251
#>  Seasonal     59.750
#>  Irregular     1.067
#>  TD & Hol.     2.610
#>  Others       33.718
#>  Total        99.395
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.034
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          0.985
#>  qs test on i                           0.865
#>  f-test on sa (seasonal dummies)        0.958
#>  f-test on i (seasonal dummies)         0.893
#>  Residual seasonality (entire series)   0.876
#>  Residual seasonality (last 3 years)    0.906
#>  f-test on sa (td)                      0.987
#>  f-test on i (td)                       0.993
#> 
#> 
#> Additional output variables
tramoseats(myseries, myspec7a)
#> RegARIMA
#> y = regression model + arima (2, 1, 0, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)      0.4032      0.051
#> Phi(2)      0.2883      0.051
#> BTheta(1)  -0.6641      0.042
#> 
#>             Estimate Std. Error
#> Week days     0.6994      0.032
#> Leap year     2.3231      0.690
#> Easter [6]   -2.5154      0.436
#> AO (5-2011)  13.4679      1.787
#> TC (4-2020) -22.2128      2.205
#> TC (3-2020) -21.0391      2.217
#> AO (5-2000)   6.7386      1.794
#> 
#> 
#> Residual standard error: 2.326 on 348 degrees of freedom
#> Log likelihood = -816.1, aic =  1654 aicc =  1655, bic(corrected for length) = 1.852
#> 
#> 
#> 
#> Decomposition
#> Model
#> AR :  1 + 0.403230 B + 0.288342 B^2 
#> D :  1 - B - B^12 + B^13 
#> MA :  1 - 0.664088 B^12 
#> 
#> 
#> SA
#> AR :  1 + 0.403230 B + 0.288342 B^2 
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 0.970348 B + 0.005940 B^2 - 0.005813 B^3 + 0.003576 B^4 
#> Innovation variance:  0.7043507 
#> 
#> Trend
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 + 0.033519 B - 0.966481 B^2 
#> Innovation variance:  0.06093642 
#> 
#> Seasonal
#> D :  1 + B + B^2 + B^3 + B^4 + B^5 + B^6 + B^7 + B^8 + B^9 + B^10 + B^11 
#> MA :  1 + 1.328957 B + 1.105787 B^2 + 1.185470 B^3 + 1.067845 B^4 + 0.820748 B^5 + 0.632456 B^6 + 0.404457 B^7 + 0.245256 B^8 + 0.001615 B^9 - 0.055617 B^10 - 0.203557 B^11 
#> Innovation variance:  0.04290744 
#> 
#> Transitory
#> AR :  1 + 0.403230 B + 0.288342 B^2 
#> MA :  1 - 0.260079 B - 0.739921 B^2 
#> Innovation variance:  0.05287028 
#> 
#> Irregular
#> Innovation variance:  0.2032994 
#> 
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s            i
#> Jan 2020 101.0 102.93775 103.0182  -1.9377453  -0.08043801
#> Feb 2020 100.1 103.53944 103.2312  -3.4394383   0.30818847
#> Mar 2020  91.8  82.47698 103.4998   9.3230241 -21.02286361
#> Apr 2020  66.7  65.77310 103.9608   0.9268969 -38.18766871
#> May 2020  73.7  79.43342 104.7269  -5.7334221 -25.29345247
#> Jun 2020  98.2  88.07766 105.3319  10.1223443 -17.25422206
#> Jul 2020  97.4  92.71048 105.4216   4.6895154 -12.71111705
#> Aug 2020  71.7  97.32129 104.9801 -25.6212858  -7.65880696
#> Sep 2020 104.7  97.44274 104.0807   7.2572622  -6.63793072
#> Oct 2020 106.7  98.20925 103.1711   8.4907485  -4.96183772
#> Nov 2020 101.6  99.98044 102.4813   1.6195550  -2.50088282
#> Dec 2020  96.6  98.99458 101.9735  -2.3945790  -2.97892307
#> 
#> Forecasts:
#>                y_f     sa_f      t_f        s_f         i_f
#> Jan 2021  93.22264 100.1984 101.7578  -6.975740 -1.55946363
#> Feb 2021  96.81455 100.8845 101.7113  -4.069924 -0.82679910
#> Mar 2021 111.72198 100.8668 101.6647  10.855228 -0.79795880
#> Apr 2021 102.76178 101.0716 101.6181   1.690178 -0.54654378
#> May 2021  95.52744 101.2474 101.5716  -5.719910 -0.32422597
#> Jun 2021 111.44221 101.2711 101.5250  10.171157 -0.25395653
#> Jul 2021 103.57813 101.2947 101.4784   2.283395 -0.18370915
#> Aug 2021  78.21363 101.3135 101.4319 -23.099833 -0.11841662
#> Sep 2021 108.57631 101.3000 101.3853   7.276282 -0.08528380
#> Oct 2021 107.32040 101.2771 101.3387   6.043321 -0.06166933
#> Nov 2021 105.33458 101.2505 101.2922   4.084088 -0.04168414
#> Dec 2021  98.79675 101.2164 101.2456  -2.419656 -0.02920922
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         6.087
#>  Seasonal     80.528
#>  Irregular     0.965
#>  TD & Hol.     3.590
#>  Others        8.102
#>  Total        99.271
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                       0.00
#>    Test for the presence of seasonality assuming stability    0.00
#>    Evolutive seasonality test                                 0.01
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
#>  Residual seasonality (last 3 years)    0.974
#>  f-test on sa (td)                      0.152
#>  f-test on i (td)                       0.224
#> 
#> 
#> Additional output variables

regarima(myseries, myspec4a)
#> y = regression model + arima (0, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Theta(1)   -0.6221      0.043
#> BTheta(1)  -0.6720      0.042
#> 
#>                Estimate Std. Error
#> Mean           0.001332      0.016
#> Monday         0.577428      0.239
#> Tuesday        0.842975      0.238
#> Wednesday      1.073966      0.240
#> Thursday       0.030442      0.239
#> Friday         0.872297      0.241
#> Saturday      -1.555483      0.238
#> Leap year      2.136324      0.726
#> Easter [6]    -2.170391      0.484
#> TC (4-2020)  -21.181047      2.222
#> TC (3-2020)  -21.228566      2.217
#> AO (5-2011)   12.919433      1.907
#> LS (11-2008) -12.465765      1.648
#> 
#> 
#> Residual standard error: 2.243 on 343 degrees of freedom
#> Log likelihood = -803.2, aic =  1638 aicc =  1640, bic(corrected for length) = 1.861
#> 
x13(myseries, myspec6b)
#> RegARIMA
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>             Estimate Std. Error
#> Phi(1)     0.0003269      0.108
#> Phi(2)     0.1688192      0.074
#> Theta(1)  -0.5485606      0.102
#> BTheta(1) -0.6660849      0.042
#> 
#>               Estimate Std. Error
#> Monday         0.55932      0.228
#> Tuesday        0.88221      0.228
#> Wednesday      1.03996      0.229
#> Thursday       0.04943      0.229
#> Friday         0.91132      0.230
#> Saturday      -1.57769      0.228
#> Leap year      2.15403      0.705
#> Easter [1]    -2.37950      0.454
#> TC (4-2020)  -35.59245      2.173
#> AO (3-2020)  -20.89026      2.180
#> AO (5-2011)   13.49850      1.857
#> LS (11-2008) -12.54901      1.636
#> 
#> 
#> Residual standard error: 2.218 on 342 degrees of freedom
#> Log likelihood = -799.1, aic =  1632 aicc =  1634, bic(corrected for length) = 1.855
#> 
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.163
#> M(2)    0.089
#> M(3)    1.181
#> M(4)    0.558
#> M(5)    1.020
#> M(6)    0.090
#> M(7)    0.083
#> M(8)    0.244
#> M(9)    0.062
#> M(10)   0.272
#> M(11)   0.256
#> Q       0.368
#> Q-M2    0.402
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t            s             i
#> Jan 2020 101.0 102.95613 102.9586  -1.95613209  -0.002494203
#> Feb 2020 100.1 103.50876 102.9592  -3.40875640   0.549602816
#> Mar 2020  91.8  82.87617 103.1664   8.92382800 -20.290271773
#> Apr 2020  66.7  66.65243 103.5971   0.04756625 -36.944710027
#> May 2020  73.7  78.87836 104.0393  -5.17835604 -25.160905985
#> Jun 2020  98.2  87.34544 104.3804  10.85456021 -17.034985133
#> Jul 2020  97.4  92.47436 104.5319   4.92563707 -12.057551871
#> Aug 2020  71.7  97.47245 104.3751 -25.77244698  -6.902636199
#> Sep 2020 104.7  97.37717 103.9182   7.32282919  -6.541070626
#> Oct 2020 106.7  98.24194 103.3047   8.45805540  -5.062719500
#> Nov 2020 101.6 100.26862 102.7746   1.33138152  -2.506014899
#> Dec 2020  96.6  99.66730 102.5133  -3.06729670  -2.845961796
#> 
#> Forecasts:
#>                y_f     sa_f      t_f          s_f        i_f
#> Jan 2021  94.53021 101.0902 102.4794  -6.56002888 -1.3891608
#> Feb 2021  97.90024 101.7395 102.5246  -3.83928384 -0.7850772
#> Mar 2021 114.09983 102.3065 102.5087  11.79328397 -0.2021598
#> Apr 2021 102.16781 102.2220 102.3759  -0.05422341 -0.1538967
#> May 2021  96.01612 101.5450 102.2100  -5.52888123 -0.6650098
#> Jun 2021 112.76658 101.3438 102.0725  11.42275939 -0.7286526
#> Jul 2021 104.13805 101.6681 102.0297   2.46989932 -0.3615193
#> Aug 2021  79.13003 102.3617 102.1360 -23.23171595  0.2257112
#> Sep 2021 109.06438 102.4772 102.3249   6.58713572  0.1523168
#> Oct 2021 108.64207 102.1329 102.5185   6.50921416 -0.3856588
#> Nov 2021 106.46022 102.5908 102.6996   3.86943752 -0.1088338
#> Dec 2021  99.79901 103.0831 102.8580  -3.28410831  0.2251086
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         2.251
#>  Seasonal     59.750
#>  Irregular     1.067
#>  TD & Hol.     2.610
#>  Others       33.718
#>  Total        99.395
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.034
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          0.985
#>  qs test on i                           0.865
#>  f-test on sa (seasonal dummies)        0.958
#>  f-test on i (seasonal dummies)         0.893
#>  Residual seasonality (entire series)   0.876
#>  Residual seasonality (last 3 years)    0.906
#>  f-test on sa (td)                      0.987
#>  f-test on i (td)                       0.993
#> 
#> 
#> Additional output variables
tramoseats(myseries, myspec7b)
#> RegARIMA
#> y = regression model + arima (2, 1, 0, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)      0.4032      0.051
#> Phi(2)      0.2883      0.051
#> BTheta(1)  -0.6641      0.042
#> 
#>             Estimate Std. Error
#> Week days     0.6994      0.032
#> Leap year     2.3231      0.690
#> Easter [6]   -2.5154      0.436
#> AO (5-2011)  13.4679      1.787
#> TC (4-2020) -22.2128      2.205
#> TC (3-2020) -21.0391      2.217
#> AO (5-2000)   6.7386      1.794
#> 
#> 
#> Residual standard error: 2.326 on 348 degrees of freedom
#> Log likelihood = -816.1, aic =  1654 aicc =  1655, bic(corrected for length) = 1.852
#> 
#> 
#> 
#> Decomposition
#> Model
#> AR :  1 + 0.403230 B + 0.288342 B^2 
#> D :  1 - B - B^12 + B^13 
#> MA :  1 - 0.664088 B^12 
#> 
#> 
#> SA
#> AR :  1 + 0.403230 B + 0.288342 B^2 
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 0.970348 B + 0.005940 B^2 - 0.005813 B^3 + 0.003576 B^4 
#> Innovation variance:  0.7043507 
#> 
#> Trend
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 + 0.033519 B - 0.966481 B^2 
#> Innovation variance:  0.06093642 
#> 
#> Seasonal
#> D :  1 + B + B^2 + B^3 + B^4 + B^5 + B^6 + B^7 + B^8 + B^9 + B^10 + B^11 
#> MA :  1 + 1.328957 B + 1.105787 B^2 + 1.185470 B^3 + 1.067845 B^4 + 0.820748 B^5 + 0.632456 B^6 + 0.404457 B^7 + 0.245256 B^8 + 0.001615 B^9 - 0.055617 B^10 - 0.203557 B^11 
#> Innovation variance:  0.04290744 
#> 
#> Transitory
#> AR :  1 + 0.403230 B + 0.288342 B^2 
#> MA :  1 - 0.260079 B - 0.739921 B^2 
#> Innovation variance:  0.05287028 
#> 
#> Irregular
#> Innovation variance:  0.2032994 
#> 
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s            i
#> Jan 2020 101.0 102.93775 103.0182  -1.9377453  -0.08043801
#> Feb 2020 100.1 103.53944 103.2312  -3.4394383   0.30818847
#> Mar 2020  91.8  82.47698 103.4998   9.3230241 -21.02286361
#> Apr 2020  66.7  65.77310 103.9608   0.9268969 -38.18766871
#> May 2020  73.7  79.43342 104.7269  -5.7334221 -25.29345247
#> Jun 2020  98.2  88.07766 105.3319  10.1223443 -17.25422206
#> Jul 2020  97.4  92.71048 105.4216   4.6895154 -12.71111705
#> Aug 2020  71.7  97.32129 104.9801 -25.6212858  -7.65880696
#> Sep 2020 104.7  97.44274 104.0807   7.2572622  -6.63793072
#> Oct 2020 106.7  98.20925 103.1711   8.4907485  -4.96183772
#> Nov 2020 101.6  99.98044 102.4813   1.6195550  -2.50088282
#> Dec 2020  96.6  98.99458 101.9735  -2.3945790  -2.97892307
#> 
#> Forecasts:
#>                y_f     sa_f      t_f        s_f         i_f
#> Jan 2021  93.22264 100.1984 101.7578  -6.975740 -1.55946363
#> Feb 2021  96.81455 100.8845 101.7113  -4.069924 -0.82679910
#> Mar 2021 111.72198 100.8668 101.6647  10.855228 -0.79795880
#> Apr 2021 102.76178 101.0716 101.6181   1.690178 -0.54654378
#> May 2021  95.52744 101.2474 101.5716  -5.719910 -0.32422597
#> Jun 2021 111.44221 101.2711 101.5250  10.171157 -0.25395653
#> Jul 2021 103.57813 101.2947 101.4784   2.283395 -0.18370915
#> Aug 2021  78.21363 101.3135 101.4319 -23.099833 -0.11841662
#> Sep 2021 108.57631 101.3000 101.3853   7.276282 -0.08528380
#> Oct 2021 107.32040 101.2771 101.3387   6.043321 -0.06166933
#> Nov 2021 105.33458 101.2505 101.2922   4.084088 -0.04168414
#> Dec 2021  98.79675 101.2164 101.2456  -2.419656 -0.02920922
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         6.087
#>  Seasonal     80.528
#>  Irregular     0.965
#>  TD & Hol.     3.590
#>  Others        8.102
#>  Total        99.271
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                       0.00
#>    Test for the presence of seasonality assuming stability    0.00
#>    Evolutive seasonality test                                 0.01
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
#>  Residual seasonality (last 3 years)    0.974
#>  f-test on sa (td)                      0.152
#>  f-test on i (td)                       0.224
#> 
#> 
#> Additional output variables
# }
```
