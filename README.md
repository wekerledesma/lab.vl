Instalar GPG2 
sudo yum install gnupg2

Crear un directorio y cambiar a él:
mkdir mi_directorio
cd mi_directorio

Crear un archivo de texto:
echo "Este es un archivo de prueba para cifrar" > mi_archivo.txt

Cifrar el archivo:
gpg2 -e -r "Tu Nombre" mi_archivo.txt

Verificar el archivo cifrado:
ls -l

Descifrar el archivo:
gpg2 -d mi_archivo.txt.gpg > mi_archivo_descifrado.txt

Ver el contenido del archivo descifrado:
cat mi_archivo_descifrado.txt

Borrar los archivos:
rm mi_archivo.txt
rm mi_archivo.txt.gpg
rm mi_archivo_descifrado.txt

practica #2
1. Iniciar y habilitar los servicios HTTP, FTP y SSH:
   
# Iniciar los servicios
sudo systemctl start httpd
sudo systemctl start vsftpd
sudo systemctl start sshd

# Habilitar los servicios para que inicien con el sistema
sudo systemctl enable httpd
sudo systemctl enable vsftpd
sudo systemctl enable sshd

# Verificar que los servicios están activos
sudo systemctl status httpd
sudo systemctl status vsftpd
sudo systemctl status sshd
✅ 2. Comprobar que los servicios funcionan:

# Probar el acceso a Apache (HTTP)
curl -I http://localhost

# Probar el acceso a FTP
ftp localhost

# Probar el acceso a SSH
ssh localhost
✅ 3. Bloquear los puertos 80 (HTTP), 21 (FTP) y 22 (SSH) con iptables:
En IPv4:

# Bloquear los puertos
sudo iptables -A INPUT -p tcp --dport 80 -j DROP
sudo iptables -A INPUT -p tcp --dport 21 -j DROP
sudo iptables -A INPUT -p tcp --dport 22 -j DROP

# Verificar las reglas
sudo iptables -L --line-numbers
En IPv6:

# Bloquear los puertos
sudo ip6tables -A INPUT -p tcp --dport 80 -j DROP
sudo ip6tables -A INPUT -p tcp --dport 21 -j DROP
sudo ip6tables -A INPUT -p tcp --dport 22 -j DROP

# Verificar las reglas
sudo ip6tables -L --line-numbers
✅ 4. Desbloquear los puertos 80, 21 y 22 con iptables:
En IPv4:

sudo iptables -D INPUT -p tcp --dport 80 -j DROP
sudo iptables -D INPUT -p tcp --dport 21 -j DROP
sudo iptables -D INPUT -p tcp --dport 22 -j DROP

# Verificar que no hay reglas
sudo iptables -L --line-numbers
En IPv6:

sudo ip6tables -D INPUT -p tcp --dport 80 -j DROP
sudo ip6tables -D INPUT -p tcp --dport 21 -j DROP
sudo ip6tables -D INPUT -p tcp --dport 22 -j DROP

# Verificar que no hay reglas
sudo ip6tables -L --line-numbers
✅ 5. Bloquear los puertos con firewall-cmd:
En IPv4:

sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" port protocol="tcp" port="80" reject'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" port protocol="tcp" port="21" reject'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv4" port protocol="tcp" port="22" reject'

# Aplicar los cambios
sudo firewall-cmd --reload

# Verificar las reglas
sudo firewall-cmd --list-all
En IPv6:

sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv6" port protocol="tcp" port="80" reject'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv6" port protocol="tcp" port="21" reject'
sudo firewall-cmd --permanent --add-rich-rule='rule family="ipv6" port protocol="tcp" port="22" reject'

# Aplicar los cambios
sudo firewall-cmd --reload

# Verificar las reglas
sudo firewall-cmd --list-all
✅ 6. Desbloquear los puertos con firewall-cmd:
En IPv4:

sudo firewall-cmd --permanent --remove-rich-rule='rule family="ipv4" port protocol="tcp" port="80" reject'
sudo firewall-cmd --permanent --remove-rich-rule='rule family="ipv4" port protocol="tcp" port="21" reject'
sudo firewall-cmd --permanent --remove-rich-rule='rule family="ipv4" port protocol="tcp" port="22" reject'

# Aplicar los cambios
sudo firewall-cmd --reload
En IPv6:

sudo firewall-cmd --permanent --remove-rich-rule='rule family="ipv6" port protocol="tcp" port="80" reject'
sudo firewall-cmd --permanent --remove-rich-rule='rule family="ipv6" port protocol="tcp" port="21" reject'
sudo firewall-cmd --permanent --remove-rich-rule='rule family="ipv6" port protocol="tcp" port="22" reject'

# Aplicar los cambios
sudo firewall-cmd --reload
✅ 7. Eliminar todas las reglas de firewall-cmd:

# Identificar la zona activa
sudo firewall-cmd --get-active-zones

# Eliminar todas las reglas de la zona activa (sustituye "public" si es otra)
sudo firewall-cmd --zone=public --remove-rich-rule-all

# Recargar el firewall
sudo firewall-cmd --reload

# Verificar que no haya reglas activas
sudo firewall-cmd --list-all

