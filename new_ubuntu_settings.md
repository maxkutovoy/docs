# Настройка нового сервера

## Aliases
```sh
alias l="ls -la --group-directories-first"
alias sai="sudo apt install"
alias sar="sudo apt remove"
alias suu="sudo apt update"
alias suuu="sudo apt update && sudo apt upgrade"
alias pv="python -m venv venv"
alias sv="source /venv/bin/activate"
alias d="docker"
alias dc="docker-compose"
alias rs="python manage.py runserver"
alias mm="python manage.py makemigrations"
alias mg="python manage.py migrate"
```

## Использовать Nemo по умолчанию
```sh
sudo apt install nemo

xdg-mime default nemo.desktop inode/directory application/x-gnome-saved-search

gsettings set org.gnome.desktop.background show-desktop-icons false

gsettings set org.nemo.desktop show-desktop-icons true
```

Поменять терминал для Nemo:
```sh
gsettings set org.cinnamon.desktop.default-applications.terminal exec 'TERMINAL'
```

Откатить если все сломалось:
```sh
xdg-mime default nautilus.desktop inode/directory application/x-gnome-saved-search

gsettings set org.gnome.desktop.background show-desktop-icons true
```

## Настройка micro

- Установить micro и зависимости:

```sh
sudo apt install micro xauth xclip
```

- Изменить строчку в файле `/etc/ssh/sshd_config`:

```sh
  #AddressFamily any to AddressFamily inet
```

- Открыть файл конфигурации /home/USER/.config/micro/settings.json и установить следующую опцию:

```sh
    "useprimary": false
```

чтобы разрешить вставку символов в PRIMARY буфер только если нажато Ctrl+C.

- Подключиться к ssh с параметром -X


## Zsh

- Установть zsh

```sh
sudo apt install zsh
```
- Установить O-my-zsh
```sh
sh -c "$(curl -fsSL https://raw.github.com/ohmyzsh/ohmyzsh/master/tools/install.sh)"
```
- Установить автодополнения
```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.zsh/zsh-autosuggestions
```

- Установить подсветку синтаксиса
```sh
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ${ZSH_CUSTOM:-~/.oh-my-zsh/custom}/plugins/zsh-syntax-highlighting
```

- Добавить в плагины (в ~/.zshrc)

```sh
plugins=(
    # other plugins...
    zsh-autosuggestions
    zsh-syntax-highlighting
)
```

- Если выскакивает ошибка `zsh-autosuggestions not found`
```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions
sudo rm -r /home/USER/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
source ~/.zshrc
```


## Установить Python 3.9.*

```sh
sudo add-apt-repository ppa:deadsnakes/ppa

sudo apt install python3.9

sudo update-alternatives --install /usr/bin/python python /usr/bin/python3.9 1

apt-get install python3.9-dev python3.9-venv
```

## Установить apt-fast

```sh
sudo add-apt-repository ppa:apt-fast/stable
sudo apt-get update
sudo apt-get install apt-fast
```

## Установить Postgres

```sh
sudo apt install postgresql postgresql-contrib

sudo -i -u postgres
```

## Установить Docker и docker-compose
```sh
sudo apt install apt-transport-https ca-certificates curl software-properties-common

curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu focal stable"

apt-cache policy docker-ce
```

Настройка docker без sudo
```sh
sudo usermod -aG docker ${USER}

su - ${USER}

sudo usermod -aG docker username
```

Docker-compose:
! Поменять версию на [актуальную](https://github.com/docker/compose/releases)
```sh
sudo curl -L "https://github.com/docker/compose/releases/download/2.6.1/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

sudo chmod +x /usr/local/bin/docker-compose

docker-compose --version
```
