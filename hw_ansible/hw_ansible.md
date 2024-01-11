# Домашнее задание к занятию 1 «Введение в Ansible» - Семикова Т.В. FOPS-9

## Подготовка к выполнению

1. Установите Ansible версии 2.10 или выше.
2. Создайте свой публичный репозиторий на GitHub с произвольным именем.
3. Скачайте [Playbook](./playbook/) из репозитория с домашним заданием и перенесите его в свой репозиторий.

## Основная часть

1. Попробуйте запустить playbook на окружении из `test.yml`, зафиксируйте значение, которое имеет факт `some_fact` для указанного хоста при выполнении playbook.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/1.jpg)

2. Найдите файл с переменными (group_vars), в котором задаётся найденное в первом пункте значение, и поменяйте его на `all default fact`.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/2.jpg)
  
3. Воспользуйтесь подготовленным (используется `docker`) или создайте собственное окружение для проведения дальнейших испытаний.
4. Проведите запуск playbook на окружении из `prod.yml`. Зафиксируйте полученные значения `some_fact` для каждого из `managed host`.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/3.jpg)
   
5. Добавьте факты в `group_vars` каждой из групп хостов так, чтобы для `some_fact` получились значения: для `deb` — `deb default fact`, для `el` — `el default fact`.
6.  Повторите запуск playbook на окружении `prod.yml`. Убедитесь, что выдаются корректные значения для всех хостов.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/5.jpg)

7. При помощи `ansible-vault` зашифруйте факты в `group_vars/deb` и `group_vars/el` с паролем `netology`.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/6.jpg)

8. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь в работоспособности.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/7.jpg)

9. Посмотрите при помощи `ansible-doc` список плагинов для подключения. Выберите подходящий для работы на `control node`.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/4.jpg)

10. В `prod.yml` добавьте новую группу хостов с именем  `local`, в ней разместите localhost с необходимым типом подключения.
11. Запустите playbook на окружении `prod.yml`. При запуске `ansible` должен запросить у вас пароль. Убедитесь, что факты `some_fact` для каждого из хостов определены из верных `group_vars`.

![ad](https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/img/8.jpg)
