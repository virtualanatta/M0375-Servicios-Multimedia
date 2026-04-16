# Configuración de Servidor de Streaming (RTMP)

RTMP es el protocolo estándar para hacer directos. Funciona mediante un "handshake" o saludo inicial entre el emisor y el servidor, estableciendo una conexión constante que permite enviar vídeo con muy poca latencia. Es lo que usan plataformas como Twitch o YouTube para recibir la señal de los streamers.

## 1. Preparación del Entorno y Script

Para no ensuciar el servidor, creamos una carpeta dedicada. Usamos un script (`rtmp.sh`) para automatizar el despliegue de Nginx con el módulo RTMP. Esto es mucho más limpio que instalarlo a pelo, ya que Docker se encarga de todas las dependencias por nosotros.

Creación de la carpeta y del script de configuración:

<img width="416" height="90" alt="imagen" src="https://github.com/user-attachments/assets/f9508172-7c13-4cf9-9e8f-a4df41d29928" />

Como Linux protege los archivos por seguridad, hay que usar `chmod +x` para darle permisos de ejecución al script. Sin esto, el sistema no te dejaría lanzarlo. Una vez con permisos, lo ejecutamos con `sudo` para que Docker levante el servicio.

Permisos de ejecución y lanzamiento del script:

<img width="416" height="90" alt="imagen" src="https://github.com/user-attachments/assets/92579eb6-93d0-4122-8ac7-09caefe529b1" />

<img width="416" height="90" alt="imagen" src="https://github.com/user-attachments/assets/e7e4f488-5b35-4cd5-85ff-8622da72893d" />

## 2. Verificación del Servidor

Para estar seguros de que el servidor está escuchando, usamos `docker ps`. Aquí confirmamos que el contenedor `nginx-rtmp` está arriba y usando el puerto `1935`, que es el puerto por defecto para este protocolo.

Comprobación del contenedor en funcionamiento:

<img width="1845" height="107" alt="imagen" src="https://github.com/user-attachments/assets/337c1986-a390-4a87-acdb-04422cfdf8f7" />

## 3. Emisión con FFmpeg (Contribución)

Para probar el servidor, usamos FFmpeg para "inyectar" un vídeo que ya tenemos en el disco (en este caso, la película que bajamos antes).

Es vital usar el parámetro `-re` para que FFmpeg lea el archivo en tiempo real; si no lo pones, intentaría enviar toda la película de golpe y el streaming fallaría. También forzamos el formato `-f flv` porque es el único que RTMP entiende para el transporte.

Lanzamiento del flujo de vídeo hacia el servidor local:

<img width="1041" height="139" alt="imagen" src="https://github.com/user-attachments/assets/cf08dff7-57e8-415c-8ddd-2ab182046451" />

## 4. Configuración Profesional con OBS

Si queremos emitir de forma profesional (con cámara o capturando pantalla), usamos OBS Studio. En los ajustes de emisión, seleccionamos "Personalizado" y ponemos la IP de nuestra máquina virtual seguida de la clave que queramos.

Ajustes de servidor y clave de retransmisión en OBS:

<img width="596" height="444" alt="imagen" src="https://github.com/user-attachments/assets/0d1bb531-205e-4319-ab8b-88eb07adc18a" />

También configuramos el bitrate y el codificador. Como tenemos un servidor potente con 4 TB, podríamos permitirnos calidades altas, pero lo ideal es ajustar el bitrate a nuestra conexión de subida para que no haya cortes.

Configuración de salida y bitrate para el directo:

<img width="593" height="445" alt="imagen" src="https://github.com/user-attachments/assets/f8719c43-0fa7-4445-a17a-470538049a53" />

## 5. Resultado Final

Para verificar que todo funciona, abrimos la dirección del stream en un reproductor como VLC. Si vemos el vídeo con fluidez, significa que nuestro servidor Nginx está recibiendo y repartiendo la señal correctamente.

Demostración del streaming funcionando en tiempo real:

<img width="631" height="401" alt="imagen" src="https://github.com/user-attachments/assets/63111c0a-f804-4011-a070-6eb683ec56fa" />
