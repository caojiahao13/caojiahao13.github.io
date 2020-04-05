---
layout: default
title: "Jiahao Cao's homepage"
description: Jupyter notebook
theme: jekyll-theme-cayman
---

## 1. How to install jupyter notebook

Jupyter notebook is an app based on **python**. However, new learners may get confused by the huge amount of packages while using python, so **Anaconda** is recommanded.

**Conda** is a powerful tool that help you manage the libraries, packages, and tools in your Computer. **Anaconda** is based on Conda while many commonly used packages and tools are already prepared for you.

So first you should visit the [official site of Anaconda](https://www.anaconda.com/) and install it.

Usually, Jupyter notebook is installed when Anaconda is installed. If you can't find it, try

```{linux}
conda install jupyter notebook
```

in your command line to install  jupyter notebook.

Now try ```jupyter notebook``` to start a Jupyter notebook server on your current location on your own computer. Or your can specify a a port by using ```jupyter notebook --port <port_number>```.

If you want to start the server but don't want to open a browser for it immediately, you can use ```jupyter notebook --no-browser```
