# dockerfiles
## code-server
```bash
docker run --detach \
    --env PASSWORD=${PASSWORD} \
    --gpus=all \
    --restart=always \
    --name=$(whoami)-code-server \
    --publish 8080:8080 \
    --volume=${HOME}/Development/workspace:/workspace \
    --volume=${HOME}/Data:/Data \
    zaemyung/code-server
```
