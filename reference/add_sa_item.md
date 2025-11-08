# Add a seasonally adjusted series to a multi-processing

Function to add a new seasonally adjusted object (class `"SA"` or
`"jSA"`) to a `workspace` object.

## Usage

``` r
add_sa_item(workspace, multiprocessing, sa_obj, name)
```

## Arguments

- workspace:

  the workspace to add the seasonally adjusted series to.

- multiprocessing:

  the name or index of the multiprocessing to add the seasonally
  adjusted series to.

- sa_obj:

  the seasonally adjusted object to add.

- name:

  the name of the seasonally adjusted series in the multiprocessing. By
  default the name of the `sa_obj` is used.

## See also

[`load_workspace`](load_workspace.md),
[`save_workspace`](save_workspace.md)

## Examples

``` r
# \donttest{
dir <- tempdir()
# Adjustment of a series with the x13 and Tramo-Seats methods
spec_x13 <- x13_spec(spec = "RSA5c", easter.enabled = FALSE)
sa_x13 <- x13(ipi_c_eu[, "FR"], spec = spec_x13)
spec_ts <- tramoseats_spec(spec = "RSA5")
sa_ts <- jtramoseats(ipi_c_eu[, "FR"], spec = spec_ts)

# Creation of a new workspace..
wk <- new_workspace()
# and of the multiprocessing "sa1" that will contain the series
new_multiprocessing(wk, "sa1")
# Addition of the adjusted series to the workspace via the sa1 multiprocessing
add_sa_item(wk, "sa1", sa_x13, "X13")
add_sa_item(wk, "sa1", sa_ts, "TramoSeats")

# Export of the new filled workspace
save_workspace(wk, file.path(dir, "workspace.xml"))
# }
```
