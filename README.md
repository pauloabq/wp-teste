# Introdução
- Obter um backup dos arquivos e um dump da base de dados (um dump .sql e um diretório com toda a estrutura de instalação do WP)
  - os backups do elementor já trazem a estrutura pronta de dump da base de dados e dos arquivos do wordpress
- Colocar o dump no diretório `./wp-database-dump`
- Colocar os arquivos do wordpress no diretório `./wp-files`
- Iniciar o container. A primeira instalação deve criar o banco e popular com os dados do dump
- Entrar no arquivo `wp-config.php`` e alterar dados de conexão, links e prefixo do database (para corresponder com o arquivo de dump)
	- Também é necessário desligar o HTTPS ($_SERVER['HTTPS'])
- Necessário plugin do elementor
- Instalar o plugin Pro Elements https://proelements.org/
  - Necessário antes adicionar arquivo `.htaccess` no mesmo diretório do arquivo `wp-config.php` com o conteúdo:
    ```
    php_value upload_max_filesize 512M
    php_value post_max_size 1024M
    ```
- Alterar URLs (https://url = url de onde veio a cópia de ambiente)
  ```
  update <prefixo>_posts 
     set guid = replace(guid, 'https://url','http://localhost:8000')
   where guid like '%https://url%';

  update <prefixo>_options 
     set option_value = replace(option_value , 'https://url','http://localhost:8000')
   where option_value like '%https://url%';

  ```
- Alterar as URLs (ex: redirecionamentos) Elementor > Tools > Replace URL

## Documentação oficial da imagem Docker
### MySql
[Link ](https://hub.docker.com/_/mysql)

- **MYSQL_DATABASE**: This variable is optional and allows you to specify the name of a database to be created on image startup

- **Initializing a fresh instance**: When a container is started for the first time, a new database with the specified name will be created and initialized with the provided configuration variables. Furthermore, it will execute files with extensions .sh, .sql and .sql.gz that are found in /docker-entrypoint-initdb.d

### Wordpress
[Link](https://hub.docker.com/_/wordpress)

