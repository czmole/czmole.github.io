---
layout: post
title: Composer got killed while updating
published: true
---
I was running a small [Digital Ocean](https://m.do.co/c/dc91876a47e0) server (512 MB RAM) for a side project and got to the problem that I could not use composer update after pushing changes related to the use of new packages.

Fortunately, I got into this that saved the day. I am sharing it, maybe it will save yours.

Depending on how many dependencies your project has, you may simply need more memory on your system. I’ve had to increase my virtual machine’s memory to at least 768mb in order to get `composer update` to work in some situations.

However, if you’re doing this on a live server, you shouldn’t be using `composer update` at all.

What you should do is:

- Run `composer update` in a local environment (either your physical machine, or a development virtual machine)
- Upload or `git push` the composer.lock file
- Run `composer install` on the live server


`composer install` will then read from the .lock file, fetching the exact same versions every time rather than finding the latest versions of every package. This makes your app less likely to break, and composer uses less memory.

Read more here: [https://getcomposer.org/doc/01-basic-usage.md#composer-lock-the-lock-file](https://getcomposer.org/doc/01-basic-usage.md#composer-lock-the-lock-file)
