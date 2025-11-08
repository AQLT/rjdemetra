# RegARIMA model specification: the pre-adjustment in X13

Function to create (and/or modify) a `c("regarima_spec","X13")` class
object with the RegARIMA model specification for the X13 method. The
object can be created from a predefined 'JDemetra+' model specification
(a `character`), a previous specification (`c("regarima_spec","X13")`
object) or a X13 RegARIMA model (`c("regarima","X13")`).

## Usage

``` r
regarima_spec_x13(
  spec = c("RG5c", "RG0", "RG1", "RG2c", "RG3", "RG4c"),
  preliminary.check = NA,
  estimate.from = NA_character_,
  estimate.to = NA_character_,
  estimate.first = NA_integer_,
  estimate.last = NA_integer_,
  estimate.exclFirst = NA_integer_,
  estimate.exclLast = NA_integer_,
  estimate.tol = NA_integer_,
  transform.function = c(NA, "Auto", "None", "Log"),
  transform.adjust = c(NA, "None", "LeapYear", "LengthOfPeriod"),
  transform.aicdiff = NA_integer_,
  usrdef.outliersEnabled = NA,
  usrdef.outliersType = NA,
  usrdef.outliersDate = NA,
  usrdef.outliersCoef = NA,
  usrdef.varEnabled = NA,
  usrdef.var = NA,
  usrdef.varType = NA,
  usrdef.varCoef = NA,
  tradingdays.option = c(NA, "TradingDays", "WorkingDays", "UserDefined", "None"),
  tradingdays.autoadjust = NA,
  tradingdays.leapyear = c(NA, "LeapYear", "LengthOfPeriod", "None"),
  tradingdays.stocktd = NA_integer_,
  tradingdays.test = c(NA, "Remove", "Add", "None"),
  easter.enabled = NA,
  easter.julian = NA,
  easter.duration = NA_integer_,
  easter.test = c(NA, "Add", "Remove", "None"),
  outlier.enabled = NA,
  outlier.from = NA_character_,
  outlier.to = NA_character_,
  outlier.first = NA_integer_,
  outlier.last = NA_integer_,
  outlier.exclFirst = NA_integer_,
  outlier.exclLast = NA_integer_,
  outlier.ao = NA,
  outlier.tc = NA,
  outlier.ls = NA,
  outlier.so = NA,
  outlier.usedefcv = NA,
  outlier.cv = NA_integer_,
  outlier.method = c(NA, "AddOne", "AddAll"),
  outlier.tcrate = NA_integer_,
  automdl.enabled = NA,
  automdl.acceptdefault = NA,
  automdl.cancel = NA_integer_,
  automdl.ub1 = NA_integer_,
  automdl.ub2 = NA_integer_,
  automdl.mixed = NA,
  automdl.balanced = NA,
  automdl.armalimit = NA_integer_,
  automdl.reducecv = NA_integer_,
  automdl.ljungboxlimit = NA_integer_,
  automdl.ubfinal = NA_integer_,
  arima.mu = NA,
  arima.p = NA_integer_,
  arima.d = NA_integer_,
  arima.q = NA_integer_,
  arima.bp = NA_integer_,
  arima.bd = NA_integer_,
  arima.bq = NA_integer_,
  arima.coefEnabled = NA,
  arima.coef = NA,
  arima.coefType = NA,
  fcst.horizon = NA_integer_
)
```

## Arguments

- spec:

  the model specification. It can be the name (`character`) of a
  pre-defined 'JDemetra+' model specification (see *Details*), an object
  of class `c("regarima_spec","X13")` or an object of class
  `c("regarima", "X13")`. The default value is `"RG5c"`.

- preliminary.check:

  a Boolean to check the quality of the input series and exclude highly
  problematic ones (e.g. the series with a number of identical
  observations and/or missing values above pre-specified threshold
  values).

  The time span of the series, which is the (sub)period used to estimate
  the regarima model, is controlled by the following six variables:
  `estimate.from, estimate.to, estimate.first, estimate.last, estimate.exclFirst`
  and `estimate.exclLast`; where `estimate.from` and `estimate.to` have
  priority over the remaining span control variables, `estimate.last`
  and `estimate.first` have priority over `estimate.exclFirst` and
  `estimate.exclLast`, and `estimate.last` has priority over
  `estimate.first`. Default= "All".

- estimate.from:

  a character in format "YYYY-MM-DD" indicating the start of the time
  span (e.g. "1900-01-01"). It can be combined with the parameter
  `estimate.to`.

- estimate.to:

  a character in format "YYYY-MM-DD" indicating the end of the time span
  (e.g. "2020-12-31"). It can be combined with the parameter
  `estimate.from`.

- estimate.first:

  a numeric specifying the number of periods considered at the beginning
  of the series.

- estimate.last:

  numeric specifying the number of periods considered at the end of the
  series.

- estimate.exclFirst:

  a numeric specifying the number of periods excluded at the beginning
  of the series. It can be combined with the parameter
  `estimate.exclLast`.

