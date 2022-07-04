## Развертывание окружения для авто тестирования

### Technology Stack

![Winscp](src/images/icons/Winscp.svg)
![Git_bash](src/images/icons/Git_bash.svg)
![Java](src/images/icons/Java.svg)
![Docker_Compose](src/images/icons/Docker.svg)
![Docker_Compose](src/images/icons/Docker_Compose.svg)
![Jenkins](src/images/icons/Jenkins.svg)
![Gradle](src/images/icons/Gradle.svg)
![Allure_Report](src/images/icons/Allure_Report.svg)
![Selenoid](src/images/icons/Selenoid.svg)



##    Подготовка

Скачиваем и устанавливаем <a target="_blank" href="https://gitforwindows.org/">Git bash</a> и <a target="_blank" href="https://winscp.net/eng/download.php">WinSCP</a>.

Открываем WinSCP заходим на выделенный сервер создаём папку test-stand.

Внутри папки test-stand создаём папку work и init.

![Подготовка](src/images/screenshots/1.png)

Внутри папки work создаём папку jenkins и папку selenoid.

![Подготовка](src/images/screenshots/2.png)

Внутри папки selenoid создаём папку video и папку logs.

![Подготовка](src/images/screenshots/3.png)

Внутри папки init создаём папку Selenoid внутри папки Selenoid создаём файл <a target="_blank" href="https://github.com/Konyaz/Testing_infrastructure/blob/master/test-stand/init/selenoid/browsers.json">browsers.json</a> .


![Подготовка](src/images/screenshots/4.png)


Открываем git bash заходим на сервер командой:

```bash
ssh юзернейм@192.168.x.xxx
```
Вводим пароль если требуется, переходим в созданную папку test-stand командой:
```bash
cd test-stand
```



##    Установка Java




Проверяем, наличие Java командой:
```bash
java --version
```
Если Java не установлена - Инструкция по установке [Java JDK](./src/images/pages/Java.md)

## Установка Docker




Проверяем, установлен ли Docker командой:
```bash
docker --version
```

Если Docker не установлен - Инструкция по установке [Docker](./src/images/pages/Docker.md).



## Установка Docker Compose




Проверяем, есть ли у нас Docker Compose командой:
```bash
docker-compose --version
```
Если Docker Compose не установлен - Инструкция по установке [Docker Compose](./src/images/pages/DockerCompose.md).

## Установка Jenkins

После того как установлена Java, прописана её переменная окружения, установлены и проверены Docker и Docker-compose

Открываем WinSCP и заходим в папку test-stand.

Внутри папки test-stand создаём файл docker-compose.yml



![DOCKER-COMPOSE](src/images/screenshots/5.png)

Сохраняем код из файла <a target="_blank" href="https://github.com/Konyaz/Testing_infrastructure/blob/master/test-stand/docker-compose(Jenkins).yml">docker-compose(Jenkins).yml</a> вставляем его на сервер в папку test-stand в файл docker-compose.yml для установки Jenkins:



![DOCKER-COMPOSE](src/images/screenshots/docker-compose.png)


Открываем Git bash На сервере переходим в папку test-stand командой:
```bash
cd test-stand
```
Пишем команду для остановки контейнеров:
```bash
sudo docker-compose down
```
После пишем команду, для того чтоб установить образ:
```bash
sudo docker-compose pull
```
Проверяем установлен ли образ командой:
```bash
sudo docker-compose imgge list
```
![JENKINS](src/images/screenshots/jenkins2.png)

После того как убедились что образ установлен успешно, пишем команду для запуска контейнера:
```bash
sudo docker-compose up
```
После первого запуска сохраняем password (пароль). Он показывается после первого запуска поэтому важно его сохранить：

![JENKINS](src/images/screenshots/jenkins.png)

Заходим в Jenkins по адресу http://192.168.x.xxx:8888

Вводим сохраненный до этого пароль в поле Administrator password.

