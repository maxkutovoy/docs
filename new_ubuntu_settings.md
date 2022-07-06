# Настройка нового сервера

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