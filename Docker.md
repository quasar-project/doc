## Docker/Podman
Собрать тестовый контейнер с Ubuntu 20.04:
```shell
podman build -t quasar/ubuntu20-04 -f .docker/x86_64-ubuntu2004-linux-gnu/Dockerfile .
podman run -it --rm quasar/ubuntu20-04
```

> Выполнять команду нужно из корня проекта.