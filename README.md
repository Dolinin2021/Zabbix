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

c. Установите Zabbix сервер, веб-интерфейс и агент \
`apt install zabbix-server-pgsql zabbix-frontend-php php8.3-pgsql zabbix-apache-conf zabbix-sql-scripts zabbix-agent`

d. Создайте базу данных \
Установите и запустите сервер базы данных. \
Выполните следующие команды на хосте, где будет располагаться база данных. \
`sudo -u postgres createuser --pwprompt zabbix` \
`sudo -u postgres createdb -O zabbix zabbix`

На хосте Zabbix сервера импортируйте начальную схему и данные. Вам будет предложено ввести недавно созданный пароль. \
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
Скриншот раздела Configuration > Hosts, где видно, что агенты подключены к серверу

<img width="1919" height="1079" alt="изображение" src="https://github.com/user-attachments/assets/79c45125-d20f-4f4c-903d-4c59b56ad744" />


Скриншот лога zabbix agent, где видно, что он работает с сервером

<img width="920" height="355" alt="изображение" src="https://github.com/user-attachments/assets/dba98187-5b48-4ed9-8d36-715615624c34" />


Скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные

<img width="1919" height="1079" alt="изображение" src="https://github.com/user-attachments/assets/b8beeb66-0185-4423-90cc-22a606158bd5" />


a. Зайдите под пользователем root \
Запустите новый сеанс оболочки с правами root. \
`$ sudo -s`

b. Установите репозиторий Zabbix \
`wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb` \
`dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb` \
`apt update` \

c. Установите Zabbix агент \
`apt install zabbix-agent` \

d. Запустите процесс Zabbix агента
Запустите процесс Zabbix агента и настройте его запуск при загрузке ОС.
`systemctl restart zabbix-agent
systemctl enable zabbix-agent`
