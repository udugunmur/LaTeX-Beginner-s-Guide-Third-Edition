# LaTeX Beginner's Guide
## Capítulo 6: Inclusión de Imágenes

En el capítulo anterior, organizamos datos mediante tablas. Sin embargo, no toda la información cabe en filas y columnas; a veces, las imágenes la comunican mejor, como diagramas, ilustraciones, capturas de pantalla y fotografías. En este capítulo, aprenderemos cómo incluir imágenes como figuras, agregar leyendas y hacer referencia a ellas al igual que a las tablas. También examinaremos de cerca cómo controlar la ubicación de figuras flotantes, un concepto que también se aplica a las tablas.

Cubriremos los siguientes temas:

- Elección del formato de imagen adecuado
- Creación de imágenes
- Incrustación de imágenes
- Escalado de una imagen
- Inclusión de páginas completas
- Colocación de imágenes detrás del texto
- Gestión de figuras flotantes
- Organización de múltiples imágenes
- Permitir que el texto fluya alrededor de las imágenes

Al final de este capítulo, podrá controlar la ubicación de las imágenes dentro de su documento con confianza y precisión.

Comenzaremos examinando los formatos gráficos.

---

### Elección del formato de imagen adecuado

Echemos un vistazo rápido a los formatos de archivo de imagen compatibles: EPS, PDF, JPG y PNG. PS significa PostScript, mientras que EPS significa Encapsulated PostScript. Ya está familiarizado con PDF, que significa Portable Document Format. Los archivos PDF no tienen que ser páginas completas; también pueden ser imágenes pequeñas. Y conoce los formatos de imagen PNG y JPG, que se utilizan ampliamente para capturas de pantalla y fotos.

Si su imagen ya está en uno de estos cuatro formatos, puede incluirla directamente en su documento, ya que estos formatos son compatibles de forma predeterminada. Convertir entre formatos no mejorará la calidad. Sin embargo, cuando crea o exporta una imagen, aún puede elegir el formato de archivo más adecuado. He aquí cómo decidir.

EPS y PDF son formatos de gráficos vectoriales. Son escalables y mantienen una alta calidad incluso a alta resolución o cuando se amplían. Por lo tanto, siempre que sea posible, debe preferir PDF (o EPS), por ejemplo, al exportar dibujos o diagramas desde otro software de oficina. Los formatos vectoriales se utilizan normalmente para lograr la mejor calidad manteniendo tamaños de archivo pequeños.

PNG y JPG son formatos de mapa de bits, también conocidos como gráficos ráster, y se utilizan comúnmente para fotografías y capturas de pantalla. Cuando amplía imágenes de mapa de bits, pueden perder nitidez a medida que los píxeles individuales se hacen más visibles, lo que produce bordes pixelados o borrosos. Las imágenes PNG utilizan compresión sin pérdidas, mientras que las imágenes JPG pueden degradarse en calidad durante el guardado. Por lo tanto, si toma capturas de pantalla, es mejor usar PNG; o, si elige JPG, asegúrese de que no se aplique compresión con pérdidas: normalmente, puede elegir un nivel de calidad al guardar. Para las fotos, el formato JPG es una buena opción para mantener pequeño el tamaño del archivo PDF resultante porque su compresión funciona bien con imágenes naturales que tienen transiciones de color suaves. Rara vez notará una pérdida en la calidad de la foto, mientras que la misma compresión puede distorsionar fácilmente líneas nítidas en diagramas o capturas de pantalla.

Además de admitir gráficos vectoriales, tanto EPS como PDF también pueden contener imágenes de mapa de bits. También se les conoce como formatos contenedores en general porque pueden incrustar múltiples tipos de contenido dentro de un solo archivo, como imágenes, texto, fuentes y contenido multimedia. Aquí nos centramos en imágenes individuales.

Hay numerosas herramientas disponibles para convertir entre formatos gráficos. Los siguientes tres programas son populares, y tanto TeX Live como MiKTeX los incluyen:

