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

1. **Instalação do MySQL**: Caso o MySQL não esteja instalado, siga as instruções específicas para o seu sistema operacional para instalar o MySQL Server.

2. **Acesso ao MySQL**: Utilize o cliente MySQL ou a linha de comando para acessar o servidor MySQL. Por exemplo, no terminal:

   .. code-block:: bash

      mysql -u root -p

   Isso abrirá o cliente MySQL e solicitará a senha do usuário root.

3. **Criação de um Novo Usuário**: Se desejar criar um novo usuário para a aplicação, execute o seguinte comando SQL no MySQL:

   .. code-block:: sql

      CREATE USER 'novousuario'@'localhost' IDENTIFIED BY 'senha';

   Substitua ``novousuario`` pelo nome de usuário desejado e ``senha`` pela senha desejada para o novo usuário.

4. **Concessão de Privilégios**: Conceda privilégios ao novo usuário para o banco de dados utilizado pela aplicação. Por exemplo, para conceder todos os privilégios ao novo usuário no banco de dados ``demo``:

   .. code-block:: sql

      GRANT ALL PRIVILEGES ON demo.* TO 'novousuario'@'localhost';

   Certifique-se de substituir ``demo`` pelo nome do banco de dados da sua aplicação.

5. **Atualização das Configurações**: No arquivo ``config.php`` da aplicação, atualize as credenciais de conexão com o banco de dados para refletir o novo usuário criado:

   .. code-block:: php

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

6. **Troca de Usuário no MySQL**: Para trocar de usuário no MySQL durante a sessão, utilize o comando ``USE`` seguido do nome do banco de dados desejado:

   .. code-block:: sql

      USE outrobanco;

   Isso mudará o contexto atual para o banco de dados especificado, permitindo que você execute consultas e operações dentro dele.
