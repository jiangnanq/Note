# Setup Parse server

1. Install and Run Parse server locally
    ```
    $ npm install -g parse-server mongodb-runner
    $ mongo-runner start
    $ parse-server --appId APPLICATION_ID --masterKey MASTER_KEY --databaseURI mongodb://loalhost/test
    ```

2. To save a object 
    ```
    curl -X POST \
    -H "X-Parse-Applicaton-Id: APPLICATION_ID" \
    -H "Content-Type: applicaton/json" \
    -d '{"score:1337,"playerName":"Jiang","cheatMode":false}' \
    http://localhost:1337/parse/classes/GameScore
    ```

3. Retrieve an object
    ```
    curl -X GET \
    -H "X-Parse-Application-Id: APPLICATION_ID" \
    http://localhost:1337/parse/classes/GameScore
    ```

3. Install and use Parse dashboard
    ```
    npm install -g parse-dashboard
    parse-dashboard --appId APPLICATION_ID --masterKey MASTER_KEY --serverURL "http://localhost:1337/parse"
    ```

4. Push to Heroku
    ```
    git add .
    git commit -m 'update'
    git push heroku master
    ```