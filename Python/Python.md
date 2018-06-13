---
title: Python
date: 2018-2-1
tags: Python
---

- Python virtual enviroment
```bash
$ pip install virtual
$ cd my_project_folder
$ virtualenv my_project
$ virtual -p /usr/bin/python2.7 my_project
$ source my_project/bin/activate
$ deactivate
```

- To activate virtualenv
```bash
$ pip install virtualenvwrapper
$ export WORKON_HOME=~/Envs
$ source /usr/local/bin/virtualenvwrapper.sh
```

- Useful command
```bash
mkvirtualenv my_project
workon my_project
deactivate
lsvirtualenv
rmvirtualenv

$ export WORKON_HOME=~/Envs
$ source /usr/local/bin/virtualenvwrapper.sh
$ deactivate
```
[Reference](http://docs.python-guide.org/en/latest/dev/virtualenvs/)

- Read file with Chinese
```Python
import codecs
with codecs.open('areachn.json', 'r', 'utf-8') as fp:
    a = json.load(fp)
```