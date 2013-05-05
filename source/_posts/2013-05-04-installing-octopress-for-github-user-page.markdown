---
layout: post
title: "installing octopress for github user page"
date: 2013-05-04 18:32
comments: true
categories: [octopress, rbenv] 
---

Here's the list of problems I ran into while setting up octopress on my github user page, and how I fixed them. Silly, but hey! Someone else might have encountered the same issues, so why not share them?

##Issue: ruby is not up-to-date.
- Fix: Get the latest that's compatible with octopress via rbenv. Install rbenv via Homebrew.
```
brew update
brew install rbenv
rbenv install 1.9.3-p0 
```

##Issue: rbenv says there's no such command 'install'
```
rbenv install 1.9.3-p0
rbenv: no such command `install'
```
- Cause: You need ruby-build in order to run "rbenv install" command.
- Fix: Run "brew ruby-build", then "rbenv install 1.9.3-p0". See [here](https://github.com/sstephenson/ruby-build#readme) for instructions. Then run
```
git clone https://github.com/sstephenson/ruby-build.git ~/.rbenv/plugins/ruby-build
```
- Now what?: Now that ruby-build is installed, back to setting ruby version.

##Issue: "rbenv install 1.9.3-p0" spits error "configure: error: C compiler cannot create executables"
```
$ rbenv install 1.9.3-p0
Downloading yaml-0.1.4.tar.gz...
-> http://dqw8nmjcqpjn7.cloudfront.net/36c852831d02cf90508c29852361d01b
Installing yaml-0.1.4...

BUILD FAILED

Inspect or clean up the working tree at /var/folders/m4/xdbt7xw53pj3wldwfrxj5fm80000gn/T/ruby-build.20130501225910.3936
Results logged to /var/folders/m4/xdbt7xw53pj3wldwfrxj5fm80000gn/T/ruby-build.20130501225910.3936.log

Last 10 log lines:
checking for gawk... no
checking for mawk... no
checking for nawk... no
checking for awk... awk
checking whether make sets $(MAKE)... no
checking for gcc... /usr/local/bin/gcc-4.2
checking whether the C compiler works... no
configure: error: in `/var/folders/m4/xdbt7xw53pj3wldwfrxj5fm80000gn/T/ruby-build.20130501225910.3936/yaml-0.1.4':
configure: error: C compiler cannot create executables
See `config.log' for more details
```
- Cause: I didn't have xcode installed on this machine. Duh!!
- Fix: Install xcode.
- Now what?: Run "rbenv install 1.9.3-p0" again, and make sure you get no errors. Then run
```
rbenv rehash
ruby --version
```

##Issue: "ruby --version" still isn't updated
```
$ ruby --version
ruby 1.8.7 (2012-02-08 patchlevel 358) [universal-darwin11.0]
```
- Cause: It's using the system default version of ruby (which is 1.8.7). 
```
$ rbenv global
system
```
- Fix: Set the system default as 1.9.3-p0. Now do "rbenv global" and see what it's set to.
```
$ rbenv global 1.9.3-p0
$ rbenv global
1.9.3-p0
```




