
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

  - [ ] Mouse & touchpad\>
      - Primary button: right
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

## Installs outside the terminal

  - [ ] Install from Chrome from Firefix; login and sync personal and
    work accounts

  - [ ] Install Slack from Ubuntu software; find workspaces linked to
    personal and work accounts

  - [ ] Install VLC media or similar video player

## Nice-to-have installs

I do this first because it can improve the experience in all that
follows.

    # Launch files easily (e.g. rstudio projects) <https://www.launchy.net/download.php#linux>
    # TODO: Add to catalog ~/git/ with file type *.rproj
    cd Downloads
    sudo gdebi launchy_2.5-1_amd64.deb
    
    # Remove stuff safely to trash -- not forever as rm does
    cd ~
    git clone https://github.com/andreafrancia/trash-cli.git
    cd trash-cli
    sudo python setup.py install
    
    # Capture screen shots
    sudo apt-get install flameshot

## Must-have installs

  - [ ] Fundamental tools

<!-- end list -->

    sudo apt-get update
    
    # To write text anywhere on Unix
    sudo apt install vim
    
    # For version control
    sudo apt-get install git
    sudo apt-get install gitk
    
    # To verify linux-package signatures
    sudo apt-get install dpkg-sig
    
    # To install rstudio, and any software from tarballs
    sudo apt-get install gdebi-core
    
    # To get stuff from the internet
    sudo apt-get install curl
    
    # For knitr
    sudo apt-get install pandoc
    
    # To install an R development environment <https://www.jimhester.com/post/2017-10-13-docker/>
    sudo apt-get update
    sudo apt-get install -y libcurl4-openssl-dev libssl-dev libssh2-1-dev libxml2-dev

  - [ ] LaTeX to build pdf manuals for R packages

This is a big install, and takes several minutes. The smaller
texlive-base didn’t work for me.

    sudo apt-get install texlive-full

## Improve the terminal

  - [ ] [Install
    zsh](https://github.com/ohmyzsh/ohmyzsh/wiki/Installing-ZSH)

<!-- end list -->

    sudo apt install zsh
    
    # Confirm installation worked
    zsh --version
    which zsh
    
    # Make zsh the default login shell for the user, e.g. mauro. 
    # No need to setup .zshrc -- oh-my-zsh will later add .zshrc
    
    # Change shell
    chsh -s $(which zsh)

  - [ ] Logout the user from ubuntu system (^alt+del), then login again

<!-- end list -->

    # Confirmed it worked
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

  - [ ] Allow multiple terminal sessions

<!-- end list -->

    sudo apt install tmux

## Use my preferred settings

  - [ ] Install [dotfiles](https://github.com/maurolepore/dotfiles)
    (based on [jimhester’s](https://github.com/jimhester/dotfiles))

  - [ ] May need to temporarly dissable [2FA on
    GitHub](https://github.com/settings/security)

<!-- end list -->

    git clone https://github.com/maurolepore/dotfiles

## R

  - [ ] Install R

<!-- end list -->

    # Check version of Ubuntu
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

## RStudio

  - [ ] Download [RStudio
    release](https://rstudio.com/products/rstudio/download/#download) or
    [RStudio
    preview](https://rstudio.com/products/rstudio/download/preview/),
    say rstudio-1.3.911-amd64.deb, then validate the signature.

<!-- end list -->

    # Import RStudio's public code-signing key <https://rstudio.com/code-signing/>
    gpg --keyserver keys.gnupg.net --recv-keys 3F32EE77E331692F
    
    # Verify signature
    cd ~/Downloads
    dpkg-sig --verify rstudio-1.3.911-amd64.deb
    
    # Install RStudio
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

    # Start R from a toy project with an empty .Rprofile (which calls unavailable packages)
    mkdir toy
    cd toy
    touch .Rprofile
    
    # Launch R
    R
    
    # Confirm the libraries are correct
    Sys.getenv("R_LIBS_USER")
    
    # Confirm repository
    options("repos")
    
    # Install packages called in .Renviron
    install.packages("pak")
    pak::pkg_install(c("devtools", "testthat", "roxygen2"))
    pak::pkg_install(c("pkgdown", "spelling"))

  - [ ] Restarting R has no complaint about unavailable packages listed
    in \~/.Rprofile

  - [ ] Get a situation report for git

<!-- end list -->

    usethis::git_sitrep()

  - [ ] \~/.Renviron uses correct `GITHUB_PAT`
  - [ ] \~/.Rprofile uses correct git protocol (https or ssh)

## Docker

<https://docs.docker.com/install/linux/docker-ce/ubuntu/>

    # Uninstall old docker versions if any
    sudo apt-get remove docker docker-engine docker.io containerd runc
    
    # Install
    sudo apt-get update
    sudo apt-get install \
        apt-transport-https \
        ca-certificates \
        curl \
        gnupg-agent \
        software-properties-common
    
    curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
    
    # Verify fingerprint
    sudo apt-key fingerprint 0EBFCD88
    
    # Setup stable repository
    sudo add-apt-repository \
       "deb [arch=amd64] https://download.docker.com/linux/ubuntu \
       $(lsb_release -cs) \
       stable"
    
    sudo apt-get update
    sudo apt-get install docker-ce docker-ce-cli containerd.io

  - [ ] [Avoid
    sudo](https://docs.docker.com/install/linux/linux-postinstall/)

<!-- end list -->

    sudo groupadd docker
    sudo usermod -aG docker $USER
    newgrp docker
    
    # Verify
    docker run --rm hello-world
    
    # Pull develpment version of R (RD) along side released version of R (R)
    docker pull rocker/r-devel

## Install my shell commands

    cd ~
    git clone git@github.com:maurolepore/bin.git
