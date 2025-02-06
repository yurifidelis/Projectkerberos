Este projeto tem como objetivo integrar o Samba, o Nextcloud e o Debian para funcionar de maneira eficiente e segura com autenticação via LDAP. Além disso, utilizamos a ferramenta ADExplorer para facilitar a manipulação de usuários dentro da estrutura.

A primeira etapa envolve a atualização do sistema Debian para garantir que todos os pacotes estejam na versão mais recente.

Em seguida,  pilha LAMP (Linux, Apache, MySQL/MariaDB e PHP), essencial para o funcionamento do Nextcloud. O Apache é configurado como servidor web, enquanto o MariaDB gerencia o banco de dados.

adicionamos repositórios e instalamos extensões do PHP para garantir a compatibilidade com o Nextcloud. Após a instalação, verificamos a versão do PHP instalada.

A instalação do servidor MariaDB, essencial para armazenar as informações do Nextcloud. Em seguida, criamos o banco de dados e o usuário responsável pela administração do Nextcloud no banco de dados.

Após isso, fazemos o download da versão mais recente do Nextcloud e configuramos as permissões necessárias para que o Apache possa gerenciar os arquivos corretamente.

Para a configuração do Apache para hospedar o Nextcloud. Criamos um arquivo de configuração específico, definindo o domínio local e os diretórios necessários. Também ativamos os módulos essenciais do Apache e verificamos a integridade da configuração.

Além disso, para permitir a autenticação via LDAP no Nextcloud, é necessário instalar o plugin LDAP disponível na loja de aplicativos do Nextcloud. Após a instalação do plugin, devemos configurar informações essenciais do servidor LDAP, como o endereço IP, o nome do domínio e outras credenciais necessárias para garantir a autenticação dos usuários.

Outro ponto importante é que a máquina virtual utilizada para rodar o Debian está configurada com a placa de rede em modo Host-Only e NAT. Isso garante a comunicação adequada entre os serviços e permite o acesso ao Nextcloud tanto localmente quanto via rede externa. O IP de acesso à interface gráfica do Nextcloud é 192.168.56.11.

Por fim, acessamos o Nextcloud via navegador, finalizamos a configuração e criamos o primeiro usuário administrador. Com essa infraestrutura, conseguimos garantir uma integração eficiente entre Samba, Nextcloud e Debian, possibilitando a autenticação via LDAP e facilitando a administração de usuários com a ferramenta ADExplorer.