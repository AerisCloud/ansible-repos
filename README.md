Repos
=====

This role installs repositories and signing keys for them on your server.

Supported OSes
--------------

name         | tagname   | notes
-------------|-----------|---------------------------------------------------------------------------------------
CentOS 6     | `centos6` | Repositories are disabled by default, make sure to use `enablerepo=` in your yum calls
CentOS 7     | `centos7` | Ditto CentOS 6
Amazon Linux | `amazon`  | Ditto CentOS 6
Debian 7     | `wheezy`  | APT Repositories are disabled by default, make sure to use `default_release=wheezy-backports` in your apt calls
Debian 8     | `jessie`  | Ditto Debian 7. Use `default_release=jessie-backports` in your apt calls

Usage
-----

In your role's meta, add a dependency to this role using the syntax described below.

### Dependency configuration

```yaml
# my_role/meta/main.yml
dependencies:
  - role: aeriscloud.repos
    # repositories are repositories officially supported by the role
    repositories:
      # this will install the official mongodb and epel repos
      centos6:
        - epel
        - mongodb
        # by default repos are disabled, but you can enable them using the following syntax
        # also repos of type testing/debuginfo/dev can not be enabled unless the repo file is
        # dedicated to it (ie. epel-testing)
        - name: elasticsearch
          enabled: true
      # but only the mongodb repo when using centos7
      centos7:
        - mongodb
      # This will install wheezy backports and the offical nginx repo
      wheezy:
        - backports
        - nginx
      # support for jessie backports will be available when the jessie backports is available.
      jessie:
        - nginx
    # (CentOS only) when you have custom CentOS repos you can use this syntax to retrieve the repo online
    remote_repositories:
      centos6:
        - http://myorg.tld/myrepo.repo
      centos7:
        - http://myorg.tld/myrepo.repo
```

Supported Repositories
----------------------

