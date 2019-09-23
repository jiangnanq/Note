## Deploy Flask app with nginx using gunicorn and supervisor

* Install required packages
```Bash
sudo apt-get install nginx supervisor python-pip python-virtualenv
```

* Create virtual environment
```Bash
virtualenv .env
activate .env/bin/activate
```

* Create Flask app
```Python
from flask import Flask

app = Flask(__name__)

@app.route('/')
def index():
    return 'hello world'

if __name__ == '__main__':
    app.run(debug=True)
```
Run the app
```Bash
python app.py
```

* Setup gunicorn
```
pip install gunicorn
gunicorn app:app -b localhost:8000 &
```

* Create supervisor file in /etc/supervisor/conf.d/hello_world.conf
```
[program:hello_world]
directory=/home/hello_world
command=/home/.env/bin/gunicorn app:app -b localhost:8000
autostart=true
autorestart=true
stderr_logfile=/var/log/hello_world/hello_world.err.log
stdout_logfile=/var/log/hello_world/hello_world.out.log
```
Enable the configuration
```
sudo supervisorctl reread
sudo service supervisor restart
```
Check the status
```
sudo supervisorctl status
```

* Setup nginx 
```
sudo vim /etc/nginx/conf.d/virtual.conf
```
```
server {
    listen 80;
    server_name domain_name;

    location / {
	proxy_pass http://127.0.0.1:8000;
    }
}
```
restart the service
```bash
sudo nginx -t
sudo service nginx restart
```
