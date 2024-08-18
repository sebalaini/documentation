# SRE

## k9s

Install [K9s](https://k9scli.io/) via `brew` as specified in the installation documentation `brew install derailed/k9s/k9s`

Run the below commands to move the configuration into `.config/k9s` instead of `Library/Application Support/`, refer to the GitHub [issues #1273](https://github.com/derailed/k9s/issues/1273), `XDG_CONFIG_HOME` is unset in MAC OS X.

```bash
mkdir -p ~/.config/k9s
mv ~/Library/Application\ Support/k9s/config.yaml ~/.config/k9s/
rm -rf ~/Library/Application\ Support/k9s/
ln -s ~/.config/k9s/ ~/Library/Application\ Support/k9s
```

Create a `monokai.yaml` file inside `~/.config/k9s/skins` and copy the [monokai theme](https://github.com/derailed/k9s/blob/master/skins/monokai.yaml)

Add the `skin` setting under the `ui` key

```
k9s:
  ui:
    skin: monokai
```
