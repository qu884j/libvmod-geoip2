libvmod-geoip2
==============

[![Gitter](https://badges.gitter.im/Join Chat.svg)](https://gitter.im/fgsch/libvmod-geoip2?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)
[![Build Status](https://travis-ci.org/fgsch/libvmod-geoip2.svg?branch=master)](https://travis-ci.org/fgsch/libvmod-geoip2)

## About

A Varnish 4.x VMOD to query MaxMind GeoIP2 DB files.

## Requirements

To build this VMOD you will need:

* make
* a C compiler, e.g. GCC or clang
* pkg-config
* python-docutils
* libvarnishapi-dev in Debian/Ubuntu or varnish-libs-devel in CentOS/RedHat
* libmaxminddb-dev in recent Debian/Ubuntu releases. See also
  https://github.com/maxmind/libmaxminddb

If you are building from Git, you will also need:

* autoconf
* automake
* libtool

In addition, to run the tests you will need:

* varnish

If varnish is installed in a non-standard prefix you will also need
to set `PKG_CONFIG_PATH` to the directory where **varnishapi.pc** is
located before running `autogen.sh` and `configure`.  For example:

```
export PKG_CONFIG_PATH=/usr/local/lib/pkgconfig
```

Finally, to use it you will need one or more GeoIP2 or GeoLite2 databases.
See https://dev.maxmind.com/.

## Installation

### From a tarball

To install this VMOD, run the following commands:

```
./configure
make
make check
sudo make install
```

The `make check` step is optional but it's good to know whether the
tests are passing on your platform.

### From the Git repository

To install from Git, clone this repository by running:

```
git clone --recursive https://github.com/fgsch/libvmod-geoip2
```

And then run `./autogen.sh` followed by the instructions above for
installing from a tarball.

## Example

```
import geoip2;

sub vcl_init {
	new country = geoip2.geoip2("GeoLite2-Country.mmdb");
}

sub vcl_recv {
	if (country.lookup("country/names/en", client.ip) != "Japan") {
		...
	}
}
```

## License

This VMOD is licensed under BSD license. See LICENSE for details.
