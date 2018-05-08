---
title: "Connect server with spawn and expect"
author: Zhang Keke
date: 2018-05-08
categories:
  - tools
tags:
  - ssh
  - spawn
  - server
---

[expect spawn and send](https://www.thegeekstuff.com/2010/10/expect-examples)

``` sh
#!/usr/bin/expect -f

#set timeout 20

set sp YourSudoPassword
set passwd UserPassword

# sudo is not always necessary

spawn sudo ssh user@ip

expect "Password:"
send "$sp\r"

expect "some stuff"
send "$passwd\r"
interact
```

* spawn: run commands
* expect: wait for specify pattern
* send: to send the strings to the process