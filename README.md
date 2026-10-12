Markdown
# 🌐 Tutorial Completo: Configuração de Servidor ISC-DHCP & Painel Webmin

<p align="center">
  <img src="https://img.shields.io/badge/status-ativo-success?style=for-the-badge&logo=github" alt="Status Ativo">
  <img src="https://img.shields.io/badge/versão-v1.0-blue?style=for-the-badge" alt="Versão">
  <img src="https://img.shields.io/badge/serviço-ISC--DHCP-orange?style=for-the-badge&logo=linux" alt="ISC-DHCP">
  <img src="https://img.shields.io/badge/painel-Webmin-red?style=for-the-badge&logo=webmin" alt="Webmin">
  <img src="https://img.shields.io/badge/licença-MIT-informational?style=for-the-badge" alt="Licença">
</p>

<p align="center">
  <b>Guia definitivo e passo a passo para instalação, configuração de escopos, segurança de rede e gerenciamento web de servidores DHCP utilizando ISC-DHCP e Webmin.</b>
</p>

---

## 📌 Portas de Rede Utilizadas

| Protocolo / Serviço | Porta | Direção / Descrição |
| :--- | :--- | :--- |
| **DHCP Server** | `UDP 67` | Escuta de requisições de clientes na rede |
| **DHCP Client** | `UDP 68` | Resposta e entrega de configurações aos clientes |
| **Webmin** | `TCP 10000` | Painel de administração web |

---

## ⚙️ 1. Instalação e Configuração do ISC-DHCP

### 🛠️ Instalação no Servidor (Linux)
Para instalar o servidor DHCP no sistema, execute o comando:
```bash
sudo apt update
sudo apt install isc-dhcp-server
```
📂 Caminho Direto do Arquivo de Configuração
A localização do arquivo de configuração principal (dhcpd.conf) fica em caminho direto:

Plaintext
/etc/dhcp/dhcpd.conf
📝 Padrão de Identação e Configuração do Arquivo dhcpd.conf
O arquivo de configuração define as regras globais de concessão de IPs e as sub-redes da infraestrutura. A indentação (tabulação e organização de blocos) deve ser respeitada rigorosamente para evitar erros de sintaxe ao iniciar o serviço.

Abaixo está o modelo padrão de identação e estrutura para configurar o arquivo:
```bash
Plaintext
authoritative;

default-lease-time 43200;
max-lease-time 43200;

option dhcp6.name-servers 0 0; # Bloqueia IPs IPv6 desnecessários
log-facility local7;

subnet 10.12.1.0 netmask 255.255.255.0 {
    authoritative;
    allow client-updates;
    
    # range de IPs distribuídos dinamicamente na rede
    range 10.12.1.11 10.12.1.200;
    
    option domain-name-servers 192.168.100.170;
    option broadcast-address 10.12.1.255;
    option routers 10.12.1.1;
    
    # Segurança: Impede que clientes desconhecidos recebam IP
    deny unknown-clients;
}
```

🔒 Explicação dos Comandos de Segurança e Parâmetros:
authoritative;: Declara que este servidor é a autoridade máxima de atribuição de endereços IP para esta rede.

range: Define a faixa inicial e final de endereços IP que serão distribuídos para as estações.

deny unknown-clients;: Comando de segurança essencial que impede que o servidor distribua endereços IP para hosts que não estejam previamente cadastrados ou registrados na rede.

Identação: Mantenha as chaves { e } alinhadas e os parâmetros internos recuados (com tabulação ou espaços) para garantir a legibilidade e o correto parsing pelo serviço.

🚀 Gerenciamento do Serviço DHCP
Após salvar e fechar o arquivo de configuração, gerencie o serviço com os comandos:

```Bash
# Iniciar o serviço
sudo systemctl start isc-dhcp-server
```
# Reiniciar o serviço (após alterações no dhcpd.conf)
```Bash
sudo systemctl restart isc-dhcp-server
```
# Verificar o status atual
```Bash
sudo systemctl status isc-dhcp-server
```
📊 Monitoramento de Distribuição de IPs
Para verificar em tempo real se o ISC-DHCP está distribuindo os endereços corretamente aos clientes (DHCPACK), utilize o comando de log:

```Bash
cat /var/log/syslog | grep "DHCPACK"
```
🖥️ 2. Instalação e Configuração do Webmin
Siga os comandos abaixo sequencialmente para instalar o painel de gerenciamento web:
Adicionar o repositório ao system source:

```Bash
echo "deb [http://download.webmin.com/download/repository](http://download.webmin.com/download/repository) sarge contrib" | sudo tee -a /etc/apt/sources.list
Adicionar a chave GPG do repositório:
```

```Bash
wget -q [http://www.webmin.com/jcameron-key.asc](http://www.webmin.com/jcameron-key.asc) -O- | sudo apt-key add -
Atualizar os pacotes do sistema:
```

```Bash
sudo apt-get update
Instalar o Webmin e dependências:
```
```Bash
sudo apt-get install webmin apt-transport-https
```
Liberar a porta no Firewall (UFW):
(Comando para liberar a porta do Webmin. Caso não seja liberada, o firewall pode bloquear e impedir o seu acesso à interface)

```Bash
sudo ufw allow 10000
```

🔑 Acesso e Gerenciamento de Módulos
Credenciais de Acesso: O login na interface web do Webmin é o mesmo utilizado para o usuário administrador do seu Linux Server.

Integração com o Servidor DHCP: Como o ISC-DHCP foi instalado por fora (de forma independente via apt), ele já aparece automaticamente na aba de servidores (Servers) do Webmin.

Módulos Adicionais: Caso o usuário não tivesse feito a instalação de forma independente, pelo próprio Webmin na aba de "Un-used Modules" seria possível baixar o serviço DHCP e várias outras aplicações (como o Samba e o LDAP) diretamente pela interface gráfica.
