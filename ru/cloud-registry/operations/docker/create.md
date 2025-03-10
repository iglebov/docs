---
title: Создать Docker-образ в {{ cloud-registry-name }}
description: В инструкции описано, как создать Docker-образ на основе Dockerfile в {{ cloud-registry-name }} и собрать его.
---

# Создать Docker-образ в {{ cloud-registry-name }}

В инструкции описано, как создать [Docker-образ](../../concepts/docker-image.md) на основе Dockerfile и собрать его.

Чтобы работать с Docker-образами, [установите и настройте](installation.md) Docker.

{% list tabs group=instructions %}

- CLI {#cli}

  1. Создайте файл Dockerfile на вашем устройстве и добавьте туда следующие строки:

     ```dockerfile
     FROM ubuntu:latest
     CMD echo "Hi, I'm inside"
     ```

     Описанный Docker-образ основан на Ubuntu и будет выполнять одну простую команду.

  1. Соберите Docker-образ. В качестве `<идентификатора_реестра>` используется `ID`, полученный при [создании реестра](../registry/create.md).

     ```bash
     docker build . \
       -t {{ cloud-registry }}/<идентификатор_реестра>/ubuntu:hello
     ```

     Флаг `-t` присваивает Docker-образу URL вида `{{ cloud-registry }}/<идентификатор_реестра>/<имя_Docker-образа>:<тег>`. Можно собрать Docker-образ без указания тега. В таком случае Docker CLI присвоит метку по умолчанию: `latest`.

{% endlist %}

После выполнения данных команд будет создан Docker-образ с тегом `hello` в вашем репозитории и полным адресом репозитория, включающим:
* Адрес сервиса {{ cloud-registry-name }} `{{ cloud-registry }}`.
* Идентификатор вашего реестра `<идентификатор_реестра>`.
* Имя вашего репозитория `ubuntu`.
