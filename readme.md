# hori-hori

A personal dotfiles templating and package-esque management framework written in around a hundred lines of bash.

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

<!--
## examples

#### Repo

List installed or available packages:

```
hori-hori -e echo (-i | -a)
```

#### Autostart

1. create a hook, e.g in `polybar/hori.sh`:

```bash
autostart() {
  launch polybar main &
}
```

2. execute it in every installed package, e.g in `herbstluftwm/autostart`:

```bash
hori-hori hook autostart --installed
```
### nyoml
A minimal configuration language inspired by toml. Can load external files into the current position on the tree. Supports key value pairs and whole line comments. Compiles to bash variables.

<table>
<tr>
<th align="center">
nyoml source
</th>
<th align="center">
bash target
</th>
</tr>
<tr>
<td>

```bash
# varsets
colo = "limestone"
[font.iosevka]
family = "Iosevka Custom"
size = 12
[limestone]
$(import "varsets/limestone")
```

</td>
<td>

```bash
__colo="limestone"
__font_iosevka_family="Iosevka Custom"
__font_iosevka_size=12
__limestone_black="#000000"
__limestone_white="#ffffff"
__limestone_section_foo="bar"
```

</td>
</tr>
</table>

### templating engine

The templating engine supports nested keys, meaning it will perform multiple lookups for any given statement, until all leaves are rendered. A template like this:

```bash
Here is a nice black: "{% {{colo}_black} %}"
```
With the above context will be rendered to:
```bash
Here is a nice black: "#000000"
```

Due to the nature of how nyoml is implemented, evaluating a leaf is a matter of replacing it with its `${!key}`.

### package manager

```
repo
├── alacritty
│   ├── alacritty.yml
.   └── hori.sh
```
```
hori-hori [setup|remove] [package...]
```

Dotfiles are folders containing `hori.sh`, a file with instructions that operates on the package scope:
```bash
grow() {
  link $(render alacritty.yml) "~/.config/alacritty/alacritty.yml"
}

weed() {
  unlink "~/.config/alacritty/alacritty.yml"
}
```

When installing or uninstalling a dotfile, hori-hori will run the `grow` or `weed` function respectively. A few hooks are predefined.

In the above example, `render` will compile a template with the current global context into a cache directory and return the path to the compiled file. It is then passed to a function that will create a symlink from it to the target location.

## addendum

Honestly, I like bash. I think it has such a strong character, and it's limitations cause one to seek novel solutions to everyday problems. Writing bash is like taking a hike in the mountains. A nice break from other, more comfortable languages.

This project was a personal challenge of mine. It's more of a show-and-tell than a practical tool.

I advise you not to use it.
-->
