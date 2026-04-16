## ¿Qué estrategias usaste para verificar que la información generada por la IA sobre códecs y contenedores es precisa y actualizada?

Busqué los conceptos mencionados y los leí (no exhaustivamente).

## ¿En qué momentos decidiste no confiar en la IA y buscar fuentes adicionales? ¿Por qué? O por el contrario, ¿has tomado por válido todo lo que te dice?

No suelo tomar todo lo que me da la IA y pegarlo directamente, sobre todo en teoría pero en práctica (como terminal o configuraciones) soy más confiado en la IA, pero sé que la inteligencia artificial toma cualquier fuente aun si está equivocada, puse muchas fuentes de Reddit puesto que lo veo como una falla, es un foro online donde cualquiera puede poner lo que quiera y la IA no lo diferencia.

## ¿Cómo ajustaste tu prompt inicial para obtener respuestas más útiles o profundas? Muestra al menos dos versiones de tu prompt y explica los cambios.

En el segundo prompt simplemente le di las preguntas y le pedí que explique detalladamente para que yo pueda hacer resumen con mis palabras. La segunda es por la IA y la tercera con el prompt propio.

## ¿Qué palabras clave o estructuras incluiste en tu prompt para guiar mejor la respuesta de la IA? ¿Funcionaron?

Busqué las fuentes, le pedí que actuase como profesor y le dije que soy nuevo en este tema.

## ¿Cómo adaptaste la respuesta de la IA a tu propio estilo o nivel de comprensión? ¿Qué partes reescribiste, simplificaste o expandiste?

Lo tengo configurado para que vaya adaptándose a mi manera de escribir y explicar para que yo pueda entenderlo mejor, conceptos que nunca vi, errores que se repiten mucho, aunque admito que también imita mis faltas de ortografía porque escribo sin preocuparme en ese aspecto.

## ¿Incluiste ejemplos propios o analogías personales? ¿Por qué crees que eso mejora tu aprendizaje?

Me ayuda a verlo como si hablara conmigo mismo y me da facilidad a imitarme.

## ¿Identificaste algún error, omisión o sesgo en la respuesta de la IA? ¿Cómo lo corregiste?

No vi ningún error de la IA sino mío, al imitar mi forma de escribir y explicar también me mostró mi problema al momento de explicar conceptos nuevos por lo que no entendí la primera vez.

## ¿La IA te dio una respuesta demasiado general? ¿Cómo la hiciste más específica o contextualizada a tu caso?

## ¿Si tuvieras que explicar este tema a un compañero que no entiende nada de códecs, cómo usarías la IA para ayudarte a preparar una explicación sencilla?

Le pediría que sea un profesor explicando a un alumno nuevo en este tema reforzando puntos "difíciles".

## ¿Qué parte del contenido generado por la IA usarías en un proyecto real (por ejemplo, configurar Jellyfin)? ¿Por qué?

Me apoyaría mucho en la instalación y configuración pero no tanto en los errores, he tenido experiencias pasadas en las que al querer corregir errores, la IA se expandía mucho y buscaba errores que no había en ese momento, errores simples como un archivo con extensión errónea me pedía configurar muchas más cosas.

## ¿Qué aprendiste sobre tu propio proceso de aprendizaje al usar la IA en esta tarea?

Copiar y pegar no sirve.

## ¿Crees que usar la IA te hizo aprender más, menos o de forma diferente? Justifica tu respuesta.

Considero que es algo que varía según cómo se usa, no es lo mismo darle directamente las preguntas y que te responda a buscar la información, decirlo que lo explique de x manera y se adapte a tu ritmo.

Prompt 2:
Informe Técnico: Formatos, Códecs y Calidad Multimedia
1. Fundamentos: Contenedores y Códecs

En el procesamiento multimedia, es vital diferenciar entre el envoltorio y el contenido:

    Códec (Codificador/Decodificador): Es el algoritmo encargado de comprimir y descomprimir los datos (ej. H.264, AAC). Su objetivo es reducir el tamaño del archivo eliminando redundancias.

    Contenedor: Es el formato de archivo (ej. MP4, MKV) que empaqueta los distintos flujos (streams) de vídeo, audio y subtítulos en una sola unidad, junto con los metadatos (títulos, etiquetas, capítulos).

