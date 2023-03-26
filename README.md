# Docker Compose: Minecraft (Windows)
This is a docker compose tutorial / intro to docker is for setting up a spigot Minecraft server. This will also install the SuperVanish plugin in one of two ways. You can either copy in the file your self and drop it in the plugins folder through a volume mount (-v) or through an environmental variable.

## Requirements
* Docker Desktop
* Visual Studio Code
* PowerShell
* GitHub Account
* Some minecraft knowledge

## GitHub: SSH Keys (Optional)
If you want to push and making changes to your own GitHub repo, you will need to setup SSH keys for GitHub.

Generate an ssh key to use in GitHub.
`$ ssh-keygen -t rsa -b 4096 -C "your_email@example.com"`   

Reading the public key
`type ~/.ssh/id_rsa.pub`   

## Start
`start.ps1` - will run the docker compose command `docker-compose up -d`, this will start the container in a detatched state.

Alternatively, using strictly docker this command could start it as well.
`docker run -d -v ${pwd}/data:/data -e TYPE=SPIGOT -p 25565:25565 -e EULA=TRUE -e OPS=jroc83 --name mc itzg/minecraft-server`

## Stop
`stop.ps1` - this scripts stops the docker compose but does not remove the container.

## Removing Container
If you need to completely remove the container this command will remove it. Because the files are volume mounted the world data should be persisted.

`docker rm -f mc`

## Persisted Data
The data is persisted through a docker volume mount (-v).
