# Docker Compose: Minecraft (Windows)
This is a docker compose / intro to docker tutorial for setting up a Minecraft spigot server.   

This is built on the `itzg/minecraft-server` docker image.

[GitHub: Docker Minecraft Server](https://github.com/itzg/docker-minecraft-server/blob/master/README.md)   

## Requirements
* Docker Desktop / Docker Compose
* Visual Studio Code
* PowerShell
* GitHub Account
* Some minecraft knowledge

## Pull Docker Image (Download)
`docker pull itzg/minecraft-server`

## Start
`start.ps1` - will run the docker compose command `docker-compose up -d`, this will start the container in a detatched state with the name of `minecraft`.

Alternatively, using strictly docker this command could start it as well:   

`docker run -d -v ${pwd}/data:/data -e TYPE=SPIGOT -p 25565:25565 -e EULA=TRUE -e OPS=jroc83 --name mc itzg/minecraft-server`

### List Containers
`Docker ps -a` will display all running containers.   

### Logs
Be sure to keep up with the logs of the container by running this command.

`docker logs minecraft` or if you want to follow the logs (stream) run `docker logs -f minecraft`

### Volume Mount (-v)
The command `-v ${pwd}/data:/data` will mount the container's data folder to the current Windows path. This is used to persist the world data.

Note: The Print Working Directory `{PWD}` command is used to get the current directory. Alternatively, Linux and iOS would use `-v (PWD)/data:/data`. Similar but not the same.

### Environment Variables
`EULA` - this shoudl be true or the server will not run.   
`TYPE` - specifies SPIGOT server.   
`OPS` - set this to your username. This will give you operator/admin status.   
`SPIGET_RESOURCES` - comma delimited plugin resource ids for Spigot to download.

### Plugins
There are two ways to set up plugins in this Dockerized image of Minecraft.

[Spigot: SuperVanish](https://www.spigotmc.org/resources/supervanish-be-invisible.1331/update?update=79065)   

#1 - Default - use a Spigot Resource ID as an environment variable (-e SPIGET_RESOURCES=1331).

#2 - copy in the `SuperVanish.jar` file into the volume mounted path `data/plugins/` ... This will require restarting the container for it to pick up the plugin after it has been copied.   

## Stop
`stop.ps1` - this scripts stops the docker compose but does not remove the container.

## Removing Container
If you need to completely remove the container this command will remove it. Because the files are volume mounted the world data should be persisted.

`docker rm -f mc`

## Persisted Data
The data is persisted through a docker volume mount (-v).

***

## Visual Studio Code (Optional)
If you want to tweak and experiment, please download Visual Studio code and install the `Docker` extension.   

## GitHub: SSH Keys (Optional)
If you want to push and make changes to your own GitHub repo, you will need to setup SSH keys for GitHub.

Generate an ssh key to use in GitHub.
`$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`   

Reading the public key
`type ~/.ssh/id_rsa.pub`   