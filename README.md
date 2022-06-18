# Ionic + Angular + Docker

this project is a simple way to use Ionic with Docker in development environment.

## requirements
- Docker

## How to use to create an angular application without any files
1. After downloading this project, run:
```
docker-compose up --build
```
2. Access the container with the command
```
docker-compose exec app-angular bash
```
4. Inside the container you will be in an environment with Ionic installed globally.
- Then create a new Ionic project
- [Ionic](https://ionicframework.com/docs/intro/cli)
- for example:
```
ionic start
```
- in this example I will use the project name equal to Ionic, which will be the same name as the directory and also the workdir.
4. Then, add the instruction in the package.json file:
```
...
"scripts": {
    ...
    "start": "ng serve --host 0.0.0.0 --port 8100",
    ...
},
...
```
- this command is necessary to start the ng server when starting the container but allow external access to the server.
5. Lastly, update the CMD from the dockerfile file
- FROM
```
WORKDIR /home/node/app
#WORKDIR /home/node/app/Ionic

CMD ["tail", "-f", "/dev/null"]
#CMD ["sh", "-c", "npm install && npm start"]
```
- TO
```
WORKDIR /home/node/app/Ionic

CMD ["sh", "-c", "npm install && npm start"]
```

-
After that you must rebuild your container to get the new workdir. Use the command:
```
docker-compose up --build
```
6. Finished! 
- Next time you start the application use the command below and your server will be ready to receive requests.
```
docker-compose up -d
```

## How to use if you already have an angular project
- You can simply copy the Dockerfile and docker-compose.yml files into your project. Then adjust versions of: npm, angular cli and ionic cli, also correct workdir path
