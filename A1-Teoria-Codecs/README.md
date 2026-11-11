# Códecs, contenedores y calidad multimedia

## Contenedor, flujos y códec

- **Contenedor** (`.mp4`, `.mkv`): el fichero que empaqueta y sincroniza los distintos flujos y sus metadatos.
- **Flujos** (*streams*): pistas independientes dentro del contenedor, normalmente una de vídeo, una o varias de audio y subtítulos.
- **Códec** (codificador/decodificador): el algoritmo que comprime y descomprime cada flujo, como H.264 o AAC.
- **Metadatos**: información sobre el contenido, como título, resolución, idioma, capítulos o espacio de color.

Cambiar de contenedor no obliga a recodificar: los flujos se copian tal cual (*remux*). Ver [A2](../A2-FFmpeg-YTDLP).

## Compresión

| Tipo | Funcionamiento | Uso |
|---|---|---|
| Con pérdida (*lossy*) | Elimina información poco perceptible; lo eliminado no se recupera | Distribución: streaming, web, MP3, H.264 |
| Sin pérdida (*lossless*) | Conserva todos los datos originales | Másteres y postproducción, para no degradar en ediciones sucesivas |

El **bitrate** es la cantidad de datos por segundo de un flujo (kbps, Mbps) y determina en gran medida su calidad y su tamaño. No hay que confundirlo con el **ancho de banda**, que es la capacidad de la red: si el bitrate supera el ancho de banda disponible, la reproducción se corta.

## Submuestreo de croma

El ojo distingue mejor los cambios de brillo (luma) que los de color (croma), así que el color se puede almacenar a menor resolución.

| Esquema | Información de color | Uso |
|---|---|---|
| 4:4:4 | Completa | Cine, diseño, croma |
| 4:2:2 | Mitad en horizontal | Televisión profesional |
| 4:2:0 | Mitad en horizontal y en vertical | Distribución: YouTube, Netflix, Blu-ray |

4:2:0 reduce a la mitad los datos de imagen sin compresión respecto a 4:4:4. Es un problema en el *chroma key*: con menos información de color, los bordes del recorte salen dentados.

## Códecs de vídeo

| Códec | Eficiencia | Compatibilidad | Licencia |
|---|---|---|---|
| H.264 / AVC | Referencia | Universal | Con *royalties* |
| H.265 / HEVC | ≈ 50 % menos bitrate que H.264 a igual calidad | Hardware moderno | Con *royalties*, licenciamiento fragmentado |
| VP9 | Similar a HEVC | Navegadores, Android, YouTube | Libre (Google) |
| AV1 | Superior a HEVC | Creciente; decodificación hardware solo en equipos recientes | Libre (Alliance for Open Media) |
| H.266 / VVC | ≈ 50 % menos bitrate que HEVC | Muy limitada | Con *royalties* |

AV1 lo desarrolla la Alliance for Open Media, fundada en 2015 por empresas como Google, Netflix, Amazon, Microsoft, Intel y Mozilla para disponer de un códec eficiente sin costes de licencia. Apple se unió más tarde.

## Transcodificación

| Modo | Qué ocurre | Coste |
|---|---|---|
| *Direct play* | El cliente soporta el formato y recibe el fichero tal cual | Mínimo |
| *Transcoding* | El servidor convierte el vídeo en tiempo real a un formato que el cliente sí soporta | Alto en CPU |

La aceleración por hardware traslada la transcodificación a bloques dedicados de la GPU: NVENC (NVIDIA), Quick Sync (Intel), AMF (AMD) y VideoToolbox (Apple). En Linux se accede a ellos a través de APIs como VAAPI. Es mucho más rápida y libera la CPU, a cambio de algo menos de calidad que la codificación por software a bitrates bajos.

## Streaming adaptativo

HLS y MPEG-DASH permiten que la calidad se ajuste a la conexión sin cortes:

1. El vídeo se divide en **segmentos** de pocos segundos.
2. Se codifica en varias calidades (**renditions**: 1080p, 720p, 480p…).
3. Un **manifiesto** (`.m3u8` en HLS, `.mpd` en DASH) indica qué segmentos y calidades existen.
4. El reproductor mide la velocidad de la red y pide cada segmento en la calidad que puede sostener en ese momento.
