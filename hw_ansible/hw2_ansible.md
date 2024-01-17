# Домашнее задание к занятию 2 «Работа с Playbook» - Семикова Т.В. FOPS-9

## Основная часть

1. Подготовьте свой inventory-файл `prod.yml`.
2. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает [vector](https://vector.dev). Конфигурация vector должна деплоиться через template файл jinja2. От вас не требуется использовать все возможности шаблонизатора, просто вставьте стандартный конфиг в template файл. Информация по шаблонам по [ссылке](https://www.dmosk.ru/instruktions.php?object=ansible-nginx-install). не забудьте сделать handler на перезапуск vector в случае изменения конфигурации!
3. При создании tasks рекомендую использовать модули: `get_url`, `template`, `unarchive`, `file`.
4. Tasks должны: скачать дистрибутив нужной версии, выполнить распаковку в выбранную директорию, установить vector.
5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.

Исправила ошибки - убрала лишние пробелы

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/02/img/1.jpg)

6. Попробуйте запустить playbook на этом окружении с флагом `--check`.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/02/img/3.jpg)

7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/02/img/1-1.jpg)
8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/02/img/2.jpg)

9. Подготовьте README.md-файл по своему playbook.

https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/02/playbook/README.md

10. Готовый playbook выложите в свой репозиторий, поставьте тег `08-ansible-02-playbook` на фиксирующий коммит, в ответ предоставьте ссылку на него.

https://github.com/SemikovaTV/hw_ansible/tree/master/hw_ansible/02/playbook

    

---
