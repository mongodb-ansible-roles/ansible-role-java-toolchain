Ansible role for java-toolchain
==================================

Installs the java toolchain

[![CircleCI](https://img.shields.io/circleci/build/github/mongodb-ansible-roles/ansible-role-java-toolchain/master?style=flat-square)](https://circleci.com/gh/mongodb-ansible-roles/ansible-role-java-toolchain)

Requirements
------------

None

Role Variables
--------------

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-------:|:--------:|
| java\_toolchain\_sha | SHA of the golang toolchain you want to download | string | "" | yes |
| java\_toolchain\_dest | Destination to download toolchain | string | "/opt" | no |

Dependencies
------------

None

Example Playbook
----------------

```yaml
- hosts: all
  roles:
    - role: ansible-role-java-toolchain
      vars:
        java_toolchain_sha: 684d8a531d064469d4ca29e831e5929420e486d6
```

Development
-----------

Testing this role locally requires the CircleCI [Local CLI](https://circleci.com/docs/2.0/local-cli/).

To install the CLI for macOS and Linux, invoke the following command:

    $ curl -fLSs https://circle.ci/cli | DESTDIR=/usr/local/bin bash

After installing the CLI, invoke the following command to run the Molecule tests:

    $ make test

License
-------

[Apache License](LICENSE)
