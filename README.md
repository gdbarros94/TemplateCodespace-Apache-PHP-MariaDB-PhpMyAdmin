# 🚀 Template Codespace: Apache + PHP + MariaDB + phpMyAdmin

> Ambiente de desenvolvimento completo e configurável para PHP com Apache, MySQL/MariaDB e phpMyAdmin

[![GitHub Codespaces](https://img.shields.io/badge/Codespaces-Ready-brightgreen?logo=github)](https://github.com/codespaces)
[![PHP](https://img.shields.io/badge/PHP-8.2-777BB4?logo=php&logoColor=white)](https://www.php.net/)
[![Apache](https://img.shields.io/badge/Apache-2.4-D22128?logo=apache&logoColor=white)](https://httpd.apache.org/)
[![MariaDB](https://img.shields.io/badge/MariaDB-10.11-003545?logo=mariadb&logoColor=white)](https://mariadb.org/)

## ✨ Características

- 🎯 **Configuração via `.env`** - Controle total sobre o ambiente
- 🔧 **Arquitetura modular** - Scripts independentes para cada serviço
- 🗄️ **MySQL/MariaDB** - Banco de dados com usuários e permissões personalizáveis
- 🌐 **Apache** - Servidor web com DocumentRoot configurável
- 🐘 **PHP 8.2** - Com extensões comuns pré-instaladas
- 📊 **phpMyAdmin** - Interface web para gerenciar bancos de dados
- ⚡ **Reload sem rebuild** - Aplique mudanças sem reconstruir o container
- 📝 **Logs coloridos** - Feedback visual durante configuração
- 🛠️ **Extensível** - Suporte opcional para Xdebug e Node.js

## 🚀 Início Rápido

### 1. Criar `.env` a partir do template

```bash
cp .devcontainer/.env.example .devcontainer/.env
```

### 2. Personalizar configurações (opcional)

Edite `.devcontainer/.env` conforme necessário:

```env
# MySQL
MYSQL_ROOT_PASSWORD=sua_senha_root
MYSQL_DATABASE=seu_banco
MYSQL_USER=seu_usuario
MYSQL_PASSWORD=sua_senha

# Apache
APACHE_DOCUMENT_ROOT=public
APACHE_PORT=80

# PHP
PHP_MEMORY_LIMIT=256M
PHP_UPLOAD_MAX_FILESIZE=64M
```

### 3. Iniciar Codespace

No GitHub: **Code** → **Codespaces** → **Create codespace**

O ambiente será configurado automaticamente! 🎉

### 4. Acessar serviços

- **Aplicação**: `http://localhost:80`
- **phpMyAdmin**: `http://localhost:80/phpmyadmin`
- **MySQL**: `localhost:3306`

## 📋 Configurações Disponíveis

### MySQL/MariaDB

```env
MYSQL_ROOT_PASSWORD=root          # Senha do root
MYSQL_DATABASE=devdb              # Nome do banco
MYSQL_USER=devuser                # Usuário do banco
MYSQL_PASSWORD=devpass            # Senha do usuário
MYSQL_HOST=127.0.0.1              # Host
MYSQL_PORT=3306                   # Porta
MYSQL_CHARSET=utf8mb4             # Charset
MYSQL_COLLATION=utf8mb4_unicode_ci # Collation
```

### Apache

```env
APACHE_DOCUMENT_ROOT=public       # Pasta raiz (relativa ou absoluta)
APACHE_PORT=80                    # Porta do servidor
APACHE_SERVER_NAME=localhost      # Nome do servidor
APACHE_ALLOW_OVERRIDE=true        # Habilitar .htaccess
APACHE_INDEXES=true               # Listagem de diretórios
APACHE_REWRITE=true               # mod_rewrite
```

### PHP

```env
PHP_DISPLAY_ERRORS=On             # Exibir erros
PHP_ERROR_REPORTING=E_ALL         # Nível de erro
PHP_UPLOAD_MAX_FILESIZE=64M       # Upload máximo
PHP_POST_MAX_SIZE=64M             # POST máximo
PHP_MEMORY_LIMIT=256M             # Limite de memória
PHP_MAX_EXECUTION_TIME=300        # Tempo de execução
```

### Ferramentas de Desenvolvimento

```env
INSTALL_XDEBUG=false              # Instalar Xdebug
INSTALL_NODEJS=false              # Instalar Node.js
NODEJS_VERSION=20                 # Versão do Node.js
TZ=America/Sao_Paulo              # Timezone
```

## 🔄 Aplicar Mudanças no `.env`

Após editar o `.env`, aplique as mudanças sem rebuild:

```bash
bash .devcontainer/reload-services.sh
```

## 📁 Estrutura do Projeto

```
.
├── .devcontainer/
│   ├── .env.example              # Template de configuração
│   ├── .env                      # Suas configurações (git-ignored)
│   ├── Dockerfile                # Imagem Docker
│   ├── devcontainer.json         # Config do devcontainer
│   ├── init.sh                   # Script de inicialização
│   ├── reload-services.sh        # Reload sem rebuild
│   ├── configure-mysql.sh        # Configuração MySQL
│   ├── configure-apache.sh       # Configuração Apache
│   ├── configure-php.sh          # Configuração PHP
│   ├── configure-phpmyadmin.sh   # Configuração phpMyAdmin
│   ├── CONFIGURATION.md          # Documentação completa
│   └── docs.md                   # Documentação original
├── public/                       # DocumentRoot padrão (será criado)
│   └── index.php                 # Arquivo de exemplo
└── README.md                     # Este arquivo
```

## 💡 Casos de Uso

### Alterar DocumentRoot

```env
# .devcontainer/.env
APACHE_DOCUMENT_ROOT=www/public
```

```bash
bash .devcontainer/reload-services.sh
```

### Aumentar Limite de Upload

```env
# .devcontainer/.env
PHP_UPLOAD_MAX_FILESIZE=256M
PHP_POST_MAX_SIZE=256M
```

```bash
bash .devcontainer/reload-services.sh
```

### Habilitar Xdebug

```env
# .devcontainer/.env
INSTALL_XDEBUG=true
```

⚠️ **Requer rebuild** do container

### Criar Múltiplos Bancos

```bash
mysql -u root -p${MYSQL_ROOT_PASSWORD}
```

```sql
CREATE DATABASE segundo_banco CHARACTER SET utf8mb4;
GRANT ALL PRIVILEGES ON segundo_banco.* TO 'seu_usuario'@'localhost';
```

## 🛠️ Scripts Modulares

| Script | Descrição |
|--------|-----------|
| `init.sh` | Inicialização completa do ambiente |
| `configure-mysql.sh` | Configura MySQL/MariaDB |
| `configure-apache.sh` | Configura Apache |
| `configure-php.sh` | Configura PHP |
| `configure-phpmyadmin.sh` | Configura phpMyAdmin |
| `reload-services.sh` | Reaplica configurações e reinicia serviços |

Todos os scripts podem ser executados individualmente:

```bash
configure-mysql.sh
configure-apache.sh /workspaces/seu-repo
configure-php.sh
configure-phpmyadmin.sh
```

## 🐛 Troubleshooting

### Verificar logs

```bash
# Apache
tail -f /var/log/apache2/error.log

# MySQL
tail -f /var/log/mysql/error.log

# PHP
tail -f /var/log/php_errors.log
```

### Verificar status dos serviços

```bash
service apache2 status
service mariadb status
```

### Testar configuração do Apache

```bash
apache2ctl configtest
```

### Conectar ao MySQL

```bash
mysql -u root -p${MYSQL_ROOT_PASSWORD}
mysql -u ${MYSQL_USER} -p${MYSQL_PASSWORD} ${MYSQL_DATABASE}
```

## 📚 Documentação Completa

Para documentação detalhada, veja:
- [CONFIGURATION.md](.devcontainer/CONFIGURATION.md) - Guia completo de configuração
- [docs.md](.devcontainer/docs.md) - Documentação original

## 🎓 Boas Práticas

- ⚠️ **Nunca commite o arquivo `.env`** com senhas reais
- ✅ Use senhas fortes, especialmente em produção
- ✅ Desabilite `PHP_DISPLAY_ERRORS` em produção
- ✅ Configure `PHPMYADMIN_ALLOW_NO_PASSWORD=false`
- ✅ Ajuste limites de PHP conforme necessário
- ✅ Use `reload-services.sh` para testar mudanças antes de rebuild

## 🤝 Contribuindo

Sinta-se à vontade para abrir issues e pull requests!

## 📄 Licença

Este template é de código aberto e pode ser usado livremente.

---

**Desenvolvido com ❤️ para facilitar o desenvolvimento PHP**
