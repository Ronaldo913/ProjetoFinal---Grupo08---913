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

### 2.1 - Zonas

Bem, agora, depois da pasta criada, vamos para as instalações da zona. 

#### 2.1.1 - Zona direta

