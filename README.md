# InfraRedeXPTO - SPRINT-2

> _💻 Status da Sprint: Concluída._

## Resumo
<p align="justify">
  
Na segunda sprint do projeto foi focado no desenvolvimento dos **containers Docker** e desenvolvimento da aplicação em si, com **backend** desenvolvido em **Python** e **MongoDB** como banco de dados. Os requisitos desenvolvidos nessa sprint foram:

- Banco de Dados
 - Criar um servidor dedicado para o banco de dados usando Docker ou AWS RDS.
 - Escolher entre MySQL, PostgreSQL ou MongoDB e justificar a escolha.

- Docker e Virtualização
 - Criar um docker-compose para gerenciamento facilitado dos serviços.
 - Demonstrar a escalabilidade dos containers e a comunicação entre eles.
</p>

## Desenvolvimento
<p align="justify">
  
Para iniciar a segunda sprint foi necessário desenvolver o **backend**, **frontend** e o **banco de dados** e deixar o código disponível no [github.](https://github.com/Suricato-Conquistador/TaskFlow)

<!-- <img src="https://github.com/user-attachments/assets/d77d97e2-8152-423f-84eb-923a8b554af9" width=700 /> -->

## Desenvolvimento da Aplicação

Optou-se inicialmente desenvolver a aplicação localmente para realizar todos os testes e garantir que a aplicação esteja funcionando para então, ser transferida para um container docker. O início foi dado pelo backend.

### Backend

Para iniciar o desenvolvimento do backend foi necessário criar uma **máquina virtual** pelo comando no terminal:

`python -m venv venv` ou `python3 -m venv venv` 

E acessá-la com:

`.\venv\Scripts\activate`

No linux com:

`venv/bin/activate`

Dentro da máquina virtual precisamos instalar as bibliotecas necessárias, nesse caso bcrypt, fastapi, pymongo e uvicorn:

`pip install bcrypt fastapi pymongo uvicorn`

Para facilitar a instalação das dependências para a equipe, criamos um requirements.txt com:

`pip freeze > requirements.txt`

Com o ambiente preparado foi possível desenvolver a aplicação com a seguinte estrutura: 

```
backend/
├── database/
    ├── models.py 
    └── schemas.py
├── configurations.py
├── main.py
├── requirements.txt
├── test_connection.py
├── .env
```

### Frontend

### Docker

Para o desenvolvimento do docker foi usada uma mesma instância na AWS do Load Balance, porém em grupos de segurança foi necessário liberar o acesso às portas 8000(onde irá rodar o backend) e a porta 27017(porta usada pelo MongoDB). Criada a instância nos conectamos à instância e instalamos o docker com o comando:

`apt install docker`