2. Compresión y Calidad Visual
Compresión Lossy vs. Lossless

    Lossy (Con pérdida): Elimina información que el sistema sensorial humano no percibe fácilmente. Permite una reducción de tamaño masiva (ej. MP3, H.264).

    Lossless (Sin pérdida): Conserva cada bit de la fuente original. Se utiliza en archivos maestros de postproducción para evitar la degradación tras múltiples ediciones.

Submuestreo de Croma (4:2:0)

El ojo humano es más sensible a los cambios de brillo (Luma) que a los de color (Croma). El submuestreo 4:2:0 reduce la resolución del color a la mitad tanto horizontal como verticalmente.

    Situaciones críticas: No podemos permitirnos esta reducción en entornos de Chroma Key (pantalla verde) o gradación de color profesional, donde se requiere información 4:4:4 para evitar bordes "dentados" y asegurar la precisión del recorte.

3. Evolución de los Códecs Modernos
Códec	Eficiencia	Compatibilidad	Licencia
H.264 (AVC)	Estándar	Universal	Royalties
H.265 (HEVC)	+50% vs H.264	Alta (HW moderno)	Royalties (Compleja)
VP9	Alta	Navegadores/Android	Libre (Google)
AV1	Muy Alta	En crecimiento	Libre (AOM)

    VVC (H.266): Promete reducir a la mitad el bitrate de HEVC, pero su adopción es lenta debido a la enorme potencia de cálculo requerida y la fragmentación de patentes.

    Consorcio AOM: Google, Netflix y Apple crearon AV1 como un estándar Royalty-free para evitar los costes millonarios de licencias que exige el grupo MPEG por usar H.265.

4. Rendimiento y Transcodificación
Aceleración por Hardware

Frente a la transcodificación por software (CPU), que es lenta pero de máxima calidad, existen chips específicos en las GPUs:

    NVENC (Nvidia), QuickSync (Intel), VAAPI (Linux).

    Ventaja: Rapidez extrema y liberación de la carga de la CPU.

    Inconveniente: Menor flexibilidad y, en bitrates muy bajos, una calidad ligeramente inferior al procesado por software.

Direct Play vs. Transcoding

En servidores como Jellyfin:

    Direct Play: El cliente soporta el códec. El servidor envía el archivo tal cual. Consumo de recursos: Mínimo.

    Transcoding: El cliente no soporta el formato. El servidor debe convertir el vídeo "al vuelo". Esto puede saturar la CPU si no se dispone de aceleración hardware.

5. Streaming Adaptativo (ABR)

Tecnologías como HLS o MPEG-DASH permiten que el vídeo no se detenga si fluctúa la conexión:

    El servidor divide el vídeo en segmentos (trozos de 2-10 seg).

    Genera varias renditions (calidades: 1080p, 720p, 360p).

    El Manifest (.m3u8) lista estas opciones.

    El cliente mide su velocidad y pide el siguiente segmento en la calidad que su red soporte en ese instante.
Prompt 3:
Bienvenido a esta introducción técnica. Como verás, el mundo del vídeo y el audio digital no trata solo de archivos, sino de cómo engañamos al ojo y al oído humano para que perciban calidad utilizando la mínima cantidad de datos posible.

A partir de las fuentes que has seleccionado, he estructurado esta lección para que entiendas la jerarquía de estos conceptos, desde lo más básico (el archivo) hasta lo más complejo (el streaming que consumes a diario).
1. La Anatomía del Multimedia: Contenedores, Flujos y Metadatos

Para empezar, debemos diferenciar entre la "caja" y el "contenido".

    Contenedor: Imagina una caja o un sobre (como un archivo .mp4 o .mkv). Su función es mantener unidos y sincronizados diferentes elementos.

    Flujos o Streams: Dentro de esa "caja" hay diferentes pistas independientes. Normalmente, verás un flujo de vídeo, uno o varios de audio (idiomas) y flujos de subtítulos.

    Códec: Es el lenguaje en el que están escritos esos flujos. Es un acrónimo de "Codificador-Decodificador". El códec decide cómo se comprime la imagen para que no ocupe terabytes.

    Metadatos: Es la "etiqueta" de la caja. Información invisible que dice quién es el autor, la resolución, la fecha o el formato de color. Es información sobre los datos.

2. La Ciencia de la Compresión: Calidad vs. Espacio

