## Switching Between Python Versions in Arch Linux using `pyenv`

### `pyenv` Installation:

- Install `pyenv`:

```
sudo pacman -S pyenv
```

- Copy these lines in your `.bashrc` or `.zshrc` file:

```
export PYENV_ROOT="$HOME/.pyenv"
command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init -)"
```

- make sure you install these packages, (recommendation: use yay package manager, it'll be easier!):

```
make gcc libffi libssl zlib bzip2 readline sqlite tk
```

### Switching between python versions using `pyenv`:

- for globally:

```
pyenv global [version of the python]
```

- for locally:

```
pyenv local [version of the python]
```

- then cross check with this:

```
python --version
```
