# Настройка ubuntu

## Aliases
```sh
alias l="ls -la --group-directories-first"
alias sai="sudo apt install"
alias sar="sudo apt remove"
alias sau="sudo apt update"
alias sauu="sudo apt update && sudo apt upgrade"
alias pv="python -m venv venv"
alias sv="source /venv/bin/activate"
alias rs="python manage.py runserver"
alias mm="python manage.py makemigrations"
alias mg="python manage.py migrate"
alias d="docker"
alias dc="docker-compose"
alias dcub="docker-compose up --build"
alias dcdv="docker-compose down -v"
alias dcr="docker-compose run"
```


## Установить apt-fast

```sh
sudo add-apt-repository ppa:apt-fast/stable
sudo apt-get update
sudo apt-get install apt-fast
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
- Установить ав2тодополнения
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

sudo apt-get install python3.9-dev python3.9-venv
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

sudo apt install docker-ce
```

Настройка docker без sudo
```sh
sudo gpasswd -a $USER docker
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
## Установить kubernetes

Загрузите последнюю версию с помощью команды:
```sh
curl -LO https://storage.googleapis.com/kubernetes-release/release/`curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt`/bin/linux/amd64/kubectl
```

Сделайте двоичный файл kubectl исполняемым:
```sh
sudo chmod +x ./kubectl
```

Переместите двоичный файл в директорию из переменной окружения PATH:
```sh
sudo mv ./kubectl /usr/local/bin/kubectl
```

Убедитесь, что установлена последняя версия:
```sh
kubectl version --client
```

Установите VirtualBox
```sh
sudo apt install virtualbox
```

Скачать и установить minikube со страницы релизов
```sh
https://github.com/kubernetes/minikube/releases
```

## Kubernetes справка
Загрузить локальный docker image в kuber
```sh
minikube image load image_name
или сразу
minikube image build -t image_name
```

Запустить Docker container в kuber
```sh
k run django --image=<image_name> --env='SECRET_KEY=sdvaihgg' --image-pull-policy='IfNotPresent' --port=8082
```
Если не работает:
```sh
eval $(minikube docker-env)
```



Зайти в pod
```sh
kubectl exec <pod_name> -it -- bash
```

## Установить nala (вместо apt)
```sh
echo "deb http://deb.volian.org/volian/ scar main" | sudo tee /etc/apt/sources.list.d/volian-archive-scar-unstable.list

wget -qO - https://deb.volian.org/volian/scar.key | sudo tee /etc/apt/trusted.gpg.d/volian-archive-scar-unstable.gpg > /dev/null

sudo apt update && sudo apt install nala
```
