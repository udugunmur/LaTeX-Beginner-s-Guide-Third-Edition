# LaTeX Beginner's Guide
## Capítulo 12: Uso de Hipervínculos y Diseño de Encabezados

En el capítulo anterior, aprendió cómo estructurar y gestionar documentos grandes. Con todo lo que ha aprendido hasta este punto, puede producir documentos bien estructurados con una excelente calidad tipográfica, adecuados para libros, artículos de revistas o una tesis universitaria.

Si planea publicar su trabajo en línea, su documento PDF se beneficiaría de características como hipervínculos y marcadores que facilitan la navegación.

En este capítulo, trabajaremos con herramientas para tales mejoras de navegación y para personalizar encabezados y colores en las siguientes secciones:

- Trabajo con hipervínculos
- Creación de marcadores
- Diseño de encabezados

Cada tema se maneja con paquetes dedicados de LaTeX, que ahora exploraremos.

---

### Trabajo con hipervínculos

Existe un paquete sofisticado llamado `hyperref` que agrega automáticamente funciones de hipervínculos a casi todos los elementos estructurales de un documento de LaTeX. Veamos cómo funciona.

#### Adición de hipervínculos

Cargue el paquete `hyperref` e inspeccione el resultado:

1. Abra el archivo `preamble.tex`, que usamos en el capítulo anterior. Al final, agregue esta línea:

```latex
\usepackage{hyperref}
```

Guarde este documento con el mismo nombre.

2. Abra nuestro Libro de Ecuaciones del capítulo anterior; lo llamamos `equations.tex`.

3. Compile el documento dos veces sin realizar ningún cambio. Veamos cómo aparece ahora el documento; aquí podemos ver cuadros rojos que indican hipervínculos:

> **Figura 12.1** – Una tabla de contenidos con hipervínculos y marcadores

Las referencias cruzadas, como las referencias a números de ecuaciones, también tienen cuadros rojos:

> **Figura 12.2** – Referencias a ecuaciones con hipervínculos

Con solo cargar el paquete `hyperref`, nuestro documento ha cambiado significativamente:

- Obtuvimos una barra de marcadores (*Bookmarks bar*) que nos permite navegar por el documento fácilmente
- El documento contiene hipervínculos resaltados por bordes rojos
- Cada entrada en la tabla de contenidos se ha convertido en un hipervínculo al principio del capítulo correspondiente
- Todas las referencias cruzadas se han convertido en hipervínculos

Esta es una mejora excelente para las versiones electrónicas de nuestros documentos.

Los cuadros rojos no aparecerán en el papel cuando imprima el documento; solo aparecen en la pantalla para la navegación electrónica. Lo mismo se aplica a los marcadores.

Si no le gusta el borde rojo predeterminado para los hipervínculos, puede cambiarlo fácilmente editando las opciones de `hyperref`. Probemos esto a continuación.

#### Personalización de hipervínculos

Ahora, pasaremos opciones al paquete `hyperref` que modifican la forma en que se enfatizan los enlaces:

1. Abra el archivo `preamble.tex` nuevamente. Esta vez, especifique las opciones para `hyperref`:

```latex
\usepackage[colorlinks=true,linkcolor=red]{hyperref}
```

2. Guarde este documento, vaya al documento principal `equations.tex` y compílelo dos veces. La tabla de contenidos ha cambiado:

> **Figura 12.3** – Tabla de contenidos con hipervínculos coloreados

En lugar de marcos, ahora usamos rojo para los hipervínculos enfatizados. A diferencia de los cuadros, podemos ver el color en un documento impreso.

`hyperref` proporciona formas de configurar estas opciones. La primera que usamos es la siguiente:

```latex
\usepackage[key=value list]{hyperref}
```

Alternativamente, podríamos escribir `\usepackage{hyperref}` y establecer las opciones después:

```latex
\hypersetup{key=value list}
```

Nuestro ejemplo haría lo mismo con lo siguiente:

```latex
\hypersetup{colorlinks=true,linkcolor=red}
```

