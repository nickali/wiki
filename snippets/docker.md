# Docker

### Create new image from container and Push

```bash
$ docker commit <container_id> new_image_name:tag_name
$ docker tag new_image_name:tag_name <REGISTRY_URL>/nali/docker/ \
    new_image_name:tag_name
$ docker push <REGISTRY_URL>/nali/docker/new_image_name:tag_name
```



