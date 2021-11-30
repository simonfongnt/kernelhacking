# kernelhacking

## Problem with `sudo make`
1. `make[1]: *** No rule to make target 'debian/canonical-certs.pem', needed by 'certs/x509_certificate_list'.  Stop.`- `5.11.0-40-generic`
* [openssl req -x509 -newkey rsa:4096 -keyout certs/mycert.pem -out certs/mycert.pem -nodes -days 3650](https://askubuntu.com/questions/1329538/compiling-the-kernel-5-11-11)
3. 
