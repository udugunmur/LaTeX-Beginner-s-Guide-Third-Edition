# LaTeX Beginner's Guide
## Capítulo 1: Primeros Pasos con LaTeX

Está familiarizado con el software de procesamiento de textos: escribe algo de texto y lo que ve en la pantalla es lo que obtiene en la página. En contraste, **LaTeX** es un sistema de composición tipográfica: escribe texto plano con comandos de marcado y LaTeX lo transforma en una salida impecable. Produce impresiones y archivos PDF de alta calidad basados en algoritmos sofisticados para justificación, división de palabras (*hyphenation*), alineación de texto, equilibrio de espacios en blanco y colocación de figuras. Viene con estilos de formato predefinidos para encabezados, márgenes y diseño general de página, los cuales puede personalizar.

Ahora que está listo para ir más allá de esos procesadores de texto "lo que ves es lo que obtienes" (*WYSIWYG*) y comenzar a utilizar un sistema diseñado para la precisión y la coherencia, está en el lugar correcto. Demos los primeros pasos juntos.

Este libro le guiará a lo largo del camino, ayudándole a aprovechar al máximo las capacidades de LaTeX. En primer lugar, examinaremos sus puntos fuertes y algunos desafíos antes de configurar las herramientas que necesitará.

En este capítulo, nos familiarizaremos con LaTeX, qué es y cómo instalarlo y utilizarlo. Específicamente, cubriremos lo siguiente:

- Comprendiendo el concepto de LaTeX
- Instalación y uso de LaTeX
- Trabajando con LaTeX en línea
- Acceso a la documentación

Al final de este capítulo, tendrá LaTeX funcionando, sabrá cómo editar y componer un documento básico, y comprenderá dónde encontrar más documentación.

¡Empecemos!

---

### Su compra incluye una copia gratuita en PDF + extras exclusivos

Su compra incluye una copia en PDF sin DRM de este libro, una prueba de 7 días para la biblioteca Packt+ (no se requiere tarjeta de crédito) y extras exclusivos adicionales. Consulte la sección *Beneficios gratuitos con su libro* en el Prefacio para desbloquearlos instantáneamente y maximizar su aprendizaje.

---

### Requisitos técnicos

Nos centraremos aquí en el sistema operativo Windows, pero también puede instalar LaTeX en macOS, Linux y otros sistemas.

Una instalación completa suele requerir alrededor de 8 GB de espacio en disco en cualquier sistema.

Si prefiere no instalar nada, puede utilizar una plataforma en línea como Overleaf, que se ejecuta completamente en su navegador y requiere una conexión constante a Internet. Cubriremos Overleaf al final de este capítulo.

