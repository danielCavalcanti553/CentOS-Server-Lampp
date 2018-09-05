# CentOS-Server-Lampp

* Download Software Putty (portable)


1. Atualzar pacotes Yum
	
	yum update -y

2. Configurar o servidor SSH
	
	> INSTALAÇÃO
	
	yum install -y openssh openssh-server

	> Habilitar Serviço e Firewall
	firewall-cmd --list-service | grep ssh
	firewall-cmd --add-service ssh
	firewall-cmd --reload

3. Verificar se as conexões estão ok (Básico)
	> Execute o comando 
	nmtui

4. Abrir o Putty
	> IP: 127.0.1.1
	> Port: 22
	> OK
	> Login: root

EXECUTAR OS COMANDOS A SEGUIR NO PUTTY
(Acesso Remoto)

PLATAFORMA LAMP

5. Adicionar repositório EPEL
rpm --import /etc/pki/rpm-gpg/RPM-GPG-KEY*
yum -y install epel-release

6. Instalar o Mysql (MariaDB)
yum -y install mariadb-server mariadb

	> INICIAR SERVIÇO E INICIALIZAÇÃO
	systemctl start mariadb.service
	systemctl enable mariadb.service

	> CONFIGURAR MYSQL
	* Senha deixar em branco
	* Sequência Opções
	mysql_secure_installation
	> Set root password > Y
	> Remove anonymous > Y
	> Disallow Root remote > N
	> Test database e acess > N
	> Reload privilege > Y
	
7. Instalar o Servidor Apache
	yum -y install httpd
	
	> INICIAR SERVIÇO E INICIALIZAÇÃO
	systemctl start httpd.service
	systemctl enable httpd.service

	> FIREWALL
firewall-cmd --permanent --zone=public --add-service=http

firewall-cmd --permanent --zone=public --add-service=https

firewall-cmd --permanent --add-port=80/tcp

firewall-cmd --permanent --add-port=443/tcp

firewall-cmd --reload

	> TESTAR NO TERMINAL
	systemctl status httpd

	> TESTAR NO HOSPEDEIRO 
	(WIndows - Navegador)
	127.0.1.1

7. Instalar o PHP 7
	\rpm -Uvh https://dl.fedoraproject.org/pub/epel/epel-release-latest-7.noarch.rpm
	rpm -Uvh https://mirror.webtatic.com/yum/el7/webtatic-release.rpm
	systemctl restart httpd.service
	yum install php70w
	systemctl restart httpd

	> TESTAR O PHP
	1. Criar um arquivo na pasta /html com o editor vi do Linux
	vi /var/www/html/info.php

	2. Na tela que abrir, aperte o botão INSERT do teclado
	digite: <?php phpinfo(); ?>

	3. Salvar e Sair
		> Aperte CTRL + C (2 vezes) 
		> Digite :wq 
		> <Enter>
	4. Testar no navegador
		127.0.1.1/info.php
