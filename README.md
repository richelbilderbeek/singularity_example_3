# singularity_example_3

Singularity example 3: install NCBI tools


```
richel@sonic:~/GitHubs/singularity_example_3$ ./script 
[sudo] password for richel: 
Using container recipe deffile: singularity_example_3.txt
Sanitizing environment
Adding base Singularity environment to container
Progress |===================================| 100.0% 
Exporting contents of shub://pavel-demin/singularity-ubuntu:1804 to /tmp/.singularity-build.TXb1Me
Running post scriptlet
+ apt-get update
Get:1 http://security.ubuntu.com/ubuntu bionic-security InRelease [88.7 kB]
Get:2 http://archive.ubuntu.com/ubuntu bionic InRelease [242 kB]                         
Get:3 http://security.ubuntu.com/ubuntu bionic-security/universe Sources [191 kB]        
Get:4 http://archive.ubuntu.com/ubuntu bionic-updates InRelease [88.7 kB]      
Get:5 http://archive.ubuntu.com/ubuntu bionic-backports InRelease [74.6 kB]                
Get:6 http://archive.ubuntu.com/ubuntu bionic/universe Sources [11.5 MB]                       
Get:7 http://security.ubuntu.com/ubuntu bionic-security/restricted amd64 Packages [5436 B]             
Get:8 http://security.ubuntu.com/ubuntu bionic-security/multiverse amd64 Packages [4172 B]
Get:9 http://security.ubuntu.com/ubuntu bionic-security/universe amd64 Packages [727 kB]   
Get:10 http://security.ubuntu.com/ubuntu bionic-security/main amd64 Packages [591 kB]      
Get:11 http://archive.ubuntu.com/ubuntu bionic/main amd64 Packages [1344 kB]                                     
Get:12 http://archive.ubuntu.com/ubuntu bionic/universe amd64 Packages [11.3 MB]                                 
Get:13 http://archive.ubuntu.com/ubuntu bionic/restricted amd64 Packages [13.5 kB]                               
Get:14 http://archive.ubuntu.com/ubuntu bionic/multiverse amd64 Packages [186 kB]                                
Get:15 http://archive.ubuntu.com/ubuntu bionic-updates/universe Sources [332 kB]                                 
Get:16 http://archive.ubuntu.com/ubuntu bionic-updates/restricted amd64 Packages [10.8 kB]                       
Get:17 http://archive.ubuntu.com/ubuntu bionic-updates/universe amd64 Packages [1247 kB]                         
Get:18 http://archive.ubuntu.com/ubuntu bionic-updates/main amd64 Packages [901 kB]                              
Get:19 http://archive.ubuntu.com/ubuntu bionic-updates/multiverse amd64 Packages [7235 B]                        
Get:20 http://archive.ubuntu.com/ubuntu bionic-backports/main amd64 Packages [2496 B]                            
Get:21 http://archive.ubuntu.com/ubuntu bionic-backports/universe amd64 Packages [3930 B]                        
Fetched 28.9 MB in 19s (1506 kB/s)                                                                               
Reading package lists... Done
+ apt-get -y install cowsay
Reading package lists... Done
Building dependency tree       
Reading state information... Done
The following additional packages will be installed:
  libtext-charwidth-perl
Suggested packages:
  filters cowsay-off
The following NEW packages will be installed:
  cowsay libtext-charwidth-perl
0 upgraded, 2 newly installed, 0 to remove and 222 not upgraded.
Need to get 27.2 kB of archives.
After this operation, 128 kB of additional disk space will be used.
Get:1 http://archive.ubuntu.com/ubuntu bionic/main amd64 libtext-charwidth-perl amd64 0.04-7.1 [9492 B]
Get:2 http://archive.ubuntu.com/ubuntu bionic/universe amd64 cowsay all 3.03+dfsg2-4 [17.7 kB]
Fetched 27.2 kB in 0s (234 kB/s)
debconf: delaying package configuration, since apt-utils is not installed
Selecting previously unselected package libtext-charwidth-perl.
(Reading database ... 47433 files and directories currently installed.)
Preparing to unpack .../libtext-charwidth-perl_0.04-7.1_amd64.deb ...
Unpacking libtext-charwidth-perl (0.04-7.1) ...
Selecting previously unselected package cowsay.
Preparing to unpack .../cowsay_3.03+dfsg2-4_all.deb ...
Unpacking cowsay (3.03+dfsg2-4) ...
Setting up libtext-charwidth-perl (0.04-7.1) ...
Setting up cowsay (3.03+dfsg2-4) ...
+ echo The post section is where you can install, and configure your container.
The post section is where you can install, and configure your container.
Found an existing definition file
Adding a bootstrap_history directory
Finalizing Singularity container
Calculating final size for metadata...
Skipping checks
Building Singularity image...
Singularity container built: ubuntu_cowsay.simg
Cleaning up...
```

Running cowsay:

```
richel@sonic:~/GitHubs/singularity_example_3$ singularity shell ubuntu_cowsay.simg 
Singularity: Invoking an interactive shell within container...

Singularity ubuntu_cowsay.simg:~/GitHubs/singularity_example_3> cowsay
bash: cowsay: command not found
Singularity ubuntu_cowsay.simg:~/GitHubs/singularity_example_3> apt search cowsay
Sorting... Done
Full Text Search... Done
cowsay/bionic,now 3.03+dfsg2-4 all [installed]
  configurable talking cow

cowsay-off/bionic 3.03+dfsg2-4 all
  configurable talking cow (offensive cows)

xcowsay/bionic 1.4-1 amd64
  Graphical configurable talking cow
```

Weird, it is installed, but it cannot be run ..?

From [here](https://github.com/richelbilderbeek/travis_cowsay/blob/master/.travis.yml)
I learn I first need to set the PATH:

```
richel@sonic:~/GitHubs/singularity_example_3$ sudo singularity shell ubuntu_cowsay.simg 
Singularity: Invoking an interactive shell within container...

Singularity ubuntu_cowsay.simg:~> export PATH=/usr/bin:/bin:/usr/games
Singularity ubuntu_cowsay.simg:~> cowsay hello 
perl: warning: Setting locale failed.
perl: warning: Please check that your locale settings:
	LANGUAGE = "en_US",
	LC_ALL = (unset),
	LANG = "en_US.UTF-8"
    are supported and installed on your system.
perl: warning: Falling back to the standard locale ("C").
 _______
< hello >
 -------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```