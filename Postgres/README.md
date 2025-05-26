# 🚀 Projeto PostgreSQL com Docker

Este projeto utiliza Docker para subir um banco de dados PostgreSQL com scripts SQL para criação de banco, tabelas e inserção de dados automaticamente.

---

## 📦 Estrutura do Projeto

```
Postgres/
├── docker-compose.yml
├── init-db/
│   ├── 01_create_db.sql
│   ├── 02_create_tables.sql
│   └── 03_insert_data.sql
```

---

## ⚙️ Pré-requisitos

- [Docker](https://www.docker.com/)
- [Docker Compose](https://docs.docker.com/compose/)

---

## ▶️ Como executar o projeto

1. **Clone o repositório ou copie os arquivos:**

```bash
git clone <url-do-repo>
cd Postgres
```

2. **Suba o container:**

```bash
docker-compose up -d
```

3. **Acesse o banco de dados via terminal:**

```bash
docker exec -it postgres_loja psql -U postgres -d loja_virtual
```

---

## 🧾 Sobre os arquivos SQL

Os scripts localizados no diretório `init-db/` são executados automaticamente na primeira inicialização do container:

- `01_create_db.sql` → Cria o banco `loja_virtual` (pode ser omitido se usar o `POSTGRES_DB` no compose).
- `02_create_tables.sql` → Cria as tabelas `clientes` e `produtos`.
- `03_insert_data.sql` → Insere dados de exemplo.

> ℹ️ A ordem dos scripts é definida alfabeticamente.

---

## 🧼 Resetando o ambiente

Para resetar completamente o banco (incluindo os dados):

```bash
docker-compose down -v
docker-compose up -d
```

---

## 📚 Conexão Externa

Você pode conectar-se ao PostgreSQL via ferramentas como DBeaver, PgAdmin ou psql local usando:

- **Host:** `localhost`
- **Porta:** `5432`
- **Usuário:** `postgres`
- **Senha:** `postgres`
- **Banco:** `loja_virtual`

---

## 📄 Licença

Este projeto está sob licença MIT. Sinta-se livre para utilizar e adaptar.
