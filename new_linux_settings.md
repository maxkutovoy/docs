# Настройка ubuntu

## Univrsal Aliases
```sh
alias m="sudo micro"
alias f="fastfetch"
alias textscale="gsettings set org.gnome.desktop.interface text-scaling-factor"
alias l="ls -la --group-directories-first"
```

## Ubuntu Aliases
```sh
alias sai="sudo apt install"
alias sar="sudo apt remove"
alias sau="sudo apt update"
alias sauu="sudo apt update && sudo apt upgrade"
alias saa="sudo apt autoremove"
```

## Fedora Aliases
```sh
alias sdi="sudo dnf install"
alias sdr="sudo dnf remove"
alias sdu="sudo dnf update"
alias sda="sudo dnf autoremove"
```


## Изменить размер иконок Babar

```sh
cd ~/.local/share/gnome-shell/extensions/babar*/schemas

```
В файле
```sh
org.gnome.shell.extensions.babar.gschema.xml
```
Установить icon-size
```sh
	<key name="icon-size" type="i">
			<default>25</default>
		</key>
```
После этого перекомпилировать схемы
```sh
glib-compile-schemas .
```


## Установить apt-fast

```sh
sudo add-apt-repository ppa:apt-fast/stable
sudo apt-get update
sudo apt-get install apt-fast
```

## Установить nala (вместо apt)
```sh
echo "deb http://deb.volian.org/volian/ scar main" | sudo tee /etc/apt/sources.list.d/volian-archive-scar-unstable.list

wget -qO - https://deb.volian.org/volian/scar.key | sudo tee /etc/apt/trusted.gpg.d/volian-archive-scar-unstable.gpg > /dev/null

sudo apt update && sudo apt install nala
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

```sh
git clone https://github.com/zsh-users/zsh-autosuggestions ~/.oh-my-zsh/custom/plugins/zsh-autosuggestions

git clone https://github.com/zsh-users/zsh-syntax-highlighting.git ~/.oh-my-zsh/custom/plugins/zsh-syntax-highlighting
```

- Добавить в плагины (в ~/.zshrc)

```sh
plugins=(zsh-autosuggestions zsh-syntax-highlighting)
```


## Установить Stacer
```sh
sudo add-apt-repository ppa:oguzhaninan/stacer

sudo apt install stacer
```


## Установить SSH server
```sh
sudo apt install openssh-server
```


## Установка и настройка Wireguard
```sh
sudo apt install wireguard resolvconf iptables
```

Копировать wg_config_file в /etc/wireguard
```sh
sudo systemctl start wg-quick@wg_ru.service
или
sudo wg-quick up wg_ru
```

## Изменить тему flatpak
```sh
sudo flatpak override --filesystem=$HOME/.themes

sudo flatpak override --env=GTK_THEME=my-theme
```

для отмены
```sh
sudo flatpak override --reset
```
