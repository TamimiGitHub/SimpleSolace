# Simple PubSub 

This repo demonstrates a simple publisher subscriber demo using 
- Solace Event broker running on a docker image
- Solace JS client `solclientjs` to communicate with the broker

## Prerequisites
- Docker
- Node 8+
- `npm install` to install the solace JS client 

## How to run
1. Run the Solace event broker in a docker image. This is done by running docker compose
```
docker-compose up -d
```
Note that the `-d` is meant to demonize the event broker to run in the background. After this is done, the event broker is running is running in a docker image and can be accessed from localhost port 80 `localhost:80`. You can run the same command without the `-d` command to see what is happening in the background when the broker is up and running

2. In separate two terminals execute the following

```
node TopicSubscriber.js  ws://localhost:80 default@default secret
```

```
node TopicPublisher.js  ws://localhost:80 default@default secret
```

## Notes
1. The event broker web interface could be accessed from `localhost:8080` with default username/password `admin/admin`. This is very helpful to know whats going on when a publisher or a subscriber connects to the broker
1. You have to wait until the solace demon in the docker image is fully running before connecting to the broker. This can be checked by accessing the broker web interface
1. You can run the Publisher as many times as you'd like and you will get the messages received on the Subscriber terminal

## Cleanup
When done with the broker, navigate to this directory and execute `docker-compose down` to kill the containers and any network ports related to the broker
