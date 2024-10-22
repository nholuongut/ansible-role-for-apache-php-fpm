# Ansible Role: Apache PHP-FPM

![](https://i.imgur.com/waxVImv.png)
### [View all Roadmaps](https://github.com/nholuongut/all-roadmaps) &nbsp;&middot;&nbsp; [Best Practices](https://github.com/nholuongut/all-roadmaps/blob/main/public/best-practices/) &nbsp;&middot;&nbsp; [Questions](https://www.linkedin.com/in/nholuong/)
<br/>

An Ansible Role that configures Apache for PHP-FPM usage on RHEL/CentOS and Debian/Ubuntu.

## Requirements

This role is dependent upon `nholuong.apache`, and also requires you have PHP running with PHP-FPM somewhere on the server or elsewhere (I usually configure PHP with the `nholuong.php` role).

When configuring your Apache virtual hosts, you can add the following line to any vhost definition to enable passthrough to PHP-FPM:

    # If using a TCP port:
    ProxyPassMatch ^/(.*\.php(/.*)?)$ "fcgi://127.0.0.1:9000/var/www/example"
    
    # If using a Unix socket:
    ProxyPassMatch ^/(.*\.php(/.*)?)$ "unix:/var/run/php5-fpm.sock|fcgi://localhost/var/www/example"

For a full usage example with the `nholuong.apache` role, see the Example Playbook later in this README.

### RedHat 6 and 7

RedHat/CentOS 7 automatically installs and enables mod_proxy_fcgi by default.

RedHat/CentOS 6 installs Apache 2.2, and is much harder to get configured with FastCGI, but here are two guides in case you need to support this use case:

  - [Apache 2.2 + mod_fastcgi](http://stackoverflow.com/a/21409702/100134)
  - [Apache 2.4 + mod_proxy_fcgi](http://unix.stackexchange.com/a/138903/16194)

## Role Variables

None.

## Dependencies

None.

## Example Playbook

    - hosts: webservers
    
      vars:
        php_enable_php_fpm: true
        apache_vhosts:
          - servername: "www.example.com"
            documentroot: "/var/www/example"
            extra_parameters: |
                  ProxyPassMatch ^/(.*\.php(/.*)?)$ "fcgi://127.0.0.1:9000/var/www/example"
    
      roles:
        - nholuong.apache
        - nholuong.php
        - nholuong.apache-php-fpm

# 🚀 I'm are always open to your feedback.  Please contact as bellow information:
### [Contact ]
* [Name: nho Luong]
* [Skype](luongutnho_skype)
* [Github](https://github.com/nholuongut/)
* [Linkedin](https://www.linkedin.com/in/nholuong/)
* [Email Address](luongutnho@hotmail.com)

![](https://i.imgur.com/waxVImv.png)
![](Donate.png)
[![ko-fi](https://ko-fi.com/img/githubbutton_sm.svg)](https://ko-fi.com/nholuong)

# License
* Nho Luong (c). All Rights Reserved.🌟
