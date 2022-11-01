1) Загрузите образ node версии 15.14

*Сделаю в процессе команды run, через pull делал в первом задании*

2) Запустите контейнер с именем first_node из образа node версии 15.14 в фоновом режиме, подключив папку data из текущей директории в /var/first/data контейнера

```
mkdir -p data
docker run --name first_node -d -t -v "$(pwd)/data:/var/first/data" node:15.14
```

*Кстати, сейчас если контейнеру докера не задавать имя, он задаст ему его сам в духе именования версий Убунты*

3) Запустите контейнер с именем second_node из образа node версии 15.14 в фоновом режиме, подключив папку data из текущей директории в /var/second/data контейнера

```
docker run --name second_node -d -t -v "$(pwd)/data:/var/second/data" node:15.14
```

4) Подключитесь к контейнеру first_node с помощью exec и создайте текстовый файл любого содержания в /var/first/data

```
docker exec -it first_node /bin/sh
echo > /var/first/data/test.txt Some content
```

5) Добавьте еще один файл в папку data на хостовой машине

```
exit
echo > data/test12.txt Some content 2
```

6) Подключитесь к контейнеру second_node с помощью exec и получите список файлов в директории /var/second/data, выведете на экран содержимое файлов

```
docker exec -it second_node /bin/sh
cd /var/second/data
ls -la
cat test.txt
cat test1.txt
```

7) Остановите оба контейнера

```
exit
docker stop first_node second_node
```

8) Удалите оба контейнера

```
docker rm first_node second_node
```

9) Удалите образ node версии 15.14

```
docker rmi node:15.14
```
