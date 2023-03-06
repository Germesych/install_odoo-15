## Установка Odoo 15

Чтобы установить базу данных PostgreSQL в системе Debian/Ubuntu, выполните следующие команды:

`sudo apt update && sudo apt upgrade`

Устанавливаем PostgreSQL: <br>
`sudo apt install postgresql`

Создаем суперпользователя: <br>
`sudo su -c "createuser -s $USER" postgres`

Проверяем статус базы данных: <br>
`systemctl status postgresql`

Если вы используете Ubuntu внутри WSL, обратите внимание, 
что системные службы не запускаются автоматически. Это означает, 
что служба PostgreSQL должна быть запущена вручную, чтобы база данных была доступна. 
Чтобы вручную запустить службу PostgreSQL, выполните следующую команду: <br>
`sudo service postgresql start`

## Каждая Odoo использует свою версию python!!! Перед установкой Odoo надо обязательно проверить версию python!!!
#### в Odoo 15 это python 8.6
### `pyenv` позволяет выбрать необходимую версию как для системы, так и локально.
Установка:<br>
```console
curl https://pyenv.run | bash
```

Если у вас zsh: <br>
```console
curl https://pyenv.run | zsh
```

Посмотреть версии: <br>
```console
pyenv install --list
```

Установка определенной версии: <br>
```console
pyenv install 3.8
```

Посмотреть установленные версии: <br>
```console
pyenv versions
```

Вывод: <br>
`system` #Значит что активирована системная версия <br>
`3.7.10` <br>
`3.8.7` <br>
`3.9.2`

Активировать локально версию (в папке) <br>
```console
pyenv local 3.8.7
```

Активировать глобально для всей системы: <br>
```console
pyenv global 3.8.7
```
<br>
<br>
<br>
### Установка системных зависимостей Odoo
```console
sudo apt update && sudo apt upgrade
```

```console
sudo apt install git`
```

```console
sudo apt install python3-dev python3-pip python3-wheel python3-venv
```

```console
sudo apt install build-essential libpq-dev libxslt-dev libzip-dev libldap2-dev libsasl2-dev libssl-dev
```

### Если вам необходимо работать с Odoo версий до 11, вам также потребуется установить препроцессор CSS less:
```console
sudo apt install npm  # Install Node.js and its package manager
```

```console
sudo ln -s /usr/bin/nodejs /usr/bin/node  # node runs Node.js
```
```console
sudo npm install -g less less-plugin-clean-css  # Install less
```

### Чтобы установить Odoo из исходного кода, мы должны начать с клонирования исходного кода Odoo непосредственно с GitHub:
Создаем рабочую директорию <br>
```console
mkdir ~/work15
```

Переходим в рабочую директорию <br>
```console
cd ~/work15
```

Клонируем odoo-15 c GitHub <br>
```console
git clone https://github.com/odoo/odoo.git -b 15.0 --depth=1
```

Опция -b 15.0 в команде Git явно загружает ветку 15.0 Odoo. На момент написания статьи это излишне, поскольку это ветвь по умолчанию, но это может измениться.

Чтобы создать новую виртуальную среду, выполните следующую команду: <br>
```console
python3 -m venv ~/work15/env15
```

Это создаст среду Python в ~/work15/env15. <br>
Мы хотим запустить весь код Python, используя ~/work15/env15/bin/python. <br>
Данная команда может подтвердить это, показав версию Python, которая была установлена в этом месте: <br>

```console
~/work15/env15/bin/python -V
```
Выведет в консоле: `Python 3.8.10`


Нам будет гораздо удобнее, <br>
если мы установим его в качестве текущего интерпретатора Python по умолчанию. <br>
Этого можно добиться, активировав виртуальную среду: <br>
```console
source ~/work15/env15/bin/activate
```

Мы можем выполнить команду which, чтобы убедиться, <br>
что используется правильный интерпретатор Python: <br>
```console
which python
```
Вывод консоли: `/home/daniel/work15/env15/bin/python`

### Чтобы отключить виртуальную среду, просто выполните команду deactivate; <br> интерпретатор Python и здесь будет использоваться по умолчанию:
```console
deactivate
```

```console
which python3
```
Вывод консоли: `/usr/bin/python`

### Активировав виртуальную среду, мы можем установить в ней зависимости Python:
```console
source ~/work15/env15/bin/activate
```
Вывод консоли станет таким: `(env15) $:` 
```console
pip install -U pip
```

```console
pip install -r ~/work15/odoo/requirements.txt
```

### Однако нам все еще необходимо установить сам Odoo. Для этого вы можете использовать pip:
```console
pip install -e ~/work15/odoo
```

### Запуск Odoo
Активируем: <br>
```console
source ~/work15/env15/bin/activate
```

Запускаем саму Odoo <br>
```console 
odoo
```

### Внутри виртуальной среды просто запустите Odoo, чтобы запустить экземпляр:
```console
odoo --version
```
Вывод терминала: `Odoo Server 15.0`

Порт прослушивания Odoo по умолчанию - `8069`. Чтобы связаться с сервисом Odoo через веб-браузер, мы должны использовать URL http://localhost:8069

Чтобы остановить сервер и вернуться в командную строку, нажмите Ctrl + C.


