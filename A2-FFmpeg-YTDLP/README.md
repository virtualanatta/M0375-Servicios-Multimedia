# FFmpeg y yt-dlp

Procesamiento de vídeo y audio desde la terminal de Ubuntu Server. Material de trabajo: el videoclip *Pequeño paria* de Daniel Melingo.

- [teoria.md](teoria.md): fundamentos de ambas herramientas, contenedores y comparativa de códecs.
- [protocolos-streaming.html](protocolos-streaming.html): comparativa visual de RTMP, HLS, RTSP y SRT. GitHub no renderiza HTML; se puede abrir descargándolo o con GitHub Pages.

## Instalación

```bash
sudo apt update && sudo apt install -y ffmpeg

sudo wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -O /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
```

<img width="1179" height="657" alt="Instalación de FFmpeg y yt-dlp" src="https://github.com/user-attachments/assets/58d7a943-8fe9-46ba-8405-f8054354c659" />

## Descarga

Primero se listan los formatos disponibles y después se descarga la mejor combinación de vídeo y audio en MP4:

```bash
yt-dlp -F https://www.youtube.com/watch?v=qfg6CcqWNSA

yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]" \
  --merge-output-format mp4 -o "pequeño_paria.mp4" \
  https://www.youtube.com/watch?v=qfg6CcqWNSA
```

<img width="1853" height="441" alt="Listado de formatos" src="https://github.com/user-attachments/assets/534951d2-2801-4986-bb51-575f5b4a7084" />
<img width="1843" height="302" alt="Descarga en MP4" src="https://github.com/user-attachments/assets/f3c9e6a5-facd-4307-972e-007fdbd0f63b" />

## Inspección y transcodificación

```bash
ffmpeg -i pequeño_paria.mp4                                     # códecs, bitrate, resolución
ffmpeg -i pequeño_paria.mp4 -c:v libx264 pequeño_paria_264.mkv  # vídeo recodificado a H.264 en MKV
```

<img width="1855" height="769" alt="Información del fichero" src="https://github.com/user-attachments/assets/9a26f5a2-6a0c-4e86-bc96-3243dfb348b8" />
<img width="1399" height="441" alt="Transcodificación a H.264" src="https://github.com/user-attachments/assets/3460bec8-ca23-471b-bf42-a5fc5669c63f" />

## Audio y bitrate

```bash
ffmpeg -i pequeño_paria.mp4 -c:v copy -c:a libmp3lame pequeño_paria_audio.mkv   # solo cambia el audio
ffmpeg -i pequeño_paria.mp4 -b:v 2500k -b:a 192k pequeño_paria_bitrate.mp4       # bitrate fijado
```

`-c:v copy` mantiene el vídeo sin recodificar, por lo que la operación es casi instantánea.

<img width="971" height="440" alt="Cambio de pista de audio" src="https://github.com/user-attachments/assets/6448aaa5-9852-4750-af92-5d82cdea0928" />
<img width="924" height="442" alt="Ajuste de bitrate" src="https://github.com/user-attachments/assets/e5878a14-ef06-4060-8076-59e10d17eb7b" />

## Recortes y extracción

```bash
ffmpeg -i pequeño_paria.mp4 -ss 00:00:35 -to 00:01:05 pequeño_paria_recorte.mp4
ffmpeg -i pequeño_paria.mp4 -vn pequeño_paria.mp3
```

`-ss` y `-to` delimitan el fragmento; `-vn` descarta el vídeo.

<img width="978" height="442" alt="Recorte" src="https://github.com/user-attachments/assets/239b057d-bed5-4c00-a177-df62229f0b28" />
<img width="763" height="439" alt="Extracción de audio" src="https://github.com/user-attachments/assets/f829f0d3-06a9-4e33-b49e-da3b5fcd175b" />

## Flujo combinado

Descarga, recorte de cinco segundos y transcodificación a H.265 en una sola línea:

```bash
yt-dlp -f "best[ext=mp4]" -o temp.mp4 https://www.youtube.com/watch?v=qfg6CcqWNSA \
  && ffmpeg -i temp.mp4 -ss 10 -t 5 -c:v libx265 clip.mkv \
  && rm temp.mp4
```

<img width="1840" height="214" alt="Flujo combinado" src="https://github.com/user-attachments/assets/971bc3a4-9d68-4232-8b4b-3d7032972c4c" />

## Resultado

<img width="619" height="199" alt="Ficheros generados" src="https://github.com/user-attachments/assets/9c449c4f-ee6d-4ce0-994b-5e819ea82892" />
