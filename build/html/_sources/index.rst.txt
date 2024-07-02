.. comp-nuvem-doc documentação principal, criado por
   sphinx-quickstart em Ter 1 Jul 10:00:00 2024.
   Você pode adaptar este arquivo completamente ao seu gosto, mas ele deve conter ao menos
   a diretiva raiz `toctree`.

Bem-vindo à documentação do comp-nuvem-doc!
===========================================

.. toctree::
   :maxdepth: 2
   :caption: Conteúdo:

   introducao
   arquivos-da-api
   conexao-com-mysql

Índices e tabelas
==================

* :ref:`genindex`
* :ref:`modindex`
* :ref:`search`

Introdução
----------

.. _introducao:

Esta documentação fornece uma visão geral da aplicação comp-nuvem, que é uma aplicação PHP utilizando MySQL como banco de dados.

Arquivos da API
---------------

.. _arquivos-da-api:

Os seguintes arquivos fazem parte da API:

- `company.sql`: Arquivo SQL que define o esquema do banco de dados.
- `config.php`: Arquivo PHP contendo a configuração de conexão com o banco de dados.
- `create.php`, `read.php`, `update.php`, `delete.php`: Arquivos PHP para operações CRUD no banco de dados.

Conexão com MySQL
------------------

.. _conexao-com-mysql:

Para conectar ao MySQL, verifique se possui as seguintes credenciais de banco de dados configuradas no arquivo `config.php`:

```php
<?php
define('DB_SERVER', 'localhost');
define('DB_USERNAME', 'root');
define('DB_PASSWORD', '');
define('DB_NAME', 'demo');

$link = mysqli_connect(DB_SERVER, DB_USERNAME, DB_PASSWORD, DB_NAME);

if($link === false){
    die("ERRO: Não foi possível conectar. " . mysqli_connect_error());
}
?>
