# Jellyfin en Docker

Servidor multimedia libre para centralizar películas y música en la red local, con transcodificación por hardware sin licencias ni suscripciones.

## Preparación

Tres directorios persistentes, para que la configuración y la biblioteca sobrevivan a la recreación del contenedor:

| Directorio | Contenido |
|---|---|
| `config` | Usuarios y ajustes |
| `cache` | Caché de imágenes y transcodificación |
| `media` | Biblioteca de vídeo y música |

```bash
mkdir -p ~/jellyfin/{config,cache,media}
```

<img width="1495" height="308" alt="Directorios de Jellyfin" src="https://github.com/user-attachments/assets/dd0cdccd-9971-47fb-bd06-a8ca9e52324b" />

## Despliegue

El contenedor se lanza con [`jellyfin.sh`](jellyfin.sh), que agrupa el `docker run` completo:

- **8096/tcp**: interfaz web.
- **7359/udp**: descubrimiento automático de clientes en la red local.
- `--user 1000:1000`: ejecución sin privilegios de root.

```bash
chmod +x jellyfin.sh
./jellyfin.sh
```

<img width="654" height="39" alt="Ejecución del script" src="https://github.com/user-attachments/assets/c4834ee9-6fab-405e-9905-f87eace5a909" />

## Configuración inicial

Asistente en `http://<IP-servidor>:8096`: idioma, usuario administrador, bibliotecas y acceso remoto.

<img width="1354" height="655" alt="Asistente de configuración (1/6)" src="https://github.com/user-attachments/assets/dd7909fe-6e96-4685-929f-836eeae0f869" />
<img width="948" height="566" alt="Asistente de configuración (2/6)" src="https://github.com/user-attachments/assets/30ba4b62-b821-4251-a6a9-b14b95972986" />
<img width="1105" height="584" alt="Asistente de configuración (3/6)" src="https://github.com/user-attachments/assets/5ac27dfe-89fa-4c9c-966c-3eced27aa669" />
<img width="883" height="414" alt="Asistente de configuración (4/6)" src="https://github.com/user-attachments/assets/f85bfa58-5c55-4014-a714-6c01342305c8" />
<img width="838" height="192" alt="Asistente de configuración (5/6)" src="https://github.com/user-attachments/assets/883ddb09-3535-40b1-888b-c052c3d82ba4" />
<img width="986" height="387" alt="Asistente de configuración (6/6)" src="https://github.com/user-attachments/assets/aa87b2a3-fa1c-4a55-a660-ae39fc1b9be9" />
<img width="974" height="264" alt="Panel de Jellyfin" src="https://github.com/user-attachments/assets/2005367e-be4e-4931-8a96-ddb30bb71ddd" />

## Contenido

La biblioteca se llenó con yt-dlp, para vídeos con su mejor calidad y metadatos ([A2](../A2-FFmpeg-YTDLP)), y con `wget` para descargas directas por URL.

<img width="1854" height="717" alt="Descarga de contenido" src="https://github.com/user-attachments/assets/ebcc6dbf-f957-4e12-93c9-a4af3b68cbde" />

## Acceso desde la red y el móvil

La máquina virtual usa red en modo puente (*bridged*) para tener IP propia en la LAN. Desde ahí se accede por navegador o con la app oficial de Jellyfin.

<img width="1426" height="608" alt="Acceso desde otro equipo" src="https://github.com/user-attachments/assets/5eec7aa4-63a6-4a3b-9ff5-60c5fffe357f" />
<img width="1843" height="302" alt="App móvil" src="https://github.com/user-attachments/assets/edfa711d-b5b5-472f-8276-93bc16e29be7" />

## Jellyfin frente a Plex

| | Jellyfin | Plex |
|---|---|---|
| Licencia | Código abierto | Propietario, con funciones de pago |
| Cuenta | No necesita | Cuenta en Plex para la mayoría de funciones |
| Dependencia externa | Ninguna: funciona solo con la red local | Autenticación a través de los servidores de Plex |
| Privacidad | Todo queda en el servidor propio | Plex conoce la biblioteca y el uso |
| Transcodificación por hardware | Incluida | Requiere Plex Pass |
| Interfaz | Correcta | Más pulida |

Para un servidor doméstico o de laboratorio sin dependencias externas, Jellyfin es la opción más coherente.
