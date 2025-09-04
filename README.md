### Start JS Console application

The JS Console application provides a playground to play with tokens issued by Keycloak.

First build the image with:

    docker build -t demo-js-console js-console
    
Then run it with:

    docker run --name demo-js-console -p 8000:80 demo-js-console
