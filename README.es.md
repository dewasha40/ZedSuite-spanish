# ZedSuite

[Español](README.es.md) · [English](README.md) · [Français](README.fr.md)

**Editor de mapas de centralitas (ECU) de código abierto, 100 % local, para Windows, macOS y Linux.**

Abre un archivo binario de una ECU Bosch EDC15/EDC16 del grupo VAG y ZedSuite detectará mapas como Driver Wish, presión del turbo, N75, SOI y limitadores de par. Puedes editarlos en una tabla, en gráficos 2D o 3D, o directamente en el volcado hexadecimal; guardar versiones, compararlas, gestionar códigos DTC compatibles, corregir checksums y exportar el binario o un mappack para WinOLS.

ZedSuite también puede abrir otros binarios con definiciones de mapas que aportes tú: proyectos WinOLS .ols, archivos TunerPro .xdf o mappacks JSON. La importación de definiciones está en fase beta. Todo se procesa localmente: no se necesita cuenta ni se suben tus archivos a la nube.

## Centralitas detectadas automáticamente

| Centralita | Método de detección |
| --- | --- |
| Bosch EDC15P | Patrones y bloques de código |
| Bosch EDC15VM+ | Patrones y bloques de código |
| Bosch EDC16U1 | Firmas estructurales |
| Bosch EDC16U31 | Firmas estructurales |
| Bosch EDC16U34 | Firmas estructurales |

Otros binarios pueden abrirse si importas sus definiciones de mapas, aunque ZedSuite no los identifique automáticamente. Las soluciones, los códigos de avería, la estimación de potencia y el checksum dependen de mapas reconocidos por la aplicación y podrían no estar disponibles para esas ECU.

## Funciones

- Editor de mapas en tabla, 2D y 3D, con navegación por teclado y edición absoluta, aditiva o porcentual.
- Volcado hexadecimal con resaltado de modificaciones respecto al original.
- Versiones por proyecto y vista para compararlas.
- Lectura y activación/desactivación de DTC en las familias compatibles EDC15 y EDC16.
- Estimación virtual de potencia y par, con informe PDF imprimible.
- Corrección de checksum implementada para familias compatibles EDC15/EDC16.
- Exportación de archivos binarios modificados y mappacks JSON compatibles con WinOLS 5.
- Detección de marca a partir de referencias de ECU.
- Temas oscuro, claro y OLED; interfaz disponible en español, inglés, francés, italiano, alemán, portugués y rumano.
- Actualizaciones automáticas desde la aplicación.

## Archivos modificados: flujo recomendado

La detección se basa principalmente en la estructura de los mapas. Para conservar la lista más completa, crea primero el proyecto con el archivo original de fábrica y después importa el archivo modificado como una nueva versión. Los mapas detectados en el original estarán disponibles al comparar las versiones.

## Descargar para Windows

Descarga el instalador desde la [página oficial de versiones](https://github.com/LeZed97/ZedSuite/releases). Para Windows de 64 bits, el archivo suele llamarse ZedSuite_x.y.z_x64-setup.exe; para Windows de 32 bits, usa la variante x86 si está publicada. ZedSuite requiere Windows 10 u 11. Comprueba que el instalador procede de la página oficial.

## Compilar desde el código fuente

Requisitos: Node.js 18 o posterior, Rust estable con las herramientas MSVC y las herramientas de compilación C++ de Visual Studio. En Windows 11, WebView2 suele venir preinstalado.

Desde la carpeta del proyecto, ejecuta en PowerShell:

```powershell
npm install
npm run app:dev
```

Para generar el instalador NSIS de Windows:

```powershell
npm run app:build
```

El instalador se genera en src-tauri/target/release/bundle/. La primera compilación descarga dependencias y puede tardar varios minutos.

## Idioma de la aplicación

La aplicación ofrece español, inglés, francés, italiano, alemán, portugués y rumano. Puedes cambiar el idioma en **Ajustes → Idioma**. Algunos nombres técnicos y nombres de mapas se conservan en inglés para que coincidan con la terminología habitual de ECU y WinOLS.

## Licencia, uso y avisos

ZedSuite se distribuye bajo GPL-3.0. La licencia cubre el código; el nombre, el logotipo y la mascota pueden tener condiciones de marca distintas. Consulta LICENSE y TRADEMARKS.md en el repositorio.

El programa está pensado para investigación, formación y uso en competición o fuera de carretera. Modificar la ECU de un vehículo de uso vial puede estar regulado o ser ilegal según el lugar, afectar a la garantía, dañar el motor o incumplir normas de emisiones. Haz copias de seguridad y eres responsable del uso que hagas de la aplicación.

- [Repositorio de este fork](https://github.com/dewasha40/ZedSuite-spanish)
- [Proyecto original](https://github.com/LeZed97/ZedSuite)
- [Versiones oficiales](https://github.com/LeZed97/ZedSuite/releases)
