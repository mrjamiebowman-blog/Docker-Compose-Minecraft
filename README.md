# Docker Compose: Minecraft (Windows)
This is a docker compose tutorial / intro to docker is for setting up a spigot Minecraft server running on a Windows host machine.

This is built on the `itzg/minecraft-server` docker image.

[GitHub: Docker Minecraft Server](https://github.com/itzg/docker-minecraft-server/blob/master/README.md)   

## Requirements
* Docker Desktop / Docker Compose
* Visual Studio Code
* PowerShell
* GitHub Account
* Some minecraft knowledge

## Visual Studio Code (Optional)
If you want to tweak and experiment, please download Visual Studio code and install the `Docker` extension.   

## GitHub: SSH Keys (Optional)
If you want to push and make changes to your own GitHub repo, you will need to setup SSH keys for GitHub.

Generate an ssh key to use in GitHub.
`$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`   

Reading the public key
`type ~/.ssh/id_rsa.pub`   

## Pull Docker Image (Download)
`docker pull itzg/minecraft-server`

## Start
`start.ps1` - will run the docker compose command `docker-compose up -d`, this will start the container in a detatched state.

Alternatively, using strictly docker this command could start it as well:   

`docker run -d -v ${pwd}/data:/data -e TYPE=SPIGOT -p 25565:25565 -e EULA=TRUE -e OPS=jroc83 --name mc itzg/minecraft-server`

### Volume Mount (-v)
The command `-v ${pwd}/data:/data` will mount the container's data folder to the current Windows path. This is used to persist the world data.

Note: The Print Working Directory `{PWD}` command is used to get the current directory. Alternatively, Linux and iOS would use `-v (PWD)/data:/data`. Similar but not the same.

### Environment Variables
`EULA` - this shoudl be true or the server will not run.   
`TYPE` - specifies SPIGOT server.   
`OPS` - set this to your username. This will give you operator/admin status.   

## Stop
`stop.ps1` - this scripts stops the docker compose but does not remove the container.

## Removing Container
If you need to completely remove the container this command will remove it. Because the files are volume mounted the world data should be persisted.

`docker rm -f mc`

## Persisted Data
The data is persisted through a docker volume mount (-v).
