# Домашнее задание к занятию 5 «Тестирование roles»

## Подготовка к выполнению

1. Установите molecule: `pip3 install "molecule==3.5.2"` и драйвера `pip3 install molecule_docker molecule_podman`.
2. Выполните `docker pull aragast/netology:latest` —  это образ с podman, tox и несколькими пайтонами (3.7 и 3.9) внутри.

## Основная часть

Ваша цель — настроить тестирование ваших ролей. 

Задача — сделать сценарии тестирования для vector. 

Ожидаемый результат — все сценарии успешно проходят тестирование ролей.

### Molecule

1. Запустите  `molecule test -s centos_7` внутри корневой директории clickhouse-role, посмотрите на вывод команды. Данная команда может отработать с ошибками, это нормально. Наша цель - посмотреть как другие в реальном мире используют молекулу.

#### Ответ
![1 task](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/c9ba7050-9603-4d08-b18b-15073397f8dc)

2. Перейдите в каталог с ролью vector-role и создайте сценарий тестирования по умолчанию при помощи `molecule init scenario --driver-name docker`.

#### Ответ
![2 task](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/a73e57c1-c75c-4d1e-9975-5ca6569e6bfb)

3. Добавьте несколько разных дистрибутивов (centos:8, ubuntu:latest) для инстансов и протестируйте роль, исправьте найденные ошибки, если они есть.

#### Ответ
![3-2 task ](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/50b0088d-a874-4d4c-9cf9-d0937770f4ff)

#### Проверка
#### centos7_lite
![3 task ](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/45f0c842-85d8-4a2f-a754-b73d3c3f0b09)
![3-1 task ](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/bcb9374f-2557-4a3d-b822-facc977819ad)

#### ubuntu:latest
![3-4 task ](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/f925d976-7833-42a7-af5b-eafc695a0791)

4. Добавьте несколько assert в verify.yml-файл для  проверки работоспособности vector-role (проверка, что конфиг валидный, проверка успешности запуска и др.). 

#### Ответ

#### verify.yml
![verify-yml](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/02dc6893-67a1-4366-96a4-2dea6344eb5f)

5. Запустите тестирование роли повторно и проверьте, что оно прошло успешно.

#### Ответ
#### centos7_lite
![4 task](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/defd5e3a-4bb2-4f04-a90f-e4a6a4312fa7)

#### ubuntu:latest
![4-1 task](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/53b74079-4809-48ad-a653-99b02a82a62e)

6. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.
#### Ответ


### Tox

1. Добавьте в директорию с vector-role файлы из [директории](./example).

#### Ответ
Добавил и поробовал сразу запустить без докера, не пошло, надо быдо добавить python версии
![3 task](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/9d532cf0-ab7f-4a1b-be39-fe0645a31547)

2. Запустите `docker run --privileged=True -v <path_to_repo>:/opt/vector-role -w /opt/vector-role -it aragast/netology:latest /bin/bash`, где path_to_repo — путь до корня репозитория с vector-role на вашей файловой системе.

#### Ответ


3. Внутри контейнера выполните команду `tox`, посмотрите на вывод.
Команда отработала с ошибкой, видимо из-за того что настройки сценария были неверные
![2-3-1 tox](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/4b3ea59e-db1a-4c5d-87ac-55e40dedd6de)

#### Ответ

4. Создайте облегчённый сценарий для `molecule` с драйвером `molecule_podman`. Проверьте его на исполнимость.

#### Ответ
![4 task molscen](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/10263e7a-0910-4c07-bdf8-c4132e292ba1)

5. Пропишите правильную команду в `tox.ini`, чтобы запускался облегчённый сценарий.

#### Ответ

![5](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/38bb89c0-09b6-458a-a270-0b84254f4292)

![3 -1task](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/0cee55f7-47b1-431e-a8d8-e85681eb40ea)

6. Запустите 
команду `tox`. Убедитесь, что всё отработало успешно.

![5 test 37jpg](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/60a38cd0-d1ab-4db2-98c1-4378aada758c)

#### Ответ

7. Добавьте новый тег на коммит с рабочим сценарием в соответствии с семантическим версионированием.

#### Ответ

После выполнения у вас должно получится два сценария molecule и один tox.ini файл в репозитории. Не забудьте указать в ответе теги решений Tox и Molecule заданий. В качестве решения пришлите ссылку на  ваш репозиторий и скриншоты этапов выполнения задания. 

#### Попробовал на виртуалке просто установить tox  и прогнать, получилось только проверить на текущей конфигурации python 310  и ansible2.12
![mytox](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/8809a162-4b35-4c13-8d69-69a83968dc50)

![tox - reqtxti](https://github.com/ALEMOLOKOV/8.5_testing_roles_Aleksandr_Molokov/assets/109212419/93741e7e-9583-4042-938e-e98efdd5c9ff)








