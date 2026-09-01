---
title: Руководство по установке прокси-сервера VLESS Reality
type: docs
---

## Введение в VLESS

[VLESS](https://en.wikipedia.org/wiki/V2Ray) — это лёгкий прокси-протокол, разработанный проектом [V2Ray](https://en.wikipedia.org/wiki/V2Ray). Он является упрощённой версией протокола VMess.  
VLESS имеет более простую структуру, меньшую вычислительную нагрузку и использует транспортный уровень (например, TLS) для обеспечения шифрования.  
Он работает быстрее, потребляет меньше ресурсов процессора и поддерживает различные способы передачи данных, включая [TCP](https://en.wikipedia.org/wiki/Transmission_Control_Protocol), mKCP, WebSocket, HTTP/2, gRPC и другие.  
Часто используется вместе с TLS для обеспечения безопасности и поддерживает механизм fallback, что позволяет маскироваться под обычный сайт.  

Почти все прокси-клиенты поддерживают VLESS, например:  
[v2rayNG](https://getfreevpn.info/zh/docs/vpn%E6%95%99%E7%A8%8B/%E4%B8%8B%E8%BD%BD%E5%92%8C%E4%BD%BF%E7%94%A8v2rayNG-VPN/),  
[v2box](https://v2box.pro/ru),  
[hiddify](https://hiddify.me/ru),  
[karing](https://karing.biz/ru),  
[sing-box](https://sing-box.info/ru),  
[shadowrocket](https://shadowrocket.ink/ru) и [stash](https://apps.apple.com/us/app/stash-rule-based-proxy/id1596063349).

---

## Процесс установки прокси-сервера VLESS Reality

### 1. VPS — Виртуальный сервер

Сначала вам нужно приобрести VPS (виртуальный сервер). Подойдут серверы, расположенные в таких странах, как Тайвань, США, Япония или Гонконг.  
Как правило, чем ближе сервер к вашей стране, тем выше скорость соединения.  
Ниже приведены несколько недорогих провайдеров VPS:

| Название | CPU | RAM | Диск | Трафик | Промокод | Цена |
|-----------|-----|-----|------|---------|----------|------|
| racknerd | 1ядра | 1ГБ | 24ГБ | 2ТБ |  | [11.29 USD/год](https://my.racknerd.com/index.php?rp=/store/new-year-specials&aff=6665) |
| hostdare | 1ядра | 1.5ГБ | 10ГБ | 1ТБ | DEAL50 | [12.99 USD/год](https://bill.hostdare.com/aff.php?aff=3766&pid=113) |
| cloudcone | 2 ядра | 2ГБ | 27ГБ | 2ТБ |  | [13.9 USD/год](https://app.cloudcone.com.cn/vps/435/create?ref=11035&token=halloween-25-fs-ssd-vps-2) |
| rarecloud | 1 ядро | 768М | 15ГБ | 1ТБ | SNOWMICRO1072 | [10.72 USD/год](https://rarecloud.io/clients/aff.php?aff=738&pid=16) |

---

### 2. Покупка VPS

[Возьмём **rarecloud** в качестве примера](https://rarecloud.io/kvm-vps/?aff=738). Он поддерживает оплату через Alipay.  
Используйте предоставленный промокод и выполните следующие шаги:
- Нажмите в правом верхнем углу и выберите язык интерфейса.
- В разделе системы выберите **debian-12**, регион — **Япония** или **Румыния**.

![vless-1003.jpg](https://vless.app/img/vless-1003.jpg)

После ввода промокода вы увидите обновлённую цену:

![vless-1003.jpg](https://vless.app/img/vless-1001.jpg)

На странице оплаты можно выбрать способ оплаты: **PayPal**, **Alipay**, **банковская карта**.

![vless-1003.jpg](https://vless.app/img/vless-1002.jpg)

---

### 3. Подключение к VPS

После успешной оплаты вы получите письмо на email с **IP-адресом** и **паролем** для входа.

![vless-1003.jpg](https://vless.app/img/vless-1004.jpg)

Загрузите программу для подключения к серверу:  
[Скачать FinalShell](https://dl.hostbuf.com/finalshell3/finalshell_windows_x64.exe)  
[Официальный сайт FinalShell](https://www.hostbuf.com/t/988.html)

После установки:
1. Откройте FinalShell → нажмите на иконку папки → появится всплывающее окно.  
2. Нажмите на иконку в левом верхнем углу.  
3. Выберите тип соединения **SSH (Linux)**.

![vless-1003.jpg](https://vless.app/img/vless-1005.jpg)

Вводим данные:
- Имя: любое
- Хост: IP из письма
- Пользователь: `root`
- Пароль: из письма  
Затем нажмите **OK**, чтобы подключиться.

![vless-1003.jpg](https://vless.app/img/vless-1006.jpg)

После подключения вы увидите примерно такой интерфейс:

![vless-1007.jpg](https://vless.app/img/vless-1007.jpg)

---

### 4. Покупка домена

1. Перейдите на сайт [https://porkbun.com/](https://porkbun.com/)  
2. Зарегистрируйте аккаунт, войдите и откройте **Domain Management**  

![vless-1008.jpg](https://vless.app/img/vless-1008.jpg)

3. Найдите и купите подходящее доменное имя (оплата через Alipay).  
4. После успешной оплаты настройте DNS-записи:

![vless-10091.jpg](https://vless.app/img/vless-10091.jpg)

- В поле **1** введите имя поддомена, например `3xui`.  
- В поле **2** — IP-адрес вашего VPS.  
- Нажмите **Add**.

![vless-10092.jpg](https://vless.app/img/vless-10092.jpg)

---

### 5. Установка 3x-ui

Подключитесь к VPS через FinalShell и выполните команды:

```

apt install curl

```

![vless-10093.jpg](https://vless.app/img/vless-10093.jpg)

```

VERSION=v2.5.5 && bash <(curl -Ls "[https://raw.githubusercontent.com/mhsanaei/3x-ui/$VERSION/install.sh](https://raw.githubusercontent.com/mhsanaei/3x-ui/$VERSION/install.sh)") $VERSION

```

Нажмите **Enter**, когда появится запрос.

![vless-10094.jpg](https://vless.app/img/vless-10094.jpg)

После завершения установки сохраните логин, пароль и URL:

![vless-10095.jpg](https://vless.app/img/vless-10095.jpg)

---

### 6. Получение SSL-сертификата

Выполните команды:

```

apt install certbot python3-certbot-nginx

```
```

certbot --nginx -d 3xui.ваш_домен

```

> Например, если ваш домен `nihao.com`, команда будет:  
> `certbot --nginx -d 3xui.nihao.com`

Результат покажет **публичный** и **приватный** ключи:

![vless-10097.jpg](https://vless.app/img/vless-10097.jpg)

---

### 7. Настройка 3x-ui

1. Откройте URL из письма, введите логин и пароль.  
2. Перейдите в настройки панели, вставьте публичный и приватный ключи.  
3. Нажмите **Сохранить**, затем **Перезапустить панель**.

![vless-10099.jpg](https://vless.app/img/vless-10099.jpg)

Теперь замените IP в старом URL на свой поддомен:  
Например:  
`http://3xui.vless.app:52983/TkH2Qe01Bore3k0`

Зайдите в панель, выберите **Inbound List → Add Inbound**, настройте Reality и создайте новый узел.

![vless-100995.jpg](https://vless.app/img/vless-100995.jpg)

Скопируйте ссылку или QR-код — узел готов.

```

vless://931884c4-[494f-4f35-ae55-10ae38f3da95@bjly.mene.lol](mailto:494f-4f35-ae55-10ae38f3da95@bjly.mene.lol):53518?encryption=none&flow=xtls-rprx-vision&security=reality&sni=tesla.com&fp=random&pbk=zFZlzd84FwymBun_YXSLNNz83vGJnUGi_34doZWr3Ac&sid=b83ffb&spx=%2F&type=tcp&headerType=none#Прокси--rea--Client001%20-%20Cloned-200G

```

---

### 8、Рекомендуемые VPN-провайдеры

* Ниже перечисленные сервисы работают по модели оплаты за трафик. На их сайтах есть инструкции по установке и использованию программного обеспечения.
* После покупки трафика срок действия не ограничен — он действителен до полного расходования.
* Если сайт недоступен, скорее всего он заблокирован — просто выберите другой сервис.

| Название | Цена | Трафик | Узлы |
| :--- | :--- | :--- | :--- |
| [Моцзе](https://1.jnk.ink/L4q20S) | 1 ¥ | 1 ГБ | 30 |
| [Ванцзи Экспресс](https://wjkc66.vip?c=REZUOC) | 7 ¥ | 20 ГБ | 54 |
| [Нюби](https://1.jnk.ink/LYet7x) | 14 ¥ | 200 ГБ | 31 |
| [Фэйту](https://1.jnk.ink/bbXkiN) | 30 ¥ | 100 ГБ | 80 |
| [Нунфу Спринг](https://1.jnk.ink/i1fXTMYk) | 45 ¥ | 200 ГБ | 40 |
| [Баобэй Клауд](https://1.jnk.ink/xxPwfy) | 55 ¥ | 600 ГБ | 64 |
| [Фридом Кэт](https://1.jnk.ink/haO8Dr) | 89 ¥ | 200 ГБ | 71 |
| [fscloud](https://1.jnk.ink/nKXcqQ) | 99 ¥ | 1000 ГБ | 82 |

---

Для инструкций по импорту узлов:
- [Настройка v2rayNG на Android](https://v2rayng.4566.lol/ru)
- [Настройка Shadowrocket на iOS](https://shadowrocket.4566.lol/ru)

📧 По всем вопросам: [leeulen60@gmail.com](mailto:leeulen60@gmail.com)

