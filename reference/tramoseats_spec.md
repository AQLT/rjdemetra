# TRAMO-SEATS model specification

Function to create (and/or modify) a `c("SA_spec", "TRAMO_SEATS")` class
object with the SA model specification for the TRAMO-SEATS method. It
can be done from a pre-defined 'JDemetra+' model specification (a
`character`), a previous specification (`c("SA_spec", "TRAMO_SEATS")`
object) or a seasonal adjustment model (`c("SA", "TRAMO_SEATS")`
object).

## Usage

``` r
tramoseats_spec(
  spec = c("RSAfull", "RSA0", "RSA1", "RSA2", "RSA3", "RSA4", "RSA5"),
  preliminary.check = NA,
  estimate.from = NA_character_,
  estimate.to = NA_character_,
  estimate.first = NA_integer_,
  estimate.last = NA_integer_,
  estimate.exclFirst = NA_integer_,
  estimate.exclLast = NA_integer_,
  estimate.tol = NA_integer_,
  estimate.eml = NA,
  estimate.urfinal = NA_integer_,
  transform.function = c(NA, "Auto", "None", "Log"),
  transform.fct = NA_integer_,
  usrdef.outliersEnabled = NA,
  usrdef.outliersType = NA,
  usrdef.outliersDate = NA,
  usrdef.outliersCoef = NA,
  usrdef.varEnabled = NA,
  usrdef.var = NA,
  usrdef.varType = NA,
  usrdef.varCoef = NA,
  tradingdays.mauto = c(NA, "Unused", "FTest", "WaldTest"),
  tradingdays.pftd = NA_integer_,
  tradingdays.option = c(NA, "TradingDays", "WorkingDays", "UserDefined", "None"),
  tradingdays.leapyear = NA,
  tradingdays.stocktd = NA_integer_,
  tradingdays.test = c(NA, "Separate_T", "Joint_F", "None"),
  easter.type = c(NA, "Unused", "Standard", "IncludeEaster", "IncludeEasterMonday"),
  easter.julian = NA,
  easter.duration = NA_integer_,
  easter.test = NA,
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
  outlier.eml = NA,
  outlier.tcrate = NA_integer_,
  automdl.enabled = NA,
  automdl.acceptdefault = NA,
  automdl.cancel = NA_integer_,
  automdl.ub1 = NA_integer_,
  automdl.ub2 = NA_integer_,
  automdl.armalimit = NA_integer_,
  automdl.reducecv = NA_integer_,
  automdl.ljungboxlimit = NA_integer_,
  automdl.compare = NA,
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
  seats.predictionLength = NA_integer_,
  seats.approx = c(NA, "None", "Legacy", "Noisy"),
  seats.trendBoundary = NA_integer_,
  seats.seasdBoundary = NA_integer_,
  seats.seasdBoundary1 = NA_integer_,
  seats.seasTol = NA_integer_,
  seats.maBoundary = NA_integer_,
  seats.method = c(NA, "Burman", "KalmanSmoother", "McElroyMatrix"),
  benchmarking.enabled = NA,
  benchmarking.target = c(NA, "Original", "CalendarAdjusted"),
  benchmarking.useforecast = NA,
  benchmarking.rho = NA_real_,
  benchmarking.lambda = NA_real_
)
```

## Arguments

- spec:

  a TRAMO-SEATS model specification. It can be the 'JDemetra+' name
  (`character`) of a predefined TRAMO-SEATS model specification (see
  *Details*), an object of class `c("SA_spec","TRAMO_SEATS")` or an
  object of class `c("SA", "TRAMO_SEATS")`. The default is `"RSAfull"`.

- preliminary.check:

  a `logical` to check the quality of the input series and exclude
  highly problematic series e.g. the series with a number of identical
  observations and/or missing values above pre-specified threshold
  values.

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

  a `character` in format "YYYY-MM-DD" indicating the end of the time
  span (e.g. "2020-12-31"). It can be combined with the parameter
  `estimate.from`.

- estimate.first:

  `numeric`, the number of periods considered at the beginning of the
  series.

- estimate.last:

  `numeric`, the number of periods considered at the end of the series.

- estimate.exclFirst:

  `numeric`, the number of periods excluded at the beginning of the
  series. It can be combined with the parameter `estimate.exclLast`.

- estimate.exclLast:

  `numeric`, the number of periods excluded at the end of the series. It
  can be combined with the parameter `estimate.exclFirst`.

- estimate.tol:

  `numeric`, the convergence tolerance. The absolute changes in the
  log-likelihood function are compared to this value to check for the
  convergence of the estimation iterations.

- estimate.eml:

  `logical`, the exact maximum likelihood estimation. If `TRUE`, the
  program performs an exact maximum likelihood estimation. If `FASLE`,
  the Unconditional Least Squares method is used.

- estimate.urfinal:

  `numeric`, the final unit root limit. The threshold value for the
  final unit root test for identification of differencing orders. If the
  magnitude of an AR root for the final model is smaller than this
  number, then a unit root is assumed, the order of the AR polynomial is
  reduced by one and the appropriate order of the differencing
  (non-seasonal, seasonal) is increased.

- transform.function:

  the transformation of the input series: `"None"` = no transformation
  of the series; `"Log"` = takes the log of the series; `"Auto"` = the
  program tests for the log-level specification.

- transform.fct:

  `numeric` controlling the bias in the log/level pre-test:
  ` transform.fct `\> 1 favours levels, `transform.fct`\< 1 favours
  logs. Considered only when `transform.function` is set to `"Auto"`.

  Control variables for the pre-specified outliers. Said pre-specified
  outliers are used in the model only when enabled
  (`usrdef.outliersEnabled=TRUE`) and when the outliers' type
  (`usrdef.outliersType`) and date (`usrdef.outliersDate`) are provided.

- usrdef.outliersEnabled:

  `logical`. If `TRUE`, the program uses the pre-specified outliers.

- usrdef.outliersType:

  a vector defining the outliers' type. Possible types are: `("AO"`) =
  additive, `("LS"`) = level shift, `("TC"`) = transitory change,
  `("SO"`) = seasonal outlier. E.g.:
  ` usrdef.outliersType= c("AO","AO","LS")`.

- usrdef.outliersDate:

  a vector defining the outliers' date. The dates should be characters
  in format "YYYY-MM-DD". E.g.:
  `usrdef.outliersDate= c("2009-10-01","2005-02-01","2003-04-01")`.

- usrdef.outliersCoef:

  a vector providing fixed coefficients for the outliers. The
  coefficients can't be fixed if the parameter ` transform.function` is
  set to `"Auto"` (i.e. if the series transformation needs to be
  pre-defined.) E.g.: `usrdef.outliersCoef= c(200,170,20)`.

  Control variables for the user-defined variables:

- usrdef.varEnabled:

  `logical` If `TRUE`, the program uses the user-defined variables.

- usrdef.var:

  a time series (`ts`) or a matrix of time series (`mts`) containing the
  user-defined variables.

- usrdef.varType:

  a vector of character(s) defining the user-defined variables component
  type. Possible types are:
  `"Undefined", "Series", "Trend", "Seasonal", "SeasonallyAdjusted", "Irregular", "Calendar"`.
  To use the user-defined calendar regressors, the type `"Calendar"`
  must be defined in conjunction with
  `tradingdays.option = "UserDefined"`. Otherwise, the program will
  automatically set `usrdef.varType = "Undefined"`.

- usrdef.varCoef:

  a vector providing fixed coefficients for the user-defined variables.
  The coefficients can't be fixed if ` transform.function` is set to
  `"Auto"` (i.e. if the series transformation needs to be pre-defined).