![JENKINS](src/images/screenshots/jenkins3.png)

Устанавливаем плагины нажимая Install suggested plugins.

![JENKINS](src/images/screenshots/jenkins4.png)

Задаем логин и пароль для администратора.

![JENKINS](src/images/screenshots/jenkins5.png)

Переходим в настройки.

![JENKINS](src/images/screenshots/jenkins6.png)

Устанавливаем плагины: GitLab , Post build task, Text File Operations, Allure Jenkins Plugin.

![JENKINS](src/images/screenshots/jenkins7.png)

Переходим в “Конфигурация глобальных инструментов”.

Настраиваем:

JDK: (Имя: jdk11, JAVA_HOME: $JAVA_HOME )

![JENKINS](src/images/screenshots/jenkins8.png)

Gradle: (name: gradle Версия: Gradle 6.8.3)

![JENKINS](src/images/screenshots/jenkins9.png)

Allure Commandline: ( Имя: allure Версия: последняя)

![JENKINS](src/images/screenshots/jenkins10.png)

#### Jenkins установлен и настроен.


## Устанавливаем Selenoid и Selenoid UI

Открываем Git bash На сервере переходим в папку test-stand командой:
```bash
cd test-stand
```
Пишем команду для остановки контейнера:
```bash
docker-compose down
```

Открываем WinSCP заходим на сервер в папку test-stand открываем docker-compose.yml

![JENKINS](src/images/screenshots/jenkins11.png)

Сохраняем код из файла  <a target="_blank" href="https://github.com/Konyaz/Testing_infrastructure/blob/master/test-stand/docker-compose.yml">docker-compose.yml</a> и вставляем его на сервер в папку test-stand в файл docker-compose.yml для установки Selenoid и Selenoid UI:

  

Сохраняем.




Для того чтоб запаролить Selenoid Ui **(Пароль на Selenoid UI Не одно и тоже что пароль на CREATE SESSION .**

**Пароль на CREATE SESSION (Selenoid) устанавливается через nginx reverse proxy  перед SELENOID либо ставится ggr )**

Заходим на сайт https://hostingcanada.org/htpasswd-generator/

Htpasswd Generator (https://hostingcanada.org/htpasswd-generator/)  - генерируем строку.
В директории c файлом docker-compose.yml создаём файл users.htpasswd

![JENKINS](src/images/screenshots/jenkins11.png)

В созданный файл вставляем сгенерированную строку. Сохраняем.

Открываем Git bash на сервере переходим в папку test-stand командой:

```bash
cd test-stand
```
Пишем команду для запуска контейнеров :
```bash
docker-compose up -d
```



#### Selenoid и Selenoid UI установлены.

## Проверка


##### Проверка Jenkins

Переходим по адресу http://192.168.x.xxx:8888

При верной установке Jenkins, должна отображаться страница авторизации.

![JENKINS](src/images/screenshots/JenkinsCheck.png)


##### Проверка Selenoid

Переходим по адресу http://192.168.x.xxx:4444

При верной установке Selenoid, должна отображаться надпись:

You are using Selenoid x.xx.x!

![SELENOID](src/images/screenshots/SelenoidCheck.png)


##### Проверка Selenoid UI

Переходим по адресу http://192.168.x.xxx:4445

При верной установке Selenoid UI, должна отображаться страница авторизации.

![SELENOID_UI](src/images/screenshots/SelenoidUICheck1.png)

Вводим заданный логин и пароль.

После авторизации Статус SSE и SELENOID должен отображаться зелёным с надписью **CONNECTED**

![SELENOID_UI](src/images/screenshots/SelenoidUICheck2.png)

## Дополнение:

<a target="_blank" href="https://github.com/Konyaz/Testing_infrastructure/blob/master/test-stand/docker-compose%20(Без%20пароля%20Selenoid%20UI).yml">docker-compose (Без пароля Selenoid UI).yml</a>






