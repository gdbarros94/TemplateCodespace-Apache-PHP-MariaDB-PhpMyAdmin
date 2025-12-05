# 📚 Documentação do Ambiente de Desenvolvimento

## 🎯 Visão Geral

Este é um ambiente de desenvolvimento completo para PHP com Apache, MySQL/MariaDB e phpMyAdmin, totalmente configurável através de variáveis de ambiente. O ambiente é modular, robusto e permite configuração precisa antes de iniciar o Codespace.

### 🚀 Características

- ✅ **Totalmente configurável via `.env`**
- ✅ **Arquitetura modular com scripts independentes**
- ✅ **Suporte a múltiplos bancos de dados e usuários**
- ✅ **DocumentRoot personalizável**
- ✅ **Configurações de PHP ajustáveis**
- ✅ **phpMyAdmin pré-configurado**
- ✅ **Scripts de recarga sem rebuild**
- ✅ **Logs coloridos e informativos**

---

## 🔧 Configuração Inicial

### 1️⃣ Configurar Variáveis de Ambiente

**Antes de iniciar o Codespace**, copie o arquivo `.env.example` para `.env` e ajuste as configurações:

```bash
cp .devcontainer/.env.example .devcontainer/.env
```

Edite `.devcontainer/.env` conforme suas necessidades. Veja a seção [Variáveis de Ambiente](#-variáveis-de-ambiente-disponíveis) para detalhes.

### 2️⃣ Iniciar o Codespace

Após configurar o `.env`, inicie o Codespace normalmente. O ambiente será configurado automaticamente com suas configurações personalizadas.

### 3️⃣ Acessar os Serviços

Após a inicialização, você terá acesso a:

- **Aplicação Web**: `http://localhost:80` (ou porta configurada)
- **phpMyAdmin**: `http://localhost:80/phpmyadmin`
- **MySQL/MariaDB**: Porta `3306`

---

## 📋 Variáveis de Ambiente Disponíveis

### 🗄️ MySQL/MariaDB

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `MYSQL_ROOT_PASSWORD` | `_43690` | Senha do usuário root |
| `MYSQL_DATABASE` | `jebusiness` | Nome do banco de dados |
| `MYSQL_USER` | `jebusiness` | Nome do usuário do banco |
| `MYSQL_PASSWORD` | `_43690` | Senha do usuário |
| `MYSQL_HOST` | `127.0.0.1` | Host do MySQL |
| `MYSQL_PORT` | `3306` | Porta do MySQL |
| `MYSQL_CHARSET` | `utf8mb4` | Charset do banco |
| `MYSQL_COLLATION` | `utf8mb4_unicode_ci` | Collation do banco |

### 🌐 Apache

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `APACHE_DOCUMENT_ROOT` | `public` | Diretório raiz (relativo ao workspace ou absoluto) |
| `APACHE_PORT` | `80` | Porta do Apache |
| `APACHE_SERVER_NAME` | `localhost` | ServerName |
| `APACHE_ALLOW_OVERRIDE` | `true` | Habilitar `.htaccess` |
| `APACHE_INDEXES` | `true` | Habilitar listagem de diretórios |
| `APACHE_REWRITE` | `true` | Habilitar mod_rewrite |

### 🐘 PHP

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `PHP_DISPLAY_ERRORS` | `On` | Exibir erros |
| `PHP_ERROR_REPORTING` | `E_ALL` | Nível de relatório |
| `PHP_UPLOAD_MAX_FILESIZE` | `64M` | Tamanho máximo de upload |
| `PHP_POST_MAX_SIZE` | `64M` | Tamanho máximo de POST |
| `PHP_MEMORY_LIMIT` | `256M` | Limite de memória |
| `PHP_MAX_EXECUTION_TIME` | `300` | Tempo máximo de execução |

### 🔐 phpMyAdmin

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `PHPMYADMIN_BLOWFISH_SECRET` | `_43690_blowfish_secret_change_me` | Secret para cookies (mín. 32 caracteres) |
| `PHPMYADMIN_ALLOW_NO_PASSWORD` | `false` | Permitir login sem senha |

### 🛠️ Desenvolvimento

| Variável | Padrão | Descrição |
|----------|--------|-----------|
| `INSTALL_XDEBUG` | `false` | Instalar Xdebug |
| `INSTALL_NODEJS` | `false` | Instalar Node.js |
| `NODEJS_VERSION` | `20` | Versão do Node.js |
| `TZ` | `America/Sao_Paulo` | Timezone |
| `APP_ENV` | `development` | Ambiente da aplicação |
| `APP_DEBUG` | `true` | Modo debug |

---

## 📁 Estrutura de Arquivos

```
.devcontainer/
├── .env.example              # Template de configuração
├── .env                      # Suas configurações (criar a partir do .example)
├── Dockerfile                # Imagem Docker configurável
├── devcontainer.json         # Configuração do devcontainer
├── init.sh                   # Script principal de inicialização
├── reload-services.sh        # Recarregar serviços sem rebuild
├── configure-mysql.sh        # Módulo de configuração MySQL
├── configure-apache.sh       # Módulo de configuração Apache
├── configure-php.sh          # Módulo de configuração PHP
├── configure-phpmyadmin.sh   # Módulo de configuração phpMyAdmin
└── docs.md                   # Esta documentação
```

---

## 🔄 Scripts Modulares

### `init.sh`
Script principal executado na criação do container. Orquestra todos os módulos.

**Uso:**
```bash
bash .devcontainer/init.sh <nome-do-repo>
```

### `configure-mysql.sh`
Configura MySQL/MariaDB com usuários, senhas e banco de dados.

**Uso:**
```bash
configure-mysql.sh
```

**Variáveis usadas:**
- `MYSQL_ROOT_PASSWORD`
- `MYSQL_DATABASE`
- `MYSQL_USER`
- `MYSQL_PASSWORD`
- `MYSQL_CHARSET`
- `MYSQL_COLLATION`

### `configure-apache.sh`
Configura Apache com DocumentRoot, VirtualHost e módulos.

**Uso:**
```bash
configure-apache.sh /caminho/do/workspace
```

**Variáveis usadas:**
- `APACHE_DOCUMENT_ROOT`
- `APACHE_PORT`
- `APACHE_SERVER_NAME`
- `APACHE_ALLOW_OVERRIDE`
- `APACHE_INDEXES`
- `APACHE_REWRITE`

### `configure-php.sh`
Configura PHP.ini com limites e configurações de desenvolvimento.

**Uso:**
```bash
configure-php.sh
```

**Variáveis usadas:**
- `PHP_DISPLAY_ERRORS`
- `PHP_ERROR_REPORTING`
- `PHP_UPLOAD_MAX_FILESIZE`
- `PHP_POST_MAX_SIZE`
- `PHP_MEMORY_LIMIT`
- `PHP_MAX_EXECUTION_TIME`
- `TZ`

### `configure-phpmyadmin.sh`
Configura phpMyAdmin com blowfish secret e conexão MySQL.

**Uso:**
```bash
configure-phpmyadmin.sh
```

**Variáveis usadas:**
- `PHPMYADMIN_BLOWFISH_SECRET`
- `PHPMYADMIN_ALLOW_NO_PASSWORD`
- `MYSQL_HOST`

### `reload-services.sh`
Reaplica todas as configurações e reinicia serviços sem rebuild.

**Uso:**
```bash
bash .devcontainer/reload-services.sh
```

---

## 💡 Casos de Uso Comuns

### 🔹 Alterar DocumentRoot

**Cenário**: Você quer que o Apache sirva arquivos da pasta `www/public` em vez de `public`.

**Solução**:
1. Edite `.devcontainer/.env`:
   ```env
   APACHE_DOCUMENT_ROOT=www/public
   ```
2. Execute:
   ```bash
   bash .devcontainer/reload-services.sh
   ```

### 🔹 Criar Múltiplos Bancos de Dados

**Cenário**: Você precisa de múltiplos bancos para diferentes projetos.

**Solução**:
1. Configure o banco principal no `.env`
2. Conecte ao MySQL e crie manualmente:
   ```bash
   mysql -u root -p${MYSQL_ROOT_PASSWORD}
   ```
   ```sql
   CREATE DATABASE segundo_banco CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
   GRANT ALL PRIVILEGES ON segundo_banco.* TO '${MYSQL_USER}'@'localhost';
   ```

### 🔹 Aumentar Limites de Upload

**Cenário**: Você precisa fazer upload de arquivos maiores que 64MB.

**Solução**:
1. Edite `.devcontainer/.env`:
   ```env
   PHP_UPLOAD_MAX_FILESIZE=256M
   PHP_POST_MAX_SIZE=256M
   ```
2. Execute:
   ```bash
   bash .devcontainer/reload-services.sh
   ```

### 🔹 Instalar Xdebug

**Cenário**: Você quer debug do PHP com breakpoints.

**Solução**:
1. Edite `.devcontainer/.env`:
   ```env
   INSTALL_XDEBUG=true
   ```
2. **Rebuild** o container (necessário para instalar Xdebug)
3. Configure sua IDE para usar porta 9003

### 🔹 Usar Porta Diferente

**Cenário**: Porta 80 está ocupada ou você quer usar 8080.

**Solução**:
1. Edite `.devcontainer/.env`:
   ```env
   APACHE_PORT=8080
   ```
2. Edite `.devcontainer/devcontainer.json`:
   ```json
   "forwardPorts": [8080, 3306]
   ```
3. Rebuild o container

---

## 🐛 Troubleshooting

### Apache não inicia

**Sintoma**: Apache falha ao iniciar ou retorna erro 500.

**Soluções**:
1. Verifique logs: `tail -f /var/log/apache2/error.log`
2. Verifique permissões do DocumentRoot:
   ```bash
   ls -la /workspaces/seu-repo/public
   ```
3. Teste configuração do Apache:
   ```bash
   apache2ctl configtest
   ```

### MySQL não conecta

**Sintoma**: Erro de conexão ou "Access denied".

**Soluções**:
1. Verifique se o serviço está rodando:
   ```bash
   service mariadb status
   ```
2. Teste conexão:
   ```bash
   mysql -u root -p${MYSQL_ROOT_PASSWORD}
   ```
3. Reconfigure MySQL:
   ```bash
   configure-mysql.sh
   ```

### phpMyAdmin retorna erro de blowfish

**Sintoma**: "The configuration file now needs a secret passphrase (blowfish_secret)"

**Soluções**:
1. Gere um novo secret:
   ```bash
   openssl rand -base64 32
   ```
2. Atualize no `.env`:
   ```env
   PHPMYADMIN_BLOWFISH_SECRET=seu_novo_secret_de_32_caracteres
   ```
3. Reconfigure:
   ```bash
   configure-phpmyadmin.sh
   ```

### DocumentRoot não atualiza

**Sintoma**: Apache continua servindo o diretório antigo.

**Soluções**:
1. Execute reload:
   ```bash
   bash .devcontainer/reload-services.sh
   ```
2. Se não funcionar, reconfigure Apache manualmente:
   ```bash
   configure-apache.sh /workspaces/seu-repo
   ```

---

## 🎓 Boas Práticas

### ✅ Segurança

- ⚠️ **Nunca commite o arquivo `.env`** com senhas reais
- Use senhas fortes para produção
- Desabilite `PHP_DISPLAY_ERRORS` em produção
- Use `PHPMYADMIN_ALLOW_NO_PASSWORD=false`

### ✅ Performance

- Ajuste `PHP_MEMORY_LIMIT` conforme necessário
- Habilite cache do PHP (OPcache) em produção
- Use `APACHE_INDEXES=false` em produção

### ✅ Desenvolvimento

- Use `APP_DEBUG=true` apenas em desenvolvimento
- Mantenha logs ativos para troubleshooting
- Teste mudanças com `reload-services.sh` antes de rebuild

---

## 📞 Suporte e Comandos Úteis

### Logs Importantes

```bash
# Apache
tail -f /var/log/apache2/error.log
tail -f /var/log/apache2/access.log

# MySQL
tail -f /var/log/mysql/error.log

# PHP
tail -f /var/log/php_errors.log
```

### Comandos Úteis

```bash
# Verificar status dos serviços
service apache2 status
service mariadb status

# Testar configuração Apache
apache2ctl configtest

# Verificar versão PHP
php -v

# Listar extensões PHP
php -m

# Verificar configurações PHP
php -i | grep -i "memory_limit\|upload_max"

# Conectar ao MySQL
mysql -u root -p
```

---

## 📝 Changelog

### v2.0.0 - Sistema Modular (2024)
- ✨ Adicionado sistema completo de configuração via `.env`
- ✨ Scripts modulares para cada serviço
- ✨ Script de reload sem rebuild
- ✨ Logs coloridos e informativos
- ✨ Documentação completa
- ✨ Suporte a múltiplas configurações
- ✨ Build arguments para Xdebug e Node.js

### v1.0.0 - Versão Inicial
- Configuração básica do ambiente
- Scripts monolíticos

---

## 📄 Licença

Este template é de código aberto e pode ser usado livremente em seus projetos.
