# Package Applications

## fpm

> The goal of fpm is to make it easy and quick to build packages such as rpms, debs, OSX packages, etc

github: https://github.com/jordansissel/fpm

docs: https://fpm.readthedocs.io/en/latest/

### Debian install

(`sudo` required on chromebook crostini)

install prerequisites

`apt-get install ruby ruby-dev rubygems build-essential`

install fpm with gem tool

`sudo gem install --no-ri --no-rdoc fpm`

test install

`fpm --version`

### Usage

**Source: dir - Directories**
Synopsis:

`fpm -s dir [other flags] path1 [path2 ...]`

The ‘dir’ source will package up one or more directories for you.

**Path mapping**

Some times you want to take a path and copy it into a package but under a different location. fpm can use the = directive to mark that:

`fpm [...] -s dir ./example/foo=/usr/bin`

This will put the file foo in the /usr/bin directory inside the package.

