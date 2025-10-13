<details> 
<summary> - ISP </summary>
  
```tcl
apt-get update && apt-get install chrony nginx iptables apache2-htpasswd -y
apt-get reinstall tzdata -y
```
</details>

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

# Действие №1 - Замена репазитория
<details>
<summary> - ISP </summary>

```bash
cp /etc/apt/sources.list.d/alt.list /etc/apt/sources.list.d/alt.list.bak
sed -i 's|^rpm.*ftp\.altlinux|# &|g' /etc/apt/sources.list.d/alt.list
cat >> /etc/apt/sources.list.d/alt.list <<EOF
rpm [p11] http://192.168.0.91/mirror p11/branch/x86_64 classic
rpm [p11] http://192.168.0.91/mirror p11/branch/noarch classic
rpm [p11] http://192.168.0.91/mirror p11/branch/x86_64-i586 classic
EOF
```
</details>

<details> 
<summary> - CLI & SRV'S </summary>

```bash
cp /etc/apt/sources.list.d/alt.list /etc/apt/sources.list.d/alt.list.bak
sed -i 's|^rpm.*ftp\.altlinux|# &|g' /etc/apt/sources.list.d/alt.list
cat >> /etc/apt/sources.list.d/alt.list <<EOF
rpm [p10] http://192.168.0.91/mirror p10/branch/x86_64 classic
rpm [p10] http://192.168.0.91/mirror p10/branch/noarch classic
rpm [p10] http://192.168.0.91/mirror p10/branch/x86_64-i586 classic
EOF
```

</details>

# Действие №2 - Установка пакетов
<details> 
<summary> - ISP </summary>

```bash
ISP
apt-get update && apt-get install chrony nginx iptables apache2-htpasswd -y
apt-get reinstall tzdata -y
iptables -t nat -A POSTROUTING -o ens20 -s 0/0 -j MASQUERADE
iptables-save > /etc/sysconfig/iptables
systemctl enable --now iptables
```

</details>

<summary> - HQ-SRV </summary>
```bash
apt-get update && apt-get install chrony nginx iptables apache2-htpasswd -y
apt-get reinstall tzdata -y


HQ-CLI
apt-get update && apt-get install chrony nginx iptables apache2-htpasswd -y
apt-get reinstall tzdata -y

BR-SRV
apt-get update && apt-get install chrony ansible task-samba-dc docker-engine docker-compose -y
```

</details>
