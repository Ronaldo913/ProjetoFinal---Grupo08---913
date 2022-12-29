# Implementação DNS Master

## 1 - Login

Primeiro, vamos entrar no usuário su redes: 

```login: su redes``` 

```senha: admin@Lab92```

Após, vamos iniciar um perfil de configuração one-shot. Para isso, digitamos o comando:

```openvpn3 sessão-início --config vpn913.labredes```

E então, vamos fazer o ssh:

```ssh administrador@10.9.13.130```

<img src="/IMG/f1.png" width=600/>

## 2 - Instalação

Agora vamos instalar o BIND9.
O BIND( é a aplicação de DNS que roda no servidor. Vamos instalá-lo via apt-get com o comando:

```sudo apt-get install bind9 dnsutils bind9-doc```

<img src="/IMG/f2.png" width=600/>

Logo depois, vamos verificar o status com o comando:

```sudo systemctl status bind9```

<img src="/IMG/f3.png" width=600/>

Se estiver tudo correto como na imagem acima, não é necessário digitar o comando:

```sudo systemctl enable bind9```

Então damos um ```ls /etc/bind``` para verificar se temos a pasta ``zones``:

<img src="/IMG/f4.png" width=600/>

Como na imagem acima, não temos a pasta zones, então vamos criá-la com:

```sudo mkdir /etc/bind/zones```

<img src="/IMG/f5.png" width=600/>

Verificando agora:

<img src="/IMG/f5-1.png" width=600/>

### 2.1 - Zonas

Bem, agora, depois da pasta criada, vamos para as instalações da zona. 
As zonas são especificadas em arquivos db. Vamos criar um diretório para armazendar os arquivos de zonas, que sera o diretório /etc/bind/zones

#### 2.1.1 - Zona direta

o arquivo db.labredes.ifalarapiraca.local conterá os nomes das máquinas do domínio labredes.ifalarapiraca.local
Aqui vamos criar o arquivo de zona direta com o comando:

```sudo cp /etc/bind/db.empty /etc/bind/zones/db.grupox.turmaxxx.ifalara.local ```

Lembrando: o arquivo db tem que ter as informações do grupo. Logo, nesse caso ficou:

<img src="/IMG/f6.png" width=600/>

#### 2.1.2 - Zona reversa

- Utilizado quando não se conhece o IP mas sabe-se o nome do host.
- vamos criar a zona reversa a partir do arquivo /etc/bind/db.127

Dessa vez utilizamos o comando:

```sudo cp /etc/bind/db.127 /etc/bind/zones/db.10.9.xx.rev```

Ficando nesse caso:

<img src="/IMG/f7.png" width=600/>

### 3 - Editando os arquivos

Agora vamos para a pasta zones com o comando:

```cd /etc/bind/zones``` 

<img src="/IMG/f8.png" width=600/>

Verificando os arquivos com ```ls -la```:

<img src="/IMG/f9.png" width=600/>

Agora vamos editar

Primeiramente, vamos editar o arquivo ```db.grupo8.turma913.ifalara.local```:

<img src="/IMG/f10.png" width=600/>

E, então, você edita conforme a imagem abaixo:

<img src="/IMG/f11.png" width=600/>

Agora vamos editar o arquivo ```db.10.9.13.rev``` com o comando:

```sudo nano db.10.9.13.rev```

E em seguida edita conforme a imagem abaixo:

<img src="/IMG/f13.png" width=600/>

Agora vamos voltar para a pasta bind com ```d ..```

### 4 - Configuração do named.conf.local

Depois disso, vamos editar o arquivo named.conf.local com o comando:

```sudo nano named.conf.local```

<img src="/IMG/f14.png" width=600/>

Ao entrar, edite o arquivo conforme a imagem abaixo:

<img src="/IMG/f15.png" width=600/>

Para checar a sintaxe de configuração do BIND deve-se executar o comando named-checkconf. Este scritp checa os arquivos /etc/bind/named.conf.local:

Dê um ```sudo named-checkconf```

Vamos verificar, agora, a sintaxe desse arquivo named com:

```cat named.conf.local```

Esperado:

<img src="/IMG/f16.png" width=600/>

Agora vamos verificar também db com o named-checkzone:

comandos:

```sudo named-checkzone grupo8.turma913.ifalara.local db.grupo8.turma913.ifalara.local```

<img src="/IMG/ronaldo5.png" width=600/>

```sudo named-checkzone 13.9.10.in-addr.arpa db.10.9.13.rev```

<img src="/IMG/ronaldo6.png" width=600/>

Agora vamos ver o status com o comando:

```systemctl status bind9```

<img src="/IMG/f3png" width=600/>

### Testes

<img src="/IMG/prrint" width=600/>

Fazendo ping:

<img src="/IMG/prrrint" width=600/>

Caso o ping não funcione, faça o seguinte passo:

Vá para ```cd /etc/netplan``` e digite o comando:

```sudo nano 00-installer-config-yaml```

img src="/IMG/ronaldo12" width=600/>





