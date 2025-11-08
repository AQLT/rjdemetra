# RegARIMA model specification, pre-adjustment in TRAMO-SEATS

Function to create (and/or modify) a `c("regarima_spec","TRAMO_SEATS")`
class object with the RegARIMA model specification for the TRAMO-SEATS
method. The object can be created from the name (`character`) of a
predefined 'JDemetra+' model specification, a previous specification
(`c("regarima_spec","TRAMO_SEATS")` object) or a TRAMO-SEATS RegARIMA
model (`c("regarima","TRAMO_SEATS")`).

## Usage

``` r
regarima_spec_tramoseats(
  spec = c("TRfull", "TR0", "TR1", "TR2", "TR3", "TR4", "TR5"),
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
  fcst.horizon = NA_integer_
)
```

## Arguments

- spec:

  the model specification. It can be the name (`character`) of a
  predefined 'JDemetra+' model specification (see *Details*), an object
  of class `c("regarima_spec","TRAMO_SEATS")` or an object of class
  `c("regarima", "TRAMO_SEATS")`. The default is `"TRfull"`.

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

## Value

A list of class `c("regarima_spec","TRAMO_SEATS")` with the following
components, each referring to a different part of the RegARIMA model
specification, mirroring the arguments of the function (for details, see
the arguments description). Each lowest-level component (except the
span, pre-specified outliers, user-defined variables and pre-specified
ARMA coefficients) is structured within a data frame with columns
denoting different variables of the model specification and rows
referring to: first row = the base specification, as provided within the
argument `spec`; second row = user modifications as specified by the
remaining arguments of the function (e.g.: `arima.d`); and third row =
the final model specification, values that will be used in the function
[`regarima`](regarima.md). The final specification (third row) shall
include user modifications (row two) unless they were wrongly specified.
The pre-specified outliers, user-defined variables and pre-specified
ARMA coefficients consist of a list with the `Predefined` (base model
specification) and `Final` values.

- estimate:

  a data frame containing Variables referring to: `span` - time span to
  be used for the estimation, `tolerance` - argument `estimate.tol`,
  `exact_ml` - argument `estimate.eml`, `urfinal` - argument
  `esimate.urfinal`. The final values can be also accessed with the
  function [`s_estimate`](specification.md).

- transform:

  a data frame containing variables referring to: `tfunction` - argument
  `transform.function`, `fct` - argument `transform.fct`. The final
  values can be also accessed with the function
  [`s_transform`](specification.md).

- regression:

  a list containing information on the user-defined variables
  (`userdef`), `trading.days` effect and `easter` effect. The
  user-defined part includes: `specification` - data frame with the
  information if pre-specified outliers (`outlier`) and user-defined
  variables (`variables`) are included in the model and if fixed
  coefficients are used (`outlier.coef` and `variables.coef`). The final
  values can be also accessed with the function
  [`s_usrdef`](specification.md); `outliers` - matrixes with the
  outliers (`Predefined` and `Final`). The final outliers can be also
  accessed with the function [`s_preOut`](specification.md); and
  `variables` - list with the `Predefined` and `Final` user-defined
  variables (`series`) and its description (`description`) including
  information on the variable type and values of fixed coefficients. The
  final user-defined variables can be also accessed with the function
  [`s_preVar`](specification.md).

  The `trading.days` data frame variables refer to: `automatic` -
  argument `tradingdays.mauto`, `pftd` - argument `tradingdays.pftd`,
  `option` - argument `tradingdays.option`, `leapyear` - argument
  `tradingdays.leapyear`, `stocktd` - argument `tradingdays.stocktd`,
  `test` - argument `tradingdays.test`. The final `trading.days` values
  can be also accessed with the function [`s_td`](specification.md). The
  `easter` data frame variables refer to: `type` - argument
  `easter.type`, `julian` - argument `easter.julian`, `duration` -
  argument `easter.duration`, `test` - argument `easter.test`. The final
  `easter` values can be also accessed with the function
  [`s_easter`](specification.md).

