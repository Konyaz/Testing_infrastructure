# Установка Docker Compose




Проверяем, есть ли у нас Docker Compose командой:
```bash
docker-compose --version
```
Устанавливаем Docker Compose Скриптом с помощью curl командой:
```bash
sudo curl -SL https://github.com/docker/compose/releases/download/v2.6.1/docker-compose-linux-x86_64 -o /usr/local/bin/docker-compose
```

Проверяем установку Docker Compose командой:
```bash
docker-compose --version
```

[Назад](/README.md)