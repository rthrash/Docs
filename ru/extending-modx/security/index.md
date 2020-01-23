---
title: "Токены и специальные слова"
translation: "extending-modx/services"
---

Как и многие веб-приложения, MODX подписывает запросы, чтобы предотвратить обработку вредоносных запросов. WordPress выполняет это через [nonces](http://codex.wordpress.org/WordPress_Nonces), а MODX использует токены. По умолчанию это поведение происходит только внутри панели управления MODX.

Если вы работаете с пользовательскими страницами менеджера (CMPs), вы можете увидеть следующие значения, включенные в данные post под ключом с именем `HTTP_MODAUTH`:

``` php
$_POST['HTTP_MODAUTH'] => modx12345xxxx.9887_abcdef1234.0987654
```

Это значение связано с пользователем и его текущим контекстом - это может показаться странным, но учтите, что сеансы также связаны с "пользователем" (даже если пользователь не вошел в систему), и вы можете начать понимать, почему соответствующий код находится в классе modUser, но поведение по умолчанию здесь заключается в том, что токены и их проверка применимы только к пользователю, который вошел в систему.

Например, вот как можно протестировать форму, которая была отправлена откуда-то из менеджера.

``` php
$token = $modx->getOption('HTTP_MODAUTH', $_POST);
if ($token != $modx->user->getUserToken($modx->context->get('key')) {
    // ERROR! Invalid request
}
```

Воссоздание этого типа безопасности на интерфейсе вашего сайта может быть немного сложнее, так как функции MODX доступны только аутентифицированному пользователю.

## Различия между Nonce и токеном

Nonce делает форму действительной в течение определенного периода времени, скажем 30 минут, после чего она больше не может быть успешно отправлена. В идеальном мире у вас были бы "одноразовые" формы, где каждая форма была бы уникально подписана и могла быть представлена только _once_. Но эта модель безопасности быстро ломается в реальном мире, где вам, возможно, придется использовать кнопку "назад", если время загрузки страницы истекает, поэтому nonce обычно настраиваются так, чтобы быть действительными в течение определенного периода времени: чем короче окно, тем более безопасным является nonce.

Токены, используемые менеджером MODX, связаны с сеансами, поэтому, пока вы вошли в систему (т.е. ваш сеанс истек), вы можете делать с формами все, что хотите.

### Пример

Допустим, мы загружаем форму менеджера, затем выходим, выполняем поручения и возвращаемся через 12 часов. Если форма была подписана с помощью nonce, вы можете отправить форму, но это, вероятно, не удастся, потому что nonce обычно имеют более короткие сроки службы. Если форма была подписана с помощью токена, вы можете _вероятно_ все еще отправить ее, потому что ваш сеанс, вероятно, все еще хорош (сеансы часто имеют 24-часовой срок службы).