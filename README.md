forward2docker
==============

Easily build and start a docker container and set up port forwardings to it, using boot2docker

This tiny script does below at once:

- Sets up [boot2docker](https://github.com/steeve/boot2docker)
- Builds images from given Dockerfiles
- Runs containers on the images
- Sets up port forwardings to the containers' exposed ports
- When done, cleans up the images/containers

Usage
-----

```
forward2docker <DOCKERFILE> <DOCKERFILE>...
```

Example
-------

```
% curl -LO https://raw.github.com/motemen/forward2docker/master/forward2docker
% chmod +x forward2docker
% ./forward2docker path/to/Dockerfile ...
```

For example, with [this dockerfile](https://gist.github.com/motemen/8954007):

```
% ./forward2docker Dockerfile.2
[2014-02-12 20:42:35] boot2docker-vm is running.
[forward2docker] boot2docker initialized.
[forward2docker] Building image...
Uploading context 10.24 kB
Uploading context 
Step 0 : FROM ubuntu
 ---> 9cd978db300e
Step 1 : RUN apt-get update
 ---> Using cache
 ---> 81dadb7bc747
Step 2 : RUN apt-get install -y python
 ---> Using cache
 ---> 19b0f0848fa7
Step 3 : RUN apt-get clean
 ---> Using cache
 ---> d573b03e60f1
Step 4 : EXPOSE 8000
 ---> Running in 4f2fc543927a
 ---> 6aa9368a2d02
Step 5 : CMD ["python", "-m", "SimpleHTTPServer"]
 ---> Running in 6f8930b1a399
 ---> c39a3eb6d327
Successfully built c39a3eb6d327
[forward2docker] Starting container...
[forward2docker] 3636376b2a6ebac6641034bc3272bf3f134729ceeb312a052db88287bbddfaf4: listen on port 18000
[forward2docker] Starting port forwarding...
Warning: Permanently added '[localhost]:2022' (RSA) to the list of known hosts.
docker@localhost's password: 
Success!
[container log comes here]
```

After hitting `Ctrl-C`, the containers are removed:

```
^CKilled by signal 2.
[forward2docker] Cleaning up container...
```
