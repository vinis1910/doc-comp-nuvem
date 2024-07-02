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

1. **Servidor Web**: Garanta que você tenha um servidor web configurado e pronto para hospedar aplicativos PHP. Exemplos comuns incluem Apache, Nginx, ou servidores integrados como o servidor embutido do PHP.

2. **MySQL**: Verifique se você tem um servidor MySQL configurado e acessível pela aplicação. As configurações de conexão com o banco de dados devem estar corretamente definidas no arquivo `config.php`.

3. **PHP**: Certifique-se de ter o PHP instalado no servidor com as extensões necessárias para executar a aplicação PHP.

4. **Código Fonte**: Clone ou copie o código fonte da aplicação comp-nuvem para o diretório raiz do servidor web.

Configuração do Banco de Dados
-------------------------------

A aplicação comp-nuvem utiliza um banco de dados MySQL. Antes de iniciar o deploy, execute as seguintes etapas:

1. **Criação do Banco de Dados**: Execute o script `company.sql` no MySQL para criar o esquema necessário:

   ```sql
   CREATE TABLE employees (
       id INT NOT NULL PRIMARY KEY AUTO_INCREMENT,
       name VARCHAR(100) NOT NULL,
       address VARCHAR(255) NOT NULL,
       salary INT(10) NOT NULL
   );