Todos los ejemplos de código de este libro están disponibles para su descarga en GitHub en [https://github.com/PacktPublishing/LaTeX-Beginner-s-Guide-Third-Edition](https://github.com/PacktPublishing/LaTeX-Beginner-s-Guide-Third-Edition).

En el sitio web del libro, [https://latexguide.org](https://latexguide.org/), puede leer, editar y compilar todos los ejemplos de código directamente en su navegador, sin necesidad de instalación. Todo lo que necesita es un dispositivo con un navegador web moderno y JavaScript habilitado, ya sea una PC, computadora portátil, tableta o teléfono inteligente.

---

### Comprendiendo el concepto de LaTeX

LaTeX es un software libre y de código abierto para la composición tipográfica de documentos. Es un sistema de preparación de documentos basado en comandos de marcado, donde usted describe la estructura y el formato de su contenido utilizando comandos de texto plano.

Fue escrito inicialmente por Leslie Lamport en la década de 1980 y está construido sobre el motor de composición tipográfica TeX de Donald Knuth, quien comenzó a desarrollarlo a finales de la década de 1970. Tiene una larga historia; puede leer sobre ella en [https://tug.org/whatis.html](https://tug.org/whatis.html). Dado que Knuth derivó el nombre de "tau épsilon ji", abreviando la palabra griega "τέχνη" para arte, artesanía o tecnología, la gente comúnmente lo pronuncia como "Jek" o "Tek". Algunos prefieren decir "tek" como en "tecnología". Lo que no debería sonar es como "teks". Para LaTeX, es similar; lo pronunciamos como "Latej" o "Leitej".

Veamos cómo podemos aprovechar al máximo LaTeX.

#### Beneficios de LaTeX

LaTeX es especialmente adecuado para documentos científicos y técnicos. La composición tipográfica superior de fórmulas matemáticas de LaTeX es legendaria. Si es estudiante o científico, LaTeX es, con diferencia, la mejor opción. Incluso si no necesita sus capacidades científicas, LaTeX tiene mucho que ofrecer: produce resultados sobresalientes de alta calidad y es increíblemente estable. Maneja documentos grandes y complejos con facilidad.

Algunas de las fortalezas notables de LaTeX son sus capacidades de referencias cruzadas, numeración automática y la generación de listas de contenidos, figuras y tablas, índices, glosarios y bibliografías. Es multilingüe con funciones específicas para cada idioma y puede utilizar incluso funciones avanzadas de PDF.

Si bien es la opción perfecta para tesis de estudiantes y publicaciones de científicos avanzados, LaTeX es increíblemente flexible: existen plantillas para cartas, CV, presentaciones, facturas, libros de filosofía, textos legales, partituras musicales e incluso notación de partidas de ajedrez. Cientos de desarrolladores y usuarios avanzados de LaTeX han escrito miles de plantillas, estilos y herramientas valiosas para todos los propósitos imaginables. Estos se recopilan y categorizan en línea en servidores de archivos.

Puede aprovechar la impresionante alta calidad de LaTeX comenzando con sus estilos predeterminados y confiando en su formato inteligente integrado. Pero puede personalizar casi todos los aspectos si necesita algo más a medida. La comunidad de LaTeX ha desarrollado una amplia gama de extensiones que cubren casi todos los requisitos de formato con los que pueda encontrarse.

#### Virtudes del código abierto

LaTeX es completamente de código abierto, con código legible libremente para todos. Esto permite a cualquiera estudiar y ajustar todo, desde el núcleo de LaTeX hasta los paquetes de extensión más recientes. Pero, ¿qué significa esto para usted como principiante? Una comunidad de LaTeX amplia, activa y solidaria cuenta con muchas personas amables y dispuestas a ayudar. Incluso si no puede beneficiarse del código fuente directamente, ellos pueden leerlo y ayudarle. Simplemente únase a un foro web de LaTeX y plantee allí sus preguntas. Los ayudantes, si es necesario, profundizarán en las fuentes de LaTeX y, con toda probabilidad, encontrarán una solución para usted, a veces recomendando un paquete adecuado y a menudo proporcionando una redefinición de un comando predeterminado.

Hoy en día, nos beneficiamos de más de 40 años de desarrollo continuo por parte de la comunidad de LaTeX. La filosofía del código abierto hizo posible un enorme progreso, ya que se invita a cada usuario a estudiar, mejorar y ampliar el software. El [Capítulo 15](https://subscription.packtpub.com/book/business-other/9781805804574/15), *Uso de recursos en línea*, le conectará con la comunidad en línea.

#### Separación de forma y contenido

Una idea central detrás de LaTeX es que el autor no debería distraerse con el formato mientras escribe. En lugar de ajustar manualmente la apariencia del texto, usted se concentra en la estructura y el significado de su contenido. Por ejemplo, utiliza un comando de LaTeX para marcarlo como encabezado de capítulo en lugar de escribir el título del capítulo con letras grandes y en negrita. Puede dejar que LaTeX aplique el estilo al encabezado o definir cómo se verán los encabezados en la configuración del documento, solo una vez para todo el documento. LaTeX se basa en archivos de estilo llamados clases y paquetes, lo que facilita el diseño y la modificación coherente de la apariencia y los detalles de todo el documento.

#### Portabilidad

LaTeX está disponible para casi todos los sistemas operativos principales, como Windows, Linux y macOS. Utiliza archivos de texto plano para documentos y estilos, que son legibles y editables en todos los sistemas operativos y versiones. Eso significa que sus documentos son portátiles y que LaTeX producirá el mismo resultado en cada sistema. Varias colecciones de software de LaTeX contienen motores compiladores, herramientas y estilos. Las llamamos distribuciones TeX. Nos centraremos en la distribución TeX Live, ya que está disponible para Windows, Linux y macOS. En Mac, la versión personalizada de TeX Live se llama MacTeX.

LaTeX no tiene su propia interfaz gráfica de usuario, lo cual es una de las razones por las que es tan portátil. Puede elegir cualquier editor de texto. Sin embargo, existen muchos editores específicos de LaTeX para cada sistema operativo importante. Algunos, como TeXworks, se ejecutan en múltiples sistemas, lo cual es una de las razones por las que lo usaremos en nuestro libro. Otra razón importante es que es sencillo y el más adecuado para principiantes.

LaTeX genera salida en PDF, lo cual es ideal para compartir, ya que se puede imprimir y leer en la mayoría de las computadoras y se ve igual independientemente del sistema operativo. Además de PDF, admite salida DVI, PostScript y HTML, sentando las bases para su distribución impresa y en línea, como en computadoras personales, lectores de libros electrónicos como el Kindle y teléfonos inteligentes. En resumen, LaTeX es portátil de tres maneras: sus archivos fuente, su implementación y la salida final.

#### Protección para su trabajo

Los documentos de LaTeX se almacenan en un formato de texto legible por humanos, no en algún formato de procesamiento de textos propietario exclusivo de un proveedor de software específico, que incluso puede diferir entre versiones del mismo software.

Intente abrir un documento de hace 20 años escrito con un procesador de textos comercial. Incluso si puede abrir el archivo, su apariencia visual se vería alterada, el formato podría desajustarse o la visualización podría ser incorrecta. LaTeX promete que el documento siempre será legible y producirá sistemáticamente el mismo resultado. A pesar del desarrollo continuo, mantiene una sólida compatibilidad con versiones anteriores.

Los documentos de los procesadores de texto pueden contener virus o macros maliciosas que pueden dañar el sistema informático y los datos. Los virus no infectan los documentos de LaTeX porque difícilmente pueden ocultarse en un archivo de texto plano.

#### Cómo empezar con LaTeX

LaTeX puede parecer un desafío al principio, pero este libro le ayudará a dominarlo paso a paso, tema por tema.

Escribir en LaTeX se parece a la programación, pero no se deje intimidar. Rápidamente se familiarizará con los comandos más utilizados, y los editores de texto con autocompletado y resaltado de sintaxis le brindarán soporte. Algunos incluso le ofrecen menús y cuadros de diálogo para insertar comandos.

¿Le preocupa que pueda llevar mucho tiempo producir resultados utilizables? No lo esté; este libro le brindará un inicio rápido con abundantes ejemplos prácticos, para que aprenda haciendo y gane confianza. Se pueden encontrar muchos más ejemplos en Internet. En el [Capítulo 15](https://subscription.packtpub.com/book/business-other/9781805804574/15), *Uso de recursos en línea*, exploraremos los recursos en línea. Hay foros de ayuda de LaTeX donde puede obtener respuestas a sus preguntas. Uno de ellos tiene una sección dedicada específicamente a los lectores de este libro y sus obras complementarias: [https://latex.org/books](https://latex.org/books).

#### Enfoques para trabajar con LaTeX

Hay dos formas principales de empezar a trabajar con LaTeX:

1. El enfoque tradicional es instalar LaTeX en su propia computadora. Es bastante sencillo y explicaremos detalladamente cómo instalarlo en Windows en la sección *Instalación y uso de LaTeX*.
2. Otra forma es utilizar LaTeX completamente en línea en su navegador. No se necesita instalación; solo necesita una computadora, tableta o teléfono conectado a Internet. Exploraremos esta opción en la sección *Trabajando con LaTeX en línea* al final de este capítulo.

Comenzaremos configurando LaTeX localmente en nuestra computadora. Si lo desea, puede omitir este momento y saltar a la sección *Trabajando con LaTeX en línea*, y luego decidir qué enfoque prefiere adoptar.

---

### Instalación y uso de LaTeX

Comencemos instalando la distribución de LaTeX TeX Live. Está disponible para Windows, Linux, macOS (como MacTeX) y otros sistemas operativos tipo Unix. TeX Live se desarrolla activamente y recibe un buen mantenimiento, lo que lo convierte en una opción confiable en todas las plataformas.

Otra distribución TeX excelente y fácil de usar para Windows es MiKTeX. Es fácil de instalar, como una aplicación común de Windows. Puede descargarla desde [https://miktex.org](https://miktex.org/). Visite [https://latexguide.org/distributions](https://latexguide.org/distributions) para obtener una comparación detallada y actualizada.

Puede instalar TeX Live de dos maneras: en modo de usuario único solo para su cuenta, o para todo el sistema para todos los usuarios de una computadora. Este último se llama modo administrador. Requiere ejecutar la instalación como administrador: inicie sesión con una cuenta de administrador o haga clic derecho en el programa de instalación y elija *Ejecutar como administrador*.

Si usted es la única persona que usa su computadora, se recomienda una instalación de usuario único.

Comencemos visitando la página principal de TeX Live y revisando las opciones de instalación disponibles. Para hacer esto, abra la página principal de TeX Live usando [https://tug.org/texlive/](https://tug.org/texlive/):

> **Figura 1.1** – Página principal de TeX Live

Siéntase libre de explorar la página de inicio con más detalle para estudiar la información ofrecida allí, aunque en este libro nos centraremos en dos tipos de instalación:

- Instalar TeX Live en línea mediante el asistente instalador de red; este método requiere una conexión constante a Internet durante típicamente unas dos horas o más.
- Instalar TeX Live fuera de línea; este método comienza con una descarga considerable, pero luego podemos continuar sin tener Internet disponible, con menor riesgo de interrupción.

Antes de comenzar la instalación, echemos un vistazo a los archivos de LaTeX y a las convenciones de empaquetado con diferente granularidad:

- Un **archivo de clase** de LaTeX define la estructura general y el diseño de un documento, como el comportamiento de las secciones, las fuentes predeterminadas, los márgenes y más. Los archivos de clase tienen la extensión de archivo `.cls`.
- Un **paquete**, también llamado archivo de estilo, es un archivo único de LaTeX con algunas macros para agregar características específicas o proporcionar una apariencia y un estilo de documento particulares. Su extensión de archivo es `.sty`.
- Un **paquete integrado (*bundle*)** es un conjunto de archivos relacionados con un propósito similar, como clases, paquetes y archivos de soporte.
- Una **colección** es un conjunto más extenso de paquetes para un campo de interés. Puede ser, por ejemplo, un conjunto extenso de paquetes de matemáticas y ciencias naturales, paquetes de música o paquetes relacionados con gráficos.
- Un **esquema (*scheme*)** es una instalación de LaTeX de un tamaño específico. Puede ser mínimo (lo mínimo necesario para trabajar), básico (lo necesario habitualmente) o completo (todo lo disponible).

Con este conocimiento, ahora podemos instalar LaTeX. La opción más sencilla es instalarlo todo completamente; ese es el esquema completo (*full scheme*). Esto garantiza que todos los paquetes estén disponibles desde el principio, por lo que no encontrará funciones faltantes más adelante.

Veamos dos métodos de instalación en una PC con Windows. El primero instala TeX Live a través de Internet, lo que requiere una buena conexión a Internet. Si no tiene una buena conexión a Internet, pase a la siguiente sección, *Instalación de TeX Live fuera de línea*.

#### Instalación de TeX Live mediante el asistente instalador de red

Descargaremos el instalador de red de TeX Live e instalaremos la distribución completa de TeX Live en nuestra computadora. Para hacer esto, siga estos pasos:

1. Haga clic en *download*, como se ve en la Figura 1.1, o vaya a [https://tug.org/texlive/acquire-netinstall.html](https://tug.org/texlive/acquire-netinstall.html):

> **Figura 1.2** – Instrucciones de instalación

2. Descargue el programa instalador ejecutable, `install-tl-windows.exe`, y ejecute el programa.
3. Confirme el modo de instalación (*Single-user* o *Administrator*), haga clic en *Next* y luego en *Install*.
4. El instalador de red detectará automáticamente el idioma de su sistema operativo. Puede cambiar el idioma de la interfaz gráfica de usuario (GUI) haciendo clic en *GUI language* en el menú de la ventana que se abre, como podemos ver en la Figura 1.3:

> **Figura 1.3** – Instalador de TeX Live

5. Puede cambiar la raíz de instalación (*installation root*): la ubicación de todos los archivos instalados de TeX Live en su disco duro. La instalación predeterminada generalmente funciona bien, aunque puede hacer clic en *Advanced* para ajustar opciones específicas, como puede ver aquí en la Figura 1.4:

> **Figura 1.4** – Opciones avanzadas del instalador de TeX Live

6. Puede cambiar la configuración de *Scheme* (las opciones incluyen *full*, *medium* y *small*) y personalizar la cantidad de colecciones de software, como formatos instalados, fuentes, estilos, paquetes de gráficos, editor, soporte de idiomas y más. Dado que las opciones recomendadas ya son las partes más significativas de la instalación, desmarcar algunas colecciones no ahorrará mucho espacio. Se recomienda el esquema completo (*full*) para que no se pierda nada más adelante.
7. Haga clic en *Install* para continuar. Ahora, no se necesita ninguna intervención durante un buen rato, y puede relajarse mientras se descargan e instalan miles de paquetes TeX:

> **Figura 1.5** – Progreso de la instalación

8. Finalmente, recibirá un mensaje de bienvenida. Haga clic en *Close* para finalizar la instalación.

Ha completado la configuración de TeX Live. Su menú Inicio ahora contiene una carpeta **TeX Live 2025** que contiene seis programas:

> **Figura 1.6** – TeX Live en el menú Inicio de Windows

Veamos brevemente cada uno de los programas:

- **DVIOUT DVI viewer**: Este es un programa visor para el formato de salida clásico de LaTeX, DVI (hoy en día, la mayoría de la gente elige la salida en PDF, por lo que probablemente no lo necesitará).
- **TeX Live command-line**: Utilícelo si desea ejecutar otros programas de TeX Live en la línea de comandos.
- **TeX Live documentation**: Esto abre el manual de TeX Live en su navegador web.
- **TeX Live Manager**: Esta es su herramienta para la gestión de paquetes (por ejemplo, para instalar y actualizar paquetes de LaTeX).
- **TeXworks editor**: Este es un editor desarrollado para crear documentos LaTeX cómodamente. Haremos un uso extensivo de TeXworks en este libro.
- **Uninstall TeX Live**: Úselo antes de instalar una nueva versión de TeX Live desde cero, o si desea instalar MiKTeX en su lugar.

Ahora pasaremos por la instalación fuera de línea de TeX Live.

#### Instalación de TeX Live fuera de línea

Cada año, el grupo de usuarios de TeX crea un DVD con la colección de software de TeX. Puede solicitar una copia aquí: [https://tug.org/dvd](https://tug.org/dvd).

También puede descargarlo usted mismo. Ahora descargaremos una imagen ISO de TeX Live con un tamaño de aproximadamente 6 GB. Después de la extracción, podemos grabarla en un DVD y ejecutar la instalación desde allí. Para hacer esto, siga estos pasos:

1. Visite el área de descarga en [https://tug.org/texlive/acquire-iso.html](https://tug.org/texlive/acquire-iso.html).
2. Descargue el archivo `texlive.iso`. Si es posible, utilice un gestor de descargas, especialmente si su conexión a Internet no es estable.
3. Grabe el archivo ISO en un DVD usando un software de grabación que admita el formato ISO, o extráigalo en su disco duro. Por ejemplo, el programa gratuito 7-Zip puede extraer archivos ISO.
4. Entre los archivos extraídos o en su DVD, encontrará los archivos por lotes del instalador `install-tl` e `install-tl-advanced`. Elija uno, inícielo y complete la instalación de manera similar a la instalación en línea. Más información disponible en [https://tug.org/texlive/quickinstall.html](https://tug.org/texlive/quickinstall.html).

Instalar TeX fuera de línea fue exactamente igual que la primera instalación. Sin embargo, esta vez tiene todos los datos y no necesitará una conexión a Internet durante la instalación ni para otra instalación posterior. Este enfoque de descarga se recomienda especialmente si es previsible que instale TeX Live en otra computadora más adelante, o si desea compartirlo con amigos o colegas.

Como TeX también se ejecuta en otros sistemas operativos, echemos un vistazo rápido a los demás sistemas.

#### Instalación de TeX Live en otros sistemas operativos

TeX también se ejecuta en muchos otros sistemas además de Windows. He aquí un vistazo rápido:

- **macOS**: Puede descargar una versión personalizada de TeX Live en [https://tug.org/mactex](https://tug.org/mactex). Descargue el archivo de gran tamaño `MacTeX.pkg` y haga doble clic en él para instalarlo. Mostrará instrucciones muy directas. MacTeX incluye TeXShop, un editor muy similar a TeXworks. Este último se puede instalar por separado.
- **Ubuntu Linux**: Utilice el Centro de software para instalar paquetes de TeX Live o ejecute `sudo apt-get install texlive-full` para obtener todo.
- **Debian Linux**: Utilice la herramienta Synaptic para instalar paquetes de TeX Live o ejecute `apt-get install texlive-full` (mediante `sudo` o como usuario `root`) para obtener todo.
- **Red Hat, CentOS y Fedora Linux**: Utilice el gestor de paquetes de Red Hat, o `yum` a través del símbolo del sistema, como `yum install texlive-scheme-full`, o DNF: `sudo dnf install texlive-scheme-full`.
- **Otros**: Visite [https://tug.org/texlive/quickinstall.html](https://tug.org/texlive/quickinstall.html) y siga las instrucciones.

Si desea la versión más reciente de TeX Live, considere descargar e instalar la versión más actual desde el sitio web oficial en lugar de la versión de los repositorios del sistema operativo, como se mencionó en el último punto.

En la siguiente sección, veremos cómo actualizar su instalación y agregar nuevos paquetes.

#### Actualización de TeX Live e instalación de nuevos paquetes

Los desarrolladores de LaTeX lanzan actualizaciones periódicamente, tanto para nuevas funciones como para corrección de errores. Es una buena idea actualizar su sistema de vez en cuando.

Para hacer esto, abra el menú Inicio, vaya a la carpeta TeX Live e inicie el **TeX Live Manager**, al que también se le conoce de forma abreviada como `tlmgr`, y también se llama TeX Live Shell. Esta aplicación se utiliza tanto para actualizar como para instalar paquetes adicionales.

Eche un vistazo a la siguiente captura de pantalla para que podamos hablar sobre cómo utilizar TeX Live Manager:

> **Figura 1.7** – El TeX Live Manager

1. La primera sección en TeX Live Manager muestra la sección **Repository**. Un repositorio es un servidor que aloja un archivo de software de TeX Live. Si el repositorio predeterminado no está disponible o es demasiado lento en su área, puede hacer clic en *Options* para elegir otro repositorio de una lista.
2. Haga clic en **File | Load repository** para sincronizar LaTeX con el estado más reciente del software.
3. La sección **PACKAGE LIST** le permite buscar paquetes por nombre o filtrar la vista para ver todos los paquetes disponibles o solo aquellos instalados, no instalados o actualizables. En el centro de la Figura 1.7, puede ver una opción para ajustar la granularidad y ver todos los paquetes, todas las colecciones y esquemas, o solo los esquemas.
4. La sección inferior muestra los paquetes coincidentes cuando se selecciona un filtro, con una breve descripción y el número de versión. Puede elegir paquetes aquí. Luego, puede hacer clic en **Install marked** si desea instalar los paquetes seleccionados o hacer clic en **Remove marked** para desinstalarlos.
5. Una forma sencilla es simplemente hacer clic en **Update all**. Si el botón **Update tlmgr** está habilitado y se puede hacer clic en él, significa que hay una actualización disponible de TeX Live Manager y puede hacer clic en el botón *Update tlmgr* para actualizar la herramienta en sí.

El procedimiento de actualización se aplica únicamente a la versión actual de TeX Live. Cada año se lanza una nueva versión de TeX Live, generalmente en marzo. Lo mejor sería desinstalar la versión actual de TeX Live para una actualización anual y luego instalar la nueva versión desde cero. Puede consultar el calendario de lanzamiento planificado y las fechas estimadas en [https://tug.org/texlive](https://tug.org/texlive).

Ahora que hemos configurado todo, es hora de empezar a escribir con LaTeX.

#### Creación de nuestro primer documento

Hemos instalado TeX y un editor; ahora, lancémonos de lleno escribiendo nuestro primer documento LaTeX utilizando el editor TeXworks.

> **Nota para usuarios de Mac**: Por favor, utilice la tecla `Cmd` cuando vea la tecla `Ctrl` aquí.

Nuestro primer objetivo es crear un documento sencillo que imprima solo una frase. Queremos utilizarlo para comprender la estructura básica de un documento LaTeX. Siga estos pasos:

1. Inicie el editor TeXworks haciendo clic en el icono del escritorio o abriéndolo en el menú Inicio. En la Figura 1.8, puede ver el editor con el menú, los botones y la barra de herramientas.
2. Haga clic en el botón **New** (o presione `Ctrl + N`) o elija **File | New** en el menú.
3. Introduzca las siguientes líneas:

```latex
\documentclass{article}
\begin{document}
This is our first document.
\end{document}
```

4. Haga clic en el botón **Save** (o presione `Ctrl + S`) para guardar el documento. Luego, elija una ubicación para almacenar sus documentos LaTeX, idealmente en su propia carpeta.
5. Asegúrese de que en el campo desplegable de la barra de herramientas de TeXworks esté seleccionado **pdfLaTeX** (este debería ser el valor predeterminado de todos modos):

> **Figura 1.8** – El editor TeXworks

6. Haga clic en el botón **Typeset** o presione `Ctrl + T`.
7. La ventana de salida se abrirá automáticamente. Échele un vistazo:

> **Figura 1.9** – La salida PDF en el editor TeXworks

Esto cubre los primeros momentos en la vida de un documento LaTeX. Editará, compondrá tipográficamente (*typeset*), comprobará el resultado y editará de nuevo. Solo recuerde guardar su trabajo con frecuencia. Afortunadamente, componer un documento lo guarda automáticamente.

A diferencia de los procesadores de texto tradicionales, LaTeX no muestra los cambios de formato de inmediato, pero siempre estará a solo un clic de distancia de ver el resultado final.

#### Exploración de editores avanzados de LaTeX

Si se siente cómodo con software complejo y prefiere un editor potente y rico en funciones, eche un vistazo a los siguientes editores de LaTeX. Visite sus sitios web para encontrar capturas de pantalla y leer sobre sus características:

- **TeXmaker**: Un editor multiplataforma que se ejecuta en Windows, Linux, macOS y otros sistemas Unix: [https://xm1math.net/texmaker](https://xm1math.net/texmaker)
- **TeXstudio**: Otro editor completo que se ejecuta en todas las plataformas principales: [https://texstudio.org](https://texstudio.org/)
- **Kile**: Un editor fácil de usar para sistemas operativos con el entorno de escritorio KDE, como Linux: [https://kile.sourceforge.io](https://kile.sourceforge.io/)
- **TeXShop**: Un editor muy popular y fácil de usar para macOS: [https://pages.uoregon.edu/koch/texshop](https://pages.uoregon.edu/koch/texshop)

Todos estos editores son gratuitos y de código abierto. Puede encontrar más opciones en [https://latexguide.org/editors](https://latexguide.org/editors).

Los editores en línea funcionan en cualquier dispositivo con conexión a Internet. Examinemos de cerca un editor y compilador en línea en la siguiente sección.

---

### Trabajando con LaTeX en línea

Se recomienda que instale LaTeX en su computadora, pero hacerlo puede ocupar alrededor de 8 GB en su disco duro y tomar alrededor de 2 horas o más.

¿Qué tal si simplemente usa LaTeX en su navegador de Internet? Aquí entra **Overleaf**. Es un servicio de LaTeX puramente en línea que matemáticos entusiastas de TeX iniciaron en 2011. Puede acceder a él a través de este enlace: [https://www.overleaf.com](https://www.overleaf.com/).

En esta sección sobre Overleaf, haremos lo siguiente:

- Comprobar los requisitos de Overleaf
- Ver los beneficios de Overleaf
- Evaluar posibles advertencias
- Utilizar el editor de Overleaf
- Probar Writefull

Vayamos a Internet ahora.

#### Qué requiere y ofrece Overleaf

Para utilizar Overleaf, solo necesita un navegador de Internet, como Firefox, Chrome, Opera, Edge o Safari. No necesita ningún software local como un compilador de LaTeX, un editor o un visor de PDF.

Es gratuito para un uso básico, y eso incluye mucho. Proporciona un TeX Live completo con proyectos ilimitados, un editor repleto de funciones, colaboración en tiempo real con otro usuario y cientos de plantillas listas para usar. Sin embargo, los documentos más grandes pueden agotar el tiempo de espera debido a recursos informáticos limitados. En particular, una cuenta gratuita es muy limitada en tiempo de compilación.

Una suscripción personal o profesional avanzada cuesta dinero y proporciona funciones avanzadas, como las siguientes:

- Más colaboradores por proyecto
- Soporte para documentos más grandes que requieren más tiempo de compilación
- Historial del documento (navegar hacia adelante y hacia atrás entre revisiones)
- Gestión avanzada de bibliografía (Mendeley, Zotero y Papers)
- Paleta de símbolos integrada
- Integración con GitHub y Dropbox
- Acceso prioritario a soporte personalizado

Las características avanzadas van más allá de la funcionalidad habitual de LaTeX. Podría ser elegible para un acceso completo a través de su institución; muchas universidades y organizaciones de investigación se asocian con Overleaf para ofrecer planes prémium a sus miembros.

#### Beneficios de Overleaf

Veamos lo que puede ganar al usar Overleaf, en comparación con el uso de un sistema LaTeX tradicional localmente en su computadora. Con Overleaf, usted puede:

- Trabajar desde cualquier dispositivo, como una PC, computadora portátil, tableta o teléfono inteligente
- Usarlo en una computadora de trabajo bloqueada donde no puede instalar software usted mismo
- Acceder a sus proyectos desde cualquier lugar (ya sea una computadora personal, de trabajo o de una biblioteca) una vez que inicie sesión con su contraseña
- Si invita a alguien a trabajar con usted, ambos pueden editar y ver instantáneamente los cambios del otro, lo que facilita la colaboración
- Tener una vista previa automática en tiempo real del resultado en PDF mientras escribe
- Realizar un seguimiento de los cambios con un historial de versiones integrado
- Anotar el código fuente de LaTeX con comentarios y respuestas a comentarios
- Trabajar con el sistema LaTeX más reciente sin necesidad de instalar una actualización

Sin embargo, existen algunas concesiones con Overleaf. Veámoslas a continuación.

#### Advertencias sobre el trabajo en línea

Vale la pena señalar algunas limitaciones:

- Necesitará una conexión constante a Internet.
- Dado que sus documentos se almacenan en línea, debe confiar a Overleaf la seguridad y privacidad de los datos. Consulte [https://www.overleaf.com/legal](https://www.overleaf.com/legal).
- Está vinculado a la plataforma de Overleaf; hasta que actualice su versión de LaTeX, podría quedar ligeramente por detrás del TeX Live oficial.
- El rendimiento depende de sus servidores y de su conexión de red, no solo del rendimiento de su propia computadora.
- Overleaf podría no estar disponible debido a mantenimiento o un incidente técnico que afecte a sus servicios. En este caso, visite [https://status.overleaf.com](https://status.overleaf.com/) para obtener información actualizada.

Ahora, echemos un vistazo más de cerca a cómo funciona Overleaf.

#### Creación de nuestro primer documento en línea

Queremos crear nuestro propio espacio en Overleaf en dos pasos. Luego, iniciaremos nuestro primer proyecto de LaTeX:

1. **Registrarse en el servicio**: Haga clic en *Register* en la página principal de Overleaf o vaya a [https://www.overleaf.com/register](https://www.overleaf.com/register). Ingrese su dirección de correo electrónico y elija una contraseña.
2. **Iniciar sesión en Overleaf**: Haga clic en *Login* en la página principal o vaya a [https://www.overleaf.com/login](https://www.overleaf.com/login):

> **Figura 1.10** – Creación de un nuevo proyecto

##### ¿Por qué necesitamos registrarnos?

Estar localizable a través de una dirección de correo electrónico es básicamente para cumplir con la ley de protección de datos. Si olvida su contraseña, puede pedirle a Overleaf que envíe un enlace de restablecimiento de contraseña a su dirección de correo electrónico. En general, al utilizar su dirección de correo electrónico, puede demostrar su identidad y la propiedad de sus datos si alguna vez lo necesita.

3. Haga clic en el botón **New Project**. Aparecerá una lista desplegable donde puede elegir tener un proyecto en blanco o uno basado en una plantilla, como una plantilla de libro, presentación, CV o tesis. Por ahora, simplemente elegimos **Blank Project**.
4. Overleaf le pide un nombre; elija uno. ¡Eso es todo! Esto es lo que tiene ahora:

> **Figura 1.11** – Un nuevo proyecto

No está completamente en blanco, ya que contiene una pequeña estructura de código, por lo que obtiene un inicio rápido y puede comenzar a completar su texto.

La vista previa en el lado derecho se actualizará cada vez que haga clic en el botón **Recompile** o presione `Ctrl + Enter`. Puede habilitar la composición tipográfica automática si abre el menú *Recompile* y elige **Auto Compile** en el menú desplegable, que está activado en la Figura 1.12.

El documento se actualiza frecuente y automáticamente mientras escribe:

> **Figura 1.12** – Configuración de compilación

Dado que Overleaf es tan diferente de los editores clásicos de LaTeX, echemos un vistazo más de cerca.

#### Explorando Overleaf

Para ver rápidamente un documento más complejo en acción y comprender qué puede esperar de Overleaf, abramos la plantilla *Masters/Doctoral Thesis* de [https://www.latextemplates.com/template/masters-doctoral-thesis](https://www.latextemplates.com/template/masters-doctoral-thesis). Una vez que esté allí, simplemente haga clic en el botón **Open in Overleaf**. Luego, Overleaf crea un proyecto para usted.

> **Figura 1.13** – Proyectos en el editor de Overleaf

En la Figura 1.13, en el extremo izquierdo, puede ver la estructura de carpetas y archivos. Junto a ella, estará el código fuente de LaTeX. En el extremo derecho, verá la salida en una vista previa en PDF, como en la Figura 1.11.

En su forma más básica, escribe su código a la izquierda, hace clic en el botón **Recompile** y ve el resultado a la derecha, como hicimos anteriormente en nuestro ejemplo.

Mientras trabaja, Overleaf realiza un seguimiento del historial. Puede etiquetar versiones para comprobarlas más adelante. Al hacer clic en el botón **History** en la parte superior se le muestran las versiones:

> **Figura 1.14** – Historial de documentos en Overleaf

Haga clic en una versión a la derecha para cambiar a ella.

Sin mirar demasiadas capturas de pantalla, esto es lo que puede hacer si hace clic en el botón **Menu** en la esquina superior izquierda:

- Permitir que Overleaf cuente las palabras de su documento, excluyendo la sintaxis del código, como comandos y entornos
- Sincronizar con Dropbox o GitHub
- Elegir el compilador (`pdfLaTeX`, `LaTeX` clásico, `XeLaTeX` o `LuaLaTeX`, para usuarios avanzados)
- Establecer una versión de TeX Live si desea compilar un archivo antiguo con una versión antigua de TeX Live o cambiar a una más nueva
- Seleccionar un documento principal `.tex` si su proyecto consta de varios documentos
- Elegir un tema de estilo visual de editor para el marcado de código y el fondo, cambiando colores entre claro, pastel, oscuro y otros
- Elegir la fuente del editor (como Consolas o Lucida) y el tamaño de la fuente
- (Des)activar la revisión ortográfica, el autocompletado, el cierre automático de corchetes y la verificación de código

El corrector ortográfico integrado de Overleaf marca los problemas con una línea ondulada. Simplemente haga clic derecho sobre ella para obtener sugerencias de reemplazo, como se muestra en la siguiente captura de pantalla:

> **Figura 1.15** – Corrección ortográfica en Overleaf

A propósito de la corrección ortográfica, hay más.

#### Retroalimentación gramatical y lingüística con Writefull

La extensión **Writefull** de Overleaf comprueba la gramática y proporciona sugerencias de redacción para su texto. Está diseñada para la redacción científica y está entrenada con millones de artículos de revistas de investigación. Puede corregir errores tipográficos, errores gramaticales, problemas de vocabulario, puntuación y más.

Veámosla en acción en nuestro ejemplo anterior de plantilla de tesis:

> **Figura 1.16** – Corrección gramatical con Writefull

Aunque el corrector ortográfico no se queja, la IA entrenada de la extensión Writefull muestra 129 posibles problemas y ofrece sugerencias para las palabras subrayadas en rojo:

- *though* puede ser reemplazado por *although*
- *doesn't* puede ser reemplazado por *does not*, en escritura formal
- Después de los encabezados (en la figura anterior), debe haber una coma de Oxford (*Oxford comma*), es decir, una coma antes de la palabra *and* al final de una lista.

Puede tomárselo con calma como lo hago en este libro, de manera no tan formal, pero su tesis o artículos de investigación y cualquier redacción científica pueden beneficiarse de estas sugerencias.

La extensión Writefull estaba disponible inicialmente para el navegador Chrome. Sin embargo, se anunció que en el futuro se admitirán otros navegadores web, como Firefox. La versión básica es gratuita y existe una versión prémium sobre la que puede leer en su sitio web.

En el momento de finalizar esta edición del libro, Writefull se ha integrado en el propio Overleaf. La información completa está disponible en [https://docs.overleaf.com/integrations-and-add-ons/ai-features/writefull](https://docs.overleaf.com/integrations-and-add-ons/ai-features/writefull).

#### Revisión y comentarios

Probablemente haya notado el texto resaltado en amarillo y los símbolos de bocadillos de diálogo en la captura de pantalla anterior. Al hacer clic en el botón **Review**, la barra de revisión se expande y se muestran los comentarios:

> **Figura 1.17** – Revisión y comentarios con Overleaf

Puede marcar fragmentos de texto, hacer clic en **Add comment**, escribir lo que piensa y también responder a los comentarios de otras personas. Eso ayuda tanto en su propia escritura como en la colaboración con colegas o un editor.

Esta y las características mencionadas anteriormente deberían proporcionar una buena perspectiva de los servicios actuales de LaTeX en la nube.

Todo el conjunto de ejemplos de código de la *Guía para principiantes de LaTeX* se puede abrir en Overleaf simultáneamente, con un solo clic. Visite [https://latexguide.org/code](https://latexguide.org/code) para obtener el paquete completo y tener su propio proyecto con todos los ejemplos del libro incluidos, listos para editar y compilar.

La siguiente sección le proporcionará una forma de acceder a documentación y referencias de soporte adicionales mientras trabaja con este libro.

---

### Acceso a la documentación

LaTeX ofrece cientos de clases y paquetes, muchos más de los que cualquier libro podría cubrir por completo. Afortunadamente, la mayoría de los paquetes proporcionan una documentación bien redactada a la que puede acceder y leer fácilmente. A medida que trabaje con este libro, encontrará muchos paquetes útiles. Si explora su documentación junto con los ejemplos de los capítulos, estará bien encaminado para convertirse en un usuario experto de LaTeX.

En los siguientes capítulos, aprenderá sobre muchos paquetes de LaTeX que brindan capacidades adicionales. Por lo tanto, veamos cómo acceder a la documentación de los paquetes.

Una vez que haya instalado LaTeX, puede abrir el manual de un paquete directamente en su computadora:

- **En una PC con Windows**: Abra el menú Inicio, seleccione la carpeta TeX Live y haga clic en **TeX Live command-line**. Alternativamente, inicie la aplicación `cmd` (Símbolo del sistema) de Windows.
- **En una Mac o cualquier computadora con Linux**: Abra la aplicación Terminal.

A continuación, escriba `texdoc nombre_del_paquete` y presione Enter. Por ejemplo, al escribir `texdoc geometry` se abre el manual en PDF para el paquete `geometry`.

Si no instaló LaTeX, puede obtener la documentación en línea. En su navegador, abra `https://texdoc.org/pkg/nombre_del_paquete`. Esa es solo una URL de plantilla, por lo que si desea el paquete `geometry`, debe escribir `https://texdoc.org/pkg/geometry`. Ese es un método sencillo para los usuarios de Overleaf que no tienen una documentación instalada localmente.

A lo largo de este libro, a menudo verá referencias a manuales o documentación de paquetes. Recuerde siempre que puede revisar la documentación utilizando el comando `texdoc` o visitando [https://texdoc.org](https://texdoc.org/), como se describió anteriormente.

Por último, hay una gran cantidad de documentación relacionada con LaTeX disponible en línea, incluidos tutoriales, guías y materiales de referencia. Analizaremos estos más a fondo en el [Capítulo 15](https://subscription.packtpub.com/book/business-other/9781805804574/15), *Uso de recursos en línea*.

---

### Resumen

En este capítulo, exploramos los beneficios clave de LaTeX; pronto será nuestro turno de utilizar sus virtudes para lograr resultados de alta calidad. Además, cubrimos la instalación, edición y uso de LaTeX, tanto localmente en su computadora como en línea en el navegador.

Ahora que tiene una configuración de LaTeX funcional y probada, está listo para escribir sus propios documentos LaTeX. En el siguiente capítulo, hablaremos sobre el formato del texto en detalle.
