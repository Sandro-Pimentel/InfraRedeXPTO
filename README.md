# InfraRedeXPTO - SPRINT-1

> _💻 Status da Sprint: Concluída._

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

## Desenvolvimento
<p align="justify">
  
Para iniciar a primeira sprint foi necessário desenvolver a estrutura de rede do projeto por meio do site **SmartDraw**:

<img src="https://github.com/user-attachments/assets/d77d97e2-8152-423f-84eb-923a8b554af9" width=700 />

A imagem ilustra toda a estrutura de rede, uma máquina conectada a rede tenta realizar o acesso à aplicação, passa primeiro pela VPN, então o load balancer recebe e distribui o acesso entre os proxys reversos A, B e C, só então se obtém o acesso às aplicações A, B e C, essa aplicação frontend realiza requisições ao backend em Python, que puxa do MongoDB, ambos hospedados no docker.

Após criada e validada a estrutura de rede o próximo passo foi configurar as máquinas na aws, foram utilizadas 4 máquinas, o load balancer, os 2 servidores de aplicação e um servidor de backup.

### Máquina 1 - Load Balancer

Para a criação da máquina do load balancer foi criada uma **nova instância na AWS** com ubuntu, além disso em **grupos de segurança** na grupo usado para criar essa instância foi necessário liberar o acesso às portas 22(para a conexão via ssh) e 80(porta usada pelo Nginx para o load balancer). Criada a instância abrimos o terminal do windows e executamos o comando:

`ssh -i ./caminho-da-chave/nome-da-chave.pem ubuntu@ip-maquina-aws`

Dentro do terminal linux o primeiro comando necessário é o responsável por atualizar os índices dos pacotes de instalação.

`apt update`

Em seguida precisamos instalar o **Nginx** com o comando:

`apt install nginx`

Como os IPs da AWS **não são elásticos**, sempre mudarão conforme se inicia a instância novamente, para não ser necessário sempre editar nos arquivos de configuração os IPs das máquinas, editamos o arquivo hosts localizado em `/etc/hosts`. Para editá-lo utilizamos o comando `vim /etc/hosts` e nele inserimos as seguintes linhas:

```bash
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

```bash
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
Para testar o código acima digite `nginx -t`. Se não houver nenhum erro use `systemctl restart nginx` para reiniciar o nginx e garantir que as alterações já estão em execução.

### Máquina 2 - App01

Para a criação da máquina do servidor de aplicação 1 foram executados os mesmos processos até a instalação do nginx. Também será criado um arquivo de configuração em `/etc/nginx/conf.d`, para isso usamos o comando:

`vim /etc/nginx/conf.d/app01.conf`

E nele inserimos o seguinte código:

```bash
server {
  listen 80;
  root /var/www/html;
  index index.html;
}
```

`root` define que `/var/www/html` será o caminho onde estarão os arquivos do frontend e `index` define que o arquivo `index.html` será renderizado ao entrar nesse IP. Use `nginx -t` para testar as alterações.

Por fim criamos a página index.html no local definido com o comando:

`vim /var/www/html/index.html`

Para diferenciar o app01, app02 e backup, adicionamos um simples html:

```html
<!DOCTYPE html>
<html>
  <head>
    <title> App01 </title>
    <style>
      html {color-scheme: light dark;}
      body {
        width: 35em; margin: 0 auto;
        font-family: Tahoma, Verdana, Arial, sans-serif;
      }
    </style>
  </head>
  <body>
    <h1> Servidor de Aplicacao 1! </h1>
  </body>
</html>
```

Esses passos podem ser replicados para a criação do app02 e do backup, as únicas alterações serão nos textos da tag `<title>` e `<h1>`.

---

Para visualizar os logs de entrada do servidor, utiliza-se o comando:

`vim /var/log/nginx/access.log`

Este comando mostra o IP da máquina que entrou no servidor, o método HTTP utilizado, a URL acessada, código de status desta requisição o horário e o Sistema Operacional.