También podemos combinar estos métodos.

Veamos una selección de opciones útiles. Para las siguientes opciones, elija `true` o `false`. Si no especifica un valor, `hyperref` selecciona el predeterminado, que se muestra aquí entre paréntesis:

- `draft`: Desactiva todas las opciones de hipertexto (`false`)
- `final`: Activa todas las opciones de hipertexto (`true`)
- `debug`: Imprime mensajes de diagnóstico adicionales en el archivo de registro `.log` (`false`)
- `backref`: Agrega enlaces inversos (*backlinks*) a la bibliografía, es decir, enlaces desde elementos bibliográficos hacia citas en el texto (`false`)
- `hyperindex`: Agrega enlaces a los números de página en el índice (`true`)
- `hyperfootnotes`: Convierte las marcas de notas al pie en hipervínculos (`true`)
- `hyperfigures`: Agrega hipervínculos a las figuras (`false`)
- `linktocpage`: Agrega enlaces a los números de página en lugar de al texto en la tabla de contenidos (TOC), lista de figuras (LOF) y lista de tablas (LOT) (`false`)
- `frenchlinks`: Utiliza versalitas para los enlaces en lugar de color (`false`)
- `bookmarks`: Escribe marcadores para la navegación del lector de PDF (`true`)
- `bookmarksopen`: Muestra todos los marcadores en una vista expandida cuando se abre el PDF (`false`)
- `bookmarksnumbered`: Incluye el número de sección en los marcadores (`false`)
- `colorlinks`: Escribe enlaces y anclas en color, según el tipo de enlace, como referencias de página, URLs, referencias de archivos y citas, en lugar de imprimir un borde alrededor de los enlaces (`false`)

Cuando habilita la opción `colorlinks`, puede elegir el color para cada tipo de enlace de la siguiente lista. Nuevamente, el valor predeterminado está entre paréntesis:

- `linkcolor`: Color de enlaces generales (`red`)
- `citecolor`: Color para citas de elementos bibliográficos (`green`)
- `urlcolor`: Color para direcciones de sitios web, es decir, URLs (`magenta`)
- `filecolor`: Color para enlaces a archivos (`cyan`)

