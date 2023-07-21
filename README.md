# Projeto de Homebroker



## Descrição do Projeto

<p align="justify">O projeto consiste em um sistema de homebroker, onde o usuário pode comprar e vender ações, além de acompanhar o valor de cada ação em tempo real.</p>

<p align="justify">O projeto foi desenvolvido utilizando a linguagem Go, ReactJs/NextJs, Apache Kafka, NestJs, Docker e Fluter (Mobile).</p>

### BIG PICTURE

```mermaid
flowchar LR
    User--> HomeBroker;
    HomeBroker --> NestJs;
    NestJs --> Kafka;
    Kafka ---> NestJs;
    NestJs ---> SistemaBolsa;
    SistemaBolsa ---> Kafka;
    Kafka ---> SistemaBolsa;
```


```mermaid
graph TD;
    A-->B;
    A-->C;
    B-->D;
    C-->D;
```