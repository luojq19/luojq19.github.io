---
title:  "Ubuntu Python Environment Setup"
date:   2023-02-09 23:50:00 +0800
permalink: /posts/2023/02/ubuntu-environment-setting/
tags:
  - utility
---

# oh-my-zsh
## Installation
```
sh -c "$(wget -O- https://raw.githubusercontent.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
## Themes
Modify `~/.zshrc`:  
`ZSH_THEME="agnoster"`

## Hide user name and machine name in the prompt
Add the following line to `~/.zshrc`:
```
prompt_context() {}
```

## Plugins
First download zsh-autosuggestions and zsh--syntax-highlighting:
```
git clone https://github.com/zsh-users/zsh-autosuggestions ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-autosuggestions
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```
Then modify `~/.zshrc`:  
```
plugins=(
    git
    last-working-dir
    z 
    extract
    zsh-syntax-highlighting
    zsh-autosuggestions
)
source $ZSH/plugins/extract/extract.plugin.zsh
source $ZSH/plugins/z/z.plugin.zsh
source $ZSH_CUSTOM/plugins/zsh-syntax-highlighting/zsh-syntax-highlighting.zsh
source $ZSH_CUSTOM/plugins/zsh-autosuggestions/zsh-autosuggestions.zsh
```

Run `source ~/.zshrc` to activate the changes.

# Anaconda
## Installation
Go to https://repo.anaconda.com/archive/ to find the newest version on your machine, e.g.
```
wget https://repo.anaconda.com/archive/Anaconda3-2022.10-Linux-x86_64.sh
```
Then run the installation script accordingly.

If the conda environment is not automatically activated, run `source ~/.zshrc`.

To create a new virtual environment, run
```
conda create -n env_name python=3.8
```

## Useful packages
**mamba:**  faster environment solving

**torch, torchvision:** refer to pytorch.org to install

**gpustat, nvtop:** convenient GPU status visualization

## Install jupyter notebook and nb_extensions
First install ipython:
```
conda install -c anaconda ipython
```
Run `ipython` command to check, if not working, deactivate and then activate the current env.

Then install jupyter notebook:
```
conda install -c anaconda notebook
```
Set up jupyter notebook remote access:
```
jupyter notebook --generate-config
```
Open `ipython`, and run the following code:
```
In [1]: from notebook.auth import passwd
In [2]: passwd()
Enter password:
Verify password:
Out[2]: 'sha1:cexxxxxxxxxxxxxxxxx'
```
Modify the config.py file just generated as follows:
```
c.NotebookApp.ip='*'
c.NotebookApp.password = u'sha1:ce...' # the cipher code above
c.NotebookApp.open_browser = False
c.NotebookApp.port =8888 # any port for access
```
If forgot the password, just regenerate the config file and regenerate the cipher code.

Install `nbextension`:
```
conda install -c conda-forge jupyter_contrib_nbextensions
```
Restart jupyter notebook, if not see nbextension, then run
```
jupyter contrib nbextension install --user --skip-running-check
```

To change different virtual env in jupyter notebook, install `nb_conda`:
```
conda install nb_conda
```

# gdrive
Refer to this [link](https://github.com/prasmussen/gdrive/issues/666) to install gdrive version 2.1.2.

# Install package without root access
Refer to this [link](https://askubuntu.com/questions/339/how-can-i-install-a-package-without-root-access)

## .deb approach
```
apt-get download package_name  # replace `package_name` with the name of the package.

dpkg -x package.deb dir
```