
```bash
apt-get update && apt-get install chrony nginx iptables apache2-htpasswd -y
apt-get reinstall tzdata -y
```


<details> 
<summary> - HQ-SRV </summary>
  
```tcl
apt-get update && apt-get install chrony dnsmasq fdisk nfs-server -y
apt-get update && apt-get install -y apache2 php8.2 apache2-mod_php8.2 mariadb-server php8.2-{opcache,curl,gd,intl,mysqli,xml,xmlrpc,ldap,zip,soap,mbstring,json,xmlreader,fileinfo,sodium}
```
</details>

<details> 
<summary> - HQ-CLI </summary>
```tcl
apt-get update && apt-get install admc chrony nfs-clients sudo libsss_sudo yandex-browser -y
```
</details>

<details> 
<summary> - BR-SRV </summary>
```tcl
apt-get update && apt-get install chrony ansible task-samba-dc docker-engine docker-compose -y
apt-repo add rpm http://altrepo.ru/local-p10 noarch local-p10
apt-get update && apt-get install sudo-samba-schema -y
```
</details>
