# Compartilhamento de arquivos com Samba

### Passo 1: 

Nomear a máquina usando o código seguinte:

<img src="/IMG/samba/image13.png" width=600/>

e depois dá o reboot com o comando:

```$ reboot```

### Passo 2:

Editar o arquivo netplan, fazendo as atribuições de IPs:

<img src="/IMG/samba/image6.png" width=600/>

Depois

### Passo 3: 

Instalar o servidor samba na vm ‘smb’ (que foi o hostname atribuído no início deste passo a passo):

<img src="/IMG/samba/image5.png" width=600/>
<img src="/IMG/samba/image15.png" width=600/>

### Passo 4: 

Digitar os seguintes comandos para verificar se o samba está funcionando:

<img src="/IMG/samba/image21.png" width=600/>
<img src="/IMG/samba/image8.png" width=600/>

Está ativo!!

<img src="/IMG/samba/image3.png" width=600/>

### Passo 5: 

Criar um arquivo de backup:

<img src="/IMG/samba/image19.png" width=600/>
<img src="/IMG/samba/image7.png" width=600/>
<img src="/IMG/samba/image4.png" width=600/>

O seguinte comando é para limpar os comentários do arquivo

<img src="/IMG/samba/image18.png" width=600/>

### Passo 6: 

Editar o arquivo  /etc/samba/smb.conf adicionando as interfaces ens160 e ens192:

Para entrar no arquivo digita o seguinte comando:

<img src="/IMG/samba/image14.png" width=600/>

utiliza o comando 29d para deletar o que tinha nele e coloca isso aqui:
[global]
   workgroup = WORKGROUP
   server string = %h server (Samba, Ubuntu)
   log file = /var/log/samba/log.%m
   max log size = 1000
   logging = file
   panic action = /usr/share/samba/panic-action %d
   server role = standalone server
   obey pam restrictions = yes
   unix password sync = yes
   passwd program = /usr/bin/passwd %u
   passwd chat = *Enter\snew\s*\spassword:* %n\n *Retype\snew\s*\spassword:* %n\n *password\supdated\ssuccessfully* .
   pam password change = yes
   map to guest = bad user
   usershare allow guests = yes
[printers]
   comment = All Printers
   browseable = no
   path = /var/spool/samba
   printable = yes
   guest ok = no
   read only = yes
   create mask = 0700
[print$]
   comment = Printer Drivers
   path = /var/lib/samba/printers
   browseable = yes
   read only = yes
   guest ok = no

Feito isso, tem que modificar as interfaces colocando da forma que está na imagem:

<img src="/IMG/samba/image12.png" width=600/>

feito isso dá esc+:+x

reiniciar o servidor:

<img src="/IMG/samba/image20.png" width=600/>

Entra no arquivo de novo e modifica para usuário permitidos serem do grupo sambashare

<img src="/IMG/samba/image1.png" width=600/>
<img src="/IMG/samba/image2.png" width=600/>
<img src="/IMG/samba/image6.png" width=600/>
<img src="/IMG/samba/image9.png" width=600/>
<img src="/IMG/samba/image10.png" width=600/>
<img src="/IMG/samba/image11.png" width=600/>
<img src="/IMG/samba/image16.png" width=600/>
<img src="/IMG/samba/image17.png" width=600/>
<img src="/IMG/samba/image22.png" width=600/>
<img src="/IMG/samba/image23.png" width=600/>
<img src="/IMG/samba/image24.png" width=600/>

