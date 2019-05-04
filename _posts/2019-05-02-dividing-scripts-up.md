---
layout: post
title:  "dividing a script into files"
date:   2019-05-02 16:39:00
categories: System Administration
---

Here, I'm going to describe dividing a script into chunks.  This technique isn't
something I invented; rather, it mirrors a technique for starting up a Unix OS.
I'll start with a simple approach, then describe how to flesh it out, to allow
build scripts to become repeatable.

So, let's take an example of an infrastructure build process, which first builds
out firewall rules, then builds a database server, then a web server.  
The infrastructure build will fail if something goes wrong early in the process, such
as a failure to correctly configure the firewall.

In addition, there are some environment variables that need to be set, such as the 
firewall server's name, and the environment, such as 'qa' (quality analysis) or 'production'.

So, here's how we could do this, if we mirror Unix's rc (run command) methodology.
For each section, we can divide the script into chunks, and number the files by the
order they should run, similar to this:

```
010_configure_firewall.sh
020_build_database_server.sh
030_build_application_server.sh
```

we also need one more 'wrapper' script that will run the scripts.  By including
three digit numbers at the beginning of each script name, we can then use a 
controller script that loads our environment variables, and utilizes  bash's
`for` loop to run them in that order, and define a 'failed' action that's 
consistent and easy-to-read for each script:

``` bash
export my_var1='one'
export my_var2='two'
#  and so on
for file in `ls build_scripts` ; do
  ./build_scripts/$file || \
    (
      echo "the $file build script failed!" ; \
      exit 1
    )
done 
```

Finally, we can rearrange the scripts one more time, to help make all of the build
as consistent, repeatable, and reversible as possible, by creating symbolic links
to the relevant files, in a more specific directory layout, that looks something like this:

```
$>tree                                                                                             
.
├── build_scripts
│   ├── application_server.down.sh
│   ├── application_server.up.sh
│   ├── database_server.down.sh
│   ├── database_server.up.sh
│   ├── firewall.down.sh
│   └── firewall.up.sh
├── start_scripts
│   ├── 010.firewall.up.sh -> ./build_scripts/firewall.up.sh
│   ├── 020.database_server.up.sh -> ./build_scripts/database_server.up.sh
│   └── 030.application_server.up.sh -> ./build_scripts/application_server.up.sh
└── stop_scripts
    ├── 010.application_server.down.sh -> build_scripts/application_server.down.sh
    ├── 020.database_server.down.sh -> ./build_scripts/database_server.down.sh
    └── 030.firewall.down.sh -> ./build_scripts/firewall.down.sh
```

Now, a wrapper script that looks like the one above, along with a config file or two,
should make it possible to run things in a predictable way.  Something like this:

``` bash
source ./startup_settings.sh`
for file in `ls ./start_scripts` ; do
  ./start_scripts/$file
done
```

Rebuilding scripts like this doesn't necessarily reduce the overall complexity.
The main purpose is to make it easier to encapsulate portions of a build.  In
the end, the hope is that, by doing this, the move to an automated build system
becomes the natural next step.