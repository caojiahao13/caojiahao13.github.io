---
layout: default
title: "Jiahao Cao's homepage"
description: Jupyter notebook
theme: jekyll-theme-cayman
---

## Connect to remote jupyter server

Do the following on your **romote server**:

## 1.Set password

Execute `ipython`.

**Note:** If the command is not found, we should add its directory to PATH via`PATH=$PATH:/opt/anaconda3/bin`, or enter the directory via `cd /opt/anaconda3/bin` and then execute `./ipython`.

```
In [1]: from notebook.auth import passwd
In [2]: passwd()
Enter password:
Verify password:
Out[2]: 'sha1:8e571a9408f9:6db9d90006692cf665fd206664f2a28e2d9f7582'
```

## 2. Modify configuration file

Edit the file `~/.jupyter/jupyter_notebook_config.py` via `vim` or others, and add the following contents.

```
c.NotebookApp.ip='localhost'
c.NotebookApp.password = u'sha1:8e571a9408f9:6db9d90006692cf665fd206664f2a28e2d9f7582'
c.NotebookApp.open_browser = False
c.NotebookApp.port = 8570
```

## 3. Initialize jupyter notebook

In the server, execute `jupyter notebook`.

## 4. Set up a link from localhost to the remote server

In local system, execute the following command

```
ssh -L localhost:8887:localhost:8570 -f -N -p 5102 USER_NAME@SERVER_IP
```

Then visit `http://localhost:8887` in the browser.

## Use jupyter server with no connection

If your connection with the server is shut down, usually the `jupyter notebook` is also terminated. We can simply use `tmux` and `nohup` to prevent this.

```
tmux nex -s jupy

nohup jupyter notebook --no-browser

```

Then you can shut down your connection with your remote server.

In your local computer, run command like:

```
ssh -L localhost:9999:localhost:17754 -f -N -p 5102 USER_NAME@SERVER_IP
```

Now you can open `localhost:9999` to use your jupyter notebook.


------
