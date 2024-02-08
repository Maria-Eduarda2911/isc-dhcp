#### Para uma melhor visualização do texto e com imagens, segue o link da documentação: 
https://docs.google.com/document/d/1IA4QmAJ-vFLjqa4xVGXrFKDXFfgFUiIGXF4mll5L2Y4/edit


## Instalação do ISC DHCP: 

sudo apt install isc-dhcp-server

Porta do Cliente DHCP: UDP 68

Porta do Servidor DHCP: UDP 67

A localização do arquivo dhcpd.conf fica em caminho direto: cd /etc/dhcp/dhcpd.conf

Padrão de indentação para adicionar hosts é mostrado no link, “deny unknown-clients;” é um comando usado para impedir que o servidor distribua ips para hosts que não estão registrados.

Comando usado para ver se o isc dhcp está distribuindo os ips:
cat /var/log/syslog | grep "DHCPACK"

### Instalação do Webmin: 

1 - echo "deb http://download.webmin.com/download/repository sarge contrib" | sudo tee -a /etc/apt/sources.list

2 - wget -q http://www.webmin.com/jcameron-key.asc -O- | sudo apt-key add -

3 - sudo apt-get update

4 - sudo apt-get install webmin apt-transport-https

5 - sudo ufw allow 10000 (Para liberar a porta do webmin, caso não seja liberado pode acontecer de você não conseguir acessar, por que o firewall está bloqueando)

#### O login é o mesmo do usuário no linux server.

Como o ISC-DHCP foi instalado por fora, ele já aparece na aba servers, caso o usuário não tivesse feito a instalação de forma independente, pelo próprio WEBMIN na aba de “Un-used Modules” pode baixar o serviço DHCP e várias outras aplicações como o SAMBA e o LDAP.


#### Tutorial de adição de Hosts é explicado no link



