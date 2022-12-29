# Implementação DNS Master

## 1 - Login

Primeiro, vamos entrar no usuário su redes: 

```login: su redes``` 

```senha: admin@Lab92```

Após, vamos iniciar um perfil de configuração one-shot. Para isso, digitamos o comando:

```openvpn3 sessão-início --config vpn913.labredes```

E então, vamos fazer o ssh:

```ssh administrador@10.9.13.130```

<img src="/IMG/f1.png"/>

## 2 -Instalação

Agora vamos instalar o BIND9.
O BIND( é a aplicação de DNS que roda no servidor. Vamos instalá-lo via apt-get com o comando:

```sudo apt-get install bind9 dnsutils bind9-doc```

<img src="/IMG/f2.png"/>