- `dvips` convierte archivos DVI (`.dvi`) al formato PostScript (`.ps`)
- `ps2pdf` convierte archivos PostScript a PDF
- `epstopdf` convierte archivos EPS (`.eps`) a PDF

Estas son herramientas de línea de comandos. Algunos editores de LaTeX las integran para proporcionar compilación con un solo clic, por ejemplo, de `.tex` a `.dvi`, luego a `.ps` y luego a `.pdf`.

Desde 2011, `pdflatex` llama a `epstopdf` automáticamente cuando incluye imágenes EPS para convertirlas sobre la marcha.

---

### Creación de imágenes

Echemos un vistazo breve a algunas herramientas potentes, gratuitas y de código abierto para crear, procesar y convertir gráficos que puede incluir en sus documentos. Todas están disponibles para Windows, macOS y Linux. En Linux, consulte primero su tienda de aplicaciones o repositorio de software para ver si el programa está disponible para la versión específica de su sistema antes de descargarlo del sitio web oficial.

#### Producción y procesamiento de imágenes de mapa de bits

Las siguientes herramientas son especialmente recomendadas. Todas admiten muchos formatos estándar, incluidos PNG, JPG y GIF, y pueden exportar a PDF:

- **GIMP** ([https://www.gimp.org](https://www.gimp.org/)) es un editor de imágenes a menudo comparado con Adobe Photoshop. Es ideal para tareas de edición y retoque fotográfico. Puede usarlo para recortar, cambiar el tamaño, enfocar, ajustar colores o combinar varias imágenes. GIMP admite muchos formatos estándar, incluidos PNG, JPG e incluso los archivos PSD de Photoshop.
- **Pinta** ([https://www.pinta-project.com](https://www.pinta-project.com/)) es un editor de imágenes inspirado en Paint.NET, que también es gratuito pero solo está disponible para Windows. En comparación con GIMP, Pinta tiene menos funciones pero utiliza mucha menos memoria y espacio en disco. Su diseño más simple también hace que sea mucho más fácil de usar.
- **Krita** ([https://krita.org](https://krita.org/)) es un estudio de arte digital completo. Puede pintar con pinceles y capas realistas y usarlo en tabletas, lo que lo hace ideal para ilustraciones digitales.
- **MyPaint** ([https://www.mypaint.app](https://www.mypaint.app/)) es un programa de pintura ligero y rápido que es ideal para bocetos rápidos y dibujos con tableta.
- **ImageMagick** ([https://imagemagick.org](https://imagemagick.org/)) es una suite de software para crear, editar y convertir imágenes. A diferencia de los editores gráficos, se utiliza principalmente desde la línea de comandos o en scripts para automatizar el procesamiento de imágenes y tareas por lotes. Puede usarlo para recortar, cambiar el tamaño, rotar, ajustar colores o aplicar efectos a imágenes. Admite cientos de formatos de archivo, lo que lo hace especialmente útil para convertir entre ellos.

Estas herramientas cubren la mayoría de las necesidades para trabajar con imágenes de mapa de bits.

#### Edición de gráficos vectoriales

Las siguientes herramientas utilizan formas vectoriales, lo que mantiene sus gráficos nítidos en cualquier tamaño. Funcionan mejor con el formato SVG, pero también pueden exportar a formatos de mapa de bits cuando sea necesario. El flujo de trabajo recomendado es crear sus gráficos en SVG y exportarlos a PDF antes de agregarlos a su documento de LaTeX:

- **Inkscape** ([https://inkscape.org](https://inkscape.org/)) es un editor de gráficos vectoriales para crear material gráfico escalable, como diagramas, iconos, dibujos técnicos e ilustraciones. Proporciona herramientas para dibujar formas, trazados y texto, así como capas, degradados y opciones de alineación: características comparables a las que se encuentran en el software de diseño profesional.
- **SVG-edit** ([https://github.com/SVG-Edit/svgedit](https://github.com/SVG-Edit/svgedit)) es un editor SVG ligero basado en navegador con funciones básicas, ideal para ediciones rápidas sin instalación. Puede usarlo en [https://svgedit.netlify.app](https://svgedit.netlify.app/).
- **draw.io** ([https://drawio.com](https://drawio.com/)) es una herramienta basada en web para crear diagramas, diagramas de flujo y otros dibujos estructurados. Puede usarlo directamente en su navegador en [https://app.diagrams.net](https://app.diagrams.net/) o instalar la versión de escritorio, llamada draw.io Desktop, para uso sin conexión.

Incluso puede crear gráficos vectoriales directamente en LaTeX. Dado que este es un tema más avanzado, escribí un libro entero sobre ello: *LaTeX Graphics with TikZ*, publicado por Packt Publishing. Por ahora, nos centraremos en las imágenes creadas fuera de LaTeX, como fotos e ilustraciones.

---

### Incrustación de imágenes

Para incluir imágenes, el paquete estándar que se debe utilizar es `graphicx`. La `x` en el nombre indica que amplía el paquete `graphics` original (ahora obsoleto).

Repasemos un documento breve en el que insertamos una imagen entre dos párrafos. Siga estos pasos:

1. Comience un nuevo documento y cargue los paquetes `babel` y `blindtext` para imprimir algo de texto de relleno, de la siguiente manera:

```latex
\documentclass[a5paper]{article}
\usepackage[english]{babel}
\usepackage{blindtext}
\usepackage{graphicx}
\pagestyle{empty}
\begin{document}
\section{Including a picture}
\blindtext
```

2. Comience un entorno `figure` y use `\centering` para centrar la imagen:

```latex
\begin{figure}
\centering
```

3. Inserte la imagen utilizando el comando `\includegraphics` con el nombre del archivo como argumento. Usaremos `example-image` como nombre de archivo, ya que es una imagen de muestra incluida con TeX Live:

```latex
\includegraphics[width=4cm]{example-image}
```

4. Agregue una leyenda, finalice el entorno `figure` y finalice el documento con texto de relleno:

```latex
\caption{Test figure}
\end{figure}
\blindtext
\end{document}
```

5. Haga clic en **Typeset** para compilar el documento y verifique el resultado, como se muestra en la siguiente captura de pantalla:

> **Figura 6.1** – Una imagen en un documento

El comando clave aquí es `\includegraphics`, donde especificamos el nombre del archivo que se incluirá. LaTeX carga este archivo si existe; de lo contrario, mostrará un mensaje de error. LaTeX admite los siguientes tipos de archivos que mencionamos antes:

- PNG, JPG y PDF si compila directamente a PDF (usando `pdflatex`)
- EPS si compila a DVI y convierte a PS y PDF (LaTeX tradicional)

No necesita especificar una extensión de nombre de archivo, ya que LaTeX busca automáticamente extensiones compatibles. Si varios archivos comparten el mismo nombre pero tienen extensiones diferentes, `pdflatex` selecciona el primero que encuentra en este orden: `.pdf`, `.png`, `.jpg`, `.jpeg`.

Coloque el archivo en el mismo directorio que su documento o especifique una ruta completa o relativa, de la siguiente manera:

```latex
\includegraphics{appendix/figure1}
```

En las rutas de archivo, use caracteres de barra diagonal (`/`); no use caracteres de barra invertida (`\`), ya que este último inicia un comando de LaTeX.

Adelante, copie una imagen de su elección en el directorio de su documento. Proporcione a `\includegraphics` su nombre de archivo y compile. LaTeX incrusta la imagen con su tamaño original.

En las siguientes secciones, veremos cómo agregar una imagen de un tamaño específico, incluir una página PDF completa o colocarla en el fondo detrás del texto.

---

### Escalado de una imagen

Al insertar una imagen, puede elegir un tamaño diferente. El comando `\includegraphics` admite esto con una lista de opciones clave-valor, de la siguiente manera:

```latex
\includegraphics[key=value list]{file name}
```

La documentación del paquete `graphicx`, disponible en [http://texdoc.org/pkg/graphicx](http://texdoc.org/pkg/graphicx), enumera todas las claves y posibles valores. Estas son las más populares y lo que hacen:

- `width`: Ancho de la imagen, por ejemplo, `width=0.9\textwidth`
- `height`: Altura de la imagen, por ejemplo, `height=3cm`
- `scale`: Factor de escala, por ejemplo, `scale=0.5`
- `angle`: Ángulo de rotación, por ejemplo, `angle=90`

Hay opciones adicionales, como para recortar, pero puede realizar fácilmente dicho procesamiento con cualquier software gráfico antes de incluirlo.

En lugar de girar una figura 90 grados, también podría utilizar el entorno `sidewaysfigure` del paquete `rotating` (consulte [https://texdoc.org/pkg/rotating](https://texdoc.org/pkg/rotating)).

---

### Inclusión de páginas completas

¿Qué sucede si queremos incluir imágenes que son más anchas o más altas que el área de texto? Si bien el comando `\includegraphics` puede manejar esto, LaTeX puede quejarse sobre el ancho o el tamaño e incluso podría moverlas a la página siguiente si no hay suficiente espacio.

Utilizando el paquete `pdfpages`, podemos insertar imágenes grandes e incluso páginas completas. El paquete `pdfpages` proporciona el comando `\includepdf`, que puede incrustar una sola página, una página parcial o un documento PDF de varias páginas completo a la vez. A pesar de su nombre, también puede incluir archivos PNG y JPG, no solo archivos PDF.

Un ejemplo de su uso básico podría verse así:

```latex
\usepackage{pdfpages}
…
\includepdf[pages=-]{contract}% include entire contract.pdf
\includepdf[pages=2-4]{spec}% include pages 2-4 of spec.pdf
```

Un uso común es combinar varios archivos PDF en un solo archivo PDF. También podemos utilizar el paquete `pdfpages` para cambiar el tamaño de varias páginas PDF y organizarlas en una sola hoja. Para obtener más detalles, eche un vistazo a la documentación en [https://texdoc.org/pkg/pdfpages](https://texdoc.org/pkg/pdfpages).

---

### Colocación de imágenes detrás del texto

¿Necesita marcas de agua? ¿Imágenes de fondo? ¿Cuadros de texto colocados en posiciones arbitrarias en la página? ¿Y todo esto sin interferir con otro texto? El paquete `eso-pic` hace esto por usted.

En *LaTeX Cookbook*, puede leer un ejemplo paso a paso de cómo hacer esto en la sección *Posicionamiento absoluto de texto* en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Ajuste del texto*.

El paquete `textpos` ofrece otro enfoque. Está desarrollado para colocar cajas con texto o gráficos en posiciones absolutas en una página; consulte [https://texdoc.org/pkg/textpos](https://texdoc.org/pkg/textpos).

Con una instalación moderna de LaTeX, puede utilizar un *hook* (gancho). Ese es un lugar en el código donde se puede insertar otro código para que se ejecute en ese momento, como una devolución de llamada o un punto de inserción. En resumen, esto es como `\AddToHook{shipout/background}{<sus comandos de imagen>}`.

Ahora, echaremos un vistazo al posicionamiento dinámico de imágenes.

---

### Gestión de figuras flotantes

Cuando ocurre un salto de página, LaTeX puede dividir el texto normal y continuar en la página siguiente. Sin embargo, no puede dividir una imagen entre páginas. Por eso LaTeX hizo que el entorno `figure` que usamos en nuestro primer ejemplo fuera un entorno flotante. Estos entornos flotantes también se denominan *floats* en resumen. LaTeX puede empujar su contenido, incluidas sus leyendas, a un lugar que funcione bien con el diseño de página y los saltos de página.

Veamos cómo abordar esto.

El entorno `figure` toma un argumento opcional que sugiere la ubicación final de la figura. Probaremos el efecto en nuestro ejemplo anterior, como se muestra aquí:

1. Regrese al ejemplo anterior de la Figura 6.1. Esta vez, agregue las opciones `h` y `t` en la línea resaltada (donde `h` y `t` representan *here* [aquí] y *top* [arriba]), de la siguiente manera:

```latex
\begin{figure}[ht]
\centering
\includegraphics{example-image}[width=4cm]
\caption{Test figure}
\end{figure}
```

2. Compile el documento y eche un vistazo al resultado. Debería verse así:

> **Figura 6.2** – Una imagen dentro del texto

3. Cambie las opciones en la línea resaltada a `!b` (donde `b` significa *bottom* [abajo]), de la siguiente manera:

```latex
\begin{figure}[!b]
```

4. Compile de nuevo. La figura ahora se ve forzada a flotar hacia la parte inferior, y ahora vemos esta página:

> **Figura 6.3** – Una imagen en la parte inferior de la página

Al agregar algunos caracteres que representan opciones de ubicación, podríamos obligar a que la figura aparezca donde queramos.

Existe una forma con asterisco, a saber, `figure*`, en un diseño de dos columnas que coloca una figura en una sola columna. En el modo de una columna, no hay diferencia con la forma sin asterisco.

Veamos ahora más de cerca el posicionamiento de figuras. Veremos cómo podemos establecer preferencias sobre dónde aparecen las figuras, como en la parte superior o inferior de la página, forzar la salida inmediata o al menos limitar la flotación, y organizar imágenes una al lado de la otra o dentro del flujo de texto.

#### Comprensión de las opciones de ubicación

El argumento opcional del entorno `figure` especifica dónde puede colocar LaTeX la figura. Cuatro letras representan cuatro lugares posibles, como se describe aquí:

- `h` significa *here* (aquí). La figura puede aparecer justo donde la escribimos en el código fuente.
- `t` significa *top* (arriba). Permite colocar la figura en la parte superior de una página.
- `b` significa *bottom* (abajo). Permite que la figura aparezca en la parte inferior de una página.
- `p` significa *page* (página). La figura se puede colocar en una página separada, donde solo pueden residir elementos flotantes, pero no texto normal.

Una quinta opción puede resultar útil:

- `!` anula los valores predeterminados de LaTeX; le indica a LaTeX que relaje algunas restricciones internas, aumentando la posibilidad de colocar el elemento flotante antes.

Si no especifica ninguna opción, LaTeX podría colocar la figura muy lejos, lo que puede resultar sorprendente para los nuevos usuarios de LaTeX. Especificar más opciones ayuda a mantenerla lo más cerca posible. La opción más flexible es utilizar la ubicación `[!htbp]`, que permite que la figura vaya prácticamente a cualquier lugar. Aún puede considerar eliminar un especificador de ubicación si no le gusta el resultado.

#### Forzar la salida de figuras

LaTeX retiene figuras y tablas hasta que encajan en el diseño de página sin violar las reglas tipográficas de LaTeX. Si desea obligar a LaTeX a imprimirlas, hay un comando para hacerlo: el comando `\clearpage` finaliza la página actual y genera todas las figuras y tablas en cola. También puede usar `\cleardoublepage`, que hace lo mismo pero en un diseño a dos caras. Asegura que la siguiente página que no sea de flotantes sea una página de la derecha. Si es necesario, inserta una página en blanco.

Finalizar una página inmediatamente, sin embargo, podría no ser el mejor enfoque, ya que podría dejar mucho espacio vacío en la página actual. El paquete `afterpage` ofrece una solución elegante. Este paquete puede retrasar la ejecución de `\clearpage` hasta que la página actual haya terminado, como se muestra:

```latex
\usepackage{afterpage}
...
body text
\afterpage{\clearpage}
```

Es posible que no necesitemos usar el paquete `afterpage` con frecuencia, ya que simplemente podemos ejecutar un comando `\clearpage` en la ubicación deseada, como al final de una sección. Podemos automatizar ese caso. Veamos esto en la siguiente sección.

#### Limitación de la flotación

Como se dijo anteriormente, una figura puede flotar muy lejos, posiblemente incluso hacia la siguiente sección. El paquete `placeins` ayuda a restringir la flotación. Si carga `placeins` con `\usepackage{placeins}` y escribe `\FloatBarrier` en algún lugar de su documento, ninguna figura puede flotar más allá de ese punto. Esta macro garantiza que los flotantes permanezcan más cerca de su lugar original.

Una forma muy conveniente de evitar que los flotantes crucen los límites de las secciones es indicando la opción `section`, de la siguiente manera:

```latex
\usepackage[section]{placeins}
```

Esta opción inserta una `\FloatBarrier` implícita al comienzo de cada sección. Dos opciones adicionales, a saber, `above` y `below`, le permiten reducir las restricciones, evitando que los flotantes aparezcan por encima del inicio de la sección actual o por debajo del comienzo de la siguiente sección.

Las figuras no pasan al siguiente capítulo porque el comando `\chapter` incluye un `\clearpage` implícito.

#### Evitar la flotación por completo

¿Desea que una imagen aparezca exactamente donde la colocó en el código? La respuesta obvia es: en ese caso, no utilice un entorno de figura flotante. Puede usar `\includegraphics` sin un entorno `figure`. Por ejemplo, podría incluir y centrar una imagen haciendo lo siguiente:

```latex
\begin{center}
\includegraphics[width=4cm]{example-image}
\end{center}
```

Sin embargo, las leyendas están diseñadas para entornos flotantes, por lo que un comando `\caption` no funcionará aquí. Si aún desea tener una leyenda, puede usar el comando `\captionof`. El paquete `caption`, las clases `KOMA-Script`, introducidas en el [Capítulo 3](https://subscription.packtpub.com/book/business-and-other/9781805804574/3), *Diseño de páginas*, y el pequeño paquete `capt-of` proporcionan ese comando, que puede usar de la siguiente manera:

```latex
\usepackage{capt-of}% or caption
…
\begin{minipage}{\linewidth}
\centering
\includegraphics{example-image}
\captionof{figure}{Test figure}
\end{minipage}
```

El entorno `minipage` mantiene una imagen y su leyenda juntas porque no puede ocurrir ningún salto de página en un entorno `minipage`. La definición de `\captionof` es la misma que la de `\caption`, excepto que hay un argumento adicional que especifica el tipo de flotante; en este caso, `figure`, como se ilustra en el siguiente fragmento de código:

```latex
\captionof{figure}[short text]{long text}
```

Tenga en cuenta que la numeración podría volverse inconsistente si mezcla flotantes reales y figuras fijas. Al renunciar a las capacidades de posicionamiento de LaTeX, debe asegurarse de que las páginas sigan estando adecuadamente llenas.

El paquete `float` proporciona un enfoque conveniente y de apariencia uniforme para esto. Introduce la opción de ubicación `H`, lo que hace que el elemento flotante aparezca justo allí, como se ilustra en el siguiente fragmento de código:

```latex
\usepackage{float}
…
\begin{figure}[H]
\centering
\includegraphics{example-image}
\caption{Test figure}
\end{figure}
```

Elija el método que mejor se adapte a sus necesidades. Cuando comencé con LaTeX, solía pensar "no use un entorno flotante cuando no quiera que flote" y prefería usar `minipage` en su lugar. Hoy en día, recomiendo un entorno `figure` con la opción `H` para una sintaxis consistente, y `H` es fácil de cambiar más adelante por otras opciones.

Para obtener información más detallada sobre la ubicación de flotantes, consulte https://latex.net/floats, que recopila explicaciones en varios idiomas.

---

### Organización de múltiples imágenes

Para agrupar varias subfiguras con leyendas individuales dentro de una sola figura, LaTeX ofrece varios paquetes de soporte entre los que puede elegir, descritos de la siguiente manera:

- `subcaption` es un paquete para subfiguras con sub-leyendas individuales y pertenece al paquete `caption`. Si utiliza hipervínculos en un documento, esta es la opción recomendada, ya que es la que mejor admite hipervínculos. Para hipervínculos, consulte también el [Capítulo 12](https://subscription.packtpub.com/book/business-and-other/9781805804574/12), *Uso de hipervínculos y diseño de encabezados*.
- `subfig` es un paquete sofisticado que admite la inclusión de figuras pequeñas. Maneja el posicionamiento, el etiquetado y las leyendas dentro de un solo flotante.
- `subfigure` todavía está disponible para este propósito y lo encontrará en línea, pero ya no se mantiene y puede considerarlo obsoleto desde que apareció `subfig`.

No cargue dos de estos paquetes juntos. En general, cargar dos paquetes que sirven para el mismo propósito puede generar conflictos.

Para alinear imágenes, apilar imágenes o posicionarlas en una cuadrícula, se proporcionan y explican ejemplos en *LaTeX Cookbook*, [Capítulo 5](https://subscription.packtpub.com/book/business-and-other/9781805804574/5), *Trabajar con imágenes*.

---

### Permitir que el texto fluya alrededor de las imágenes

Si desea agregar un diseño interactivo o visualmente atractivo, puede dejar que el texto fluya alrededor de una imagen o figura. Podemos lograr esto usando el paquete `wrapfig` y su entorno `wrapfigure`.

Modifiquemos nuestro ejemplo anterior que incrustó una imagen (consulte la Figura 6.3). Nos gustaría que la imagen apareciera en el lado izquierdo, acompañada por el texto del cuerpo en el lado derecho, con la ayuda de los siguientes pasos:

1. En nuestro código de ejemplo para la Figura 6.3, cargue adicionalmente el paquete `wrapfig`, de la siguiente manera:

```latex
\documentclass[a5paper]{article}
\usepackage[english]{babel}
\usepackage{blindtext}
\usepackage{graphicx}
\usepackage{wrapfig}
\pagestyle{empty}
\begin{document}
```

2. Comience una sección sin numerar y coloque un entorno `wrapfig` dentro de un texto de relleno, de esta manera:

```latex
\section*{Text flowing around an image}
\blindtext
\begin{wrapfigure}{l}{4cm}
\includegraphics[width=4cm]{example-image}
\caption{Test figure}
\end{wrapfigure}
\blindtext
\end{document}
```

3. Compile el documento y eche un vistazo. Debería ver el siguiente resultado:

> **Figura 6.4** – Texto que fluye alrededor de una imagen

Las opciones del entorno `wrapfigure` difieren del entorno `figure`. Usamos solo dos de ellas. Si necesita más, aquí está la definición completa:

```latex
\begin{wrapfigure}[number of lines]{placement}[overhang]{width}
```

El primer argumento opcional indica el número de líneas de texto envueltas. Si se omite, esto se calculará automáticamente a partir de la altura. El segundo argumento, `placement`, puede ser uno de los caracteres `r`, `l`, `i` u `o` para el lado derecho, izquierdo, interior o exterior, o las letras mayúsculas correspondientes `R`, `L`, `I` u `O`, con el mismo significado, pero permitiendo que la figura flote. Solo se permite un carácter para especificar la opción. El otro argumento opcional, `overhang`, puede establecer un ancho por el cual la figura debe sobresalir en el margen; el valor predeterminado es 0 pt. El argumento final, y obligatorio, proporciona el ancho de la figura.

Puede leer más en el manual en [https://texdoc.org/pkg/wrapfig](https://texdoc.org/pkg/wrapfig).

---

### Resumen

En este capítulo, cubrimos cómo incluir imágenes en nuestros documentos de LaTeX. Aprendió qué formatos de imagen son compatibles y cómo controlar el posicionamiento de las figuras.

LaTeX puede generar automáticamente una lista de figuras, similar a una tabla de contenidos. Trataremos dichas listas en el [Capítulo 7](https://subscription.packtpub.com/book/business-and-other/9781805804574/7), *Uso de referencias cruzadas*.

Dado que las figuras se numeran automáticamente, puede hacer referencias cruzadas a ellas dentro de su texto. En el próximo capítulo, aprenderá cómo hacerlo utilizando las funciones de referencia integradas de LaTeX.