- estimate.exclLast:

  a numeric specifying the number of periods excluded at the end of the
  series. It can be combined with the parameter `estimate.exclFirst`.

- estimate.tol:

  a numeric, convergence tolerance. The absolute changes in the
  log-likelihood function are compared to this value to check for the
  convergence of the estimation iterations.

- transform.function:

  the transformation of the input series: `"None"` = no transformation
  of the series; `"Log"` = takes the log of the series; `"Auto"` = the
  program tests for the log-level specification.

- transform.adjust:

  pre-adjustment of the input series for the length of period or leap
  year effects: `"None"` = no adjustment; `"LeapYear"` = leap year
  effect; `"LengthOfPeriod"` = length of period. Modifications of this
  variable are taken into account only when `transform.function` is set
  to `"Log"`.

- transform.aicdiff:

  a numeric defining the difference in AICC needed to accept no
  transformation when the automatic transformation selection is chosen
  (considered only when `transform.function` is set to `"Auto"`).

  Control variables for the pre-specified outliers. The pre-specified
  outliers are used in the model only when enabled
  (`usrdef.outliersEnabled=TRUE`) and the outlier type
  (`usrdef.outliersType`) and date (`usrdef.outliersDate`) are provided.

- usrdef.outliersEnabled:

  logical. If `TRUE`, the program uses the pre-specified outliers.

- usrdef.outliersType:

  a vector defining the outlier type. Possible types are: `("AO")` =
  additive, `("LS")` = level shift, `("TC")` = transitory change,
  `("SO")` = seasonal outlier. E.g.:
  `usrdef.outliersType = c("AO","AO","LS")`.

- usrdef.outliersDate:

  a vector defining the outlier dates. The dates should be characters in
  format "YYYY-MM-DD". E.g.:
  `usrdef.outliersDate= c("2009-10-01","2005-02-01","2003-04-01")`.

- usrdef.outliersCoef:

  a vector providing fixed coefficients for the outliers. The
  coefficients can't be fixed if `transform.function` is set to `"Auto"`
  i.e. the series transformation need to be pre-defined. E.g.:
  ` usrdef.outliersCoef=c(200,170,20)`.

  Control variables for the user-defined variables:

- usrdef.varEnabled:

  a logical. If `TRUE`, the program uses the user-defined variables.

- usrdef.var:

  a time series (`ts`) or a matrix of time series (`mts`) with the
  user-defined variables.

- usrdef.varType:

  a vector of character(s) defining the user-defined variables component
  type. Possible types are:
  `"Undefined", "Series", "Trend", "Seasonal", "SeasonallyAdjusted", "Irregular", "Calendar"`.
  The type `"Calendar"`must be used with
  `tradingdays.option = "UserDefined"` to use user-defined calendar
  regressors. If not specified, the program will assign the
  `"Undefined"` type.

- usrdef.varCoef:

  a vector providing fixed coefficients for the user-defined variables.
  The coefficients can't be fixed if `transform.function` is set to
  `"Auto"` i.e. the series transformation need to be pre-defined.

- tradingdays.option:

  to specify the set of trading days regression variables:
  `"TradingDays"` = six day-of-the-week regression variables;
  `"WorkingDays"` = one working/non-working day contrast variable;
  `"None"` = no correction for trading days and working days effects;
  `"UserDefined"` = user-defined trading days regressors (regressors
  must be defined by the `usrdef.var` argument with `usrdef.varType` set
  to `"Calendar"` and `usrdef.varEnabled = TRUE`). `"None"` must also be
  specified for the "day-of-week effects" correction
  (`tradingdays.stocktd` to be modified accordingly).

- tradingdays.autoadjust:

  a logical. If `TRUE`, the program corrects automatically for the leap
  year effect. Modifications of this variable are taken into account
  only when `transform.function` is set to `"Auto"`.

- tradingdays.leapyear:

  a `character` to specify whether or not to include the leap-year
  effect in the model: `"LeapYear"` = leap year effect;
  `"LengthOfPeriod"` = length of period, `"None"` = no effect included.
  The leap-year effect can be pre-specified in the model only if the
  input series hasn't been pre-adjusted (`transform.adjust` set to
  `"None"`) and if the automatic correction for the leap-year effect
  isn't selected (`tradingdays.autoadjust` set to `FALSE`).

- tradingdays.stocktd:

  a numeric indicating the day of the month when inventories and other
  stock are reported (to denote the last day of the month, set the
  variable to 31). Modifications of this variable are taken into account
  only when `tradingdays.option` is set to `"None"`.

- tradingdays.test:

  defines the pre-tests for the significance of the trading day
  regression variables based on the AICC statistics: `"Add"` = the
  trading day variables are not included in the initial regression model
  but can be added to the RegARIMA model after the test; `"Remove"` =
  the trading day variables belong to the initial regression model but
  can be removed from the RegARIMA model after the test; `"None"` = the
  trading day variables are not pre-tested and are included in the
  model.

