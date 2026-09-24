# Практическое задание с самопроверкой «Система мониторинга Zabbix» 

### Задание 1
Скриншот авторизации в админке
<img width="1919" height="1079" alt="изображение" src="https://github.com/user-attachments/assets/07bfaeb1-45a5-4e4b-a698-6da122a3bc20" />

Установите и сконфигурируйте Zabbix для выбранной платформы \
a. Зайдите под пользователем root \
Запустите новый сеанс оболочки с правами root.
`$ sudo -s`

b. Установите репозиторий Zabbix \
`wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb` \
`dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb` \
`apt update`

c. Установите Zabbix сервер, веб-интерфейс и агент
`apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent`

d. Создайте базу данных \
Установите и запустите сервер базы данных.
Выполните следующие команды на хосте, где будет располагаться база данных.
`sudo -u postgres createuser --pwprompt zabbix` \
`sudo -u postgres createdb -O zabbix zabbix`

На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль.
`zcat /usr/share/zabbix-sql-scripts/postgresql/server.sql.gz | sudo -u zabbix psql zabbix`

e. Настройте базу данных для Zabbix сервера
Отредактируйте файл `nano /etc/zabbix/zabbix_server.conf`
DBPassword=password

f. Запустите процессы Zabbix сервера и агента
Запустите процессы Zabbix сервера и агента и настройте их запуск при загрузке ОС.
`systemctl restart zabbix-server zabbix-agent apache2` \
`systemctl enable zabbix-server zabbix-agent apache2`

---

### Задание 2
`Приведите ответ в свободной форме........`

1. `Заполните здесь этапы выполнения, если требуется ....`
2. `Заполните здесь этапы выполнения, если требуется ....`
3. `Заполните здесь этапы выполнения, если требуется ....`
4. `Заполните здесь этапы выполнения, если требуется ....`
5. `Заполните здесь этапы выполнения, если требуется ....`
6. 

```
Поле для вставки кода...
....
....
....
....
```

`При необходимости прикрепитe сюда скриншоты
![Название скриншота 2](ссылка на скриншот 2)`
