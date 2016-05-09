# packer-poudriere

![Version](https://img.shields.io/github/tag/uchida/packer-poudriere.svg?maxAge=2592000)
[![License](https://img.shields.io/github/license/uchida/packer-poudriere.svg?maxAge=2592000)](https://tldrlegal.com/license/creative-commons-cc0-1.0-universal)
[![CircleCI](https://img.shields.io/circleci/project/uchida/packer-poudriere.svg?maxAge=2592000)](https://circleci.com/gh/uchida/packer-poudriere)

packer template for building poudriere, clean room package builder for FreeBSD,
including jail to build FreeBSD 9 and 10 packages and default ports tree.

The Vagrant image is available at [uchida/poudriere](https://atlas.hashicorp.com/uchida/boxes/poudriere).

```console
vagrant init uchida/poudriere; vagrant up
```

## Building Images

To build images, simply run:

```console
$ git clone https://github.com/uchida/packer-poudriere
$ cd packer-poudriere
$ packer build template.json
```

If you want to build only virtualbox, vmware or qemu.

```console
$ packer build -only=virtualbox-iso template.json
$ packer build -only=vmware-iso template.json
$ packer build -only=qemu template.json
```

## Release setup

```console
$ cp template.json template.json.orig
$ jq ".variables.version = \"$(git describe --abbrev=0 --tags)\"" template.json.orig > template.json
$ "diff -uB template.json{.orig,} || :"
$ packer build template.json
```

## License

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")]
(http://creativecommons.org/publicdomain/zero/1.0/deed)

dedicated to public domain, no rights reserved.
