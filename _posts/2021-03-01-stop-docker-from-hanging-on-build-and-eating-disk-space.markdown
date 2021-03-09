---
layout: post
title: "Stop Docker from Hanging on Build and Eating Disk Space"
---

I was recently building a `Dockerfile` which would hang on `docker build` at
this point in the file
```
RUN bash -c 'useradd ${USER_NAME} -m -u ${USER_UID} -g ${USER_GID} -d ${USER_HOME}'
```
Docker would then eat up all the storage I had allocated to it, and become
unusable. The only way out of this was to prune everything, losing my
containers, images and volumes then re-build. All this would take around
30 minutes.

## What's going on?

It turns out that when using `useradd` in Golang apps, Golang creates huge
sparse files, tanking any disk space whilst doing so. You can see various bug
reports raised in a number of different projects:

* [Podman Build Hangs](https://github.com/containers/podman/issues/1808)

* [Moby Build Hangs](https://github.com/moby/moby/issues/5419)

* [Useradd Hangs with Large UID](https://forums.docker.com/t/run-adduser-seems-to-hang-with-large-uid/27371)

## What's the fix?

`useradd` has a `-l, --no-log-init` option which prevents the creation of the
offending sparse files, and Docker will happily continue as intented. The
hanging line from above now becomes
```
RUN bash -c 'useradd -l ${USER_NAME} -m -u ${USER_UID} -g ${USER_GID} -d ${USER_HOME}'
```
This is supposedly out of Docker's hands, but it'd be nice if it was handled
a little more gracefully.
