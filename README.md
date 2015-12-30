Hapi Server running local or on OpenShift in support of Snowflake
====================================================================
This is a sample Hapi Server that supports basic User Authentication
locally on running on OpenShift.

Locally
----------------------------------------------------------
Install Mongo db and Redis and start them
I used Redis 2.18.24, downloaded the zip
[http://download.redis.io/releases/redis-2.8.24.tar.gz](http://download.redis.io/releases/redis-2.8.24.tar.gz)
and ```make```


Steps to get your custom Node.js version running on OpenShift
----------------------------------------------------------

* Create an account at http://openshift.redhat.com/

* Install the command line tool ```rhc```

* Create a namespace, if you haven't already do so

  ```  rhc domain create <yournamespace>```

* Create a nodejs application - this nodejs, mongodb, rockmongo and
  redis (2.8.13)

```
rhc app-create mysnowflake  nodejs-0.10 mongodb-2.4 rockmongo-1.1 \
http://cartreflect-claytondev.rhcloud.com/reflect?github=transformatordesign/openshift-redis-cart
  
  ```

* Add this repository
```
    cd mysnowflake
    git remote add upstream -m master git://github.com/bartonhammond/snowflake-hapi-openshift.git
    git pull -s recursive -X theirs upstream master
```

* Copy config.sample.js to config.js and provide values

```cp src/config.sample.js src/config.js```

* Then push the repo to OpenShift
```
    git push
``
That's it, you can now checkout your application at:[ http://mysnowflake-$yournamespace.rhcloud.com](http://mysnowflake-$yournamespace.rhcloud.com/)

There are numerous ```curl``` command in ```curl.md```

* If you want to have this project also in your GitHub account follow
these steps

  * https://forums.openshift.com/how-to-keep-a-github-repository-and-an-openshift-repository-in-sync