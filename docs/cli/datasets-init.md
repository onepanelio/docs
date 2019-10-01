Initialize Dataset in current directory and create Dataset in Onepanel.

## Syntax

```
onepanel datasets init [OPTIONS]
```

### Options
`-n`, `--name`  Dataset name.

`--help`        Show this message and exit.

## Examples

Initialize Dataset in current directory, will be prompted for name, will default to `cwd` name:

```
onepanel datasets init
```

Initialize Dataset in current directory and add a name:

```
onepanel datasets init -n different-name-from-cwd
```