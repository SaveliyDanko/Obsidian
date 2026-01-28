Remove one or more containers
```shell
docker rm [OPTIONS] CONTAINER [CONTAINER...]
docker rm -fv $(docker ps -a -q)
```

`-f, --force` - Force the removal of a running container (uses SIGKILL)
`-v, --volumes` - Remove anonymous volumes associated with the container
