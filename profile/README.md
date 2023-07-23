# Projeto de Homebroker

## Descrição do Projeto

<p align="justify">O projeto consiste em um sistema de homebroker, onde o usuário pode comprar e vender ações, além de acompanhar o valor de cada ação em tempo real.</p>

<p align="justify">O projeto foi desenvolvido utilizando a linguagem Go, ReactJs/NextJs, Apache Kafka, NestJs, Docker e Fluter (Mobile).</p>

### BIG PICTURE

```mermaid
%%{init: { "fontFamily": "Trebuchet MS, Verdana, Arial, Sans-Serif", "logLevel": 2 } }%%

graph LR;
    User(User) <--> HomeBroker[Home Broker \n `React / Next.JS`];
    HomeBroker[Home Broker \n `React / Next.JS`] <-->|Rest| NestJs[Backend \n Nest.js];
    NestJs[Backend \n Nest.js] -->|SSE - Tempo Real| HomeBroker[Home Broker \n `React / Next.JS`] ;
    NestJs[Backend \n Nest.js] --> Kafka[/Apache Kafka/];
    NestJs[Backend \n Nest.js]  <-->|Rest| Mobile[Mobile\n Flutter];
    Mobile[Mobile\n Flutter] -->|SSE - Tempo Real| NestJs[Backend \n Nest.js] ;
    Kafka[/Apache Kafka/] ---> NestJs[Backend \n Nest.js];
    SistemaBolsa[Sistema Bolsa \n Golang] ---> Kafka[/Apache Kafka/];
    Kafka[/Apache Kafka/] ---> SistemaBolsa[Sistema Bolsa \n Golang];

```

## Tecnologias utilizadas

- Linguagem Go
- ReactJs/NextJs
- Apache Kafka
- NestJs
- Docker
- Flutter (Mobile)

## Arquitetura de projeto (Visão Geral)

```mermaid
%%{init: { "fontFamily": "Trebuchet MS, Verdana, Arial, Sans-Serif", "logLevel": 2 } }%%
graph LR;
    User(User) -->|1 - Faz negociação| homebroker(NextJs\n Front-end e Back-end);
    homebroker(NextJs\n Front-end e Back-end) -.-> |8 - recebe a resposta| User(User);
    homebroker(NextJs\n Front-end e Back-end) --> |2 - REST \n comprar/vender\nconsultar dados| NestJs[Backend \n Nest.js];
    NestJs[Backend \n Nest.js] --> |3 - Publica compra/venda| Kafka[/Apache Kafka/];

    subgraph t [Sistema Bolsa]
        Kafka[/Apache Kafka/] --> |4 - Consome compra/venda| SistemaBolsa[Sistema Bolsa \n Golang];
        SistemaBolsa[Sistema Bolsa \n Golang] -.-> |5 - Publica novos matches| Kafka[/Apache Kafka/];
        Kafka[/Apache Kafka/] -.-> |6 - Consome novos matches| NestJs[Backend \n Nest.js];
    end

    NestJs[Backend \n Nest.js] -.-> |7 - Notifica o frontenf \n Server Sent Events | homebroker(NextJs\n Front-end e Back-end);

```



# Projeto Go 
 

# Projeto Nest.js
## Arquitetura de projeto (Visão Detalhada Nest.js)

```mermaid
%%{init: { "fontFamily": "Trebuchet MS, Verdana, Arial, Sans-Serif", "logLevel": 2 } }%%
graph LR;
    api ---|REST| nest;
    nest---->|3 - Publica \n compra/venda | kafka;
    kafka-->|4- Consome \n compra/venda|go;
    go-..-> |5 - Puclica novos patches|kafka1[kafka];
    kafka1-..->|6-Consome novos matches| nest;

```

## Tecnologias utilizadas no projeto Nest

- TypesScript/Javascript
- Nest.js
- Prisma ORM
- Mongo DB
- Apache Kafka
- Docker
- REST 
- SSE (Server Sent Events)

## TODO

- [x] Criar projeto Nest.js
- [x] Criar o banco de dados Mongo e integrar com o Prisma ORM
- [ ] Criar rotas REST:
    - [x] Assets (Ativos)
    - [x] Wallets (Carteiras)
    - [x] Wallet Assets (Ativos da Carteira)
    - [x] Orders (Ordens de Compra e Venda)
- [x] Criar integração com o microserviço Golang (Matches) utilizando Apache Kafka
