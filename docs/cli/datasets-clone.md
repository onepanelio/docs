Clone a Dataset so that you can make changes to it and push back up.

## Syntax

```
onepanel datasets clone [OPTIONS] PATH [DIRECTORY]
```

### Options

`-q`, `--quiet`         Minimize chatter from executed commands.

`-v`, `--version`       The version of the Dataset. If none is provided, latest is used.

`--help`                Show this message and exit.

## Examples

Clone latest Dataset version:

```
onepanel clone onepanel-demo/datasets/mnist
```

Clone a specific Dataset version:

```
onepanel clone onepanel-demo/datasets/mnist -v 2
```

Clone Dataset into a specific directory (defaults to cwd if omitted):

```
onepanel clone onepanel-demo/datasets/mnist mnist-dataset
```