- easter.enabled:

  a logical. If `TRUE`, the program considers the Easter effect in the
  model.

- easter.julian:

  a logical. If `TRUE`, the program uses the Julian Easter (expressed in
  Gregorian calendar).

- easter.duration:

  a numeric indicating the duration of the Easter effect (length in
  days, between 1 and 20).

- easter.test:

  defines the pre-tests for the significance of the Easter effect based
  on the t-statistic (the Easter effect is considered as significant if
  the t-statistic is greater than 1.96): `"Add"` = the Easter effect
  variable is not included in the initial regression model but can be
  added to the RegARIMA model after the test; `"Remove"` = the Easter
  effect variable belongs to the initial regression model but can be
  removed from the RegARIMA model after the test; `"None"` = the Easter
  effect variable is not pre-tested and is included in the model.

- outlier.enabled:

  a logical. If `TRUE`, the automatic detection of outliers is enabled
  in the defined time span.

  The time span during which outliers will be searched is controlled by
  the following six variables:
  `outlier.from, outlier.to, outlier.first, outlier.last, outlier.exclFirst`
  and `outlier.exclLast`; where `outlier.from` and `outlier.to` have
  priority over the remaining span control variables, `outlier.last` and
  `outlier.first` have priority over `outlier.exclFirst` and
  `outlier.exclLast`, and `outlier.last` has priority over
  `outlier.first`.

- outlier.from:

  a character in format "YYYY-MM-DD" indicating the start of the time
  span (e.g. "1900-01-01"). It can be combined with the parameter
  `outlier.to`.

- outlier.to:

  a character in format "YYYY-MM-DD" indicating the end of the time span
  (e.g. "2020-12-31"). it can be combined with the parameter
  `outlier.from`.

- outlier.first:

  a numeric specifying the number of periods considered at the beginning
  of the series.

- outlier.last:

  a numeric specifying the number of periods considered at the end of
  the series.

- outlier.exclFirst:

  a numeric specifying the number of periods excluded at the beginning
  of the series. It can be combined with the parameter
  `outlier.exclLast`.

- outlier.exclLast:

  a numeric specifying the number of periods excluded at the end of the
  series. It can be combined with the parameter `outlier.exclFirst`.

- outlier.ao:

  a logical. If `TRUE`, the automatic detection of additive outliers is
  enabled (`outlier.enabled` must be also set to `TRUE`).

- outlier.tc:

  a logical. If `TRUE`, the automatic detection of transitory changes is
  enabled (`outlier.enabled` must be also set to `TRUE`).

- outlier.ls:

  a logical. If `TRUE`, the automatic detection of level shifts is
  enabled (`outlier.enabled` must be also set to `TRUE`).

- outlier.so:

  a logical. If `TRUE`, the automatic detection of seasonal outliers is
  enabled (`outlier.enabled` must be also set to `TRUE`).

- outlier.usedefcv:

  a logical. If `TRUE`, the critical value for the outlier detection
  procedure is automatically determined by the number of observations in
  the outlier detection time span. If `FALSE`, the procedure uses the
  entered critical value (`outlier.cv`).

- outlier.cv:

  a numeric. The entered critical value for the outlier detection
  procedure. The modification of this variable is only taken into
  account when `outlier.usedefcv` is set to `FALSE`.

- outlier.method:

  determines how the program successively adds detected outliers to the
  model. At present, only the `AddOne` method is supported.

- outlier.tcrate:

  a numeric. The rate of decay for the transitory change outlier.

- automdl.enabled:

  a logical. If `TRUE`, the automatic modelling of the ARIMA model is
  enabled. If `FALSE`, the parameters of the ARIMA model can be
  specified.

  Control variables for the automatic modelling of the ARIMA model (when
  `automdl.enabled` is set to `TRUE`):

- automdl.acceptdefault:

  a logical. If `TRUE`, the default model (ARIMA(0,1,1)(0,1,1)) may be
  chosen in the first step of the automatic model identification. If the
  Ljung-Box Q statistics for the residuals is acceptable, the default
  model is accepted and no further attempt will be made to identify
  another model.

- automdl.cancel:

  the cancellation limit (`numeric`). If the difference in moduli of an
  AR and an MA roots (when estimating ARIMA(1,0,1)(1,0,1) models in the
  second step of the automatic identification of the differencing
  orders) is smaller than the cancellation limit, the two roots are
  assumed equal and cancel out.

- automdl.ub1:

  the first unit root limit (`numeric`). It is the threshold value for
  the initial unit root test in the automatic differencing procedure.
  When one of the roots in the estimation of the ARIMA(2,0,0)(1,0,0)
  plus mean model, performed in the first step of the automatic model
  identification procedure, is larger than the first unit root limit in
  modulus, it is set equal to unity.