### CentOS 6

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`couchbase`](http://www.couchbase.com/)                                      | `couchbase`
[`elasticsearch`](https://www.elastic.co/products/elasticsearch)              | `elasticsearch-2.x`
[`endpoint`](https://packages.endpoint.com/)                                  | `endpoint`
[`epel`](https://fedoraproject.org/wiki/EPEL)                                 | `epel`
[`epel-testing`](https://fedoraproject.org/wiki/EPEL/testing)                 | `epel-testing`
[`epel-yum-rawhide`](https://repos.fedorapeople.org/repos/james/yum-rawhide/) | `epel-yum-rawhide`
[`hortonworks`](http://hortonworks.com/)                                      | `ambari-1x` `HDP-1.3.0.0` `HDP-UTILS-1.1.0.15`
[`ius`](https://iuscommunity.org/pages/About.html)                            | `ius` `ius-testing` `ius-dev` `ius-archive`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mesophere`](https://www.mesosphere.com/)                                    | `mesosphere`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`mysql`](https://www.mysql.fr/products/community/)                           | `mysql56-community` `mysql-connectors-community` `mysql-tools-community` 
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`percona`](https://www.percona.com)                                          | `percona-release-x86_64`
[`postgresql 9.0`](http://yum.postgresql.org/repopackages.php)                | `pgdg90`
[`postgresql 9.1`](http://yum.postgresql.org/repopackages.php)                | `pgdg91`
[`postgresql 9.2`](http://yum.postgresql.org/repopackages.php)                | `pgdg92`
[`postgresql 9.3`](http://yum.postgresql.org/repopackages.php)                | `pgdg93`
[`postgresql 9.4`](http://yum.postgresql.org/repopackages.php)                | `pgdg94`
[`postgresql 9.5`](http://yum.postgresql.org/repopackages.php)                | `pgdg95`
[`remi`](http://rpms.famillecollet.com/)                                      | `remi` `remi-php55` `remi-php56` `remi-php70` `remi-test`
[`rpmforge`](http://repoforge.org/)                                           | `rpmforge` `rpmforge-extra` `rpmforge-testing`
[`mysql`](https://www.mysql.fr/products/community/)                           | `mysql56-community` `mysql-connectors-community` `mysql-tools-community`
[`slc6-devtoolset`](http://linux.web.cern.ch/linux/devtoolset/)               | `gcc-4.8` and other related tools


_nb:_ `epel`, `ius` and `remi` also provides the `debuginfo` and `source` variants of their repos.

### CentOS 7

Some of those repositories point to CentOS 6 repos due to the lack of a CentOS 7 version, they will be updated as they
become available.

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`couchbase`](http://www.couchbase.com/)                                      | `couchbase`
[`elasticsearch`](https://www.elastic.co/products/elasticsearch)              | `elasticsearch-2.x`
[`endpoint`](https://packages.endpoint.com/)                                  | `endpoint`
[`epel`](https://fedoraproject.org/wiki/EPEL)                                 | `epel`
[`epel-testing`](https://fedoraproject.org/wiki/EPEL/testing)                 | `epel-testing`
[`epel-yum-rawhide`](https://repos.fedorapeople.org/repos/james/yum-rawhide/) | `epel-yum-rawhide`
[`hortonworks`](http://hortonworks.com/)                                      | `ambari-1x` `HDP-1.3.0.0` `HDP-UTILS-1.1.0.15`
[`ius`](https://iuscommunity.org/pages/About.html)                            | `ius` `ius-testing` `ius-dev` `ius-archive`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mesophere`](https://www.mesosphere.com/)                                    | `mesosphere`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`mysql`](https://www.mysql.fr/products/community/)                           | `mysql56-community` `mysql-connectors-community` `mysql-tools-community`
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`percona`](https://www.percona.com)                                          | `percona-release-x86_64`
[`postgresql 9.3`](http://yum.postgresql.org/repopackages.php)                | `pgdg93`
[`postgresql 9.4`](http://yum.postgresql.org/repopackages.php)                | `pgdg94`
[`postgresql 9.5`](http://yum.postgresql.org/repopackages.php)                | `pgdg95`
[`remi`](http://rpms.famillecollet.com/)                                      | `remi` `remi-php55` `remi-php56` `remi-php70` `remi-test`
[`rpmforge`](http://repoforge.org/)                                           | `rpmforge` `rpmforge-extra` `rpmforge-testing`


_nb:_ `epel`, `ius` and `remi` also provides the `debuginfo` and `source` variants of their repos.

### Amazon Linux

Actually almost everything can be found up to date on the Amazon repos (both amzn and amzn-preview), only adding the few
softwares that might be missing from it.

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`hortonworks`](http://hortonworks.com/)                                      | `ambari-1x` `HDP-1.3.0.0` `HDP-UTILS-1.1.0.15`

### Debian 7

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`backports`](https://packages.debian.org/wheezy-backports/)                  | `backports`
[`dotdeb`](https://www.dotdeb.org)                                            | `dotdeb`
[`elasticsearch`](https://www.elastic.co/products/elasticsearch)              | `elasticsearch-2.x`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`mysql`](https://www.mysql.fr/products/community/)                           | `mysql56-community`
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`percona`](https://www.percona.com)                                          | `percona`
[`postgresql`](http://www.postgresql.org)                                     | `postgresql`


_nb:_ `deb-src` is not provided. `deb` is only provided.

### Debian 8

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`backports`](https://packages.debian.org/jessie-backports/)                  | `backports`
[`dotdeb`](https://www.dotdeb.org)                                            | `dotdeb`
[`elasticsearch`](https://www.elastic.co/products/elasticsearch)              | `elasticsearch-2.x`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`mysql`](https://www.mysql.fr/products/community/)                           | `mysql56-community`
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`percona`](https://www.percona.com)                                          | `percona`
[`postgresql`](http://www.postgresql.org)                                     | `postgresql`


_nb:_ `deb-src` is not provided. `deb` is only provided.
