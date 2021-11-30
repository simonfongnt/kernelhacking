# kernelhacking

## Requirements
* [setup the platform](https://kernelnewbies.org/OutreachyfirstpatchSetup)
* [follw the guideline](https://kernelnewbies.org/FirstKernelPatch)
* vim setup
```
# ~/.vimrc
filetype plugin indent on
syntax on
set title
set tabstop=8
set softtabstop=8
set shiftwidth=8
set noexpandtab
set list listchars=tab:»\ ,trail:·,extends:»,precedes:«                                                       
```
## Steps
1. `find drivers/staging -name TODO` - see what's left to fix
2. `vim drivers/staging/XXX/TODO` - read what to fix
3. `perl scripts/checkpatch.pl -f --terse drivers/staging/XXX/* | less` - check issues of individual module
4. `vim drivers/staging/XXX/XXX.c` - fix it
5. `git add drivers/staging/XXX/XXX.c` - update to git
6. `git commit -s -v` - commit to git
7. `git format-patch -o /tmp/ HEAD^` - patch it
8. `./scripts/checkpatch.pl /tmp/0001-PATCH-staging-XXX-Fix-???.patch` - check patch format
9. `./scripts/get_maintainer.pl /tmp/0001-PATCH-staging-XXX-Fix-???.patch` - find out who to send
10. `mutt -H /tmp/0001-PATCH-staging-XXX-Fix-???.patch` - send it, multiple recipient divided by `,`

## Troubleshoot

### `sudo make`
```
make[1]: *** No rule to make target 'debian/canonical-certs.pem', needed by 'certs/x509_certificate_list'.  Stop.
```

`openssl req -x509 -newkey rsa:4096 -keyout certs/mycert.pem -out certs/mycert.pem -nodes -days 3650`[(1)](https://askubuntu.com/questions/1329538/compiling-the-kernel-5-11-11)

```
BTF: .tmp_vmlinux.btf: pahole (pahole) is not available
Failed to generate BTF for vmlinux
Try to disable CONFIG_DEBUG_INFO_BTF
make: *** [Makefile:1161: vmlinux] Error 1
```
`sudo apt install dwarves`[(2)](https://stackoverflow.com/questions/61657707/btf-tmp-vmlinux-btf-pahole-pahole-is-not-available)

### Undo Module Installation (Remove built kernel)
```
uname -srm  # get kernel version e.g. Linux 5.16.0-rc3+
locate "*5.16.0-rc3*" | sudo xargs -ixxx rm -rf 'xxx'
sudo update-grub2
```

### `checkpatch.pl`
```
ModuleNotFoundError: No module named 'ply'
```
`pip uninstall ply; pip uninstall pyhcl; pip install ply; pip install pyhcl`

`conda install ply`

```
ModuleNotFoundError: No module named 'git'
```
`pip install gitpython`

### `git commit -s -v`
```
fatal: unable to auto-detect email address
```
`git config user.email "you@example.com"`

`git config user.name "Your Name"`

### Undo a commit
`git commit --amend`
or

`git reset --hard HEAD^`
or

`git checkout HEAD^^ -- . and then git add -A && git commit`
