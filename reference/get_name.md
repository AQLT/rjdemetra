# Get the Java name of a multiprocessing or a sa_item

Generic functions to retrieve the Java name of a `multiprocessing` or a
`sa_item`.

## Usage

``` r
get_name(x)
```

## Arguments

- x:

  the object to retrieve the name from.

## Value

A `character`.

## See also

Other functions to retrieve information from a workspace,
multiprocessing or sa_item: [`count`](count.md),
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
add_sa_item(wk, "sap1", sa_x13, "X13")
add_sa_item(wk, "sap1", sa_ts, "TramoSeats")

sa_item1 <- get_object(mp, 1)
sa_item2 <- get_object(mp, 2)

get_name(sa_item1) # returns "X13"
#> [1] "X13"
get_name(sa_item2) # returns "TramoSeats"
#> [1] "TramoSeats"

get_name(mp) # returns "sap1"
#> [1] "sap1"

# To retrieve the name of every sa_item in a given multiprocessing:
sapply(get_all_objects(mp), get_name)
#>          X13   TramoSeats 
#>        "X13" "TramoSeats" 

# To retrieve the name of every multiprocessing in a given workspace:
sapply(get_all_objects(wk), get_name)
#>   sap1 
#> "sap1" 

# To retrieve the name of every sa_item in a given workspace:
lapply(get_all_objects(wk),function(mp){
  sapply(get_all_objects(mp), get_name)
})
#> $sap1
#>          X13   TramoSeats 
#>        "X13" "TramoSeats" 
#> 
# }
```
