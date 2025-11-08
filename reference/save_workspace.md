# Save a workspace

Function to save a `workspace` object into a 'JDemetra+' workspace.

## Usage

``` r
save_workspace(workspace, file)
```

## Arguments

- workspace:

  the workspace object to export

- file:

  the path where to export the 'JDemetra+' workspace (.xml file). By
  default, if not specified, a dialog box opens.

## Value

A boolean indicating whether the export is successful.

## See also

[`load_workspace`](load_workspace.md)

## Examples

``` r
# \donttest{
dir <- tempdir()
# Creation and export of an empty 'JDemetra+' workspace
wk <- new_workspace()
new_multiprocessing(wk, "sa1")
save_workspace(wk, file.path(dir, "workspace.xml"))
# }
```
