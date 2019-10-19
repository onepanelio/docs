Clone a Project from Onepanel

## Syntax

```
onepanel projects clone [OPTIONS] PATH [DIRECTORY]
```

### Options
`--help`        Show this message and exit.

## Examples

Clone Project from Onepanel in a directory with the Project name:

```
onepanel projects clone <account>/projects/<project-name>
```

Clone Project from Onepanel in a directory with a different name than Project name:

```
onepanel projects clone <account>/projects/<project-name> <directory-name>
```

Clone Project from Onepanel in current working directory:

```
onepanel projects clone <account>/projects/<project-name> .
```