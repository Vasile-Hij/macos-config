# macos-config

## I. Git
```bash
$ brew install git
$ $ sh-keygen -t rsa -b 4096 -C "your_name@email.com"
$ ssh-add id_rsa_<change_me>
$ cd ~/.ssh/
$ touch config
$ subl -a config.
```
Then add:

    Host github.com
        AddKeysToAgent yes
        IdentityFile ~/.ssh/id_rsa_<change_me>

Copy key to clipboard the paste it to Github>Settings>SSH and GPG keys:
```bash
$ cat ~/.ssh/id_rsa_<change_me>.pub | pbcopy
```

Set globally:
```bash
$ git config --global user.name "Your Name"
$ git config --global user.email your_name@email.com
```

Set locally in your repo `~/.gitconfig` if you already have a different and this is just a test key:

```bash 
$ git config user.name "Your Name Here"
$ git config user.email your@email.com
```




## II. Install Oh-my-zsh for Mac:
```bash
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```

## III. Powerlevel10k install

#### Manual download
```bash
$ git clone --depth=1 https://github.com/romkatv/powerlevel10k.git ~/powerlevel10k
echo 'source ~/powerlevel10k/powerlevel10k.zsh-theme' >>~/.zshrc
```

Set `ZSH_THEME="powerlevel10k/powerlevel10k"` in ~/.zshrc.

```bash
$ exec zshrc
```

#### Configuration wizard for powerlevel10k
```bash
$ p10k configure
```
##### Note: if fonts are not displayed correctly it's recommended to install [these fonts](https://github.com/romkatv/powerlevel10k?tab=readme-ov-file#meslo-nerd-font-patched-for-powerlevel10k) already added in [this repo](https://github.com/Vasile-Hij/macos-config/Fonts)


## IV. Wezterm Install
```bash
$ brew install --cask wezterm
```

```bash
cp .wezterm.lua ~/
```

### zsh-autosuggestions
```bash
$ git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
```
Set `plugins=(zsh-autosuggestions)` in `vim ~/.zshrc`


### zsh-syntax-highlighting
```bash
$ git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
Set `plugins=(zsh-syntax-highlighting)` in `vim ~/.zshrc`


#### Uninstall Zsh + Oh My Zsh + Powerlevel10k theme (macOS & Linux)
[Source](https://gist.github.com/breithbarbot/254e58bd87009963b3f58405d75cbe6c)

```
	#!/bin/sh

	# Uninstall Zsh + Oh My Zsh + Powerlevel10k theme (macOS & Linux)
	# run: sh -c "$(curl -fsSL "$(echo "$(curl -s "https://api.github.com/gists/254e58bd87009963b3f58405d75cbe6c")" | grep -o '"raw_url": *"[^"]*"' | cut -d'"' -f4)")"

	# Remove installations + configurations
	rm -f ~/.p10k.zsh
	rm -rf -- ${ZSH_CUSTOM:-$HOME/.oh-my-zsh/custom}/themes/powerlevel10k
	sh ~/.oh-my-zsh/tools/uninstall.sh -y
	sudo chsh -s $(which bash)
	if [ "$(uname -s)" = "Darwin" ]; then
	  brew uninstall zsh
	else
	  sudo apt remove zsh -y
	  sudo apt autoremove -y
	fi
	rm -Rf ~/.zsh*
```

## V. Kubernetes
```bash
$ brew install kubectx
$ brew tap johanhaleby/kubetail && brew install kubetail
```
### k8s aliases
[Source](https://github.com/ahmetb/kubectl-aliases?tab=readme-ov-file)

 **Disclaimer**: on this repo `.kubectl-aliases` does not inlcude any `delete` command as a safety measure.
```bash
cp .kubectl-aliases ~/
```

Set in ~/.zshrc
```vim
[ -f ~/.kubectl_aliases ] && source ~/.kubectl_aliases
function kubectl() { echo "+ kubectl $@">&2; command kubectl $@; }
```
then: 
```bash
$ source ~/.zshrc
```

-----