- automdl.ub2:

  the second unit root limit (`numeric`). When one of the roots in the
  estimation of the ARIMA(1,0,1)(1,0,1) plus mean model, which is
  performed in the second step of the automatic model identification
  procedure, is larger than second unit root limit in modulus, it is
  checked if there is a common factor in the corresponding AR and MA
  polynomials of the ARMA model that can be canceled (see
  `automdl.cancel`). If there is no cancellation, the AR root is set
  equal to unity (i.e. the differencing order changes).

- automdl.mixed:

  a logical. This variable controls whether ARIMA models with
  non-seasonal AR and MA terms or seasonal AR and MA terms will be
  considered in the automatic model identification procedure. If
  `FALSE`, a model with AR and MA terms in both the seasonal and
  non-seasonal parts of the model can be acceptable, provided there are
  no AR or MA terms in either the seasonal or non-seasonal terms.

- automdl.balanced:

  a logical. If `TRUE`, the automatic model identification procedure
  will have a preference for balanced models (i.e. models for which the
  order of the combined AR and differencing operator is equal to the
  order of the combined MA operator).

- automdl.armalimit:

  the ARMA limit (`numeric`). It is the threshold value for t-statistics
  of ARMA coefficients and constant term used for the final test of
  model parsimony. If the highest order ARMA coefficient has a t-value
  smaller than this value in magnitude, the order of the model is
  reduced. If the constant term t-value is smaller than the ARMA limit
  in magnitude, it is removed from the set of regressors.

- automdl.reducecv:

  numeric, ReduceCV. The percentage by which the outlier's critical
  value will be reduced when an identified model is found to have a
  Ljung-Box statistic with an unacceptable confidence coefficient. The
  parameter should be between 0 and 1, and will only be active when
  automatic outlier identification is enabled. The reduced critical
  value will be set to (1-ReduceCV)\*CV, where CV is the original
  critical value.

- automdl.ljungboxlimit:

  the Ljung Box limit (`numeric`). Acceptance criterion for the
  confidence intervals of the Ljung-Box Q statistic. If the LjungBox Q
  statistics for the residuals of a final model is greater than the
  Ljung Box limit, then the model is rejected, the outlier critical
  value is reduced and model and outlier identification (if specified)
  is redone with a reduced value.

- automdl.ubfinal:

  numeric, final unit root limit. The threshold value for the final unit
  root test. If the magnitude of an AR root for the final model is
  smaller than the final unit root limit, then a unit root is assumed,
  the order of the AR polynomial is reduced by one and the appropriate
  order of the differencing (non-seasonal, seasonal) is increased. The
  parameter value should be greater than one.

  Control variables for the non-automatic modelling of the ARIMA model
  (when `automdl.enabled` is set to `FALSE`):

- arima.mu:

  logical. If `TRUE`, the mean is considered as part of the ARIMA model.

- arima.p:

  numeric. The order of the non-seasonal autoregressive (AR) polynomial.

- arima.d:

  numeric. The regular differencing order.

- arima.q:

  numeric. The order of the non-seasonal moving average (MA) polynomial.

- arima.bp:

  numeric. The order of the seasonal autoregressive (AR) polynomial.

- arima.bd:

  numeric. The seasonal differencing order.

- arima.bq:

  numeric. The order of the seasonal moving average (MA) polynomial.

  Control variables for the user-defined ARMA coefficients. Coefficients
  can be defined for the regular and seasonal autoregressive (AR)
  polynomials and moving average (MA) polynomials. The model considers
  the coefficients only if the procedure for their estimation
  (`arima.coefType`) is provided, and the number of provided
  coefficients matches the sum of (regular and seasonal) AR and MA
  orders (`p,q,bp,bq`).

- arima.coefEnabled:

  logical. If `TRUE`, the program uses the user-defined ARMA
  coefficients.

- arima.coef:

  a vector providing the coefficients for the regular and seasonal AR
  and MA polynomials. The vector length must be equal to the sum of the
  regular and seasonal AR and MA orders. The coefficients shall be
  provided in the following order: regular AR (*Phi*; `p` elements),
  regular MA (*Theta*; `q` elements), seasonal AR (*BPhi*; `bp`
  elements) and seasonal MA (*BTheta*; `bq` elements). E.g.:
  `arima.coef=c(0.6,0.7)` with `arima.p=1, arima.q=0,arima.bp=1` and
  `arima.bq=0`.

- arima.coefType:

  a vector defining the ARMA coefficients estimation procedure. Possible
  procedures are: `"Undefined"` = no use of any user-defined input (i.e.
  coefficients are estimated), `"Fixed"` = the coefficients are fixed at
  the value provided by the user, `"Initial"` = the value defined by the
  user is used as the initial condition. For orders for which the
  coefficients shall not be defined, the `arima.coef` can be set to `NA`
  or `0`, or the `arima.coefType` can be set to `"Undefined"`. E.g.:
  `arima.coef = c(-0.8,-0.6,NA)`,
  `arima.coefType = c("Fixed","Fixed","Undefined")`.

- fcst.horizon:

  the forecasting horizon (`numeric`). The forecast length generated by
  the RegARIMA model in periods (positive values) or years (negative
  values). By default, the program generates a two-year forecast
  (`fcst.horizon` set to `-2`).

