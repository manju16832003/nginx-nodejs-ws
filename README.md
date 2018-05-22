# HOW TO RUN

## Clone the repo

## NPM Install

## Run the WS-Server (ws-server.js)

    First run the ws-server.js `> node ws-server.js`

    that should print 'Server started' and listening on port 8010 and waiting for a client to connect to it. When it receives a client request, it ecohes and sends it back to client.

## Configure Nginx : Nginx proxy configuration

    ```
    server {
        listen 8020;
        location / {
            proxy_pass http://<YourLocalIP>:8010;
            proxy_http_version 1.1;
            proxy_set_header Upgrade $http_upgrade;
            proxy_set_header Connection "upgrade";
            proxy_set_header Host $host;
        }
    }
    ```

## Test: We can test this with wscat 

    We have already installed wscat lib in the first step (`npm install`)

    Lets test it out

    `node_modules/wscat/bin/wscat --connect ws://<YourLocalIP>:8020`

    OR

    `node_modules/wscat/bin/wscat -c ws://<YourLocalIP>:8020`

    Example: Run

    ```
     > node_modules/wscat/bin/wscat --connect ws://<YourLocalIP>:8020
        connected (press CTRL+C to quit)
        > hello
        < Server received from client: hello
        > 
    ```

