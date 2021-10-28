[:house_with_garden:](../../index.md)

Debian
-

1. How to Install a Debian Minimal Server [:door:](https://www.howtoforge.com/tutorial/debian-minimal-server/)

2. Configure the server
```shell
sudo apt remove vim-common
sudo apt install dnsutils net-tools curl vim
sudo update-alternatives --config editor

# choose vim.basic
```

3. how to set up ssh keys [:door:](https://linuxize.com/post/how-to-set-up-ssh-keys-on-debian-10/)
```shell
# setup user login over ssh
mkdir -p ~/.ssh
touch ~/.ssh/authorized_keys
# add your public key into authorized_keys 

# disable password login
# update value in /etc/ssh/sshd_config

# To disable tunneled clear text passwords, change to no here!
# PasswordAuthentication * => PasswordAuthentication no
# PermitEmptyPasswords * => PermitEmptyPasswords no
# ChallengeResponseAuthentication * => ChallengeResponseAuthentication no
# UsePAM * => UsePAM no

# disbale root login
# PermitRootLogin * => PermitRootLogin no
sudo systemctl restart sshd
```

4. set up some alias
```shell
# Add alias
alias reboot='systemctl reboot'
alias poweroff='systemctl poweroff'
```

5. add a new user
```shell
# Then add a new user that will be able to use sudo.
useradd -m -G sudo <username> # (-m creates the home directory /home/user; -G adds the user to the sudoers group)
# set the password for the new user
passwd <username>
```
6. sudo without password [:door:](https://bingozb.github.io/views/default/58.html#%E8%A7%A3%E5%86%B3)
```shell
sudo su -
echo "`whoami`     ALL=(ALL) NOPASSWD:ALL" > /etc/sudoers.d/sudoers
"`whoami` ALL=(ALL) NOPASSWD: NOPASSWD: ALL"
```


8. Arrow keys don't work in insert mode
* Research [:see_no_evil:](https://vi.stackexchange.com/questions/9760/arrow-keys-dont-work-in-insert-mode)
```shell
user@debian:~$ cat /etc/vim/vimrc.tiny
" Vim configuration file, in effect when invoked as "vi". The aim of this
" configuration file is to provide a Vim environment as compatible with the
" original vi as possible. Note that ~/.vimrc configuration files as other
" configuration files in the runtimepath are still sourced.
" When Vim is invoked differently ("vim", "view", "evim", ...) this file is
" _not_ sourced; /etc/vim/vimrc and/or /etc/vim/gvimrc are.

" Debian system-wide default configuration Vim
set runtimepath=~/.vim,/var/lib/vim/addons,/usr/share/vim/vimfiles,/usr/share/vim/vim82,/usr/share/vim/vimfiles/after,/var/lib/vim/addons/after,~/.vim/after

set compatible

" vim: set ft=vim:
```

```shell
user@debian:~$ cat /etc/vim/vimrc.tiny
" Vim configuration file, in effect when invoked as "vi". The aim of this
" configuration file is to provide a Vim environment as compatible with the
" original vi as possible. Note that ~/.vimrc configuration files as other
" configuration files in the runtimepath are still sourced.
" When Vim is invoked differently ("vim", "view", "evim", ...) this file is
" _not_ sourced; /etc/vim/vimrc and/or /etc/vim/gvimrc are.

" Debian system-wide default configuration Vim
set runtimepath=~/.vim,/var/lib/vim/addons,/usr/share/vim/vimfiles,/usr/share/vim/vim82,/usr/share/vim/vimfiles/after,/var/lib/vim/addons/after,~/.vim/after

set nocompatible
set backspace=2

" vim: set ft=vim:
```

or vim-full
```shell
sudo apt remove vim-common
sudo apt install vim
```

or
```shell
echo "set nocompatible" >> .vimrc
echo "set backspace=2" >> .vimrc
```