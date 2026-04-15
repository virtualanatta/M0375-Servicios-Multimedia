# guia practica de ffmpeg y yt-dlp
en esta sección documentamos el proceso de instalación y uso de las herramientas de procesamiento multimedia mediante la terminal de ubuntu server utilizando como material de trabajo el video de daniel melingo pequeño paria
# instalacion de herramientas
lo primero es preparar el sistema operativo para poder trabajar con multimedia instalamos ffmpeg desde los repositorios oficiales de ubuntu y descargamos el binario de yt-dlp dándole los permisos necesarios para su ejecución
Bash
## instalamos ffmpeg
sudo apt update && sudo apt install -y ffmpeg
## instalamos yt-dlp y damos permisos
sudo wget https://github.com/yt-dlp/yt-dlp/releases/latest/download/yt-dlp -O /usr/local/bin/yt-dlp
sudo chmod a+rx /usr/local/bin/yt-dlp
<img width="1179" height="657" alt="imagen" src="https://github.com/user-attachments/assets/58d7a943-8fe9-46ba-8405-f8054354c659" />
# auditoria y descarga de contenido
antes de bajar el archivo hacemos una auditoria de formatos con el parámetro -F para ver que opciones nos da el servidor de youtube y luego bajamos la mejor calidad disponible forzando el contenedor mp4 para facilitar el trabajo posterior
## auditoria de formatos
yt-dlp -F https://www.youtube.com/watch?v=qfg6CcqWNSA
## descarga definitiva en mp4
yt-dlp -f "bestvideo[ext=mp4]+bestaudio[ext=m4a]/best[ext=mp4]" --merge-output-form
<img width="1853" height="441" alt="imagen" src="https://github.com/user-attachments/assets/534951d2-2801-4986-bb51-575f5b4a7084" />
<img width="1843" height="302" alt="imagen" src="https://github.com/user-attachments/assets/f3c9e6a5-facd-4307-972e-007fdbd0f63b" />
# analisis técnico y transcodificacion
una vez tenemos el archivo local usamos ffmpeg para ver sus metadatos internos como el bitrate y los codecs originales despues hacemos la primera prueba de transcodificacion pasando el video a un contenedor mkv usando el codec h264
Bash
## ver informacion tecnica
ffmpeg -i pequeño_paria.mp4

# conversion a mkv con h264
ffmpeg -i pequeño_paria.mp4 -vcodec libx264 pequeño_paria_264.mkv
<img width="1855" height="769" alt="imagen" src="https://github.com/user-attachments/assets/9a26f5a2-6a0c-4e86-bc96-3243dfb348b8" />
<img width="1399" height="441" alt="imagen" src="https://github.com/user-attachments/assets/3460bec8-ca23-471b-bf42-a5fc5669c63f" />
# manipulacion de audio y bitrate
en este paso probamos como cambiar solo la pista de sonido de un archivo manteniendo el video intacto con la opcion copy y tambien ajustamos el bitrate manualmente para controlar el peso del archivo final
## cambiar audio a mp3 manteniendo video original
ffmpeg -i pequeño_paria.mp4 -vcodec copy -acodec mp3 pequeño_paria_audio.mkv
## ajuste manual de bitrate
ffmpeg -i pequeño_paria.mp4 -b:v 2500k -b:a 192k pequeño_paria_bitrate.mp4
<img width="971" height="440" alt="imagen" src="https://github.com/user-attachments/assets/6448aaa5-9852-4750-af92-5d82cdea0928" />
<img width="924" height="442" alt="imagen" src="https://github.com/user-attachments/assets/e5878a14-ef06-4060-8076-59e10d17eb7b" />
# recortes y extraccion de pistas
finalmente usamos las funciones de recorte para sacar un fragmento exacto del video mediante marcas de tiempo y usamos el parametro -vn para anular la imagen y extraer el audio limpio de la cancion
## recorte de fragmento exacto
ffmpeg -i pequeño_paria.mp4 -ss 00:00:35 -to 00:01:05 pequeño_paria_recorte.mp4
## extraccion de audio mp3 sin video
ffmpeg -i pequeño_paria.mp4 -vn pequeño_paria_final.mp3
<img width="978" height="442" alt="imagen" src="https://github.com/user-attachments/assets/239b057d-bed5-4c00-a177-df62229f0b28" />
<img width="763" height="439" alt="imagen" src="https://github.com/user-attachments/assets/f829f0d3-06a9-4e33-b49e-da3b5fcd175b" />
# ejemplo propio combinado
como cierre de la practica realizamos una operacion que junta la descarga directa desde red con una transcodificacion a h265 y un recorte de cinco segundos demostrando la integracion de ambas herramientas en un solo flujo
yt-dlp -f "best[ext=mp4]" -o "temp.mp4" https://www.youtube.com/watch?v=qfg6CcqWNSA && ffmpeg -i temp.mp4 -ss 10 -t 5 -vcodec libx265 clip_pro.mkv && rm temp.mp4
<img width="1840" height="214" alt="imagen" src="https://github.com/user-attachments/assets/971bc3a4-9d68-4232-8b4b-3d7032972c4c" />

## ARchivos generados: <img width="619" height="199" alt="imagen" src="https://github.com/user-attachments/assets/9c449c4f-ee6d-4ce0-994b-5e819ea82892" />






