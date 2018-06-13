---
title: Parse Server setup
date: 28 Jul 2017
tags: Parse
---

1. Install and Run Parse server locally
```bash
$ npm install -g parse-server mongodb-runner
$ mongo-runner start
$ parse-server --appId APPLICATION_ID --masterKey MASTER_KEY --databaseURI mongodb://loalhost/test
```

2. To save a object 
```bash
curl -X POST \
-H "X-Parse-Applicaton-Id: APPLICATION_ID" \
-H "Content-Type: applicaton/json" \
-d '{"score:1337,"playerName":"Jiang","cheatMode":false}' \
http://localhost:1337/parse/classes/GameScore
```

3. Retrieve an object
```bash
curl -X GET \
-H "X-Parse-Application-Id: APPLICATION_ID" \
http://localhost:1337/parse/classes/GameScore
```

3. Install and use Parse dashboard
```bash
npm install -g parse-dashboard
parse-dashboard --appId APPLICATION_ID --masterKey MASTER_KEY --serverURL "http://localhost:1337/parse"
```

4. Push to Heroku
```bash
git add .
git commit -m 'update'
git push heroku master
```