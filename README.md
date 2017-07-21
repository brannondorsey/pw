# Bash password generator

Generate strong passwords using `/dev/urandom`. Creates a 17 character password using `a-zA-Z0-9._!@#$%^&*()` characters by default.

```bash
$ pw
ZScTXCIP6(8vbsFU@
```

## Install

```bash
# clone repo
git clone https://github.com/brannondorsey/pw
cd pw

# install in PATH...
sudo cp pw /usr/local/bin/pw

# or call from directory with
./pw
```

## Usage

Password length and custom character set can be passed as optional first and second arguments respectively. Number of passwords to generate can optionally be passed as the final parameter.

```
usage: pw [length [characters [num_passwords]]]
```

```bash
$ pw 10 a-zA-Z
KuacEiwjDT

$ pw 15 0-9 
264679522188786

# you must escape special bash characters
$ pw 17 a-z\!\& 
!q!gxglquw&nfrvlv

# generate 10 sh!tty passwords
$ pw 3 dog 10
god
dod
gog
odd
odd
goo
ddd
ogd
gdo
ooo
```

## What it do

Here is the script:

```bash
$ cat pw
#!/bin/sh

# usage: pw [length [characters]]
tr -dc "${2:-'a-zA-Z0-9._!@#$%^&*()'}" < /dev/urandom | fold -w "${1:-17}" | head -n "${3:-1}"
```
