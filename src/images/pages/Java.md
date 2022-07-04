

Проверяем наличие Java командой:
```bash
 java --version
```
Если Java не установлена устанавливаем командой:
```bash
sudo apt-get install default-jdk
```

Соглашаемся на установку и потом ждем, пока всё установится.

Ещё раз проверяем версию Java командой:

```bash
 java --version
```

## Прописываем переменную окружения JAVA_HOME

Java вероятнее всего установилась вот так:

/usr/lib/jvm/java-11-openjdk-amd64 в JAVA_HOME <font color="red"> необходимо прописывать именно этот путь, который не включает папку bin. </font> 

Редактируем файл с переменными окружения командой:
```bash
sudo nano /etc/environment
```

Добавляем крайней строчкой  <font color="red">(Строк может быть больше чем одна поэтому ставить нужно крайней строчкой не удаляя и не трогая другие строки):</font>
```bash
JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
```

![JAVA_HOME](/src/images/screenshots/bash.png)


Нажимаем последовательно Ctrl+S (сохранить), Ctrl+X (выйти из редактора nano).

Обновляем сведения о переменных окружения командой:
```bash
source /etc/environment
```
Проверяем, прописалась ли переменная окружения командой:
```bash
echo $JAVA_HOME
```
