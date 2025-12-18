# kuber-homeworks_3.3

# Домашнее задание к занятию «Как работает сеть в K8s»

### Цель задания

Настроить сетевую политику доступа к подам.

### Чеклист готовности к домашнему заданию

1. Кластер K8s с установленным сетевым плагином Calico.

### Инструменты и дополнительные материалы, которые пригодятся для выполнения задания

1. [Документация Calico](https://www.tigera.io/project-calico/).
2. [Network Policy](https://kubernetes.io/docs/concepts/services-networking/network-policies/).
3. [About Network Policy](https://docs.projectcalico.org/about/about-network-policy).

-----

### Задание 1. Создать сетевую политику или несколько политик для обеспечения доступа

1. Создать deployment'ы приложений frontend, backend и cache и соответсвующие сервисы.
2. В качестве образа использовать network-multitool.
3. Разместить поды в namespace App.
4. Создать политики, чтобы обеспечить доступ frontend -> backend -> cache. Другие виды подключений должны быть запрещены.
5. Продемонстрировать, что трафик разрешён и запрещён.

-----
**Поднял кластер 1 мастер / 2 воркер ноды**
<img width="769" height="380" alt="1" src="https://github.com/user-attachments/assets/89d284d0-ae2c-4286-a09e-1d9034d4c1b6" />

Присоединяем воркеры к мастеру:
<img width="1215" height="540" alt="2" src="https://github.com/user-attachments/assets/bdb1193f-62ea-43c9-9e71-e7db9bd9d9ce" />

**Применяем манифесты (приложены в репозиторий):**
- [namespace.yaml](https://github.com/Werest/kuber-homeworks_3.3/blob/633f773c044bd6c6958d2b815110be97406132fc/namespace.yaml)
- [deployments.yaml](https://github.com/Werest/kuber-homeworks_3.3/blob/633f773c044bd6c6958d2b815110be97406132fc/deployments.yaml)
- [services.yaml](https://github.com/Werest/kuber-homeworks_3.3/blob/633f773c044bd6c6958d2b815110be97406132fc/services.yaml)
- [network-policies.yaml](https://github.com/Werest/kuber-homeworks_3.3/blob/633f773c044bd6c6958d2b815110be97406132fc/network-policies.yaml)

<img width="882" height="533" alt="3" src="https://github.com/user-attachments/assets/a390322f-72b0-47e0-929c-eb26101112a1" />

**Проверяем разрешенные подключения:**
- Получаем имена подов
  - Проверяем frontend -> backend
  - Проверяем backend -> cache
<img width="1357" height="1175" alt="image" src="https://github.com/user-attachments/assets/7bcc9b3c-a8bd-40a0-a32f-d1142b66982a" />

**Проверяем запрещенные подключения:**
- Проверяем, что frontend НЕ может обратиться напрямую к cache
- Проверяем, что cache НЕ может обратиться к backend
- Проверяем, что backend НЕ может обратиться к frontend
<img width="1562" height="434" alt="image" src="https://github.com/user-attachments/assets/92ca2a38-8950-49fb-ad03-5eef93a965d3" />

**Проверка политик:**
- Просмотр всех сетевых политик в namespace app
- Детальный просмотр конкретной политики
<img width="1103" height="559" alt="image" src="https://github.com/user-attachments/assets/890ba3cc-d897-41c7-b778-ccfb22b4e468" />

-----

### Правила приёма работы

1. Домашняя работа оформляется в своём Git-репозитории в файле README.md. Выполненное домашнее задание пришлите ссылкой на .md-файл в вашем репозитории.
2. Файл README.md должен содержать скриншоты вывода необходимых команд, а также скриншоты результатов.
3. Репозиторий должен содержать тексты манифестов или ссылки на них в файле README.md.
