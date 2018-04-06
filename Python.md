# Notes for Python Language 

- Python virtual enviroment
```
$ pip install virtual
$ cd my_project_folder
$ virtualenv my_project
$ virtual -p /usr/bin/python2.7 my_project
$ source my_project/bin/activate
$ deactivate
```

- To activate virtualenv
```
$ pip install virtualenvwrapper
$ export WORKON_HOME=~/Envs
$ source /usr/local/bin/virtualenvwrapper.sh
```

- Useful command
```
mkvirtualenv my_project
workon my_project
deactivate
lsvirtualenv
rmvirtualenv
```
[Details](http://docs.python-guide.org/en/latest/dev/virtualenvs/)

- Read file with Chinese
```Python
import codecs
with codecs.open('areachn.json', 'r', 'utf-8') as fp:
    a = json.load(fp)
```
