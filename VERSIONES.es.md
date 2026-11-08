# ZedSuite — versiones y descargas

Historial resumido en español de las versiones publicadas. Esta página pertenece al fork [dewasha40/ZedSuite-spanish](https://github.com/dewasha40/ZedSuite-spanish). Los instaladores se descargan desde las publicaciones oficiales del proyecto original; así se evita redistribuir ejecutables de terceros desde este fork.

- [Descargar la última versión oficial](https://github.com/LeZed97/ZedSuite/releases/latest)
- [Ver todas las publicaciones oficiales](https://github.com/LeZed97/ZedSuite/releases)

> Los resúmenes explican los cambios principales de cada versión. En cada enlace **Descargas y notas originales** puedes consultar las notas completas y los instaladores publicados por el autor.

## ZedSuite 1.2.6 — 8 de octubre de 2026

[Descargas y notas originales de la 1.2.6](https://github.com/LeZed97/ZedSuite/releases/tag/v1.2.6)

- **Herramientas:** añade «Fin de inyección» para EDC15P. Calcula el final de la inyección a partir del avance y la duración, usando los selectores y mapas de duración de la ECU; permite elegir mapas y aplicar el limitador SOI.
- **EDC15VM:** detecta y nombra correctamente el limitador SOI del software 038906012GN.
- **Linux:** AppImage y `.deb` se compilan ahora sobre Ubuntu 22.04 y funcionan con distribuciones de esa generación (Ubuntu 22.04/24.04, Debian 12/13 y Mint 21/22).
- **EDC15P:** mejora la detección de mapas SOI en archivos preparados con ejes modificados; muestra el eje de linealización MAP en valores originales; incorpora dos mapas BIP y elimina una detección falsa.
- **Editor y proyectos:** corrige la persistencia de cambios y ejes entre versiones, el cálculo de potencia con ediciones, la verificación del checksum y la actualización segura de proyectos.
- **Actualizaciones:** la aplicación solo acepta instaladores publicados como activos de una versión de ZedSuite en GitHub.

## ZedSuite 1.2.5 — 28 de septiembre de 2026

[Descargas y notas originales de la 1.2.5](https://github.com/LeZed97/ZedSuite/releases/tag/v1.2.5)

- **Editor:** reorganiza la cabecera del proyecto y los botones; permite cerrar un mapa abierto con doble clic; las propiedades numéricas admiten decimales y se aplican al instante.
- **Selección y edición:** permite seleccionar conjuntamente celdas y ejes, copiar mapas con sus ejes al portapapeles y pegarlos conservando valores y ejes; los cambios de ejes ya no quedan limitados por el rango de valores de las celdas.
- **Linux:** corrige el inicio de AppImage para cuentas de usuario distintas de la primera y aclara los requisitos de glibc y distribución.

## ZedSuite 1.2.4 — 18 de septiembre de 2026

[Descargas y notas originales de la 1.2.4](https://github.com/LeZed97/ZedSuite/releases/tag/v1.2.4)

- **Launch control EDC15P/EDC15VM:** conserva el mapa añadido al volver a detectar; refleja si la solución ya está aplicada y evita aplicarla dos veces.
- **Definiciones importadas:** permite importar archivos TunerPro `.xdf` y mappacks JSON desde la barra de versiones. Las definiciones importadas mantienen sus propios ejes, factores y ajustes.
- **Editor:** mejora la ventana de estimación de potencia, traduce las propiedades de mapa a los siete idiomas e identifica qué lista de mapas se exportará.

## ZedSuite 1.2.3 — 14 de septiembre de 2026

[Descargas y notas originales de la 1.2.3](https://github.com/LeZed97/ZedSuite/releases/tag/v1.2.3)

- **Mapas propios (beta):** permite abrir proyectos WinOLS `.ols`, importar versiones ROM y sus mapas, y cargar definiciones TunerPro `.xdf` o mappacks JSON en cualquier binario.
- **Múltiples mappacks:** muestra las definiciones detectadas por ZedSuite y las importadas en listas separadas, que se pueden exportar por separado.
- **Búsqueda:** añade búsqueda de mapas por nombre o dirección.
- **Límites y correcciones:** aumenta el tamaño máximo de importación de 10 a 42 MB y corrige la presentación de mapas y proyectos sin definiciones.
- **Nota:** las definiciones externas están en fase beta; soluciones, códigos de avería, estimación de potencia y checksum requieren mapas reconocidos por ZedSuite.

## ZedSuite 1.2.2 — 13 de septiembre de 2026

[Descargas y notas originales de la 1.2.2](https://github.com/LeZed97/ZedSuite/releases/tag/v1.2.2)

- **Idiomas:** añade portugués y rumano a la aplicación, el instalador, las descripciones de 1.776 códigos de avería VAG y la hoja de ruta.
- **EDC15P:** incorpora cuatro mapas PID del control de presión del turbo.
- **Linux:** AppImage y `.deb` pueden actualizarse desde la propia aplicación.
- **Detección y presentación:** corrige varios detectores EDC15/EDC16, el recuerdo de preferencias de visualización, la exportación de ejes reflejados y la organización de interruptores MAP/MAF y de humo.

## ZedSuite 1.2.1 — 13 de septiembre de 2026

[Descargas y notas originales de la 1.2.1](https://github.com/LeZed97/ZedSuite/releases/tag/v1.2.1)

- **Linux:** primera versión para Linux, con AppImage y paquete `.deb`.
- **Portapapeles:** copia y pega mapas con Excel, LibreOffice, EDC Suite y otras aplicaciones; convierte los valores respetando factores y offsets.
- **Orientación:** permite aplicar la orientación y propiedades de un mapa a mapas de su misma familia y recordar la presentación por ECU.
- **Informes:** permite poner un logotipo propio en el PDF del dinamómetro.
- **Códigos de avería:** completa las descripciones en español, italiano y alemán, además de inglés y francés.
- **Editor:** lista de mapas plegable, celdas más grandes y mejoras de zoom y ventanas.

## ZedSuite 1.2.0 — 9 de septiembre de 2026

[Descargas y notas originales de la 1.2.0](https://github.com/LeZed97/ZedSuite/releases/tag/v1.2.0)

- **EDC16:** detecta el interruptor MAP/MAF que indica qué sensor utiliza la limitación de humo.
- **Identificación:** corrige la identificación errónea de ciertos EDC15VM V6 como EDC15P, aumentando los mapas detectados en esos archivos.
- **Pantallas pequeñas:** adapta el zoom del panel principal para evitar desbordamientos.
- **Documentación:** añade una página de colaboradores y actualiza la hoja de ruta.

## ZedSuite 1.1.9 — 9 de septiembre de 2026

[Descargas y notas originales de la 1.1.9](https://github.com/LeZed97/ZedSuite/releases/tag/v1.1.9)

- **Guardado:** conserva los bytes modificados por códigos de avería y soluciones al volver a guardar una versión; impide aplicar esos cambios a la versión original sin guardar.
- **Launch control:** muestra el mapa solo en las versiones donde existe y evita duplicar una solución ya aplicada.
- **Pantallas pequeñas:** mejora el tamaño mínimo, el zoom del panel y del editor, y el ajuste de ventanas al área visible del escritorio.
- **Detección:** corrige ejes de mapas, límites de sobrepresión, mapas de limitación de aire y variantes EDC15P/EDC15VM.

## ZedSuite 1.1.8 — 8 de septiembre de 2026

[Descargas y notas originales de la 1.1.8](https://github.com/LeZed97/ZedSuite/releases/tag/v1.1.8)

- **1.4 TDI de tres cilindros:** completa la detección de mapas y mejora la identificación de archivos sin número de pieza.
- **Ejes y unidades:** corrige nombres, factores, unidades y precisión decimal en varias familias EDC15/EDC16.
- **WinOLS:** corrige la exportación de ejes, nombres y unidades en mappacks, incluida la duración de inyección y mapas N75.
- **Otros arreglos:** integra correcciones de estimación de potencia, nombres de proyectos, interruptores MAP/MAF y documentación.

## ZedSuite 1.1.7 — 7 de septiembre de 2026

[Descargas y notas originales de la 1.1.7](https://github.com/LeZed97/ZedSuite/releases/tag/v1.1.7)

- **macOS:** primera versión universal para Apple Silicon e Intel; incluye actualizaciones automáticas y almacenamiento de proyectos propio.
- **Estimación de potencia:** integra el cálculo en el editor y utiliza los cambios actuales de la versión abierta.
- **Códigos de avería:** permite gestionar DTC en varias ECU EDC15 compactas.
- **Interfaz y detección:** corrige mapas SOI y MAP/MAF, escalado del editor y ventanas; evita fallos del fondo animado cuando WebGL no está disponible.

---

### Descarga segura

Los botones anteriores llevan a las páginas oficiales de cada versión en `LeZed97/ZedSuite`. Descarga allí el instalador correspondiente a tu sistema operativo y evita instaladores republicados por terceros.