- tradingdays.mauto:

  defines whether the calendar effects should be added to the model
  manually (`"Unused"`) or automatically. During the automatic
  selection, the choice of the number of calendar variables can be based
  on the F-Test (`"FTest"`) or the Wald Test (`"WaldTest"`); the model
  with higher F value is chosen, provided that it is higher than
  `tradingdays.pftd`).

- tradingdays.pftd:

  `numeric`. The p-value used in the test specified by the automatic
  parameter (`tradingdays.mauto`) to assess the significance of the
  pre-tested calendar effects variables and whether they should be
  included in the RegArima model.

  Control variables for the manual selection of calendar effects
  variables (`tradingdays.mauto` is set to `"Unused"`):

- tradingdays.option:

  to choose the trading days regression variables: `"TradingDays"` = six
  day-of-the-week regression variables; `"WorkingDays"` = one
  working/non-working day contrast variable; `"None"` = no correction
  for trading days and working days effects; `"UserDefined"` =
  user-defined trading days regressors (regressors must be defined by
  the `usrdef.var` argument with `usrdef.varType` set to `"Calendar"`
  and `usrdef.varEnabled = TRUE`). `"None"` must also be chosen for the
  "day-of-week effects" correction (and `tradingdays.stocktd` must be
  modified accordingly).

- tradingdays.leapyear:

  `logical`. Specifies if the leap-year correction should be included.
  If `TRUE`, the model includes the leap-year effect.

- tradingdays.stocktd:

  numeric indicating the day of the month when inventories and other
  stock are reported (to denote the last day of the month set the
  variable to 31). Modifications of this variable are taken into account
  only when `tradingdays.option` is set to `"None"`.

- tradingdays.test:

  defines the pre-tests of the trading day effects: `"None"` = calendar
  variables are used in the model without pre-testing; `"Separate_T"` =
  a t-test is applied to each trading day variable separately and the
  trading day variables are included in the RegArima model if at least
  one t-statistic is greater than 2.6 or if two t-statistics are greater
  than 2.0 (in absolute terms); `"Joint_F"` = a joint F-test of
  significance of all the trading day variables. The trading day effect
  is significant if the F statistic is greater than 0.95.

- easter.type:

  a`character` that specifies the presence and the length of the Easter
  effect: `"Unused"` = the Easter effect is not considered; `"Standard"`
  = influences the period of `n` days strictly before Easter Sunday;
  `"IncludeEaster"` = influences the entire period (`n`) up to and
  including Easter Sunday; `"IncludeEasterMonday"` = influences the
  entire period (`n`) up to and including Easter Monday.

- easter.julian:

  `logical`. If `TRUE`, the program uses the Julian Easter (expressed in
  Gregorian calendar).

- easter.duration:

  `numeric` indicating the duration of the Easter effect (length in
  days, between 1 and 15).

- easter.test:

  `logical`. If `TRUE`, the program performs a t-test for the
  significance of the Easter effect. The Easter effect is considered as
  significant if the modulus of t-statistic is greater than 1.96.

- outlier.enabled:

  `logical`. If `TRUE`, the automatic detection of outliers is enabled
  in the defined time span.

  The time span of the series to be searched for outliers is controlled
  by the following six variables:
  `outlier.from, outlier.to, outlier.first, outlier.last, outlier.exclFirst`
  and `outlier.exclLast`; where `outlier.from` and `outlier.to` have
  priority over the remaining span control variables, `outlier.last` and
  `outlier.first` have priority over `outlier.exclFirst` and
  `outlier.exclLast`, and `outlier.last` has priority over
  `outlier.first`.

- outlier.from:

  a character in format "YYYY-MM-DD" indicating the start of the time
  span (e.g. "1900-01-01"). It can be combined with `outlier.to`.

- outlier.to:

  a character in format "YYYY-MM-DD" indicating the end of the time span
  (e.g. "2020-12-31"). It can be combined with `outlier.from`.

- outlier.first:

  `numeric` specifying the number of periods considered at the beginning
  of the series.

- outlier.last:

  `numeric` specifying the number of periods considered at the end of
  the series.

- outlier.exclFirst:

  `numeric` specifying the number of periods excluded at the beginning
  of the series. It can be combined with `outlier.exclLast`.

- outlier.exclLast:

  `numeric` specifying the number of periods excluded at the end of the
  series. It can be combined with `outlier.exclFirst`.

- outlier.ao:

  `logical`. If `TRUE`, the automatic detection of additive outliers is
  enabled (`outlier.enabled` must also be set to `TRUE`).

- outlier.tc:

  `logical`. If `TRUE`, the automatic detection of transitory changes is
  enabled (`outlier.enabled` must also be set to `TRUE`).

- outlier.ls:

  `logical`. If `TRUE`, the automatic detection of level shifts is
  enabled (`outlier.enabled` must also be set to `TRUE`).

- outlier.so:

  `logical`. If `TRUE`, the automatic detection of seasonal outliers is
  enabled (`outlier.enabled` must also be set to `TRUE`).

- outlier.usedefcv:

  `logical`. If `TRUE`, the critical value for the outliers' detection
  procedure is automatically determined by the number of observations in
  the outlier detection time span. If `FALSE`, the procedure uses the
  entered critical value (`outlier.cv`).

- outlier.cv:

  `numeric`. The entered critical value for the outliers' detection
  procedure. The modification of this variable is only taken in to
  account when `outlier.usedefcv` is set to `FALSE`.

- outlier.eml:

  `logical` for the exact likelihood estimation method. It controls the
  method applied for a parameter estimation in the intermediate steps of
  the automatic detection and correction of outliers. If `TRUE`, an
  exact likelihood estimation method is used. When `FALSE`, the fast
  Hannan-Rissanen method is used.

- outlier.tcrate:

  `numeric`. The rate of decay for the transitory change outlier.

- automdl.enabled:

  `logical`. If `TRUE`, the automatic modelling of the ARIMA model is
  enabled. If `FALSE`, the parameters of the ARIMA model can be
  specified.

  Control variables for the automatic modelling of the ARIMA model
  (`automdl.enabled` is set to `TRUE`):

- automdl.acceptdefault:

  `logical`. If `TRUE`, the default model (ARIMA(0,1,1)(0,1,1)) may be
  chosen in the first step of the automatic model identification. If the
  Ljung-Box Q statistics for the residuals is acceptable, the default
  model is accepted and no further attempt will be made to identify
  another model.

- automdl.cancel:

  `numeric`, the cancellation limit. If the difference in moduli of an
  AR and an MA roots (when estimating ARIMA(1,0,1)(1,0,1) models in the
  second step of the automatic identification of the differencing
  orders) is smaller than the cancellation limit, the two roots are
  assumed equal and canceled out.

- automdl.ub1:

  `numeric`, the first unit root limit. It is the threshold value for
  the initial unit root test in the automatic differencing procedure.
  When one of the roots in the estimation of the ARIMA(2,0,0)(1,0,0)
  plus mean model, performed in the first step of the automatic model
  identification procedure, is larger than first unit root limit in
  modulus, it is set equal to unity.

- automdl.ub2:

  `numeric`, the second unit root limit. When one of the roots in the
  estimation of the ARIMA(1,0,1)(1,0,1) plus mean model, which is
  performed in the second step of the automatic model identification
  procedure, is larger than second unit root limit in modulus, it is
  checked if there is a common factor in the corresponding AR and MA
  polynomials of the ARMA model that can be canceled (see
  `automdl.cancel`). If there is no cancellation, the AR root is set
  equal to unity (i.e. the differencing order changes).

