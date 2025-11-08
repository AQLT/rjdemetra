# Count the number of objects inside a workspace or multiprocessing

Generic functions to count the number of `multiprocessing` (respectively
`sa_item`) inside a `workspace` (respectively `multiprocessing`).

## Usage

``` r
count(x)
```

## Arguments

- x:

  the `workspace` or the `multiprocessing`.

## See also

Other functions to retrieve information from a workspace,
multiprocessing or sa_item: [`get_model`](get_model.md),
[`get_name`](get_name.md), [`get_ts`](get_ts.md).

## Examples

``` r
wk <- new_workspace()
mp <- new_multiprocessing(wk, "sap1")
count(wk) # 1 multiprocessing inside the workspace wk
#> [1] 1
count(mp) # 0 sa_item inside the multiprocessing mp
#> [1] 0

```
