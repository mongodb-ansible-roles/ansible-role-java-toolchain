Ansible role for java-toolchain
==================================

Installs the java toolchain

[![GitHub Actions](https://github.com/mongodb-ansible-roles/ansible-role-java-toolchain/workflows/Molecule%20Test/badge.svg)](https://github.com/mongodb-ansible-roles/ansible-role-java-toolchain/actions?query=workflow%3A%22Molecule+Test%22)
[![GitHub Actions](https://github.com/mongodb-ansible-roles/ansible-role-java-toolchain/workflows/Release/badge.svg)](https://github.com/mongodb-ansible-roles/ansible-role-java-toolchain/actions?query=workflow%3A%22Release%22)

Explanation
-----------

This role will use the `/opt/java/toolchain_version` file to determine whether to install a new toolchain or not.

The `/opt/java/toolchain_version` file will be created by this role with the user specified `java_toolchain_sha` as its contents.

The `/opt/java/toolchain_version` file only shows the latest toolchain that was installed on the host. It does not have any record of older toolchain installations.

If the version file and `java_toolchain_sha` match, the toolchain will not be downloaded.

If the versions don't match, the new toolchain will be downloaded to the `/tmp` directory and then moved into the `/opt/java/revisions` directory. From there, the toolchain installation script is run.

This role will delete existing java toolchains if the version specified doesn't match.

Exception for PPC and s390x
---------------------------

The strategy for the Java toolchain on PPC and s390x is different than x86_64 and aarm64 machines.
Oracle does not offer a packages JDK for these platforms. Instead, we install Java through the system package manager and then create a "fake" Java toolchain at `/opt/java`. The jdk, usually jdk8, is then symlinked to that location from `/etc/alternatives/java_sdk_1.8.0` to `/opt/java/jdk8`. This is needed to run ant.

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

License
-------

[Apache License](LICENSE)
