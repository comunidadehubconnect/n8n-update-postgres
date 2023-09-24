<p align="center">
<img src="https://cwmkt.com.br/wp-content/uploads/2023/08/logo-github-cwmkt.svg" alt="DispZap Whats Marketing" width="240" />
<p align="center">Seja bem-vindo ao Guia de atualização de migrar N8N para Postgres 🚀</p>
</p>
  
<p align="center">
<img src="https://whatsapp.com/favicon.ico" alt="WhatsAPP-logo" width="32" />
<span>Grupo WhatsaAPP: </span>
<a href="https://link.cwmkt.com.br/grupo-whats" target="_blank">Grupo</a>
</p>

<hr />
<hr />

### Migração de banco de dados Sqlite para Postgres

### Criando Banco de dados Usuario e Senha

```bash
sudo -i -u postgres psql
```

```bash
CREATE ROLE n8n_user WITH LOGIN PASSWORD 'SenhaAqui';
```

```bash
CREATE DATABASE n8n_db;
```

```bash
GRANT ALL PRIVILEGES ON DATABASE n8n_db TO n8n_user;
```

```bash
GRANT CONNECT ON DATABASE n8n_db TO n8n_user;
```

```bash
\q
```


### Remover base atual do Sqlite

```bash
pm2 delete n8n
```

```bash
sudo mv /root/.n8n/.env /home
```

```bash
rm -rf .n8n
```

### Instalando última versão do n8n

```bash
npm install -g n8n
```

```bash
pm2 start n8n --cron-restart="0 0 * * *" -- start
```

```bash
sudo pm2 startup ubuntu -u root && sudo pm2 startup ubuntu -u root --hp /root && sudo pm2 save
```

```bash
sudo mv /home/.env /root/.n8n/
```

```bash
nano /root/.n8n/.env
```
### Adicione as seguintes variavéis para o postgres:

```
DB_TYPE=postgresdb
DB_POSTGRESDB_HOST=localhost
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_USER=n8n_user
DB_POSTGRESDB_PASSWORD=ColoqueUmaSenhaAqui
DB_POSTGRESDB_DATABASE=n8n_db
EXECUTIONS_DATA_PRUNE=true
EXECUTIONS_DATA_MAX_AGE=168
EXECUTIONS_DATA_PRUNE_MAX_COUNT=5000
```

```bash
rm -rf .env
```

```bash
ln -s ./.n8n/.env .env
```

```bash
pm2 restart all --update-env
```

### Atualizando e baixando update do Worflows e API

```bash
sudo -i -u quepasa
git pull
exit
```

```bash
systemctl restart quepasa
```

### Subindo Worflows para quepasa

```bash
bash /opt/quepasa-source/helpers/update-workflows.sh
```

### Instalações finalizadas ✅

Configue os Worflows no N8N

Adicione os community nodes ao seu N8N

```bash
n8n-nodes-chatwoot
```

```bash
n8n-nodes-quepasa
```

Pegue a senha do postgres do Chatwoot em:

```bash
nano /home/chatwoot/chatwoot/.env
```

Acesse opção Credenciais, adicione suas credenciais Postgres, salve.

### Abra Worflows a seguir e clique em salvar, em cada um deles:

GetChatwootContacts

ChatwootProfileUpdate

QuepasaToChatwoot

QuepasaQrcode

QuepasaAutomatic

ChatwootToQuepasa

### Plataforma pronta pra uso! 😎🚀🚀

