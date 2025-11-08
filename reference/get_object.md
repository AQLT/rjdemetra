# Get objects inside a workspace or multiprocessing

Generic functions to retrieve all (`get_all_objects()`)
`multiprocessing` (respectively `sa_item`) from a `workspace`
(respectively `multiprocessing`) or to retrieve a single one
(`get_object()`) .

## Usage

``` r
get_object(x, pos = 1)

get_all_objects(x)
```

## Arguments

- x:

  the object in which to store the extracted `multiprocessing` or
  `sa_item`.

- pos:

  the index of the object to extract.

## Value

An object of class `multiprocessing` or `sa_item` (for `get_object()`)
or a list of objects of class `multiprocessing` or `sa_item` (for
`get_all_objects()`).

## See also

Other functions to retrieve information from a workspace,
multiprocessing or sa_item: [`count`](count.md),
[`get_model`](get_model.md), [`get_name`](get_name.md),
[`get_ts`](get_ts.md).

## Examples

``` r
# \donttest{

sa_x13 <- x13(ipi_c_eu[, "FR"], spec = "RSA5c")

wk <- new_workspace()
mp <- new_multiprocessing(wk, "sap1")
add_sa_item(wk, "sap1", sa_x13, "X13")

# A way to retrieve the multiprocessing:
mp <- get_object(wk, 1)
# And the sa_item object:
sa_item <- get_object(mp, 1)
# }
```
