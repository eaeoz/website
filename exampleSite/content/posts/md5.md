+++
title = "MD5 Command Windows and Linux Usage"
#image = "/images/post/meeting.png"
author = "Sedat"
date = 2019-11-16T05:00:00Z
description = "bitwarden raspberry docker"
categories = ["linux, windows"]
type = "post"

+++
#### Windows:

```
certutil -hashfile test.iso md5
```

#### Linux:

```
md5sum filename > md5sums.txt
md5sum -c md5sums.txt

sha512sum filename > sha512sums.txt
sha512sum -c sha512sums.txt
```