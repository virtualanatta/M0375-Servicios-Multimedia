# Servidor de streaming RTMP

Servidor de directos con nginx y el módulo RTMP en Docker. Se emite con FFmpeg y OBS y se reproduce con VLC.

RTMP mantiene una conexión TCP persistente entre emisor y servidor tras un *handshake* inicial, lo que permite enviar vídeo con baja latencia. Es el protocolo de ingesta que usan plataformas como Twitch o YouTube.

## Despliegue

El contenedor se lanza desde un script en un directorio dedicado, de modo que Docker resuelve las dependencias de nginx-rtmp sin instalar nada en el sistema.

<img width="416" height="90" alt="Directorio y script" src="https://github.com/user-attachments/assets/f9508172-7c13-4cf9-9e8f-a4df41d29928" />
<img width="416" height="90" alt="Permisos de ejecución" src="https://github.com/user-attachments/assets/92579eb6-93d0-4122-8ac7-09caefe529b1" />
<img width="416" height="90" alt="Ejecución" src="https://github.com/user-attachments/assets/e7e4f488-5b35-4cd5-85ff-8622da72893d" />

```bash
docker ps --filter name=nginx-rtmp
```

El contenedor escucha en el puerto **1935**, el estándar de RTMP.

<img width="1845" height="107" alt="Contenedor en ejecución" src="https://github.com/user-attachments/assets/337c1986-a390-4a87-acdb-04422cfdf8f7" />

## Emisión con FFmpeg

```bash
ffmpeg -re -i video.mp4 -c copy -f flv rtmp://<IP-servidor>/live/<clave>
```

- `-re` lee el fichero a velocidad real. Sin él, FFmpeg enviaría el vídeo tan rápido como pudiera y el directo fallaría.
- `-f flv` encapsula en FLV, el formato que transporta RTMP.

<img width="1041" height="139" alt="Emisión con FFmpeg" src="https://github.com/user-attachments/assets/cf08dff7-57e8-415c-8ddd-2ab182046451" />

## Emisión con OBS

*Ajustes → Emisión → Personalizado*, con `rtmp://<IP-servidor>/live` como servidor y cualquier clave de retransmisión.

<img width="596" height="444" alt="Servidor y clave en OBS" src="https://github.com/user-attachments/assets/0d1bb531-205e-4319-ab8b-88eb07adc18a" />

El bitrate de salida se ajusta a la velocidad de subida de la conexión para evitar cortes.

<img width="593" height="445" alt="Salida y bitrate en OBS" src="https://github.com/user-attachments/assets/f8719c43-0fa7-4445-a17a-470538049a53" />

## Reproducción

En VLC, *Medio → Abrir ubicación de red*: `rtmp://<IP-servidor>/live/<clave>`.

<img width="631" height="401" alt="Directo en VLC" src="https://github.com/user-attachments/assets/63111c0a-f804-4011-a070-6eb683ec56fa" />
