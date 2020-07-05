---
title: Azure CLI Login SSLError
author: Suresh Siva
date: 2020-07-03 08:00:00 +0800
categories: [Azure, CLI]
tags: [azure, azure-cli, cli, login, issues, az]
math: true
pin: yes
---

## **Issue**

When logging in to azure through `azure-cli` with `az login` command, you might experience below SSL error blocking the login.

``` ruby

Please ensure you have network connection. Error detail: HTTPSConnectionPool(host='login.microsoftonline.com', port=443): Max retries exceeded with url: /common/oauth2/token (Caused by SSLError(SSLError("bad handshake: Error([('SSL routines', 'ssl3_get_server_certificate', 'certificate verify failed')])")))

```

![SSLError Error]({{ "/assets/img/posts/20200703_az_login_issue.png" | relative_url }})

This error may happen when connecting Azure from devices attached to a proxy.

## **Fix**

Setting up the below environment variable on my Mac terminal has helped me to fix the above issue.

``` shell
export AZURE_CLI_DISABLE_CONNECTION_VERIFICATION=1
```

Hope this helps!!
