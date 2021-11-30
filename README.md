# kernelhacking

## Requirements
* [setup the platform](https://kernelnewbies.org/OutreachyfirstpatchSetup)
* [follw the guideline](https://kernelnewbies.org/FirstKernelPatch)

## Problem with `sudo make`
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

## Revert Grub / Boot menu
```
uname -srm  # get kernel version e.g. Linux 5.16.0-rc3+
locate "*5.16.0-rc3*" | sudo xargs -ixxx rm -rf 'xxx'
sudo update-grub2
```

## Problem with `checkpatch.pl`
```
ModuleNotFoundError: No module named 'ply'
```
`pip uninstall ply; pip uninstall pyhcl; pip install ply; pip install pyhcl`

`conda install ply`

```
ModuleNotFoundError: No module named 'git'
```
`pip install gitpython`
