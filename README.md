<p align="center">
 <img src="https://github.com/jsantos-examples/flexpag-desafio-backend/blob/main/contents/flexpag.png" width="600" alt="Banner Flexpag">
</p>

# 🚀 Desafio backend

Bem-vindo(a). Este é o desafio Back end!

O objetivo deste desafio é avaliar suas habilidades em programação.
Quando concluir o desafio, basta responder o e-mail onde recebeu o link do repositório.
Em seguida, enviaremos o feedback e as instruções dos próximos passos!

Caso tenha alguma dúvida, nós estamos disponíveis para tirá-las.
Bom desafio!

> ⚠️ **É importante que o seu repo esteja público, caso contrário não iremos conseguir avaliar sua resposta**

---

- [🧠 Contexto](#-contexto)
  - [🚰 Fluxo esperado](#-fluxo-esperado)
- [✔️ Critérios de Avaliação](#️-critérios-de-avaliação)
- [:rocket: Instruções](#rocket-instruções)
  - [:notebook: To-do list](#notebook-to-do-list)

# 🧠 Contexto

A Flexpag é uma empresa de tecnologia especializada em soluções digitais de pagamento. Sabendo disso, montamos um desafio que consiste em implementar um serviço de pagamento agendando.

### 🚰 Fluxo esperado

- Quando um agendamento é enviado deve ser registrado como `pending` e retornado o id;
- O usuário deve conseguir consultar o status do agendamento `pending`|`paid`;
- :warning: **Se o pagamento ainda não foi realizado o usuário pode**;
  - Excluir o agendamento;
  - Atualizar a data:hora do agendamento;
  
## ✔️ Critérios de Avaliação

Além dos requisitos levantados acima, iremos olhar para os seguintes critérios durante a correção do desafio:

- Eficiência e simplicidade;

## :rocket: Instruções

Chegou a hora de colocar a mão na massa!

### Aplicação

A aplicação já está com o pre setup default. 

**dependências:**
- spring-boot-starter-web
- spring-boot-starter-data-jpa
- spring-boot-devtools
- h2
- lombok

| componente | porta |
| --------- | ----------- |
| Aplicação  | `8080` |

aplication.yaml foi configurado para apontar para o banco local h2
```
spring:
  datasource:
    driverClassName: org.h2.Driver
    url: jdbc:h2:mem:payment-scheduler
    username: admin
    password: admin
  h2:
    console:
      enabled: true
      path: /h2-console
  jpa:
    database-platform: org.hibernate.dialect.H2Dialect
    hibernate:
      ddl-auto: update
    properties:
      hibernate:
        format_sql: true
        show_sql: true
```

### :notebook: To-do list
- [X] Fazer o fork do projeto
- [X] Implementar solução
- [X] Enviar link do projeto

:information_source: _Sinta-se livre para incluir quaisquer observações que achar necessário_

---

_O desafio acima foi cuidadosamente construído para propósitos de avaliação apenas._




# Observações sobre o projeto:
---
> Removi o target/ do .gitignore para realizar o docker build 
---
>### Este projeto foi desenvolvido com [Docker](https://www.docker.com/) então ao iniciar o projeto digite:

    Criando imagem: docker build -t spring-app .
    
    Rodando a imagem: docoker run -p 8080:8080 spring-app

---
>### Antes de fazer qualquer requisição no projeto consulte a documentação:
   
    http://localhost:8080/swagger-ui/index.html#/payment-scheduler-controller

---
>### Certifique-se de que o projeto esta rodando antes de acessar a documentação.

# Exemplos básicos de requisição:
   
    Method POST
    Rota: /payment-scheduler

    Enviado: {
      "namePayment": "Comprar carro",
      "schedulingDate": "2122-10-16T15:58:09.644Z"
    }
    
    Recebido: {
      "3fa85f64-5717-4562-b3fc-2c963f66afa6"
    }
---
    
    Method GET
    Rota: /payment-scheduler/3fa85f64-5717-4562-b3fc-2c963f66afa6
    
    Recebido: {
       "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
       "namePayment": "Comprar carro",
       "schedulingDate": "2122-10-16T15:58:09.644Z",
       "created_at": "2022-10-16T15:58:09.644Z",
       "status": "pending"
    }
---
    
    Method PATCH
    Rota: /payment-scheduler/3fa85f64-5717-4562-b3fc-2c963f66afa6
    
    Enviado: {
      "schedulingDate": "3122-10-16T15:58:09.644Z"
    }
    
    Recebido: {
       "id": "3fa85f64-5717-4562-b3fc-2c963f66afa6",
       "namePayment": "Comprar carro",
       "schedulingDate": "3122-10-16T15:58:09.644Z",
       "created_at": "2022-10-16T15:58:09.644Z",
       "status": "pending"
    }
---
>### Lembrando que você não pode atualizar ou deletar um agendamento que ja foi pago.
>### Ao chegar na data de agendamento(schedulingDate) o status será modificado para paid. 
    
