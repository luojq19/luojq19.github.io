---
title: 'Tricks and Utilities'
date: 2023-02-13
permalink: /posts/2023/07/tricks-and-utilities/
tags:
  - utility
---

### Free Proxy Website
[https://proxyscrape.com/free-proxy-list](https://proxyscrape.com/free-proxy-list)

Usage:
```
proxy = random.choice(proxies)
response = requests.get(url=pdb_url, proxies=proxy)
```

### Slow reaction of commands in a certain directory
Probably due to too many changes for git, run `git status` to refresh the index.
