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

<img src="/IMG/f9." width=600/>




