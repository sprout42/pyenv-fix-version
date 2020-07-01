# pyenv-fix-version

pyenv-fix-version is a [pyenv](https://github.com/pyenv/pyenv) plugin
that provides a `pyenv fix-version` command to try and fix up any missing
library dependencies there may be for an installed python version.

# Installation
### Installing as a pyenv plugin

Installing pyenv-fix-version as a pyenv plugin will allow running this tool
through pyenv: `pyenv fix-version`

```
$ git clone git://github.com/sprout42/pyenv-fix-version.git $(pyenv root)/plugins/pyenv-fix-version
```

## Dependencies

Currently only works on MacOS X and uses the following xcode commandlines tools:
- `otool`
- `install_name_tool`

## Usage

To check for any dependency issues in an installed pyenv version run:

```
$ pyenv fix-version
No problems found for 3.8.3
```

You can check for issues with any installed version using the `PYENV_VERSION`
variable:

```
$ PYENV_VERSION=2.7.16 pyenv fix-version
Cannot resolve the following dependencies for version 2.7.16:
  libcrypto.1.0.0.dylib
  libssl.1.0.0.dylib
```

If you have dependency issues that need corrected they can be fixed by providing
one or more directories to search for a matching filename:

```
$ PYENV_VERSION=2.7.16 pyenv fix-version /usr/local/Cellar/openssl

Searching for libssl.1.0.0.dylib
Changing "/usr/local/opt/openssl/lib/libssl.1.0.0.dylib" to "/usr/local/Cellar/openssl/1.0.2t/lib/libssl.1.0.0.dylib" in "/Users/user/.pyenv/versions/2.7.16/lib/python2.7/lib-dynload/_ssl.so"

Searching for libcrypto.1.0.0.dylib
Changing "/usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib" to "/usr/local/Cellar/openssl/1.0.2t/lib/libcrypto.1.0.0.dylib" in "/Users/user/.pyenv/versions/2.7.16/lib/python2.7/lib-dynload/_ssl.so"

Searching for libssl.1.0.0.dylib
Changing "/usr/local/opt/openssl/lib/libssl.1.0.0.dylib" to "/usr/local/Cellar/openssl/1.0.2t/lib/libssl.1.0.0.dylib" in "/Users/user/.pyenv/versions/2.7.16/lib/python2.7/lib-dynload/_hashlib.so"

Searching for libcrypto.1.0.0.dylib
Changing "/usr/local/opt/openssl/lib/libcrypto.1.0.0.dylib" to "/usr/local/Cellar/openssl/1.0.2t/lib/libcrypto.1.0.0.dylib" in "/Users/user/.pyenv/versions/2.7.16/lib/python2.7/lib-dynload/_hashlib.so"
```
