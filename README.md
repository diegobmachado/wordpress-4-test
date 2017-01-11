# wordpress-4-test
Test for back-end job

##Login e senha
admin

1^C%t*sDbfGqftNTC*

##O que fazer

Criar um Post Type no Tema, Festas, contendo os seguintes itens:
 - Titulo
 - Descrição da Festa
 - Data da festa
 - Imagem destaque da festa
 - 3 fotos da festa

Gerar uma página contendo no minimo 2 posts do post type criado

Ao finalizar me enviar um merge request para avaliação.

### Atenção

Pode ser utilizado o Vagrant que tem no projeto, mas não envie nenhum arquivo referente a ele no Merge, apenas os do projeto/tema.

###Vagrant

Usado o vagrant-hostmanager, vagrant-cachier;

Para usar o Vagrant, instale [Hostmanager Plugin Vagrant]

```shell
$ vagrant plugin install vagrant-hostmanager
$ vagrant plugin install vagrant-cachier
```

Caso você tenha o wp-config.php na raiz do seu projeto, remova.

```shell
$ vagrant up
```

Após o Vagrant subir, devido a um problema no Apache, o projeto **NÃO** vai funcionar de primeira. Siga os seguintes passos via terminal:

```shell
$ vagrant ssh
```

Vai entrar na VM, dentro da VM siga com os commandos:

```shell
$ sudo -s
$ a2enmod rewrite ssl expires headers 
$ source /etc/apache2/envvars 
$ echo -e "DirectoryIndex index.php index.html \n \
<VirtualHost *:80> \n \
    ServerName wp-test.dev \n \
    DocumentRoot /var/www/wp-test.dev/www \n \
    <Directory "/var/www/wp-test.dev/www"> \n \
         AllowOverride All \n \
         Options -Indexes +FollowSymLinks \n \
         Require all granted \n \
    </Directory> \n \
</VirtualHost>" > /etc/apache2/sites-enabled/000-default.conf
$ /usr/sbin/apache2 -V
$ echo "ServerName localhost" | sudo tee /etc/apache2/conf-available/fqdn.conf
$ a2enconf fqdn
$ service apache2 restart
```

Pronto! Só acessar [WpTest] e codar!

[WpTest]: <http://wp-test.dev>
[PHP-Composer]: <https://getcomposer.org/download/>
[Search-Replace-DB]: https://github.com/interconnectit/Search-Replace-DB
[Hostmanager Plugin Vagrant]: <https://github.com/devopsgroup-io/vagrant-hostmanager>
[vagrant-cachier]: <https://github.com/fgrehm/vagrant-cachier>
[Prestissimo]: <https://github.com/hirak/prestissimo>