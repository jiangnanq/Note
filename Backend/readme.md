## Test server for fullstack development

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

    [Reference 1] (https://vishnut.me/blog/ec2-flask-apache-setup.html)

    [Reference 2, config Apache server] (http://flask.pocoo.org/docs/1.0/deploying/mod_wsgi/)

* Domain service use Amazon route 53, link to EC2 server

* HTTPS configuration

    Use certbot.eff.org to config HTTPS service on Apache server

    [Reference 1] (https://certbot.eff.org/lets-encrypt/debianjessie-apache)

    [Reference 2] (https://hackernoon.com/how-to-set-up-https-for-your-domain-on-aws-8f771686603d)