- automdl.armalimit:

  `numeric`, the arma limit. It is the threshold value for t-statistics
  of ARMA coefficients and the constant term used for the final test of
  model parsimony. If the highest order ARMA coefficient has a t-value
  smaller than this value in magnitude, the order of the model is
  reduced. If the constant term has a t-value smaller than the ARMA
  limit in magnitude, it is removed from the set of regressors.

- automdl.reducecv:

  `numeric`, ReduceCV. The percentage by which the outlier critical
  value will be reduced when an identified model is found to have a
  Ljung-Box statistic with an unacceptable confidence coefficient. The
  parameter should be between 0 and 1, and will only be active when
  automatic outlier identification is enabled. The reduced critical
  value will be set to (1-ReduceCV)xCV, where CV is the original
  critical value.

- automdl.ljungboxlimit:

  `numeric`, the Ljung Box limit, setting the acceptance criterion for
  the confidence intervals of the Ljung-Box Q statistic. If the LjungBox
  Q statistics for the residuals of a final model is greater than Ljung
  Box limit, then the model is rejected, the outlier critical value is
  reduced, and model and outlier identification (if specified) is redone
  with a reduced value.

- automdl.compare:

  `logical`. If `TRUE`, the program compares the model identified by the
  automatic procedure to the default model (ARIMA(0,1,1)(0,1,1)) and the
  model with the best fit is selected. Criteria considered are residual
  diagnostics, the model structure and the number of outliers.

  Control variables for the non-automatic modelling of the ARIMA model
  (`automdl.enabled` is set to `FALSE`):

- arima.mu:

  `logical`. If `TRUE`, the mean is considered as part of the ARIMA
  model.

- arima.p:

  `numeric`. The order of the non-seasonal autoregressive (AR)
  polynomial.

- arima.d:

  `numeric`. The regular differencing order.

- arima.q:

  `numeric`. The order of the non-seasonal moving average (MA)
  polynomial.

- arima.bp:

  `numeric`. The order of the seasonal autoregressive (AR) polynomial.

- arima.bd:

  `numeric`. The seasonal differencing order.

- arima.bq:

  `numeric`. The order of the seasonal moving average (MA) polynomial.

  Control variables for the user-defined ARMA coefficients. Such
  coefficients can be defined for the regular and seasonal
  autoregressive (AR) polynomials and moving average (MA) polynomials.
  The model considers the coefficients only if the procedure for their
  estimation (`arima.coefType`) is provided, and the number of provided
  coefficients matches the sum of (regular and seasonal) AR and MA
  orders (`p,q,bp,bq`).

- arima.coefEnabled:

  `logical`. If `TRUE`, the program uses the user-defined ARMA
  coefficients.

- arima.coef:

  a vector providing the coefficients for the regular and seasonal AR
  and MA polynomials. The length of the vector must be equal to the sum
  of the regular and seasonal AR and MA orders. The coefficients shall
  be provided in the following order: regular AR (*Phi* - `p` elements),
  regular MA (*Theta* - `q` elements), seasonal AR (*BPhi* - `bp`
  elements) and seasonal MA (*BTheta* - `bq` elements). E.g.:
  `arima.coef=c(0.6,0.7)` with `arima.p=1, arima.q=0,arima.bp=1` and
  `arima.bq=0`.

- arima.coefType:

  avector defining the ARMA coefficients estimation procedure. Possible
  procedures are: `"Undefined"` = no use of user-defined input (i.e.
  coefficients are estimated), `"Fixed"` = fixes the coefficients at the
  value provided by the user, `"Initial"` = the value defined by the
  user is used as initial condition. For orders for which the
  coefficients shall not be defined, the `arima.coef` can be set to `NA`
  or `0` or the `arima.coefType` can be set to `"Undefined"`. E.g.:
  `arima.coef = c(-0.8,-0.6,NA)`,
  `arima.coefType = c("Fixed","Fixed","Undefined")`.

- fcst.horizon:

  `numeric`, the forecasting horizon. The length of the forecasts
  generated by the RegARIMA model in periods (positive values) or years
  (negative values). By default, the program generates two years
  forecasts (`fcst.horizon` set to `-2`).

- seats.predictionLength:

  integer: the number of forecasts used in the decomposition. Negative
  values correspond to number of years. Default=-1.

- seats.approx:

  character: the approximation mode. When the ARIMA model estimated by
  TRAMO does not accept an admissible decomposition, SEATS: `"None"` -
  performs an approximation; `"Legacy"` - replaces the model with a
  decomposable one; `"Noisy"` - estimates a new model by adding a white
  noise to the non-admissible model estimated by TRAMO.
  Default="Legacy".

- seats.trendBoundary:

  numeric: the trend boundary. The boundary beyond which an AR root is
  integrated in the trend component. If the modulus of the inverse real
  root is greater than the trend boundary, the AR root is integrated in
  the trend component. Below this value, the root is integrated in the
  transitory component. Possible values \[0,1\]. Default=0.5.

- seats.seasdBoundary:

  numeric: the seasonal boundary. The boundary beyond which a negative
  AR root is integrated in the seasonal component. If the modulus of the
  inverse negative real root is greater (or equal) than Seasonal
  boundary, the AR root is integrated into the seasonal component.
  Otherwise the root is integrated into the trend or transitory
  component. Possible values \[0,1\]. Default=0.8.

- seats.seasdBoundary1:

  numeric: the seasonal boundary (unique). The boundary beyond which a
  negative AR root is integrated in the seasonal component, when the
  root is the unique seasonal root. If the modulus of the inverse
  negative real root is greater (or equal) than Seasonal boundary, the
  AR root is integrated into the seasonal component. Otherwise the root
  is integrated into the trend or transitory component. Possible values
  \[0,1\]. Default=0.8.

- seats.seasTol:

  numeric: the seasonal tolerance. The tolerance (measured in degrees)
  to allocate the AR non-real roots to the seasonal component (if the
  modulus of the inverse complex AR root is greater than the trend
  boundary and the frequency of this root differs from one of the
  seasonal frequencies by less than Seasonal tolerance) or the
  transitory component (otherwise). Possible values in \[0,10\]. Default
  value 2.

- seats.maBoundary:

  numeric: the MA unit root boundary. When the modulus of an estimated
  MA root falls in the range (xl, 1), it is set to xl. Possible values
  \[0.9,1\]. Default=0.95.

- seats.method:

  character: the estimation method for the unobserved components. The
  choice can be made from:

  - `"Burman"`: the default value. May result in a significant
    underestimation of the components' standard deviation, as it may
    become numerically unstable when some roots of the MA polynomial are
    near 1;

  - `"KalmanSmoother"`: it is not disturbed by the (quasi-) unit roots
    in MA;

  - `"McElroyMatrix"`: it has the same stability issues as the Burman's
    algorithm.

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

A two-element list of class `c("SA_spec", "TRAMO_SEATS")`, containing:
(1) an object of class `c("regarima_spec", "TRAMO_SEATS")` with the
RegARIMA model specification, (2) an object of class
`c("seats_spec", "data.frame")` with the SEATS algorithm specification.
Each component refers to a different part of the SA model specification,
mirroring the arguments of the function (for details see the function
arguments in the description). Each lowest-level component (except span,
pre-specified outliers, user-defined variables and pre-specified ARMA
coefficients) is structured as a data frame with columns denoting
different variables of the model specification and rows referring to:

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

- `regarima`: an object of class `c("regarima_spec", "TRAMO_SEATS")`.
  See *Value* of the function
  [`regarima_spec_tramoseats`](regarima_spec_tramoseats.md).

- `seats`: a data.frame of class `c("seats_spec", "data.frame")`,
  containing the *seats* variables in line with the names of the
  arguments variables. The final values can also be accessed with the
  function [`s_seats`](specification.md).

