# Projeto de integração ldap
Este projeto tem como objetivo integrar o Samba, o Nextcloud e o Debian para funcionar de maneira eficiente e segura com autenticação via LDAP. Além disso, utilizamos a ferramenta ADExplorer para facilitar a manipulação de usuários dentro da estrutura.

O primeiro passo envolve a atualização do sistema Debian para garantir que todos os pacotes estejam na versão mais recente.

Em seguida, pilha ___LAMP (Linux, Apache, MySQL/MariaDB e PHP)___, essencial para o funcionamento do Nextcloud. O Apache é configurado como servidor web, enquanto o MariaDB gerencia o banco de dados.

Um passo importante nesse processo é a instalação de algumas extensões do PHP para garantir a compatibilidade com o Nextcloud. Após a instalação, podemos ver a versão do PHP instalada, sendo ela a ___8.1___.

A instalação do serviço ___MariaDB___, essencial para armazenar as informações do Nextcloud. Em seguida, criamos o banco de dados e o usuário responsável pela administração do Nextcloud no banco de dados.

Após isso, fazemos o download da versão mais recente do Nextcloud, que no momento é a ___30.0.2___, e configuramos as permissões necessárias para que o Apache possa gerenciar os arquivos corretamente.

Para a configuração do Apache para hospedar o Nextcloud. Criamos um arquivo de configuração específico, definindo o domínio local e os diretórios necessários. Também ativamos os módulos essenciais do Apache e verificamos a integridade da configuração.

Além disso, para permitir a autenticação via LDAP no Nextcloud, é necessário instalar o ___plugin LDAP___ disponível na loja de aplicativos do Nextcloud. Após a instalação do plugin, devemos configurar informações essenciais do servidor LDAP, como o endereço IP, o nome do domínio e outras credenciais necessárias para garantir a autenticação dos usuários.

Outro ponto importante é que a máquina virtual utilizada para rodar o Debian está configurada com a placa de rede em modo ___Host-Only___ e ___NAT___. Isso garante a comunicação adequada entre os serviços e permite o acesso ao Nextcloud tanto localmente quanto via rede externa. O IP de acesso à interface gráfica do Nextcloud é ___192.168.56.11___.

As máquinas virtuais que hospedam o Nextcloud e o Samba estão configuradas no VirtualBox e utilizam o firewall UFW para liberar a porta ___389___, garantindo a comunicação adequada para a autenticação via LDAP. O arquivo de configuração do Samba ___(smb.conf)___ foi devidamente ajustado para permitir essa integração sem conflitos.

Além disso, criamos uma nova Unidade Organizacional (OU) no Samba chamada ___"SystemUsers"___. Dentro dessa OU, configuramos um usuário específico, denominado ___"Bind.nextcloud"___, que é utilizado para estabelecer a conexão entre o Nextcloud e o servidor LDAP, garantindo autenticação segura e eficiente.

Por fim, acessamos o Nextcloud via navegador, finalizamos a configuração e criamos o primeiro usuário administrador. Com essa infraestrutura, conseguimos garantir uma integração eficiente entre Samba, Nextcloud e Debian, possibilitando a autenticação via LDAP e facilitando a administração de usuários com a ferramenta ADExplorer.
## A importancia da integração.
A integração do LDAP ao Nextcloud proporciona diversas vantagens para a gestão de usuários e compartilhamento de arquivos. O Samba é uma excelente escolha para essa implementação, pois permite a integração direta com o Active Directory, facilitando a administração centralizada de usuários e grupos. Com o Nextcloud configurado para autenticação via LDAP, é possível garantir um controle de acesso unificado, simplificando o gerenciamento de permissões e aumentando a segurança da plataforma. Além disso, essa integração possibilita o compartilhamento eficiente de arquivos entre usuários autenticados via Active Directory, promovendo maior colaboração dentro da organização. Dessa forma, a combinação entre Samba, Nextcloud e LDAP oferece uma solução robusta, segura e escalável para ambientes corporativos que necessitam de um gerenciamento eficiente de identidade e compartilhamento de dados.