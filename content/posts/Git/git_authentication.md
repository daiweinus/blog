---
title: "fatal: Authentication failed for 'https://github.com/yourusername/githubtest.git/' "
Username: your_username
Password: your_token"
date: 2021-11-15T12:02:42+08:00
draft: true
toc: false
images:
  - "totoro.jpeg"
tags: 
  - Git
---

### fatal: Authentication failed for 'https:/githubtest.git/'

这是因为github开启了Two Factor Authentication (2FA）验证，所以当你使用这些 `git clone`, `git fetch`, `git pull` or `git push`命令的时候就会需要输入你的 PAT (Personal Access Token). 

在github settings 打开 Developer settings, 创建PAT, 创建完成后copy 你的PAT 再 使用之前的 git push 命令就可以输入用户名和你的PAT了（注意输入PAT,不是你的github密码）. 请参考 GitHub　[Creating a personal access token](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/creating-a-personal-access-token).

```java
$ git clone https://github.com/username/repo.git
Username: your_username
Password: your_token
```



![Developer settings](https://docs.github.com/assets/images/help/settings/developer-settings.png)

![Personal access tokens](https://docs.github.com/assets/images/help/settings/personal_access_tokens_tab.png)

![Generate new token button](https://docs.github.com/assets/images/help/settings/generate_new_token.png)

![Generate token button](https://docs.github.com/assets/images/help/settings/generate_token.png)

![Newly created token](https://docs.github.com/assets/images/help/settings/personal_access_tokens.png)



