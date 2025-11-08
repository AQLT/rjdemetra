# Get the position of an object

Generic functions to retrieve the position of the contained
`multiprocessings` or the contained `sa_items`.

## Usage

``` r
get_position(x, name)
```

## Arguments

- x:

  An object containing other objects whose names we want to know

- name:

  a`character` specifiing an object

## Value

A `integer`

## See also

Other functions to retrieve information from a workspace,
multiprocessing or sa_item: [`get_name`](get_name.md),
[`get_all_names`](get_all_names.md), [`count`](count.md),
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

get_position(wk, "sap1")
#> [1] 1
get_position(wk, "sap2")
#> [1] 2

add_sa_item(wk, "sap1", sa_x13, "X13")
add_sa_item(wk, "sap1", sa_ts, "TramoSeats")

get_position(mp, "TramoSeats")
#> [1] 2
get_position(mp, "X13")
#> [1] 1
# }
```
