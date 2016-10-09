## Overview

Intended as an environment to play with development tools for apprentices, trainees, or anyone to work on.

## Quickstart

* Install ansible
* Run vagrant up


## Setup

### Pre-requisites

* VirtualBox
* Vagrant
* Python 
* OpenSSL - Need to build for MacOS

The code was developed and tested on a Mac but should work fine on other platforms that meet the above requirements.

See the background section below for details on the dependencies for MacOS.


### Installing ansible

Since Ansible has been packaged for use with pip I've used virtualenv for python to allow a local installation that doesn't need admin access or muck up any of your system libraries.  I prefer this approach as it's cleaner and has less in the way of side-affects.  Feel free to install ansible from RPMs/.deb or other package managers onto your system natively if that is easier for you.

Create a virtual python environment and activate it

```
virtualenv ansible-env
. ansible-env/bin/activate
```

Install ansible

```
pip install ansible
pip install passlib 
```

The passlib module is needed for password generation


### Inital VM

Start VM using this

```
vagrant up
```

## Background

### Missing ffi.h file

It seems that attempting to install recent ansible on macOS Sierra results in errors like this:

```
(ansible-env)melman:vagrant-general-development fiona$ pip install ansible
You are using pip version 6.0.8, however version 8.1.2 is available.
You should consider upgrading via the 'pip install --upgrade pip' command.
Collecting ansible
  Downloading ansible-2.1.2.0.tar.gz (1.9MB)
    100% |################################| 1.9MB 221kB/s 
Collecting paramiko (from ansible)
  Downloading paramiko-2.0.2-py2.py3-none-any.whl (171kB)
    100% |################################| 172kB 782kB/s 
Collecting jinja2 (from ansible)
  Downloading Jinja2-2.8-py2.py3-none-any.whl (263kB)
    100% |################################| 266kB 418kB/s 
Collecting PyYAML (from ansible)
  Downloading PyYAML-3.12.tar.gz (253kB)
    100% |################################| 253kB 425kB/s 
Requirement already satisfied (use --upgrade to upgrade): setuptools in ./ansible-env/lib/python2.7/site-packages (from ansible)
Collecting pycrypto>=2.6 (from ansible)
  Downloading pycrypto-2.6.1.tar.gz (446kB)
    100% |################################| 446kB 429kB/s 
Collecting pyasn1>=0.1.7 (from paramiko->ansible)
  Downloading pyasn1-0.1.9-py2.py3-none-any.whl
Collecting cryptography>=1.1 (from paramiko->ansible)
  Downloading cryptography-1.5.2.tar.gz (400kB)
    100% |################################| 401kB 636kB/s 
Collecting MarkupSafe (from jinja2->ansible)
  Downloading MarkupSafe-0.23.tar.gz
Collecting idna>=2.0 (from cryptography>=1.1->paramiko->ansible)
  Downloading idna-2.1-py2.py3-none-any.whl (54kB)
    100% |################################| 57kB 707kB/s 
Collecting six>=1.4.1 (from cryptography>=1.1->paramiko->ansible)
  Downloading six-1.10.0-py2.py3-none-any.whl
Collecting enum34 (from cryptography>=1.1->paramiko->ansible)
  Downloading enum34-1.1.6-py2-none-any.whl
Collecting ipaddress (from cryptography>=1.1->paramiko->ansible)
  Downloading ipaddress-1.0.17-py2-none-any.whl
Collecting cffi>=1.4.1 (from cryptography>=1.1->paramiko->ansible)
  Downloading cffi-1.8.3.tar.gz (403kB)
    100% |################################| 405kB 570kB/s 
Collecting pycparser (from cffi>=1.4.1->cryptography>=1.1->paramiko->ansible)
  Downloading pycparser-2.14.tar.gz (223kB)
    100% |################################| 225kB 567kB/s 
Installing collected packages: pycparser, cffi, ipaddress, enum34, six, idna, MarkupSafe, cryptography, pyasn1, pycrypto, PyYAML, jinja2, paramiko, ansible
  Running setup.py install for pycparser
    Build the lexing/parsing tables
  Running setup.py install for cffi
    building '_cffi_backend' extension
    cc -fno-strict-aliasing -fno-common -dynamic -arch i386 -arch x86_64 -g -Os -pipe -fno-common -fno-strict-aliasing -fwrapv -DENABLE_DTRACE -DMACOSX -DNDEBUG -Wall -Wstrict-prototypes -Wshorten-64-to-32 -DNDEBUG -g -fwrapv -Os -Wall -Wstrict-prototypes -DENABLE_DTRACE -arch i386 -arch x86_64 -pipe -DUSE__THREAD -I/usr/include/ffi -I/usr/include/libffi -I/System/Library/Frameworks/Python.framework/Versions/2.7/include/python2.7 -c c/_cffi_backend.c -o build/temp.macosx-10.12-intel-2.7/c/_cffi_backend.o
    c/_cffi_backend.c:15:10: fatal error: 'ffi.h' file not found
    #include <ffi.h>
             ^
    1 error generated.
    error: command 'cc' failed with exit status 1
    Complete output from command /Users/fiona/wd/fionahiklas/vagrant-general-development/ansible-env/bin/python -c "import setuptools, tokenize;__file__='/private/var/folders/3v/g0gf81jx1gj0_k96xgb0nk5w0000gp/T/pip-build-BslVEO/cffi/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /var/folders/3v/g0gf81jx1gj0_k96xgb0nk5w0000gp/T/pip-_cYesP-record/install-record.txt --single-version-externally-managed --compile --install-headers /Users/fiona/wd/fionahiklas/vagrant-general-development/ansible-env/include/site/python2.7:
    running install
    
    running build
    
    running build_py
    
    creating build
    
    creating build/lib.macosx-10.12-intel-2.7
    
    creating build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/__init__.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/api.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/backend_ctypes.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/cffi_opcode.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/commontypes.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/cparser.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/ffiplatform.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/lock.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/model.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/recompiler.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/setuptools_ext.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/vengine_cpy.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/vengine_gen.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/verifier.py -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/_cffi_include.h -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/parse_c_type.h -> build/lib.macosx-10.12-intel-2.7/cffi
    
    copying cffi/_embedding.h -> build/lib.macosx-10.12-intel-2.7/cffi
    
    running build_ext
    
    building '_cffi_backend' extension
    
    creating build/temp.macosx-10.12-intel-2.7
    
    creating build/temp.macosx-10.12-intel-2.7/c
    
    cc -fno-strict-aliasing -fno-common -dynamic -arch i386 -arch x86_64 -g -Os -pipe -fno-common -fno-strict-aliasing -fwrapv -DENABLE_DTRACE -DMACOSX -DNDEBUG -Wall -Wstrict-prototypes -Wshorten-64-to-32 -DNDEBUG -g -fwrapv -Os -Wall -Wstrict-prototypes -DENABLE_DTRACE -arch i386 -arch x86_64 -pipe -DUSE__THREAD -I/usr/include/ffi -I/usr/include/libffi -I/System/Library/Frameworks/Python.framework/Versions/2.7/include/python2.7 -c c/_cffi_backend.c -o build/temp.macosx-10.12-intel-2.7/c/_cffi_backend.o
    
    c/_cffi_backend.c:15:10: fatal error: 'ffi.h' file not found
    
    #include <ffi.h>
    
             ^
    
    1 error generated.
    
    error: command 'cc' failed with exit status 1
    
    ----------------------------------------
    Command "/Users/fiona/wd/fionahiklas/vagrant-general-development/ansible-env/bin/python -c "import setuptools, tokenize;__file__='/private/var/folders/3v/g0gf81jx1gj0_k96xgb0nk5w0000gp/T/pip-build-BslVEO/cffi/setup.py';exec(compile(getattr(tokenize, 'open', open)(__file__).read().replace('\r\n', '\n'), __file__, 'exec'))" install --record /var/folders/3v/g0gf81jx1gj0_k96xgb0nk5w0000gp/T/pip-_cYesP-record/install-record.txt --single-version-externally-managed --compile --install-headers /Users/fiona/wd/fionahiklas/vagrant-general-development/ansible-env/include/site/python2.7" failed with error code 1 in /private/var/folders/3v/g0gf81jx1gj0_k96xgb0nk5w0000gp/T/pip-build-BslVEO/cffi
```

