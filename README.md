# wax

[![Build Status](https://travis-ci.org/chocolateboy/App-Wax.svg?branch=master)](https://travis-ci.org/chocolateboy/App-Wax)
[![CPAN](https://img.shields.io/cpan/v/App-Wax.svg)](http://search.cpan.org/dist/App-Wax/)

<!-- START doctoc generated TOC please keep comment here to allow auto update -->
<!-- DON'T EDIT THIS SECTION, INSTEAD RE-RUN doctoc TO UPDATE -->

- [NAME](#name)
- [SYNOPSIS](#synopsis)
- [DESCRIPTION](#description)
- [INSTALLATION](#installation)
  - [INSTALL](#install)
  - [UPDATE](#update)
  - [UNINSTALL](#uninstall)
- [EXAMPLES](#examples)
  - [espeak](#espeak)
  - [grep](#grep)
  - [jsview](#jsview)
  - [nman](#nman)
- [VERSION](#version)
- [SEE ALSO](#see-also)
- [AUTHOR](#author)
- [COPYRIGHT AND LICENSE](#copyright-and-license)

<!-- END doctoc generated TOC please keep comment here to allow auto update -->

## NAME

wax - webify your CLI

## SYNOPSIS

    wax [OPTIONS] program [OPTIONS] ...

e.g.:

    $ wax vim -R https://registry.npmjs.org/left-pad/-/left-pad-1.2.0.tgz

runs:

    $ vim -R /tmp/wax_abcd1234.tgz

## DESCRIPTION

`wax` is a command-line program which runs other command-line programs and converts their URL
arguments to local file paths. By default, the files are removed after the command has exited.

As well as adding transparent support for remote resources to commands that don't support them
natively, `wax` can be used to:

- add support for HTTPS (and any other protocols supported by [LWP](https://metacpan.org/pod/LWP)) to programs that only support HTTP
- add a mirroring layer to network requests (remote resources are only fetched if they've been updated)
- add a caching layer to network requests (remote resources are only fetched once)

For more details, see the `wax` [man page](bin/README.md).

## INSTALLATION

### INSTALL

Install [cpanminus](https://github.com/miyagawa/cpanminus#installation) if it's not already installed,
then:

    cpanm App::Wax

### UPDATE

    cpanm App::Wax

### UNINSTALL

    cpanm --uninstall App::Wax

## EXAMPLES

### espeak

    $ alias espeak="wax espeak"
    $ espeak -f http://www.setec.org/mel.txt

### grep

    $ wax grep -B1 demons http://www.mplayerhq.hu/DOCS/man/en/mplayer.1.txt

### jsview

Browse files in Node module tarballs

```bash
#!/bin/sh

# usage: jsview <module> e.g. jsview left-pad
wax --cache view $(npm info --json "$@" | jq -r .dist.tarball)
```

### nman

Node.js man-page viewer

```bash
#!/bin/sh

node_version=${NODE_VERSION:-`node --version`}
docroot="https://cdn.rawgit.com/nodejs/node/$node_version/doc/api"
wax --cache -D pandoc --standalone --from markdown --to man "$docroot/$1.md" | man -l -
```

## VERSION

2.0.0

## SEE ALSO

- [rlwrap](http://utopia.knoware.nl/~hlub/uck/rlwrap/#rlwrap)
- [sshfs](http://fuse.sourceforge.net/sshfs.html)
- [zsh completion script](https://github.com/chocolateboy/App-Wax/wiki/Zsh-completion-script)

## AUTHOR

[chocolateboy](mailto:chocolate@cpan.org)

## COPYRIGHT AND LICENSE

Copyright (C) 2010-2018 by chocolateboy

This library is free software; you can redistribute it and/or modify
it under the same terms as Perl itself, either Perl version 5.10.1 or,
at your option, any later version of Perl 5 you may have available.