## Value

A list of class `c("regarima_spec","X13")` with the following
components, each referring to a different part of the RegARIMA model
specification, mirroring the arguments of the function (for details, see
the arguments description). Each lowest-level component (except span,
pre-specified outliers, user-defined variables and pre-specified ARMA
coefficients) is structured within a data frame with columns denoting
different variables of the model specification and rows referring to:
first row = base specification, as provided within the argument `spec`;
second row = user modifications as specified by the remaining arguments
of the function (e.g.: `arima.d`); and third row = final model
specification, values that will be used in the function
[`regarima`](regarima.md). The final specification (third row) shall
include user modifications (row two) unless they were wrongly specified.
The pre-specified outliers, user-defined variables and pre-specified
ARMA coefficients consist of a list of `Predefined` (base model
specification) and `Final` values.

- estimate:

  a data frame. Variables referring to: `span` - time span for the model
  estimation, `tolerance` - argument `estimate.tol`. The final values
  can also be accessed with the function
  [`s_estimate`](specification.md).

- transform:

  a data frame. Variables referring to: `tfunction` - argument
  `transform.function`, `adjust` - argument `transform.adjust`,
  `aicdiff` - argument `transform.aicdiff`. The final values can also be
  accessed with the function [`s_transform`](specification.md).

- regression:

  a list containing the information on the user-defined variables
  (`userdef`), `trading.days` effect and `easter` effect. The
  user-defined part includes: `specification` - data frame with the
  information if pre-specified outliers (`outlier`) and user-defined
  variables (`variables`) are included in the model and if fixed
  coefficients are used (`outlier.coef` and `variables.coef`). The final
  values can also be accessed with the function
  [`s_usrdef`](specification.md); `outliers` - matrices with the
  outliers (`Predefined` and `Final`). The final outliers can also be
  accessed with the function [`s_preOut`](specification.md); and
  `variables` - a list with the `Predefined` and `Final` user-defined
  variables (`series`) and its description (`description`) including the
  information on the variable type and the values of fixed coefficients.
  The final user-defined variables can also be accessed with the
  function [`s_preVar`](specification.md). Within the data frame
  `trading.days`, the variables refer to: `option` - argument
  `tradingdays.option, autoadjust` - argument
  `tradingdays.autoadjust, leapyear` - argument
  `tradingdays.leapyear, stocktd` - argument
  `tradingdays.stocktd, test` - argument `tradingdays.test`. The final
  `trading.days` values can be also accessed with the function
  [`s_td`](specification.md). Within the data frame `easter` variables
  refer to: `enabled` - argument `easter.enabled, julian` - argument
  `easter.julian, duration` - argument `easter.duration, test` -
  argument `easter.test`. The final `easter` values can be also accessed
  with the function [`s_easter`](specification.md).

- outliers:

  a data frame. Variables referring to: `enabled` - argument
  `outlier.enabled`, `span` - time span for the outlier detection,
  `ao` - argument `outlier.ao, tc` - argument `outlier.tc, ls` -
  argument `outlier.ls, so` - argument `outlier.so, usedefcv` - argument
  `outlier.usedefcv, cv` - argument `outlier.cv, method` - argument
  `outlier.method, tcrate` - argument `outlier.tcrate`. The final values
  can also be accessed with the function [`s_out`](specification.md).

- arima:

  a list of a data frame with the ARIMA settings (`specification`) and
  matrices with the information on the pre-specified ARMA coefficients
  (`coefficients`). The matrix `Predefined` refers to the pre-defined
  model specification, and the matrix `Final` to the final
  specification. Both matrices contain the value of the ARMA
  coefficients and the procedure for its estimation. In the data frame
  `specification`, the variable `enabled` refers to the argument
  `automdl.enabled` and all remaining variables
  (`automdl.acceptdefault, automdl.cancel, automdl.ub1, automdl.ub2, automdl.mixed, automdl.balanced, automdl.armalimit, automdl.reducecv, automdl.ljungboxlimit, automdl.ubfinal, arima.mu, arima.p, arima.d, arima.q, arima.bp, arima.bd, arima.bq`),
  to the respective function arguments. The final values of the
  `specification` can be also accessed with the function
  [`s_arima`](specification.md) and the final pre-specified ARMA
  coefficients, with the function [`s_arimaCoef`](specification.md).

- forecast:

  a data frame with the forecast horizon (argument `fcst.horizon`). The
  final value can also be accessed with the function
  [`s_fcst`](specification.md).

- span:

  a matrix containing the final time span for the model estimation and
  outlier detection. It contains the same information as the variable
  span in the data frames estimate and outliers. The matrix can be also
  accessed with the function [`s_span`](specification.md).

## Details

The available predefined 'JDemetra+' model specifications are described
in the table below:

