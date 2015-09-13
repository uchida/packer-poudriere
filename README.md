# packer-poudriere

[![CircleCI](https://img.shields.io/circleci/project/uchida/packer-poudriere.svg)](https://circleci.com/gh/uchida/packer-poudriere)
[![License](https://img.shields.io/github/license/uchida/packer-poudriere.svg)](http://creativecommons.org/publicdomain/zero/1.0/deed)

packer template to build FreeBSD (zfsroot) with poudriere images

vagrant images are available at [uchida/poudriere](https://atlas.hashicorp.com/uchida/boxes/poudriere).

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

vagrant images at [Atlas](https://atlas.hashicorp.com) are released by [Circle CI](https://circleci.com/).
setup instructions are the following:

1. sign up
  - [Atlas](https://atlas.hashicorp.com/account/new)
  - [Circle CI](https://circleci.com/signup).
2. get API token
  - [Atlas](https://atlas.hashicorp.com/settings/tokens)
  - [Circle CI](https://circleci.com/account/api)
3. create build configuration at [Atlas](https://atlas.hashicorp.com/tutorial/packer-vagrant),
  this sets `ATLAS_USERNAME` and `ATLAS_NAME` environment variables
4. create project at [Circle CI](https://circleci.com/add-projects)
5. add atlas environment variables Circle CI project
6. edit circle.yml

```console
$ ATLAS_USERNAME={{ your atlas username here }}
$ ATLAS_NAME={{ your atlas box name here }}
$ ATLAS_TOKEN={{ your atlas api token here }}
$ CIRCLE_USERNAME={{ your circle ci username here }}
$ CIRCLE_PROJECT={{ your circle ci project here }}
$ CIRCLE_TOKEN={{ your circle ci token here }}
$ for name in ATLAS_USERNAME ATLAS_NAME ATLAS_TOKEN; do
    curl -X POST -H "Content-Type: application/json" -H "Accept: application/json" -d "{\"name\":\"$name\",\"value\":\"$(eval echo \$$name)\"}" "https://circleci.com/api/v1/project/$CIRCLE_USERNAME/$CIRCLE_PROJECT/envvar?circle-token=$CIRCLE_TOKEN"
  done
```

## License

[![CC0](http://i.creativecommons.org/p/zero/1.0/88x31.png "CC0")]
(http://creativecommons.org/publicdomain/zero/1.0/deed)

dedicated to public domain by [contributors](https://github.com/uchida/packer-poudriere/graphs/contributors).

