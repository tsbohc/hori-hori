# hori-hori

A personal dotfiles templating and management framework written in a hundred lines of bash.

- Toml-inspired configuration language
- Logicless recursive templating
- Package-like management

```
USAGE
  $ hori-hori <operation> <arguments>

  install or remove packages
    {-s, setup}    <package(s)>
    {-r, remove}   <package(s)>

  run hook in packages or command with package name as argument
    {-e, exec}     <command> (<package(s)> | -i | -a)
    {-k, hook}     <hook> (<package(s)> | -i | -a)

OPTIONS
  -h, --help       display this message
  -i, --installed  replaced with installed packages
  -a, --available  replaced with available packages
```
