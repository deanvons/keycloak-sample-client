### Start JS Console application

Before interacting with the client make sure you are running the correct version of KC (16), use the command below to run the container

    docker run -p 8080:8080 -e KEYCLOAK_USER=admin -e KEYCLOAK_PASSWORD=admin quay.io/keycloak/keycloak:16.1.1

The JS Console application provides a playground to play with tokens issued by Keycloak.

First build the image with:

    docker build -t demo-js-console js-console
    
Then run it with:

    docker run --name demo-js-console -p 8000:80 demo-js-console

It will fail at first because we need to configure KC to recognise the client as a valid consumer of the tokens

## Creating the realm

Open [Keycloak Admin Console](http://localhost:8080/auth/admin/). Login with
username `admin` and password `admin`.

Create a new realm called `demo` (find the `add realm` button in the drop-down
in the top-left corner). 

Once created set a friendly Display name for the realm, for 
example `Demo SSO`.

## Create a client

Now create a client for the JS console by clicking on `clients` then `create`.

Fill in the following values:

* Client ID: `js-console`
* Click `Save`

On the next form fill in the following values:

* Valid Redirect URIs: `http://localhost:8000/*`
* Web Origins: `http://localhost:8000`

## Enable user registration

Let's enable user self-registration

Open the [Keycloak Admin Console](http://localhost:8080/auth/admin/). 

Click on `Realm settings` then `Login`.

Fill in the following values:

* User registration: `ON`

To try this out open the [JS Console](http://localhost:8000). 

You will be automatically redirected to the login screen. Click on `Register` 
and fill in the form.

You will then be able to login and the js-console will retrieve and display ID and Access tokens which can be used to access restricted data from the API
