# Projeto de integração ldap
Este projeto tem como objetivo integrar o Samba, o Nextcloud e o Debian para funcionar de maneira eficiente e segura com autenticação via LDAP. Além disso, utilizamos a ferramenta ADExplorer para facilitar a manipulação de usuários dentro da estrutura.

![ADexplorer](/assets/imgadexplore.png)

O primeiro passo envolve a atualização do sistema Debian para garantir que todos os pacotes estejam na versão mais recente.

Em seguida, pilha **LAMP (Linux, Apache, MySQL/MariaDB e PHP)**, essencial para o funcionamento do Nextcloud. O Apache é configurado como servidor web, enquanto o MariaDB gerencia o banco de dados.

Um passo importante nesse processo é a instalação de algumas extensões do PHP para garantir a compatibilidade com o Nextcloud. Após a instalação, podemos ver a versão do PHP instalada, sendo ela a **8.3.14**.
![ADexplorer](/assets/extensoesphp.png)

![ADexplorer](/assets/phpversao.png)

A instalação do serviço ___MariaDB___, essencial para armazenar as informações do Nextcloud. Em seguida, criamos o banco de dados e o usuário responsável pela administração do Nextcloud no banco de dados.

![MariaDB](/assets/installmaria.png)

Após isso, fazemos o download da versão mais recente do Nextcloud, que no momento é a **30.0.5**, e configuramos as permissões necessárias para que o Apache possa gerenciar os arquivos corretamente.

Para a configuração do Apache para hospedar o Nextcloud. Criamos um arquivo de configuração específico, definindo o domínio local e os diretórios necessários. Também ativamos os módulos essenciais do Apache e verificamos a integridade da configuração.

Além disso, para permitir a autenticação via LDAP no Nextcloud, é necessário instalar o **plugin LDAP** disponível na loja de aplicativos do Nextcloud.
![ADexplorer](/assets/plug.jpeg)
 Após a instalação do plugin, devemos configurar informações essenciais do servidor LDAP, como o endereço IP, o nome do domínio e outras credenciais necessárias para garantir a autenticação dos usuários.
![ADexplorer](/assets/paginteg.jpeg)
Outro ponto importante é que as máquinas virtuais utilizadas para rodarem o Debian e o alpine estão configurada com a placa de rede em modo **Host-Only** e **NAT**. 
![ADexplorer](/assets/interfacesderede.png)

Isso garante a comunicação adequada entre os serviços e permite o acesso ao Nextcloud tanto localmente quanto via rede externa. O IP de acesso à interface gráfica do Nextcloud é **192.168.56.11**.

![ip](/assets/Screenshot_3.png)

As máquinas virtuais que hospedam o Nextcloud e o Samba estão configuradas no VirtualBox e utilizam o firewall UFW para liberar a porta **389**, garantindo a comunicação adequada para a autenticação via LDAP. O arquivo de configuração do Samba ___(smb.conf)___ foi devidamente ajustado para permitir essa integração sem conflitos.

![portas](/assets/portas.png)
![ADexplorer](/assets/confdonext.png)

Além disso, temos uma Unidade Organizacional (OU) no Samba chamada **"Users"**.
![ADexplorer](/assets/users.png)

 Dentro dessa OU, configuramos um usuário específico, denominado **"Bind.nextcloud"**, que é utilizado para estabelecer a conexão entre o Nextcloud e o servidor LDAP, garantindo autenticação segura e eficiente.

![ADexplorer](/assets/whats.jpeg)

Por fim, acessamos o Nextcloud via navegador, finalizamos a configuração e criamos o primeiro usuário administrador. Com essa infraestrutura, conseguimos garantir uma integração eficiente entre Samba, Nextcloud e Debian, possibilitando a autenticação via LDAP e facilitando a administração de usuários com a ferramenta ADExplorer.



## A importancia da integração.
A integração do LDAP ao Nextcloud proporciona diversas vantagens para a gestão de usuários e compartilhamento de arquivos. O Samba é uma excelente escolha para essa implementação, pois permite a integração direta com o Active Directory, facilitando a administração centralizada de usuários e grupos. Com o Nextcloud configurado para autenticação via LDAP, é possível garantir um controle de acesso unificado, simplificando o gerenciamento de permissões e aumentando a segurança da plataforma. Além disso, essa integração possibilita o compartilhamento eficiente de arquivos entre usuários autenticados via Active Directory, promovendo maior colaboração dentro da organização. Dessa forma, a combinação entre Samba, Nextcloud e LDAP oferece uma solução robusta, segura e escalável para ambientes corporativos que necessitam de um gerenciamento eficiente de identidade e compartilhamento de dados.