## Details

The available predefined 'JDemetra+' model specifications are described
in the table below:

|                   |                            |                           |                         |                       |              |                |              |
|-------------------|----------------------------|---------------------------|-------------------------|-----------------------|--------------|----------------|--------------|
| **Identifier** \| | **Log/level detection** \| | **Outliers detection** \| | **Calendar effects** \| | **ARIMA**             | RSA0 \|      | *NA* \|        | *NA* \|      |
| *NA* \|           | Airline(+mean)             | RSA1 \|                   | automatic \|            | AO/LS/TC \|           | *NA* \|      | Airline(+mean) | RSA2 \|      |
| automatic \|      | AO/LS/TC \|                | 2 td vars + Easter \|     | Airline(+mean)          | RSA3 \|               | automatic \| | AO/LS/TC \|    | *NA* \|      |
| automatic         | RSA4 \|                    | automatic \|              | AO/LS/TC \|             | 2 td vars + Easter \| | automatic    | RSA5 \|        | automatic \| |
| AO/LS/TC \|       | 7 td vars + Easter \|      | automatic                 | RSAfull \|              | automatic \|          | AO/LS/TC \|  | automatic \|   | automatic    |

## References

More information and examples related to 'JDemetra+' features in the
online documentation: <https://jdemetra-new-documentation.netlify.app/>

## See also

[`tramoseats`](tramoseats.md)

## Examples

