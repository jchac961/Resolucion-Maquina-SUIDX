# Resolucion-Maquina-SUIDX

En este write up describimos paso a paso la resolucion de la maquina suidx

Lo primero que realizamos es la conexión o despliegue de la maquina
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 214718" src="https://github.com/user-attachments/assets/d9a8b8d1-18ab-40a4-b167-a967a0d3bd48" />

# Reconocimiento
Hacemos un nmap para verificar los puertos que esta maquina tiene abiertos/ utilizando el comando nmap -p- 172.17.0.2
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 214718" src="https://github.com/user-attachments/assets/ed50f932-6b3a-41fc-a999-f62a576a36ca" />

Luego enviamos otro nmap pero ahora utilizamos el siguiente comando, -sV que se encargara de solicitar las versiones de los servicios que se encuentran corriendo en esta maquina al igual que utilizamos el comando -sC que utiliza los script por defecto para verificar vulnerabilidades en los servicios / nmap -p- -sV -sC 172.17.0.2
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 215554" src="https://github.com/user-attachments/assets/ebcb6165-31a1-4180-ba40-b23d0502a869" />

Dentro de los servicios que se encontraban ejecutando pudimos ver el servicio http utilizando el puerto 8080, por lo cual accedimos mediante el navegador con la ruta http:172.17.0.2:8080 para verificar si encontrabamos algo relevante
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 215917" src="https://github.com/user-attachments/assets/637bf4bc-c3e8-4a33-8ab7-8d04a6052e31" />

En vista de que no pudimos obtener ninguna información que fuera de importancia para poder acceder a la maquina, procedimos a utilizar la herramienta feroxbuster utilizando el diccionario, esta herramienta nos encontro un subdominio llamado /user
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 220139" src="https://github.com/user-attachments/assets/2787fc05-eebd-4849-8865-c8b149119062" />

Procedimos a ingresar y pudimos obtener un nombre de usuario llamado "hacker"
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 220202" src="https://github.com/user-attachments/assets/e4031008-12a7-4be2-b468-f86862080967" />

# Explotacion 

Ya teniendo este usuario procedimos a hacer un ataque de fuerza bruta al servicio ssh utilizando la herramienta hydra, la cual nos encontro una contraseña para este usuario
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 222007" src="https://github.com/user-attachments/assets/906c1a1e-e52e-493a-8904-ee52dec16912" />

Ya teniendo esta contraseña ingresamos por medio del servicio ssh utilizando el usuario: hacker y la contraseña: amorcito
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 222306" src="https://github.com/user-attachments/assets/e1feb896-575f-4eac-bacb-099516339ab7" />

Ya teniendo el control de la maquina procedimos a buscar los binarios mal configurados con el comando find / -perm -4000 -type f 2>/dev/null
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 222319" src="https://github.com/user-attachments/assets/f85c5a15-5219-43ce-b681-f1b4abfa95fc" />

# Escalación de privilegios

Buscamos en la pagina de www.gtfobins.github.io el binario python y utilizamos el siguiente comando ./python3.10 -c 'import os; os.execl("/bin/sh", "sh", "-p")', haciendole unaligera modificación ingresandole el numero de version de python que la maquina estaba utilizando
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 222657" src="https://github.com/user-attachments/assets/32ab107c-a20f-4fe1-b1f7-fc05547e065c" />

Obteniendo los privilegios como root, y procedimos a listar los archivos y encontramos el archivo "flag.txt"
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 222724" src="https://github.com/user-attachments/assets/83a45fc4-3abe-4985-a7cd-0383e894315d" />

# Resultados 

Abrimos o listamos el contenido del archivo el cual contenia la bandera de este reto
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 222747" src="https://github.com/user-attachments/assets/f0e0841d-d47e-4b3b-a0f7-4ac6c9c7762d" />

Introdujimos el contenido del archivo para asi dar por terminada esta maquina
<img width="1920" height="1140" alt="Captura de pantalla 2025-12-14 222800" src="https://github.com/user-attachments/assets/f8378d7a-eee3-4099-8bb9-a97be0e795a4" />

