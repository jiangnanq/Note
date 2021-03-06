## Python 

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
    ```python
    import codecs
    with codecs.open('areachn.json', 'r', 'utf-8') as fp:
        a = json.load(fp)
    ```
- Filter list
    ```python
    test = range(-5, 5)
    lessthanzero = list(filter(lambda x:x < 0, test))
    ```
- Sort list of turple
    ```python
    sorted(result, key=lambda x: x[0], reverse=True)
    ```
- Combine to list
    ```python
    a = [1, 2]
    b = [3, 4]
    c = a + b
    ```
- Sort a dictionary
    ```python
    import operator
    x = {1:2, 3:4, 4:3, 1:0}
    sorted_x = operator(x.items(), key=operator.itemgetter(1))
    Filter dict by value
       sorted_dict = {k: v for k, v in areadata.items() if v > 0}
    ```
- Reduce
```python
    from functools import reduce
    product = reduce((lambda x, y: x+y), [1, 2, 3, 4])
```
