## ELK stack

### Steps

- [Check .env file for Environment variables](#check-env-file)
- [Create certificates](#create-certificates)
- [Up ELK stack](#up-elk-stack)
- [Create passwords for your users](#create-users-passwords)

### Check env file

In the main directory open .env file
(if using Windows - configure your folder setting to showing hidden files, if linux - ctrl + H)

Correct for your environment

### Create certificates

In the main directory use command: 

````
docker-compose -f create-certs.yml run --rm create_certs
````

Runs once and after removes container

### Up ELK stack

In the main directory use command: 

````
docker-compose up
````

Use flag -d for detach up (won't showing any logs in the console)

### Create users password

For having different users for each of part of ELK stack, use next command

````
docker exec elasticsearch /bin/bash -c "bin/elasticsearch-setup-passwords \
auto --batch --url https://elasticsearch:9200"

where elasticsearch - container name and dns name in bridge docker network
````
Supply users by new passwords using .env file or docker-compose.yml file directly

Need to restart the stack after apply new passwords
````
docker-compose stop
docker-compose up
````
