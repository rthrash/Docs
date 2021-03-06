---
title: "Git FAC (Часто используемые команды)"
translation: "contribute/code/git-github/frequent-commands"
---

На этой странице кратко рассматриваются некоторые распространенные сценарии использования Git для разработки MODX.

## Как мне получить и синхронизировать локальную ветку разработки?

Во-первых, вы должны **никогда не выполнять фиксацию напрямую в ветке версии**. Уже одно это сделает работу с git намного приятнее.

Чтобы обновить локальную копию для разработки, например ветку основной версии 2.x, запустите:

``` php
git fetch upstream
git checkout 2.x
Switched to branch "2.x"
git merge --ff-only upstream/2.x
```

Это предполагает, что официальный репозиторий добавлен как «upstream», и что у вас есть форк, добавленный как «origin». [Подробнее о пультах дистанционного управления](<https://git-scm.com/book/en/v2/Git-Basics-Working-with-Remotes>)

## Как мне создать тематическую ветку?

Сначала убедитесь, что ваша локальная копия ветки версии (например, `2.x`) актуальна. См. Предыдущий раздел.

Затем запустите:

``` bash
git checkout -b myFeatureBranchName 2.x
```

## Существует ли соглашение об именах для ветвей функций?

Обычно один из: «issue-1234», «feature-1234» или «fix-1234», где «1234» - это идентификатор соответствующей проблемы на GitHub.

Если нет проблем с тем, над чем вы планируете работать, подумайте о создании этого, чтобы обсудить это, или используйте описательное имя ветки, например `feature-magic-resources`.

Избегайте имен, которые напоминают номера версий выпуска.

``` php
git checkout -b  myAwesomeFeature 2.x
```

Да. Никогда не выполняйте фиксацию непосредственно в ветке версии. Всегда создавайте отдельную ветку для каждой функции или проблемы, над которой вы работаете.

## Как сохранить синхронизацию моей функциональной ветки с ветвью исходной версии?

Хотя заманчиво использовать `git merge` для извлечения изменений из upstream, это добавляет дополнительные избыточные коммиты к вашим изменениям.

Лучше "воспроизвести" ваши коммиты с помощью `git rebase`.

В своей функциональной ветке запустите:

``` bash
git fetch upstream
git rebase upstream/2.x
```

Если вы еще больше отклонились от ветки выпуска, использование интерактивного режима полезно, чтобы помочь вам устранять любые конфликты по очереди.

``` php
git fetch upstream
git rebase 2.x
```

Чтобы узнать больше, вот страница помощи git rebase: <http://www.kernel.org/pub/software/scm/git/docs/git-rebase.html>

## Мне действительно нужно беспокоиться о том, чтобы выбрать правильную (версию) ветку?

Да. Основные интеграторы предпочитают тратить свое время на анализ и принятие значительных вкладов, а не через сложные препятствия и конфликты слияния, чтобы применить ваши изменения к правильной ветви.

[См. Руководство для участников, чтобы узнать, какие ветки использовать](contribute/code/contributors-guide), и спросите в [сообществе Slack](<https://modx.org>) или [форуме](https: // community .modx.com), если вы не уверены, какая ветвь вам подходит.
