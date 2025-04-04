# InfraRedeXPTO

> _💻 Status do Projeto: Em Desenvolvimento._

## Resumo
<p align="justify"> 
Este repositório é destinado ao desenvolvimento de uma infraestrutura de TI robusta, segura e escalável para uma empresa fictícia XPTO. 
</p>

### Desafio
<p align="justify">
O projeto é uma atividade em trio da faculdade e seu objetivo é criar uma infraestrutura de ti para a empresa XPTO. Ela deve possuir uma arquitetura de rede, uma representação visual de sua topologia e conexões, um load balancer, proxy reverso, um banco de dados e backend utilizando docker, uma VPN segura e DHCP.
</p>

### Requisitos

#### Arquitetura de Rede
- [ ] Desenhar a topologia de rede, identificando as máquinas, conexões e fluxos de dados.
- [ ] Incluir a segmentação de redes, endereçamento IPV4.
- [ ] Especificar a integração entre o Load Balancer, Proxy Reverso e Banco de Dados.

#### Configuração do Load Balancer
- [ ] Implementar um Load Balancer com Nginx ou HAProxy.
- [ ] Configurar o balanceamento entre, no mínimo, 3 máquinas para distribuir o tráfego.
- [ ] Criar um mecanismo de monitoramento de disponibilidade e resposta dos servidores.

#### Proxy Reverso
- [ ] Configurar uma máquina com Nginx para atuar como Proxy Reverso.
- [ ] Gerenciar requisições e redirecioná-las para os servidores apropriados.

#### Banco de Dados
- [ ] Criar um servidor dedicado para o banco de dados usando Docker ou AWS RDS.
- [ ] Escolher entre MySQL, PostgreSQL ou MongoDB e justificar a escolha.

#### VPN
- [ ] Configurar uma VPN segura (OpenVPN) para acessos externos.
- [ ] Integrar a VPN ao firewall da rede para maior controle de acessos.

#### Docker e Virtualização
- [ ] Utilizar Docker para hospedar servidores web e banco de dados.
- [ ] Criar um docker-compose para gerenciamento facilitado dos serviços.
- [ ] Demonstrar a escalabilidade dos containers e a comunicação entre eles. 

#### Endereçamento IPv4 e Segmentação de Redes
- [ ] Definir a estrutura de endereçamento da empresa.
- [ ] Implementar DHCP para gerenciar alocação dinâmica de endereços.

#### Segurança Reforçada
- [ ] Implementar autenticação multifator (2FA) para o acesso remoto.
- [ ] Criar regras avançadas de firewall para proteger servidores internos.

#### Alta Disponibilidade
- [ ] Implementar replicação de dados entre diferentes servidores.
- [ ] Garantir redundância no balanceamento de carga para evitar falhas.

#### Monitoramento e Análise
- [ ] Configurar ferramentas como Prometheus e Grafana para monitoramento de 
tráfego e desempenho.
- [ ] Criar um painel de métricas para acompanhamento em tempo real.

### ⚙ Tecnologias ⚙

<div> 

</div>
