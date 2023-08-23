<p align="center">
	<img src="https://www.chatwoot.com/docs/img/logo.png" alt="Chatwoot-logo" width="250" />	
	<p align="center">O Chatwoot oferece todas as ferramentas para gerenciar conversas, construir relacionamentos e encantar seus clientes em um só lugar.</p>
</p>

<p align="left">
	<img src="https://whatsapp.com/favicon.ico" alt="WhatsAPP-logo" width="32" />
	<span>Grupo WhatsaAPP: </span>
	<a href="https://chat.whatsapp.com/CLKge3hmHmmBcIL04mBzmT" target="_blank">Grupo</a>
</p>

<hr />
<hr />

### Migração de banco de dados Sqlite para Postgres

# Criando Banco de dados Usuario e Senha

```bash
sudo -i -u postgres psql
```

```bash
CREATE ROLE n8n_user WITH LOGIN PASSWORD 'DigiteUmaSenhaAqui';
CREATE DATABASE n8n_db;
GRANT ALL PRIVILEGES ON DATABASE n8n_db TO n8n_user;
GRANT CONNECT ON DATABASE n8n_db TO n8n_user;
\q
```

# Remover base atual do Sqlite

```bash
pm2 delete n8n
```

```bash
sudo mv /root/.n8n/.env /home
```

```bash
rm -rf .n8n
```

# Upgrade NodeJS

```bash
sudo apt-get remove nodejs
```

```bash
sudo apt-get purge nodejs

```bash
sudo apt-get autoremove
```

```bash
curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash -
```
```bash
sudo apt-get install -y nodejs
```

# Instalando última versão do n8n

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
nano /root/.n8n/.env
```

```
DB_TYPE=postgresdb
DB_POSTGRESDB_HOST=localhost
DB_POSTGRESDB_PORT=5432
DB_POSTGRESDB_USER=n8n_user
DB_POSTGRESDB_PASSWORD=M@rcelo2050
DB_POSTGRESDB_DATABASE=n8n_db
C8Q_SINGLETHREAD=false
C8Q_QUEPASAINBOXCONTROL=1001
C8Q_GETCHATWOOTCONTACTS=1002
C8Q_QUEPASACHATCONTROL=1003
C8Q_CHATWOOTPROFILEUPDATE=1004
C8Q_POSTTOWEBCALLBACK=1005
C8Q_POSTTOCHATWOOT=1006
C8Q_CHATWOOTTOQUEPASAGREETINGS=1007
C8Q_CW_PUBLIC_URL="app.chatwoot.com"
C8Q_QP_DEFAULT_USER="contato@email.com"
C8Q_QP_BOTTITLE="SocialAtendimento"
C8Q_QP_CONTACT="contato@email.com"
N8N_EDITOR_BASE_URL="https://conector.n8n.com"
WEBHOOK_URL="https://conector.n8n.com"
```

```bash
ln -s ./.n8n/.env .env
```

```bash
pm2 restart all --update-env
```


# Subindo Worflows para Quepasa

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

Acesse opção Credenciais, adicione suas credenciais Postgres, salve.

# Abra Worflows a seguir e clique em salvar

GetChatwootContacts
ChatwootProfileUpdate
QuepasaToChatwoot
QuepasaQrcode
QuepasaAutomatic
ChatwootToQuepasa
