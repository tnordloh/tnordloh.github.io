---
layout: post
title:  "working with long bash scripts"
date:   2019-04-27 11:00:00
categories: System Administration
---

Like Vi, Bash is the lowest common denominator on Unix/Linux 
systems.  This means that the basic building blocks of any infrastructure deploy
tends to be written in bash. Also, as infrastructure grows, these bash scripts tend to grow,
sometimes into messy balls of mixed up commands. Because they are harder to test,
they can get to the point where they are difficult to understand, and breaking
them down seems too daunting to even think about.  Over time, maybe entire sections
are copied and pasted, and it might reach the point where they simply can't be modified,
without threatening a complicated enterprise server build.

To lay the ground work for breaking up larger bash scripts, I'll describe
some simple ways to add flow control in Bash.

### overriding a failed command

When Jenkins, or other build tools, runs a series of Bash commands, the default
behavior is to abort, if any command exits with an error. But sometimes an
error is ok.  For example, if you need to stop, then start a docker instance,
then the very first time the script runs, or if the docker instance ever dies,
then the `docker stop` command will fail.  Using the bash (`||`) and `true`
command will do the trick to bypass this error, and ensure that Jenkins
continues to run through all of its commands:

```
docker stop my_amazing_website || true
docker start my_amazing_website
```

You don't need to understand Docker, or Jenkins, to understand this sequence.  The idea is
that by appending `|| true` to a command, you can ensure that, no matter what the command
is doing, it will return as a success.  This helps to make sure, if a command is changing
the status of something, and that status has already been changed, the command itself won't
generate an error.

### Respecting a failed command

When running a script manually, the Jenkins introspection which will stop a
script when an individual command won't prevent a script from continuing past
an error.  Using Bash's `&&` operator will ensure that, if one command in a
series of commands that have dependencies on each other, the execution of these
commands will stop when the first one returns a non-zero value.

```
build_my_amazing_website && run deploy_my_amazing_website
```

### What failed again?

That's cool and all, but let's add one more command to that chain, to make the failure more informative.
The command is getting a little long too, so I'm adding the `\` operator, which tells bash that a command
is being split across multiple lines.

```
build_my_amazing_website && \
  run deploy_my_amazing_website || \
  echo "The 'build_my_amazing_website' command failed!"
```

### Stop, there was a failure!

if the command is crucial to the rest of a script, maybe we don't want to keep
going. I'll group the `echo` command with `exit`, to demonstrate linking two
commands together.

```
build_my_amazing_website && \
  run deploy_my_amazing_website || \
  (
    echo "The 'build_my_amazing_website' command failed!"
    exit(1)
  )
```

These are some of the basic building blocks to help make Bash scripts more likely to stop properly,
if there is some error during the build process, and to make sure they are more likely to respond
predictably when they encounter an error, using flow control. To really understand what a bash script
is doing though, it can be executed in verbose mode by explicitly calling bash, and passing the `-x` parameter. This will print each line of the script, inlined with the output of that line.  An example
call of that script looks like `bash -x my_amazing_deploy_script`.
