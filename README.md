# singularity_example_3

Branch|[![Travis CI logo](pics/TravisCI.png)](https://travis-ci.org)
---|---
`master`|[![Build Status](https://travis-ci.org/richelbilderbeek/singularity_example_3.svg?branch=master)](https://travis-ci.org/richelbilderbeek/singularity_example_3)

Singularity example 3: install `cowsay`.

This example is very similar to example 1, except that I have
struggled myself to get to the -different- result.

### Problem with image

At the top of the `def` file, this works fine:

```
BootStrap: library
From: ubuntu:16.04
```

My own uploaded image, however ...

```
BootStrap: library
From: richelbilderbeek/default/ubuntu_disco:ubuntu 
```

gives this error:

```
richel@sonic:~/GitHubs/singularity_example_3$ sudo singularity build lolcow.sif lolcow.def 
INFO:    Starting build...
INFO:    Running post scriptlet
+ apt-get -y update
Hit:1 http://us.archive.ubuntu.com/ubuntu disco InRelease
Reading package lists... Done
+ apt-get -y install fortune cowsay lolcat
Reading package lists... Done
Building dependency tree       
Reading state information... Done
E: Unable to locate package fortune
E: Unable to locate package cowsay
E: Unable to locate package lolcat
FATAL:   post proc: exit status 100
FATAL:   While performing build: while running engine: exit status 255
```

I guess my image is ?read-only?

## Error that happens once

```
INFO:    Adding labels
INFO:    Adding environment to container
INFO:    Adding runscript
INFO:    Creating SIF file...
INFO:    Build complete: ubuntu_cowsay.sif
richel@sonic:~/GitHubs/singularity_example_3$ ./ubuntu_cowsay.sif 
FATAL:   container creation failed: mount /proc/self/fd/3->/usr/local/var/singularity/mnt/session/rootfs error: can't mount image /proc/self/fd/3: failed to find loop device: could not attach image file to loop device: Failed to set loop flags on loop device: resource temporarily unavailable
```

Just run it again:

```
richel@sonic:~/GitHubs/singularity_example_3$ ./ubuntu_cowsay.sif 
 _______________
< cowsay works! >
 ---------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```
