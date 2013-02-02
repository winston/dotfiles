# Dot Files
For use on my machines. Gloriously copied from a few places.

## Prerequisites

### Install Zsh

    brew install zsh

### Install [Prezto](https://github.com/sorin-ionescu/prezto)

1) Launch Zsh

    zsh

2) Clone the repository:

    git clone --recursive https://github.com/sorin-ionescu/prezto.git "${ZDOTDIR:-$HOME}/.zprezto"

3) Create a new Zsh configuration by copying the Zsh configuration files provided:

    setopt EXTENDED_GLOB
    for rcfile in "${ZDOTDIR:-$HOME}"/.zprezto/runcoms/^README.md(.N); do
      ln -s "$rcfile" "${ZDOTDIR:-$HOME}/.${rcfile:t}"
    done

4) Set Zsh as your default shell:

    chsh -s /bin/zsh

## Installation

    git clone git://github.com/winston/dotfiles ~/.dotfiles
    cd ~/.dotfiles
    rake install

## License

Just use lah.
