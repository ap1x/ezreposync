# ezreposync

Create local EL6/7 yum repositories with group and security metadata. Multiple repos can be specified, defaults to all enabled. Remote repo(s) are downloaded and local repo(s) are created, there is no need to run `createrepo`. Group and security metadata are included in the local repo(s) when found.

This tool automates the procedure described by Red Hat [here](https://access.redhat.com/solutions/23016) and tries to emulate the behavior of `reposync` in EL8.

## Requirements

* Enterprise Linux 6 or 7 (RHEL, CentOS)
* `yum-utils` and `createrepo`

## Usage

```
Usage: ezreposync [OPTIONS] [repoid] ...
Sync yum repo(s) with group and security metadata. Defaults to all enabled.
Compatable with EL6/7. Requires yum-utils and createrepo. Must be run as root.

Options:
    -d <directory>   Directory to download repositories to: defaults to current
                     directory
    -g               Generate local.repo template in download directory
    -h               Print usage and exit
    -l <file>        File to write log to: defaults to none
    -v               Enable verbose logs and output
    -V               Print version and exit
```

### Examples

Sync all currently enabled repos to `/tmp/repos`

```
ezreposync -d /tmp/repos
```

Sync repos `base` and `extras` to the current working directory, and write a verbose log to `/var/log/ezreposync.log`

```
ezreposync -v -l /var/log/ezreposync.log base extras
```

Sync repos `base` and `extras` to `/tmp/repos`, and generate a template .repo file at `/tmp/repos/local.repo`

```
ezreposync -d /tmp/repos -g base extras
```