- outliers:

  a data frame. Variables referring to: `ao` - argument `outlier.ao`,
  `tc` - argument `outlier.tc`, `ls` - argument `outlier.ls`, `so` -
  argument `outlier.so`, `usedefcv` - argument `outlier.usedefcv`,
  `cv` - argument `outlier.cv`, `eml` - argument `outlier.eml`,
  `tcrate` - argument `outlier.tcrate`. The final values can be also
  accessed with the function [`s_out`](specification.md).

- arima:

  a list containing a data frame with the ARIMA settings
  (`specification`) and matrices giving information on the pre-specified
  ARMA coefficients (`coefficients`). The matrix `Predefined` refers to
  the pre-defined model specification and matrix `Final`, to the final
  specification. Both matrices contain the values of the ARMA
  coefficients and the procedure for its estimation. In the data frame
  `specification`, the variable `enabled` refers to the argument
  `automdl.enabled` and all remaining variables
  (`automdl.acceptdefault, automdl.cancel, automdl.ub1, automdl.ub2, automdl.armalimit, automdl.reducecv, automdl.ljungboxlimit, automdl.compare, arima.mu, arima.p, arima.d, arima.q, arima.bp, arima.bd, arima.bq`),
  to the respective function arguments. The final values of the
  `specification` can be also accessed with the function
  [`s_arima`](specification.md), and final pre-specified ARMA
  coefficients with the function [`s_arimaCoef`](specification.md).

- forecast:

  a data frame with the forecasting horizon (argument `fcst.horizon`).
  The final value can be also accessed with the function
  [`s_fcst`](specification.md).

- span:

  a matrix containing the final time span for the model estimation and
  outliers' detection. It contains the same information as the variable
  span in the data frames estimate and outliers. The matrix can be also
  accessed with the function [`s_span`](specification.md).

## Details

The available predefined 'JDemetra+' model specifications are described
in the table below:

|                   |                            |                           |                         |                       |              |                |              |
|-------------------|----------------------------|---------------------------|-------------------------|-----------------------|--------------|----------------|--------------|
| **Identifier** \| | **Log/level detection** \| | **Outliers detection** \| | **Calendar effects** \| | **ARIMA**             | TR0 \|       | *NA* \|        | *NA* \|      |
| *NA* \|           | Airline(+mean)             | TR1 \|                    | automatic \|            | AO/LS/TC \|           | *NA* \|      | Airline(+mean) | TR2 \|       |
| automatic \|      | AO/LS/TC \|                | 2 td vars + Easter \|     | Airline(+mean)          | TR3 \|                | automatic \| | AO/LS/TC \|    | *NA* \|      |
| automatic         | TR4 \|                     | automatic \|              | AO/LS/TC \|             | 2 td vars + Easter \| | automatic    | TR5 \|         | automatic \| |
| AO/LS/TC \|       | 7 td vars + Easter \|      | automatic                 | TRfull \|               | automatic \|          | AO/LS/TC \|  | automatic \|   | automatic    |

## References

More information and examples related to 'JDemetra+' features in the
online documentation: <https://jdemetra-new-documentation.netlify.app/>

## Examples

