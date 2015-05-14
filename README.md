Repos
=====

This role installs repositories and signing keys for them on your server.

Supported OSes
--------------

name     | tagname   | notes
---------|-----------|---------------------------------------------------------------------------------------
CentOS 6 | `centos6` | Repositories are disabled by default, make sure to use `enablerepo=` in your yum calls
CentOS 7 | `centos7` | Ditto CentOS 6

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
      # this will install the officials mongodb and epel repos
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
    # when you have custom repos you can use this syntax to retrieve the repo online
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
[`elasticsearch`](https://www.elastic.co/products/elasticsearch)              | `elasticsearch-1.5`
[`endpoint`](https://packages.endpoint.com/)                                  | `endpoint`
[`epel`](https://fedoraproject.org/wiki/EPEL)                                 | `epel`
[`epel-testing`](https://fedoraproject.org/wiki/EPEL/testing)                 | `epel-testing`
[`epel-yum-rawhide`](https://repos.fedorapeople.org/repos/james/yum-rawhide/) | `epel-yum-rawhide`
[`hortonworks`](http://hortonworks.com/)                                      | `ambari-1x` `HDP-1.3.0.0` `HDP-UTILS-1.1.0.15`
[`ius`](https://iuscommunity.org/pages/About.html)                            | `ius` `ius-testing` `ius-dev` `ius-archive`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`remi`](http://rpms.famillecollet.com/)                                      | `remi` `remi-php55` `remi-php56` `remi-test`
[`rpmforge`](http://repoforge.org/)                                           | `rpmforge` `rpmforge-extra` `rpmforge-testing`

_nb:_ `epel`, `ius` and `remi` also provides the `debuginfo` and `source` variants of their repos.

### CentOS 7

Some of those repositories point to CentOS 6 repos due to the lack of a CentOS 7 version, they will be updated as they
become available.

name                                                                          | provides
------------------------------------------------------------------------------|-----------------------------------------------
[`couchbase`](http://www.couchbase.com/)                                      | `couchbase`
[`elasticsearch`](https://www.elastic.co/products/elasticsearch)              | `elasticsearch-1.5`
[`endpoint`](https://packages.endpoint.com/)                                  | `endpoint`
[`epel`](https://fedoraproject.org/wiki/EPEL)                                 | `epel`
[`epel-testing`](https://fedoraproject.org/wiki/EPEL/testing)                 | `epel-testing`
[`epel-yum-rawhide`](https://repos.fedorapeople.org/repos/james/yum-rawhide/) | `epel-yum-rawhide`
[`hortonworks`](http://hortonworks.com/)                                      | `ambari-1x` `HDP-1.3.0.0` `HDP-UTILS-1.1.0.15`
[`ius`](https://iuscommunity.org/pages/About.html)                            | `ius` `ius-testing` `ius-dev` `ius-archive`
[`jenkins`](http://jenkins-ci.org/)                                           | `jenkins`
[`mongodb`](http://mongodb.org/)                                              | `mongodb`
[`nginx`](http://nginx.org/)                                                  | `nginx`
[`remi`](http://rpms.famillecollet.com/)                                      | `remi` `remi-php55` `remi-php56` `remi-test`
[`rpmforge`](http://repoforge.org/)                                           | `rpmforge` `rpmforge-extra` `rpmforge-testing`

_nb:_ `epel`, `ius` and `remi` also provides the `debuginfo` and `source` variants of their repos.

