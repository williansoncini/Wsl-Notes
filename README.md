# Notas de WSL - Windowns subsystem Linux

Cara já vou deixar algumas coisas aqui armazendas para poupar tempo depois rsrsrs

# Instalação

> Abrir o CMD como administrador

```cmd
wsl --install -d Ubuntu
```

# 'Setar' ip estático

> Precisa de CMD ou powerShell com privilégio de administrador também

Para deixar como estático mesmo, é necessário criar um arquivo .bat ou .ps1 com o código abaixo

```cmd
wsl -d Ubuntu -u root ip addr add 10.0.0.10/24 broadcast 192.168.50.255 dev eth0 label eth0:1
netsh interface ip add address "vEthernet (WSL)" 192.168.50.88 255.255.255.0
```

Coloque esse arquivo no agendador de tarefas, para sempre ser executado no logon.

> Se lembre de setar a opções de 'Executar como provilégios altos' para dar certo

[Fonte dessas informações](https://lifesaver.codes/answer/static-ip-on-wsl-2-418)

# Ssh

## Instalar o SSH

```shell
sudo apt remove openssh-server
sudo apt install openssh-server
```

## Configuração básica

> Editar o arquivo sshd_config 

```shell
sudo vi /etc/ssh/sshd_config
```

- Adicionar 

```shell
PasswordAuthentication yes
AllowUsers yourusername
```

## Subir serviço

```shell
sudo service ssh start
```

## Gerar chave (Caso de erro de chaves)

```shell
ssh-keygen -A
```

## Links uteis

[SSH - Wsl](https://www.illuminiastudios.com/dev-diaries/ssh-on-windows-subsystem-for-linux/)