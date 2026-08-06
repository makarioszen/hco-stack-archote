# 🏗️ HCO Stack — Archote (Core, Industria & PPA)

Repositório da stack **Archote** para deploy no Dokploy (Organização **HCO - Public**).

---

## 📁 Estrutura do Repositório

```text
.
├── archote-core/           # Stack Core (Postgres principal, Redis, n8n Core, PgAdmin)
│   ├── docker-compose.yml
│   └── .env
├── archote-industria/      # Stack Industria (n8n Industria + Redis)
│   ├── docker-compose.yml
│   └── .env
├── archote-ppa/            # Stack PPA Distribuidora (n8n PPA + Redis)
│   ├── docker-compose.yml
│   └── .env
└── dumps/                  # Dump consolidado da base de dados Postgres em partes (<80MB)
    ├── archote_postgres.sql.part_aa
    ├── archote_postgres.sql.part_ab
    ├── archote_postgres.sql.part_ac
    ├── archote_postgres.sql.part_ad
    ├── archote_postgres.sql.part_ae
    └── archote_postgres.sql.part_af
```

---

## 🚀 Deploy e Auto-Restore no Dokploy

### 1. Auto-Restore de Banco de Dados via `.env`
O `docker-compose.yml` em `archote-core` está pré-configurado para auto-restaurar o banco quando a variável de ambiente **`RESTORE_DB=true`** for definida no Dokploy.

### 2. Comandos de Restore Manual:
Para concatenar as 6 partes do dump e restaurar manualmente no container Postgres:

```bash
# 1. Concatenar as partes do dump em um unico arquivo SQL
cat dumps/archote_postgres.sql.part_* > /tmp/archote_postgres.sql

# 2. Restaurar no container postgres do Archote
docker exec -i archote_postgres psql -U n8n -d n8n < /tmp/archote_postgres.sql

# 3. Limpar o dump temporario
rm /tmp/archote_postgres.sql
```
