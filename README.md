# Rede Social Containerizada

**Autor:** Luiz Gustavo da Silva Barros
**Data:** 26 de Junho de 2026
**Disciplina:** DevOps

---

## 1. Visão Geral da Aplicação

Este documento apresenta a arquitetura e o processo de simulação de uma Rede Social, um sistema web completo baseado no conceito de microsserviços. A aplicação foi desenvolvida utilizando Docker, para containerizar 3 camadas de serviços. Além disso, utilizamos Kubernetes para a orquestração desses containers e Helm para automatizar o deploy da aplicação.

A arquitetura segue o modelo de **três camadas** (frontend, backend e banco de dados).

---

## 2. Arquitetura e Componentes (Containers)

A aplicação é dividida em três containers independentes, cada um com uma função específica:

### 2.1. Frontend (`frontend_amizade`)

- **Tecnologia:** Aplicação de página única (SPA) desenvolvida com **Vue.js**, servida por um servidor **NGINX**, realizando um Proxy Reverso para evitar a exposição das portas de Backend e Banco de Dados.
- **Responsabilidade:** Interface com o usuário. Exibe a UI, gerencia o estado da aplicação e faz requisições REST para o backend, realizando operações como cadastro, login, postagens e entre outras.

### 2.2. Backend (`backend_amizade`)

- **Tecnologia:** API RESTful desenvolvida em **Java** com o framework **Spring Boot**. Utiliza **Spring Security** para autenticação baseada em tokens JWT.
- **Responsabilidade:** Camada lógica da aplicação. Faz validação de dados, gerenciamento de usuários e comunicação com o banco de dados. Expõe endpoints seguros consumidos pelo frontend.

### 2.3. Banco de Dados (`mysql_db_amizade`)

- **Tecnologia:** Imagem Docker customizada baseada no **MySQL**.
- **Responsabilidade:** Armazena todos os dados da aplicação (usuários, credenciais, relacionamentos, etc.). A imagem já inclui um script `init.sql` para criar automaticamente as tabelas e estruturas na primeira execução.

---

## 3. Como Executar a Aplicação

Para rodar a aplicação no seu ambiente local, siga os passos abaixo:

1. **Pré-requisitos:**
   Ter o Docker instalado;
   Ter o Minikube instalado;
   Ter o Helm instalado.


2. **Deploy da Aplicação:**

Após instalar os pré-requisitos, execute o script: 
```bash
   bash helm-up.sh -ibf
```
no terminal


3. **Inserir o caminho da aplicação em etc/hosts:**

Para obter o IP do Minikube, no terminal:
```bash
   minikube ip
```

```bash
   nano etc/hosts
```
E insira o caminho redesocial.k8s.local

5. **Acessar a aplicação em redesocial.k8s.local**
