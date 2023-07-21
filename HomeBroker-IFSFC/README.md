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