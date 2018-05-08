---
title: "Use jupyter on remote server"
author: Zhang Keke
date: 2018-05-08
categories:
  - tools
tags:
  - jupyter
---

If you want to use jupyter on remote server, this blog might be useful.

Step1:
Run jupyter without browser on  remote server:

``` sh
jupyter notebook --no-browser --port=8888
```

Step2:
Bind local port to remote server:

``` sh
ssh -N -f -L localhost:8888:ip:8888 user@ip
```
Step3:
Open browser on you local machine and direct to `localhost:8888` 

To Stop Local Process:

``` sh
ps aux|grep jupyter

kill pid
```