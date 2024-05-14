# Trabajar con el núcleo de WordPress

## Introducción

Si has completado la lectura de [Cómo funcionan las traducciones de WordPress](https://es.wordpress.org/team/handbook/traducciones/formacion/traducir/) ahora tienes una comprensión general de cómo el proyecto WordPress gestiona la traducción y la localización.

Esto incluye cosas como qué proyectos se traducen, la prioridad de la traducción y cómo se estructuran los equipos de traducción.

Ahora, exploraremos más sobre cómo se usan las traducciones, los componentes técnicos de las traducciónes en WordPress, y cómo se relacionan con tus responsabilidades como Locale Managet o GTE.

### Internacionalización de WordPress

Los desarrolladores de WordPress optaron por utilizar el sistema de localización [GNU gettext](https://www.gnu.org/software/gettext/) para proporcionar infraestructura de localización a WordPress. gettext en un sistema maduro y ampliamente utilizado para la traducción modular de software y, es el estándar para la localización en el ámbito del código abierto / software libre.

gettext utiliza la traducción a nivel de cadena. Cada cadena de texto que se muestra a los usuarios se traduce individualmente, ya sea un párrafo o una sola palabra. En WordPress, dichas cadenas son generadas, traducidos y utilizados por los archivos PHP de WordPress a través de dos funciones PHP.

1. [__()](https://developer.wordpress.org/reference/functions/__/) se usa cuando el mensaje se pasa como argumento a otra función.
2. [_e()](https://developer.wordpress.org/reference/functions/_e/) se usa para escribir el mensaje directamente en la página.

### Tipos de fichero

Hay varios tipos de archivos utilizados en el marco de traducción gettext.

Estos archivos son utilizados o generados por herramientas de traducción durante el mismo proceso de traducción.

#### Archivos POT (Portable Object Template)

El primer paso en el proceso de localización es que se utiliza un programa para buscar en el código fuente de WordPress y seleccionar cada mensaje pasado a una función `__()` o `_e()`.

Esta lista de mensajes en inglés se introduce en un archivo de plantilla con un formato especial (archivo POT), que constituye la base de todas las traducciones.

Generalmente, puedes descargar un archivo POT para WordPress, por lo que no deberías tener que generar el tuyo propio.

También pueden crearse archivos POT independientes para temas y plugins, si el desarrollador del tema o plugin ha incluido todo el texto en las funciones `__()` o `_e()`.

#### Ficheros PO (Portable Object)

El segundo paso en el proceso de localización consiste en que el traductor traduzca todos los mensajes del fichero POT al idioma de destino, y guarde tanto los mensajes en inglés como los traducidos en un fichero PO.

#### Ficheros MO (Machine Object)

El paso final en el proceso de localización es que el archivo PO se ejecuta a través de un programa que lo convierte en un archivo binario optimizado legible por máquina (archivo MO).

Compilar las traducciones a código máquina hace que el programa localizado sea mucho más rápido a la hora de recuperar las traducciones mientras se está ejecutando.

#### Archivos JSON

A partir de WordPress 5.0, los componentes JavaScript se traducen mediante archivos JSON. Dentro del código JavaScript existen funciones de traducción similares a las del código PHP.

Estas cadenas se extraen automáticamente y se ponen a disposición para su traducción en el sitio [translate.wordpress.org](https://translate.wordpress.org/). Cuando se crea un paquete de idioma o un paquete de instalación localizado, las traducciones de las funciones JavaScript se incluyen como archivos JSON.

## Casos especiales y otros proyectos

### Traducción directa

Aunque gettext funciona bien para la mayoría de los aspectos de WordPress, hay algunos componentes del software que no se prestan a la localización con gettext o que no deberían traducirse. Estos incluyen:

- `readme.html`: Este es un archivo HTML estático, no un archivo PHP y, como tal, no se puede ejecutar a través de gettext.
- `license.txt`: Por razones legales, debe mantenerse en inglés. Sin embargo, puede añadir una versión traducida al archivo.
- `wp-config-sample.php`

![Un ejemplo de archivo wp-config-sample.php traducido](https://raw.githubusercontent.com/WPES/spain-handbook/main/assets/traducciones-formacion-traducir-6.webp)

### Parámetros de localización

Los proyectos de traducción para cada localización contienen algunos parámetros que nunca deben ser "traducidos", sino adaptados a las especificidades del idioma de destino.

Los más importantes están marcados como «Priority: high» y se encuentran en el núcleo principal de traducción y en la parte «Administration» y se pueden encontrar ordenando las cadenas de traducción en orden de prioridad descendente.

Puede ver una lista completa de estos parámetros, así como cómo o si localizarlos, en [Localization parameters](https://make.wordpress.org/polyglots/handbook/for-editors/working-with-core/#localization-parameters).

### Plugins, temas y otros proyectos

Como se mencionó anteriormente, muchas localizaciones contribuyen con traducciones más allá del núcleo de WordPress.

Para plugins, temas y otros proyectos en [translate.wordpress.org](https://translate.wordpress.org/), los paquetes de idiomas se publicarán automáticamente cuando el proyecto esté traducido al menos en un 90%.

![Ejemplo de un plugin que no ha alcanzado el umbral para su liberación](https://raw.githubusercontent.com/WPES/spain-handbook/main/assets/traducciones-formacion-traducir-7.webp)

Cuando se publica una nueva versión del plugin o tema con cadenas añadidas o actualizadas, las nuevas traducciones aprobadas para el proyecto siempre activarán la creación de un nuevo paquete de idioma.

Las traducciones del `readme` de los plugins se actualizan cadena por cadena después de ser aprobadas sin ningún umbral específico.

Las traducciones de los [proyectos Meta](https://translate.wordpress.org/locale/es/default/meta/) se despliegan en distintos intervalos.

## Lanzamiento de paquetes de WordPress

Un paquete de lanzamiento es un archivo ZIP que consiste en WordPress en su totalidad, junto con los archivos de traducción para el núcleo, los temas por defecto, Akismet y cualquier cambio personalizado que pueda tener.

Una vez completada la traducción del núcleo de WordPress, es el momento de generar un paquete. La mayoría de las localizaciones utilizan lanzamientos automáticos, lo que significa que el paquete se lanzará una vez que se alcance el umbral de traducción.

Aunque no es el método recomendado, los Locale Manager pueden crear paquetes de publicación manualmente, si su configuración regional no utiliza publicaciones automáticas.

### Publicación automática

Se recomienda que los Locale Manager se aseguren de que su configuración regional es apta para la publicación automática de paquetes. Esto se debe a que el proceso de liberación manual de paquetes ya no se recomienda y está sujeto a eliminación.

Si nunca has realizado cambios personalizados y [i18n.svn.wordpress.org](https://i18n.svn.wordpress.org/es_ES/) está completamente vacío para su configuración regional, no necesitas hacer nada. El paquete de publicación se creará automáticamente.

Si tienes cambios personalizados menores para la versión estable actual (como la 5.8), consistentes en -como mucho- los siguientes archivos:

- `readme.html`
- `license.txt`
- `wp-config-sample.php`

Asegúrate de que estos archivos existen en un directorio `branches/x.x/dist` en `i18n.svn.wordpress.org`. Si es así, el paquete de lanzamiento se creará automáticamente.

### ¿Cuándo se lanza un nuevo paquete?

Solo se creará una nueva compilación si se ha modificado una traducción después de la última compilación.

Esto significa que rechazar y aprobar una traducción dentro del proyecto WordPress en [translate.wordpress.org](https://translate.wordpress.org/) activará una nueva compilación.

Los paquetes de versiones y los paquetes de idiomas para versiones estables se construyen normalmente cada hora en punto.

### Umbrales de traducción

Los paquetes de lanzamiento y los paquetes de idiomas para versiones estables se suelen crear cada hora en punto después de que el subproyecto «x.x.x - Development» esté al menos al 90% Y el subproyecto «Administration» esté al menos al 75%.

### Liberación manual

Nota: No es recomendable liberar paquetes manualmente, por lo que se recomienda a las comunidades locales que se aseguren de que son aptas para las liberaciones automáticas. Si diriges una configuración regional que no es apta para las versiones automatizadas, esto es lo que debes saber.

En primer lugar debes obtener el número de revisión del paquete de WordPress correspondiente.

Las versiones están disponibles en la lista de etiquetas en el núcleo de Trac o en esta página en la sección «Release Revisions».

Esta lista no incluye las versiones preliminares, incluidas las betas y las versiones candidatas. Para ellos, tendrás que buscar una referencia a la versión «bump» en el registro de revisiones [build.trac.wordpress.org](https://build.trac.wordpress.org/).

Una vez que tengas el número de revisión de la versión que vas a empaquetar, es hora de construir el paquete. Para ello, sigue estos pasos:

- Inicia sesión como GTE en tu sitio local de WordPress [es.wordpress.org](https://es.wordpress.org/).
- Dirígete a **Herramientas → Publicar paquetes**.
- Desplázate hasta la sección **Crear nuevo paquete**.
- Selecciona **translate.wordpress.org** si quieres utilizar las traducciones actuales. Si ha registrado los archivos de mensajes traducidos en Subversion, seleccione **Subversion**.
- Para **Locale branch for dist files**, selecciona la ubicación de tus archivos traducidos en [i18n.svn.wordpress.org/es_ES/](https://i18n.svn.wordpress.org/es_ES/).
- Para **WordPress branch**, seleccione la rama original correspondiente.
- Para **WordPress revision**, seleccione el número de revisión que encontró al principio.
- La **WordPress Version** se utilizará como nombre del paquete (por ejemplo, 3.9, 3.9-beta3, 3.9-RC1).
- Haga clic en el botón **Crear paquete**.

Antes de publicar el paquete, descarga el archivo `zip` o `tar.gz` desde los enlaces de la parte superior de la página y pruébalo.

Cuando estés listo para publicar la versión final, haz clic en el enlace Publicación de la versión que aparece en la columna Acción. Esto marca el lanzamiento oficial de esa versión.

Se pedirá a los usuarios que actualicen el paquete de idioma en su panel de control y se actualizará la información de descarga en su sitio web.
