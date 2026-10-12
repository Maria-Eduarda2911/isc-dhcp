# 🌐 Tutorial: Configuração de Servidor ISC-DHCP & Painel Webmin

<p align="center">
  <img src="https://img.shields.io/badge/status-ativo-success?style=for-the-badge&logo=github" alt="Status Ativo">
  <img src="https://img.shields.io/badge/versão-v1.0-blue?style=for-the-badge" alt="Versão">
  <img src="https://img.shields.io/badge/serviço-ISC--DHCP-orange?style=for-the-badge&logo=linux" alt="ISC-DHCP">
  <img src="https://img.shields.io/badge/painel-Webmin-red?style=for-the-badge&logo=webmin" alt="Webmin">
  <img src="https://img.shields.io/badge/licença-MIT-informational?style=for-the-badge" alt="Licença">
</p>

<p align="center">
  <b>Guia passo a passo para instalação, configuração de escopos, segurança de rede e gerenciamento web de servidores DHCP utilizando ISC-DHCP e Webmin.</b>
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

### 🛠️ Instalação no Servidor Linux
```bash
sudo apt update
sudo apt install isc-dhcp-server
