# LaTeX Beginner's Guide
## Capítulo 11: Desarrollo de Documentos Grandes

El primer capítulo de este libro mencionó que LaTeX puede manejar documentos grandes con facilidad. Una vez que comience a crear documentos más grandes, verá que LaTeX continúa funcionando de manera confiable sin importar cuán grande se vuelva el documento. Para la computadora, la estructura del código fuente no importa, pero para usted, como autor, es importante mantener las cosas organizadas. Los documentos largos pueden abarcar cientos de páginas con miles de líneas, por lo que una estructura manejable es esencial.

Al final de este capítulo, podrá configurar un proyecto de documento grande con múltiples archivos, una portada y páginas preliminares (*front matter*) y finales (*back matter*) numeradas por separado.

En este capítulo, veremos los siguientes temas:

- División de la entrada
- Creación de páginas preliminares y finales
- Diseño de una portada
- Trabajo con plantillas
- Organización de archivos y carpetas

Es un gran paso hacia la redacción de una tesis, un libro o un informe exhaustivo.

Comencemos construyendo un documento a partir de varios archivos.

---

### División de la entrada

Para mantener manejable un documento grande, podemos dividirlo en varios archivos más pequeños. Esto nos permite trabajar en los capítulos por separado manteniendo una estructura general limpia.

