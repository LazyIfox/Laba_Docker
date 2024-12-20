# Лабораторная работа №3 по Информационным технологиям
Выполнила Сологубова Влада
## Задание 1:
Ответ: [Ссылка](https://hub.docker.com/repository/docker/ladala/custom-nginx/general) на dockerhub-репозиторий.
## Задание 2:
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080

2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"

3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```

4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

Ниже предоставлены картинки к заданию два. Скриншот консоли и страница веб браузера:
<img width="602" alt="2 1" src="https://github.com/user-attachments/assets/2eb31a3f-36ee-424f-99ab-bd566024dbc8" />

<img width="593" alt="2 22" src="https://github.com/user-attachments/assets/e2bb9cfb-4ea4-4384-a144-6da047a0b811" />

## Задание 3:
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
- Ответ: docker attach позволяет подключится к стандартному потоку ввода/вывода/ошибок контейнера

2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.

3. Выполните ```docker ps -a``` и объясните своими словами почему контейнер остановился.
- Ответ: Комбинация Ctrl-C подала сигнал nginx завершить работу, поэтому контейнер остановился.

4. Перезапустите контейнер

5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.

6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.

7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".

8. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.

9. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.

10. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.
- Ответ: Изменили в конфигурации Nginx порт с 80 на 81, поэтому запрос к порту 80 возвращает сообщение об ошибке, так как не удалось произвести соединение.
12. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

Ниже предоставлены картинки к заданию три (скриншоты консоли):
<img width="602" alt="3 1" src="https://github.com/user-attachments/assets/bae82f80-a718-4c26-a10a-ad209e35b5f7" />

<img width="599" alt="3 2" src="https://github.com/user-attachments/assets/5223e21d-bf04-4e3d-ac0a-10a5801aae94" />

## Задание 4:

- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.

- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера. 

- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.

- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.

- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.

Ниже предоставлены картинки к заданию четыре (скриншоты консоли):
<img width="570" alt="4 1" src="https://github.com/user-attachments/assets/e236f16c-4845-4f44-bce6-45c64fc26db6" />

<img width="336" alt="4 2" src="https://github.com/user-attachments/assets/860f101d-608c-409d-b8c6-91b23919ec77" />

## Задание 5:

1. Создайте отдельную директорию(например /tmp/ZGU/docker/task) и 2 файла внутри него.
"compose.yaml" с содержимым:

```
version: "3"
services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```

"docker-compose.yaml" с содержимым:

```
version: "3"
services:
  registry:
    image: registry:2

    ports:
    - "5000:5000"
```

И выполните команду "docker compose up -d". Какой из файлов был запущен и почему? (подсказка: https://docs.docker.com/compose/compose-application-model/#the-compose-file )
- Ответ: Путь по умолчанию для файла Compose — compose.yaml(предпочтительно). Compose также поддерживает docker-compose.yaml для обратной совместимости с более ранними версиями. Если существуют оба файла, Compose предпочитает канонический compose.yaml.
- Ниже скриншоты созданных файлов и консоли:

<img width="385" alt="5 1" src="https://github.com/user-attachments/assets/e312bdca-6b12-4c89-9ae8-07a54992daac" />

<img width="412" alt="5 2" src="https://github.com/user-attachments/assets/6c4b0316-117e-4929-bc10-898d5f8b09ed" />

<img width="580" alt="5 20 1" src="https://github.com/user-attachments/assets/974f9656-363d-4daf-8844-04c5fe95191c" />

<img width="596" alt="5 21" src="https://github.com/user-attachments/assets/fbc6f367-0281-409f-a269-348bbf1b94ef" />

2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)
- Ниже скриншоты отредактированного файла compose.yaml и скриншоты консоли:

<img width="375" alt="5 3" src="https://github.com/user-attachments/assets/4aac5cf6-d9cc-4cb4-af31-c7d9a044d052" />

<img width="598" alt="5 22" src="https://github.com/user-attachments/assets/f2f7b390-28d4-4a2a-8c66-b5c5196ac808" />

3. Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/
- Ниже скриншот консоли:

<img width="593" alt="5 23" src="https://github.com/user-attachments/assets/6943d149-0ec5-4351-a905-f8893b09ce80" />

4. Откройте страницу "https://127.0.0.1:9000" и произведите начальную настройку portainer.(логин и пароль адмнистратора)

5. Откройте страницу "http://127.0.0.1:9000/#!/home", выберите ваше local  окружение. Перейдите на вкладку "stacks" и в "web editor" задеплойте следующий компоуз:

```
version: '3'

services:
  nginx:
    image: 127.0.0.1:5000/custom-nginx
    ports:
      - "9090:80"
```
Ниже скриншоты страницы portainer:

<img width="600" alt="5 6" src="https://github.com/user-attachments/assets/934cf544-52e2-4b4b-8dad-4011df316587" />

<img width="602" alt="5 8" src="https://github.com/user-attachments/assets/75755a4a-87da-4702-a707-63c1682ec1fc" />

6. Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".
- Ниже требуемый скриншот:

<img width="601" alt="5 9" src="https://github.com/user-attachments/assets/51d92730-4bbc-4031-aaaa-0dfebd74d79e" />

7. Удалите любой из манифестов компоуза(например compose.yaml).  Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.
- Ответ: Docker Compose видит контейнер task-portainer-1, который был созданы ранее, но он больше не определены в текущем файле Compose (после удаления файла compose.yaml текущим файлом стал docker compose.yaml). warning предлагает очистить контейнер с помощью --remove-orphans, что мы и делаем. В конце гасим compose-проект с помошью команды down.
- Ниже скриншот консоли:

<img width="599" alt="5 24" src="https://github.com/user-attachments/assets/cfee0b7c-7b4b-4bdd-84fe-0c04f017f37a" />
