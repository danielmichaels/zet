# GoLand and templ with autocomplete

To use `templ` with autocomplete via its
[Plugin](https://github.com/templ-go/templ-jetbrains) you must do the following:

- Go to settings>templ and enter the path to the `templ` binary (e.g. `$HOME/.local/bin/templ`)
- Close all GoLand instances
- Launch GoLand via the terminal inside the project directory (e.g. `goland .`)

It works but still needs some refining at the project level.

The alternative is to use `neovim` for the `templ` files or VSCode. As
a GoLand subscriber these are sub par alternatives but may be required in the
short term.

Tags:

  #go #templ
