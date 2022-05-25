# Notas de WSL - Windowns subsystem Linux

Cara já vou deixar algumas coisas aqui armazendas para poupar tempo depois rsrsrs

- [Notas de WSL - Windowns subsystem Linux](#notas-de-wsl---windowns-subsystem-linux)
- [Instalação](#instalação)
- ['Setar' ip estático](#setar-ip-estático)
- [Ssh](#ssh)
  - [Instalar o SSH](#instalar-o-ssh)
  - [Configuração básica](#configuração-básica)
  - [Subir serviço](#subir-serviço)
  - [Gerar chave (Caso de erro de chaves)](#gerar-chave-caso-de-erro-de-chaves)
- [Configuções](#configuções)
  - [Links uteis](#links-uteis)

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
``

## Gerar chave (Caso de erro de chaves)

```shell
ssh-keygen -A
```

# Configuções

É importante configurar corretamente seu WSL senão ele vai torrar sua memória sem dó quando você usar um docker ou coisa do tipo

Essa configução vale para o Windows, então va até `C:/Users/%username%/` e crie o arquivo `.wslconfig`

Dentro do arquivo você pode fazer cofigurações como essas abaixo para não deixar o WSL consumir todos os seus recursos

```py
[wsl2]
memory=20GB # Limits VM memory in WSL 2 
processors=4 # Makes the WSL 2 VM use 4 virtual processors
localhostForwarding=true # Boolean specifying if ports bound to wildcard or localhost in the WSL 2 VM should be connectable from the host via localhost:port.
```

Informações tiradas do link abaixo

https://stackoverflow.com/questions/68706512/how-to-create-a-wslconfig-file

## Links uteis

[SSH - Wsl](https://www.illuminiastudios.com/dev-diaries/ssh-on-windows-subsystem-for-linux/)