|                       |                            |                           |                         |                       |                       |             |
|-----------------------|----------------------------|---------------------------|-------------------------|-----------------------|-----------------------|-------------|
| **Identifier** \|     | **Log/level detection** \| | **Outliers detection** \| | **Calendar effects** \| | **ARIMA**             | RG0 \|                | *NA* \|     |
| *NA* \|               | *NA* \|                    | Airline(+mean)            | RG1 \|                  | automatic \|          | AO/LS/TC \|           | *NA* \|     |
| Airline(+mean)        | RG2c \|                    | automatic \|              | AO/LS/TC \|             | 2 td vars + Easter \| | Airline(+mean)        | RG3 \|      |
| automatic \|          | AO/LS/TC \|                | *NA* \|                   | automatic               | RG4c \|               | automatic \|          | AO/LS/TC \| |
| 2 td vars + Easter \| | automatic                  | RG5c \|                   | automatic \|            | AO/LS/TC \|           | 7 td vars + Easter \| | automatic   |

## References

More information and examples related to 'JDemetra+' features in the
online documentation: <https://jdemetra-new-documentation.netlify.app/>

## Examples

``` r
# \donttest{
myseries <- ipi_c_eu[, "FR"]
myspec1 <- regarima_spec_x13(spec = "RG5c")
myreg1 <- regarima(myseries, spec = myspec1)

 # To modify a pre-specified model specification
myspec2 <- regarima_spec_x13(spec = "RG5c",
                             tradingdays.option = "WorkingDays")
myreg2 <- regarima(myseries, spec = myspec2)

 # To modify the model specification of a "regarima" object
myspec3 <- regarima_spec_x13(myreg1, tradingdays.option = "WorkingDays")
myreg3 <- regarima(myseries, myspec3)

 # To modify the model specification of a "regarima_spec" object
myspec4 <- regarima_spec_x13(myspec1, tradingdays.option = "WorkingDays")
myreg4 <- regarima(myseries, myspec4)

 # Pre-specified outliers
myspec1 <- regarima_spec_x13(spec = "RG5c", usrdef.outliersEnabled = TRUE,
              usrdef.outliersType = c("LS", "AO"),
              usrdef.outliersDate = c("2008-10-01", "2002-01-01"),
              usrdef.outliersCoef = c(36, 14),
              transform.function = "None")

myreg1 <- regarima(myseries, myspec1)
myreg1
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     0.07859      0.114
#> Phi(2)     0.19792      0.076
#> Theta(1)  -0.48272      0.111
#> BTheta(1) -0.65916      0.043
#> 
#>               Estimate Std. Error
#> Monday         0.64094      0.228
#> Tuesday        0.81794      0.229
#> Wednesday      1.05374      0.229
#> Thursday       0.06981      0.228
#> Friday         0.93434      0.228
#> Saturday      -1.63686      0.226
#> Leap year      2.11550      0.697
#> Easter [1]    -2.38135      0.451
#> AO (9-2008)   31.95554      2.924
#> LS (9-2008)  -57.04093      2.657
#> TC (4-2020)  -35.62104      2.120
#> AO (3-2020)  -21.00931      2.145
#> AO (5-2011)   13.21877      1.832
#> TC (9-2008)   23.44654      4.001
#> TC (12-2001) -20.47521      2.922
#> AO (12-2001)  17.13461      2.962
#> TC (2-2002)   10.61731      1.937
#> 
#> Fixed outliers: 
#>              Coefficients
#> LS (10-2008)           36
#> AO (1-2002)            14
#> 
#> 
#> Residual standard error: 2.178 on 337 degrees of freedom
#> Log likelihood = -792.6, aic =  1629 aicc =  1632, bic(corrected for length) = 1.901
#> 
s_preOut(myreg1)
#>   type       date coeff
#> 1   LS 2008-10-01    36
#> 2   AO 2002-01-01    14


 # User-defined variables
var1 <- ts(rnorm(length(myseries))*10, start = start(myseries),
           frequency = 12)
var2 <- ts(rnorm(length(myseries))*100, start = start(myseries),
           frequency = 12)
var <- ts.union(var1, var2)

myspec1 <- regarima_spec_x13(spec = "RG5c", usrdef.varEnabled = TRUE,
                             usrdef.var = var)
myreg1 <- regarima(myseries, myspec1)
myreg1
#> y = regression model + arima (2, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     0.01215      0.108
#> Phi(2)     0.16352      0.075
#> Theta(1)  -0.54810      0.102
#> BTheta(1) -0.66761      0.042
#> 
#>                Estimate Std. Error
#> r.var1       -1.257e-02      0.010
#> r.var2       -3.007e-04      0.001
#> Monday        5.585e-01      0.230
#> Tuesday       8.678e-01      0.230
#> Wednesday     1.039e+00      0.231
#> Thursday      4.572e-02      0.231
#> Friday        9.057e-01      0.232
#> Saturday     -1.546e+00      0.230
#> Leap year     2.134e+00      0.709
#> Easter [1]   -2.490e+00      0.467
#> TC (4-2020)  -3.541e+01      2.166
#> AO (3-2020)  -2.095e+01      2.182
#> AO (5-2011)   1.360e+01      1.870
#> LS (11-2008) -1.248e+01      1.631
#> 
#> 
#> Residual standard error: 2.212 on 340 degrees of freedom
#> Log likelihood = -798.2, aic =  1634 aicc =  1637, bic(corrected for length) = 1.883
#> 

myspec2 <- regarima_spec_x13(spec = "RG5c", usrdef.varEnabled = TRUE,
                             usrdef.var = var1, usrdef.varCoef = 2,
                             transform.function = "None")
myreg2 <- regarima(myseries, myspec2)
s_preVar(myreg2)
#> $series
#>               Jan          Feb          Mar          Apr          May
#> 1990 -15.34266387 -11.14761221  15.97811635  -6.39805078  15.66690553
#> 1991   2.25973337  -5.14857122  -8.23788240   3.34415250  -0.93490765
#> 1992  -1.29408799   4.07795520  -5.83968954  -1.93449890  -2.69546670
#> 1993   1.76436411  11.28307358   4.35001744   5.48833492   6.47418304
#> 1994 -11.87530126   3.62417465  -5.49435319   6.92949838  -0.60843916
#> 1995 -12.50367945  15.82132306  12.52529118  -2.09395701  -6.39033687
#> 1996   4.16082526 -12.95865368   6.82633090   4.96913333  14.39660656
#> 1997 -13.56043492  -3.14751072 -10.19265181  -6.12249656  -2.89068749
#> 1998  -7.33749597  -7.08484753  14.75092459   8.45004185  12.93994431
#> 1999   3.92236141   3.78419970   1.66175673  11.53387369   0.14748302
#> 2000   0.77160580   5.58395338  -1.66854367  -2.27980619   2.42666056
#> 2001 -17.98743117  -9.57051078  -4.74058606 -18.60461283   2.53690073
#> 2002  14.14224665   2.41625825 -14.36087478  -3.14552745  -4.80542811
#> 2003   5.99672514  -5.04358892  -4.06909625  -4.60935206  22.14908426
#> 2004  -7.63245040 -11.18492914  11.97977461   9.81193912  11.91749205
#> 2005  12.76706963   8.21075754   4.19785146  17.11661220 -22.15632715
#> 2006   6.13377167  14.83931321  -4.43773736   2.68589741 -12.28216829
#> 2007   0.59301839   8.48264703  25.75396587   0.94259964  -5.19949532
#> 2008   1.32582442  -9.74084022 -12.50949663  -0.46336042  11.37387771
#> 2009  -3.29112249   1.13049080  10.51229395   3.26977400   7.87037444
#> 2010   2.59523192  -7.73404126 -18.05527531   1.78383232  -5.25777309
#> 2011  -4.41476451  -2.46028129   3.65792190  -0.34132882   2.96227003
#> 2012   0.13030894   0.51249629   5.38638152   5.19672613 -24.22911275
#> 2013   0.01828103   1.40092252  -5.20598538  23.65811636 -16.96474415
#> 2014  14.56857971 -19.33784243  -8.80400798  -7.97730162  -8.86130974
#> 2015   1.73137014   5.77917253  -1.16008707   9.04521145  -0.16586710
#> 2016 -16.46117829  -1.23604069  -9.71640654  10.68587364  23.16252874
#> 2017 -19.41405982  14.15706719   5.96399657  -6.52922289  -1.54144673
#> 2018   3.62795564   7.70735944 -12.88986224  -7.13194370  -1.02383386
#> 2019  10.47205425 -15.46576348 -10.46005681 -22.72669757  -3.16651938
#> 2020  -2.14418765  16.74899343   1.16360148  14.26565587  -2.39667330
#>               Jun          Jul          Aug          Sep          Oct
#> 1990 -14.49155712  -7.91503959  -5.04480733   4.01826700   9.71396469
#> 1991   3.04062078  -4.76507534  -2.41311717   8.24155833 -15.55643970
#> 1992   0.73658232   3.57236138   5.50428418   0.38401793 -16.09575292
#> 1993   8.78463454   3.50797869   0.49879720   8.35749446  -2.81725199
#> 1994 -11.93540930  -1.19908059  -7.08107950 -16.16663973   4.95847824
#> 1995   3.98902937  13.41973500  -0.37607422   5.43670114  17.40218394
#> 1996  12.07358558   2.38514694  -2.98837878  13.84621050  -7.00069022
#> 1997  15.06983292   3.67722694  -0.20034941  -9.79921959 -14.00912333
#> 1998   2.98161142  -4.05682490  -1.38807578  -2.22592731  17.47150257
#> 1999   0.21440845  -8.26352170   0.47399133  -2.93107372  12.07632181
#> 2000  -9.28482969  15.15406678  -8.11598824  13.11247408   8.15566796
#> 2001  -2.14401713 -23.70181451   0.03258078   6.69745568   2.26820843
#> 2002   8.36254248  -0.52349287   9.51957625  14.94512798  -3.44214729
#> 2003  14.86967820  -3.55098858   8.76203737  -2.14696646  20.20798363
#> 2004   6.32833568   5.32825947  -8.20121900  -1.59325676  -0.17532122
#> 2005  -1.84878197   6.71168243  -7.95140242 -15.66257835  12.13732488
#> 2006   4.78528762  16.69859573  -0.36455545  -4.40936271   7.34408890
#> 2007   7.74428621  12.28289259  18.80606885  -1.25241723  -7.59094766
#> 2008  12.64449891  -5.48742076   6.82391430  -9.29773363  -9.75148693
#> 2009   4.41559619 -10.19304514  -1.58698326 -16.37701292  28.39266231
#> 2010   4.00186316  -1.22587586  -0.71345032  20.95734365  13.22082615
#> 2011  -2.21059772   1.87706159  -4.38062172  -0.88733579   6.34250029
#> 2012  -8.06290253  -4.84679992  -6.53077284  -2.93764247  -2.76989004
#> 2013   6.82585584  13.61561976  19.05955757  -6.72838542 -10.62911432
#> 2014  -2.94827785  -8.86651693   0.99084673   7.20546895  10.00469215
#> 2015  -9.22297409 -10.60114550 -17.87199640 -10.66551779 -11.29829171
#> 2016 -16.82873392   1.35875428   4.98437767  13.33462968  -0.22954568
#> 2017  -4.43645660  -5.18233778   2.06107064  16.39453666 -15.64734714
#> 2018  -6.47611750  -3.73253836   0.83347213   9.17216273  -2.58953302
#> 2019 -14.76190645  -1.00387827  -7.46222611   2.03645883   4.97450361
#> 2020 -11.05473915   3.22897729   0.21746800   3.17624820  -9.69700843
#>               Nov          Dec
#> 1990  -5.79663020  16.04179789
#> 1991   0.93501283  -3.66949421
#> 1992 -10.49710115  20.52033974
#> 1993  -7.91679461   0.01653727
#> 1994  12.99750970 -16.15985506
#> 1995  -3.24455939  -4.47511333
#> 1996  18.60931509  18.03924959
#> 1997  14.45014910  -4.23481621
#> 1998  -0.81704668   1.24141586
#> 1999   0.32001384   1.80397550
#> 2000   1.20032668   8.81789848
#> 2001  -5.91868492  -4.05414494
#> 2002   6.45775407 -15.34500551
#> 2003 -18.38661562   1.72937164
#> 2004  -3.90664205  -4.02775110
#> 2005  15.03810074 -11.69425021
#> 2006  -5.75309458   0.74897554
#> 2007  -5.09303603  -1.56039669
#> 2008  -0.27117079   4.46671886
#> 2009   9.61819160   5.08432001
#> 2010  12.00558995  -7.81874565
#> 2011   8.65538237  -4.30593090
#> 2012   1.36469589  10.67207722
#> 2013  16.33683158   5.40830359
#> 2014   5.27999513  11.63605931
#> 2015   3.87267796  12.70263382
#> 2016  -1.91523237  -4.40614893
#> 2017   5.11589918 -15.39661373
#> 2018   6.77025733  -4.20100735
#> 2019 -10.14286644  11.45760347
#> 2020  14.34467716  -9.88804847
#> 
#> $description
#>              type coeff
#> userdef Undefined     2
#> 

 # Pre-specified ARMA coefficients
myspec1 <- regarima_spec_x13(spec = "RG5c", automdl.enabled =FALSE,
             arima.p = 1, arima.q = 1, arima.bp = 0, arima.bq = 1,
             arima.coefEnabled = TRUE, arima.coef = c(-0.8, -0.6, 0),
             arima.coefType = c(rep("Fixed", 2), "Undefined"))

s_arimaCoef(myspec1)
#>                Type Value
#> Phi(1)        Fixed  -0.8
#> Theta(1)      Fixed  -0.6
#> BTheta(1) Undefined   0.0
myreg1 <- regarima(myseries, myspec1)
myreg1
#> y = regression model + arima (1, 1, 1, 0, 1, 1)
#> Log-transformation: yes
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)     -0.8000       0.00
#> Theta(1)   -0.6000       0.00
#> BTheta(1)  -0.6977       0.04
#> 
#>              Estimate Std. Error
#> Monday       0.006317      0.002
#> Tuesday      0.007824      0.002
#> Wednesday    0.010528      0.002
#> Thursday     0.001857      0.002
#> Friday       0.010099      0.002
#> Saturday    -0.018439      0.002
#> Easter [1]  -0.020593      0.004
#> TC (4-2020) -0.475720      0.031
#> AO (3-2020) -0.213355      0.023
#> AO (5-2011)  0.143705      0.016
#> 
#> 
#> Residual standard error: 0.0256 on 347 degrees of freedom
#> Log likelihood = 802.3, aic =  1733 aicc =  1734, bic(corrected for length) = -7.15
#> 
# }
```
