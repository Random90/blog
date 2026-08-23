---
title: "Proving your Android app respects user privacy without source code"
date: 2026-08-23
---

### Living in the slop era

Publishing source code of the app you worked on for months or years might not be the best idea in the age of AI and slop.
What's stopping bots and agents from forking your work and spinning up their own version? Nothing. 
We have to use something different to prove that our app won't send any user data to your server, some cloud or advertising platform. 

On Google play there is a section talking about privacy and how user data is processed. The problem is that this section is just a declaration.
There is no substance behind it, Google is not and can't verify this.  It's just a promise and there is no reason to trust it.
So how to actually prove that the app doesn't send any data in a way anyone can verify?

### Proving privacy-first principle

How a program can share user data with anybody developers wants? Using a some kind of transportation protocol suite, like an Internet. 
You probably can see where I'm going with this:

If the app CANNOT access the internet, it can't exfiltrate any data.

WIP
