# hori-hori

A tiny dotfiles templating and management framework written in bash and awk in `~150 loc`

Consists of three main parts:
- Configuration language
- Templating engine
- Package manager

### nyaml
A minimal, indentation based configuration language inspired by yaml. Can load external files into the current position on the tree. Supports key value pairs and whole line comments. Compiles to bash variables.

<table>
<tr>
<th align="center">
nyaml source
</th>
<th align="center">
bash target
</th>
</tr>
<tr>
<td>

```yaml
# varsets
colo: "limestone"
iosevka: ''
  family: "Iosevka Custom"
  size: 12
limestone: require varsets/limestone
```

</td>
<td>

```bash
__colo="limestone"
__iosevka=''
__iosevka_family="Iosevka Custom"
__iosevka_size=12
__limestone_black="#000000"
__limestone_white="#ffffff"
```

</td>
</tr>
</table>

### templating engine

The templating engine supports nested keys, meaning it will perform multiple lookups for any given statement, until all leaves are rendered. A template like this:

```bash
Here is a nice black: "{% {{colo}_black} %}"
```
With the above context will be render to:
```bash
Here is a nice black: "#000000"
```

Due to the nature of how nyaml is implemented, evaluating a leaf is a matter of replacing it with its `${!key}`.

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

In the above example, `render` will compile a template with the current global context into a cache directory and returns a path to the compiled file. It is then passed to a function that will it with the target location.

## addendum

This project was a personal challenge of mine. It's more of a show-and-tell than a practical tool. I advise you not to use it.

Honestly, I like bash. I think it has such a strong character, and it's limitations cause one to seek novel solutions to everyday problems. Writing bash is like taking a hike in the mountains. A nice break from other, more comfortable languages.
