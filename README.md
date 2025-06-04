# InfraRedeXPTO - SPRINT-3

> _💻 Status da Sprint: Concluída._

## Resumo
<p align="justify">
  
Na terceira sprint do projeto foi focado no desenvolvimento do **VPN** para que a aplicação possa ser acessada apenas pela máquina que possuir os certificados e chaves, além de conectado com o OpenVPN. Os requisitos desenvolvidos nessa sprint foram:

- VPN
 - Configurar uma VPN segura (OpenVPN) para acessos externos.
 - Integrar a VPN ao firewall da rede para maior controle de acessos.
</p>

## Desenvolvimento
<p align="justify">
  
Para iniciar a terceira sprint foi necessário acessar a **instância da AWS** que está rodando o **Load Balancer**.

## Desenvolvimento

Antes de iniciar o desenvolvimento devemos atualizar os indexes com `apt update` e instalar o openvpn e o easyrsa com `apt install openvpn easy-rsa`.
