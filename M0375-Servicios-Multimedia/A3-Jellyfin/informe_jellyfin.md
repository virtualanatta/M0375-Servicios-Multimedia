# Despliegue de Jellyfin en Docker

Jellyfin es un servidor multimedia de código abierto que sirve para centralizar tus películas y música sin pagar licencias. Es la mejor opción porque es gratis total y te deja usar la aceleración por hardware sin suscripciones, algo que está muy bien para que la CPU no sufra al convertir vídeos al vuelo.

## Preparación y Requisitos Oficiales

Antes de lanzar el servidor, es obligatorio crear tres carpetas: **config**, **cache** y **media**. Las creamos porque si no lo haces, Docker perderá toda tu configuración y biblioteca cada vez que el contenedor se detenga.

- **config**: Guarda tus usuarios y ajustes.
- **cache**: Ayuda a que la interfaz vaya fluida.
- **media**: Donde guardamos los vídeos reales.

<img width="1495" height="308" alt="imagen" src="https://github.com/user-attachments/assets/dd0cdccd-9971-47fb-bd06-a8ca9e52324b" />

Para no escribir el comando gigante de Docker cada vez, usamos un script (`jellyfin.sh`). Es más cómodo y evita errores. En este archivo, lo más importante que hay que cambiar es la ruta del mount, poniendo la dirección real de tu carpeta de vídeos en el servidor.

Para que el sistema te deje lanzarlo, hay que darle permisos de ejecución con `chmod +x jellyfin.sh`. Sin esto, Linux lo verá como un simple archivo de texto y no lo arrancará.

```bash
chmod +x jellyfin.sh
./jellyfin.sh
```

<img width="654" height="39" alt="imagen" src="https://github.com/user-attachments/assets/c4834ee9-6fab-405e-9905-f87eace5a909" />

## Configuración del Servidor

Una vez arrancado, entras por la IP de tu servidor (puerto **8096**) y sigues el asistente.

<img width="1354" height="655" alt="imagen" src="https://github.com/user-attachments/assets/dd7909fe-6e96-4685-929f-836eeae0f869" />

<img width="948" height="566" alt="imagen" src="https://github.com/user-attachments/assets/30ba4b62-b821-4251-a6a9-b14b95972986" />

<img width="1105" height="584" alt="imagen" src="https://github.com/user-attachments/assets/5ac27dfe-89fa-4c9c-966c-3eced27aa669" />

<img width="883" height="414" alt="imagen" src="https://github.com/user-attachments/assets/f85bfa58-5c55-4014-a714-6c01342305c8" />

<img width="838" height="192" alt="imagen" src="https://github.com/user-attachments/assets/883ddb09-3535-40b1-888b-c052c3d82ba4" />

<img width="986" height="387" alt="imagen" src="https://github.com/user-attachments/assets/aa87b2a3-fa1c-4a55-a660-ae39fc1b9be9" />

<img width="974" height="264" alt="imagen" src="https://github.com/user-attachments/assets/2005367e-be4e-4931-8a96-ddb30bb71ddd" />

## Descarga de Contenido

Para llenar el servidor usamos dos herramientas clave:

- **yt-dlp**: La usamos porque es la mejor para bajar vídeos de YouTube con la máxima calidad y manteniendo los metadatos.
- **wget**: Funciona bajando archivos directamente desde un enlace. Es muy simple: le das la URL y te descarga el archivo tal cual en la carpeta donde estés.

<img width="1854" height="717" alt="imagen" src="https://github.com/user-attachments/assets/ebcc6dbf-f957-4e12-93c9-a4af3b68cbde" />

## Acceso y Aplicación Móvil

Con todo configurado, ya puedes entrar desde cualquier PC de la red o desde el móvil. Si no te conecta, revisa que VMware esté en modo puente (**Bridged**) para que el servidor tenga su propia IP.

<img width="1426" height="608" alt="imagen" src="https://github.com/user-attachments/assets/5eec7aa4-63a6-4a3b-9ff5-60c5fffe357f" />

**App Jellyfin y cómo entrar desde el smartphone:**

<img width="1843" height="302" alt="imagen" src="https://github.com/user-attachments/assets/edfa711d-b5b5-472f-8276-93bc16e29be7" />

## Jellyfin vs Plex

Si hablamos de elegir entre Jellyfin y Plex, la gran diferencia es quién tiene el mando del sistema. Plex es mucho más comercial y visualmente está muy pulido, pero tiene el problema de que te obliga a pasar por sus propios servidores. Para usar Plex, casi siempre necesitas crearte una cuenta en su web y loguearte, lo que significa que ellos saben qué tienes y cuándo lo ves; además, si un día se cae su servicio externo, tú podrías tener problemas para entrar en tu propia casa a ver tus películas.

Jellyfin, en cambio, es totalmente tuyo. Al ser de código abierto, todo se queda dentro de tu máquina virtual de Ubuntu. No necesitas registrarte en ningún sitio ni pedir permiso a una empresa externa para entrar a tu servidor. Si tu red local funciona, Jellyfin funciona. Es la opción más realista si buscas privacidad total y no quieres que nadie rastree tus hábitos de consumo.
