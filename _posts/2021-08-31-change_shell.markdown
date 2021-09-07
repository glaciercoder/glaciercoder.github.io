---
layout: default
title:  "How to change shell for a certain user on Linux"
date:   2021-08-31 15:26:39 +0800
categories: Linux
---

# Background

Recently I need to run my code on a server, but default bash is hard to use



# Contents

Versions of shell are stored in `\etc\shells`

- A user can change their own shell to any thing: which, however must be listed in the **/etc/shells** file.
- Only root can run a shell not listed in **/etc/shells** file.
- If an account has a restricted login shell, then only root can change that user’s shell.



Check `/etc/passwd` can find account information for each user.

```shell
# change the shell in /etc/passwd to bash just like modify the /etc/passwd
usermod --shell /bin/bash user
# or
chsh --shell /bin/sh user
chsh -s /bin/sh user
```
[More on login shell and non-login shell](https://tecadmin.net/difference-between-login-and-non-login-shell/)

 ==Attention: Change login-in shell must restart to take effect==









