# packer-poudriere

[![CircleCI](https://img.shields.io/circleci/project/uchida/packer-poudriere.svg)](https://circleci.com/gh/uchida/packer-poudriere)
[![License](https://img.shields.io/github/license/uchida/packer-poudriere.svg)](http://creativecommons.org/publicdomain/zero/1.0/deed)

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

Vagrant images at [Atlas](https://atlas.hashicorp.com) are released by [Circle CI](https://circleci.com/).
setup instructions are the following:

1. Sign up
  - [Atlas](https://atlas.hashicorp.com/account/new)
  - [Circle CI](https://circleci.com/signup).
2. Get API token
  - [Atlas](https://atlas.hashicorp.com/settings/tokens)
  - [Circle CI](https://circleci.com/account/api)
3. Create build configuration at [Atlas](https://atlas.hashicorp.com/tutorial/packer-vagrant),
  this sets `ATLAS_USERNAME` and `ATLAS_NAME` environment variables to build configuration
4. Create project at [Circle CI](https://circleci.com/add-projects)
5. Add Atlas environment variables to Circle CI project:
  ```console
  $ ATLAS_USERNAME={{ your atlas username here }}
  $ ATLAS_NAME={{ your atlas box name here }}
  $ ATLAS_TOKEN={{ your atlas api token here }}
  $ CIRCLE_USERNAME={{ your circle ci username here }}
  $ CIRCLE_PROJECT={{ your circle ci project here }}
  $ CIRCLE_TOKEN={{ your circle ci token here }}
  $ CIRCLE_ENVVARENDPOINT="https://circleci.com/api/v1/project/$CIRCLE_USERNAME/$CIRCLE_PROJECT/envvar?circle-token=$CIRCLE_TOKEN"
  $ CIRCLE_POST_OPTS='-X POST -H "Content-Type: application/json" -H "Accept: application/json"'
  $ for name in ATLAS_USERNAME ATLAS_NAME ATLAS_TOKEN; do
      value=$(eval echo \$$name)
      curl $CIRCLE_POST_OPTS -d "{\"name\":\"$name\",\"value\":\"$value\"}" "$CIRCLE_ENVVARENDPOINT"
    done

  ```
6. Edit circle.yml


## License

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")]
(http://creativecommons.org/publicdomain/zero/1.0/deed)

dedicated to public domain by [contributors](https://github.com/uchida/packer-poudriere/graphs/contributors).
