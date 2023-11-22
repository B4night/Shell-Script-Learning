# show git branch name at linux prompt

``` shell
# related code

parse_git_branch() {
 git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}

PS1='\[\033[01;32m\]\u\[\033[00m\]:\[\033[01;34m\]\W\[\033[01;31m\] $(parse_git_branch)\[\033[00m\]\$ '

```



the prompt is like `user-name:current-dir-name (branch-name)`



# zsh, omz and useful plugins

``` shell
# this is for fedora
sudo dnf install zsh
sh -c "$(curl -fsSL https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

# below is plugin installation

# download thefuck
# requirements:
# python (3.5+)
# pip
# python-dev
pip install thefuck

# fzf: fuzzy finder
sudo dnf install fzf

# bat: cat with syntax highlight
sudo dnf install bat

# zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git
echo "source ${(q-)PWD}/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh" >> ${ZDOTDIR:-$HOME}/.zshrc
source ./zsh-syntax-highlighting/zsh-syntax-highlighting.zsh

# autosuggestions
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
# add plugins, need to be done mannually
# plugins=( 
# 	other plugins...
# 	zsh-autosuggestions
# )
source ~/.zshrc

```