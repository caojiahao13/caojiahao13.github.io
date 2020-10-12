---
layout: default
title: "Jiahao Cao's homepage"
description: Jupyter notebook
theme: jekyll-theme-cayman
---

## 3.Use R in jupyter notebook

Packages to install:

```
install.packages('devtools')
install.packages(c('repr', 'IRdisplay', 'evaluate', 'crayon', 'pbdZMQ', 'uuid', 'digest'))

devtools::install_github('IRkernel/IRkernel')
```

### Install for current user

```IRkernel::installspec() ```

### Install for all users

```IRkernel:installspec(user = FALSE)```

It may take some time. After this, hopefully you can find ```R``` in the same place you find python or conda environments.