``` r
# \donttest{
myseries <- ipi_c_eu[, "FR"]
myspec1 <- regarima_spec_tramoseats(spec = "TRfull")
myreg1 <- regarima(myseries, spec = myspec1)

 # To modify a pre-specified model specification
myspec2 <- regarima_spec_tramoseats(spec = "TRfull",
             tradingdays.mauto = "Unused",
             tradingdays.option = "WorkingDays",
             easter.type = "Standard",
             automdl.enabled = FALSE, arima.mu = TRUE)
myreg2 <- regarima(myseries, spec = myspec2)

 # To modify the model specification of a "regarima" object
myspec3 <- regarima_spec_tramoseats(myreg1,
             tradingdays.mauto = "Unused",
             tradingdays.option = "WorkingDays",
             easter.type = "Standard", automdl.enabled = FALSE,
             arima.mu = TRUE)
myreg3 <- regarima(myseries, myspec3)

 # To modify the model specification of a "regarima_spec" object
myspec4 <- regarima_spec_tramoseats(myspec1,
             tradingdays.mauto = "Unused",
             tradingdays.option = "WorkingDays",
             easter.type = "Standard",
             automdl.enabled = FALSE, arima.mu = TRUE)
myreg4 <- regarima(myseries, myspec4)

 # Pre-specified outliers
myspec1 <- regarima_spec_tramoseats(spec = "TRfull",
             usrdef.outliersEnabled = TRUE,
             usrdef.outliersType = c("LS", "LS"),
             usrdef.outliersDate = c("2008-10-01" ,"2003-01-01"),
             usrdef.outliersCoef = c(10, -8), transform.function = "None")
s_preOut(myspec1)
#>   type       date coeff
#> 1   LS 2008-10-01    10
#> 2   LS 2003-01-01    -8
myreg1 <- regarima(myseries, myspec1)
myreg1
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
s_preOut(myreg1)
#>   type       date coeff
#> 1   LS 2008-10-01    10
#> 2   LS 2003-01-01    -8


 # User-defined variables
var1 <- ts(rnorm(length(myseries))*10, start = start(myseries),
           frequency = 12)
var2 <- ts(rnorm(length(myseries))*100, start = start(myseries),
           frequency = 12)
var <- ts.union(var1, var2)

myspec1 <- regarima_spec_tramoseats(spec = "TRfull",
            usrdef.varEnabled = TRUE, usrdef.var = var)
s_preVar(myspec1)
#> $series
#>                 var1         var2
#> Jan 1990   2.0236067   -8.0085080
#> Feb 1990  -7.1753865 -142.2369549
#> Mar 1990   3.6169476  110.8148963
#> Apr 1990  13.9900429  107.8477638
#> May 1990   3.7269896  -44.0250341
#> Jun 1990 -15.6564429  -77.8169014
#> Jul 1990  -0.5169454 -181.8590012
#> Aug 1990   5.1408210 -112.4080904
#> Sep 1990   5.4989952  106.0523843
#> Oct 1990   8.6781691 -147.8700159
#> Nov 1990   6.8436008 -155.1560169
#> Dec 1990  -1.6267998   77.7506675
#> Jan 1991 -17.8436472  106.8440137
#> Feb 1991 -10.3714557  -18.3587701
#> Mar 1991   8.3014772  155.8242931
#> Apr 1991   6.0734694  -21.3242384
#> May 1991  -1.2218636   93.0535264
#> Jun 1991   9.3312514   41.0811796
#> Jul 1991  -9.6127668 -127.9844298
#> Aug 1991   2.5508171  -78.2366628
#> Sep 1991  -5.4540157 -227.6083450
#> Oct 1991   9.3036074  -12.6395908
#> Nov 1991  -5.3765056  144.8146707
#> Dec 1991  -4.5242607 -144.2757372
#> Jan 1992  -4.3929097  146.7187177
#> Feb 1992  -6.1622311  -74.3299901
#> Mar 1992   4.4163455  -30.4223839
#> Apr 1992   4.8259745   33.7658063
#> May 1992   5.4214438  -60.7502085
#> Jun 1992 -22.9078465  -29.5560270
#> Jul 1992   3.1035185  -13.4537140
#> Aug 1992  14.0407898   81.4784367
#> Sep 1992  13.7711764  -27.2921733
#> Oct 1992  10.6039565  215.9485797
#> Nov 1992   6.3217289  109.1737569
#> Dec 1992  10.8492804   74.3384845
#> Jan 1993  13.5645944 -120.7859353
#> Feb 1993   3.6242404   32.7818052
#> Mar 1993  21.6934446  -53.4165106
#> Apr 1993   1.3913051  128.3946719
#> May 1993  13.7632653    2.8931340
#> Jun 1993  -4.9144999  -39.5677069
#> Jul 1993  15.3491576  -69.4868327
#> Aug 1993  -4.1619872 -149.2080701
#> Sep 1993  -5.2054380  144.4257235
#> Oct 1993   8.5058387  -34.7017388
#> Nov 1993   3.3449657   -4.0259166
#> Dec 1993  -8.2935177  124.6632110
#> Jan 1994  -2.1869594 -134.6301524
#> Feb 1994 -15.4508372  -57.3901281
#> Mar 1994   2.3322978  -70.5959250
#> Apr 1994   0.3106964 -185.7404541
#> May 1994   3.5786565  -24.6970481
#> Jun 1994  16.0862422  -33.5560929
#> Jul 1994  14.2985426  -24.9376870
#> Aug 1994  -9.4833964   45.9522561
#> Sep 1994  10.1570554  -46.0075481
#> Oct 1994   0.3773461    5.8932798
#> Nov 1994 -17.4423940  -74.2591082
#> Dec 1994  -9.7007381 -216.3574004
#> Jan 1995  -2.2902736  -23.2896492
#> Feb 1995  -9.7484568   87.4906829
#> Mar 1995  26.9237242  -97.3494027
#> Apr 1995  13.9239386  -51.2746864
#> May 1995  13.6007615  -92.3487986
#> Jun 1995  -3.6541588 -149.4425725
#> Jul 1995  -8.6893720  -16.5930360
#> Aug 1995  -5.0655673  158.2238321
#> Sep 1995  12.1470730  101.4602266
#> Oct 1995   5.0695868 -114.6478343
#> Nov 1995 -20.9497131  -90.9849112
#> Dec 1995   0.3407924  310.9182685
#> Jan 1996   8.5272870 -106.9552775
#> Feb 1996   7.4322814  -70.0109518
#> Mar 1996   5.5715361  -19.8444470
#> Apr 1996 -12.4858322   74.3620121
#> May 1996  -2.0787431   -5.0159767
#> Jun 1996   4.2396946  131.3143547
#> Jul 1996  -5.0669744    8.6013515
#> Aug 1996  -6.1152331  -62.9851372
#> Sep 1996  24.1165945   65.5070329
#> Oct 1996  -1.6495814    1.9393549
#> Nov 1996  -4.4040605   69.6269961
#> Dec 1996   5.2197617  200.8869895
#> Jan 1997 -19.1832225   -5.6978283
#> Feb 1997 -19.8264996   24.0415504
#> Mar 1997   5.2120016   -2.1890165
#> Apr 1997   7.7778320  -83.0808160
#> May 1997  -8.1211887  140.2474316
#> Jun 1997   9.1074832  -72.3869110
#> Jul 1997   9.4875395  133.0580365
#> Aug 1997 -13.4804945  -81.1333019
#> Sep 1997   3.5417586  179.5036105
#> Oct 1997   5.3026393   68.6626326
#> Nov 1997  -3.1097493    8.9378001
#> Dec 1997  -2.4415553   32.4547737
#> Jan 1998  -2.9187819    7.1318125
#> Feb 1998 -11.2808616   23.3048376
#> Mar 1998 -11.2288159  198.6376577
#> Apr 1998  20.5393864  -95.1670789
#> May 1998  -9.0951843  -55.8642319
#> Jun 1998   4.5837916   25.5814543
#> Jul 1998  -0.4661845  -19.8076172
#> Aug 1998  -6.8095460   42.8789144
#> Sep 1998 -14.8882940    7.0770111
#> Oct 1998  -3.9251301 -153.6653804
#> Nov 1998 -17.4968202   45.3984370
#> Dec 1998  -0.3866763   87.4398568
#> Jan 1999  -7.9715324 -129.7737568
#> Feb 1999  -9.1592054 -107.8965237
#> Mar 1999   0.7326746 -113.4849941
#> Apr 1999  12.3817132    2.2614307
#> May 1999   7.1837134   -2.1461225
#> Jun 1999   5.3946650  -27.8772443
#> Jul 1999 -10.6123399   -2.4206406
#> Aug 1999  -5.4073787   82.5020302
#> Sep 1999  -7.1520471  -75.0182780
#> Oct 1999  -1.7892009   53.6210466
#> Nov 1999   1.6497028 -157.2717483
#> Dec 1999  -7.2740817  -98.6427417
#> Jan 2000  -5.3783713  198.3512323
#> Feb 2000  -5.9966490 -185.1378443
#> Mar 2000  11.8208775  -90.9788183
#> Apr 2000   1.8921288 -195.1440016
#> May 2000   2.4894911  -80.0276459
#> Jun 2000  10.4664341 -186.9361599
#> Jul 2000 -12.8930094  -75.0571483
#> Aug 2000   3.7511557  -59.0938385
#> Sep 2000  -5.5691839  -74.2099269
#> Oct 2000   3.0242663   69.3512077
#> Nov 2000   2.2226647   -5.9463974
#> Dec 2000  -9.6216696 -186.3895099
#> Jan 2001   0.5203237 -127.4508920
#> Feb 2001   9.0004038 -178.1770808
#> Mar 2001  -3.9490088  -50.8593389
#> Apr 2001   9.5414600 -173.6878286
#> May 2001  -5.8821435    4.0481303
#> Jun 2001 -14.7658453  -12.4179458
#> Jul 2001 -13.7777577  -61.2753432
#> Aug 2001 -13.4567231   16.0662477
#> Sep 2001  -7.3663796  -66.2359632
#> Oct 2001  -4.7011150  -33.4851661
#> Nov 2001  13.8060934   62.3011586
#> Dec 2001  16.7501093  102.8194292
#> Jan 2002  11.7690663 -113.4578240
#> Feb 2002  -1.4889834   91.6911054
#> Mar 2002  -1.7782336  121.3874789
#> Apr 2002   8.0312186  -68.5932457
#> May 2002  -4.1579535 -109.4568193
#> Jun 2002  12.1248959   36.4874099
#> Jul 2002  12.4036003 -100.8017083
#> Aug 2002   6.8567588   55.4996436
#> Sep 2002  -0.2679868   43.6065921
#> Oct 2002   3.0958051   10.5373296
#> Nov 2002   2.4986433  -25.3737853
#> Dec 2002 -13.5646087  -97.6491232
#> Jan 2003   5.9937977   39.4217766
#> Feb 2003   0.0864779  101.4903026
#> Mar 2003   0.9071661   63.1443810
#> Apr 2003  -6.5705741  -48.3398255
#> May 2003  -4.8178225 -152.6333936
#> Jun 2003   0.1775788   61.6842281
#> Jul 2003  -8.5953576  122.9286839
#> Aug 2003  13.5770498   15.7453027
#> Sep 2003  12.1506118  140.6342056
#> Oct 2003  14.5391292   39.6800917
#> Nov 2003  -0.8591198   32.6422964
#> Dec 2003  -6.1756875 -145.9343308
#> Jan 2004  -2.1826025  -79.9295527
#> Feb 2004 -13.2600521   47.0012796
#> Mar 2004 -23.6220890 -115.0180520
#> Apr 2004 -14.0996955  -27.1596716
#> May 2004   2.5439714   45.7424220
#> Jun 2004   2.9587030   -1.6957936
#> Jul 2004   0.5678979  -54.1594360
#> Aug 2004  -1.0265486   87.5813417
#> Sep 2004  19.5192303   74.0838155
#> Oct 2004   8.7856596  -16.4812388
#> Nov 2004 -13.0661693  -75.0964284
#> Dec 2004   0.9034427 -125.3366291
#> Jan 2005   9.0235804 -103.6236261
#> Feb 2005   5.4942132   -2.9438569
#> Mar 2005  -8.6983920  -27.4943778
#> Apr 2005  -0.3921465   48.5451470
#> May 2005  -5.1845168   91.6982034
#> Jun 2005  -9.1184962  -98.5343916
#> Jul 2005   1.5031364 -149.1189746
#> Aug 2005   4.4035545   81.9592449
#> Sep 2005  13.1978206  101.3404533
#> Oct 2005   2.4656113  105.3605251
#> Nov 2005   9.4182660   -7.1428639
#> Dec 2005  -3.4215133   95.2444607
#> Jan 2006  -2.7614681  -38.4037519
#> Feb 2006   3.8365678  -41.7759992
#> Mar 2006  14.4691022  -47.0268171
#> Apr 2006  17.3390029 -169.0180287
#> May 2006   4.5642938  -94.5497655
#> Jun 2006   7.0750349  -34.3011960
#> Jul 2006  20.6378922   35.8462408
#> Aug 2006   0.2391059    4.8188861
#> Sep 2006   2.4594946  113.0172278
#> Oct 2006   2.7205914  -52.7632312
#> Nov 2006  -9.9245858   47.9575325
#> Dec 2006  -0.2757795  141.7529298
#> Jan 2007  22.2284516   -8.0090773
#> Feb 2007   1.5550390  -39.4187003
#> Mar 2007  -8.6911632   52.5257637
#> Apr 2007 -11.7448945  -79.5935096
#> May 2007 -17.5967731   24.5096448
#> Jun 2007   0.5836159  -77.9319835
#> Jul 2007  11.6451986   59.4923871
#> Aug 2007   3.3762789  110.8890896
#> Sep 2007 -10.5451872  -94.2969030
#> Oct 2007   6.6076911   70.0343989
#> Nov 2007  -8.2340900  -42.4674825
#> Dec 2007   4.3703366 -114.3137603
#> Jan 2008   3.7238811   23.3440224
#> Feb 2008 -16.4674913  -18.9236577
#> Mar 2008 -19.2355227 -166.3411256
#> Apr 2008   3.8083303  191.5690770
#> May 2008  13.7570535  -81.6894436
#> Jun 2008   8.2584873   38.3650493
#> Jul 2008  -4.1611500  -45.8632251
#> Aug 2008   9.8214959  -71.5703978
#> Sep 2008   2.4218073   42.9548541
#> Oct 2008  -9.3792685 -116.9852745
#> Nov 2008  15.0585850  132.2088309
#> Dec 2008 -10.6585117  136.5964636
#> Jan 2009   1.6227053  -24.9723710
#> Feb 2009   2.6047039  -42.4721350
#> Mar 2009 -14.8820199  109.8439335
#> Apr 2009  14.1518387   67.0923041
#> May 2009   5.6250751    3.0954656
#> Jun 2009   6.4205574  236.8511961
#> Jul 2009  -8.9053264  258.5788113
#> Aug 2009  -1.1653752  121.2280955
#> Sep 2009  -9.4197475 -125.1196841
#> Oct 2009  11.1582792   40.0266042
#> Nov 2009   4.7013513   93.4707631
#> Dec 2009   8.6061271  -47.2669846
#> Jan 2010  -0.7039665  158.3013221
#> Feb 2010  -6.1318021   59.7754220
#> Mar 2010  -3.3671496   46.6084586
#> Apr 2010  -2.1584018  -74.4367537
#> May 2010   6.2113229   95.9055258
#> Jun 2010 -12.8402652   15.2637081
#> Jul 2010 -13.0009244  -76.9368697
#> Aug 2010  -3.7676946  139.3080739
#> Sep 2010   1.0374865   91.8668766
#> Oct 2010  -7.0356227  101.6087064
#> Nov 2010  14.9741394   53.4635439
#> Dec 2010  -3.0282688  -98.7628560
#> Jan 2011 -13.7683133  118.7792273
#> Feb 2011   8.8317017  -51.7542212
#> Mar 2011   6.7142028  -25.9560251
#> Apr 2011  12.3002238  -32.8064671
#> May 2011  16.4546788    7.3432395
#> Jun 2011  -1.8292604  -24.7863020
#> Jul 2011 -13.7925781 -137.3862256
#> Aug 2011  12.5060060   -4.0445818
#> Sep 2011 -18.7623677   42.1538239
#> Oct 2011  -3.6878757   20.1597506
#> Nov 2011 -21.2929731 -169.7191918
#> Dec 2011   3.3764603   64.2287683
#> Jan 2012 -15.7457485  -99.5239613
#> Feb 2012  -1.9631941   96.3813900
#> Mar 2012   9.1506011 -165.6037231
#> Apr 2012  10.7863654  107.0861091
#> May 2012  14.5280285  -10.9026360
#> Jun 2012 -16.5328109  189.9186393
#> Jul 2012 -27.6186752 -113.7030733
#> Aug 2012   2.6436916  -27.9719758
#> Sep 2012  10.2457159  -89.4129051
#> Oct 2012  -6.5918555   13.6701846
#> Nov 2012  -3.8630438  -74.9165418
#> Dec 2012  -2.4249895   51.8199077
#> Jan 2013   2.2059324  -19.2337214
#> Feb 2013 -14.8109003    2.8809812
#> Mar 2013   7.2469120   35.8590886
#> Apr 2013 -23.7751470   -2.8995035
#> May 2013  -0.6540921  114.7042072
#> Jun 2013  -4.6970481   37.3588935
#> Jul 2013  -2.8051629   32.3339211
#> Aug 2013   5.7483659  -82.9819320
#> Sep 2013  -2.0567685  139.4462582
#> Oct 2013   2.3488051  -19.1543577
#> Nov 2013   1.1062832   27.2277021
#> Dec 2013   2.7420223 -108.1659008
#> Jan 2014  15.7491963 -232.9399361
#> Feb 2014   5.6776783  -54.9625959
#> Mar 2014  -0.5961225   -7.2579991
#> Apr 2014  -1.4958771  103.2288404
#> May 2014   2.6616879   21.5138526
#> Jun 2014   5.2840324  -49.4340125
#> Jul 2014  -5.7938809  151.2138281
#> Aug 2014   9.4219937  -57.9463264
#> Sep 2014  -7.0636136  167.4789634
#> Oct 2014 -12.7540210 -100.0980259
#> Nov 2014   7.3325992  122.2702835
#> Dec 2014  -4.2020709  107.7188166
#> Jan 2015  -2.5537509  -61.1945460
#> Feb 2015  -3.6923822   50.6866968
#> Mar 2015  12.1244833   46.0068373
#> Apr 2015  -4.4536301  148.4391861
#> May 2015  11.3866752   88.1963226
#> Jun 2015   1.9052348  -53.6702239
#> Jul 2015 -13.6639361  128.5553707
#> Aug 2015 -12.9810260   58.7848533
#> Sep 2015 -21.3709831 -130.8482026
#> Oct 2015  -0.9620553   31.6726325
#> Nov 2015   6.9450905  119.4158303
#> Dec 2015  -4.7459123   91.3057148
#> Jan 2016  17.6313061  -78.6752993
#> Feb 2016  20.2584606  -41.0929700
#> Mar 2016   4.2761881   47.6373682
#> Apr 2016  -5.6647935   18.5915868
#> May 2016  -8.3383531 -132.4716253
#> Jun 2016   3.9825915  117.2371055
#> Jul 2016 -14.7453793   23.1492772
#> Aug 2016  -3.9544120   48.3071904
#> Sep 2016  -1.3070247  -53.5319580
#> Oct 2016 -19.9949395  137.8135819
#> Nov 2016  -9.9593086 -130.2671671
#> Dec 2016   4.2011400   63.4857535
#> Jan 2017  -0.6286163   99.9655161
#> Feb 2017  -0.8013185  -33.7748953
#> Mar 2017  -0.3228341   -8.6033607
#> Apr 2017  -7.1898093 -171.8817584
#> May 2017 -11.1656132  -92.9121572
#> Jun 2017  -7.8026990   81.3676046
#> Jul 2017 -17.7695853   52.6413546
#> Aug 2017  -4.2783487  101.1957390
#> Sep 2017 -20.3102701   83.1379809
#> Oct 2017  27.5076475   41.5134145
#> Nov 2017  15.1366972  -66.1257061
#> Dec 2017   0.3398894   54.8811286
#> Jan 2018   7.4079278  -53.9367800
#> Feb 2018 -12.7080818  -17.1318426
#> Mar 2018  -1.6356423  -76.6734605
#> Apr 2018  -6.1094549  -60.6574846
#> May 2018  12.5188419  164.7312821
#> Jun 2018   2.5031947   84.1069348
#> Jul 2018 -17.0558168   33.8175097
#> Aug 2018  -8.5541313  -40.4883076
#> Sep 2018  -1.4490163   90.0009039
#> Oct 2018  -3.2444696  119.0666655
#> Nov 2018  -1.7256490   -4.7539083
#> Dec 2018 -12.3606292   78.6925425
#> Jan 2019 -19.0230421  116.6684112
#> Feb 2019  -0.9450402  -27.1823871
#> Mar 2019   0.3255579  -31.3704285
#> Apr 2019   4.6129012  -28.6300150
#> May 2019  13.8140030  -80.3440263
#> Jun 2019  -4.1647627   -9.4555455
#> Jul 2019   6.8094267   -7.4046506
#> Aug 2019  -4.1437304   71.4490683
#> Sep 2019  -5.1834551   12.4718366
#> Oct 2019  -6.8401973  129.6594339
#> Nov 2019  -8.8564860 -111.4492926
#> Dec 2019   0.4923707  -84.2058813
#> Jan 2020   1.8556122 -150.4294209
#> Feb 2020  -6.0865779  -28.4026455
#> Mar 2020  -7.3110285    4.2869041
#> Apr 2020  27.1514421   -0.8866413
#> May 2020 -13.3938704 -294.9083784
#> Jun 2020  -6.4601525    2.0358254
#> Jul 2020  -9.3245461   -9.8446980
#> Aug 2020  -7.6908693   58.9109098
#> Sep 2020   3.7157978  -42.5751629
#> Oct 2020   3.5543278   63.4658985
#> Nov 2020  -9.8399849  -57.8524902
#> Dec 2020   2.1472959  -16.9109048
#> 
#> $description
#>           type coeff
#> var1 Undefined    NA
#> var2 Undefined    NA
#> 
myreg1 <- regarima(myseries,myspec1)

myspec2 <- regarima_spec_tramoseats(spec = "TRfull",
             usrdef.varEnabled = TRUE,
             usrdef.var = var, usrdef.varCoef = c(17,-1),
             transform.function = "None")
myreg2 <- regarima(myseries, myspec2)

 # Pre-specified ARMA coefficients
myspec1 <- regarima_spec_tramoseats(spec = "TRfull",
             arima.coefEnabled = TRUE, automdl.enabled = FALSE,
             arima.p = 2, arima.q = 0, arima.bp = 1, arima.bq = 1,
             arima.coef = c(-0.12, -0.12, -0.3, -0.99),
             arima.coefType = rep("Fixed", 4))
myreg1 <- regarima(myseries, myspec1)
myreg1
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
summary(myreg1)
#> y = regression model + arima (2, 1, 0, 1, 1, 1)
#> 
#> Model: RegARIMA - TRAMO/SEATS
#> Estimation span: from 1-1990 to 12-2020
#> Log-transformation: no
#> Regression model: mean, trading days effect(2), leap year effect, Easter effect, outliers(4)
#> 
#> Coefficients:
#> ARIMA: 
#>           Estimate Std. Error T-stat Pr(>|t|)
#> Phi(1)       -0.12       0.00     NA       NA
#> Phi(2)       -0.12       0.00     NA       NA
#> BPhi(1)      -0.30       0.00     NA       NA
#> BTheta(1)    -0.99       0.00     NA       NA
#> 
#> Regression model: 
#>                Estimate Std. Error  T-stat Pr(>|t|)    
#> Mean          -0.007018   0.028698  -0.245  0.80694    
#> Week days      0.704716   0.029477  23.907  < 2e-16 ***
#> Leap year      2.163501   0.675295   3.204  0.00148 ** 
#> Easter [6]    -2.360603   0.384746  -6.135 2.24e-09 ***
#> TC (4-2020)  -25.280857   2.517080 -10.044  < 2e-16 ***
#> TC (3-2020)  -21.581618   2.569059  -8.401 8.88e-16 ***
#> AO (5-2011)   14.219490   1.748501   8.132 6.88e-15 ***
#> LS (11-2008)  -6.225300   2.608253  -2.387  0.01751 *  
#> ---
#> Signif. codes:  0 ‘***’ 0.001 ‘**’ 0.01 ‘*’ 0.05 ‘.’ 0.1 ‘ ’ 1
#> 
#> 
#> Residual standard error: 2.712 on 350 degrees of freedom
#> Log likelihood = -882.9, aic =  1784, aicc =  1784, bic(corrected for length) = 2.127
#> 
s_arimaCoef(myspec1)
#>            Type Value
#> Phi(1)    Fixed -0.12
#> Phi(2)    Fixed -0.12
#> BPhi(1)   Fixed -0.30
#> BTheta(1) Fixed -0.99
s_arimaCoef(myreg1)
#>            Type Value
#> Phi(1)    Fixed -0.12
#> Phi(2)    Fixed -0.12
#> BPhi(1)   Fixed -0.30
#> BTheta(1) Fixed -0.99
# }
```
