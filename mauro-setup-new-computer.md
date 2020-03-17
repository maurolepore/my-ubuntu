* [x] [Install ubuntu](https://ubuntu.com/tutorials/tutorial-install-ubuntu-desktop#1-overview), maybe alongside Windows.

* [x] Ensure user, e.g. mauro, owns ~ (/home/mauro) and all its contents:

```
chown mauro -R ~
```

Now mauro can add ssh keys at ~/.ssh, launch RStudio from a terminal at ~, etc.

More: 

* https://askubuntu.com/questions/633733/gdebi-core-package-is-not-available
* https://docs.rstudio.com/resources/install-r/

--



* [x] Install R

    * Check version of Ubuntu

```
lsb_release -a
```

    * [Instructions for Ubuntu 18-04](https://www.digitalocean.com/community/tutorials/how-to-install-r-on-ubuntu-18-04-quickstart) (If you’re not using 18.04, find the relevant repository from the [R Project Ubuntu list](https://cloud.r-project.org/bin/linux/ubuntu/), named for each release.)

```
sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys E298A3A825C0D65DFD57CBB651716619E084DAB9
sudo add-apt-repository 'deb https://cloud.r-project.org/bin/linux/ubuntu bionic-cran35/'
sudo apt update
sudo apt install r-base
```       

More:

* https://docs.rstudio.com/resources/install-r-source/
* pre-release: https://cran.rstudio.com/src/base-prerelease/

--



* [x] Install RStudio, e.g. rstudio-1.3.911-amd64.deb

     * [x] Import [RStudio's public code-signing key](https://rstudio.com/code-signing/)

```
gpg --keyserver keys.gnupg.net --recv-keys 3F32EE77E331692F

```

    * [x] Install the dpkg-sig package.

```
sudo apt install dpkg-sig
```

    * [x] Download [RStudio release](https://rstudio.com/products/rstudio/download/#download) or [RStudio preview](https://rstudio.com/products/rstudio/download/preview/), say rstudio-1.3.911-amd64.deb, then validate the signature.

```
cd ~/Downloads
dpkg-sig --verify rstudio-1.3.911-amd64.deb
```

    * [x] Install gdebi: 

```
sudo apt-get update
sudo apt-get install gdebi-core
```

    * [x] Install RStudio

```
sudo gdebi rstudio-1.3.911-amd64.deb
```

More:

* <https://linuxconfig.org/rstudio-on-ubuntu-18-04-bionic-beaver-linux>

--



* [ ] [Install an R development environment](https://www.jimhester.com/post/2017-10-13-docker/)

```
sudo apt-get update
sudo apt-get install -y libcurl4-openssl-dev libssl-dev libssh2-1-dev libxml2-dev
```

More:

* [Maybe you need more tools?](https://www.r-bloggers.com/installing-our-r-development-environment-on-ubuntu-16-04/)

--


* [x] Install more terminal tools
    
    * [x] Install vim

```
sudo apt install vim
```

    * [x] Install git

```
sudo apt install git
```

    * [ ] Install LaTeX

Necessary to build pdf manuals for R packages, and to run `devtools::check(remote = TRUE, manual = TRUE)`

```
# This is a large installation but a smaller one (texlive-base) didn't work for me
sudo apt-get install texlive-full
```




--


* [x] Install dotfiles


    * [x] Temporarily dissable 2FA at GitHub <https://github.com/settings/security>

```
git clone https://github.com/maurolepore/dotfiles
```




--


* [ ] Setup R libraries

* Setup user libraries by adding the environmental variable `R_LIBS_USER` to a temporary local .Renviron file (for now in your current working directory; you may later add this to a more permanent .Renviron -- once you install usethis you can do it with `usethis::edit_r_environ()`). Run `.libPats()` and look for something similar to this (except that `%v` should instead be your current R version, e.g. `3.6`):

```
R_LIBS_USER="home/mauro/R/x86_64-pc-linux-gnu-library/%v"
# Or
R_LIBS_USER="~/R/%p-library/%v"
```

(It's important to get this right. I missed the "-library" bit and `R_LIBS_USER` wasn't used by `installed.packages()` -- even though it showed up by `Sys.getenv("R_LIBS_USER")`; weird.)

* Chapter 9 Set up an R dev environment: https://rstats.wtf/set-up-an-r-dev-environment.html

* Setup ssh keys https://happygitwithr.com/ssh-keys.html

* Show current branch in the bash terminal prompt: https://www.shellhacks.com/show-git-branch-terminal-command-prompt/

* Install a launcher to make it easier to launch rstudio projects: https://www.launchy.net/ (add file type *.rproj to catalog)