Separaremos el preámbulo del texto del cuerpo y colocaremos cada capítulo en su propio archivo. Como proyecto de ejemplo, crearemos un documento de varios capítulos sobre ecuaciones y sistemas de ecuaciones, similar en estilo a una tesis o un libro. Podemos reutilizar material del ejemplo del [Capítulo 9](https://subscription.packtpub.com/book/business-and-other/9781805804574/9), *Escritura de fórmulas matemáticas*, donde trabajamos con teoremas sobre ecuaciones.

Crearemos varios archivos, paso a paso:

1. Comience un nuevo archivo y recopile todas las cargas de paquetes y sus opciones, como hicimos en nuestros preámbulos en los capítulos anteriores. Pueden ser muchos paquetes sobre los que ya hemos aprendido, como esto:

```latex
\usepackage[english]{babel}
\usepackage[T1]{fontenc}
\usepackage{lmodern}
\usepackage{microtype}
\usepackage{natbib}
\usepackage{tocbibind}
\usepackage{amsmath}
\usepackage{amsthm}
\newtheorem{thm}{Theorem}[chapter]
\newtheorem{lem}[thm]{Lemma}
\theoremstyle{definition}
\newtheorem{dfn}[thm]{Definition}
```

Guarde este archivo como `preamble.tex`.

2. Comience otro documento nuevo y copie el contenido del capítulo de Ecuaciones del ejemplo de teoremas de la sección *Escritura de teoremas y definiciones* del [Capítulo 9](https://subscription.packtpub.com/book/business-and-other/9781805804574/9), *Escritura de fórmulas matemáticas*:

```latex
\chapter{Equations}
\section{Quadratic equations}
\begin{dfn}
A quadratic equation is an equation of the form
\begin{equation}
  \label{quad}
  ax^2 + bx + c = 0
\end{equation}
where \( a, b \) and \( c \) are constants and \( a \neq 0 \).
\end{dfn}
```

Guarde este documento como `chapter1.tex`.

3. Cree otro documento para el siguiente capítulo y escriba el título del capítulo y algo más de texto, incluidas algunas secciones. Guárdelo como `chapter2.tex`:

```latex
\chapter{Equation Systems}
\section{Linear Systems}
...
\section{Non-linear Systems}
...
```

4. Ahora, cree el documento de nivel superior, `equations.tex`. Este comienza con el comando `\documentclass` y enumera el preámbulo y los capítulos para su inclusión:

```latex
\documentclass{book}
\input{preamble}
\begin{document}
\tableofcontents
\include{chapter1}
\include{chapter2}
\end{document}
```

5. Compile el documento dos veces. Recuerde que esta acción es necesaria para obtener finalmente la tabla de contenidos. Verifique el contenido para ver si todo está en su lugar correcto:

> **Figura 11.1** – Tabla de contenidos

Construimos un documento de nivel superior llamado `equations.tex`. Puede elegir un nombre significativo, ya que el nombre del archivo determina el nombre del PDF resultante.

Este archivo `.tex` sirve como marco para nuestro proyecto. Es un documento normal de LaTeX, pero lo redujimos tanto como fue posible y usamos dos comandos para importar archivos `.tex` externos:

- El comando `\input` inserta otro archivo, exactamente como si lo hubiéramos escrito directamente
- El comando `\include` también lee un archivo externo, pero inserta automáticamente `\clearpage` antes de él

Comparemos estos comandos en detalle.

#### Inclusión de pequeños fragmentos de código

La forma más sencilla de leer otro archivo en su documento es con este comando:

```latex
\input{filename}
```

Cuando LaTeX encuentra este comando, lee el contenido del archivo llamado `filename`, exactamente como si hubiera sido escrito directamente allí. El compilador de LaTeX procesa todos los comandos en este archivo.

Si no se proporciona ninguna extensión de nombre de archivo, LaTeX asume la extensión `.tex` e inserta `filename.tex`. También puede especificar una ruta, ya sea relativa o absoluta. Dado que una barra invertida inicia un comando, use barras diagonales (`/`) en lugar de barras invertidas (`\`) en los nombres de ruta. Por ejemplo, use `\input{chapters/ch01.tex}` en lugar de `\input{chapters\ch01.tex}`.

El uso de rutas relativas facilita mover o copiar un proyecto. Evite caracteres especiales y espacios en nombres de archivos y rutas; limítese a letras, números, `-` y `_`.

Use `\input` para colocar su preámbulo en un archivo separado. Mantiene ordenado su documento principal y puede copiar y adaptar fácilmente un preámbulo separado para sus otros proyectos.

Sin embargo, dividir un documento con `\input` no siempre es suficiente para gestionar proyectos grandes. Podría comentar líneas individuales de `\input` para compilar solo partes de un documento grande, especialmente cuando la compilación completa lleva tiempo. Pero hacerlo alteraría la numeración de páginas, la numeración de secciones y las referencias cruzadas. El comando `\include` está diseñado para manejar estos problemas, así que veámoslo más de cerca a continuación.

#### Inclusión de partes más grandes de un documento

Para incorporar secciones más grandes de un documento, como capítulos enteros, el siguiente comando es más adecuado:

```latex
\include{filename}
```

El argumento se maneja de manera similar a `\input`, pero existen diferencias clave:

- `\include` inicia implícitamente una nueva página. De forma simplificada, `\include{filename}` se comporta así:

```latex
\clearpage
\input{filename}
\clearpage
```

Esto hace que `\include` sea útil para rangos de páginas como capítulos o secciones. Una consecuencia es que solo puede usar `\include` después de `\begin{document}`.
- `\include` no se puede anidar. Aún puede usar `\input` en documentos incluidos, aunque agregar demasiadas capas puede hacer que la estructura sea más difícil de administrar.
- Lo más importante es que `\include` admite un mecanismo para elegir qué partes del documento desea compilar, que se especifica mediante otro comando, a saber, `\includeonly`.

Veamos cómo funciona `\includeonly`.

#### Compilación de partes de un documento

Dicho documento parcial, destinado a `\input` o `\include`, no se puede compilar por sí solo; necesita un documento raíz que especifique la clase de documento.

Sin embargo, una vez que intercambie partes del documento usando `\include` mientras compila su documento raíz, puede elegir qué secciones o capítulos se incluyen con este comando:

```latex
\includeonly{file list}
```

El comando `\includeonly` debe aparecer en el preámbulo, es decir, antes de `\begin{document}`.

El argumento puede ser un solo nombre de archivo o una lista de nombres de archivo separados por comas. Si no se especifica un archivo llamado `name.tex` en este argumento, `\include{name}` no insertará el archivo; actuará igual que un comando `\clearpage`. Esto permite la exclusión de bloques o capítulos enteros de la compilación. Si trabaja en un documento grande, esto acelera la compilación cuando incluye solo su capítulo actual, manteniendo intactas las etiquetas y referencias.

Al igual que con el archivo `main.tex`, LaTeX escribe un archivo `.aux` para cada archivo `.tex` incluido y los lee todos durante la compilación, ya que contienen información como números de capítulo y de página. Siempre que cada archivo incluido se haya compilado al menos una vez, las referencias cruzadas y la numeración de páginas, capítulos, secciones, etc., seguirán siendo correctas, incluso cuando excluya temporalmente algunos capítulos.

Pruébelo agregando lo siguiente:

```latex
\includeonly{chapter2}
```

Agréguelo a su preámbulo en `equations.tex` y compile. El resultado será solo el segundo capítulo, manteniendo la numeración correcta. Eche un vistazo a la salida aquí con Acrobat Reader:

> **Figura 11.2** – Nuestro documento con solo el Capítulo 2

En la parte superior de la Figura 11.2, puede ver 3/3 páginas en lugar de 5 páginas en el primer ejemplo del capítulo actual. En el lateral, verá tres páginas en miniatura, y la tercera es nuestro Capítulo 2. Esto nos muestra que el Capítulo 1, *Ecuaciones*, no está incluido aquí, sino solo el Capítulo 2, como deseábamos. Además, los números de página siguen siendo los mismos que en el documento completo, y los números originales de capítulo y sección no se modifican.

El tiempo de compilación es significativamente más corto si trabaja en un documento enorme con muchos capítulos y utiliza `\includeonly` para incluir solo el capítulo en el que está trabajando.

Finalmente, comente el comando `\includeonly` para componer su documento completo cuando termine su trabajo.

Por supuesto, puede utilizar `\include` sin `\includeonly` simplemente para dividir un documento grande en archivos.

Volvamos ahora a la estructura de un documento más grande.

---

### Creación de páginas preliminares y finales

Los libros suelen comenzar con material introductorio, como información sobre derechos de autor, un prólogo, agradecimientos o una dedicatoria. Similar para una tesis. Esta parte, incluida la portada y la tabla de contenidos, se llama páginas preliminares (*front matter*). Una tesis puede seguir la misma estructura.

Al final, un libro o tesis puede incluir un epílogo y material complementario, como una bibliografía y un índice. Esta parte se llama páginas finales (*back matter*).

La clase `book` y otras clases similares, como `scrbook` y `memoir`, admiten esta división en secciones directamente. También admiten diferentes estilos de numeración para páginas y capítulos. Veamos cómo funciona.

En nuestro ejemplo, el libro comienza con una dedicatoria. Las páginas preliminares incluirán la tabla de contenidos, la lista de tablas y figuras y una dedicatoria. Todas las páginas de las páginas preliminares estarán numeradas con números romanos. Al final, agregamos un apéndice con demostraciones complementarias que nos gustaría mantener separadas de los capítulos principales:

1. Cree un archivo llamado `dedication.tex`:

```latex
\chapter{Dedication}
This book is dedicated to one of the greatest mathematicians of all time: Carl Friedrich Gauss. Without him, this book wouldn't have been possible.
```

2. Cree un archivo llamado `proofs.tex`:

```latex
\chapter{Proofs}
...
```

3. Amplíe el archivo principal, `equations.tex`, mediante las líneas resaltadas:

```latex
\documentclass{book}
\input{preamble}
\begin{document}
\frontmatter
\include{dedication}
\tableofcontents
\listoftables
\listoffigures
\mainmatter
\include{chapter1}
\include{chapter2}
\backmatter
\include{proofs}
\nocite{*}
\bibliographystyle{plainnat}
\bibliography{example}
\end{document}
```

Como puede ver en la última línea resaltada, reutilizamos el archivo `example.bib` del [Capítulo 8](https://subscription.packtpub.com/book/business-and-other/9781805804574/8), *Gestión de contenidos, índices y bibliografía*. Compile, ejecute BibTeX y vuelva a compilar. Compruebe la numeración dentro de la tabla de contenidos:

> **Figura 11.3** – Tabla de contenidos de un documento complejo

Vimos que LaTeX imprimió el número de página de la página de contenidos en números romanos. Esto se aplica a todas las páginas de las páginas preliminares. Además, todos los capítulos de las páginas preliminares y finales no están numerados, a pesar de que no utilizamos el comando con asterisco, `\chapter*`.

Este comportamiento está controlado por tres comandos, a saber, `\frontmatter`, `\mainmatter` y `\backmatter`. Cada uno inicia una nueva página y ajusta tanto la numeración de páginas como la de capítulos de la siguiente manera:

- `\frontmatter`: Las páginas se numeran con números romanos en minúsculas. Los capítulos generan una entrada en la tabla de contenidos, pero no reciben un número.
- `\mainmatter`: Los números de página cambian a números arábigos. Los capítulos se numeran y producen entradas en la tabla de contenidos.
- `\backmatter`: Las páginas continúan con números arábigos. Los capítulos aparecen nuevamente en la entrada de la tabla de contenidos pero no están numerados.

Al igual que la clase `book`, las clases `scrbook` y `memoir` proporcionan los mismos comandos con un comportamiento muy similar.

Un documento grande suele comenzar con una portada, así que veamos cómo crear una en LaTeX.

---

### Diseño de una portada

Puede crear una portada atractiva rápidamente utilizando el comando `\maketitle`, como hicimos en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*. La mayoría de las clases de documentos ofrecen este comando para generar una portada razonable y preformateada. Si desea un control completo sobre el diseño, puede utilizar un entorno `titlepage` en su lugar. Por lo tanto, diseñemos una bonita portada para nuestro libro de ecuaciones.

En el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), ya utilizamos algunos comandos de formato, como `\centering`, y comandos de tamaño y forma de fuente, como `\Huge` y `\bfseries`, para dar formato a un título. Lo haremos de manera similar dentro de un entorno `titlepage`:

1. Cree un archivo, `title.tex`, con el siguiente contenido:

```latex
\begin{titlepage}
\raggedleft
{\Large The Author\\[1in]}
{\large The Big Book of\\}
{\Huge\scshape Equations\\[.2in]}
{\large Packed with hundreds of examples and solutions\\}
\vfill
{\itshape 2011, Publishing company}
\end{titlepage}
```

2. Agregue esta línea justo después de `\frontmatter`:

```latex
\include{title}
```

3. Nuestro libro final estará en formato A5, y también la portada. Por lo tanto, agreguemos eso al preámbulo:

```latex
\usepackage[a5paper]{geometry}
```

4. Compile; ahora tenemos una portada:

> **Figura 11.4** – Una portada

El entorno `titlepage` coloca su contenido en una página separada. Aunque esta portada se numerará como cualquier otra página, el número de página no se imprimirá en esa página.

En este entorno, utilizamos comandos de fuentes básicos de LaTeX para modificar el tamaño y el estilo de la fuente. Al agrupar con llaves, limitamos el alcance de esos comandos. En corchetes después de saltos de línea como `\\[.2in]`, agregamos un poco de espacio vertical adicional antes de la siguiente línea. El comando `\vfill` inserta un espacio vertical flexible que se estira tanto como sea posible para llenar toda la página. De esta manera, empujamos la última línea hacia la parte inferior de la página.

Tenga en cuenta que esta página tiene las mismas dimensiones de página que las otras páginas del documento. Eso significa que, en un libro a doble cara, es una página de la derecha. Por lo tanto, puede notar los márgenes izquierdo y derecho desiguales, lo que podría parecer indeseable, especialmente si su título está en el centro. Sin embargo, la explicación es simple: esta portada está pensada para ser un título interior (*inner title*), no la portada exterior (*cover page*). La página de título interior es, por supuesto, una página de la derecha.

Una portada exterior (*cover page*) es diferente. Dicha página debe ser de una sola cara y, por lo tanto, debe tener márgenes izquierdo y derecho iguales. Una portada exterior a menudo se produce como un documento independiente y se imprime por separado. Para un documento electrónico, puede utilizar el paquete `pdfpages`. Consulte la sección *Inclusión de páginas enteras* en el [Capítulo 6](https://subscription.packtpub.com/book/business-and-other/9781805804574/6), *Inclusión de imágenes*, o la sección *Combinación de archivos PDF* en el [Capítulo 9](https://subscription.packtpub.com/book/business-and-other/9781805804574/9), *Optimización de archivos PDF*, en *LaTeX Cookbook*, y en [https://texdoc.org/pkg/pdfpages](https://texdoc.org/pkg/pdfpages).

El paquete `titling` ofrece funciones para crear portadas sofisticadas. Para obtener algunas ideas sobre cómo se pueden diseñar portadas, puede consultar *Some Examples of Title Pages*, de Peter Wilson, disponible desde `texdoc titlepages` y en [https://texdoc.org/pkg/titlepages](https://texdoc.org/pkg/titlepages).

Un marco de documento que consta de archivos, encabezados, una portada y configuraciones de estilo se denomina plantilla (*template*). Aprenderemos a utilizar plantillas en la siguiente sección.

---

### Trabajo con plantillas

Al crear un documento, especificamos la clase de documento, elegimos los paquetes y opciones apropiados y establecemos una estructura para el contenido. Repetir estos pasos para cada documento nuevo se vuelve tedioso rápidamente.

Si planea producir varios documentos del mismo tipo, puede crear una plantilla. Este podría ser un archivo `.tex` que contenga lo siguiente:

- Una declaración de una clase de documento adecuada junto con opciones significativas
- Paquetes utilizados habitualmente que son más adecuados para su tipo de documento
- Un diseño predefinido para el encabezado, el pie de página y el texto principal
- Macros de creación propia para agilizar su trabajo
- Un marco de comandos de sección, donde completa los títulos y el texto del cuerpo
- Un marco que contiene comandos `\include` o `\input`, para los cuales puede crear los fragmentos de texto del cuerpo más adelante

A medida que crezcan sus habilidades en LaTeX, sus plantillas evolucionarán y se volverán mejores y más sofisticadas. Muchos usuarios publican sus elaboradas plantillas en línea. Muchas universidades, institutos, revistas y editoriales hacen lo mismo, ofreciendo plantillas oficiales para documentos como tesis, artículos, artículos de revistas y libros que coinciden con sus requisitos de formato.

Puede encontrar una colección cuidadosamente seleccionada de plantillas, organizadas por tipos de documentos como tesis, informes, cartas y presentaciones, junto con resultados de muestra, en una galería de plantillas en [https://latextemplates.com](https://latextemplates.com/).

Puede descargar una plantilla y comenzar a completar su texto. Alternativamente, puede comenzar un documento con una plantilla predefinida ofrecida por su editor. Probemos eso primero.

Los editores de LaTeX a menudo proporcionan plantillas para comenzar. TeXworks también ofrece algunas. Así que probaremos esta característica. Tomemos una, abrámosla, modifiquémosla y compilémosla:

1. En el menú principal de TeXworks, haga clic en **File** (Archivo), luego en **New from template** (Nuevo a partir de plantilla). Se abrirá una ventana que le permitirá elegir una plantilla:

> **Figura 11.5** – Selección de plantilla de TeXworks

2. En la parte inferior de la ventana, puede leer el código fuente de la plantilla. He aquí un ejemplo de KOMA-Script (`KOMA-letter.tex`):

```latex
% !TEX TS-program = pdflatex
% !TEX encoding = UTF-8 Unicode
% An alternative to the standard LaTeX letter class.
\documentclass[fontsize=12pt, paper=a4]{scrlttr2}
% Don't forget to read the KOMA-Script documentation,
% scrguien.pdf
\setkomavar{fromname}{} % your name
\setkomavar{fromaddress}{Address \\ of \\ Sender}
\setkomavar{signature}{} % printed after the \closing
\renewcommand{\raggedsignature}{\raggedright} % make
% the signature ragged right
\setkomavar{subject}{} % subject of the letter
\begin{document}
\begin{letter}{Name and \\ Address \\ of \\ Recipient}
\opening{} % eg. Hello
\closing{} %eg. Regards
\end{letter}
\end{document}
```

3. Haga clic en **Open** (Abrir). Rellene los huecos y edite el texto de relleno del ejemplo:

```latex
\documentclass[fontsize=12pt, paper=a4]{scrlttr2}
\setkomavar{fromname}{My name} % your name
\setkomavar{fromaddress}{Street, City}
\setkomavar{signature}{Name} % printed after the \closing
\setkomavar{subject}{Invoice 1/2021} % subject of the letter
\setkomavar{place}{Place}
\setkomavar{date}{January 1, 2021}
\begin{document}
\begin{letter}{Customer Name\\ Street No. X \\ City \\ Zipcode}
\opening{To whom it may concern} % eg. Hello
Text follows \ldots
\bigskip
\closing{With kind regards} %eg. Regards
\end{letter}
\end{document}
```

4. Compile el documento. Eche un vistazo a nuestra carta de prueba:

> **Figura 11.6** – Un documento de carta

¡Eso fue fácil! Simplemente abrimos la plantilla y modificamos el texto del marcador de posición. Al leer la documentación de KOMA-Script, podemos aprender que el comando `\setkomavar` se utiliza para especificar valores para los parámetros de plantilla como nombre, dirección y asunto. Usamos eso para declarar fecha y lugar también.

Una vez que haya escrito sus datos personales en esta plantilla, puede guardarla para usarla más adelante en lugar de escribir su dirección para cada carta.

La documentación de KOMA-Script, disponible a través de `texdoc koma-script` y en [https://texdoc.org/pkg/koma-script](https://texdoc.org/pkg/koma-script), describe bien las características de la clase `scrlttr2`. Con esto, puede crear una plantilla de carta comercial de aspecto profesional.

Imagine colocar una carta de solicitud de empleo creada con el diseño y las fuentes de LaTeX junto con el paquete `microtype` al lado de una carta de solicitud producida con algún otro software de procesamiento de textos. ¿Cuál causará una mejor impresión?

Al buscar plantillas, código y consejos de LaTeX en Internet, encontrará una gran cantidad de información y código. Este código puede estar desactualizado y la información puede ser obsoleta.

Cuando desarrolla su propia plantilla, probablemente desee utilizar los mejores paquetes, opciones y soluciones modernas disponibles en la actualidad. ¿Cómo puede estar seguro?

Ambas preguntas pueden responderse estudiando el documento `l2tabu`. Este nombre es el atajo común para *An essential guide to LaTeX2e usage*. Este documento destaca comandos y paquetes obsoletos y demuestra los errores más comunes y graves que cometen los usuarios de LaTeX. Como LaTeX se ha desarrollado a lo largo de muchos años, algunos paquetes y técnicas todavía están disponibles y descritos en recursos en línea, pero es posible que ya no se recomienden. Lea esta guía. Le ayudará a evaluar las plantillas y el código que encuentre en línea y se asegurará de producir usted mismo un código óptimo.

Simplemente escriba `texdoc l2tabuen` (`en` significa inglés) en el símbolo del sistema o visite [https://texdoc.org/pkg/l2tabuen](https://texdoc.org/pkg/l2tabuen).

Para probar una plantilla, puede utilizar el paquete `blindtext` y sus comandos, `\blindtext` y `\Blinddocument`. El comando `\blindtext` genera un párrafo de texto simulado y el comando `\Blinddocument` genera contenido simulado para un documento grande, incluidas secciones y listas. Eso demostrará la calidad de salida de la plantilla. Al usar este paquete, debemos cargar el paquete `babel` con una opción de idioma, por ejemplo, simplemente con una plantilla básica de artículo mínimo:

```latex
\documentclass{article}
\usepackage[english]{babel}
\usepackage{blindtext}
\begin{document}
\begin{abstract}
\blindtext
\end{abstract}
\Blinddocument
\end{document}
```

Eso nos da un documento que comienza así:

> **Figura 11.7** – Un artículo con texto simulado

Si usa el editor TeXworks, como hicimos en el ejemplo anterior, puede elegir entre algunas plantillas listas para usar o descargar una plantilla desde [https://latextemplates.com](https://latextemplates.com/). Sin embargo, si trabaja en línea con [https://overleaf.com](https://overleaf.com/), tiene aún más opciones. Básicamente, puede hacer clic en **New Project** (Nuevo proyecto) y elegir una de varias plantillas básicas:

> **Figura 11.8** – Apertura de una plantilla en Overleaf

Si hace clic en **View All** (Ver todas), puede explorar un catálogo completo:

> **Figura 11.9** – El catálogo de plantillas de Overleaf

La colección de plantillas de Overleaf contiene varios miles de plantillas listas para usar para completar su texto. Las instituciones y los usuarios aportan muchas de ellas. La calidad puede variar, pero puede ver capturas de pantalla de los contenidos o títulos mientras navega y probar esas plantillas usted mismo.

Puede ingresar palabras clave como el tipo de documento, el nombre de la universidad o facultad, las características o los nombres de los paquetes en la barra de búsqueda (**Search**).

Puede hacer clic en **Open as Template** (Abrir como plantilla) y obtener un documento compilable con texto de relleno. Eso le permite probar unas 10 plantillas en unos 10 minutos hasta encontrar la perfecta.

Algunas plantillas son bastante complejas, con contenido dividido en varios archivos y organizadas en carpetas. Veamos cómo podemos configurar nosotros mismos una estructura de este tipo a continuación.

---

### Organización de archivos y carpetas

Anteriormente en este capítulo, aprendimos cómo dividir un documento en varios archivos. A medida que un proyecto crece (piense en una tesis o un libro), acumulará rápidamente muchos de ellos: archivos `.tex` de capítulos, apéndices, páginas preliminares y finales, archivos de bibliografía, figuras en varios formatos y tal vez archivos con macros personalizadas también.

Mantener todo en una sola carpeta se vuelve rápidamente difícil de administrar. Un mejor enfoque es agrupar archivos relacionados en carpetas y subcarpetas. Esto hace que el proyecto sea más fácil de navegar y mantener a medida que crece, especialmente porque LaTeX también crea archivos auxiliares en la carpeta de su proyecto.

Aquí hay una estructura de ejemplo simple con nombres de marcadores de posición para mostrar cómo podría configurar las cosas:

```text
project/
    preamble.tex
    macros.tex
    main.tex
    university-style.sty
    frontmatter/
        titlepage.tex
        abstract.tex
        preface.tex
        acknowledgements.tex
    chapters/
        chapter01-intro.tex
        chapter02-methods.tex
        ...
    figures/
        logo.png
        chapter01/
            plot.png
            diagram.png
        chapter02/
            ...
    tables/
        ...
    appendices/
        appendixA.tex
        appendixB.tex
    backmatter/
        bibliography.tex
        indexes.tex
        declaration.tex
```

Dicha estructura de proyecto le brinda un mejor control sobre todas las partes de su contenido. Las buenas convenciones de nomenclatura, como los prefijos numéricos y los nombres de archivos descriptivos, también ayudan.

Su archivo `main.tex` puede verse entonces como algo parecido a esto:

```latex
\documentclass[12pt,a4paper]{report}
\usepackage{university-style}
\input{preamble}
\input{macros}
\usepackage{graphicx}
\graphicspath{
  {figures/}
  {figures/chapter01/}
  {figures/chapter02/}
}
\begin{document}
\input{frontmatter/titlepage}
\input{frontmatter/abstract}
\input{frontmatter/preface}
\input{frontmatter/acknowledgements}
\include{chapters/chapter01-intro}
\include{chapters/chapter02-methods}
\appendix
\include{appendices/appendixA}
\include{appendices/appendixB}
\input{backmatter/bibliography}
\input{backmatter/indexes}
\input{backmatter/declaration}
\end{document}
```

El comando `\graphicspath` especifica dónde busca LaTeX los archivos de imagen. Al definir estas rutas una vez en el preámbulo, puede incluir gráficos sin repetir nombres de directorios largos.

Ahora, puede concentrar la mayor parte de su trabajo en los archivos de capítulo.

De vez en cuando, haga una copia de seguridad de toda la carpeta del proyecto, como un archivo `project.zip`, y guárdela en otro lugar en caso de que su computadora se dañe. Para proyectos más grandes, es una buena idea utilizar el control de versiones, como Git, para realizar un seguimiento de los cambios a lo largo del tiempo. Si es nuevo en esto, la documentación oficial de Git en [https://git-scm.com](https://git-scm.com/) es un punto de partida claro y amigable para principiantes.

---

### Resumen

Las técnicas presentadas en este capítulo le ayudarán a crear y mantener proyectos más grandes. Muchas personas aprenden LaTeX principalmente porque planean escribir textos más largos, como una tesis o un libro. Sin embargo, dividir documentos y utilizar plantillas también es útil para escritos breves, como cartas; piense en el encabezado, el pie de página y los campos de dirección.

En este capítulo, creamos y gestionamos documentos grandes que constan de varios archivos, incluidas páginas preliminares y finales y una portada separada, y los organizamos en una buena estructura de carpetas.

Ahora que podemos desarrollar y manejar documentos grandes, veremos cómo mejorarlos aún más en el próximo capítulo.
