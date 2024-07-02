.. comp-nuvem-doc documentação principal, criado por
   sphinx-quickstart em Ter 1 Jul 10:00:00 2024.
   Você pode adaptar este arquivo completamente ao seu gosto, mas ele deve conter ao menos
   a diretiva raiz `toctree`.

Deploy da Aplicação comp-nuvem
===============================

Nesta seção, vamos abordar como realizar o deploy da aplicação comp-nuvem, que utiliza PHP e MySQL como banco de dados.

Configuração do Ambiente
-------------------------

Antes de iniciar o deploy, certifique-se de ter o ambiente configurado corretamente:

1. **Servidor Web**

   - **Instalação do Apache (Exemplo para sistemas baseados em Debian/Ubuntu):**

     ```bash
     sudo apt update
     sudo apt install apache2
     ```

   - **Instalação do PHP e Módulos Necessários:**

     ```bash
     sudo apt install php libapache2-mod-php php-mysql
     ```

   - **Verificação da Instalação:**

     Para verificar se o Apache está rodando, abra um navegador e visite `http://localhost`. Você deve ver a página padrão do Apache.

2. **MySQL**

   - **Instalação do MySQL Server (Exemplo para sistemas baseados em Debian/Ubuntu):**

     ```bash
     sudo apt update
     sudo apt install mysql-server
     ```

   - **Configuração Inicial do MySQL:**

     Durante a instalação, o MySQL solicitará uma senha para o usuário root do MySQL. Certifique-se de configurar uma senha forte.

   - **Acesso ao MySQL:**

     Use o cliente MySQL para acessar o servidor MySQL:

     ```bash
     mysql -u root -p
     ```

     Insira a senha definida durante a instalação.

3. **Código Fonte**

   - **Clone do Repositório da Aplicação:**

     Clone o repositório da aplicação comp-nuvem para o diretório raiz do servidor web (geralmente `/var/www/html/` no Apache):

     ```bash
     sudo git clone https://github.com/seu-usuario/comp-nuvem /var/www/html/comp-nuvem
     ```

Configuração do Banco de Dados
-------------------------------

A aplicação comp-nuvem utiliza um banco de dados MySQL. Antes de iniciar o deploy, execute as seguintes etapas:

1. **Criação do Banco de Dados e Tabelas**

   - **Acesso ao MySQL:**

     ```bash
     mysql -u root -p
     ```

   - **Criação do Banco de Dados:**

     ```sql
     CREATE DATABASE demo;
     ```

   - **Criação das Tabelas:**

     Utilize o arquivo SQL fornecido para criar as tabelas necessárias:

     ```bash
     mysql -u root -p demo < /var/www/html/comp-nuvem/api/company.sql
     ```

2. **Criação de um Novo Usuário**

   - **Criação do Usuário:**

     ```sql
     CREATE USER 'novousuario'@'localhost' IDENTIFIED BY 'senha';
     ```

   - **Concessão de Privilégios:**

     ```sql
     GRANT ALL PRIVILEGES ON demo.* TO 'novousuario'@'localhost';
     ```

   Certifique-se de substituir `senha` pela senha desejada para o novo usuário.

3. **Atualização das Configurações no Arquivo `config.php`**

   Edite o arquivo `config.php` da aplicação para refletir as novas credenciais de conexão:

   ```php
   <?php
   define('DB_SERVER', 'localhost');
   define('DB_USERNAME', 'novousuario');
   define('DB_PASSWORD', 'senha');
   define('DB_NAME', 'demo');

   $link = mysqli_connect(DB_SERVER, DB_USERNAME, DB_PASSWORD, DB_NAME);

   if($link === false){
       die("ERRO: Não foi possível conectar. " . mysqli_connect_error());
   }
   ?>
