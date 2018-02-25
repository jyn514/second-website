---
layout:	post
title:	"Password Managers"
date:	2018-02-24 22:17:46 -0500
excerpt: What a password manager is and how to use one
---

# Intro

On the web today, there many different services we use.
We use email, Facebook, GitHub, Google, Twitter, dozens of various services.
Each of these require their own username and password.

We're told, of course, to use a different password for each account.
Very few of us, however, actually do so.
How are we supposed to remember a dozen random passwords, each different?
Traditionally, we use the same password for each, perhaps with slight differences.
This makes it very easy for hackers to [get into your accounts][xkcd resuse].

There are very few common remedies for this -
there's ways to [check if you've been hacked](https://haveibeenpwned.com/)
and [multi-factor auth](https://en.wikipedia.org/wiki/Multi-factor_authentication),
but most peoples' response is to either write sticky notes of passwords
or ignore the problem altogether.

This is wrong.

What you should be using is a [password manager][manager].

## Password Managers
A password manager is an easy way to keep track of passwords.
It can be anything from an [encrypted Excel Spreadsheet][encrypt spreadsheet]
to [your browser's builtin manager][ddg browser passwords].
It takes one 'master password', and in return keeps track of everything else for you.
There's no need to remember multiple passwords,
it's easy to meet any complexity requirement,
and it doesn't matter how often you're required to change your passwords.

## What to use
I recommend [Keepass](https://keepass.info). It
- encrypts your databases with [state of the art encryption][keepass aes]
- organizes your passwords [by groups](https://keepass.info/features.html#lnkgroups)
- stores usernames, URLs, and
[arbitrary data](https://keepass.info/features.html#lnktimes )
- randomly [generates passwords](https://keepass.info/help/base/pwgenerator.html)
- is [open source][source zip]
- is fully interoperable with many [other programs][wiki derivatives]
- has [many other features](https://keepass.info/features.html)

Once you start using a password manager, you can start using things like
`W(xv|u7N''fAs,{t|J` for all your accounts.

## Appendix
- If you're not on Windows, or just want more features, check out [Keepassxc][xc]
(Keepass Cross-Platform Community Edition). It supports global autotype and
[timed one-time passwords][totp], a.k.a. two-factor auth.
- For mobile, look into [Keepass2Android](https://github.com/PhilippC/keepass2android)
or [MiniKeePass](https://itunes.apple.com/us/app/minikeepass/id451661808?mt=8)
(iPhone only)
- I've written a [presentation on secure passwords][password presentation]

[xkcd resuse]: https://xkcd.com/792/
[manager]: https://en.wikipedia.org/wiki/Password_manager
[encrypt spreadsheet]: https://support.office.com/en-us/article/Protect-an-Excel-file-7359d4ae-7213-4ac2-b058-f75e9311b599
[ddg browser passwords]: https://duckduckgo.com/?q=browser+manage+password+saving
[keepass aes]: https://keepass.info/help/base/security.html
[source zip]: https://keepass.info/download.html
[wiki derivatives]: https://en.wikipedia.org/wiki/KeePass#Unofficial_KeePass_derivatives
[xc]: https://keepassxc.org/
[totp]: https://en.wikipedia.org/wiki/Time-based_One-time_Password_Algorithm
[password presentation]: https://drive.google.com/open?id=15u4uXxC5K7v2Llsu8L4JVDcFNjyavW4pKBJ2GW5YV5M
