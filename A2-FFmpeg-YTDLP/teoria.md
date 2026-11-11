# FFmpeg y yt-dlp: fundamentos

## FFmpeg

Herramienta libre de línea de comandos para procesar vídeo y audio, y motor de buena parte del software multimedia. Documentación: [ffmpeg.org/documentation.html](https://ffmpeg.org/documentation.html).

- Transcodificación entre códecs de vídeo y audio.
- Cambio de contenedor sin recodificar (*remux*).
- Filtros: escalado, recorte, cambio de fotogramas por segundo, marcas de agua.
- Gestión independiente de pistas: extraer audio, eliminar canales, añadir subtítulos.
- Emisión en red por RTMP, HLS o SRT.

## yt-dlp

Descargador de contenido multimedia por terminal, sucesor activo de youtube-dl. Permite elegir con precisión formato y calidad, descargar solo el audio e incrustar subtítulos, metadatos y carátulas. Necesita FFmpeg para unir las pistas de vídeo y audio cuando se descargan por separado.

## Instalación

| Sistema | Procedimiento |
|---|---|
| Ubuntu | `apt install ffmpeg`; yt-dlp desde su binario oficial en `/usr/local/bin` |
| macOS | `brew install ffmpeg yt-dlp` |
| Windows | Descargar ambos ejecutables y añadir su carpeta al `PATH` |

## Contenedores

Cambio de contenedor sin tocar el contenido:

```bash
ffmpeg -i video.mp4 -c copy video.mkv
```

`-c copy` copia los flujos intactos: sin pérdida de calidad y casi instantáneo.

| Contenedor | Cuándo usarlo |
|---|---|
| MP4 | Distribución y web: compatible con navegadores, televisores, consolas y móviles |
| MKV | Bibliotecas personales y servidores como Jellyfin: varias pistas de audio, subtítulos y capítulos en un solo fichero |

## Recodificación

```bash
ffmpeg -i entrada.mp4 -c:v libx264 salida.mkv
```

`-c:v libx264` obliga a recodificar el vídeo con H.264 por software. H.264 ofrece el mejor equilibrio entre calidad y compatibilidad. H.265 (`libx265`) consigue la misma calidad con aproximadamente la mitad de tamaño, pero su decodificación es más exigente y puede dar tirones en equipos sin soporte por hardware.

## Códecs al descargar con yt-dlp

| Códec | Ventaja | Inconveniente | Recomendado para |
|---|---|---|---|
| H.264 | Compatible con todo | Ficheros más grandes | Reproductores y televisores antiguos |
| VP9 | Buena compresión; estándar de YouTube en 2K y 4K | Soporte irregular fuera de navegadores | Uso general en dispositivos actuales |
| AV1 | Máxima compresión | Decodificación pesada sin hardware compatible | Archivo a largo plazo con equipos recientes |
