---
title: Build My Github Pages With Jekyll
published: true
---

This blog system was built based on the Jekyll theme [Hacker-Blog](http://jekyllthemes.org/themes/hacker-blog/), so this article introduces the whole process of building a blog locally.

*  [](#Ruby)Ruby

In Windows system, use RubyInstaller to install Ruby environment, download link is here：[RubyInstaller](http://rubyinstaller.org/downloads/).

After downloading rubyinstaller, double click rubyinstaller-2.7.0-1-x64.exe file, start up the Ruby installation wizard, click Next, continue the wizard, and check Add Ruby executables to your PATH until the Ruby installation program is finished.

<!-- more -->

After Ruby is installed, there will be an option, choose to install MSYS2, if it is not checked, open cmd yourself, enter "ridk install" to install MSYS2, there will be a choice of 123, choose 3 and then press Enter, this process will download many installation packages, be patient, be sure to install it completely. After the installation is complete, you will be asked to select 123 again, then press Enter directly. If the installation still fails, you can proceed as follows.

Modify the **mirrorlist.mingw64** file in the **msys64/etc/pacman.d** folder, comment out the default installation source, and add the following sources:

```
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/x86_64
Server = http://mirrors.ustc.edu.cn/msys2/mingw/x86_64
Server = http://mirror.bit.edu.cn/msys2/mingw/x86_64
```

Similarly, modify the other two files **mirrorlist.mingw32** and **mirrorlist.msys** in this folder to the corresponding sources.

```
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/mingw/i686
Server = http://mirrors.ustc.edu.cn/msys2/mingw/i686
Server = http://mirror.bit.edu.cn/msys2/mingw/i686
```

```
Server = https://mirrors.tuna.tsinghua.edu.cn/msys2/msys/$arch/
Server = http://mirrors.ustc.edu.cn/msys2/msys/$arch/
Server = http://mirror.bit.edu.cn/msys2/msys/$arch/
```

*  [](#RubyGems)RubyGems

Download the compressed package from the [RubyGems Official Website](https://rubygems.org/pages/download) unzip it, without spaces in the path, and execute the following command to install.

```
cmd rubygems-3.1.2
ruby setup.rb
```

Add [https://gems.ruby-china.com](https://gems.ruby-china.com) to sources.

```
gem sources --add https://gems.ruby-china.com/ --remove https://rubygems.org/
gem sources -l
```

Ensure there is only **https://gems.ruby-china.com**.

Or you should config **~/.bundle/config** by run:

```
bundle config mirror.https://rubygems.org https://gems.ruby-china.com
```

After that, in file **~/.bundle/config**, you will see:

```
---
BUNDLE_MIRROR__HTTPS://RUBYGEMS__ORG/: "https://gems.ruby-china.com"
```

*  [](#install-jekyll-dependencies)Install jekyll dependencies

```bash
gem install bundler
gem install jekyll
gem install jekyll-seo-tag
gem install jekyll-paginate
gem install jekyll-sitemap
```

*  [](#hacker-hlog)Hacker-Blog

Download jekyll theme blog: [Hacker-Blog](http://jekyllthemes.org/themes/hacker-blog/).

Unzip and cd into the hacker-blog folder, and start up the local environment.

```bash
cd blog-directory
bundle install
jekyll serve --watch --port 8000
```

Enter the address [http://127.0.0.1:8000/](http://127.0.0.1:8000/)  in the browser.

Finally, personalize the theme, then upload to github repo and set up CNAME file.
