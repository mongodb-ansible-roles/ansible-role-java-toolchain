Ansible role for java-toolchain
==================================

Installs the java toolchain

[![CircleCI](https://img.shields.io/circleci/build/github/mongodb-ansible-roles/ansible-role-java-toolchain/master?style=flat-square)](https://circleci.com/gh/mongodb-ansible-roles/ansible-role-java-toolchain)

Explanation
-----------

This role will use the `/opt/java/toolchain_version` file to determine whether to install a new toolchain or not.

The `/opt/java/toolchain_version` file will be created by this role with the user specified `java_toolchain_sha` as its contents.

The `/opt/java/toolchain_version` file only shows the latest toolchain that was installed on the host. It does not have any record of older toolchain installations.

If the version file and `java_toolchain_sha` match, the toolchain will not be downloaded.

If the versions don't match, the new toolchain will be downloaded to the `/tmp` directory and then moved into the `/opt/java/revisions` directory. From there, the toolchain installation script is run.

This role will delete existing java toolchains if the version specified doesn't match.

Requirements
------------

`ansible-role-toolchain` must be up to date in your `requirements.yml`

    ---
    - src: git+https://github.com/mongodb-ansible-roles/ansible-role-toolchain.git
      version: v1.1.0

Role Variables
--------------

| Name | Description | Type | Default | Required |
|------|-------------|:----:|:-------:|:--------:|
| `java_toolchain_sha` | SHA of the Java toolchain you want to download | string | "" | yes |
| `java_toolchain_dest` | Final destination of the Java toolchain | string | `/opt/java` | yes |
| `java_toolchain_url` | You may specify a custom URL to download the Java toolchain from | string | `""` | no |

Dependencies
------------

- [`mongodb-ansible-roles.ansible-role-toolchain`](https://github.com/mongodb-ansible-roles/ansible-role-toolchain)

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
