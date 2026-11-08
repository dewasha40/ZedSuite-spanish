# ZedSuite

[Español](README.es.md) · [English](README.md) · [Français](README.fr.md)

![Plataformas](https://img.shields.io/badge/plataforma-Windows%20%7C%20macOS%20%7C%20Linux-0078d4) ![Motor](https://img.shields.io/badge/motor%20de%20detección-Rust-e6522c) ![Licencia](https://img.shields.io/badge/licencia-GPL--3.0-2ea44f) ![Descargas](https://img.shields.io/github/downloads/LeZed97/ZedSuite/total)

**Editor de mapas de centralitas (ECU) de código abierto, 100 % local, para Windows, macOS y Linux.**

Abre un archivo de una ECU Bosch EDC15/EDC16 del grupo VAG y ZedSuite detectará mapas como Driver Wish, Turbo Boost, N75, SOI y limitadores de par. Edítalos en una tabla, en un gráfico 2D o una superficie 3D, o directamente en el volcado hexadecimal. Guarda y compara versiones, desactiva o vuelve a activar DTC, corrige el checksum y exporta el binario o un mappack de WinOLS.

También puedes abrir otras ECU si aportas sus definiciones de mapas: un proyecto WinOLS `.ols`, un archivo TunerPro `.xdf` o un mappack JSON. El editor, el volcado hexadecimal y las versiones funcionan igual con esos archivos; consulta [Usar tus propias definiciones de mapas](#-usar-tus-propias-definiciones-de-mapas-beta), función todavía en **fase beta**.

Sin cuentas, nube ni límites: todo se ejecuta localmente y tus archivos permanecen en tu ordenador.

![Interfaz de ZedSuite](docs/screenshot.png)

## 🚗 Centralitas detectadas automáticamente

| ECU | Método de detección |
|-----|---------------------|
| Bosch EDC15P | Basado en patrones y bloques de código |
| Bosch EDC15VM+ | Basado en patrones y bloques de código |
| Bosch EDC16U1 | Basado en firmas estructurales |
| Bosch EDC16U31 | Basado en firmas estructurales |
| Bosch EDC16U34 | Basado en firmas estructurales |

**También se pueden abrir las demás ECU.** La limitación afecta a la detección automática, no a la aplicación: puedes abrir cualquier binario y proporcionar la lista de mapas mediante un proyecto WinOLS `.ols`, un archivo TunerPro `.xdf` o un mappack JSON. Consulta [Usar tus propias definiciones de mapas](#-usar-tus-propias-definiciones-de-mapas-beta).

La identificación es estricta por diseño: un archivo solo se abre como una de estas ECU si contiene pruebas positivas (números de hardware Bosch, cadenas de familia o firmas estructurales). Un volcado de 2 MB de otra ECU (EDC17, Marelli, Siemens, etc.) se rechaza para evitar interpretarlo erróneamente como EDC16.

La detección tampoco es perfecta. Cada familia se calibró con todos los archivos disponibles, pero había menos volcados EDC16U31 que de las otras familias; en algunos U31 puede que no se detecten todos los mapas. Puede ocurrir algo parecido con EDC15VM, especialmente en los volcados de 1 MB de motores V6, cuyo análisis quedó deliberadamente incompleto. Cuando se detectan todos los mapas EDC15/16, la calidad de los mappacks es excepcional frente a lo disponible en el mercado.

## 📥 Usar tus propias definiciones de mapas (beta)

Que ZedSuite no detecte un archivo ya no es un callejón sin salida. Se crea un proyecto con cualquier binario y puedes añadirle la lista de mapas:

- Un **proyecto WinOLS `.ols`**: las versiones ROM guardadas pasan a ser versiones del proyecto y los mapas definidos por su autor aparecen en su propio mappack.
- Un archivo **TunerPro `.xdf`** o un **mappack JSON**, que se importa desde la lista de mapas una vez abierto el proyecto.

Los mapas se guardan con el proyecto y se abren como los demás: tabla, vistas 2D y 3D, volcado hexadecimal, versiones, comparación y exportación de mappack. Cada archivo de definiciones crea su propia raíz en la lista, junto a la que genera el detector; así, una ECU reconocida puede mostrar ambas.

Las funciones que dependen del detector no están disponibles para esos archivos: soluciones, códigos de avería, estimación de potencia, checksum e indicador de integridad. Estas funciones utilizan mapas identificados por ZedSuite; la aplicación lo indica en lugar de abrir una ventana vacía.

> ⚠️ **Esta función está en fase beta.** El lector `.ols` se desarrolló con proyectos de WinOLS 5; no admite formatos antiguos. Es posible que aún no entienda ciertos archivos de definiciones o que interprete de otra forma sus ejes y conversiones. También pueden aparecer errores; queda mucho trabajo para cubrir todos los casos. Informa de cualquier problema e incluye el archivo si puedes: así se puede corregir.

## ⚙️ Funciones

- **Detección automática de mapas** — motor Rust integrado, con detectores por familia (Bosch EDC15/EDC16 del grupo VAG).
- **Tus propias definiciones de mapas (beta)** — abre cualquier binario e importa un proyecto WinOLS `.ols`, un archivo TunerPro `.xdf` o un mappack JSON; los mapas se guardan con el proyecto y se editan igual que los detectados.
- **Comprobación de integridad de la detección** — un indicador de confianza informa si se encontraron todos los mapas esperados para la familia; un clic muestra los que faltan.
- **Editor de mapas** — vistas de tabla, gráfico 2D y superficie 3D; navegación con teclado, copiar y pegar entre mapas, cambios absolutos, aditivos o porcentuales, propagación a mapas similares y atajos al estilo WinOLS. El gráfico 2D se usa para mapas de una línea (curvas, linealizaciones y valores únicos); las matrices completas se muestran en 3D y en la tabla para consultar valores exactos.
- **Editor hexadecimal** — vista virtualizada con minimapa y resaltado de cambios respecto al original.
- **Versiones** — versión «Ori» y versiones con nombre por proyecto, con vista de comparación.
- **Almacenamiento eficiente** — binario original y archivo de cambios por versión; se reconstruye automáticamente al exportar.
- **Dinamómetro virtual** — estimación de potencia y par a partir de los mapas, con informe PDF imprimible.
- **DTC activados/desactivados** — consulta la tabla de averías, desactiva códigos y vuelve a activarlos (EDC15 y EDC16). Cada código VAG incluye su descripción en los siete idiomas de la aplicación.
- **Soluciones** — parches de un clic (launch control, etc.). Se mantuvieron deliberadamente al mínimo para no retrasar más el lanzamiento; podrían añadirse otras más adelante.
- **Corrección de checksum** — implementada de forma nativa para las familias EDC15 y EDC16.
- **Detección automática de marca** — base de referencias de ECU integrada (números de pieza Bosch/VAG).
- **Exportación** — binarios `.bin` modificados y mappacks JSON compatibles con WinOLS 5.
- **Actualizaciones automáticas** — la aplicación comprueba una vez al día si hay nuevas versiones en GitHub y permite instalarlas con un clic.
- **3 temas** — oscuro, claro y OLED, para todo tipo de pantallas.
- **Cualquier tamaño de pantalla** — panel de mapas redimensionable y zoom en el editor al estilo del navegador, desde portátiles hasta monitores ultrapanorámicos.
- **Siete idiomas** — inglés, francés, español, italiano, alemán, portugués y rumano, en la aplicación y el instalador. Añadir otro es sencillo (un único archivo de traducciones); los nombres de los mapas se mantienen en inglés deliberadamente.

## 🔧 Trabajo con archivos modificados

El motor de detección se basa deliberadamente en la **estructura, no en los datos**: utiliza cabeceras, disposición de ejes y firmas que sobreviven a una reprogramación. Por eso detecta correctamente archivos Stage 1/2/3 en la gran mayoría de los casos; se dedicó mucho trabajo de banco a ello.

Aun así, un archivo **muy modificado** (ejes reescritos, bloques desplazados o parches de protección agresivos) puede ocultar mapas al escáner. Flujo recomendado:

1. Crea el proyecto a partir del **archivo original de fábrica**: ahí se detectan todos los mapas.
2. Importa el archivo modificado como una **nueva versión** del proyecto.

Todas las versiones del proyecto comparten la lista de mapas detectada en el original. Así tendrás el conjunto completo también en el archivo modificado y podrás comparar las versiones.

## 🏗️ Cómo se creó

ZedSuite comenzó como un SaaS web: un editor Next.js conectado a un microservicio de detección Rust (Actix). El plan era llegar a cubrir toda la gama diésel VAG hasta MD1, además de las antiguas EDC15/16/17 diésel de otras marcas. Al no disponer de tiempo para terminar ese proyecto, su autor decidió publicar lo que estaba realmente consolidado: el alcance VAG EDC15/EDC16, terminado como herramienta de escritorio local y de código abierto.

En el diseño se combinaron las funciones más interesantes de las dos herramientas utilizadas durante años: la detección automática y sencillez de EDCSuite, y la comodidad de edición de WinOLS.

El motor Rust se integró en el contenedor Tauri como comandos IPC. El frontend sigue usando la antigua interfaz `/api/*`, que `src/lib/local/api.ts` implementa ahora sobre el almacenamiento local. Así se conservó el editor de la versión web, probado durante años, eliminando la dependencia de servidores.

El motor de detección procede de largas sesiones de ingeniería inversa con volcados reales. Cada familia tiene su detector, creado localizando mapas en referencias de WinOLS/damos y extrayendo firmas estructurales (cabeceras de dimensiones, disposición de ejes, bloques selectores y separación entre mapas). Después se validó con archivos originales y modificados hasta que los resultados coincidieron mapa por mapa con las referencias. Los detectores se basan en la estructura y no en los valores para que sigan funcionando en archivos reprogramados. El mismo método se aplicó a los checksums EDC15/EDC16, reimplementados de forma nativa y validados byte a byte con pares anteriores y posteriores.

Rust fue una elección deliberada para el motor: el proyecto se concibió como SaaS y cada detección debía ejecutarse en el servidor. Además de ser más rápido que EDCSuite en C# (sin runtime de .NET ni recolector de basura, código nativo en un binario pequeño), permite detectar errores en compilación. Un análisis completo tarda menos de un segundo: unos 0,1 s en EDC15VM (512 KB), de 0,3 a 0,5 s en EDC16 (1–2 MB) y alrededor de un segundo en EDC15P, el análisis más pesado. Tauri también está escrito en Rust, así que el mismo motor que se ejecutaba en el servidor funciona ahora integrado en la aplicación.

La interfaz es una página web de HTML, CSS y TypeScript, representada por el motor del sistema: WebView2 en Windows, WebKit en macOS y WebKitGTK en Linux. El contenedor Rust abre la ventana, lee y escribe archivos y ejecuta el detector; cada plataforma se compila de forma nativa.

Por eso las versiones de macOS y Linux no necesitaron reescribirse. El panel, el editor, las vistas 2D/3D, el volcado hexadecimal y las herramientas DTC y de potencia son el mismo código en los tres sistemas. El contenedor se ocupa de la barra de título, los cuadros de diálogo, el almacenamiento de proyectos y la instalación de actualizaciones.

La tecnología web también aporta portabilidad. No se incluye un navegador, así que el instalador de Windows ocupa unos 6 MB y la aplicación se inicia en un segundo. Los gráficos, temas e idiomas se crean con herramientas adecuadas para ello, y cada corrección de la interfaz llega a Windows, macOS y Linux a la vez.

## 🧭 Qué es ZedSuite y qué no pretende ser

ZedSuite mantiene el espíritu de EDCSuite: una herramienta accesible para aprender el oficio. Abres un archivo, ves los mapas, entiendes qué hace cada uno y lo editas tú. Por eso no incluye soluciones automáticas (EGR off, DPF off o ajustes de un clic), ni las incluirá: se trata de comprender el archivo, no de pulsar un botón.

**El autor no añadirá nuevas familias de ECU.** Cada detector requirió meses de ingeniería inversa sobre cientos de archivos originales y modificados, contrastados con mappacks WinOLS y referencias damos. Repetirlo para otra familia supondría al menos dos o tres meses y reunir un corpus amplio de archivos originales y mappacks. ZedSuite se mantiene en el tiempo libre del autor y un trabajo de ese tamaño no puede regalarse. La lista de **detección automática** se limita a las VAG EDC15/EDC16, completadas con rigor. Una nueva familia podría incorporarse mediante una contribución que cumpla los requisitos indicados abajo.

Esto no impide trabajar con otras ECU: aporta tus propias definiciones y el editor funcionará con cualquier archivo, como se explicó antes. La aplicación no inventará una lista de mapas cuya fiabilidad no pueda garantizar.

## 🤝 Contribuir

Se aceptan contribuciones, especialmente nuevos detectores de ECU, siempre que sigan las normas de [CONTRIBUTING.md](CONTRIBUTING.md). Allí se explica la arquitectura, cómo se crearon las familias existentes y los requisitos antes de publicar una nueva (corpus, banco de pruebas, invariantes, cero falsos positivos, ejes y unidades correctos). El autor mantiene ZedSuite en su tiempo libre. Revisará y aceptará contribuciones, pero no puede asumir después la mitad del trabajo corrigiéndolas. Una contribución limpia y de alcance menor es mejor que una rápida que induzca a error; hasta cumplir los requisitos, la solicitud permanece como borrador.

Si encuentras un error o un mapa no detectado, abre una incidencia con el tipo de ECU y el número de software del archivo; adjunta el volcado si puedes. Así se corrige el detector: muchas de las correcciones publicadas surgieron de archivos enviados por usuarios. Los archivos solo se usan para arreglar el detector y nunca se comparten.

## 🙏 Agradecimientos

- **Dilemma**, que publicó [VAGEDCSuite](https://github.com/Blackfrosch/VAGEDCSuite) hace unos 14 años. Ese programa permitió al autor practicar y aprender este oficio: reconocimiento automático de mapas e interfaz sencilla cuando no había nada parecido. Es un trabajo enorme para una herramienta nacida en los años 2000 (¡su creador debe ser extraterrestre!). Buena parte de la lógica de detección EDC15 de ZedSuite hereda directamente el trabajo de EDCSuite.
- **Skalda**, que [mantuvo vivo VAGEDCSuite](https://github.com/skaldamramra/VAGEDCSuite), actualizando la detección y añadiendo muchos mapas EDC15. La versión privada de EDCSuite del autor partió de su trabajo y fue la que utilizó a diario hasta que pudo crear ZedSuite.

### 👥 Colaboradores

La lista de quienes aportaron código, informes o archivos, junto con los cambios y la versión en que se incorporaron, está en [CONTRIBUTORS.md](CONTRIBUTORS.md). Un volcado acompañado de un informe permite corregir la detección; los archivos solo se usan para ello y nunca se comparten.

## ⬇️ Descargar

Consulta la [página de versiones y descargas en español de este fork](https://dewasha40.github.io/ZedSuite-spanish/) para leer las notas traducidas y comparar las versiones. La página enlaza directamente a los archivos de descarga originales, sin alojar copias en este fork. También puedes abrir la [última versión oficial](https://github.com/LeZed97/ZedSuite/releases/latest) o [todas las publicaciones originales](https://github.com/LeZed97/ZedSuite/releases). Una vez instalada, la aplicación se actualiza automáticamente en los tres sistemas.

**Windows** — descarga `ZedSuite_x.y.z_x64-setup.exe` y ejecútalo (en Windows de 32 bits, usa `ZedSuite_x.y.z_x86-setup.exe`). ZedSuite requiere **Windows 10 u 11**; adaptarlo a Windows 7 habría requerido mucho más trabajo.

**macOS** — descarga `ZedSuite_x.y.z_macos-universal.dmg`, ábrelo y arrastra ZedSuite a la carpeta Aplicaciones. Incluye Apple Silicon e Intel; requiere **macOS 12 o posterior**. La aplicación no está firmada con certificado de desarrollador de Apple, por lo que en el primer inicio macOS impedirá abrirla. Ve a **Ajustes del Sistema > Privacidad y seguridad > Abrir igualmente** (en macOS 14 o anterior, haz clic derecho en la aplicación y selecciona **Abrir**). Solo hay que hacerlo una vez; las actualizaciones se abren directamente. También puedes instalar o actualizar desde Terminal:

```bash
curl -fsSL https://raw.githubusercontent.com/LeZed97/ZedSuite/master/install-macos.sh | sh
```

**Linux** — descarga `ZedSuite_x.y.z_linux-x86_64.AppImage`, dale permisos de ejecución (`chmod +x`) y ejecútalo, o instala el `.deb` con `sudo apt install ./ZedSuite_x.y.z_linux-amd64.deb`. Para x86 de 64 bits. Ambos paquetes se compilan en Ubuntu 22.04 y funcionan en Ubuntu 22.04/24.04, Debian 12/13, Mint 21/22 y distribuciones de esa generación (webkit2gtk 4.1, glibc 2.35 o posterior). También se actualizan solos: AppImage reemplaza su propio archivo y `.deb` usa la solicitud de contraseña del sistema. La compatibilidad con Linux fue aportada por [@bferd](https://github.com/bferd).

## 🗺️ Hoja de ruta

El trabajo en curso, los planes y las peticiones de usuarios están en [ROADMAP.md](ROADMAP.md), disponible también en [francés](ROADMAP.fr.md), [español](ROADMAP.es.md), [italiano](ROADMAP.it.md), [alemán](ROADMAP.de.md), [portugués](ROADMAP.pt.md) y [rumano](ROADMAP.ro.md). La misma página se abre desde el panel de la aplicación en el idioma seleccionado, mediante el botón de hoja de ruta junto al de ayuda. Incluye, entre otros temas, la lectura de números de hardware y software de archivos que la aplicación no detecta y la exportación de listas de mapas a `.xdf`.

## 📫 Contacto

- 🌐 Sitio web — [zedperf.com](https://zedperf.com)
- 📸 Instagram — [@zedperf](https://instagram.com/zedperf)
- ▶️ YouTube — [@ZedPerf](https://www.youtube.com/@ZedPerf)
- 👥 Facebook — [zedperf](https://www.facebook.com/zedperf.1/)
- 🔗 Todo en un mismo sitio: [linktr.ee/zedperf](https://linktr.ee/zedperf)

## ☕ Invítame a un café

ZedSuite es y siempre será gratuito. Si te ahorró tiempo o una licencia de WinOLS, puedes ayudar a financiar las próximas sesiones de ingeniería inversa:

- **PayPal**: [paypal.me/zedperf](https://www.paypal.com/paypalme/zedperf)
- **BTC** (Bitcoin): `bc1qj2e42vpphx73xguspqd9c6uqrs9ra0yywcq97a`
- **SOL / USDC** (Solana): `AqjSzxi7pBkwcCVkyVxBVLTk9TgPmui71bNgVgNLWrJC`
- **TRX** (Tron): `TRDgrasP7yaEKcz54r8spbmgZdRBFpNerW`

## 🚀 Primeros pasos (desarrollo)

Requisitos previos:
- [Node.js](https://nodejs.org) ≥ 18
- [Rust](https://rustup.rs) (estable): el motor de detección y el contenedor de la aplicación usan Rust/Tauri
- Windows 10/11 (WebView2 viene preinstalado en Windows 11), macOS 12 o posterior con las herramientas de línea de comandos de Xcode (`xcode-select --install`), o Linux con los [requisitos de Tauri](https://tauri.app/start/prerequisites/) (webkit2gtk 4.1, gtk3, libayatana-appindicator, librsvg)

```bash
npm install
npm run app:dev     # inicia la aplicación de escritorio con recarga automática
```

Compila el instalador:

```bash
npm run app:build   # genera el instalador NSIS en src-tauri/target/release/bundle/
```

En macOS, `npx tauri build --target universal-apple-darwin` genera `.app` y `.dmg` para ambas arquitecturas (`src-tauri/tauri.macos.conf.json` contiene la configuración específica). En Linux, `npx tauri build` genera AppImage y `.deb` (`src-tauri/tauri.linux.conf.json`). Las versiones oficiales se compilan en los equipos del autor: Windows de forma nativa y macOS/Linux en máquinas virtuales.

## 🧱 Arquitectura

```
src/                  frontend Next.js (exportación estática, servido por Tauri)
  app/dashboard/      lista de proyectos (se abre al iniciar)
  app/editor/         editor de mapas
  lib/local/          backend local: almacenamiento de proyectos y puente API
  lib/ecu/            utilidades ECU TypeScript (listas DTC, checksums)
src-tauri/            contenedor de escritorio Rust
  src/detector/       motor de detección (una carpeta por fabricante)
  src/commands.rs     comandos IPC expuestos al frontend
```

Los proyectos se guardan en `%APPDATA%/com.zedsuite.app/projects/` en Windows, `~/Library/Application Support/com.zedperf.zedsuite/projects/` en macOS y `~/.local/share/com.zedsuite.app/projects/` en Linux: una carpeta por proyecto con el binario original, los metadatos y las versiones.

## ⚖️ Licencia y marcas registradas

[GPL-3.0](LICENSE): puedes usar, estudiar, modificar y redistribuir ZedSuite, pero las obras derivadas deben publicarse con la misma licencia. Si mejoras el motor de detección o añades compatibilidad con ECU, la comunidad recibe esas mejoras.

**La licencia cubre únicamente el código.** El nombre, el logotipo y la mascota de ZedSuite son marcas de ZedPerf y están excluidos expresamente de la licencia GPL (§7(e)): se permiten los forks, pero deben utilizar su propio nombre e identidad visual. Consulta la política completa en [TRADEMARKS.md](TRADEMARKS.md). Las versiones oficiales se publican exclusivamente en la [página de versiones del repositorio original](https://github.com/LeZed97/ZedSuite/releases).

## ⚠️ Aviso legal

ZedSuite está pensado para investigación, formación y uso en competición o fuera de carretera. Modificar la ECU de un vehículo que circula por vías públicas puede ser ilegal según la jurisdicción, anular la garantía, dañar el motor o incumplir la normativa de emisiones. Cada usuario es responsable del uso que haga del software.

**Aviso de seguridad**: el software de reprogramación es un objetivo habitual de quienes distribuyen malware mediante herramientas gratuitas. Descarga siempre el instalador desde el [GitHub oficial](https://github.com/LeZed97/ZedSuite/releases); es la única forma de asegurarte de que es legítimo.

---

- [Fork en español](https://github.com/dewasha40/ZedSuite-spanish)
- [Proyecto original](https://github.com/LeZed97/ZedSuite)
