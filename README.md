# InfraRedeXPTO - SPRINT-1

> _💻 Status do Projeto: Concluída._

## Resumo
<p align="justify">
  
Na primeira sprint do projeto foi focado no desenvolvimento do **Load Balancer** configurado no **Nginx** em uma máquina instância da **AWS**. Os requisitos desenvolvidos nessa sprint foram:

- Arquitetura de Rede
   - Desenhar a topologia de rede, identificando as máquinas, conexões e fluxos de dados.
   - Incluir a segmentação de redes, endereçamento IPV4.
   - Especificar a integração entre o Load Balancer, Proxy Reverso e Banco de Dados.
- Configuração do Load Balancer
   - Implementar um Load Balancer com Nginx ou HAProxy.
   - Configurar o balanceamento entre, no mínimo, 3 máquinas para distribuir o tráfego.

</p>

### Desenvolvimento
<p align="justify">
  
Para iniciar a primeira sprint foi necessário desenvolver a estrutura de rede do projeto por meio do site **SmartDraw**:

<img src="https://github.com/user-attachments/assets/ac35d36b-aa96-43aa-b1de-82a8683a4b74" width=700 />

A imagem ilustra toda a estrutura de rede, uma máquina conectada a rede realiza o acesso à aplicação, o load balancer recebe e distribui o acesso entre os proxys reversos A,B e C, só então se obtém o acesso às aplicações A,B e C, essa aplicação frontend realiza requisições requisições ao backend em Python, que puxa do MongoDB, ambos hospedados no docker.

Após criada e validada a estrutura de rede o próximo passo foi configurar as máquinas na aws, foram utilizadas 4 máquinas, o load balancer, os 2 servidores de aplicação e um servidor de backup.

#### Máquina 1 - Load Balancer

Para criar a máquina do load balancer foi criada uma **nova instância na AWS** com ubuntu, além disso em **grupos de segurança** na grupo usado para criar essa instância foi necessário liberar o acesso às portas 22(para a conexão via ssh) e 80(porta usada pelo Nginx para o load balancer). Criada a instância abrimos o terminal do windows e executamos o comando:

`ssh -i ./caminho-da-chave/nome-da-chave.pem ubuntu@ip-maquina-aws`

Dentro do terminal linux o primeiro comando necessário é o responsável por atualizar os índices dos pacotes de instalação.

`apt update`

Em seguida precisamos instalar o **Nginx** com o comando:

`apt install nginx`

Como os IPs da AWS **não são elásticos**, sempre mudarão conforme se inicia a instância novamente, para não ser necessário sempre editar nos arquivos de configuração os IPs das máquinas, editamos o arquivo hosts localizado em `/etc/hosts`. Para editá-lo utilizamos o comando `vim /etc/hosts` e nele inserimos as seguintes linhas:

```
174.129.170.229 xptolb
54.91.183.11 xptoapp01
34.201.105.75 xptoapp02
13.219.74.4 xptobackup

```

Para salvar `:x` ou `:wq`. Com essas alterações ao criar o load balance, em vez de digitamos nos lugares necessários o IP das instâncias na AWS que sempre mudarão, podemos apenas digitar os nomes definidos nesse arquivo. Para criar o arquivo de cofiguração, antes excluímos o arquivo de configuração padrão para evitar possíveis erros, localizado em `/etc/nginx/sites-enabled`, para a exclusão, o comando: 

`rm /etc/nginx/sites-enabled/default`

Criamos um arquivo de configuração para o load balance em `/etc/nginx/conf.d` chamado "loadbalance.conf" com:

`vim /etc/nginx/conf.d/loadbalance.conf`

Nele inserimos o seguinte código:

```
upstream apps {
  server xptoapp01 weight=1;
  server xptoapp02 weight=1;

  server xptobackup backup;
}

server {
  listen 80 default_server;
  server_name xptolb;

  location / {
    proxy_pass http://apps;
  }
}
```
