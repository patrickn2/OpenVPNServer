# OpenVPNServer

# Instalar OpenVPN no servidor de VPN

## Fazer Update do sistema:
```bash
yum update -y
```

## Baixar o script instalador
[Script no GitHub](https://github.com/angristan/openvpn-install):
```bash
wget https://raw.githubusercontent.com/Angristan/openvpn-install/master/openvpn-install.sh -O centos7-vpn.sh
```

## Dar poder de execução para o script
```bash
chmod +x centos7-vpn.sh
```

## Executar o script para instalar
Usar porta random, o resto pode ser default:
```bash
./centos7-vpn.sh
```

## Editar o config do OpenVPN
Comentar as linhas que possuem "push" e adicionar as linhas abaixo:
```bash
vi /etc/openvpn/server.conf
```

Adicionar as linhas abaixo no config:
```bash
push "route-nopull"
push "route 104.244.42.0 255.255.255.0"
push "route 199.59.148.0 255.255.255.0"
```

## Reiniciar o servidor e verificar status
Se ele não tiver sido reiniciado, matar o servidor com o comando `kill`:
```bash
systemctl restart openvpn@server
systemctl status openvpn@server
```

## Configurar Firewall
Adicionando a porta escolhida pelo OpenVPN:
```bash
systemctl start firewalld
firewall-cmd --zone=public --permanent --add-port=PORTA/udp
firewall-cmd --zone=public --permanent --add-masquerade
firewall-cmd --reload
```

## Para criar/remover usuários
Usar o mesmo script de instalação:
```bash
./centos7-vpn.sh
```

This Markdown formatting includes code blocks for commands and headers for different sections of the process.
