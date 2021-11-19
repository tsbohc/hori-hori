# hori-hori

A personal dotfiles templating and management framework written in a hundred lines of bash.

- Toml-inspired configuration language
- Logicless recursive templating
- Package-like management

```
USAGE
  $ hori-hori <operation> [arguments]

  {-s, setup}    <package(s)>
  {-r, remove}   <package(s)>
  {-e, exec}     <command> (<package(s)> | -i | -a)
  {-k, hook}     <hook> (<package(s)> | -i | -a)

OPTIONS
  -h, --help       display this message
  -i, --installed  replaced with installed packages
  -a, --available  replaced with available packages

EXAMPLES
  $ hori-hori -e echo -i                list installed packages
  $ hori-hori ... | yay -S --needed -   install required dependencies
```