Found a solution documented [here](http://stackoverflow.com/questions/22875270/error-installing-bcrypt-with-pip-on-os-x-cant-find-ffi-h-libffi-is-installed)

Installed the latest XCode tools using the following command

```
xcode-select --install
```

### Missing OpenSSL headers

After the above problems more compile errors occur when trying to install Ansible using pip.

After some research it seems that MacOS doesn't ship with OpenSSL headers.  To resolve this issue I needed to download and build the OpenSSL library.

The archive was downloaded from [here](https://www.openssl.org/source/openssl-1.1.0b.tar.gz)

Instructions for building can be found [here](https://wiki.openssl.org/index.php/Compilation_and_Installation#OS_X)

Un-archived and then ran the following commands to build and deploy

```
./Configure darwin64-x86_64-cc shared enable-ec_nistp_64_gcc_128 no-ssl2 no-ssl3 no-comp --openssldir=/usr/local/ssl/macos-x86_64
make depend
make
su - admin
cd <working directory> # substitue path to where the OpenSSL code is
sudo make install
```

Now running the commands to install ansible appears to work and is able to pickup the OpenSSL headers/library.

### Python2 Dependency

Apparently Ansible [now needs python2](http://stackoverflow.com/questions/32429259/ansible-fails-with-bin-sh-1-usr-bin-python-not-found#34402816)

The dependencies are given [here](http://docs.ansible.com/ansible/intro_installation.html#managed-node-requirements)


### Creating Users

The ansible script creates a developer user but needs to handle forcing the password to change.  There are some links that may help with this

* Creating user and password [stackoverflow post](http://stackoverflow.com/questions/19292899/creating-a-new-user-and-password-with-ansible)
* Documention for [user module](http://docs.ansible.com/ansible/user_module.html)



