# Guía práctica de FFmpeg y yt-dlp

En esta sección documentamos el proceso de instalación y uso de las herramientas de procesamiento multimedia mediante la terminal de Ubuntu Server, utilizando como material de trabajo el video de Daniel Melingo, *Pequeño Paria*.

## Instalación de herramientas

Lo primero es preparar el sistema operativo para poder trabajar con multimedia. Instalamos FFmpeg desde los repositorios oficiales de Ubuntu y descargamos el binario de yt-dlp, dándole los permisos necesarios para su ejecución. FFmpeg se instala con `apt`, mientras que yt-dlp puede descargarse directamente desde su binario oficial y hacerse ejecutable con `chmod` [web:1][web:11].

### Instalamos FFmpeg

```bash
sudo apt update && sudo apt install -y ffmpeg
```

### Instalamos yt-dlp y damos permisos

```bash
sudo wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -O /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```

<img width="1179" height="657" alt="imagen" src="https://github.com/user-attachments/assets/58d7a943-8fe9-46ba-8405-f8054354c659" />

## Auditoría y descarga de contenido

Antes de bajar el archivo hacemos una auditoría de formatos con el parámetro `-F` para ver qué opciones nos da el servidor de YouTube y luego bajamos la mejor calidad disponible, forzando el contenedor MP4 para facilitar el trabajo posterior. El uso de `-F` permite listar los formatos disponibles y elegir una combinación adecuada de vídeo y audio [web:11].

### Auditoría de formatos

```bash
yt-dlp -F https://www.youtube.com/watch?v=qfg6CcqWNSA
```

### Descarga definitiva en MP4

```bash
yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]" --merge-output-form
```

<img width="1853" height="441" alt="imagen" src="https://github.com/user-attachments/assets/534951d2-2801-4986-bb51-575f5b4a7084" />
<img width="1843" height="302" alt="imagen" src="https://github.com/user-attachments/assets/f3c9e6a5-facd-4307-972e-007fdbd0f63b" />

## Análisis técnico y transcodificación

Una vez tenemos el archivo local, usamos FFmpeg para ver sus metadatos internos, como el bitrate y los códecs originales. Después hacemos la primera prueba de transcodificación pasando el video a un contenedor MKV usando el códec H.264. FFmpeg permite inspeccionar la entrada con `-i` y también convertir entre contenedores y códecs de forma directa [web:8][web:14].

### Ver información técnica

```bash
ffmpeg -i pequeño_paria.mp4
```

### Conversión a MKV con H.264

```bash
ffmpeg -i pequeño_paria.mp4 -vcodec libx264 pequeño_paria_264.mkv
```

<img width="1855" height="769" alt="imagen" src="https://github.com/user-attachments/assets/9a26f5a2-6a0c-4e86-bc96-3243dfb348b8" />
<img width="1399" height="441" alt="imagen" src="https://github.com/user-attachments/assets/3460bec8-ca23-471b-bf42-a5fc5669c63f" />

## Manipulación de audio y bitrate

En este paso probamos cómo cambiar solo la pista de sonido de un archivo, manteniendo el video intacto con la opción `copy`, y también ajustamos el bitrate manualmente para controlar el peso del archivo final. FFmpeg permite copiar streams sin recodificarlos y definir bitrate de vídeo y audio de forma explícita [web:8][web:12].

### Cambiar audio a MP3 manteniendo el video original

```bash
ffmpeg -i pequeño_paria.mp4 -vcodec copy -acodec mp3 pequeño_paria_audio.mkv
```

### Ajuste manual de bitrate

```bash
ffmpeg -i pequeño_paria.mp4 -b:v 2500k -b:a 192k pequeño_paria_bitrate.mp4
```

<img width="971" height="440" alt="imagen" src="https://github.com/user-attachments/assets/6448aaa5-9852-4750-af92-5d82cdea0928" />
<img width="924" height="442" alt="imagen" src="https://github.com/user-attachments/assets/e5878a14-ef06-4060-8076-59e10d17eb7b" />

## Recortes y extracción de pistas

Finalmente, usamos las funciones de recorte para sacar un fragmento exacto del video mediante marcas de tiempo y usamos el parámetro `-vn` para anular la imagen y extraer el audio limpio de la canción. FFmpeg permite hacer cortes por tiempo con `-ss` y `-to`, y también extraer solo el audio con `-vn` [web:6][web:14].

### Recorte de fragmento exacto

```bash
ffmpeg -i pequeño_paria.mp4 -ss 00:00:35 -to 00:01:05 pequeño_paria_recorte.mp4
```

### Extracción de audio MP3 sin video

```bash
ffmpeg -i pequeño_paria.mp4 -vn pequeño_paria_final.mp3
```

<img width="978" height="442" alt="imagen" src="https://github.com/user-attachments/assets/239b057d-bed5-4c00-a177-df62229f0b28" />
<img width="763" height="439" alt="imagen" src="https://github.com/user-attachments/assets/f829f0d3-06a9-4e33-b49e-da3b5fcd175b" />

## Ejemplo propio combinado

Como cierre de la práctica realizamos una operación que junta la descarga directa desde red con una transcodificación a H.265 y un recorte de cinco segundos, demostrando la integración de ambas herramientas en un solo flujo. Este tipo de encadenado es habitual en flujos de automatización con `yt-dlp` y `ffmpeg` [web:11][web:8].

```bash
yt-dlp -f "best[ext=mp4]" -o "temp.mp4" https://www.youtube.com/watch?v=qfg6CcqWNSA && ffmpeg -i temp.mp4 -ss 10 -t 5 -vcodec libx265 clip_pro.mkv && rm temp.mp4
```

<img width="1840" height="214" alt="imagen" src="https://github.com/user-attachments/assets/971bc3a4-9d68-4232-8b4b-3d7032972c4c" />

## Archivos generados

<img width="619" height="199" alt="imagen" src="https://github.com/user-attachments/assets/9c449c4f-ee6d-4ce0-994b-5e819ea82892" />
