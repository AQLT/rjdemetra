# Create a workspace or a multi-processing

Functions to create a 'JDemetra+' workspace (`new_workspace()`) and to
add a new multi-processing (`new_multiprocessing()`).

## Usage

``` r
new_workspace()

new_multiprocessing(workspace, name)
```

## Arguments

- workspace:

  a workspace object

- name:

  character name of the new multiprocessing

## Value

`new_workspace()` returns an object of class `workspace` and
`new_multiprocessing()` returns an object of class `multiprocessing`.

## See also

[`load_workspace`](load_workspace.md),
[`save_workspace`](save_workspace.md), [`add_sa_item`](add_sa_item.md)

## Examples

``` r
# To create and export an empty 'JDemetra+' workspace
wk <- new_workspace()
mp <- new_multiprocessing(wk, "sa1")

```
