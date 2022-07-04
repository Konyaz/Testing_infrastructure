
#   Установка Java

1. Проверяем наличие Java командой:
```bash
 java --version
```
2. Если Java не установлена устанавливаем командой:
```bash
sudo apt-get install default-jdk
```

3. Соглашаемся на установку и потом ждем, пока всё установится.

4. Ещё раз проверяем версию Java командой:

```bash
 java --version
```

## Прописываем переменную окружения JAVA_HOME

- Java вероятнее всего установилась вот так:

/usr/lib/jvm/java-11-openjdk-amd64 в JAVA_HOME  ***необходимо прописывать именно этот путь, который не включает папку bin.***

1. Редактируем файл с переменными окружения командой:
```bash
sudo nano /etc/environment
```

2. Добавляем крайней строчкой ***(Строк может быть больше чем одна поэтому ставить нужно крайней строчкой не удаляя и не трогая другие строки)***

```bash
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

![JAVA_HOME](/src/images/screenshots/bash.png)


3. Нажимаем последовательно Ctrl+S (сохранить), Ctrl+X (выйти из редактора nano).

4. Обновляем сведения о переменных окружения командой:
```bash
source /etc/environment
```
5. Проверяем, прописалась ли переменная окружения командой:
```bash
echo $JAVA_HOME
```




<a target="_blank" href="https://github.com/Konyaz/Testing_infrastructure/blob/master/README.md#установка-docker">Назад</a>