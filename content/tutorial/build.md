---
weight: 2
title: Build and Install
bookToc: false
---

## Build and Install

#### OS

Currently only Linux environments are supported.

#### Dependencies

- cmake
- clang
- openssl
- libpcre

#### Build Release

```sh
git clone https://github.com/amelielabs/amelie
cd amelie
make release
```

#### Build Release (pass cmake options directly)

```sh
git clone https://github.com/amelielabs/amelie
cd amelie
cd build
cmake -DCMAKE_BUILD_TYPE=Release -DCMAKE_INSTALL_PREFIX=<install_path> .
make
```

#### Build Debug

```sh
git clone https://github.com/amelielabs/amelie
cd amelie
make debug
```

#### Running tests

```sh
make
cd test
../build/amelie test
```
