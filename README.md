# 🏗️ HCO Stack — Archote (Unificada)

Repositório unificado da stack **Archote** para deploy no Dokploy ou Coolify (Organização **HCO**).

---

## 📁 Estrutura do Repositório

```text
.
├── docker-compose.yml       # Stack unificada (Postgres, n8n Indústria, n8n PPA, Redis, RabbitMQ, PgAdmin)
├── .env                     # Variáveis de ambiente consolidadas
└── dumps/                   # Dump consolidado da base de dados Postgres em partes
    ├── archote_postgres.sql.part_aa
    └── archote_postgres.sql.part_ab
```

---

## 🚀 Como Fazer o Deploy no Dokploy / Coolify

1. **Repositório**: Conecte este repositório (`https://github.com/makarioszen/hco-stack-archote`).
2. **Docker Compose Path**: `./docker-compose.yml`
3. **Variáveis de Ambiente**: Copie o conteúdo do arquivo `.env` para as Environment Variables da aplicação.

---

## 💾 Restauração do Banco de Dados PostgreSQL

Para unir as partes do dump e restaurar no container do banco de dados:

```bash
# 1. Concatenar as partes do dump em um único arquivo SQL
cat dumps/archote_postgres.sql.part_* > /tmp/archote_postgres.sql

# 2. Restaurar no container postgres do Archote
docker exec -i <CONTAINER_POSTGRES_ID> psql -U n8n -d n8n < /tmp/archote_postgres.sql

# 3. Limpar o arquivo temporário
rm /tmp/archote_postgres.sql
```
