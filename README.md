# Rede Social Containerizada

**Autor:** Luiz Gustavo da Silva Barros
**Data:** 30 de Abril de 2026
**Disciplina:** DevOps

---

## 1. Visão Geral da Aplicação

Este documento apresenta a arquitetura e o processo de implantação da **Aplicação Amizade**, um sistema web completo baseado no conceito de microsserviços. A aplicação foi desenvolvida utilizando Docker, para containerizar 3 camadas de serviços.

A arquitetura segue o modelo de **três camadas** (frontend, backend e banco de dados), todas containerizadas com **Docker**.

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
   Ter o Docker instalado.


2. **Criar arquivo .env para configuração de variáveis de ambiente:**

```bash
   MYSQL_ROOT_PASSWORD=change_me_root
   MYSQL_DATABASE=amizade_db
   MYSQL_USER=user_app
   MYSQL_PASSWORD=change_me_user

   DB_HOST=db
   DB_NAME=amizade_db
   DB_USER=user_app
   DB_PASSWORD=change_me_user

   # Generate a strong secret: openssl rand -hex 64
   JWT_SECRET="a2c4e6858c1b4e29a3f2d8e5g1h3i5j7k9l2m4n6o8p1q3r5s7t9u1v3w5x7y9z0a2b4"
```

3. **Construir e enviar imagens para o Docker Hub:**

```bash
   docker build -t lgstavo/frontend ./frontend
   docker build -t lgstavo/backend ./backend
   docker build -t lgstavo/db ./db

   docker push lgstavo/frontend
   docker push lgstavo/backend
   docker push lgstavo/db
```

4. **Inicializar o container:**

```bash
   docker compose up --build
```

5. **Acessar a aplicação em [localhost](http://localhost:80)**
