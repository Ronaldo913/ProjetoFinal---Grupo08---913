# Configurando o servidor DNS Slave

## 1 - Configurar o DNS master na interface de rede

Para fazer a configuração do Slave, primeiro a gente configura o arquivo do netplan de acordo com as nossas informações da planilha com o comando:

```sudo nano /etc/netplan/00-instaler-config.yaml```

Damos logo um cat no arquivo para verificar como ele está:

<img src="/IMG/ns2/image25.png" width=600/>

Temos que configurar a interface com os endereços do ns1 e ns2 conforme mostra na segunda linha do resultado do comando ```ifconfig``` na imagem abaixo:

<img src="/IMG/ns2/image18.png" width=600/>

obs.: aqui está sendo considerado que o DNS Master já foi configurado.

Então agora vamos editar esse arquivo com o comando:

```sudo nano /etc/netplan/00-instaler-config.yaml```

<img src="/IMG/ns2/image12.png" width=600/>

E então edita o arquivo conforme a imagem abaixo:

<img src="/IMG/ns2/image5.png" width=600/>

Logo após editar o arquivo dê um ```sudo netplan apply```.

Agora damos um ```ifconfig```:

<img src="/IMG/ns2/image16.png" width=600/>

Agora digitamos o comando:

```resolvectl status```

<img src="/IMG/ns2/image27.png" width=600/>

resultado:

<img src="/IMG/ns2/image32.png" width=600/>

Então o ping já vai tá funcionando:

<img src="/IMG/ns2/image1.png" width=600/>

## Configurar e instalar servidor DNS secundário (slave)

Para quem já tem o bind instalado é verificar se ele existe com o comando:

```sudo systemctl status bind9```

<img src="/IMG/ns2/image13.png" width=600/>

Como vemos acima, não existe. Então temos que instalar com o comando:

```sudo apt-get install bind9 dnsutils bind9-doc -y```

<img src="/IMG/ns2/image9.png" width=600/>

Então, vamos olhar de novo o status.

<img src="/IMG/ns2/image29.png" width=600/>

Agora digite o comando ```sudo nano /etc/default/named``` e antes do ```-u``` ponha um ```-4```

Logo após, para salvar digitamos:

```sudo system restart bind9```

Beleza, configuramos!

## 3 - Zonas

Vamos agora digitar o comando:

```cat /etc/bind/named.conf.local```

<img src="/IMG/ns2/image3.png" width=600/>
<img src="/IMG/ns2/image4.png" width=600/>

Agora vamos editar esse arquivo conforme a imagem abaixo:

```sudo nano /etc/bind/named.conf.local```

<img src="/IMG/ns2/image6.png" width=600/>

Logo após dê um ```sudo named-checkconf``` para checar a configuração. Se não aparecer nada é porque deu tudo certo.

<img src="/IMG/ns2/image15.png" width=600/>

Depois disso, execute o comando:

```sudo systemctl restart bind9.service```

Logo  dá um status de novo:

<img src="/IMG/ns2/image33.png" width=600/>

É isso! Agora é só testar.

## 4 - Testes

<img src="/IMG/ns2/image7.png" width=600/>
<img src="/IMG/ns2/image8.png" width=600/>
<img src="/IMG/ns2/image10.png" width=600/>
<img src="/IMG/ns2/image14.png" width=600/>
<img src="/IMG/ns2/image17.png" width=600/>
<img src="/IMG/ns2/image20.png" width=600/>
<img src="/IMG/ns2/image23.png" width=600/>
<img src="/IMG/ns2/image28.png" width=600/>
<img src="/IMG/ns2/image37.png" width=600/>

Checkzone:
<img src="/IMG/ns2/image11.png" width=600/>
<img src="/IMG/ns2/image22.png" width=600/>

