Login with a combination of either:

- Email and password
- Username and password
- Username and token

## Syntax

```
onepanel login [OPTIONS]
```

### Options

`-e`, `--email`     Email you use to login to the website with.

`-u`, `--username`  The name you see in the top right of the website, once you log in.

`-p`, `--password`  Password you use when logging into the website.

`-t`, `--token`     One of the tokens that was created, from the settings > tokens and variables page.

`--help`          Show this message and exit.

## Examples

Log in with email/password prompt:
```
onepanel login
```

Log in with email and token:
```
onepanel login -u <username> -t <token>
```