Git + Perforce (git-p4)
=======================

## Clone multiple different paths from a depot

### Into a single directory

    $ git p4 clone -v --dest=PROJECT_DIR //DEPOT/path1/... //DEPOT/path2/... //DEPOT/pathn/...

### Using client spec, while also limiting depot paths

```
$ export P4CLIENT=MY_WORKSPACE
$ ws_paths=$(p4 workspace -o | grep -P '^\t//DEPOT/' | cut -f2 -d$'\t' | cut -f1 -d' ')
$ git p4 clone -v --use-client-spec --dest=PROJECT_DIR ${ws_paths[*]}
```
