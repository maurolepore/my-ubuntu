
This is how I build the Ubuntu environment I like.

## Ubuntu

  - [ ] [Install
    ubuntu](https://ubuntu.com/tutorials/tutorial-install-ubuntu-desktop#1-overview),
    maybe alongside Windows. Minimal seems fine.

  - [ ] Ubuntu can restart and boot on Windows

  - [ ] Ubuntu can restart and boot on Ubuntu

  - [ ] Ubuntu’s boot menu (F12 on thinkpad) lists ubuntu first, windows
    second

Universal Access:

  - [ ] Dock \> Auto-hide the dock

  - [ ] Universal Access \> Cursor size: largest; Large Text: ON

Devices:

  - [ ] Mouse & touchpad\> Primary button: right

  - [ ] Displays \>
    
      - Display arrangement: 2-1
      - Scale: 100%
      - Resolution: Same for both so windows fit the same way in both
        screens
      - Night Light: on

## Tweaks on the terminal

  - [ ] Ensure user, e.g. mauro, owns \~ (/home/mauro) and all its
    contents:

<!-- end list -->

    chown mauro -R ~

Now mauro can add ssh keys at \~/.ssh, launch RStudio from a terminal at
\~, etc.

More:

  - <https://askubuntu.com/questions/633733/gdebi-core-package-is-not-available>
  - <https://docs.rstudio.com/resources/install-r/>

## Small installs outside the terminal

  - [ ] Install from Chrome from Firefix; login and sync personal and
    work accounts

  - [ ] Install Slack from Ubuntu software; find workspaces linked to
    personal and work accounts

  - [ ] Install VLC media or similar video player

## Small installs from the terminal

### Linux tools

  - [ ] Install the dpkg-sig package.

<!-- end list -->

    sudo apt install dpkg-sig

  - [ ] Install gdebi:

<!-- end list -->

    sudo apt-get update
    sudo apt-get install gdebi-core

  - [ ] Install flameshot to capture screen shots

<!-- end list -->

    apt install flameshot

  - [ ] [Install an R development
    environment](https://www.jimhester.com/post/2017-10-13-docker/)

<!-- end list -->

    sudo apt-get update
    sudo apt-get install -y libcurl4-openssl-dev libssl-dev libssh2-1-dev libxml2-dev

  - [ ] Install vim

<!-- end list -->

    sudo apt install vim

  - [ ] Install git

<!-- end list -->

    sudo apt install git

  - [ ] Install LaTeX (to build pdf manuals for R packages)

<!-- end list -->

    # Big install! The smaller texlive-base didn't work for me
    sudo apt-get install texlive-full

  - [ ] Install curl

<!-- end list -->

    sudo apt-get install curl

  - [ ] [Install
    zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

<!-- end list -->

    sudo apt install zsh

  - [ ] Make zsh the default login shell for the user, e.g. mauro. No
    need to setup .zshrc if planning to next install oh-my-zsh (adds its
    own .zshrc).

<!-- end list -->

    # Confirm installation worked
    zsh --version
    which zsh
    
    # Setup .zshrc following promts
    zsh
    
    # Login mauro. -f indicates the user needs no further authentication (password)
    sudo login mauro -f
    
    # Change shell
    chsh -s $(which zsh)

  - Logout the user from ubuntu system (press the windows key then type
    “Log out” or **restart the computer**).

<!-- end list -->

    which zsh

  - [ ] [Install
    oh-my-zsh](https://github.com/ohmyzsh/ohmyzsh#basic-installation)

<!-- end list -->

    sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"

  - [ ] Install plugins for oh-my-szh

<!-- end list -->

    # [oh-my-zsh] plugin 'zsh-syntax-highlighting'
    cd ~/.oh-my-zsh/plugins/
    git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
    
    # [oh-my-zsh] plugin 'zsh-autosuggestions'
    cd ~/.oh-my-zsh/custom/plugins
    git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions

  - [ ] Install scripts

<!-- end list -->

    # [oh-my-zsh] autojump (https://github.com/wting/autojump)
    cd ~
    git clone git://github.com/wting/autojump.git
    cd autojump
    ./install.py
    # or
    #./uninstall.py

More: [Show current branch in the bash terminal
prompt](https://www.shellhacks.com/show-git-branch-terminal-command-prompt/):
This may already be in the .zshrc file

  - [ ] Install tmux

<!-- end list -->

    sudo apt install tmux

  - [ ] Install [dotfiles](https://github.com/maurolepore/dotfiles)

  - [ ] May need to temporarly dissable [2FA on
    GitHub](https://github.com/settings/security)

<!-- end list -->

    git clone https://github.com/maurolepore/dotfiles

  - [ ] Temoprarily comment out .Rprofile

### Other tools

  - [ ] [Install launchy](https://www.launchy.net/download.php#linux),
    e.g. launchy\_2.5-1\_amd64.deb. Then open Launcy from windows key,
    add to catalog \~/git/ with file type \*.rproj

<!-- end list -->

    cd Downloads
    sudo gdebi launchy_2.5-1_amd64.deb

## Bigger installs from the termianal

### R

  - [ ] Install R
    
      - Check version of Ubuntu

<!-- end list -->

    lsb_release -a

  - [Instructions for
    Ubuntu 18-04](https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-18-04-quickstart)
    (If you’re not using 18.04, find the relevant repository from the [R
    Project Ubuntu list](https://cloud.r-project.org/bin/linux/ubuntu/),
    named for each release.)

<!-- end list -->

    sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
    sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/'
    sudo apt update
    sudo apt install r-base

More:

  - <https://docs.rstudio.com/resources/install-r-source/>
  - pre-release: <https://cran.rstudio.com/src/base-prerelease/>

### RStudio

  - [ ] Install RStudio, e.g. rstudio-1.3.911-amd64.deb

  - [ ] Import [RStudio’s public code-signing
    key](https://rstudio.com/code-signing/)

<!-- end list -->

    gpg --keyserver keys.gnupg.net --recv-keys 3F32EE77E331692F

  - [ ] Download [RStudio
    release](https://rstudio.com/products/rstudio/download/#download) or
    [RStudio
    preview](https://rstudio.com/products/rstudio/download/preview/),
    say rstudio-1.3.911-amd64.deb, then validate the signature.

<!-- end list -->

    cd ~/Downloads
    dpkg-sig --verify rstudio-1.3.911-amd64.deb

  - [ ] Install RStudio

<!-- end list -->

    sudo gdebi rstudio-1.3.911-amd64.deb

More:
<https://linuxconfig.org/rstudio-on-ubuntu-18-04-bionic-beaver-linux>

## Setup ssh keys

  - [ ] [Setup ssh keys](https://happygitwithr.com/ssh-keys.html)

  - [ ] Enable [2FA on GitHub](https://github.com/settings/security)

## R setup

  - [ ] Setup R libraries

Setup user libraries by adding the environmental variable `R_LIBS_USER`
to a temporary local .Renviron file (for now in your current working
directory; you may later add this to a more permanent .Renviron – once
you install usethis you can do it with `usethis::edit_r_environ()`). Run
`.libPats()` and look for something similar to this (except that `%v`
should instead be your current R version, e.g. `3.6`):

    # Should expand to R_LIBS_USER="home/mauro/R/x86_64-pc-linux-gnu-library/%v"
    R_LIBS_USER="~/R/%p-library/%v"

(It’s important to get this right. I missed the “-library” bit and
`R_LIBS_USER` wasn’t used by `installed.packages()` – even though it
showed up by `Sys.getenv("R_LIBS_USER")`; weird.)

  - More: [Set up an R dev
    environment](https://rstats.wtf/set-up-an-r-dev-environment.html)

  - [ ] Install packages for development

<!-- end list -->

    install.packages("pak")
    pak::pkg_install(c("devtools", "testthat", "roxygen2"))
    pak::pkg_install(c("pkgdown", "spelling"))

  - [ ] Comment back in \~/.Rprofile

  - [ ] Restarting R has no complaint about unavailable packages listed
    in \~/.Rprofile

  - [ ] Get a situation report for git

<!-- end list -->

    usethis::git_sitrep()

  - [ ] \~/.Renviron uses correct `GITHUB_PAT`
  - [ ] \~/.Rprofile uses correct git protocol (https or ssh)