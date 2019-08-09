# singularity_example_3

Branch|[![Travis CI logo](pics/TravisCI.png)](https://travis-ci.org)
---|---
`master`|[![Build Status](https://travis-ci.org/richelbilderbeek/singularity_example_3.svg?branch=master)](https://travis-ci.org/richelbilderbeek/singularity_example_3)

Singularity example 3: install cowsay

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