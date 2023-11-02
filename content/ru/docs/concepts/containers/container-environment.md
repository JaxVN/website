---
reviewers:
title: Контейнерное окружение
content_type: concept
weight: 20
---

<!-- overview -->

На этой странице описаны ресурсы, доступные для контейнеров в соответствующем окружении. 




<!-- body -->

## Контейнерное окружение

Контейнерное окружение Kubernetes предоставляет контейнерам несколько важных ресурсов:

* Файловую систему, сочетающую в себе [образ](/docs/concepts/containers/images/) и один или несколько [томов](/docs/concepts/storage/volumes/).
* Информацию о самом контейнере.
* Информацию о других объектах в кластере.

### Информация о контейнере

*Hostname* контейнера — имя Pod'а, в котором запущен контейнер. Его можно получить с помощью команды `hostname` или функции [`gethostname`](https://man7.org/linux/man-pages/man2/gethostname.2.html) в libc.

Имя Pod'а и его пространство имен можно получить из переменных окружения в [Downward API](/docs/tasks/inject-data-application/downward-api-volume-expose-pod-information/).

Контейнеру также доступны переменные окружения из определения Pod'а, заданные пользователем, а также любые переменные окружения, указанные статически в образе контейнера.

### Информация о кластере

Список всех сервисов, активных на момент создания контейнера, доступен этому контейнеру в виде переменных окружения. Этот список ограничен сервисами в пространстве имен, которому принадлежит Pod с данным контейнером, а также сервисами управляющего слоя Kubernetes.

Для сервиса *foo*, связанного с контейнером *bar*, определены следующие переменные:

```shell
FOO_SERVICE_HOST=<хост, на котором запущен сервис>
FOO_SERVICE_PORT=<порт, на котором запущен сервис>
```

Сервисы получают выделенные IP-адреса и доступны для контейнера через DNS, если включен [аддон DNS](https://releases.k8s.io/v{{< skew currentPatchVersion >}}/cluster/addons/dns/). 


## {{% heading "whatsnext" %}}


* [Хуки жизненного цикла контейнера](/docs/concepts/containers/container-lifecycle-hooks/).
* Упражнение: [Подключаем обработчики к событиям жизненного цикла контейнера](/docs/tasks/configure-pod-container/attach-handler-lifecycle-event/).