Repo
====

This role installs repositories and signing keys for them on your server.

Supported OSes
--------------

name     | tagname   | notes
---------|-----------|---------------------------------------------------------------------------------------
CentOS 6 | `centos6` | Repositories are disabled by default, make sure to use `enablerepo=` in your yum calls
CentOS 7 | `centos7` | Ditto CentOS 6

Usage
-----

In your role's meta, add a dependency to this role using the syntax descibed below.

### Dependency configuration

```yaml
# my_role/meta/main.yml
dependencies:
  - role: repo
    # repositories are repositories officially supported by the role
    repositories:
      # this will install the officials mongodb and epel repos
      centos6:
        - epel
        - mongodb
      # but only the mongodb repo when using centos7
      centos7:
        - mongodb
    # when you have custom repos you can use this syntax to retrieve the repo online
    # see below for more details
    remote_repositories:
      centos6:
        - wizcorp
      centos7:
        - wizcorp
```

Supported Repositories
----------------------

### centos6

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`couchbase`](http://www.couchbase.com/)                                      | `couchbase`
[`endpoint`](https://packages.endpoint.com/)                                  | `endpoint`
[`epel`](https://fedoraproject.org/wiki/EPEL)                                 | `epel` `epel-testing`
[`epel-yum-rawhide`](https://repos.fedorapeople.org/repos/james/yum-rawhide/) | `epel-yum-rawhide`
[`hortonworks`](http://hortonworks.com/)                                      | `ambari-1x` `HDP-1.3.0.0` `HDP-UTILS-1.1.0.15`
[`ius`](https://iuscommunity.org/pages/About.html)                            | `ius` `ius-testing` `ius-dev` `ius-archive`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`remi`](http://rpms.famillecollet.com/)                                      | `remi` `remi-php55` `remi-php56` `remi-test`
[`rpmforge`](http://repoforge.org/)                                           | `rpmforge` `rpmforge-extra` `rpmforge-testing`

_nb:_ `epel`, `ius` and `remi` also providers `debuginfo` and `source` variants of their repos

### centos7

Some of those repositories point to CentOS 6 repos due to the lack of a CentOS 7 version, they will be updated as they
become available.

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`couchbase`](http://www.couchbase.com/)                                      | `couchbase`
[`endpoint`](https://packages.endpoint.com/)                                  | `endpoint`
[`epel`](https://fedoraproject.org/wiki/EPEL)                                 | `epel` `epel-testing`
[`epel-yum-rawhide`](https://repos.fedorapeople.org/repos/james/yum-rawhide/) | `epel-yum-rawhide`
[`hortonworks`](http://hortonworks.com/)                                      | `ambari-1x` `HDP-1.3.0.0` `HDP-UTILS-1.1.0.15`
[`ius`](https://iuscommunity.org/pages/About.html)                            | `ius` `ius-testing` `ius-dev` `ius-archive`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`remi`](http://rpms.famillecollet.com/)                                      | `remi` `remi-php55` `remi-php56` `remi-test`
[`rpmforge`](http://repoforge.org/)                                           | `rpmforge` `rpmforge-extra` `rpmforge-testing`

_nb:_ `epel`, `ius` and `remi` also providers `debuginfo` and `source` variants of their repos

Remote Repositories
-------------------

If a repository is not available, or if you want to use a private repository, then you can use remote repositories to
provide an extra data source for repository files. Remote repositories do not support installing GPG keys so they should
use either url keys (`gpgkey=http://myprivaterepo/mykey.gpg`) or disable gpg checks (not recommended).

### Configuration

You will need to set a global variable (for example in `group_vars/all`) called `remote_repositories_url` that contains
the URL to the base of your repository.

Your online repository should follow the following file organization:

```
├── centos6
│   ├── custom.repo
│   └── wizcorp.repo
└── centos7
    └── wizcorp.repo
```

### Example

`remote_repositories_url` is set to `http://myord.tld/repos` and my dependency file looks like this:

```yaml
dependencies:
  - role: repo
    remote_repositories:
      centos6:
        - myorg
```

Then when installing the repository on CentOS 6 it will fetch the repository file from `http://myord.tld/repos/centos6/myorg.repo`.

Possible future enhancements
----------------------------

* Support for more than one remote repository
* Architecture in the repository file (might be necessary for some distro)
* Debian and Ubuntu support