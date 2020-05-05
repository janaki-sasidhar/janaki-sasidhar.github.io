---
layout : post
title : help
date : 2020-02-02 20:50:50
author : sasidhar
categories : help
---

{% highlight javascript %}
#!/bin/bash
# rsync using variables

SOURCEDIR=/home/user/Documents/
DESTDIR=/media/diskid/user_backup/Documents/

rsync -avh --exclude="*.bak" $SOURCEDIR $DESTDIR
{% endhighlight %}
