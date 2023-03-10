Links
[How To Remove Docker Images, Containers, and Volumes | DigitalOcean](https://www.digitalocean.com/community/tutorials/how-to-remove-docker-images-containers-and-volumes)
# Remove Containers
User the `docker ps` command with `-a` flag to locate the name or ID of the containers you want to remove:
```bash
docker ps -a # list all docker images
docker rm `ID_or_Name` `ID_or_Name` # delete docker image
```

# Remove dangling resources

Docker provides a single command that will clean up any resources — images, containers, volumes, and networks — that are _dangling_ (not tagged or associated with a container):
```bash
docker system prune
```
To additionally remove any stopped containers and all unused images (not just dangling images), add the `-a` flag to the command:
```bash
docker system prune -a
```

# Removing Images

Use  `docker images -a` to locate the ID of the image you want to remove. From there, you can remove it:
```bash
docker rmi IMAGEID1 IMAGEID2
```

## Clean dangling images
Docker images consist of multiple layers. Dangling images are layers that have no relationship to any tagged images. They no longer serve a purpose and consume disk space. They can be located by adding the filter flag `-f` with a value of `dangling=true` to the `docker images` command. When you’re sure you want to delete them, you can use the `docker image prune` command:
**List:**
```bash
docker images -f dangling=true
```
**Remove:**
```bash
docker image prune
```

# Remove Volumes
```bash
docker volume ls
docker volume rm volume_name volume_name
```

## Remove dangling volumes
```bash
docker volume ls -f dangling=true
docker volume prune
```