Hay muchas más opciones para personalizar los bordes de los enlaces, el tamaño de la página PDF, las anclas, la apariencia de los marcadores y el estilo de visualización de la página PDF. La documentación de `hyperref` los enumera todos. Simplemente escriba `texdoc hyperref` en la línea de comandos o visite [https://texdoc.org/pkg/hyperref](https://texdoc.org/pkg/hyperref).

Supongamos que desea desactivar todo el resaltado de enlaces, por ejemplo para imprimir en papel; proporcione la opción `hidelinks` sin valor. Luego, los enlaces aparecerán como texto normal sin bordes ni colores.

Algunas opciones de texto nos permiten especificar los metadatos de los archivos PDF, como el nombre del autor, el título y las palabras clave. Puede ver esta información inspeccionando las propiedades del documento en el lector de PDF. Esto es aún más beneficioso, ya que los motores de búsqueda de Internet pueden encontrar y clasificar su documento PDF según estos metadatos. Si publica en línea, esto mejora las posibilidades de que los lectores encuentren su publicación.

Por eso ahora agregaremos metadatos de PDF a nuestro Libro de Ecuaciones del [Capítulo 11](https://subscription.packtpub.com/book/business-and-other/9781805804574/11), *Desarrollo de documentos grandes*. Además de elegir palabras clave sensatas, estableceremos el título y el nombre del autor. Durante el desarrollo, ¿por qué no elegir al gran matemático a quien dedicamos nuestro libro? Hagámoslo:

1. Abra el archivo `preamble.tex` y agregue las siguientes líneas:

```latex
\hypersetup{
  pdfauthor={Carl Friedrich Gauss},
  pdftitle={The Big Book of Equations},
  pdfsubject={Solving Equations and Equation Systems},
  pdfkeywords={equations,mathematics}
}
```

2. Guarde ese archivo. Vaya al documento principal `equations.tex` y haga clic en **Typeset** para compilar.
3. Inspeccionemos la sección Propiedades del documento (*Document Properties*). Si está utilizando Acrobat Reader, haga clic en el menú **File** (Archivo) y luego en **Properties** (Propiedades):

> **Figura 12.4** – Metadatos PDF en Propiedades del documento

Eso fue fácil. Proporcionamos todas las propiedades del documento utilizando opciones de `hyperref`; solo tuvimos que encerrar cada entrada entre llaves.

Las opciones de metadatos más utilizadas son las siguientes:

- `pdftitle`
- `pdfauthor`
- `pdfsubject`
- `pdfcreator`
- `pdfproducer`
- `pdfkeywords`

Los metadatos del PDF almacenan información básica sobre un documento para los lectores y los motores de búsqueda. Los campos de metadatos más comunes describen el documento en sí: `pdftitle`, `pdfauthor` y `pdfsubject` definen el título, el autor y el tema general, respectivamente. Los campos `pdfcreator` y `pdfproducer` documentan el software utilizado para generar y procesar el PDF, que generalmente se configura automáticamente pero se puede personalizar. Elegir cuidadosamente los metadatos vale la pena, especialmente para los archivos PDF compartidos en línea. Utilice un título claro y descriptivo en lugar de un nombre de archivo y elija un conjunto pequeño y enfocado de palabras clave significativas. Piense en lo que los lectores podrían buscar y evite términos vagos. Los buenos metadatos mejoran la capacidad de búsqueda y le dan a su PDF un acabado más profesional.

Debido a que el paquete `hyperref` redefine los comandos de muchos otros paquetes para agregar la funcionalidad de hipervínculos, debemos cargarlo después de esos paquetes. Una buena regla general es cargar el paquete `hyperref` al final de su preámbulo. Algunos paquetes son excepciones a esa regla, a saber: `algorithm`, `amsrefs`, `bookmark`, `chappg`, `cleveref`, `glossaries`, `hypernat`, `linguex`, `sidecap` y `tabularx`. Para obtener más información, consulte [https://latexguide.org/hyperref](https://latexguide.org/hyperref).

Hay otras formas de agregar hipervínculos y marcadores, que veremos ahora.

#### Creación manual de hipervínculos

Dado que el paquete `hyperref` crea automáticamente enlaces para casi todos los tipos de referencias cruzadas, rara vez necesitará crear hipervínculos usted mismo. Aún así, el paquete proporciona comandos de usuario para hacerlo cuando sea necesario:

- `\href{URL}{text}` convierte `text` en un hipervínculo que apunta a la `URL` (la dirección del sitio web)
- `\url{URL}` imprime la `URL` y la vincula
- `\nolinkurl{URL}` imprime la `URL` sin vincularla
- `\hyperref[label]{text}` convierte el texto en un hipervínculo que se vincula a la ubicación donde se establece la etiqueta (*label*) (es decir, el mismo lugar al que apuntaría `\ref{label}`)
- `\hypertarget{name}{text}` crea un nombre de destino para posibles hipervínculos con `text` como ancla
- `\hyperlink{name}{text}` convierte el texto en un hipervínculo que apunta al nombre de destino `name`

Un ancla es un destino de salto interno en el documento. Los comandos de sección como `\chapter` o `\section` crean automáticamente anclas a las que pueden apuntar los hipervínculos y las entradas de la tabla de contenidos.

A veces, sin embargo, agrega una entrada a la tabla de contenidos manualmente usando el comando `\addcontentsline`, lo que crea una entrada de tabla de contenidos con hipervínculo. Aún así, no ha habido un comando de sección correspondiente que establezca el ancla. La entrada de la tabla de contenidos apunta al ancla creada más recientemente, que puede ser el capítulo o sección anterior. Como resultado, al hacer clic en la entrada de la tabla de contenidos se salta a la página incorrecta.

El comando `\phantomsection` viene al rescate; simplemente establece un ancla como lo haría `\hypertarget{}{}`. A menudo se utiliza de esta manera para crear una entrada en la tabla de contenidos para la bibliografía mientras se vincula a la página correcta, de la siguiente manera:

```latex
\cleardoublepage
\phantomsection
\addcontentsline{toc}{chapter}{Bibliography}
\bibliography{name}
```

En efecto, puede pensar en `\phantomsection` como la inserción de un ancla invisible de `\section`. El comando `\addcontentsline` posterior hace referencia a ese ancla.

---

### Creación de marcadores

Es posible que su panel de marcadores ya esté lleno de entradas de capítulos y secciones creadas por `hyperref`. ¿Pero qué pasa si desea agregar marcadores usted mismo? Puede hacerlo de la siguiente manera:

- `\pdfbookmark[level]{text}{name}` crea un marcador con `text` en el nivel opcionalmente especificado `level`. El nivel predeterminado es 0. Trate el nombre `name` igual que con el comando `\label`; debe ser único porque identifica el ancla interna.

También puede insertar marcadores relativos al nivel actual:

- `\currentpdfbookmark{text}{name}` coloca un marcador en el nivel actual
- `\belowpdfbookmark{text}{name}` crea un marcador un nivel más profundo
- `\subpdfbookmark{text}{name}` desciende un nivel y crea un marcador en ese nivel más profundo

El paquete `bookmark` ofrece opciones de personalización adicionales, incluidos el estilo y el color de fuente. Puede leer sobre él ejecutando `texdoc bookmark` en la línea de comandos o visitando [https://texdoc.org/pkg/bookmark](https://texdoc.org/pkg/bookmark).

#### Uso de fórmulas matemáticas y símbolos especiales en marcadores

Debido a las limitaciones del formato PDF, no podemos utilizar matemáticas ni símbolos especiales dentro de los marcadores de PDF. Esto se convierte en un problema, por ejemplo, cuando un título de sección contiene símbolos matemáticos o comandos de fuente, ya que `hyperref` intentaría colocarlos en el marcador. Para evitar esto, puede proporcionar dos versiones del título: una para TeX y otra para el marcador PDF. Utilice este comando:

```latex
\texorpdfstring{string with TeX code}{pdf text string}
```

Devuelve el argumento según el contexto para evitar este tipo de problemas. Se puede utilizar así:

```latex
\section{The equation \texorpdfstring{$y=x^2$}{y=x\texttwosuperior}}
```

Eso puede resultar útil.

Si carga `hyperref` con la opción `unicode`, puede utilizar caracteres de texto Unicode en los marcadores, como aquí:

```latex
\section{\texorpdfstring{$\gamma$}{\textgamma} radiation}
```

Veamos rápidamente cómo funcionan estos comandos en un pequeño documento de muestra:

```latex
\documentclass{article}
\usepackage{bm}
\usepackage[colorlinks=true,psdextra,unicode]{hyperref}
\begin{document}
\pdfbookmark[1]{\contentsname}{toc}
\tableofcontents
\pdfbookmark[1]{Abstract}{abstract}
\begin{abstract}
\centering
Sample sections follow.
\end{abstract}
\section{The equation \texorpdfstring{$y=x^2$}{y=x\texttwosuperior}}
\section{\texorpdfstring{$\gamma$}{\textgamma} radiation}
\section[\texorpdfstring{Let $\int\sim\sum$ for $n\rightarrow\infty$}
{Let \int\sim\sum\ for n\rightarrow\infty}]
{Let $\bm{\int\sim\sum}$ for $\bm{n\rightarrow\infty}$}
\end{document}
```

Como se resalta en el código anterior, el comando `\section` hace estas tres cosas:

- Imprime el encabezado de sección. Esta vez, usamos el comando `\bm` del paquete `bm` para producir matemáticas en negrita. Compárelo con los otros encabezados.
- Coloca el nombre de la sección en la tabla de contenidos.
- Crea un marcador con símbolos de texto Unicode en lugar de símbolos matemáticos. Cargamos `hyperref` con las opciones `unicode` y `psdextra`, que permiten símbolos matemáticos en los marcadores.

Obtenemos esta salida con marcadores:

> **Figura 12.5** – Fórmulas matemáticas en marcadores

En el primer argumento del comando `\texorpdfstring`, usamos `$...$` para ingresar al modo matemático. Sin embargo, en el segundo argumento de `\texorpdfstring`, omitimos `$...$` intencionalmente ya que será texto Unicode, no glifos de fuentes matemáticas.

Si bien las fórmulas matemáticas en encabezados y marcadores pueden no ser una buena idea de todos modos, podemos hacerlo si realmente lo necesitamos.

En la siguiente sección, pasaremos al diseño y formato de los encabezados.

---

### Diseño de encabezados

En el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*, abordamos brevemente el desafío de personalizar los encabezados. Tiene que haber una manera coherente de modificar la fuente, el espaciado y la numeración de los encabezados en todo el documento. Afortunadamente, existe un paquete muy útil para eso: `titlesec`. Lo usaremos ahora para diseñar encabezados de capítulos y secciones.

Volvamos al ejemplo que usamos anteriormente en este capítulo. Nuestro objetivo es crear encabezados con las siguientes características:

- Títulos centrados
- Un tamaño de fuente más pequeño
- Espacio reducido arriba y abajo
- Una fuente sans-serif, que es una buena opción para encabezados en negrita

Comencemos:

1. Abra el archivo `preamble.tex`, que usamos anteriormente en este capítulo. Inserte esta línea para cargar el paquete `titlesec`:

```latex
\usepackage{titlesec}
```

2. Agregue este comando para especificar el diseño y la fuente de los encabezados de capítulo:

```latex
\titleformat{\chapter}[display]
  {\normalfont\sffamily\Large\bfseries\centering}
  {\chaptertitlename\ \thechapter}{0pt}{\Huge}
```

3. Ahora, defina el encabezado de sección llamando nuevamente al comando `\titleformat`:

```latex
\titleformat{\section}
  {\normalfont\sffamily\large\bfseries\centering}
  {\thesection}{1em}{}
```

4. Agregue esta línea para ajustar el espaciado del encabezado de capítulo:

```latex
\titlespacing*{\chapter}{0pt}{30pt}{20pt}
```

5. Guarde `preamble.tex` y compile el documento principal `equations.tex`. Veamos cómo han cambiado los encabezados:

> **Figura 12.6** – Encabezados centrados

En el paso 1, cargamos el paquete `titlesec`, que proporciona una interfaz integral para personalizar encabezados de partes, capítulos, secciones e incluso partes de sección más pequeñas hasta subpárrafos.

En el paso 2, seleccionamos un estilo `display` que coloca el número de encabezado y el título en líneas separadas. Primero cambiamos a la fuente base usando el comando `\normalfont`, para estar seguros. Al aplicar `\sffamily`, cambiamos a una fuente sans-serif, establecimos el tamaño y el peso y, finalmente, declaramos que todo el encabezado se centrará.

En el paso 3, todo es muy similar al paso 2; simplemente omitimos `[display]` para obtener el número y el título en la misma línea.

Para comprender los argumentos restantes, eche un vistazo a la forma general del comando `\titleformat`:

```latex
\titleformat{cmd}[shape]{format}{label}{sep}{before}[after]
```

El significado de los argumentos es el siguiente:

- `cmd`: representa el comando de sección que redefinimos, es decir, `\part`, `\chapter`, `\section`, `\subsection`, `\subsubsection`, `\paragraph` o `\subparagraph`.
- `shape`: especifica la forma del párrafo, con el efecto de los posibles valores como sigue:
  - `display`: coloca la etiqueta en un párrafo separado
  - `hang`: crea una etiqueta colgante, como en las secciones estándar, y es la opción predeterminada
  - `runin`: produce un título integrado (*run-in*) como lo hace `\paragraph` de forma predeterminada
  - `leftmargin`: coloca el título en el margen izquierdo
  - `rightmargin`: coloca el título en el margen derecho
  - `drop`: envuelve el texto alrededor del título y requiere cuidado para evitar superposiciones
  - `wrap`: funciona como `drop`, pero ajusta el espacio para el título para que coincida con la línea de texto más larga
  - `frame`: funciona como `display` y además enmarca el título
- `format`: puede contener comandos que se aplicarán a la etiqueta y al texto del título.
- `label`: imprime la etiqueta, es decir, el número.
- `sep`: es una longitud que especifica la separación entre la etiqueta y el texto del título. Con la opción `display`, es la separación vertical. Con la opción `frame`, significa la distancia entre el texto y el marco. De lo contrario, es la separación horizontal entre la etiqueta y el título.
- `before`: puede contener código que viene antes del cuerpo del título. Se permite que el último comando tome un argumento, que luego debería ser el texto del título.
- `after`: puede contener código que viene después del cuerpo del título.

Son muchas opciones. Consulte la documentación de `titlesec` para obtener aún más información ejecutando `texdoc titlesec` o visitando [https://texdoc.org/pkg/titlesec](https://texdoc.org/pkg/titlesec).

Usamos el comando de `titlesec` llamado `\chaptertitlename`, cuyo valor predeterminado es `\chaptername`. Por lo tanto, el valor predeterminado es *Chapter*. En un apéndice, cambia a `\appendixname`.

Usando el siguiente comando, personalizamos el espaciado de todos los encabezados de capítulo:

```latex
\titlespacing*{cmd}{left}{beforesep}{aftersep}[right]
```

Los argumentos tienen los siguientes significados:

- `left`: funciona de manera diferente según la forma elegida: con `drop`, `leftmargin` y `rightmargin`, es el ancho del título. Con `wrap`, es el ancho máximo. Con `runin`, establece la sangría antes del título. De lo contrario, aumenta el margen izquierdo. Si es negativo, disminuye, lo que significa que sobresale hacia el margen.
- `beforesep`: establece el espacio vertical antes del título.
- `aftersep`: establece la separación entre el título y el texto. Con una forma `hang`, `block` y `display`, tiene un significado vertical. Con una forma `runin`, `drop`, `wrap`, `leftmargin` y `rightmargin`, es un ancho horizontal. Nuevamente, puede ser un valor negativo.
- `right`: aumenta el margen derecho cuando se utiliza una forma `hang`, `block` o `display`.

Si usa el asterisco, `titlesec` elimina la sangría del párrafo siguiente. Eso es como en las secciones estándar: el texto que sigue al encabezado de una sección no tiene sangría de párrafo. Con `drop`, `wrap` y `runin`, la versión con asterisco no tiene significado.

En nuestro ejemplo, evitamos sangrar el párrafo que sigue a un encabezado de capítulo y especificamos un espacio de 30pt antes del encabezado y un espacio de 20pt después de él. Eso es menos en comparación con las clases estándar, que usan 50pt por encima de los encabezados de capítulo.

Es muy recomendable leer la documentación de `titlesec` para aprovecharla al máximo. Su apéndice muestra cómo se definirían los encabezados en clases estándar usando `\titleformat` y `\titlesec`. Esa es una excelente manera de comenzar: copiar estas definiciones y modificarlas.

El uso de encabezados sans-serif es muy común hoy en día. No tienen la apariencia pesada y antigua de los encabezados serif en negrita. Sin embargo, el texto serif ofrece la mejor legibilidad para el cuerpo del texto. Ahora le toca a usted elegir: ya tiene las herramientas.

---

### Resumen

En este capítulo, mejoramos nuestro documento con una estructura de hipertexto que incluye enlaces coloreados y marcadores para la navegación. Ahora podemos editar los metadatos del PDF y personalizar los estilos de nuestros encabezados.

En el próximo capítulo, exploraremos nuevas formas de estilos y navegación.
