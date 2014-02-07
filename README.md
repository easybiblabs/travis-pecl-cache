travis-pecl-cache
=================

Example Repository to show Pecl Caching on Travis

This repository is an example how to cache pecl modules
between travis builds to speed up the test cycle.

Its current status is "works for me": It does its job on
the repo where I need it, but is only roughly tested, and
there sure are edge cases where it breaks. Use with caution.

Usage
=====
Copy the lines from ```before_install```, ```before_script```
and ```cache``` to your own ```.travis.yml```.

Adjust the content of the MODULE envvar to your needs. The
pattern to use is "NAME\_OF\_THE\_MODULE.so:NAME\_OF\_THE\_PECL\_PACKAGE",
separated by a space.

The shell script first tries to copy all found modules in the cache to
the current php extension dir, and then compiles (and then caches) every
module where the file is not yet there. It does not check the validity or
integrity of the file.

The modules are not enabled by this script, you have to do so on your own
using Travis ```phpenv config-add php.some.file.ini``` mechanism.

Warning
======
Since this script just adds the modules (and continues to do so for every
php version update on travis), you might want clear/clean up the travis cache
occasionally.