

•	Задайте имя компьютера CLI,
Делается во время установки
•	При установке укажите имена пользователь user с паролем resu, и пользователь root с паролем toor,
User -обычный пользователь
Toor- администратор
•	IP адрес вам приход от провайдера по DHCP,
DHCP- получать адрес автоматически. IP прописывать не надо



Пока устанавливается операционная система на CLI перейдём к настройке SRV

•	На SRV необходимо сделать следующие настройки: 
Текущие учетные данные пользователь user с паролем resu, и пользователь root с паролем toor.
•	Настройте следующий IP адрес 10.11.12.10 с маской 255.255.255.0 (24) шлюз по умолчанию 10.11.12.1 и DNS сервер 10.11.12.1

IP
vim /etc/net/ifaces/ens33/ipv4address	Я
Записываем: 10.11.12.10/24

ШЛЮЗ
vim /etc/net/ifaces/ens33/ipv4route
Записываем default via 10.11.12.1

DNS
vim /etc/net/ifaces/ens33/resolv.conf
Записываем nameserver 10.11.12.1

Настройки
vim /etc/net/ifaces/ens33/options
Меняем dhsp -> static

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
systemctl restart network

	
•	Проверьте связность между SRV и CLI, а так же доступность в интернет.
Запустить команду ping по ip адресу CLI

•	Проведите обновление системы.
apt-get update && apt-get dist-upgrade && update-kernel

•	Задайте имя компьютера SRV. 
vim /etc/hostname


•	Поменяйте пароль пользователю user на P@ssw0rd.
passwd user


•	Подключите созданную NFS шару с сервера 10.11.12.1. Она должна автоматический монтироваться по пути /mnt/nfsshare.
Делаем папку
mkdir /mnt/nfsshare

Записываешь в файл
vim /etc/fstab

Адрес роут   папка роут    папка с сервера
10.11.12.1:/mysharedir /mnt/nfsshare

Монтируем шару
  Адрес роут        папка рутер  папка сервера
mount 10.11.12.1:/mysharedir /mnt/nfsshare


•	Настройте подключение по SSH для удалённого конфигурирования устройства.
В поисковик вбиваем установка ssh alt linux , на яндекс дзене.
apt-get update;
apt-get install openssh-server

!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
systemctl enable sshd.service


Откроем на сервере файл 
vim /etc/openssh/sshd_config

В нем раскомментировать 2 строки:
# Authentication:
#LoginGraceTime 2m
PermitRootLogin yes
# To disable tunneled clear text passwords, change to no here!
PasswordAuthentication yes

Сохранить правки - перезапустить сервис ssh.
!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!!
systemctl enable sshd.service

systemctl restart sshd.service
•	Необходимо поставить сервер для игры «CS 1.6» выбор пути установки на ваш выбор но мы рекомендуем поставить через docker.
Устанавливаем docker
apt-get install docker-ce
apt-get install docker-engine
systemctl enable --now docker
Запускаем docker
docker run --rm -it alt
Запуск docker демон
apt-get install docker-engine-rootless
Ищем пакет на github для  cs 1.6
Вбиваем в поисковик cajuclc cs 1.6

•	Установите хранилище данных nextcloud.
•	Настройте пользователя USER_RESU с паролем P@ssw0rd для доступа с клиентского компьютера

# apt-get install deploy
# deploy nextcloud
ПАРОЛЬ ДЛЯ АДМИНСКОГО ВХОДА
# journalctl -b |grep admin-pass
deploy nextcloud password=5Z4SAq2U28rWyVz

Смотрим и ищем пароль
Заходим на сайт
http://localhost/nextcloud

•	Установите Web-интерфейс Алтератор для управления сервером с CLI.
apt-get install alterator-fbi
service alteratord start; service ahttpd start
ЗАХОДИМ НА САЙТ
 https://localhost:8080/












•	Настройка клиентского компьютера:
•	Проведите обновление системы.

apt-get update && apt-get dist-upgrade && update-kernel


•	Создайте пользователя user2 с паролем P@ssw0rd.

useradd -p P@ssw0rd user2

•	Установите Яндекс браузер.
apt-get install yandex-browser-stable
•	Настройте блокировщик рекламы для работы с Яндекс браузером
В Яндекс браузере- Настройки- Инструменты
•	Подключитесь к nextcloud и сохраните учётные данные для входа.
Перейти на сайт http://localhost/nextcloud

•	Установите хранилище данных nextcloud.
•	Настройте пользователя USER_RESU с паролем P@ssw0rd для доступа с клиентского компьютера
Пуск- Центр Приложений
# apt-get install deploy
# deploy nextcloud
Заходим на сайт
http://localhost/nextcloud
Логин: USER_RESU
Пароль: P@ssw0rd

Установите антивирус Kaspersky.
Вбиваете в поисковик, ищем сайт Red soft
cd /home/user/Загрузки/
скачиваем пакет rpm
apt-get install kesl-11.3.0-7441.x86_64.rpm
идем по инструкции
Скачиваем пакет для граф установки
apt-get install kesl-gui-11.3.0-7441.x86_64.rpm
Настраиваем доступ админа
sudo -E kesl-control --grant-role admin user
•	Настройте расписание сканирование системы.
•	Проверить работоспособность антивируса с помощью программы eicar.
Создаем файл «eicar.com»
Записать в него
X5O!P%@AP[4\PZX54(P^)7CC)7}$EICAR-STANDARD-ANTIVIRUS-TEST-FILE!$H+H*


•	Установите Telegram (они должны запускается, но не авторизовывайтесь)
apt-get install telegram-desktop

•	Установите Steam (они должны запускается, но не авторизовывайтесь)
apt-get install i586-steam

•	Установите игру «CS 1.6» (установочный файл запрашиваете у экспертов) используя программное обеспечение «Play on Linux» и программное обеспечение wine (их тоже необходимо установить)
apt-get install wine-full i586-wine
apt-get install eepm
epm play i586-fix
apt-get install playonlinux
•	После установки запустите игру и подключитесь к своему серверу 
