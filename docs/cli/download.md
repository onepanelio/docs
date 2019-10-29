Download Dataset or Job output.

## Syntax

```
onepanel download [OPTIONS] PATH [DIRECTORY]
```

Dataset download syntax will look like this:

```
onepanel download <account>/datasets/<dataset>
```

Job output download syntax will look like this:

```
onepanel download <account>/projects/<project>/jobs/<job-number>
```

### Options

`--delete`              Deletes files locally that are not in the Dataset.

`--archive`             Download Job output as a compressed file. Applies to Job output only.

`-q`, `--quiet`         Minimize chatter from executed commands.

`-b`, `--background`    Run the download in the background. Will work even if SSH session is terminated.

`-v`, `--version`       The version of the Dataset. If none is provided, latest is used.

`--include`             Only download files matching this regex pattern.

`--help`                Show this message and exit.

## Examples

### Datasets

Download latest Dataset version:

```
onepanel download onepanel-demo/datasets/mnist
```

Download a specific Dataset version:

```
onepanel download onepanel-demo/datasets/mnist -v 2
```

Download Dataset into a specific directory (defaults to cwd if omitted):

```
onepanel download onepanel-demo/datasets/mnist mnist-dataset
```

### Jobs

Download Job output:

```
onepanel download onepanel-demo/projects/examples/jobs/100
```

Download Job output as a compressed file:

```
onepanel download onepanel-demo/projects/examples/jobs/100 --archive
```

Download Job output into a specific directory (defaults to cwd if omitted):

```
onepanel download onepanel-demo/projects/examples/jobs/100 job-100-output
```