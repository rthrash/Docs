---
title: "MySQL 5.0.51"
translation: "getting-started/installation/troubleshooting/mysql-5.0.51"
---

## Почему MODX не поддерживает сервер MySQL версии 5.0.51?

MySQL 5.0.51, включая 5.0.51a, имеет серьезные ошибки с PDO, в частности с операторами группировки, упорядочения и подготовки.

Это вызовет неисправимые ошибки в обычных запросах в MODX, а также в других приложениях с открытым исходным кодом, поэтому MODX не поддерживает установку с установленным MySQL 5.0.51. Пожалуйста, обновите вашу установку MySQL.

## MySQL 5.0.51 список ошибок сервера

Вот лишь некоторые из возникающих ошибок:

- <http://bugs.mysql.com/bug.php?id=32202>
- <http://bugs.php.net/bug.php?id=47655>
- <http://bugs.mysql.com/bug.php?id=36406>
