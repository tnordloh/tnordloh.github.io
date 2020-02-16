---
layout: post
title:  "running dangerous scripts"
date:   2019-04-28 17:00:00
categories: System Administration
---

In this post, I'm going to describe the mentality for running manual build scripts
where there's a lot riding on the outcome.  Maybe it's a build script that can only
be run in production, and has to be run perfectly, on the first shot.  Or maybe
there's high visibility, where any errors during the running of the script will
be embarrassing, in one way or another. It's possible that the script needs to be
run because an important application or website is down, creating pressure to work
more quickly than you want to.

Ideally, your environment isn't fragile in this way, and you can build toward
removing these kinds of system vulnerabilities.  Over the last 20 years, I've
seen that, by far, the most likely source of damage to a system, will be a 
person, with good intentions, accidentally damaging the system. Because of this,
I'm a big fan of automated builds.  But reality interferes with this.  It's very
easy to do tasks manually, and it's easy, over time, to build simple manual
tasks into byzantine, dangerous, complex tasks, one day, and one change at a time.

Also, it's hard to get buy-in on fixing these issues.  So, think about what the right action to take would be, if something goes wrong while the script runs.  For this, it's good to have team members weigh in.  This serves two purposes.  Talking
about the dangerous aspects of a long, complicated script, and explicitly addressing
how to handle those scripts failing, makes sure your team knows what the risks are,
and the work it will take to fix any issues.  And it highlights the broken process.
Sometimes, complaining about scripts doesn't make anyone buy in on why it's super
important to get away from using them.  Really examining the danger they represent,
to the reputation of your team, and to the environment, through the lens of "what
is the best way to react if this goes sideways, in these ways?" can help your team to
prioritize removal of these pain points.  Here are some possible scenarios to think through:

* If a script starts generating errors partway through.
* If you just added did a copy+paste of 50 lines of a script, made 20 edits, start the script, then realize you missed an edit.
* If you started the script in production, when you should have run it in dev.

There are two choices in these scenarios.  Hit the `ctrl+c`, or let it finish.  It can be helpful to know the best response beforehand.  If the script is modifying data, without any sort of rollback capability, it might be better to let it finish, rather than have partial conversion.

### Handling fearfulness

Finding a good mindset before running a script like this is important. Taking that breath beforehand can help you to think through whether you're totally prepared to run it, whether all the edits you made are correct, whether you're logged in to the right server.  There are pressures to move fast, that need to be managed. Overcoming this, so you can bring your whole mind online, to really examine what you're doing, can only help.

### Handling (over)confidence

It's possibly even more likely to be really sure that everything will work perfectly.  Typically, we've earn that confidence, if the script has always run perfectly in the past. Take a moment to make sure you're logged in to the right system, to think through who the script will affect, and how you'd recover from the script aborting. 