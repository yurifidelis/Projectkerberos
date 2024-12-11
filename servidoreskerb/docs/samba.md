## Documentação da instalação do samba-ad-dc no debian 12

<p>Primeiramente instalei alguns pacotes necessarios do kerberos juntamente com o samba, usando o seguindo comando:
<code> 
sudo apt-get install samba krb5-user krb5-config winbind libpam-winbind libnss-winbind</code>

<h1>Segunda etapa</h1>
<p>Assim que terminou a instalação, desabilitei e parei os processos do samba.</p>
<code>
$ sudo systemctl stop samba-ad-dc.service smbd.service nmbd.service winbind.service <br>$ sudo systemctl disable samba-ad-dc.service smbd.service nmbd.service winbind.service 
</code>
<p>Proximo passo, devemos remover ou renomear o arquivo de configuração antigo o samba, para que não ocorra um erro.</p>
<code>$ sudo mv /etc/samba/smb.conf /etc/samba/smb.conf.initial</code>
<p>Usaremos o proximo comando para criar o domain, realm, senha para o adminstrador do dominio de forma interativa. Algumas perguntas, eu deixei marcado o padrão, por exemplo o dns.</p>
<code>$ sudo samba-tool domain provision --use-rfc2307 --interactive</code>

<p>Meu realm é 'Chilelocal' e meu dominio é Santiago</p>

<h1>Terceira etapa</h1>
<p>Remoção do arquivo antigo do kerberos do diretório /etc e linkando o novo que foi gerado pelo samba. O novo arquivo se encontra em /var/lib/samba/private</p>
<p>Usei o seguinte comando para fazer os procedimentos</p>
<code>
$ sudo mv /etc/krb5.conf /etc/krb5.conf.initial
$ sudo ln -s /var/lib/samba/private/krb5.conf /etc/
</code>

<h1>Quarta etapa</h1>
<p>Iniciando o serviço samba</p>
<code>
-$ sudo systemctl start samba-ad-dc.service
-$ sudo systemctl status samba-ad-dc.service
-$ sudo systemctl enable samba-ad-dc.service
</code>

<p>Usando o comando a baixo, podemos observar o dominio.</p>
<code>$ sudo samba-tool domain level show</code>
