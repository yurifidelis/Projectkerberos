## Documentação do Nextcloud
<h1> Primeira etapa </h1>
#### Atualização pelo bando de dados do debian
 <code> sudo apt-get update -y && sudo apt-get upgrade -y </code>
<h1> segunda etapa </h1>
#### Instalando a pilha LAMP
<p> Primeiro de tudo, instalei o apache2 usando o codigo: </p>
 <code> sudo apt-get install apache2 -y </code>

<p> Abaixo temos o status do apache2 no debian, para isso utilizamos o seguinte codigo. </p>
<code> sudo systemctl status apache2 </code>

<code> apache2.service - The Apache HTTP Server
     Loaded: loaded (/lib/systemd/system/apache2.service; enabled; vendor preset: enabled)
     Active: active (running) since Wed 2023-03-08 17:35:28 CST; 5s ago
       Docs: https://httpd.apache.org/docs/2.4/
    Process: 39464 ExecStart=/usr/sbin/apachectl start (code=exited, status=0/SUCCESS)
   Main PID: 39469 (apache2)
      Tasks: 6 (limit: 4675)
     Memory: 12.3M
        CPU: 325ms
     CGroup: /system.slice/apache2.service 
</code>
<h1> terceira etapa </h1>
### instalando as extensões do PHP 
<p> Esse código serve para instalar os repositorios por meios de fontes seguras. </p>
<code> apt -y install lsb-release apt-transport-https ca-certificates </code>

<p> Esse código serve para instalar os repositorios por meios de fontes seguras. </p>
<code> wget -O /etc/apt/trusted.gpg.d/php.gpg https://packages.sury.org/php/apt.gpg </code>
 
<p> Adicionando a chave GPG no repositorio padrão </p> 
<code> echo "deb https://packages.sury.org/php/ $(lsb_release -sc) main" | tee /etc/apt/sources.list.d/php.list </code>

<p> Instalando as extensões do php </p>
<code> sudo apt-get install php8.3 php8.1-common php8.3-curl libapache2-mod-php php8.3-imap php8.3-redis php8.1-cli php8.3-snmp php8.3-xml php8.3-zip php8.3-mbstring php8.3-gd php8.3-xml php8.3-mysql php-mbstring -y </code>

Apois a instalação do php, podemos verificar a versão instalada com o comando:
<code> PHP -v </code>

<h1> Quarta etapa </h1>

#### Serviço MariaDB
<p> Utilizando o comando seguinte, instalei o serviço Mariadb.</p>
  <code> sudo apt-get install mariadb-server -y </code>

<h1> Quinta etapa </h1>

<p> Criação do banco de dados do Nextcloud e o usuario. </p>
<p>Criando o banco de dados:</p>
 <code> CREATE USER 'admin'@'localhost' IDENTIFIED BY 'Minha_senha'; </code> <br>
 <p>Criando o banco de dados:</p>
<code>CREATE DATABASE nextclouddb; </code> <br>
<code>GRANT ALL PRIVILEGES ON nextcloud.* TO 'nextcloud'@'localhost'; </code><br>
<p>Aplicando os privilegios:</p>
<code>FLUSH PRIVILEGES; </code><br>
<code>EXIT; </code>
  
<h1> Sexta etapa</h1>
### Download do nextcloud
<p>Abrindo o diretório que vai ficar o arquivo raiz do nextcloud.</p>
<code> cd /var/www/html </code>
<p>Depois que estiver no diretório, você deve baixa a versão mais atual do serviço.</p>
<code>wget https://download.nextcloud.com/server/releases/nextcloud-30.0.2.zip</code>
<p> Instale o zip no debian com o seguinte comando para para descompactar o arquivo.</p>
<code>apt-get install -y zip</code>

<p>Descompatando os arquivos</p>
<code>Unzip nextcloud-30.0.2.zip</code>

<p>Dando as permissões aos arquivos.</p>
<code> chown -R www-data:www-data nextcloud/</code>

<h1>setima etapa</h1>
### Criação de um arquivo de configuração no diretorio do apache para o nextcloud.
<p> Primeiramente iremos ate o diretorio do apache2.</p>
<code>cd /etc/apache2/sites-available/</code>

<p> Criaremos um arquivo de configuração dentro desse diretório.</p>
<code> touch nextcloud.conf</code>

<p> Abra o arquivo com o nano ou vim.</p>
<code>nano nextcloud.conf</code>
<code>
<p>Você deve deixar parecido o seu arquivo de configuração.</code>
<VirtualHost *:80>
ServerName nextcloudlocal.com
DocumentRoot /var/www/html/nextcloud


<Directory /var/www/html/nextcloud>
AllowOverride All
</Directory>

ErrorLog ${APACHE_LOG_DIR}/error.log
CustomLog ${APACHE_LOG_DIR}/access.log combined

</VirtualHost>
</code>
<p>Habilitando a configuração do apache par ao nextcloud</p>
<p> desativando o arquivo padrão do apache2.</p>
<code>a2dissite 000-default.conf</code>
<code>sudo a2enmod rewrite</code>
<p>Habilitando o novo arquivo de configuração.</code>
<code>sudo a2ensite nextcloud.conf</code>

<p>Checando se está tudo em ordem, com o comando:</p>
<code>apachectl -t</code>
<br>
<Code>
root@vps:~# apachectl -t
Syntax OK
</code>

<h1> Oitava parte</h1>
### Finalização da instalação.
<p>Acesse o nextcloud pelo dominio que está alocado e adicione o login do adminstrador e a senha para futuros acessos.</p>
