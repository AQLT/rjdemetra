# X-13ARIMA model specification, SA/X13

Function to create (and/or modify) a `c("SA_spec", "X13")` class object
with the SA model specification for the X13 method. It can be done from
a pre-defined 'JDemetra+' model specification (a `character`), a
previous specification (`c("SA_spec", "X13")` object) or a seasonal
adjustment model (`c("SA", "X13")` object).

## Usage

``` r
x13_spec(
  spec = c("RSA5c", "RSA0", "RSA1", "RSA2c", "RSA3", "RSA4c", "X11"),
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
  fcst.horizon = NA_integer_,
  x11.mode = c(NA, "Undefined", "Additive", "Multiplicative", "LogAdditive",
    "PseudoAdditive"),
  x11.seasonalComp = NA,
  x11.lsigma = NA_integer_,
  x11.usigma = NA_integer_,
  x11.trendAuto = NA,
  x11.trendma = NA_integer_,
  x11.seasonalma = NA_character_,
  x11.fcasts = NA_integer_,
  x11.bcasts = NA_integer_,
  x11.calendarSigma = NA,
  x11.sigmaVector = NA,
  x11.excludeFcasts = NA,
  benchmarking.enabled = NA,
  benchmarking.target = c(NA, "Original", "CalendarAdjusted"),
  benchmarking.useforecast = NA,
  benchmarking.rho = NA_real_,
  benchmarking.lambda = NA_real_
)
```

## Arguments

- spec:

  an x13 model specification. It can be the 'JDemetra+' name
  (`character`) of a predefined X13 'JDemetra+' model specification (see
  *Details*), an object of class `c("SA_spec","X13")` or an object of
  class `c("SA", "X13")`. The default is `"RSA5c"`.

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

- x11.mode:

  character: the decomposition mode. Determines the mode of the seasonal
  adjustment decomposition to be performed: `"Undefined"` - no
  assumption concerning the relationship between the time series
  components is made; `"Additive"` - assumes an additive relationship;
  `"Multiplicative"` - assumes a multiplicative relationship;
  `"LogAdditive"` - performs an additive decomposition of the logarithms
  of the series being adjusted; `"PseudoAdditive"` - assumes an
  pseudo-additive relationship. Could be changed by the program, if
  needed.

- x11.seasonalComp:

  logical: if `TRUE`, the program computes a seasonal component.
  Otherwise, the seasonal component is not estimated and its values are
  all set to 0 (additive decomposition) or 1 (multiplicative
  decomposition).

- x11.lsigma:

  numeric: the lower sigma boundary for the detection of extreme values,
  \> 0.5, default=1.5.

- x11.usigma:

  numeric: the upper sigma boundary for the detection of extreme values,
  \> lsigma, default=2.5.

- x11.trendAuto:

  logical: automatic Henderson filter. If `TRUE`, an automatic selection
  of the Henderson filter's length for the trend estimation is enabled.

- x11.trendma:

  numeric: the length of the Henderson filter. The user-defined length
  of the Henderson filter. The option is available when the automatic
  Henderson filter selection is disabled (`x11.trendAuto=FALSE`). Should
  be an odd number in the range (1, 101\].

