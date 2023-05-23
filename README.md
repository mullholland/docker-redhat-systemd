Docker RedHat Systemd
=====================

This Dockerfile can build containers capable to use systemd.

Branches
--------

This repository has multiple tags that relate to RedHat versions.

|RedHat Version|Docker image tag|
|------------------|-------------------|
|8                 |8                  |
|9 (latest)        |9, latest          |

Manually starting
-----------------

```shell
docker run \
  --tty \
  --privileged \
  --volume /sys/fs/cgroup:/sys/fs/cgroup:ro \
  mullholland/docker-redhat-systemd
```
