# Testing Apache OIDC Locally

This directory contains some sample files and instructions for
experimenting with our Keycloak server using local Docker containers.
The general idea is to spin up two Apache containers, one serving
static content (with server-side includes configured so we can display
headers and environment information), and one acting as the OpenID
Connect authenticating reverse proxy.

# Create an Application Container

Spin up and Apache container serving some static content. This container
will play the role of an application being protected by the authenticating
reverse proxy.

```
docker run -dit -p 8110:80 \
       -v "$PWD/app.conf":/usr/local/apache2/conf/httpd.conf \
       -v "$PWD/index.html":/usr/local/apache2/htdocs/index.html \
       -v "$PWD/user.shtml":/usr/local/apache2/htdocs/user.shtml \
       --name apache-app httpd:2.4
```

Now make sure you can see some content:

```
curl http://localhost:8110/user.shtml
```

# Create an Authenticating Reverse Proxy Container

We again use Apache, but this time we use a Docker image that has mod_auth_oidc
installed and configured. This proxy will require authentication, handle the
authentication flow with redirects, and then forward requests to the appplication.

In order to use this, you will need to configure a client in Keycloak
* Created client "garrick-test"
* Set Access Type to "confidential"
* Set Valid Redirect URIs to "http://localhost:8111/oauth2callback"
* Set Login Theme to "stanford-no-form"
* Save

Now copy the provided sample secret.conf file:

```
cp sample.secret.conf local.secret.conf
```

Edit the file to include the client secret for the client you created in Keycloak,
and add a securely generated pass phrase for the session keys.


```
docker run -dit -p 8111:80 \
       -v "$PWD/proxy.conf":/usr/local/apache2/conf/httpd.conf \
       -v "$PWD/local.secret.conf":/usr/local/apache2/conf/extra/secret.conf \
       -v "$PWD/oidc.conf":/usr/local/apache2/conf/extra/oidc.conf \
       --link apache-app:app \
       --name apache-proxy somrit/apache-oidc
```

Now open a fresh web browser with private (incognito) mode, and go to this url:

[http://localhost:8111/user.shtml](http://localhost:8111/user.shtml)
