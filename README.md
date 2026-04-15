# M0375 - Servicios Multimedia

Este repositorio contiene la documentación técnica y las prácticas del módulo **M0375: Servicios**. El enfoque principal de estas actividades es el despliegue, la configuración y el análisis de protocolos de transmisión, códecs y servidores multimedia en entornos locales.

Toda la infraestructura descrita en estas prácticas está pensada para ejecutarse en entornos autohospedados. Las pruebas de carga multimedia y streaming se han diseñado teniendo en cuenta un servidor principal con 4 TB de almacenamiento, gestión de red con SQM y filtrado mediante AdGuard Home.

---

## Índice de Actividades

* **[A1-Teoria-Codecs](M0375-Servicios-Multimedia/A1-Teoria-Codecs) (Ref: B7A0)**
  * Análisis profundo sobre formatos contenedores, eficiencia de compresión (H.264, AV1) y transcodificación por hardware.
  * Incluye una auditoría crítica sobre el uso de la IA en la búsqueda de documentación técnica.

* **[A2-FFmpeg-YTDLP](M0375-Servicios-Multimedia/A2-FFmpeg-YTDLP) (Ref: B7A2)**
  * Documentación teórica sobre los protocolos RTMP, HLS, RTSP y SRT.
  * Guía práctica de instalación y uso de FFmpeg y YT-DLP para la manipulación y descarga de streams de vídeo y audio por consola.

* **[A3-Jellyfin](M0375-Servicios-Multimedia/A3-Jellyfin) (Ref: B7A3)**
  * Despliegue de un servidor multimedia Jellyfin mediante contenedores Docker.
  * Comparativa técnica frente a Plex y guía de configuración del cliente móvil.

* **[A4-RTMP-Streaming](M0375-Servicios-Multimedia/A4-RTMP-Streaming) (Ref: B8A4)**
  * Implementación de un servidor de streaming en directo utilizando `nginx-rtmp-module`.
  * Configuración de la ingesta de vídeo mediante OBS Studio y FFmpeg, y visualización del flujo en red local a través de VLC.

---

## Stack Tecnológico y Herramientas

* **Sistemas y Contenedores:** Ubuntu Server, Docker.
* **Procesamiento de Medios:** FFmpeg, YT-DLP.
* **Servidores Web/Streaming:** NGINX (RTMP Module), Jellyfin.
* **Protocolos Analizados:** RTMP, RTSP, HLS, SRT.
* **Clientes de Prueba:** OBS Studio, VLC Media Player.

---

**Autor:** David Coca  
**Ciclo:** Administración de Sistemas Informáticos en Red (ASIR)
