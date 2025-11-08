# Get the Java name of all the contained object

Generic functions to retrieve the Java name of the contained
`multiprocessings` or the contained `sa_items`.

## Usage

``` r
get_all_names(x)
```

## Arguments

- x:

  An object containing other objects whose names we want to know

## Value

A `character` vector containing all the names.

## See also

Other functions to retrieve information from a workspace,
multiprocessing or sa_item: [`get_name`](get_name.md),
[`get_position`](get_position.md), [`count`](count.md),
[`get_model`](get_model.md), [`get_ts`](get_ts.md).

## Examples

``` r
# \donttest{
spec_x13 <- x13_spec(spec = "RSA5c", easter.enabled = FALSE)
sa_x13 <- x13(ipi_c_eu[, "FR"], spec = spec_x13)
spec_ts <- tramoseats_spec(spec = "RSA5")
sa_ts <- tramoseats(ipi_c_eu[, "FR"], spec = spec_ts)

wk <- new_workspace()
mp <- new_multiprocessing(wk, "sap1")
mp2 <- new_multiprocessing(wk, "sap2")

get_all_names(wk)
#> [1] "sap1" "sap2"

add_sa_item(wk, "sap1", sa_x13, "X13")
add_sa_item(wk, "sap1", sa_ts, "TramoSeats")

get_all_names(mp)
#> [1] "X13"        "TramoSeats"
# }
```
