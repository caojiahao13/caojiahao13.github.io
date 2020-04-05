---
layout: default
title: "Jiahao Cao's homepage"
description: Jupyter notebook
theme: jekyll-theme-cayman
---

## 2.Set your configuration

your configurations are stored in ```jupyter_notebook_config.py```. The path to this file should be ```C:\Users\<user_name>\.jupyter\``` in Windows or ```/Users/<user_name>/.jupyter/``` in Linux/MacOS.

You can find the file using ``` jupyter notebook --generate-config ``` and choose ```N```. This command is to reset the ```jupyter_notebook_config.py``` by the default configuration.

Now you can open ```jupyter_notebook_config.py``` by editors like vim.(tip: use ```/``` to find text in vim, e.g. ```/c.NotebookApp.notebook_dir```)

#### Use nb_conda to link conda with jupyter notebook

Conda give us a good way to manage packages and we hope we can use this while running jupyter.

Install nb_conda with command line:

```
conda install nb_conda
```

Then all environments in conda can be used and there will be a ```conda``` tag at the top of Jupyter notebook page.
