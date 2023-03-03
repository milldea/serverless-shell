# Serverless Shell

See the original project for details.  
https://github.com/capitalone/serverless-shell

## Install

```
cd ./{your project}
# ssh
git clone git@github.com:milldea/serverless-shell.git
# https
git clone https://github.com/milldea/serverless-shell.git
cd serverless-shell
npm i
```

Add the plugin and set some env vars in your `serverless.yml`:

```yaml
provider:
  name: aws
  environment:
    SOME_VAR: foobar
plugins:
  - ./serverless-shell
custom:
  shellBinary: zsh or bash and so on...
```

## Usage
Example in a python project
```
$ serverless shell
Serverless: Spawning python3.6...
Python 3.6.1 (default, Mar 22 2017, 06:17:05) 
[GCC 6.3.0 20170321] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import os
>>> os.environ['SOME_VAR']
'foobar'
```
and in a NodeJS project:
```
$ serverless shell
Serverless: Spawning node...
> process.env.SHELL
'foobar'
```

### Per function & stage specific env vars
Since the main reason for building this was to test code with the configs for
various stages, it supports properly building the environment. For example:
```
$ serverless -s staging shell -f status
```

## Custom shell (babel) support
If you want to launch a different shell than the runtime's default, you can
specify that with in the `custom` section of your config. This can be used
to for things like using `babel-node` instead of `node` or even dropping to
`bash` with the right env vars set.

Example:
```
  custom:
    shellBinary: babel-node
```

This feature can also be activated by a CLI switch:
```
$ sls shell -S bash
```
