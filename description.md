# Описание подхода в работе с кодовой базе проекта

## Проект

Система оценки кредитной истории и инструменты для ее улучшения

## Git flow

Использует Issue Branch Workflow + элементы Gitflow

В проекте присутствуют основные ветки dev и prod, каждая из них собирается в рабочий инстанс. Сборка dev доступна из корпоративной сети, prod смотрит "наружу"

dev служит веткой тестирования, где можно увидеть изменения и внести правки в случае необходимости

prod - ветка production

dev сливается с prod в начале каждой недели, для поддержания актуальности.

Новые фичи/исправления багов создаются в ветках `feature/(номер issue в Jira)` и `fix/(номер issue в Jira)` соответственно. После реализации задачи, эти ветки сливаются в dev.

### Плюсы

- В GitLab можно сразу перейти на задачу в Jira по названию ветки
- Сразу видно, какие задачи являются добавлением функционала, а какие - исправлением ошибки
- Разграничение на ветки dev и prod позволяет оттестировать выполненные задачи в браузере до того, как они попадут "наружу"
- Между dev и prod не возникают merge conflcts

### Минусы

- Поддержание двух инстансов, что означает отдельные конфигурации для каждой из них (переменные окружения, ключи и пр.)
- Огромные merge requests dev -> prod, что не дает возможности провести code review до синхронизации
- Ветки не защищены, что позволяет ввести изменения непосредственно в prod

### Возможные улучшения

- Защитить ветку prod, дать возможность ее изменения исключительно администратору, чтобы разработчик не имел возможности вливать в нее изменения
- Использовать code review, тэгать других разработчиков после реализации задачи и не давать провести МР до него, для проверки друг друга и соблюдения общего code style

### Минусы этих улучшений

- Заливка изменений займет гораздо больше времени и не позволит быстро вливать хотфиксы и ошибки сборки

Ранее в проекте также использовалась ветка test, но от нее быстро отказались, поскольку пришлось поддерживать три разных инстанса и была путаница в файлах конфигурации, где проверять изменения и каков был статус синхронизации. Также это приводило к многим merge conflct'ам.
