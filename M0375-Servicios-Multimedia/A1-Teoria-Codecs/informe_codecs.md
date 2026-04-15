# Fundamentos de FFmpeg
Es una herramienta de software libre que funciona mediante comandos, en el ambito del procesamiento multimedia actua como el motor principal para manipular, transcodificar, grabar y emitir video y audio. Su página oficial es https://ffmpeg.org/documentation.html, donde está la documentación técnica
## Caracteristicas
1. Permite transcodificar archivos entre diferentes codecs de video y audio
2. Facilita el multiplexado, en otras palabras, cambiar de contenedores multimedia sin perder calidad
3. Incorpora filtros avanzados para escalar resoluciones, recortar, cambiar la tasa de fotogramas o aplicar marcas de agua
4. Gestiona pistas de forma independiente, permitiendo extrar audio, eliminar canales o añadir subtitulos
5. Permite realizar transimiones en red, mediante protocolos RTMP,HLS o SRT
# Instalación y Requisitos Previos
Los requisitos indispensables són 2, conexion a internet y conocimientos en uso de terminal, sin olvidar la dependencia de yt-dlp con FFmpeg, este debe de estar instalado antes
## Linux
  Este es el entorno nativo, desde la terminal actualizamos los repositorios con sudo apt update e instalamos FFmpeg con sudo apt install ffmpeg
  Para yt-dlp, la mejor practica es descargar su ejectuable oficial con el comando sudo wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -O /usr/local/bin/yt-dlp, dandole permisos de ejecucion con el comando  sudo chmod a+rx /usr/local/bin/yt-dlp
## macOS
La vía mas rapida y directa es mediante el gestor de paquetes Homebrew, debido a que resuelve las dependencias automaticamente, en la terminal se ejecuta mediante brew install ffmpeg y posteriormente brew install yt-dlp
## Windows
Este requiere configuración manual, donde primero descargamos el archivo .zip desde su pagina oficial, el paso mas importante es acceder a la configuracion avanzada del ssistema y añadir la ruta de la carpeta bin a las variables de entorno (PATH), para que la consola reconozca los comandos, para yt-dlp sirve con descargar el ejecutable de github en la misma ruta de FFmpeg para que tengan compatibilidad
# Contenedores y Manipulación
Es posible cambiar de contenedor sin modificar el contenido del video o audio, este se logra mediante el multiplexado, esto se consigue sin recodificar, por lo que el proceso es rapido y sin perdida de calidad.
Por ejemplo, para pasar de un archivo .mp4 a .mk, la operacion en FFmpeg seria_ ffmpeg -i video.mp4 -c copy videoo.mkv, donde el parametro -c copy ordena al sistema para que copie las pistas de origen intactas hacia el nuevo contenedor
Respecto a los conteoedores, el MP4 es el universal, ofreciendo maxima compatibilidad con navegadores, televisores, consolas y dispositivos moviles, conviene usarlo cuando el objetivo es la distribucion masiva o subida web, potr otro lado el MKV es un formato de codigo abierto mucho mas flexible, es la eleccino predefinida para colecciones personales y servidores locales como Jellyfin, ya que permite encapsular multiples pistas de video, diversos idiomas de audio y multiples subtitulos en un unico archivo
# Análisis de Comandos y Códecs en FFmpeg
El comando ffmpeg -i metal-violin-f616.mp4 -vcodec libx264 metal-violin-f616.mkv recodifica el video, este comando justifica la accion con el parametro -vcodec libx264, el cual ordena explicitamente a FFmpeg que vuelva a procesar la imagen utilizando el codec de software H.265
El codec H.264 en el comando destaca por el equilibro entre calidad visual y compatibilidad de harware en cualquier dispositivo del mundo, pero si se compara con el H.265, este ofrece el doble de eficiencia en compresion, obteniendo la misma calidad con la mitad de tamaño, pero el problema que tiene es la exigencia de una potencia computacional mayor para ser decodificado, lo que provoca tirones o bloqueos al reproducirlo en hardware antiguo sin aceleracion grafica dedicada
# Fundamentos y Características de yt-dlp
# Comparativa de Códecs en yt-dlp
