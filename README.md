# Практическое задание с самопроверкой «Система мониторинга Zabbix» 

### Задание 1
Скриншот авторизации в админке

<img width="1919" height="1079" alt="изображение" src="https://github.com/user-attachments/assets/f71aafe6-2d5e-4ba4-8b8d-a19985846ade" />

Установите и сконфигурируйте Zabbix для выбранной платформы \
a. Зайдите под пользователем root \
Запустите новый сеанс оболочки с правами root. \
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

<img width="886" height="353" alt="изображение" src="https://github.com/user-attachments/assets/352d5022-e629-42ca-a8fb-8833d0d6db40" />


Скриншот раздела Monitoring > Latest data для обоих хостов, где видны поступающие от агентов данные

<img width="1919" height="1079" alt="изображение" src="https://github.com/user-attachments/assets/b8beeb66-0185-4423-90cc-22a606158bd5" />


a. Зайдите под пользователем root \
Запустите новый сеанс оболочки с правами root. \
`$ sudo -s`

b. Установите репозиторий Zabbix \
`wget https://repo.zabbix.com/zabbix/6.0/ubuntu/pool/main/z/zabbix-release/zabbix-release_latest_6.0+ubuntu24.04_all.deb` \
`dpkg -i zabbix-release_latest_6.0+ubuntu24.04_all.deb` \
`apt update` 

c. Установите Zabbix агент \
`apt install zabbix-agent`

d. Запустите процесс Zabbix агента
Запустите процесс Zabbix агента и настройте его запуск при загрузке ОС. \
`systemctl restart zabbix-agent` \
`systemctl enable zabbix-agent`

e. Редактирование конфигурационного файла \
`sudo nano /etc/zabbix/zabbix_agentd.conf` \
Были изменены параметры: Server, ServerActive и Hostname

f. Запуск и добавление агента в автозагрузку \
`sudo systemctl restart zabbix-agent` \
`sudo systemctl enable zabbix-agent`

g. Просмотр логов для проверки работоспособности \
`sudo tail -n 20 /var/log/zabbix/zabbix_agentd.log`
