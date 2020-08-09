---
title: Linux SSR Setting
published: true
---

This article mainly introduces the **SSR** Internet access method of the Ubuntu series.

### ShadowsocksR GUI Client

Since the VPN of Ubuntu system is mainly Shadowsocks (SS) client, here is introduced with ShadowsocksR (SSR) client **electron-ssr**.

Client address: [electron-ssr-0.2.6.deb](https://github.com/qingshuisiyuan/electron-ssr-backup/releases/download/v0.2.6/electron-ssr-0.2.6.deb) The project was closed in May 2019, and it is feasible and cherished.

Install the following dependencies before installing the client:

```shell
sudo apt-get install libcanberra-gtk-module libcanberra-gtk3-module gconf2 gconf-service libappindicator1
```

<!-- more -->

Optional dependencies (If the software reports an error, please install optional dependencies):

```shell
sudo apt-get install libssl-dev
sudo apt-get install libsodium-dev
```

Start installation

```shell
cd Downloads
sudo dpkg -i electron-ssr-0.2.6.deb
```

Run the software after installation:

```shell
electron-ssr
```

Hot key:

| Global or In-app  | Keyboard Combination                    | Function                |
|:-------------|:---------------------------|:--------------------|
| Global    | Command Or Control+Shift+W | Switch the main window display or not       |
| In-app  | Command Or Control+Shift+B | Switch whether to display the operation menu  |


### Chrome Extension - SwitchyOmega

Add Proxy Servers：

![proxy:](/images/20200329/sendpix0.jpg)

Configure auto switch：


*   Configure Switch Rules

*   Configure Rule List Config：

    *   Rule List Format:   AutoProxy
    *   Rule List URL:

        ```shell
        https://raw.githubusercontent.com/gfwlist/gfwlist/master/gfwlist.txt
        ```

![auto switch:](/images/20200329/sendpix1.jpg)

### End Words

Enjoy your Internet surfing!
