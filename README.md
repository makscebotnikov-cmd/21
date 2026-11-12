# Домашнее задание к занятию 4 «Оркестрация группой Docker контейнеров на примере Docker Compose» Чеботников М.Б.

### Инструкция к выполению

1. Для выполнения заданий обязательно ознакомьтесь с [инструкцией](https://github.com/netology-code/devops-materials/blob/master/cloudwork.MD) по экономии облачных ресурсов. Это нужно, чтобы не расходовать средства, полученные в результате использования промокода.
2. Практические задачи выполняйте на личной рабочей станции или созданной вами ранее ВМ в облаке.
3. Своё решение к задачам оформите в вашем GitHub репозитории в формате markdown!!!
4. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.

## Задача 1

Сценарий выполнения задачи:
- Установите docker и docker compose plugin на свою linux рабочую станцию или ВМ.
- Если dockerhub недоступен создайте файл /etc/docker/daemon.json с содержимым: ```{"registry-mirrors": ["https://mirror.gcr.io", "https://daocloud.io", "https://c.163.com/", "https://registry.docker-cn.com"]}```
- Зарегистрируйтесь и создайте публичный репозиторий  с именем "custom-nginx" на https://hub.docker.com (ТОЛЬКО ЕСЛИ У ВАС ЕСТЬ ДОСТУП);
- скачайте образ nginx:1.21.1;
- Создайте Dockerfile и реализуйте в нем замену дефолтной индекс-страницы(/usr/share/nginx/html/index.html), на файл index.html с содержимым:
```
<html>
<head>
Hey, Netology
</head>
<body>
<h1>I will be DevOps Engineer!</h1>
</body>
</html>
```
- Соберите и отправьте созданный образ в свой dockerhub-репозитории c tag 1.0.0 (ТОЛЬКО ЕСЛИ ЕСТЬ ДОСТУП). 
- Предоставьте ответ в виде ссылки на https://hub.docker.com/<username_repo>/custom-nginx/general .

## Ответ 

Dockerfile:
```dockerfile
FROM nginx:1.21.1
COPY index.html /usr/share/nginx/html/index.html
```

Сборка и публикация образа в мой репозиторий Docker Hub:
```bash
docker login -u chebtnik
docker build -t chebtnik/custom-nginx:1.0.0 .
docker push chebtnik/custom-nginx:1.0.0
```

<img width="625" height="135" alt="1" src="https://github.com/user-attachments/assets/1420ddcb-b713-44c5-b331-bf64b47888ab" />


---

<img width="1078" height="807" alt="2" src="https://github.com/user-attachments/assets/dd1d0ce0-3a1d-4ec1-9b13-2c9b374c3c03" />


---

<img width="1980" height="938" alt="3" src="https://github.com/user-attachments/assets/59386c44-03d8-4948-b7b5-b0f913ce3678" />


---

Ссылка: https://hub.docker.com/repository/docker/chebtnik/custom-nginx/general

---

## Задача 2
1. Запустите ваш образ custom-nginx:1.0.0 командой docker run в соответвии с требованиями:
- имя контейнера "ФИО-custom-nginx-t2"
- контейнер работает в фоне
- контейнер опубликован на порту хост системы 127.0.0.1:8080
2. Не удаляя, переименуйте контейнер в "custom-nginx-t2"
3. Выполните команду ```date +"%d-%m-%Y %T.%N %Z" ; sleep 0.150 ; docker ps ; ss -tlpn | grep 127.0.0.1:8080  ; docker logs custom-nginx-t2 -n1 ; docker exec -it custom-nginx-t2 base64 /usr/share/nginx/html/index.html```
4. Убедитесь с помощью curl или веб браузера, что индекс-страница доступна.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

## Ответ 

<img width="1171" height="438" alt="4" src="https://github.com/user-attachments/assets/33831cca-bde9-4cd1-8082-1c1d07141e8a" />


---

## Задача 3
1. Воспользуйтесь docker help или google, чтобы узнать как подключиться к стандартному потоку ввода/вывода/ошибок контейнера "custom-nginx-t2".
2. Подключитесь к контейнеру и нажмите комбинацию Ctrl-C.
3. Выполните ```docker ps -a``` и объясните своими словами почему контейнер остановился.
4. Перезапустите контейнер
5. Зайдите в интерактивный терминал контейнера "custom-nginx-t2" с оболочкой bash.
6. Установите любимый текстовый редактор(vim, nano итд) с помощью apt-get.
7. Отредактируйте файл "/etc/nginx/conf.d/default.conf", заменив порт "listen 80" на "listen 81".
8. Запомните(!) и выполните команду ```nginx -s reload```, а затем внутри контейнера ```curl http://127.0.0.1:80 ; curl http://127.0.0.1:81```.
9. Выйдите из контейнера, набрав в консоли  ```exit``` или Ctrl-D.
10. Проверьте вывод команд: ```ss -tlpn | grep 127.0.0.1:8080``` , ```docker port custom-nginx-t2```, ```curl http://127.0.0.1:8080```. Кратко объясните суть возникшей проблемы.
11. * Это дополнительное, необязательное задание. Попробуйте самостоятельно исправить конфигурацию контейнера, используя доступные источники в интернете. Не изменяйте конфигурацию nginx и не удаляйте контейнер. Останавливать контейнер можно. [пример источника](https://www.baeldung.com/linux/assign-port-docker-container)
12. Удалите запущенный контейнер "custom-nginx-t2", не останавливая его.(воспользуйтесь --help или google)

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

## Ответ 

<img width="1705" height="993" alt="5" src="https://github.com/user-attachments/assets/2720377e-61e7-45ba-9110-412dfe54e1a7" />


---

**Пункт 3. Почему контейнер остановился.**

Командой `docker attach custom-nginx-t2` я подключился к стандартным потокам ввода/вывода не «контейнера вообще», а его главного процесса — того, что запущен с PID 1. В образе nginx это мастер-процесс `nginx -g 'daemon off;'`. По умолчанию `docker attach` пробрасывает сигналы в контейнер (`--sig-proxy=true`), поэтому нажатие Ctrl-C отправило сигнал SIGINT прямо мастер-процессу nginx. Получив SIGINT, nginx выполняет быстрое завершение работы и выходит.

Контейнер живёт ровно столько, сколько живёт его процесс с PID 1. Как только nginx завершился, Docker перевёл контейнер в состояние `Exited`, что и видно в `docker ps -a`. Чтобы отключиться, не останавливая контейнер, нужно было использовать комбинацию Ctrl-P, Ctrl-Q или подключаться с `docker attach --sig-proxy=false`.

---

<img width="1829" height="554" alt="6" src="https://github.com/user-attachments/assets/e941dbe6-70ea-4e17-9d26-db434124c478" />


---

**Пункт 10. Суть проблемы.**

После изменения порта Nginx на 81 в контейнере, Docker продолжал пробрасывать трафик с хостового 8080 на порт 80 контейнера, который более не использовался. Это привело к ошибке соединения. Для исправления нужно либо вернуть listen 80 в конфиге Nginx, либо изменить проброс портов при запуске контейнера.

---

## Задача 4


- Запустите первый контейнер из образа ***centos*** c любым тегом в фоновом режиме, подключив папку  текущий рабочий каталог ```$(pwd)``` на хостовой машине в ```/data``` контейнера, используя ключ -v.
- Запустите второй контейнер из образа ***debian*** в фоновом режиме, подключив текущий рабочий каталог ```$(pwd)``` в ```/data``` контейнера. 
- Подключитесь к первому контейнеру с помощью ```docker exec``` и создайте текстовый файл любого содержания в ```/data```.
- Добавьте ещё один файл в текущий каталог ```$(pwd)``` на хостовой машине.
- Подключитесь во второй контейнер и отобразите листинг и содержание файлов в ```/data``` контейнера.


В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод.

## Ответ 

<img width="1429" height="650" alt="7" src="https://github.com/user-attachments/assets/8665bfff-2ba4-47dd-b5ee-7a914639a8df" />


---

## Задача 5

1. Создайте отдельную директорию(например /tmp/netology/docker/task5) и 2 файла внутри него.
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

2. Отредактируйте файл compose.yaml так, чтобы были запущенны оба файла. (подсказка: https://docs.docker.com/compose/compose-file/14-include/)

3. Выполните в консоли вашей хостовой ОС необходимые команды чтобы залить образ custom-nginx как custom-nginx:latest в запущенное вами, локальное registry. Дополнительная документация: https://distribution.github.io/distribution/about/deploying/
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
6. Перейдите на страницу "http://127.0.0.1:9000/#!/2/docker/containers", выберите контейнер с nginx и нажмите на кнопку "inspect". В представлении <> Tree разверните поле "Config" и сделайте скриншот от поля "AppArmorProfile" до "Driver".

7. Удалите любой из манифестов компоуза(например compose.yaml).  Выполните команду "docker compose up -d". Прочитайте warning, объясните суть предупреждения и выполните предложенное действие. Погасите compose-проект ОДНОЙ(обязательно!!) командой.

В качестве ответа приложите скриншоты консоли, где видно все введенные команды и их вывод, файл compose.yaml , скриншот portainer c задеплоенным компоузом.

## Ответ 

Сначала у меня была установлена только standalone-версия Docker Compose (v2.34.0), и команда `docker compose` (через пробел) не работала. Я подключил тот же бинарник как плагин Docker CLI, после чего `docker compose` заработала:
```bash
mkdir -p ~/.docker/cli-plugins
ln -s "$(which docker-compose)" ~/.docker/cli-plugins/docker-compose
docker compose version
```
Все команды ниже запускаются **без ключа `-f`**: Compose сам выбирает файл в текущем каталоге.

**Пункт 1. Какой файл запустился и почему.**

```bash
cd /tmp/netology/docker/task5
docker compose up -d
```

Запустился файл `compose.yaml`, то есть поднялся только сервис **portainer**, а `registry` из `docker-compose.yaml` не запустился.

Причина в приоритете имён файлов. Когда ключ `-f` не указан, Compose ищет файл в рабочем каталоге в строгом порядке: `compose.yaml` → `compose.yml` → `docker-compose.yaml` → `docker-compose.yml`. Берётся первый найденный файл, остальные игнорируются. `compose.yaml` — это каноническое, «новое» имя по спецификации Compose, а `docker-compose.yaml` поддерживается только ради обратной совместимости, поэтому у него приоритет ниже. Compose сам сообщает об этом предупреждением: `Found multiple config files with supported names: compose.yaml, docker-compose.yaml. Using compose.yaml`.

Ключом `-f` этот механизм как раз отключается — файл задаётся вручную, и приоритет имён уже не участвует. Поэтому здесь `-f` не используется.

**Пункт 2. Запуск обоих файлов через include.**

Итоговый `compose.yaml`:
```yaml
include:
  - docker-compose.yaml

services:
  portainer:
    network_mode: host
    image: portainer/portainer-ce:latest
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock
```
(Строку `version` я убрал: в Compose v2 она устарела и только вызывает предупреждение `the attribute version is obsolete`.)

```bash
docker compose up -d
docker compose ps
```

<img width="1862" height="914" alt="8" src="https://github.com/user-attachments/assets/10e2d3b6-d26f-4555-a997-42ab214589e4" />

**Пункт 3. Загрузка образа в локальный registry.**
```bash
docker tag chebtnik/custom-nginx:1.0.0 127.0.0.1:5000/custom-nginx:latest
docker push 127.0.0.1:5000/custom-nginx:latest
curl http://127.0.0.1:5000/v2/_catalog
```

---

<img width="1841" height="616" alt="9" src="https://github.com/user-attachments/assets/ca95ae24-44f3-42e3-bc76-2b57d628d093" />


---

<img width="1689" height="818" alt="10" src="https://github.com/user-attachments/assets/1c9eddbf-4703-4703-a57c-d498a3c20e7b" />


---

<img width="1526" height="892" alt="11" src="https://github.com/user-attachments/assets/f1554319-f00c-47a4-8601-63a7ac47b376" />


---

**Пункт 7. Warning после удаления compose.yaml.**

```bash
rm compose.yaml
docker compose up -d
```

Compose выдал предупреждение:
`WARN[0000] Found orphan containers ([task5-portainer-1]) for this project. If you removed or renamed this service in your compose file, you can run this command with the --remove-orphans flag to clean it up.`

Суть предупреждения. Compose связывает контейнеры с проектом по имени проекта (по умолчанию это имя каталога, `task5`) — на каждом контейнере стоит метка `com.docker.compose.project=task5`. После удаления `compose.yaml` Compose по приоритету имён взял `docker-compose.yaml`, где описан только `registry`. Контейнер `portainer` при этом остался запущенным и по-прежнему помечен как часть проекта `task5`, но в текущей конфигурации его уже нет. Такой контейнер называется «осиротевшим» (orphan). Compose сам его не трогает, а только предупреждает и предлагает убрать ключом `--remove-orphans`.

Выполняю предложенное действие:
```bash
docker compose up -d --remove-orphans
```

Гашу проект одной командой:
```bash
docker compose down
```

---

### Правила приема

Домашнее задание выполните в файле readme.md в GitHub-репозитории. В личном кабинете отправьте на проверку ссылку на .md-файл в вашем репозитории.
