# Package index

## Seasonal adjustment functions

Functions to perform seasonal adjustment with X-13ARIMA or TRAMO-SEATS

- [`jx13()`](x13.md) [`x13()`](x13.md) : Seasonal Adjustment with
  X13-ARIMA
- [`x13_spec()`](x13_spec.md) : X-13ARIMA model specification, SA/X13
- [`jtramoseats()`](tramoseats.md) [`tramoseats()`](tramoseats.md) :
  Seasonal Adjustment with TRAMO-SEATS
- [`tramoseats_spec()`](tramoseats_spec.md) : TRAMO-SEATS model
  specification
- [`user_defined_variables()`](user_defined_variables.md) : Display a
  list of all the available output objects (series, parameters,
  diagnostics)
- [`plot(`*`<regarima>`*`)`](plot.md)
  [`plot(`*`<decomposition_X11>`*`)`](plot.md)
  [`plot(`*`<decomposition_SEATS>`*`)`](plot.md)
  [`plot(`*`<final>`*`)`](plot.md) [`plot(`*`<SA>`*`)`](plot.md) :
  Plotting regarima, decomposition or final results of a SA
- [`save_spec()`](save_spec.md) [`load_spec()`](save_spec.md) : Saving
  and loading a model specification, SA and pre-adjustment in X13 and
  TRAMO-SEATS
- [`s_estimate()`](specification.md) [`s_transform()`](specification.md)
  [`s_usrdef()`](specification.md) [`s_preOut()`](specification.md)
  [`s_preVar()`](specification.md) [`s_td()`](specification.md)
  [`s_easter()`](specification.md) [`s_out()`](specification.md)
  [`s_arima()`](specification.md) [`s_arimaCoef()`](specification.md)
  [`s_fcst()`](specification.md) [`s_span()`](specification.md)
  [`s_x11()`](specification.md) [`s_benchmarking()`](specification.md)
  [`s_seats()`](specification.md) : Access a model specification, a SA
  or a pre-adjustment model in X13 and TRAMO-SEATS

## RegARIMA functions

Functions to only peform regARIMA estimation

- [`jregarima()`](regarima.md) [`jregarima_tramoseats()`](regarima.md)
  [`jregarima_x13()`](regarima.md) [`regarima()`](regarima.md)
  [`regarima_tramoseats()`](regarima.md) [`regarima_x13()`](regarima.md)
  : RegARIMA model, pre-adjustment in X13 and TRAMO-SEATS
- [`regarima_spec_tramoseats()`](regarima_spec_tramoseats.md) : RegARIMA
  model specification, pre-adjustment in TRAMO-SEATS
- [`regarima_spec_x13()`](regarima_spec_x13.md) : RegARIMA model
  specification: the pre-adjustment in X13

## Manipulate Java objects

Functions to manipulate the Java objects of a seasonal adjustment or a
regARIMA model

- [`get_jspec()`](jSA.md) [`get_dictionary()`](jSA.md)
  [`get_indicators()`](jSA.md) [`jSA2R()`](jSA.md) : Functions around
  'jSA' objects

## Manipulate JDemetra+ workspaces

Functions to import and export models JDemetra+ workspaces

- [`load_workspace()`](load_workspace.md) : Load a 'JDemetra+' workspace
- [`new_workspace()`](new_workspace.md)
  [`new_multiprocessing()`](new_workspace.md) : Create a workspace or a
  multi-processing
- [`save_workspace()`](save_workspace.md) : Save a workspace
- [`add_sa_item()`](add_sa_item.md) : Add a seasonally adjusted series
  to a multi-processing
- [`get_jmodel()`](get_model.md) [`get_model()`](get_model.md) : Get the
  seasonally adjusted model from a workspace
- [`compute()`](compute.md) : Compute a workspace multi-processing(s)
- [`count()`](count.md) : Count the number of objects inside a workspace
  or multiprocessing
- [`get_name()`](get_name.md) : Get the Java name of a multiprocessing
  or a sa_item
- [`get_all_names()`](get_all_names.md) : Get the Java name of all the
  contained object
- [`get_object()`](get_object.md) [`get_all_objects()`](get_object.md) :
  Get objects inside a workspace or multiprocessing
- [`get_position()`](get_position.md) : Get the position of an object
- [`get_ts()`](get_ts.md) : Get the input raw time series

## Database

- [`ipi_c_eu`](ipi_c_eu.md) : Industrial Production Indices in
  manufacturing industry in the European Union