- x11.seasonalma:

  a vector of character(s) specifying which seasonal moving average
  (i.e. seasonal filter) will be used to estimate the seasonal factors
  for the entire series. The vector can be of length: 1 - the same
  seasonal filter is used for all periods (e.g.: \`seasonal.filter =
  "Msr"\` or \`seasonal.filter = "S3X3"\` ); or have a different value
  for each quarter (length 4) or each month (length 12) - (e.g. for
  quarterly series: \`seasonal.filter = c("S3X3", "Msr", "S3X3",
  "Msr")\`). Possible filters are: \`"Msr"\`, \`"Stable"\`,
  \`"X11Default"\`, \`"S3X1"\`, \`"S3X3"\`, \`"S3X5"\`, \`"S3X9"\`,
  \`"S3X15"\`. \`"Msr"\` - the program chooses the final seasonal filter
  automatically.

- x11.fcasts:

  numeric: the number of forecasts generated by the RegARIMA model in
  periods (positive values) or years (negative values).Default value:
  fcasts=-1.

- x11.bcasts:

  numeric: the number of backcasts used in X11. Negative figures are
  translated in years of backcasts. Default value: bcasts=0.

- x11.calendarSigma:

  character to specify if the standard errors used for extreme values
  detection and adjustment are computed: from 5 year spans of irregulars
  (`"None"`, the default); separately for each calendar month/quarter
  (`"All"`); separately for each period only if Cochran’s hypothesis
  test determines that the irregular component is heteroskedastic by
  calendar month/quarter (`"Signif"`); separately for two complementary
  sets of calendar months/quarters specified by the x11.sigmaVector
  parameter (`"Select"`, see parameter `x11.sigmaVector`).

- x11.sigmaVector:

  a vector to specify one of the two groups of periods for whose
  standard errors used for extreme values detection and adjustment will
  be computed. Only used if `x11.calendarSigma = "Select"`. Possible
  values are: "Group1" and "Group2".

- x11.excludeFcasts:

  logical: to exclude forecasts and backcasts. If `TRUE`, the RegARIMA
  model forecasts and backcasts are not used during the detection of
  extreme values in the seasonal adjustment routines.

- benchmarking.enabled:

  logical: to enable benchmarking. If `TRUE`, the benchmarking is
  enabled.

- benchmarking.target:

  character: the target of the benchmarking procedure, which can be the
  raw series (`"Original"`) or the series the adjusted for calendar
  effects (`"CalendarAdjusted"`).

- benchmarking.useforecast:

  logical: If `TRUE`, the forecasts of the seasonally adjusted variable
  and of the target variable are used in the benchmarking computation so
  the benchmarking constrains is also applied to the forecasting period.

- benchmarking.rho:

  numeric: the value of the AR(1) parameter (set between 0 and 1) in the
  function used for benchmarking.

- benchmarking.lambda:

  numeric: a parameter used for benchmarking that relatesto to the
  weights in the regression equation. It is typically equal to 0, 1/2 or
  1.

## Value

A two-element list of class `c("SA_spec", "X13")`, containing: (1) an
object of class `c("regarima_spec", "X13")` with the RegARIMA model
specification; (2) an object of class `c("X11_spec", "data.frame")` with
the X11 algorithm specification. Each component refers to different
parts of the SA model specification, mirroring the arguments of the
function (for details, see the function arguments in the description).
Each lowest-level component (except span, pre-specified outliers,
user-defined variables and pre-specified ARMA coefficients) is
structured as a data frame with columns denoting different variables of
the model specification and rows referring to:

- first row: the base specification, as provided within the argument
  `spec`;

- second row: user modifications as specified by the remaining arguments
  of the function (e.g.: `arima.d`);

- and third row: the final model specification.

  The final specification (third row) shall include user modifications
  (row two) unless they were wrongly specified. The pre-specified
  outliers, user-defined variables and pre-specified ARMA coefficients
  consist of a list of `Predefined` (base model specification) and
  `Final` values.

- `regarima`: an object of class `c("regarima_spec", "x13")`. See
  *Value* of the function [`regarima_spec_x13`](regarima_spec_x13.md).

- `x11`: a data.frame of class `c("X11_spec", "data.frame")`, containing
  the *x11* variables in line with the names of the arguments variables.
  The final values can be also accessed with the function
  [`s_x11`](specification.md).

## Details

The available predefined 'JDemetra+' model specifications are described
in the table below:

|                       |                            |                           |                         |                       |                       |             |
|-----------------------|----------------------------|---------------------------|-------------------------|-----------------------|-----------------------|-------------|
| **Identifier** \|     | **Log/level detection** \| | **Outliers detection** \| | **Calendar effects** \| | **ARIMA**             | RSA0 \|               | *NA* \|     |
| *NA* \|               | *NA* \|                    | Airline(+mean)            | RSA1 \|                 | automatic \|          | AO/LS/TC \|           | *NA* \|     |
| Airline(+mean)        | RSA2c \|                   | automatic \|              | AO/LS/TC \|             | 2 td vars + Easter \| | Airline(+mean)        | RSA3 \|     |
| automatic \|          | AO/LS/TC \|                | *NA* \|                   | automatic               | RSA4c \|              | automatic \|          | AO/LS/TC \| |
| 2 td vars + Easter \| | automatic                  | RSA5c \|                  | automatic \|            | AO/LS/TC \|           | 7 td vars + Easter \| | automatic   |

## References

More information and examples related to 'JDemetra+' features in the
online documentation: <https://jdemetra-new-documentation.netlify.app/>
BOX G.E.P. and JENKINS G.M. (1970), "Time Series Analysis: Forecasting
and Control", Holden-Day, San Francisco.

BOX G.E.P., JENKINS G.M., REINSEL G.C. and LJUNG G.M. (2015), "Time
Series Analysis: Forecasting and Control", John Wiley & Sons, Hoboken,
N. J., 5th edition.

## See also

[`x13`](x13.md)

## Examples

``` r
# \donttest{
myseries <- ipi_c_eu[, "FR"]
myspec1 <- x13_spec(spec = "RSA5c")
myreg1 <- x13(myseries, spec = myspec1)

# To modify a pre-specified model specification
myspec2 <- x13_spec(spec = "RSA5c", tradingdays.option = "WorkingDays")
myreg2 <- x13(myseries, spec = myspec2)

# To modify the model specification of a "X13" object
 myspec3 <- x13_spec(myreg1, tradingdays.option = "WorkingDays")
 myreg3 <- x13(myseries, myspec3)

# To modify the model specification of a "X13_spec" object
 myspec4 <- x13_spec(myspec1, tradingdays.option = "WorkingDays")
 myreg4 <- x13(myseries, myspec4)

# Pre-specified outliers
 myspec1 <- x13_spec(spec = "RSA5c", usrdef.outliersEnabled = TRUE,
             usrdef.outliersType = c("LS", "AO"),
             usrdef.outliersDate = c("2008-10-01", "2002-01-01"),
             usrdef.outliersCoef = c(36, 14),
             transform.function = "None")

 myreg1 <- x13(myseries, myspec1)
 myreg1
#> RegARIMA
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
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.151
#> M(2)    0.097
#> M(3)    1.206
#> M(4)    0.558
#> M(5)    1.041
#> M(6)    0.037
#> M(7)    0.082
#> M(8)    0.242
#> M(9)    0.062
#> M(10)   0.267
#> M(11)   0.252
#> Q       0.366
#> Q-M2    0.399
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t            s           i
#> Jan 2020 101.0 102.89447 102.9447  -1.89446776  -0.0502488
#> Feb 2020 100.1 103.56224 102.9860  -3.46224124   0.5762734
#> Mar 2020  91.8  82.81896 103.2071   8.98103618 -20.3881828
#> Apr 2020  66.7  66.62390 103.6164   0.07610348 -36.9925073
#> May 2020  73.7  78.88976 104.0255  -5.18976181 -25.1357871
#> Jun 2020  98.2  87.30845 104.3450  10.89154932 -17.0365408
#> Jul 2020  97.4  92.39390 104.4861   5.00609785 -12.0921816
#> Aug 2020  71.7  97.51560 104.3380 -25.81559971  -6.8224392
#> Sep 2020 104.7  97.40102 103.9044   7.29897634  -6.5033820
#> Oct 2020 106.7  98.39408 103.3109   8.30592464  -4.9168409
#> Nov 2020 101.6 100.23574 102.7824   1.36426365  -2.5467131
#> Dec 2020  96.6  99.67219 102.4984  -3.07218537  -2.8261840
#> 
#> Forecasts:
#>                y_f     sa_f      t_f          s_f         i_f
#> Jan 2021  94.41766 101.0272 102.4220  -6.60952495 -1.39481900
#> Feb 2021  97.82331 101.6172 102.4196  -3.79385040 -0.80247216
#> Mar 2021 114.01485 102.1273 102.3712  11.88751670 -0.24388469
#> Apr 2021 102.04691 102.0672 102.2273  -0.02033583 -0.16002624
#> May 2021  95.95071 101.4262 102.0682  -5.47547024 -0.64200227
#> Jun 2021 112.61492 101.2166 101.9501  11.39833187 -0.73348910
#> Jul 2021 104.00289 101.5502 101.9316   2.45263829 -0.38137799
#> Aug 2021  79.03331 102.3155 102.0544 -23.28216183  0.26109558
#> Sep 2021 108.98851 102.3414 102.2480   6.64711680  0.09343944
#> Oct 2021 108.49736 102.1909 102.4372   6.30644391 -0.24626669
#> Nov 2021 106.32534 102.4451 102.6074   3.88025741 -0.16229864
#> Dec 2021  99.71313 102.9154 102.7518  -3.20223190  0.16356694
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         1.625
#>  Seasonal     41.918
#>  Irregular     0.727
#>  TD & Hol.     1.851
#>  Others       55.678
#>  Total       101.800
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.042
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          0.974
#>  qs test on i                           0.779
#>  f-test on sa (seasonal dummies)        0.921
#>  f-test on i (seasonal dummies)         0.826
#>  Residual seasonality (entire series)   0.770
#>  Residual seasonality (last 3 years)    0.894
#>  f-test on sa (td)                      0.974
#>  f-test on i (td)                       0.988
#> 
#> 
#> Additional output variables
 s_preOut(myreg1)
#>   type       date coeff
#> 1   LS 2008-10-01    36
#> 2   AO 2002-01-01    14


# User-defined calendar regressors
 var1 <- ts(rnorm(length(myseries))*10, start = start(myseries), frequency = 12)
 var2 <- ts(rnorm(length(myseries))*100, start = start(myseries), frequency = 12)
 var <- ts.union(var1, var2)
 myspec1 <- x13_spec(spec = "RSA5c", tradingdays.option = "UserDefined",
                     usrdef.varEnabled = TRUE,
                     usrdef.var = var,
                     usrdef.varType = c("Calendar", "Calendar"))
#> Warning: With tradingdays.option = "UserDefined", the parameters tradingdays.autoadjust, tradingdays.leapyear and tradingdays.stocktd are ignored.
 myreg1 <- x13(myseries, myspec1)
 myreg1
#> RegARIMA
#> y = regression model + arima (3, 1, 1, 0, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)      0.3595      0.209
#> Phi(2)      0.1177      0.210
#> Phi(3)     -0.3259      0.155
#> Theta(1)   -0.6771      0.192
#> BTheta(1)  -0.7343      0.039
#> 
#>              Estimate Std. Error
#> Easter [8]     -2.891      0.686
#> TC (4-2020)   -36.231      2.021
#> AO (3-2020)   -22.969      2.463
#> LS (11-2008)  -12.368      1.610
#> AO (5-2011)     9.825      2.265
#> TC (2-2009)    -8.128      1.857
#> 
#> 
#> Residual standard error: 2.839 on 347 degrees of freedom
#> Log likelihood = -889.4, aic =  1803 aicc =  1804, bic(corrected for length) = 2.267
#> 
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.376
#> M(2)    0.310
#> M(3)    3.000
#> M(4)    0.733
#> M(5)    2.377
#> M(6)    0.514
#> M(7)    0.116
#> M(8)    0.294
#> M(9)    0.074
#> M(10)   0.369
#> M(11)   0.334
#> Q       0.818
#> Q-M2    0.881
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  23-Henderson
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t          s             i
#> Jan 2020 101.0 103.76443 103.7718  -2.764432  -0.007371637
#> Feb 2020 100.1 104.34515 103.9252  -4.245147   0.419965250
#> Mar 2020  91.8  81.04300 104.1168  10.757002 -23.073821166
#> Apr 2020  66.7  68.07471 104.2936  -1.374714 -36.218923904
#> May 2020  73.7  77.34542 104.4050  -3.645424 -27.059534745
#> Jun 2020  98.2  88.68292 104.4313   9.517080 -15.748342655
#> Jul 2020  97.4  93.46921 104.3778   3.930791 -10.908580688
#> Aug 2020  71.7  95.43752 104.2570 -23.737519  -8.819459329
#> Sep 2020 104.7  99.17267 104.0850   5.527329  -4.912314376
#> Oct 2020 106.7  97.12864 103.8669   9.571357  -6.738282414
#> Nov 2020 101.6  99.69487 103.6276   1.905134  -3.932784061
#> Dec 2020  96.6 102.36060 103.4003  -5.760595  -1.039736263
#> 
#> Forecasts:
#>                y_f     sa_f      t_f         s_f         i_f
#> Jan 2021  98.44952 101.2056 103.1901  -2.7560785 -1.98454698
#> Feb 2021  98.43821 102.5471 103.0165  -4.1088538 -0.46944312
#> Mar 2021 110.75460 101.9734 102.8973   8.7811716 -0.92383422
#> Apr 2021 103.71542 102.9016 102.8411   0.8138272  0.06051994
#> May 2021  99.53055 103.1863 102.8510  -3.6557369  0.33528360
#> Jun 2021 111.31381 101.6749 102.8754   9.6388933 -1.20051449
#> Jul 2021 105.69802 101.5389 102.9077   4.1591091 -1.36882965
#> Aug 2021  79.42133 103.3872 102.9666 -23.9658420  0.42058783
#> Sep 2021 108.59095 102.9687 103.0586   5.6222373 -0.08983556
#> Oct 2021 112.00799 102.4761 103.1532   9.5318659 -0.67704911
#> Nov 2021 105.36088 103.8747 103.2467   1.4862299  0.62793860
#> Dec 2021  98.66941 104.3502 103.4522  -5.6808324  0.89800432
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         1.963
#>  Seasonal     59.842
#>  Irregular     3.416
#>  TD & Hol.     0.172
#>  Others       34.046
#>  Total        99.439
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.269
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          0.000
#>  qs test on i                           0.002
#>  f-test on sa (seasonal dummies)        0.813
#>  f-test on i (seasonal dummies)         0.754
#>  Residual seasonality (entire series)   0.568
#>  Residual seasonality (last 3 years)    1.000
#>  f-test on sa (td)                      0.000
#>  f-test on i (td)                       0.000
#> 
#> 
#> Additional output variables

 myspec2 <- x13_spec(spec = "RSA5c", usrdef.varEnabled = TRUE,
             usrdef.var = var1, usrdef.varCoef = 2,
             transform.function = "None")
 myreg2 <- x13(myseries, myspec2)
 s_preVar(myreg2)
#> $series
#>               Jan          Feb          Mar          Apr          May
#> 1990  12.65038490   6.99530402  -4.78932287 -13.14202741  -9.03645819
#> 1991 -14.22799149   6.85714751 -15.74190181 -10.39202637  10.62892692
#> 1992  13.53031635   6.55348285   2.08748369   4.79304525  11.19721889
#> 1993  -4.78648838 -16.27036866  10.95973351 -11.30615770   7.49407597
#> 1994  25.86841900 -16.41368825   1.85576753   8.08139505   4.62741902
#> 1995  -5.87793245  21.10958544   1.06319181   2.88638282  -8.28129022
#> 1996  -6.13436596   7.49492399  13.68161796   8.09041925  10.52043916
#> 1997 -18.90227763  14.61477127  -3.93734253   5.88577012 -10.59461309
#> 1998  -7.84406639  -4.70589637  26.18843475  17.81970431   3.11227898
#> 1999  -0.91846724   6.97447152   8.50194263  -2.82469962  10.56820511
#> 2000   4.60803569   6.45915651   2.86538618 -19.55302496  -0.70122520
#> 2001   5.21310799  -4.71600217  -3.86758443  -0.32921492 -15.89925204
#> 2002   3.72374042 -15.66243530  -8.27262343  10.43432242  -5.61818713
#> 2003  14.64151538 -13.44497531  -0.07853537  -7.09360740  14.19910316
#> 2004  -2.08778684  16.38748991   7.14250476   0.21730272  -7.10864161
#> 2005  13.30182641  19.42670865   4.54756408  -4.35878269  16.42250741
#> 2006 -13.89147408  -6.44304935  -3.17781887 -26.11142582  -4.04070180
#> 2007   9.33783648  -4.30394846  13.18921431   7.86662563   3.90908196
#> 2008 -17.16257245  -3.55226178   9.79276002 -11.74070697  -3.96460863
#> 2009 -13.67382107   3.71975670   7.52496103  -8.44102704 -14.74703765
#> 2010  -2.43510381   3.04153582  -1.56110528   6.66411599 -21.43024893
#> 2011  16.07831850  15.28664770   2.85760869   9.66478863   0.41676859
#> 2012   5.73972934   9.16852243  11.82521119   0.89920960 -14.23925932
#> 2013  -6.78534611  18.72999491  -9.15749659  -0.12128002 -11.17237976
#> 2014   1.97141988 -15.34357208   0.26618737   3.62927093  -6.77324332
#> 2015 -14.97546434  -1.52302024  13.18666001  -7.75961869  11.48134828
#> 2016  -6.73465522 -11.51931160  -8.74614335  -0.56005464  -6.48120780
#> 2017  -5.30695812   1.30699486   8.77061311   5.57893934  11.50015537
#> 2018   1.14206605  -1.61878192   5.52162660   3.48733451  -0.62679216
#> 2019  -0.98173680   2.61431794   9.10112488  17.07880340  -1.16850068
#> 2020  -2.51076580  -5.41457261  -0.93337603  -5.41383993   0.71532898
#>               Jun          Jul          Aug          Sep          Oct
#> 1990  -6.82677769   3.74599658   8.09784422 -10.27311894   2.71204716
#> 1991 -12.79380891 -17.65259960 -23.94684943   6.61851420   2.79202139
#> 1992   3.58970059  11.98583489   5.63019465   3.60364311   8.25363990
#> 1993   5.07040903   1.49227768   7.56914894  -4.27224530 -13.47831121
#> 1994  -1.40862948 -18.30167300   4.04087877  -0.13750674  -1.02241238
#> 1995   2.59246188  -4.95230738  -2.89501667   6.40683953  -1.41462861
#> 1996  15.76710173  11.52029911  -5.17742857  -6.35012824  -4.00123911
#> 1997   7.02083603  -2.54390092  -3.80451079   7.22051799  13.27842786
#> 1998   6.04652922   8.02925361  -7.42182079 -10.86486271  15.85888347
#> 1999  -1.64563751  -5.05197318  -4.02419900  22.95251358  -0.58040167
#> 2000 -19.93476957   1.21132684   4.35595856   1.38904324   9.82497501
#> 2001 -16.31630380  -6.19216932  -4.28563857  21.43623439  13.81055332
#> 2002   4.58990225   4.61175487   5.88209678  13.65187644   2.37584966
#> 2003  21.00753869   0.56429659   8.05545122  -1.92729984  -1.20578134
#> 2004   0.67650247  18.67312976   7.39326267   9.65687441   4.69334931
#> 2005  -1.19391302   0.03403357  -2.87662480  10.04914840 -15.19681487
#> 2006  19.63939389  -9.08038236   2.31002822  10.83031391 -10.23062790
#> 2007   5.55016634   4.95861493 -15.88836847  -3.21264477 -15.52052891
#> 2008   0.28959344 -14.70506429   9.65172228  -7.81441694  12.57319338
#> 2009  -1.27286512  -1.13083340  18.06296611  -9.16313634   3.26036046
#> 2010  -7.85684050   8.56316142  -3.54721322   1.86108946   3.85897720
#> 2011  -1.86568045 -13.51099737  -9.53225887 -12.82607152  13.48738780
#> 2012   1.85840157   6.47343621   1.23381550  -5.57040623  -4.24403791
#> 2013   2.69965596  15.11653990  -5.93155678 -16.14954366 -13.73896551
#> 2014  -3.86793166  -2.10774079  -6.33652476   0.79569318   2.38637053
#> 2015  11.40960766  -3.34901191   6.29659134   7.34016764  18.02049619
#> 2016   2.67518834   3.49756194 -12.17302032   0.81927914  -7.95643416
#> 2017  -2.82304681 -17.42631121   4.01343311   6.49059795  10.87865196
#> 2018  -4.82827570  19.95979803 -12.51509572   5.28487960 -12.47616265
#> 2019  16.78622239  10.14766041   1.42581271   0.25446068  -6.78451736
#> 2020 -18.22621951  10.99169761   7.55876838  -3.84879611  10.16790220
#>               Nov          Dec
#> 1990   3.72163386 -14.73803514
#> 1991 -19.75798133   4.96506933
#> 1992  -0.40392584  -6.05456736
#> 1993   0.82595585  11.53728116
#> 1994   2.02454445   8.03320548
#> 1995  -8.79847386  -5.23639611
#> 1996   5.93241461  -0.01094905
#> 1997  -1.25492499  11.39794704
#> 1998  -1.40704169  -9.75276634
#> 1999   1.22377660  -2.00777681
#> 2000  -2.86391397  16.94152064
#> 2001  -9.81823126  13.12917276
#> 2002 -13.01932383  17.37977175
#> 2003  -2.41185306  -2.55729561
#> 2004   7.32928056  13.33797734
#> 2005  10.80588866   4.35371426
#> 2006  19.75884923   5.01748489
#> 2007   9.61515998 -10.86315269
#> 2008 -20.46247314  18.19078188
#> 2009  17.29406356   6.18631030
#> 2010   6.05504903   5.22120605
#> 2011   0.87489524  -5.66758222
#> 2012  14.21456362  -8.10897493
#> 2013  11.92737540   1.16453951
#> 2014  -5.11546412  -8.20642372
#> 2015 -11.48480057  12.16381354
#> 2016  -5.84737942   5.34806561
#> 2017  11.59117507 -15.10504494
#> 2018  -0.41651340 -10.54737293
#> 2019  -3.72064237  12.11360613
#> 2020  -5.23622538   0.27453819
#> 
#> $description
#>              type coeff
#> userdef Undefined     2
#> 

# Pre-specified ARMA coefficients
 myspec1 <- x13_spec(spec = "RSA5c", automdl.enabled = FALSE,
             arima.p = 1, arima.q = 1, arima.bp = 0, arima.bq = 1,
             arima.coefEnabled = TRUE,
             arima.coef = c(-0.8, -0.6, 0),
             arima.coefType = c(rep("Fixed", 2), "Undefined"))

 s_arimaCoef(myspec1)
#>                Type Value
#> Phi(1)        Fixed  -0.8
#> Theta(1)      Fixed  -0.6
#> BTheta(1) Undefined   0.0
 myreg1 <- x13(myseries, myspec1)
 myreg1
#> RegARIMA
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
#> 
#> 
#> Decomposition
#> Monitoring and Quality Assessment Statistics:
#>       M stats
#> M(1)    0.097
#> M(2)    0.052
#> M(3)    0.750
#> M(4)    0.749
#> M(5)    0.731
#> M(6)    0.126
#> M(7)    0.075
#> M(8)    0.220
#> M(9)    0.075
#> M(10)   0.293
#> M(11)   0.281
#> Q       0.300
#> Q-M2    0.331
#> 
#> Final filters: 
#> Seasonal filter:  3x5
#> Trend filter:  13 terms Henderson moving average
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t         s         i
#> Jan 2020 101.0 103.50059 103.4716 0.9758398 1.0002804
#> Feb 2020 100.1 103.70789 104.1959 0.9652110 0.9953168
#> Mar 2020  91.8  85.02419 105.2353 1.0796927 0.8079439
#> Apr 2020  66.7  66.06576 106.3700 1.0096002 0.6210940
#> May 2020  73.7  77.29646 107.2332 0.9534719 0.7208256
#> Jun 2020  98.2  88.21419 107.6348 1.1131996 0.8195693
#> Jul 2020  97.4  92.04371 107.5406 1.0581929 0.8558971
#> Aug 2020  71.7  95.53300 106.9592 0.7505260 0.8931720
#> Sep 2020 104.7  97.32774 105.9849 1.0757467 0.9183169
#> Oct 2020 106.7  98.74148 104.7928 1.0805996 0.9422542
#> Nov 2020 101.6 100.23569 103.5604 1.0136110 0.9678964
#> Dec 2020  96.6  99.45166 102.3889 0.9713262 0.9713127
#> 
#> Forecasts:
#>                y_f     sa_f       t_f       s_f       i_f
#> Jan 2021  91.86627 99.03608 101.33234 0.9276040 0.9773393
#> Feb 2021  93.73814 98.76312 100.39814 0.9491209 0.9837146
#> Mar 2021 109.97904 99.04192  99.55589 1.1104292 0.9948373
#> Apr 2021  99.51314 98.51411  98.84092 1.0101410 0.9966935
#> May 2021  92.44138 97.26558  98.27297 0.9504018 0.9897491
#> Jun 2021 109.51917 97.80126  97.82297 1.1198135 0.9997780
#> Jul 2021  99.72232 96.85484  97.49522 1.0296059 0.9934317
#> Aug 2021  74.93973 97.28720  97.30419 0.7702938 0.9998254
#> Sep 2021 104.15955 97.30940  97.21500 1.0703955 1.0009711
#> Oct 2021 102.57254 96.84676  97.16553 1.0591221 0.9967193
#> Nov 2021 100.68100 96.97009  97.14932 1.0382686 0.9981552
#> Dec 2021  94.63045 97.42206  97.13060 0.9713452 1.0030007
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         5.183
#>  Seasonal     82.105
#>  Irregular     1.148
#>  TD & Hol.     3.365
#>  Others       10.592
#>  Total       102.393
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.406
#>  
#>  Identifiable seasonality present
#> 
#> Residual seasonality tests
#>                                       P.value
#>  qs test on sa                          1.000
#>  qs test on i                           0.939
#>  f-test on sa (seasonal dummies)        0.990
#>  f-test on i (seasonal dummies)         0.972
#>  Residual seasonality (entire series)   0.989
#>  Residual seasonality (last 3 years)    0.996
#>  f-test on sa (td)                      0.994
#>  f-test on i (td)                       0.959
#> 
#> 
#> Additional output variables

# To define a seasonal filter
 myspec1 <- x13_spec("RSA5c", x11.seasonalma = rep("S3X1", 12))
 mysa1 <- x13(myseries, myspec1)
# }
```
