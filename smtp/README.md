# Простенький SMTP сервер

1. `sudo docker compose up -d`
2. Зайдите в докер контейнер через `sudo docker exec -it smpt-mail-1 bash` и добавьте вручную юзера через `sudo adduser`, в примере это `vanya`. Мне впадлу разбираться как добавлять юзеров в докере, `useradd` чета не работает, кому не впадлу киньте сюда пр.
3. Проверьте работоспособность через `telnet` например.
```
telnet localhost 25

> EHLO client.example.com
> MAIL FROM: <sender@example.com>
> RCPT TO: <testuser@example.com>
> DATA
> Subject: Test Message
> Hello, this works now!
> .
> QUIT
```