Como los archivos de vídeo originales son masivos, necesitamos comprimirlos. Aquí entran dos conceptos vitales:

    Compresión Lossy (Con pérdida): Es la más común. Se elimina información que el ser humano no nota fácilmente para reducir el tamaño. Si comprimes demasiado, aparecerán "cuadraditos" (artefactos). Una vez eliminada, esa información no se puede recuperar.

    Compresión Lossless (Sin pérdida): Mantiene cada bit original. El archivo es enorme, pero la calidad es perfecta. Se usa principalmente en entornos profesionales de edición o archivos maestros.

    Bitrate (Tasa de bits): Es la cantidad de información que se procesa por segundo (se mide en Mbps o kbps).

        Diferencia clave: El Bitrate define la calidad del archivo; el Ancho de Banda es la "tubería" por donde pasa ese archivo. Si el bitrate es mayor que tu ancho de banda, el vídeo se cortará.

3. El Color y el Ojo Humano: Chroma Subsampling

Aquí es donde empezamos a ahorrar espacio de forma inteligente. El ojo humano detecta mucho mejor los cambios de brillo (Luma) que los cambios de color (Croma).

    4:4:4: No hay compresión de color. Cada píxel tiene su propio dato de color. Se usa en cine y diseño.

    4:2:2: Se usa en televisión profesional.

    4:2:0: Es el estándar de internet (YouTube, Netflix). Se elimina gran parte de la información de color porque nuestro ojo apenas lo nota, ahorrando hasta un 50% de espacio.

        ¿Cuándo es un problema? En ediciones de Chroma Key (pantalla verde). Si tienes poca información de color (4:2:0), el recorte de los bordes será defectuoso.

4. La Guerra de Códecs: De H.264 a AV1

Seguramente has visto términos como H.265 o HEVC. Es importante aclarar que H.265 y HEVC son lo mismo (High Efficiency Video Coding). Es el sucesor del H.264 (AVC), el estándar actual.

    H.265/HEVC: Comprime el doble de mejor que H.264 con la misma calidad, pero requiere mucha más potencia de procesador.

    VP9: La alternativa gratuita de Google, usada masivamente en YouTube.

    AV1: Es el nuevo estándar impulsado por el consorcio AOM (Alliance for Open Media). Es Royalty-Free (sin costes de licencia), lo que permite a gigantes como Netflix o Google ahorrar millones en derechos de autor mientras ofrecen una compresión superior a H.265.

    VVC (H.266): El futuro. Promete reducir el peso de los archivos 4K y 8K a la mitad de lo que ocupa hoy el H.265, aunque aún es muy pesado de procesar.

5. El Servidor en Acción: Transcodificación y Aceleración

Cuando montas un servidor (como Jellyfin o Plex), te encuentras con estos escenarios:

    Direct Play (Reproducción Directa): El dispositivo donde ves el vídeo soporta el códec original. El servidor solo envía el archivo. Es lo ideal porque no consume recursos.

    Transcoding (Transcodificación): Si tu TV no entiende el códec (por ejemplo, es muy vieja), el servidor debe convertir el vídeo "al vuelo" a un formato que la TV entienda. Esto es un "asesino de CPUs".

    Aceleración por Hardware: Para evitar que la CPU se queme transcodificando, usamos chips específicos de la tarjeta gráfica:

        Intel QuickSync / VAAPI: Muy eficientes en servidores con procesadores Intel.

        NVENC: El motor de las tarjetas NVIDIA.

        VideoToolbox: El sistema de Apple.

6. Streaming de Nueva Generación: ABR y Manifiestos

¿Te has fijado que YouTube a veces baja de calidad para no cortarse? Eso es el ABR (Adaptive Bitrate Streaming) y funciona mediante protocolos como HLS (de Apple) o MPEG-DASH.

Conceptos que debes dominar aquí:

    Segmentos: El servidor no te envía un archivo gigante de 2GB. Corta el vídeo en "trocitos" de pocos segundos.

    Rendition (Versión): El servidor guarda el mismo vídeo en varias calidades (1080p, 720p, 480p). Cada una es una "rendition".

    Manifest (Manifiesto): Es un archivo de texto (como el .m3u8 en HLS o .mpd en DASH). Es el "índice" que le dice al reproductor dónde están todos los segmentos y qué calidades hay disponibles.

    El Proceso: Tu reproductor mide tu velocidad de internet cada pocos segundos. Si ve que tu red va lenta, mira el Manifiesto y pide automáticamente el siguiente Segmento de una Rendition más baja para que la película no se detenga.
