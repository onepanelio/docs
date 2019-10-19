Initialize Project in current working directory working (cwd) and in Onepanel.

## Syntax

```
onepanel projects init [OPTIONS]
```

### Options
`--help`        Show this message and exit.

## Examples

Initialize Project in cwd, will default to cwd name:

```
onepanel projects init
```

!!! note "Note" 
    Project name should be 3 to 25 characters long, lower case alphanumeric or '-' and must start and end with an alphanumeric character. If the directory name doesn't match these criteria, you will be prompted to enter a valid name.