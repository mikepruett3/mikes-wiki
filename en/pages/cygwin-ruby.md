# Installing Ruby 2.3.0 on Cygwin x64

[Github - Ruby 2.3.0 on Cygwin x64](https://gist.github.com/aspyatkin/d2b28fc754e009bd4a48)

### Prerequisites
 - [Cygwin x64](http://cygwin.org/)
 - [apt-cyg](https://github.com/transcode-open/apt-cyg)

### Installation
#### Install essential packages
The following packages should be installed with `apt-cyg`:
 - git
 - gcc-core
 - gcc-g++
 - make
 - zlib-devel
 - curl
 - autoconf
 - libiconv
 - libiconv-devel
 - rsync
 - patch
 - unzip
 - openssh
 - openssl-devel
 - libxml2-devel
 - libxslt-devel
 - libffi-devel
 - libgdbm-devel
 - libreadline-devel

#### Install rbenv
Install [rbenv](https://github.com/rbenv/rbenv) and [ruby-build](https://github.com/rbenv/ruby-build) as usual.

#### Build Ruby 2.3.0
```
$ rbenv install 2.3.0
$ rbenv global 2.3.0
$ rbenv rehash
```

To check, run `ruby -v`. You will get something like that:
```
ruby 2.3.0p0 (2015-12-25 revision 53290) [x86_64-cygwin]
```
