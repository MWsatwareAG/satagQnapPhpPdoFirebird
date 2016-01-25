# PHP Firebird PDO for Qnap x86 NAS

This Vagrantfile compiles the PHP Firebird PDO extension to use on Qnap x86 based NAS systems.

The extension was tested on the following system(s):
* TS-251, Firmware: 4.2.0, PHP Version: 5.5.29

It requires the following steps:

1. Start the [Vagrant](https://www.vagrantup.com) machine `vagrant up` - it may be time to fetch a coffee, this will take some time.  The Vagrant machine creates two files `libfbclient.so.2` and `pdo_firebird.so`
2. Enable ssh access to your Qnap NAS and copy the two files to the following places:
    * Copy `pdo_firebird.so` to `/usr/local/apache/modules/`
    * Copy `libfbclient.so.2` to `/usr/local/lib/`
3. Run `ldconfig` once to include the shared library
4. Run `ldd /usr/local/apache/modules/pdo_firebird.so` to check that all libraries are loaded
5. Edit the php.ini and add the following lines
```
[firebird]
extension = pdo_firebird.so
```
6. Restart the webserver with `/etc/init.d/Qthttpd.sh restart` or by rebooting the NAS
7. Check `phpinfo()` output, it should contain the line  **PDO Driver for Firebird** *enabled*