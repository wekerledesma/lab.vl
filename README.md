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

Borrar los archivos 
rm mi_archivo.txt
rm mi_archivo.txt.gpg
rm mi_archivo_descifrado.txt
