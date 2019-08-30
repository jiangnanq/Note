## Web application solution

* Flask/Gunicorn/Nginx/supervisor solution

    1. Setup flask app

    2. Setup Gunicorn: install Gunicorn, start gunicorn service in background

    3. Use supervisor to monitor and control Gunicorn process, write configuraion file, restart the service.

    4. Setup Nginx: Write config file, the port should be same as gunicorn, restart the service

       [Reference](https://medium.com/ymedialabs-innovation/deploy-flask-app-with-nginx-using-gunicorn-and-supervisor-d7a93aa07c18)

* To connect to the AWS server

    ```
    ssh -i aws_ec2.pem admin@ec2address
    ```

* The python project location is ~/PycharmProjects/testServer

* To run a flask app 
    ```
    source env/bin/activate
    export FLASK_APP=test.py
    flask run --host=0.0.0.0
    ```

* app.wsgi configuration
    ```
    activate_this = '/home/admin/ec2server/ec2server/bin/activate_this.py'
    with open(activate_this) as f:
        exec(f.read(), dict(__file__=activate_this))
    
    import sys
    import logging
    
    logging.basicConfig(stream=sys.stderr)
    sys.path.insert(0,"/var/www/html/ec2server/")
    
    from test import app as application
    ```

* Apache configuration

    - location /ect/apache2/sites-availiable
    - Log file location: /etc/log/apache2/error.log
    ```
    WSGIDaemonProcess test threads=5
    WSGIScriptAlias / /var/www/html/ec2server/app.wsgi
    
    <Directory /var/www/ec2server>
        WSGIProcessGroup test
        WSGIApplicationGroup %{GLOBAL}
        Order deny,allow
        Allow from all
    </Directory>
    ```

    [Reference 1](https://vishnut.me/blog/ec2-flask-apache-setup.html)

    [Reference 2, config Apache server](http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/)

* Domain service use Amazon route 53, link to EC2 server

* HTTPS configuration

    Use certbot.eff.org to config HTTPS service on Apache server

    [Reference 1](https://certbot.eff.org/lets-encrypt/debianjessie-apache)

    [Reference 2](https://hackernoon.com/how-to-set-up-https-for-your-domain-on-aws-8f771686603d)

* Check apache status
    ```
    sudo systemctl status apache2
    ```

* View logs
    ```
    tail -10 /var/log/apache2/access.log
    ```


* User supervisor to run script in backend

  1. Prepare the config file in /etc/supervisor/conf.d/udp.conf

  2. sudo supervisorctl reread

  3. sudo service supervisor restart

  4. sudo supervisorctl status

     ```
     [program:udp]
       directory=/home/pi/smartward
       command=/home/pi/.local/share/virtualenvs/smartward-Kb6GjW-e/bin/python -u udp.py
       autostart=true
       autorestart=true
       stderr_logfile=/var/log/smartward/udp.err.log
       stdout_logfile=/var/log/smartward/udp.out.log
     ```
 
