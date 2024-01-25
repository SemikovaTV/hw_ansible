# Домашнее задание к занятию 3 «Использование Ansible» - Семикова Т.В. FOPS-9

## Основная часть

1. Допишите playbook: нужно сделать ещё один play, который устанавливает и настраивает LightHouse.
2. При создании tasks рекомендую использовать модули: `get_url`, `template`, `yum`, `apt`.
3. Tasks должны: скачать статику LightHouse, установить Nginx или любой другой веб-сервер, настроить его конфиг для открытия LightHouse, запустить веб-сервер.
4. Подготовьте свой inventory-файл `prod.yml`.
5. Запустите `ansible-lint site.yml` и исправьте ошибки, если они есть.
6. Попробуйте запустить playbook на этом окружении с флагом `--check`.

```bash
root@debian:/hw/hw_ansible/03/playbook# ansible-playbook site.yml -i inventory/prod.yml --check

PLAY [Install nginx] **************************************************************************

TASK [Gathering Facts] ************************************************************************
ok: [lighthouse01]

TASK [Nginx-install epel-release] *************************************************************
ok: [lighthouse01]

TASK [Nginx-install] **************************************************************************
ok: [lighthouse01]

TASK [Nginx-create general config file] *******************************************************
ok: [lighthouse01]

PLAY [Install Lighthouse] *********************************************************************

TASK [Gathering Facts] ************************************************************************
ok: [lighthouse01]

TASK [Lighthouse | install dependencies] ******************************************************
ok: [lighthouse01]

TASK [Lighthouse copy from git] ***************************************************************
ok: [lighthouse01]

TASK [Lighthouse create config] ***************************************************************
ok: [lighthouse01]

PLAY [Install Clickhouse] *********************************************************************

TASK [Gathering Facts] ************************************************************************
ok: [clickhouse01]

TASK [Get clickhouse distrib] *****************************************************************
ok: [clickhouse01] => (item=clickhouse-client)
ok: [clickhouse01] => (item=clickhouse-server)
ok: [clickhouse01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] ************************************************************
ok: [clickhouse01]

TASK [Create database] ************************************************************************
skipping: [clickhouse01]

PLAY [Install Vector] *************************************************************************

TASK [Gathering Facts] ************************************************************************
ok: [vector01]

TASK [Get VECTOR] *****************************************************************************
ok: [vector01]

TASK [Install VECTOR] *************************************************************************
ok: [vector01]

TASK [Configure Vector | ensure what directory exists] ****************************************
ok: [vector01]

TASK [Configure Vector | Template config] *****************************************************
ok: [vector01]

PLAY RECAP ************************************************************************************
clickhouse01               : ok=3    changed=0    unreachable=0    failed=0    skipped=1    rescued=0    ignored=0
lighthouse01               : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
vector01                   : ok=5    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

7. Запустите playbook на `prod.yml` окружении с флагом `--diff`. Убедитесь, что изменения на системе произведены.
```bash
root@debian:/hw/hw_ansible/03/playbook# ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install nginx] ************************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [lighthouse01]

TASK [Nginx-install epel-release] ***********************************************************
ok: [lighthouse01]

TASK [Nginx-install] ************************************************************************
ok: [lighthouse01]

TASK [Nginx-create general config file] *****************************************************
ok: [lighthouse01]

PLAY [Install Lighthouse] *******************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [lighthouse01]

TASK [Lighthouse | install dependencies] ****************************************************
ok: [lighthouse01]

TASK [Lighthouse copy from git] *************************************************************
ok: [lighthouse01]

TASK [Lighthouse create config] *************************************************************
ok: [lighthouse01]

PLAY [Install Clickhouse] *******************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [clickhouse01]

TASK [Get clickhouse distrib] ***************************************************************
ok: [clickhouse01] => (item=clickhouse-client)
ok: [clickhouse01] => (item=clickhouse-server)
ok: [clickhouse01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] **********************************************************
ok: [clickhouse01]

TASK [Create database] **********************************************************************
ok: [clickhouse01]

PLAY [Install Vector] ***********************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [vector01]

TASK [Get VECTOR] ***************************************************************************
ok: [vector01]

TASK [Install VECTOR] ***********************************************************************
ok: [vector01]

TASK [Configure Vector | ensure what directory exists] **************************************
changed: [vector01]

TASK [Configure Vector | Template config] ***************************************************
changed: [vector01]

RUNNING HANDLER [Start VECTOR] **************************************************************
changed: [vector01]

PLAY RECAP **********************************************************************************
clickhouse01               : ok=4    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
lighthouse01               : ok=8    changed=0    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
vector01                   : ok=6    changed=3    unreachable=0    failed=0    skipped=0    rescued=0    ignored=0
```

8. Повторно запустите playbook с флагом `--diff` и убедитесь, что playbook идемпотентен.
```bash
root@debian:/hw/hw_ansible/03/playbook# ansible-playbook site.yml -i inventory/prod.yml --diff

PLAY [Install nginx] ************************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [lighthouse01]

TASK [Nginx-install epel-release] ***********************************************************
ok: [lighthouse01]

TASK [Nginx-install] ************************************************************************
ok: [lighthouse01]

TASK [Nginx-create general config file] *****************************************************
ok: [lighthouse01]

PLAY [Install Lighthouse] *******************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [lighthouse01]

TASK [Lighthouse | install dependencies] ****************************************************
ok: [lighthouse01]

TASK [Lighthouse copy from git] *************************************************************
ok: [lighthouse01]

TASK [Lighthouse create config] *************************************************************
ok: [lighthouse01]

PLAY [Install Clickhouse] *******************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [clickhouse01]

TASK [Get clickhouse distrib] ***************************************************************
ok: [clickhouse01] => (item=clickhouse-client)
ok: [clickhouse01] => (item=clickhouse-server)
ok: [clickhouse01] => (item=clickhouse-common-static)

TASK [Install clickhouse packages] **********************************************************
ok: [clickhouse01]

TASK [Create database] **********************************************************************
ok: [clickhouse01]

PLAY [Install Vector] ***********************************************************************

TASK [Gathering Facts] **********************************************************************
ok: [vector01]

TASK [Get VECTOR] ***************************************************************************
ok: [vector01]

TASK [Install VECTOR] ***********************************************************************
ok: [vector01]

TASK [Configure Vector | ensure what directory exists] **************************************
ok: [vector01]

TASK [Configure Vector | Template config] ***************************************************
ok: [vector01]

PLAY RECAP **********************************************************************************
clickhouse01               : ok=4    changed=0    unreachable=0    failed=0    skipped=0    r  escued=0    ignored=0
lighthouse01               : ok=8    changed=0    unreachable=0    failed=0    skipped=0    r  escued=0    ignored=0
vector01                   : ok=5    changed=0    unreachable=0    failed=0    skipped=0    r  escued=0    ignored=0
```

9. Подготовьте README.md-файл по своему playbook. В нём должно быть описано: что делает playbook, какие у него есть параметры и теги.

https://github.com/SemikovaTV/hw_ansible/blob/master/hw_ansible/03/playbook/README.md

10. Готовый playbook выложите в свой репозиторий, поставьте тег `08-ansible-03-yandex` на фиксирующий коммит, в ответ предоставьте ссылку на него.

https://github.com/SemikovaTV/hw_ansible/tree/master/hw_ansible/03/playbook