``` r
# \donttest{
myseries <- ipi_c_eu[, "FR"]
myspec1 <- tramoseats_spec(spec = c("RSAfull"))
mysa1 <- tramoseats(myseries, spec = myspec1)

# To modify a pre-specified model specification
myspec2 <- tramoseats_spec(spec = "RSAfull", tradingdays.mauto = "Unused",
                           tradingdays.option = "WorkingDays",
                           easter.type = "Standard",
                           automdl.enabled = FALSE, arima.mu = TRUE)
mysa2 <- tramoseats(myseries, spec = myspec2)

# To modify the model specification of a "SA" object
myspec3 <- tramoseats_spec(mysa1, tradingdays.mauto = "Unused",
                           tradingdays.option = "WorkingDays",
                           easter.type = "Standard", automdl.enabled = FALSE, arima.mu = TRUE)
mysa3 <- tramoseats(myseries, myspec3)

# To modify the model specification of a "SA_spec" object
myspec4 <- tramoseats_spec(myspec1, tradingdays.mauto = "Unused",
                           tradingdays.option = "WorkingDays",
                           easter.type = "Standard", automdl.enabled = FALSE, arima.mu = TRUE)
mysa4 <- tramoseats(myseries, myspec4)

# Pre-specified outliers
myspec5 <- tramoseats_spec(spec = "RSAfull",
                           usrdef.outliersEnabled = TRUE,
                           usrdef.outliersType = c("LS", "LS"),
                           usrdef.outliersDate = c("2008-10-01", "2003-01-01"),
                           usrdef.outliersCoef = c(10,-8), transform.function = "None")
s_preOut(myspec5)
#>   type       date coeff
#> 1   LS 2008-10-01    10
#> 2   LS 2003-01-01    -8
mysa5 <- tramoseats(myseries, myspec5)
mysa5
#> RegARIMA
#> y = regression model + arima (2, 1, 0, 1, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)      0.4872      0.051
#> Phi(2)      0.2964      0.051
#> BPhi(1)    -0.2070      0.071
#> BTheta(1)  -0.8048      0.044
#> 
#>              Estimate Std. Error
#> Week days      0.6814      0.039
#> Leap year      1.9125      0.726
#> Easter [6]    -2.4901      0.461
#> TC (4-2020)  -22.4492      2.288
#> TC (3-2020)  -21.2013      2.296
#> AO (5-2011)   12.6414      1.908
#> LS (11-2008) -14.2909      1.954
#> 
#> Fixed outliers: 
#>              Coefficients
#> LS (10-2008)           10
#> LS (1-2003)            -8
#> 
#> 
#> Residual standard error: 2.421 on 347 degrees of freedom
#> Log likelihood = -831.3, aic =  1687 aicc =  1688, bic(corrected for length) = 1.949
#> 
#> 
#> 
#> Decomposition
#> Model
#> AR :  1 + 0.487236 B + 0.296353 B^2 - 0.207019 B^12 - 0.100867 B^13 - 0.061351 B^14 
#> D :  1 - B - B^12 + B^13 
#> MA :  1 - 0.804783 B^12 
#> 
#> 
#> SA
#> AR :  1 - 0.389767 B - 0.130954 B^2 - 0.259902 B^3 
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 1.807789 B + 0.901808 B^2 - 0.269318 B^3 + 0.305238 B^4 - 0.126109 B^5 
#> Innovation variance:  0.434195 
#> 
#> Trend
#> AR :  1 - 0.877002 B 
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 0.714788 B - 0.995207 B^2 + 0.719581 B^3 
#> Innovation variance:  0.02178125 
#> 
#> Seasonal
#> AR :  1 + 0.877002 B + 0.769133 B^2 + 0.674532 B^3 + 0.591566 B^4 + 0.518805 B^5 + 0.454993 B^6 + 0.399030 B^7 + 0.349950 B^8 + 0.306907 B^9 + 0.269159 B^10 + 0.236053 B^11 
#> D :  1 + B + B^2 + B^3 + B^4 + B^5 + B^6 + B^7 + B^8 + B^9 + B^10 + B^11 
#> MA :  1 + 2.178999 B + 3.063892 B^2 + 4.121863 B^3 + 5.003640 B^4 + 5.601993 B^5 + 6.042224 B^6 + 6.245708 B^7 + 6.304190 B^8 + 6.112595 B^9 + 5.879629 B^10 + 5.538195 B^11 + 4.649065 B^12 + 3.623707 B^13 + 2.832188 B^14 + 1.903031 B^15 + 1.111724 B^16 + 0.543666 B^17 + 0.100438 B^18 - 0.158107 B^19 - 0.300012 B^20 - 0.253276 B^21 - 0.169309 B^22 
#> Innovation variance:  0.2937308 
#> 
#> Transitory
#> AR :  1 + 0.487236 B + 0.296353 B^2 
#> MA :  1 + 0.374200 B + B^2 
#> Innovation variance:  0.0004441626 
#> 
#> Irregular
#> Innovation variance:  0.2270517 
#> 
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t           s            i
#> Jan 2020 101.0 103.36086 103.6698  -2.3608556  -0.30898902
#> Feb 2020 100.1 103.77440 103.7591  -3.6743960   0.01526074
#> Mar 2020  91.8  82.68181 103.8823   9.1181885 -21.20051445
#> Apr 2020  66.7  66.03104 104.0672   0.6689644 -38.03612893
#> May 2020  73.7  78.40145 104.3488  -4.7014498 -25.94737674
#> Jun 2020  98.2  87.17684 104.5662  11.0231647 -17.38939710
#> Jul 2020  97.4  92.05260 104.5630   5.3474007 -12.51040945
#> Aug 2020  71.7  96.37053 104.3138 -24.6705259  -7.94324202
#> Sep 2020 104.7  97.23252 103.8686   7.4674839  -6.63612508
#> Oct 2020 106.7  98.61143 103.4107   8.0885663  -4.79928434
#> Nov 2020 101.6 100.11916 103.0293   1.4808373  -2.91011190
#> Dec 2020  96.6  99.92823 102.7128  -3.3282284  -2.78459980
#> 
#> Forecasts:
#>                y_f     sa_f      t_f        s_f         i_f
#> Jan 2021  93.59565 100.9960 102.4996  -7.399679 -1.50358792
#> Feb 2021  97.28250 101.2996 102.3539  -4.015335 -1.05431433
#> Mar 2021 111.80873 101.4867 102.2239  10.324214 -0.73723634
#> Apr 2021 103.12191 101.5917 102.1076   1.532091 -0.51591304
#> May 2021  95.98703 101.6419 102.0033  -5.653012 -0.36144565
#> Jun 2021 112.41967 101.6567 101.9096  10.762935 -0.25290781
#> Jul 2021 103.94320 101.6482 101.8251   2.296412 -0.17699539
#> Aug 2021  78.58807 101.6248 101.7488 -23.036711 -0.12394718
#> Sep 2021 109.12657 101.5928 101.6796   7.534699 -0.08675036
#> Oct 2021 107.23292 101.5558 101.6166   5.678242 -0.06071652
#> Nov 2021 105.47170 101.5165 101.5590   3.956022 -0.04250960
#> Dec 2021  99.15981 101.4766 101.5063  -2.317856 -0.02975541
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         3.137
#>  Seasonal     61.551
#>  Irregular     0.352
#>  TD & Hol.     2.592
#>  Others       30.919
#>  Total        98.551
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.243
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
#>  Residual seasonality (last 3 years)    0.990
#>  f-test on sa (td)                      0.024
#>  f-test on i (td)                       0.089
#> 
#> 
#> Additional output variables
s_preOut(mysa5)
#>   type       date coeff
#> 1   LS 2008-10-01    10
#> 2   LS 2003-01-01    -8

# User-defined calendar regressors
var1 <- ts(rnorm(length(myseries))*10, start = start(myseries), frequency = 12)
var2 <- ts(rnorm(length(myseries))*100, start = start(myseries), frequency = 12)
var<- ts.union(var1, var2)

myspec6 <- tramoseats_spec(spec = "RSAfull", tradingdays.option = "UserDefined",
                           usrdef.varEnabled = TRUE, usrdef.var = var,
                           usrdef.varType = c("Calendar", "Calendar"))
#> Warning: With tradingdays.option = "UserDefined", the parameters tradingdays.leapyear and tradingdays.stocktd are ignored.
s_preVar(myspec6)
#> $series
#>                   var1          var2
#> Jan 1990   8.765031871   -0.04656092
#> Feb 1990  -0.501382118  -11.76236571
#> Mar 1990  22.803903528   18.41482138
#> Apr 1990  13.798105639  -86.12007223
#> May 1990  -5.736360343   77.93108467
#> Jun 1990 -14.168374281  -45.40641716
#> Jul 1990 -12.449074589 -202.86071844
#> Aug 1990   9.000824800   13.74981227
#> Sep 1990  19.894302565  -65.31652495
#> Oct 1990 -27.869752864   72.00350979
#> Nov 1990  -0.231353042   80.84364277
#> Dec 1990   2.041608395   96.24521304
#> Jan 1991   0.442285247   10.31380723
#> Feb 1991   6.270974878   68.63601515
#> Mar 1991  -9.472495541  109.51989336
#> Apr 1991 -11.228269438   18.18922153
#> May 1991  -0.203236495  -19.68754162
#> Jun 1991  12.250255435  -84.80613844
#> Jul 1991   0.830589847 -187.74430764
#> Aug 1991 -18.859151704 -258.61413063
#> Sep 1991  10.569271276   10.80672274
#> Oct 1991   6.129121886 -183.83419463
#> Nov 1991   5.896500909  -12.30852580
#> Dec 1991  -0.664513411   14.74878788
#> Jan 1992  -6.081078807 -143.06464098
#> Feb 1992   9.473045743  -10.59880850
#> Mar 1992   3.931699575   50.31819093
#> Apr 1992  -3.852059312  251.26804489
#> May 1992  -6.092631219  -44.13813498
#> Jun 1992  -3.843851460 -217.89991293
#> Jul 1992  -9.014236692  -67.81489679
#> Aug 1992   8.729458934   72.88472658
#> Sep 1992   5.618212586 -124.34327365
#> Oct 1992 -17.572785220  -58.82719769
#> Nov 1992  -8.121160950  110.85391313
#> Dec 1992   2.386905873  -50.23799876
#> Jan 1993  25.060017195   34.72986863
#> Feb 1993  -9.805871650  174.81467948
#> Mar 1993  15.661250555   46.28553413
#> Apr 1993  -7.588674355   76.78697074
#> May 1993   4.938451044   45.10162329
#> Jun 1993  -3.271504519  -35.25772249
#> Jul 1993  -4.348790398   36.64544857
#> Aug 1993  15.197231060  -48.81248718
#> Sep 1993   0.036778033   87.33900144
#> Oct 1993  -4.023399502  179.87806220
#> Nov 1993 -14.954664332  105.07952142
#> Dec 1993  -9.459855132  217.52306395
#> Jan 1994   9.064295082  -18.35628629
#> Feb 1994 -18.138676228  -68.67930022
#> Mar 1994  -9.517754317    2.52921842
#> Apr 1994  11.268520993   77.70312224
#> May 1994   1.398890649  135.80460668
#> Jun 1994   1.003399767   31.19454244
#> Jul 1994 -12.045286294   99.11976849
#> Aug 1994  -0.834582964  -38.18986462
#> Sep 1994  -7.970822469  -88.02615153
#> Oct 1994  11.015245786    2.30683213
#> Nov 1994   1.084104063   70.83967956
#> Dec 1994 -11.905067990  147.10711674
#> Jan 1995   2.799212761  142.31851069
#> Feb 1995   7.774077731  -73.17572527
#> Mar 1995  -2.210897240 -122.78623180
#> Apr 1995  -1.376768354  -84.65572264
#> May 1995   1.152300433  164.14782427
#> Jun 1995  15.332695729 -253.69827268
#> Jul 1995  -6.557744602  151.49668186
#> Aug 1995   8.583787007  134.44652874
#> Sep 1995 -11.876705517   34.22179953
#> Oct 1995   5.395403804  -32.46704812
#> Nov 1995  -2.663621627  -95.09212602
#> Dec 1995   7.581722346   12.25963233
#> Jan 1996 -10.314020292  220.95975457
#> Feb 1996  10.249315104  130.49280363
#> Mar 1996  -1.452615921  -52.55140662
#> Apr 1996   1.092238302  115.16359225
#> May 1996 -14.785987947   82.61668965
#> Jun 1996 -22.791912223  115.62448319
#> Jul 1996   6.000768904   41.09726943
#> Aug 1996  -3.465781995   -5.60486435
#> Sep 1996  -2.851536719   78.01771348
#> Oct 1996  -6.476521580 -192.31777839
#> Nov 1996 -12.722147004  -27.36494881
#> Dec 1996  -1.751731809   60.37177315
#> Jan 1997 -22.013195775 -131.73483134
#> Feb 1997   5.798759794   95.55886301
#> Mar 1997   0.627964711    1.28535381
#> Apr 1997  17.751245181   29.14360940
#> May 1997  13.836946999 -201.68055585
#> Jun 1997  16.309602864 -159.64884036
#> Jul 1997  -8.083912981   79.05133025
#> Aug 1997   0.955654515   -5.59537712
#> Sep 1997   9.168081903  278.46565380
#> Oct 1997   4.738435430   39.54117043
#> Nov 1997  -3.952457160  269.79624187
#> Dec 1997   4.293985438  105.66101329
#> Jan 1998   8.509307909  178.18693119
#> Feb 1998  -1.703946179  131.86880388
#> Mar 1998  -0.007914038  -72.40831537
#> Apr 1998   8.606414955  -26.32911657
#> May 1998   6.403423802  -34.85907549
#> Jun 1998   1.068762896  -21.32519004
#> Jul 1998 -14.604777644   74.86664662
#> Aug 1998   4.551713753 -300.45498345
#> Sep 1998  12.720846841  -20.57101950
#> Oct 1998 -19.151875806  -14.35167183
#> Nov 1998   2.355890946  131.09571969
#> Dec 1998  10.559143097   76.45732607
#> Jan 1999   4.316772438   56.44685721
#> Feb 1999 -17.459432119  -17.53213851
#> Mar 1999  26.345754763   -0.25746856
#> Apr 1999  -0.308035714   58.87499380
#> May 1999 -22.561887639   17.53171579
#> Jun 1999  18.368225390  139.69229710
#> Jul 1999   4.985355661   82.54166479
#> Aug 1999   1.562468467   55.47305107
#> Sep 1999   5.565016905   54.53779827
#> Oct 1999   6.871069775  -53.63845039
#> Nov 1999 -33.041822297 -183.92675089
#> Dec 1999   8.783299631  -71.23421939
#> Jan 2000  14.611756864   -9.45664557
#> Feb 2000  -1.094066808   24.30159689
#> Mar 2000  13.256063791  102.04461058
#> Apr 2000  11.406805737   92.32619914
#> May 2000  -9.303642146   26.31799404
#> Jun 2000  -1.946233382  -68.75861883
#> Jul 2000   9.240072693   22.08611800
#> Aug 2000  -2.837713588  -55.41037774
#> Sep 2000   6.438188432   55.18463880
#> Oct 2000  12.049299753  -16.18329852
#> Nov 2000  -9.864334772  135.14035346
#> Dec 2000  13.629994009   -0.53331422
#> Jan 2001  -6.371366390 -240.51334407
#> Feb 2001 -12.527051445   98.98093589
#> Mar 2001  -5.751377304 -123.30316799
#> Apr 2001 -16.763008174    2.74105624
#> May 2001   2.628120182  -39.10052334
#> Jun 2001 -14.208832929  240.18101774
#> Jul 2001   7.738467161   55.41959989
#> Aug 2001  -6.301913980   56.07759451
#> Sep 2001 -25.232229681 -143.07888081
#> Oct 2001  10.456761237   25.65309367
#> Nov 2001   7.513402330   44.75129842
#> Dec 2001   7.981608534   90.91545502
#> Jan 2002 -15.676418337  -65.76117921
#> Feb 2002 -11.474768636   25.47812926
#> Mar 2002   4.355867220 -136.29594240
#> Apr 2002  10.532004191 -115.16580441
#> May 2002   9.635066048    9.23561855
#> Jun 2002   6.939309379  -52.61090352
#> Jul 2002  -2.300709516  -94.12824980
#> Aug 2002  -9.355586095 -116.03851187
#> Sep 2002  -9.026203778  146.32167885
#> Oct 2002  -0.308600940 -122.70357371
#> Nov 2002  -8.686782246  128.91223057
#> Dec 2002  21.877875041   52.19834145
#> Jan 2003  15.385301545    3.86469118
#> Feb 2003 -18.820726709    0.54809002
#> Mar 2003   9.158750045  205.09627114
#> Apr 2003  -4.017400140   58.40034881
#> May 2003 -12.568740002  -71.96403767
#> Jun 2003  11.843968692   31.72919743
#> Jul 2003  10.085724636   16.67156540
#> Aug 2003 -10.661521156  250.26785326
#> Sep 2003 -10.802139977   40.04087093
#> Oct 2003 -15.265903705  107.21119854
#> Nov 2003 -13.704004261    5.50009631
#> Dec 2003 -12.935694331   -6.13638601
#> Jan 2004 -29.610297132 -107.64435907
#> Feb 2004  11.255956830   50.43042930
#> Mar 2004   0.040275376   53.62245498
#> Apr 2004   1.626711541 -135.49772917
#> May 2004 -14.839223699   22.75063071
#> Jun 2004  11.648603184 -252.94187083
#> Jul 2004 -12.724193004  -81.85311433
#> Aug 2004 -11.137786657 -158.95299935
#> Sep 2004 -13.069370448 -108.24933233
#> Oct 2004  -1.742082303   20.58043597
#> Nov 2004  -6.832515233 -108.11823198
#> Dec 2004  -6.215682860  -18.87925541
#> Jan 2005  -1.551632320   31.27564538
#> Feb 2005 -10.864935828    7.47169985
#> Mar 2005   5.502220067  -60.43448541
#> Apr 2005  13.947806779    4.52466495
#> May 2005 -15.883192579  164.85396371
#> Jun 2005  20.675835289  -75.56829840
#> Jul 2005 -16.971130469  -28.81793527
#> Aug 2005   8.605076312  -73.01505059
#> Sep 2005  -3.796434887   52.41485203
#> Oct 2005  18.476301068  -59.17005292
#> Nov 2005  10.376561791 -118.39119861
#> Dec 2005 -14.695747682  120.03531317
#> Jan 2006 -27.769482100  -90.80713269
#> Feb 2006  -0.769797878 -154.88176869
#> Mar 2006  -9.544920721   40.80449528
#> Apr 2006   7.086794196   87.23428206
#> May 2006  17.770868082 -186.04776905
#> Jun 2006   8.663143079   20.61176045
#> Jul 2006   1.530058172 -106.55260009
#> Aug 2006  -0.463890794   44.42791106
#> Sep 2006 -16.728474148   39.00637392
#> Oct 2006 -10.898906119  -11.94045102
#> Nov 2006  -0.761757047  147.49626484
#> Dec 2006 -13.058317158 -129.46582609
#> Jan 2007  -0.623845628 -146.76126825
#> Feb 2007   3.423715685  -21.13007304
#> Mar 2007  -5.489306150   41.96187254
#> Apr 2007   9.150613267  143.33403558
#> May 2007  -0.876039035  -73.74681135
#> Jun 2007  -0.255794707  -12.50153428
#> Jul 2007 -12.543574063   27.98241470
#> Aug 2007  18.801248228  -44.73720260
#> Sep 2007  -1.409493686    4.79576801
#> Oct 2007  -1.066911374  109.28525350
#> Nov 2007   7.245550904   50.80096757
#> Dec 2007   4.288180835  -86.99107994
#> Jan 2008 -15.802157511  -70.26764757
#> Feb 2008   7.747558144 -135.94072699
#> Mar 2008 -11.642921245   34.56469912
#> Apr 2008   0.088543033   42.18054806
#> May 2008  -4.550780017   32.67116657
#> Jun 2008 -10.026900477  -96.35751113
#> Jul 2008   4.280695718   47.86579776
#> Aug 2008   2.025623016   78.05649166
#> Sep 2008   1.815832754  -18.54254995
#> Oct 2008   5.656938676  -37.14157620
#> Nov 2008  -2.776569799  -37.59064151
#> Dec 2008 -13.642484813 -104.97730923
#> Jan 2009  12.992072495   13.55098866
#> Feb 2009 -19.928465574 -104.19342492
#> Mar 2009  -1.037160872  137.15434613
#> Apr 2009   2.997662573   21.17230202
#> May 2009  -4.030004095  -41.99902912
#> Jun 2009   3.384909572  -51.45817426
#> Jul 2009 -14.784270394  -48.11891408
#> Aug 2009  -0.465149259   -2.28961166
#> Sep 2009   0.316881860  -23.58173751
#> Oct 2009   2.815326072   -4.29158886
#> Nov 2009   8.031952537  -53.34721852
#> Dec 2009  -2.088583488   24.09236569
#> Jan 2010  -3.367281762   27.57879994
#> Feb 2010  -4.563097517   98.73378846
#> Mar 2010  10.242603097  -60.71750184
#> Apr 2010  14.573951507  -24.31552344
#> May 2010  -2.249305874  -18.37188962
#> Jun 2010   2.900685098   56.45491125
#> Jul 2010   2.592765437  -64.56633054
#> Aug 2010   0.098922998 -198.41975169
#> Sep 2010  -1.846739254  -93.28107935
#> Oct 2010  16.542465847  186.45597497
#> Nov 2010   4.368543558   30.76683344
#> Dec 2010   8.473161118 -187.34768073
#> Jan 2011   9.962823002 -138.15863726
#> Feb 2011  10.674524423  121.42810047
#> Mar 2011  -0.533425785   14.14819037
#> Apr 2011   9.929262251    6.31038506
#> May 2011  -4.993526848  123.54612674
#> Jun 2011 -11.163933292 -109.65462143
#> Jul 2011  -9.745167645  -67.87837062
#> Aug 2011  27.874035400  -55.98672378
#> Sep 2011  -7.733134688   21.54763562
#> Oct 2011  34.805397484 -205.54352012
#> Nov 2011  -6.174219736  -52.04086283
#> Dec 2011   5.207824425   25.22639057
#> Jan 2012   5.925402530   15.31564241
#> Feb 2012  -9.003468488   49.21244244
#> Mar 2012  14.742813210   53.38223818
#> Apr 2012  10.851326027  -20.71323619
#> May 2012 -17.066874385    3.51198991
#> Jun 2012 -11.686962998 -112.09760249
#> Jul 2012 -14.194533339  -33.19658718
#> Aug 2012   6.459709494 -127.72551270
#> Sep 2012  -4.271327890   53.86513275
#> Oct 2012  11.898281468  134.88412839
#> Nov 2012  -1.398591424   60.11115022
#> Dec 2012   1.893959765   -1.27195862
#> Jan 2013   0.575844052   71.61389956
#> Feb 2013  -5.872461267   40.56344197
#> Mar 2013  -2.414145797  -35.48522938
#> Apr 2013   7.638003907  -83.12560816
#> May 2013  -6.780967332   22.50229021
#> Jun 2013   8.369941394  -68.84118696
#> Jul 2013   0.419394664  -64.87876143
#> Aug 2013   9.793095986   47.17313456
#> Sep 2013  14.960956543   17.46062477
#> Oct 2013  13.811671565  -39.32748689
#> Nov 2013   1.771868508   12.32405780
#> Dec 2013  -6.045588857 -200.66676498
#> Jan 2014  -0.064125536  120.97835399
#> Feb 2014 -10.309176045   14.03724416
#> Mar 2014  -5.966193013  -87.58278740
#> Apr 2014  12.300053344   96.23647351
#> May 2014 -21.252639407  119.02676925
#> Jun 2014   5.465412848   19.19778176
#> Jul 2014  10.114553407 -182.76005309
#> Aug 2014  13.671746024  -84.00768199
#> Sep 2014   7.078379701  162.33939897
#> Oct 2014  -1.225158540   16.00414539
#> Nov 2014  -7.994091347  160.01512693
#> Dec 2014  -1.793600041   11.42747080
#> Jan 2015   1.094528569 -136.54245494
#> Feb 2015   2.309265529   43.85387343
#> Mar 2015 -12.696631620  -96.15072720
#> Apr 2015   6.205258113  121.63488867
#> May 2015  -6.423485204  -78.07119719
#> Jun 2015   6.623578138  -68.22932097
#> Jul 2015   2.458842772 -224.34263707
#> Aug 2015  -8.478936872   18.02763931
#> Sep 2015  -4.347674107   78.15066352
#> Oct 2015   8.831759490  -95.72313412
#> Nov 2015   5.863186803    9.14070547
#> Dec 2015  -2.566920407  -41.57419781
#> Jan 2016  12.201357048  -66.14235523
#> Feb 2016  23.258879673   68.39716351
#> Mar 2016 -13.070423363   89.23843412
#> Apr 2016   0.002714681  -72.69075674
#> May 2016  11.425115700  101.57440260
#> Jun 2016  -2.219401352  -39.55934314
#> Jul 2016  -2.083145925  215.95110680
#> Aug 2016   7.499227118  221.55815780
#> Sep 2016   1.176056177  -25.57170694
#> Oct 2016   0.990212037   30.22917004
#> Nov 2016  13.616884687  -66.58050504
#> Dec 2016  -8.389882385  -69.60612070
#> Jan 2017 -10.649372190   68.33419337
#> Feb 2017  21.131680157  -58.92748703
#> Mar 2017   5.106671868   -7.40935495
#> Apr 2017  12.002630345 -111.22710265
#> May 2017  10.454600553  -59.10622513
#> Jun 2017   7.204436071   85.69446096
#> Jul 2017   5.029684073   50.88933898
#> Aug 2017   9.558412135   39.71038981
#> Sep 2017   4.921280559   38.67572514
#> Oct 2017  -1.559494684   37.01361846
#> Nov 2017  -4.330621776  103.67230979
#> Dec 2017 -12.234203505  235.87650580
#> Jan 2018  -2.903433729  -91.36020752
#> Feb 2018   3.402319889  127.55994229
#> Mar 2018   2.345520557 -143.90900919
#> Apr 2018   0.118239369    3.81422070
#> May 2018   6.047329872  -50.35721949
#> Jun 2018   7.375097630 -171.31774452
#> Jul 2018  -8.981034882   75.24516306
#> Aug 2018   1.718213563  -88.34021094
#> Sep 2018   9.132347891   13.65187786
#> Oct 2018 -11.051534547   42.62818848
#> Nov 2018   3.934501445  -92.51397505
#> Dec 2018 -13.698426711  -96.90957364
#> Jan 2019   7.394716153  -22.65827784
#> Feb 2019   6.383709370  -97.82239636
#> Mar 2019 -22.803538615  -53.33541279
#> Apr 2019 -20.112246984   86.63929336
#> May 2019  20.687405597  -49.33809414
#> Jun 2019 -13.150525575 -122.86158387
#> Jul 2019 -11.097503996  128.45631501
#> Aug 2019   0.548967197  121.17801722
#> Sep 2019  -8.625873906    1.78670750
#> Oct 2019   9.307754912  170.02477760
#> Nov 2019   5.711704007  134.41153529
#> Dec 2019  12.348319265   24.72495028
#> Jan 2020   4.620031264   -9.58509945
#> Feb 2020  -7.342081944  -10.58947708
#> Mar 2020  13.233606241 -126.11547136
#> Apr 2020   4.572947704 -176.02103994
#> May 2020  -7.364807522  179.14308123
#> Jun 2020  21.436128315  -80.10345784
#> Jul 2020  -3.381593680  -55.79331805
#> Aug 2020  -0.709703999   75.61174887
#> Sep 2020  -0.882100204   -6.56542801
#> Oct 2020   3.550907169  140.38251009
#> Nov 2020 -12.048084555   80.61231085
#> Dec 2020  14.560005038  -12.53344382
#> 
#> $description
#>          type coeff
#> var1 Calendar    NA
#> var2 Calendar    NA
#> 
mysa6 <- tramoseats(myseries, myspec6)
#> Warning: [decomposition.Model decomposition: Parameters cut off]

myspec7 <- tramoseats_spec(spec = "RSAfull", usrdef.varEnabled = TRUE,
                           usrdef.var = var, usrdef.varCoef = c(17,-1),
                           transform.function = "None")
mysa7 <- tramoseats(myseries, myspec7)
#> Warning: [decomposition.Model decomposition: Parameters cut off]

# Pre-specified ARMA coefficients
myspec8 <- tramoseats_spec(spec = "RSAfull",
                           arima.coefEnabled = TRUE, automdl.enabled = FALSE,
                           arima.p = 2, arima.q = 0,
                           arima.bp = 1, arima.bq = 1,
                           arima.coef = c(-0.12, -0.12, -0.3, -0.99),
                           arima.coefType = rep("Fixed", 4))
mysa8 <- tramoseats(myseries, myspec8)
#> Warning: [decomposition.Model decomposition: Parameters cut off]
mysa8
#> RegARIMA
#> y = regression model + arima (2, 1, 0, 1, 1, 1)
#> Log-transformation: no
#> Coefficients:
#>           Estimate Std. Error
#> Phi(1)       -0.12          0
#> Phi(2)       -0.12          0
#> BPhi(1)      -0.30          0
#> BTheta(1)    -0.99          0
#> 
#>                Estimate Std. Error
#> Mean          -0.007018      0.029
#> Week days      0.704716      0.029
#> Leap year      2.163501      0.675
#> Easter [6]    -2.360603      0.385
#> TC (4-2020)  -25.280857      2.517
#> TC (3-2020)  -21.581618      2.569
#> AO (5-2011)   14.219490      1.749
#> LS (11-2008)  -6.225300      2.608
#> 
#> 
#> Residual standard error: 2.712 on 350 degrees of freedom
#> Log likelihood = -882.9, aic =  1784 aicc =  1784, bic(corrected for length) = 2.127
#> 
#> 
#> 
#> Decomposition
#> Model
#> AR :  1 - 0.120000 B - 0.120000 B^2 - 0.300000 B^12 + 0.036000 B^13 + 0.036000 B^14 
#> D :  1 - B - B^12 + B^13 
#> MA :  1 - 0.950000 B^12 
#> 
#> 
#> SA
#> AR :  1 - 1.024538 B - 0.011455 B^2 + 0.108545 B^3 
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 1.941460 B + 0.995458 B^2 + 0.036596 B^3 - 0.098708 B^4 + 0.008921 B^5 
#> Innovation variance:  0.4957156 
#> 
#> Trend
#> AR :  1 - 0.904538 B 
#> D :  1 - 2.000000 B + B^2 
#> MA :  1 - 0.722193 B - 0.998833 B^2 + 0.723360 B^3 
#> Innovation variance:  0.1026625 
#> 
#> Seasonal
#> AR :  1 + 0.904538 B + 0.818189 B^2 + 0.740083 B^3 + 0.669433 B^4 + 0.605527 B^5 + 0.547723 B^6 + 0.495436 B^7 + 0.448140 B^8 + 0.405360 B^9 + 0.366664 B^10 + 0.331661 B^11 
#> D :  1 + B + B^2 + B^3 + B^4 + B^5 + B^6 + B^7 + B^8 + B^9 + B^10 + B^11 
#> MA :  1 + 2.915179 B + 5.617938 B^2 + 8.595374 B^3 + 11.505684 B^4 + 14.135215 B^5 + 16.348945 B^6 + 18.036965 B^7 + 19.197199 B^8 + 19.965176 B^9 + 20.301074 B^10 + 20.149549 B^11 + 19.110304 B^12 + 17.206569 B^13 + 14.558551 B^14 + 11.650924 B^15 + 8.806927 B^16 + 6.228869 B^17 + 4.044510 B^18 + 2.357558 B^19 + 1.170033 B^20 + 0.354583 B^21 - 0.052292 B^22 
#> Innovation variance:  0.2584115 
#> 
#> Transitory
#> AR :  1 - 0.120000 B - 0.120000 B^2 
#> MA :  1 + 1.287572 B + 0.287572 B^2 
#> Innovation variance:  9.66767e-06 
#> 
#> Irregular
#> Innovation variance:  0.1228651 
#> 
#> 
#> 
#> Final
#> Last observed values
#>              y        sa        t          s            i
#> Jan 2020 101.0 104.26082 104.1042  -3.260821   0.15661216
#> Feb 2020 100.1 104.61371 104.5530  -4.513714   0.06076253
#> Mar 2020  91.8  83.22384 104.8133   8.576159 -21.58942879
#> Apr 2020  66.7  64.54936 105.1877   2.150645 -40.63830016
#> May 2020  73.7  77.68315 105.6408  -3.983146 -27.95763593
#> Jun 2020  98.2  85.98531 105.6977  12.214693 -19.71243272
#> Jul 2020  97.4  91.30785 105.6878   6.092154 -14.37997103
#> Aug 2020  71.7  96.93855 105.3429 -25.238546  -8.40432490
#> Sep 2020 104.7  96.44550 104.0342   8.254501  -7.58868184
#> Oct 2020 106.7  97.99258 103.1705   8.707420  -5.17788550
#> Nov 2020 101.6 100.37821 102.7766   1.221785  -2.39834446
#> Dec 2020  96.6  98.88800 101.7659  -2.287995  -2.87795452
#> 
#> Forecasts:
#>                y_f     sa_f       t_f         s_f         i_f
#> Jan 2021  90.45630 99.25146 100.88131  -8.3529406 -1.62984885
#> Feb 2021  92.96291 99.26414 100.40502  -5.6858753 -1.14087970
#> Mar 2021 107.94414 99.16721  99.96582   9.4108234 -0.79860872
#> Apr 2021 100.06082 99.00111  99.56013   1.7251675 -0.55902344
#> May 2021  92.32683 98.79338  99.18469  -5.8047774 -0.39131514
#> Jun 2021 109.76210 98.56264  98.83656  11.5896516 -0.27391913
#> Jul 2021  99.28583 98.32134  98.51308   1.7410215 -0.19174293
#> Aug 2021  72.73390 98.07763  98.21185 -24.3850120 -0.13421991
#> Sep 2021 105.42789 97.83673  97.93068   8.1237153 -0.09395290
#> Oct 2021 103.20722 97.60185  97.66762   6.1153709 -0.06576632
#> Nov 2021 101.03104 97.37483  97.42087   4.2605212 -0.04603637
#> Dec 2021  96.56590 97.15661  97.18883  -0.4705564 -0.03222456
#> 
#> 
#> Diagnostics
#> Relative contribution of the components to the stationary
#> portion of the variance in the original series,
#> after the removal of the long term trend
#>  Trend computed by Hodrick-Prescott filter (cycle length = 8.0 years)
#>            Component
#>  Cycle         3.408
#>  Seasonal     72.835
#>  Irregular     0.303
#>  TD & Hol.     3.240
#>  Others       18.296
#>  Total        98.081
#> 
#> Combined test in the entire series
#>  Non parametric tests for stable seasonality
#>                                                           P.value
#>    Kruskall-Wallis test                                      0.000
#>    Test for the presence of seasonality assuming stability   0.000
#>    Evolutive seasonality test                                0.072
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
#>  Residual seasonality (last 3 years)    0.881
#>  f-test on sa (td)                      0.008
#>  f-test on i (td)                       0.052
#> 
#> 
#> Additional output variables
s_arimaCoef(myspec8)
#>            Type Value
#> Phi(1)    Fixed -0.12
#> Phi(2)    Fixed -0.12
#> BPhi(1)   Fixed -0.30
#> BTheta(1) Fixed -0.99
s_arimaCoef(mysa8)
#>            Type Value
#> Phi(1)    Fixed -0.12
#> Phi(2)    Fixed -0.12
#> BPhi(1)   Fixed -0.30
#> BTheta(1) Fixed -0.99
# }
```
