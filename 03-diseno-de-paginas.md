# LaTeX Beginner's Guide
## Capítulo 3: Diseño de Páginas

Ahora que sabe cómo dar formato al texto, es hora de mirar páginas completas y la estructura general del documento.

En este capítulo, estructuraremos un documento utilizando capítulos y secciones, y aprenderemos cómo ajustar el diseño de su página, incluidos los márgenes, la orientación de la página, los encabezados y los pies de página. Esto le da control sobre todo el diseño del documento.

Cubriremos los siguientes temas:

- Estructuración con capítulos
- Ajuste de los márgenes de página
- Creación de un diseño a dos columnas
- Diseño de encabezados y pies de página
- Adición de notas al pie
- Gestión de saltos de página
- Ampliación de una página
- Cambio del interlineado
- Alineación de la altura del área de texto
- Creación de una tabla de contenidos

Trabajar a través de estos puntos construirá una mejor comprensión de las clases y paquetes de documentos.

Comenzaremos con un documento de ejemplo de varias páginas que seguiremos utilizando a lo largo de los capítulos para probar nuevas funciones. Puede ver, editar y compilar todos los ejemplos en línea en el sitio web complementario del libro: [https://latexguide.org/chapter-03](https://latexguide.org/chapter-03).

---

### Estructuración con capítulos

Comencemos a escribir un documento más largo. Seleccionaremos la clase de documento `book` y llenaremos las páginas con texto de relleno para explorar el diseño de la página:

1. Cree un nuevo documento e introduzca las siguientes líneas como nuestro preámbulo:

```latex
\documentclass[a4paper,12pt]{book}
\usepackage[english]{babel}
\usepackage{blindtext}
```

2. Continúe escribiendo el cuerpo del documento que contiene un encabezado de capítulo, encabezados de sección y subsección, y algo de texto de relleno:

```latex
\begin{document}
\chapter{Exploring the page layout}
In this chapter we will study the layout of pages.
\section{Some filler text}
\blindtext
\section{A lot more filler text}
More dummy text will follow.
\subsection{Plenty of filler text}
\blindtext[10]
\end{document}
```

3. Compile haciendo clic en **Typeset**. Mire la primera página:

> **Figura 3.1** – Una página de ejemplo

Hemos elegido la clase de documento `book`. Esta clase es adecuada para documentos extensos como un libro, un informe científico o una tesis, cuando se imprime a doble cara. Los libros suelen ser a doble cara y constan de capítulos. De forma predeterminada, y esto es muy común, los capítulos comienzan en las páginas de la derecha, que tienen números de página impares. Si es necesario, LaTeX inserta una página en blanco a la izquierda, de número par, para que el siguiente capítulo pueda comenzar en la página de la derecha siguiente.

Además, los libros a menudo tienen partes preliminares (*front matter*), que incluyen una o más páginas de título, y partes finales (*back matter*), que generalmente constan de bibliografía, índice y otro contenido relevante. La clase `book` admite todo esto.

Usamos la opción `a4paper` para que el documento se formateara para que quepa en papel A4. Para el tamaño de papel carta de EE. UU., usaríamos la opción `letterpaper` en su lugar. La opción de clase de documento `12pt` le indicó a LaTeX que use un tamaño de fuente base de 12 pt.

Cargamos el paquete `babel`. Ese paquete proporciona herramientas de soporte tipográfico para muchos idiomas, incluidas las reglas de separación silábica adecuadas para el idioma elegido y las traducciones para términos implícitos. Por ejemplo, usamos la opción `english` con `babel` y obtuvimos *Chapter 1* en nuestro encabezado de capítulo. Si elegimos `french` en lugar de `english`, obtendremos *Chapitre 1* en nuestro encabezado.

El inglés americano es el predeterminado. Para el inglés británico, usaríamos la opción `british` con `babel`. Hay diferencias muy pequeñas entre los dos. En inglés británico, algunas palabras se escriben de manera diferente y las reglas de división silábica son un poco diferentes, por ejemplo.

Cargamos el paquete `blindtext`, que ha sido desarrollado para producir texto de relleno. Utiliza `babel` para detectar el idioma del documento; le indicamos el idioma `english` a `babel`, lo que en realidad significa inglés americano. Sin `babel`, `blindtext` usaría texto de relleno en latín de forma predeterminada. Luego, el comando `\blindtext` imprime un texto simulado solo para llenar el espacio.

El comando `\chapter` produjo un encabezado grande, que siempre comenzará en una página nueva. Ya hemos visto el comando `\section`. Es nuestro segundo nivel de sección y genera un encabezado más pequeño que `\chapter`. La numeración de este encabezado se actualiza automáticamente mediante LaTeX. Por último, refinamos la estructuración con el comando `\subsection` seguido de más texto simulado para llenar la página.

Otro paquete ampliamente utilizado para texto simulado se llama `lipsum`. Genera el famoso texto *Lorem Ipsum* que los tipógrafos han utilizado durante décadas.

Veamos ahora cómo ajustar los márgenes predeterminados.

---

### Ajuste de los márgenes de página

A veces, los editores o supervisores solicitan que siga sus especificaciones para un documento. Además del tamaño de fuente, el interlineado y otros problemas de estilo, puede haber especificaciones para los márgenes. En este caso, necesitaría anular los valores predeterminados de LaTeX, especificando los márgenes con precisión.

El paquete `geometry` lo hace fácil. Cargaremos el paquete `geometry` e indicaremos el ancho y el alto exactos de todos los márgenes:

1. Amplíe el preámbulo del ejemplo anterior en este capítulo con este comando:

```latex
\usepackage[a4paper, inner=1.5cm, outer=3cm, top=2cm, bottom=3cm, bindingoffset=0.5cm]{geometry}
```

2. Haga clic en **Typeset** para compilar el código y observe cómo cambian los márgenes.

El paquete `geometry` maneja el diseño, incluido el tamaño del papel, los márgenes y otras dimensiones. Elegimos el tamaño de papel A4, con un margen exterior de 3 cm y un margen interior de 1.5 cm.

Cuando un libro a doble cara está abierto frente a nosotros, los dos márgenes interiores se fusionan visualmente en un único espacio central. Para lograr márgenes visualmente equilibrados (izquierdo, central y derecho), podemos establecer el margen interior en la mitad del ancho del margen exterior. Por eso los márgenes exteriores suelen ser más anchos que los márgenes interiores. Puede haber una razón para hacer que el margen interior sea un poco más ancho: podríamos perder este espacio más adelante debido a métodos de encuadernación como el pegado o el grapado. Pero esto depende del tipo de encuadernación, y luego se hace con una opción adicional de compensación de encuadernación `bindingoffset`.

Establecemos el margen superior en 2 cm y el margen inferior en 3 cm. Por último, especificamos un valor de 0.5 cm para una corrección de encuadernación.

En los primeros días de LaTeX, era común manipular las dimensiones del diseño directamente. Este enfoque tenía algunas desventajas. Podríamos cometer errores fácilmente al calcular las longitudes; por ejemplo, el margen izquierdo más el margen derecho más el ancho del texto podrían no ajustarse al ancho del papel.

El paquete `geometry` simplifica este proceso. Proporciona una interfaz fácil de usar para la configuración del diseño. Proporciona autocompletado, calcula los valores faltantes para que coincidan con el tamaño del papel e incluso añade longitudes faltantes utilizando un enfoque heurístico para lograr un diseño bien equilibrado.

El paquete `geometry` entiende las opciones como pares `clave=valor`, separados por comas. Si carga `geometry` sin ningún argumento, puede establecer esos argumentos más tarde con el comando `\geometry{lista de argumentos}`.

Echemos un vistazo más de cerca a las opciones del paquete `geometry` para controlar cada aspecto del diseño de su página.

#### Elección del tamaño de papel

El paquete `geometry` ofrece varias opciones para configurar el tamaño y la orientación del papel:

- `paper=name` establece el tamaño del papel por nombre, por ejemplo, `paper=a4paper`. Los tamaños admitidos incluyen `letterpaper`, `executivepaper`, `legalpaper`, `a0paper`, `a6paper`, `b0paper`, `b6paper`, entre otros.
- `paperwidth` y `paperheight` establecen dimensiones de papel personalizadas, como `paperwidth=7in` y `paperheight=10in`.
- `papersize={width,height}` establece tanto el ancho como la altura del papel en una sola clave, como `papersize={7in,10in}`. Este es un ejemplo de un argumento de doble valor.
- `portrait` establece la orientación del papel en modo vertical, que es la opción predeterminada. `landscape` cambia la orientación del papel a modo horizontal.

Si ya ha especificado el nombre del papel en la clase de documento, `geometry` lo seleccionará automáticamente. De hecho, todas las opciones de clase de documento se pasan a los paquetes que las admiten.

#### Especificación del área de texto

Utilice estas opciones para controlar el tamaño del bloque de texto:

- `textwidth` establece el ancho del área de texto principal, como `textwidth=140mm`.
- `textheight` establece su altura, como `textheight=180mm`.
- `lines` ofrece una forma alternativa de definir la altura del texto especificando el número de líneas, como `lines=25`.
- `includehead` incluye el encabezado de página en el cálculo de la altura del texto; esta opción está establecida en `false` por defecto.
- `includefoot` incluye el pie de página en el área de texto; esta opción también está establecida en `false` de forma predeterminada.

#### Configuración de los márgenes

Puede controlar los márgenes visibles utilizando las siguientes opciones:

- `left` y `right` definen el ancho de los márgenes izquierdo y derecho, como `left=2cm`. Úselos para documentos a una sola cara.
- `inner` y `outer` establecen el ancho del margen interior y exterior, como `inner=2cm`. Úselos para documentos a doble cara.
- `top` y `bottom` establecen la altura de los márgenes verticales, como `top=25mm`.
- `twoside` habilita el modo de diseño a doble cara. Esto significa que los márgenes izquierdo y derecho se intercambiarán en las páginas de la izquierda, también llamadas páginas pares o versos (*verso pages*).

Si su libro está impreso y encuadernado, ya sea con pegamento, grapas u otros medios, la encuadernación puede cubrir parte del margen interior. Puede establecer un valor para la opción `bindingoffset` para reservar ancho a fin de compensar la parte del margen interior que está oculta en la encuadernación, de modo que el margen interior visible se vea tan ancho como espera.

Esa es solo una selección de opciones de uso común; hay muchas más. Puede elegir y configurar algunas opciones de forma intuitiva; por ejemplo, `\usepackage[margin=3cm]{geometry}` dará como resultado un margen de 3 cm en cada borde del papel, y el tamaño del papel proviene de la clase de documento, a menos que se especifique lo contrario.

El autocompletado funciona así:

- `paperwidth = left + width + right`, donde `width=textwidth` por defecto
- `paperheight = top + height + bottom`, donde `height=textheight` por defecto

Si decide incluir notas marginales dentro del cuerpo del texto al calcular el diseño, el ancho podría ser mayor que `textwidth`. Si se dan dos dimensiones del lado derecho de cada fórmula, se calculará la dimensión faltante. Por eso puede ser suficiente especificar `left` y `right`, y `top` y `bottom`, respectivamente. Incluso si solo se especifica un margen, las otras dimensiones se determinarán utilizando proporciones de margen predeterminadas, de la siguiente manera:

- `top:bottom = 2:3`
- `left:right = 1:1` para documentos a una sola cara
- `inner:outer = 2:3` para documentos a doble cara

Puede sonar complejo, pero así es exactamente como `geometry` le ayuda a lograr un diseño de página limpio y equilibrado, incluso cuando faltan algunos valores.

El paquete `geometry` viene con un manual completo. No deje que su longitud le intimide; está diseñado para guiarle a través de las numerosas funciones.

Como se mostró anteriormente en el [Capítulo 1](https://subscription.packtpub.com/book/business-and-other/9781805804574/1), *Primeros pasos con LaTeX*, puede abrir el manual escribiendo `texdoc geometry` en la línea de comandos, en una ventana de terminal o en Internet en [https://texdoc.org/pkg/geometry](https://texdoc.org/pkg/geometry).

Ahora que sabe cómo configurar la geometría básica de la página, pasaremos a las opciones para cambiar el diseño del texto, como la orientación horizontal y el formato en varias columnas.

---

### Creación de un diseño a dos columnas

Ya sabe que una clase de documento define los cimientos de su documento. Proporciona comandos y entornos que amplían las funciones estándar de LaTeX. Aunque la clase proporciona un estilo predeterminado, puede personalizarlo utilizando las opciones de clase de documento.

Cambiemos la orientación de nuestro primer ejemplo a horizontal y compongamos nuestro texto en dos columnas:

1. Añada las opciones `landscape` y `twocolumn` a la línea `\documentclass` de nuestro ejemplo, de la siguiente manera:

```latex
\documentclass[a4paper,12pt,landscape,twocolumn]{book}
```

2. Cargue el paquete `geometry`:

```latex
\usepackage{geometry}
```

3. Haga clic en **Typeset** para compilar y ver el nuevo diseño en efecto:

> **Figura 3.2** – Un diseño de página horizontal a dos columnas

Al utilizar la opción `landscape`, cambiamos la orientación de la página de vertical a horizontal. La opción `twocolumn` divide el cuerpo del texto del documento en dos columnas.

Cargamos el paquete `geometry` para asegurarnos de que la página PDF coincida con el diseño horizontal. Sin él, el PDF final permanecería en modo vertical.

El comando `\twocolumn[opening text]` inicia una página a dos columnas con un texto de apertura opcional sobre el ancho completo. `\onecolumn` comienza una página a una sola columna. Si desea equilibrar las columnas en la última página o si desea tener más de dos columnas, utilice el paquete `multicols`.

Las clases base de LaTeX son `article`, `book`, `report`, `slides` y `letter`. Como sugiere el nombre, la última se puede utilizar para escribir cartas, aunque existen otras clases adecuadas, como `scrlttr2`.

`slides` se puede utilizar para crear presentaciones, pero hoy en día existen clases más potentes y ricas en funciones, como `beamer` y `powerdot`.

Resumamos las opciones de las clases base:

- `a4paper`, `a5paper`, `b5paper`, `letterpaper`, `legalpaper` o `executivepaper`: La salida se formateará de acuerdo con este tamaño de papel; por ejemplo, A4 se formateará como 210 mm x 297 mm. La opción `letterpaper` (8.5 pulg. x 11 pulg.) es la predeterminada. Cargar el paquete `geometry` permite más tamaños.
- `10pt`, `11pt` o `12pt`: El tamaño del texto normal en el documento; el valor predeterminado es 10 puntos (`10pt`). El tamaño de los encabezados, notas al pie, índices, etc., se escalará en consecuencia.
- `landscape`: Cambia al formato horizontal intercambiando el ancho y el alto de las dimensiones del papel de salida.
- `onecolumn` o `twocolumn`: Decide si las páginas serán de una columna (predeterminado) o de dos columnas. La clase `letter` no lo admite.
- `oneside` o `twoside`: Controla el diseño para imprimir en una o ambas caras de una página. `oneside` es el valor predeterminado, excepto para la clase `book`. `twoside` no es aplicable a la clase `slides` ni a la clase `letter`.
- `openright` o `openany`: La primera opción permite que los capítulos comiencen en una página de la derecha (el valor predeterminado para la clase `book`), mientras que la segunda opción permite que los capítulos comiencen en cualquier página (el valor predeterminado para la clase `report`). Estas opciones solo son compatibles con las clases `book` y `report` porque las otras clases no proporcionan capítulos.
- `titlepage` o `notitlepage`: La primera provoca una página de título separada cuando se usa `\maketitle` y es el valor predeterminado, excepto para la clase `article`. El valor predeterminado de `article` es `notitlepage`, lo que significa que el texto normal puede seguir al título en la misma página.
- `final` o `draft`: Si se establece `draft`, LaTeX marcará las líneas sobrellenadas (*overfull lines*) con una caja negra, lo cual es útil para revisar y mejorar el resultado. Algunos paquetes también admiten estas opciones, comportándose de manera diferente en ese caso, como omitir la incrustación de gráficos y listados cuando se ha elegido `draft`. `final` es el valor predeterminado.
- `openbib`: Cuando se establece esta opción, la bibliografía se formateará en estilo abierto en lugar de estilo comprimido.
- `fleqn`: Esto alinea las fórmulas desplegadas a la izquierda en lugar de centrarlas.
- `leqno`: Para las fórmulas numeradas desplegadas, el número se colocará en el lado izquierdo. El lado derecho es el predeterminado.

Muchas otras clases también admiten estas opciones y, a menudo, ofrecen aún más. Para un tamaño de fuente base poco común, las clases `extarticle`, `extbook`, `extreport` y `extletter` proporcionan tamaños de fuente base de 8 puntos a 20 puntos. Las clases `KOMA-Script` admiten tamaños de fuente base arbitrarios.

Las clases `KOMA-Script` sirven como alternativas mejoradas a las clases base: para cada clase base, como `article`, `book` o `report`, hay una clase KOMA correspondiente (`scrartcl`, `scrbook` y `scrreprt`, respectivamente). Ofrecen un conjunto de características significativamente ampliado, con muchos comandos y opciones adicionales para personalizar el diseño y el comportamiento del documento. Visite [https://texdoc.org/pkg/koma-script](https://texdoc.org/pkg/koma-script) para consultar el manual.

Como se han mencionado los encabezados de página, explorémoslos ahora.

---

### Diseño de encabezados y pies de página

Cuando probamos la versión inicial de nuestro ejemplo, es posible que haya notado que, excepto en la primera página del capítulo, todas las demás páginas mostraban el número de página, el título del capítulo y el título de la sección en sus encabezados. Así, en nuestro diseño a doble cara, en la página 2, en el encabezado de una página izquierda, el número de página está en el margen exterior; aquí, en el lado izquierdo:

> **Figura 3.3** – El encabezado de la página 2

Por el contrario, así es como se ve el encabezado de nuestra página derecha en la página 3, con el número de página en el margen exterior, que ahora está en el lado derecho:

> **Figura 3.4** – El encabezado de la página 3

En un diseño a una sola cara, no habría tal diferencia en el diseño del encabezado; seguiría un estilo uniforme. Los encabezados en un diseño a una sola cara son como en la Figura 3.4. De forma predeterminada, el texto del encabezado está en el lado izquierdo y el número de página en el lado derecho.

Aunque estos encabezados estándar ya son bastante adecuados, podemos personalizarlos aún más para que se adapten mejor a nuestras preferencias.

La forma predeterminada de los encabezados de página es inclinada (*slanted*). Además, están escritos en letras mayúsculas. Usaremos tipografía en negrita en su lugar y usaremos una fuente en versalitas (*small-caps*) para el título del capítulo. Cargaremos el paquete `fancyhdr` y usaremos sus comandos para lograrlo:

1. Cargue el primer ejemplo de este capítulo.
2. Inserte las líneas destacadas para obtener esto:

```latex
\documentclass[a4paper,12pt]{book}
\usepackage[english]{babel}
\usepackage{blindtext}
\usepackage{fancyhdr}
\fancyhf{}
\fancyhead[LE]{\scshape\nouppercase{\leftmark}}
\fancyhead[RO]{\nouppercase{\rightmark}}
\fancyfoot[LE,RO]{\thepage}
\pagestyle{fancy}
\begin{document}
\chapter{Exploring the page layout}
In this chapter we will study the layout of pages.
\section{Some filler text}
\blindtext
\section{A lot more filler text}
More dummy text will follow.
\subsection{Plenty of filler text}
\blindtext[10]
\end{document}
```

3. Compile el código. Los pies de página contendrán el número de página en su lado exterior.
4. El encabezado de una página de la derecha ahora se ve de la siguiente manera:

> **Figura 3.5** – El nuevo encabezado de la página 2

5. El encabezado de una página de la izquierda ahora se ve así:

> **Figura 3.6** – El nuevo encabezado de la página 3

Usamos el paquete `fancyhdr` para personalizar los encabezados y pies de página de nuestro documento. Los nombres de los comandos del paquete comienzan con `\fancy`. Nuestra primera acción fue llamar a `\fancyhf{}`; este comando borra los encabezados y pies de página. Además, utilizamos los siguientes comandos:

- `\leftmark`: Almacena el título del capítulo junto con el número del capítulo. Se utilizan letras mayúsculas de forma predeterminada.
- `\rightmark`: Almacena el título de la sección junto con su número. También se utilizan letras mayúsculas.
- `\nouppercase`: Este comando evita el paso automático a mayúsculas en su argumento.
- `\scshape`: Cambiamos a una fuente en versalitas (*small-caps*).

Usamos el comando `\fancyhead` con el argumento opcional `LE` para colocar el título del capítulo en el encabezado. `LE` significa *left-even* (izquierda-par) y significa que este título de capítulo se colocará en el lado izquierdo del encabezado en las páginas de números pares.

Por el contrario, llamamos al comando `\fancyhead` con `RO` para poner el título de la sección en el encabezado. `RO` significa *right-odd* (derecha-impar) y significa que este encabezado de sección se mostrará en el lado derecho del encabezado en las páginas de números impares.

Posteriormente, usamos `\fancyfoot` para mostrar el número de página en el pie de página. Esta vez, usamos `LE` y `RO`, que mostraron el número de página tanto en páginas pares como impares, siempre en el lado exterior. Luego, el comando `\thepage` imprime el número de página.

Todos estos comandos se utilizan para modificar un estilo de página proporcionado por `fancyhdr`; este estilo se llama `fancy`. Tuvimos que indicarle a LaTeX que use este estilo, y lo hicimos mediante el comando `\pagestyle{fancy}`.

Enfatizar escribiendo todas las letras en mayúsculas, como lo hace `fancyhdr` de forma predeterminada, se denomina *all caps*. Se considera ampliamente un estilo cuestionable. Por eso cambiamos a versalitas.

Existen diferentes estilos de encabezados y pies de página. Esa combinación se denomina **estilo de página** (*page style*). Veamos qué estilos de página están disponibles.

#### Comprensión de los estilos de página

LaTeX y sus clases base ofrecen cuatro estilos de página integrados:

- `empty`: No se muestra ni encabezado ni pie de página.
- `plain`: Sin encabezado. El número de página se imprimirá y centrará en el pie de página.
- `headings`: El encabezado contiene títulos de capítulos, secciones y/o subsecciones, según la clase, así como el número de página. El pie de página permanece vacío.
- `myheadings`: El encabezado contiene texto definido por el usuario y el número de página; el pie de página está vacío.

El paquete `fancyhdr` introduce un potente estilo de página llamado `fancy`, que permite a los usuarios personalizar tanto el encabezado como el pie de página.

Se pueden utilizar los siguientes dos comandos para elegir el estilo de página:

- `\pagestyle{name}`: Cambia al estilo de página `name` a partir de este punto en adelante.
- `\thispagestyle{name}`: Aplica el estilo de página `name` solo a la página actual; las páginas siguientes conservarán el estilo utilizado anteriormente.

Habrá notado que el estilo de la página cambia donde comienza un capítulo, difiriendo del estilo de otras páginas. Dichas páginas tendrán un estilo `plain`. Si cree que todas las páginas deben usar el mismo estilo, considere algunos libros: es muy común que los comienzos de los capítulos difieran en estilo. Por lo general, tienen un encabezado en blanco. El comando `\thispagestyle` se puede utilizar para anular eso.

Podemos modificar el contenido y el posicionamiento en encabezados y pies de página, como veremos a continuación.

#### Personalización de encabezados y pies de página

LaTeX divide tanto los encabezados como los pies de página en tres partes: izquierda, centro y derecha (`l`, `c` y `r`, respectivamente). Puede personalizar cada parte utilizando los siguientes comandos:

- Para el encabezado: `\lhead`, `\chead` o `\rhead`
- Para el pie de página: `\lfoot`, `\cfoot` o `\rfoot`

Cada uno de estos comandos requiere un argumento obligatorio, como `\chead{User's guide}` o `\cfoot{\thepage}`. Este argumento se colocará en el área correspondiente de la página.

Alternativamente, podría utilizar estos comandos versátiles:

- Encabezado: `\fancyhead[code]{text}`
- Pie de página: `\fancyfoot[code]{text}`

Aquí, `code` puede consistir en una o más letras:

- `L`: Izquierda (*Left*)
- `C`: Centro (*Center*)
- `R`: Derecha (*Right*)
- `E`: Página par (*Even page*)
- `O`: Página impar (*Odd page*)

No importa si elegimos letras mayúsculas o minúsculas. Ya utilizamos tales combinaciones en nuestro ejemplo.

Otra personalización es modificar la línea de separación entre el texto y el pie de página, a continuación.

#### Uso de líneas decorativas en encabezados o pies de página

Podemos añadir y ajustar líneas entre el encabezado y el cuerpo del texto, y el cuerpo del texto y el pie de página, respectivamente, con estos dos comandos:

```latex
\renewcommand{\headrulewidth}{width}
\renewcommand{\footrulewidth}{width}
```

Aquí, `width` puede ser un valor como `1pt`, `0.5mm`, etc. El valor predeterminado es `0.4pt` para la línea del encabezado y `0pt` para la línea del pie de página. `0pt` significa que una línea no es visible.

Mientras que `\newcommand` define un nuevo comando, `\renewcommand` reescribe un comando existente. Incidentalmente, hemos conocido un nuevo concepto: muchos comandos de LaTeX se pueden redefinir de esta manera. Esto puede ser simplemente cambiar un valor, como aquí, o redefinir el código de un comando.

#### Modificación de las marcas de encabezado de LaTeX

Como ya sabemos, las clases y paquetes de LaTeX almacenan automáticamente los números y encabezados de sección en las macros `\leftmark` y `\rightmark`. Se hará cuando llamemos a `\chapter`, `\section` o `\subsection`. Por lo tanto, podríamos simplemente usar `\leftmark` y `\rightmark` en los argumentos de los comandos de `fancyhdr`.

A veces es posible que necesitemos actualizar manualmente esas entradas, incluso si confiamos en esta automatización. Por ejemplo, los comandos de sección con asterisco como `\chapter*` y `\section*` no producirán una entrada de encabezado, como se indicó anteriormente. En tal caso, dos comandos nos ayudarán:

- `\markright{right head}` establece el encabezado derecho
- `\markboth{left head}{right head}` establece tanto el encabezado izquierdo como el derecho

El estilo de encabezados predeterminado `headings` es fácil de usar y da buenos resultados. `myheadings` se puede usar junto con `\markright` y `\markboth`. Sin embargo, la forma más flexible la proporciona `fancyhdr`, especialmente en combinación con `\markright` y `\markboth`.

Una muy buena alternativa a `fancyhdr` es el paquete llamado `scrpage-scrlayer`. Pertenece a `KOMA-Script`, pero `scrpage-scrlayer` también funciona con otras clases. Proporciona una funcionalidad similar y ofrece aún más funciones.

El pie de página es un buen lugar para añadir notas. Veamos cómo hacer eso en la siguiente sección.

---

### Adición de notas al pie

Como se mencionó brevemente en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*, LaTeX proporciona un comando para componer notas al pie. Veámoslo en acción.

Volvamos al primer ejemplo de este capítulo. Insertaremos una nota al pie en el cuerpo del texto y una en un encabezado de sección:

1. Modifique el ejemplo insertando una nota al pie, como se muestra en la línea destacada:

```latex
\documentclass[a4paper,12pt]{book}
\usepackage[english]{babel}
\usepackage{blindtext}
\begin{document}
\chapter{Exploring the page layout}
In this chapter we will study the layout of pages.
\section{Some filler text}
\blindtext
\section{A lot more filler text}
More dummy text\footnote{serving as a placeholder} will follow.
\subsection{Plenty of filler text}
\blindtext[10]
\end{document}
```

2. Compile el código para ver cómo se ve la nota al pie en la impresión:

> **Figura 3.7** – Texto con una nota al pie

El comando `\footnote{text}` colocó un número en superíndice en la posición actual.

Además, imprime el texto de su argumento en la parte inferior de la página, marcado por el mismo número. Como hemos visto, dichas notas están separadas del texto principal por una línea horizontal.

`\footnote[number]{text}` produce una nota al pie marcada por este número opcional, un número entero. Si no damos el número opcional, se incrementará y se utilizará un contador interno. Esto se hará automáticamente; no tenemos que preocuparnos.

Dos comandos adicionales nos ayudan a colocar selectivamente solo una marca o texto de nota al pie:

- `\footnotemark[number]` produce un número en superíndice en el texto como una marca de nota al pie. Si no se da el argumento opcional, también incrementa y utiliza el contador interno de notas al pie. No se generará ningún texto de nota al pie.
- `\footnotetext[number]{text}` genera texto de nota al pie sin colocar una marca de nota al pie en el texto, y no incrementa el contador interno de notas al pie.

Establezca un comando de nota al pie justo después del texto relacionado. No deje un espacio en el medio; de lo contrario, obtendría un espacio entre el texto y la marca de nota al pie siguiente.

En la Figura 3.7, vimos una línea que separa las notas al pie del texto. Ahora veremos cómo ajustar esa línea.

#### Modificación de la línea de nota al pie

La línea que separa las notas al pie del texto es producida por el comando `\footnoterule`. Si deseamos omitir esa línea o modificarla, debemos redefinirla. Aprendimos sobre `\renewcommand` anteriormente, así que usémoslo.

Usaremos `\renewcommand` para anular el comando `\footnoterule` predeterminado:

1. Tome el ejemplo anterior y agregue las siguientes líneas al preámbulo:

```latex
\renewcommand{\footnoterule}
  {\noindent\smash{\rule[3pt]{\textwidth}{0.4pt}}}
```

2. Haga clic en **Typeset** para compilar y vea cómo ha cambiado la línea:

> **Figura 3.8** – Una línea de nota al pie modificada

El comando `\footnoterule` existente será reemplazado por la nueva definición que escribimos en la segunda línea del primer paso. El comando `\rule[raising]{width}{height}` dibuja una línea, aquí de 0.4 pt de grosor, y tan ancha como el texto, elevada un poco, en 3 pt. A través del comando `\smash`, hacemos que nuestra línea pretenda tener una altura y profundidad de cero, por lo que no ocupa ningún espacio vertical. De esta manera, el equilibrio de la página no se verá afectado. Ya conoce `\noindent`, que evita la sangría del párrafo.

Si desea omitir esa línea de nota al pie por completo, solo necesita escribir lo siguiente:

```latex
\renewcommand{\footnoterule}{}
```

Ahora, el comando está definido para no hacer nada y no obtendremos una línea divisoria.

#### Uso de paquetes para ampliar los estilos de notas al pie

Existen diferentes hábitos para configurar notas al pie. Algunos estilos requieren notas al pie numeradas por página; es posible que deban colocarse en el documento como las llamadas notas finales (*endnotes*), y se pueden usar símbolos en lugar de números. Existen más exigencias y, por tanto, se han desarrollado varios paquetes para cumplirlas. He aquí una selección:

- `endnotes`: Coloca notas al pie al final del documento.
- `manyfoot`: Permite notas al pie anidadas.
- `bigfoot`: Reemplaza y amplía `manyfoot` y mejora el manejo de saltos de página con notas al pie.
- `savefnmark`: Útil cuando necesita utilizar notas al pie varias veces.
- `footmisc`: Un paquete polivalente; introduce numeración por página, puede ahorrar espacio cuando se utilizan muchas notas al pie cortas, ofrece símbolos en lugar de números como marcas de notas al pie y proporciona sangría francesa (*hanging indentation*) y otros estilos.

Eche关 un vistazo a la documentación del paquete correspondiente para obtener más información utilizando el comando `texdoc`, como se explicó en el [Capítulo 1](https://subscription.packtpub.com/book/business-and-other/9781805804574/1), *Primeros pasos con LaTeX*, o en [https://texdoc.org](https://texdoc.org/).

Como hemos hablado de las notas al pie al final de una página, veamos cómo forzar el final de una página nosotros mismos en caso de que no queramos dejar que suceda automáticamente.

---

### Gestión de saltos de página

Como ha visto en nuestro ejemplo, el propio LaTeX maneja el salto de página. Puede haber ocasiones en las que queramos insertar un salto de página nosotros mismos antes de que lo haga LaTeX. LaTeX ofrece varios comandos para lograr esto, con o sin equilibrio vertical.

Ahora volveremos a la primera versión de nuestro ejemplo e insertaremos manualmente un salto de página justo antes de la subsección 1.2.1:

1. Inserte la línea destacada en nuestro ejemplo, que contiene el comando `\pagebreak`:

```latex
\documentclass[a4paper,12pt]{book}
\usepackage[english]{babel}
\usepackage{blindtext}
\begin{document}
\chapter{Exploring the page layout}
In this chapter we will study the layout of pages.
\section{Some filler text}
\blindtext
\section{A lot more filler text}
More dummy text will follow.
\pagebreak
\subsection{Plenty of filler text}
\blindtext[10]
\end{document}
```

2. Compile el código y eche un vistazo al resultado:

> **Figura 3.9** – Una página estirada

3. Reemplace `\pagebreak` con `\newpage`.
4. Compile de nuevo y compare:

> **Figura 3.10** – Una página no estirada

Al principio, insertamos el comando `\pagebreak`; como su nombre indica, provoca un salto de página. Además, el texto se ha estirado para llenar la página hasta el final. Eso puede ser deseable para tener la misma altura de texto en todas las páginas.

Posteriormente, debido al espacio en blanco obviamente desagradable entre los párrafos y los encabezados, reemplazamos `\pagebreak` por `\newpage`. Este comando también corta la página, pero no estira el texto: el espacio restante de la página permanecerá vacío.

Por lo tanto, `\pagebreak` se comporta como `\linebreak` y `\newpage` funciona como `\newline` (para páginas en lugar de líneas). Incluso hay un comando `\nopagebreak` que es análogo a `\nolinebreak` y prohíbe el salto de página. `\pagebreak` no romperá una línea, mientras que `\nopagebreak` no se refiere a la mitad de una línea; ambos comandos se aplican al final de la línea actual. Por supuesto, tienen un efecto inmediato cuando se usan entre párrafos.

Si utiliza el formato de dos columnas, tanto `\pagebreak` como `\newpage` comenzarán en una nueva columna en lugar de en una nueva página.

Hay dos variantes adicionales: `\clearpage` funciona como `\newpage`, excepto que comenzará en una página nueva, incluso en modo de dos columnas. `\cleardoublepage` hace lo mismo pero hace que el siguiente texto comience en una página de la derecha, insertando una página en blanco si es necesario. Esto último es útil para documentos a doble cara.

Más importante aún, ambos comandos hacen que todas las figuras y tablas que LaTeX tiene en su memoria se impriman inmediatamente.

`\pagebreak` y `\nopagebreak` pueden tomar un argumento opcional que solicita un cierto salto de línea, de la siguiente manera. El argumento es un número entero entre 0 y 4. Aquí, 0 significa que se permite un salto de página, 1 significa que es deseado, 2 y 3 marcan solicitudes más insistentes para que LaTeX intente más estirar el texto para llegar al fondo de la página, y 4 forzará un salto de página. `\pagebreak` y `\nopagebreak` son muy similares al par de comandos `\linebreak` y `\nolinebreak`, que vimos en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*.

Dichos saltos de página manuales reducen la cantidad de texto que cabe en la página. Examinemos ahora lo contrario: añadir más texto a una página.

---

### Ampliación de una página

Puede haber ocasiones en las que deseemos agregar un poco más de texto a una página, incluso si se comprime un poco o aumenta la altura del texto. Hay un comando que nos ayudará: `\enlargethispage`.

Modificaremos nuestro ejemplo ligeramente. Esta vez, intentaremos evitar una página casi vacía comprimiendo el texto en la página anterior:

1. Elimine el comando `\newpage` de nuestro ejemplo y cambie a una fuente base de 11 pt. Esta vez, use menos texto de relleno en la subsección:

```latex
\documentclass[a4paper,11pt]{book}
\usepackage[english]{babel}
\usepackage{blindtext}
\usepackage[a4paper, inner=1.5cm, outer=3cm, top=2cm, bottom=3cm, bindingoffset=1cm]{geometry}
\begin{document}
\chapter{Exploring the page layout}
In this chapter we will study the layout of pages.
\section{Some filler text}
\blindtext
\section{A lot more filler text}
More dummy text will follow.
\subsection{Plenty of filler text}
\blindtext[3]
\end{document}
```

2. Compile, y el resultado consistirá en dos páginas. Esta es la primera página:

> **Figura 3.11** – Una página completamente llena

Y este es el texto en la segunda página:

> **Figura 3.12** – Texto restante en la segunda página

3. Inserte este comando justo después de la línea `\subsection`:

```latex
\enlargethispage{\baselineskip}
```

4. Compile nuevamente, y ahora nuestro documento cabe en una sola página:

> **Figura 3.13** – Todo el texto cabe en una sola página

Usamos el comando `\enlargethispage` para comprimir más texto en una página. Este comando toma la altura adicional solicitada como argumento. El comando `\baselineskip` devuelve la altura de una línea de texto que usamos como argumento. Por lo tanto, LaTeX pudo colocar una línea adicional en la página, e incluso la línea restante encajó también porque LaTeX comprimió algo de espacio en blanco.

Podríamos usar factores: escriba `\enlargethispage{2\baselineskip}` para obtener dos líneas más en una página. Ni siquiera necesita ser un valor entero. Como siempre, al indicar una longitud, puede utilizar otras unidades, como `10pt`, `0.5in`, `1cm` o `5mm`, e incluso valores negativos.

Solo la página actual se verá afectada por este comando. Hay una versión con asterisco: `\enlargethispage*` encogería adicionalmente todos los espacios verticales de la página a su mínimo.

Sin embargo, `\enlargethispage` debe considerarse solo como una posible solución fácil cuando necesita colocar rápidamente más texto en una sola página. En general, podemos ajustar la cantidad de texto en la página cambiando los márgenes, como ya sabemos, o ajustando el interlineado dentro del texto. Examinemos el interlineado en la siguiente sección.

---

### Cambio del interlineado

Sin algo de espacio vertical entre las líneas, la legibilidad de nuestro texto podría verse afectada. Añadir dicho espacio ayudaría a guiar el ojo a lo largo de la línea. Aunque LaTeX ya garantiza una buena legibilidad al elegir un interlineado significativo, los editores pueden requerir un espaciado diferente.

Modificaremos el primer ejemplo de este capítulo añadiendo media altura de línea al interlineado:

1. Amplíe el preámbulo de nuestro ejemplo con este comando:

```latex
\usepackage[onehalfspacing]{setspace}
```

2. Compile el código para ver el cambio:

> **Figura 3.14** – Interlineado adicional

Cargamos el paquete `setspace` para ajustar el interlineado. Proporcionamos la opción `onehalfspacing`, que aumenta el espaciado en la mitad de una altura de línea para todo el documento.

El paquete `setspace` entiende tres opciones:

- `singlespacing` es el valor predeterminado. No se insertará ningún espacio adicional. El texto se compondrá con el interlineado predeterminado de LaTeX, que es aproximadamente el 20 por ciento de la altura de la línea.
- `onehalfspacing` significa espaciado de uno y medio, como puede ver en nuestro ejemplo.
- `doublespacing` se puede utilizar para obtener aún más espacio; la distancia entre las líneas de base de líneas de texto sucesivas sería el doble de alta que una sola línea.

En la jerga de los tipógrafos, la distancia entre las líneas de base de líneas de texto consecutivas se denomina **interlínea** o *leading* (pronunciado "ledding", del metal plomo (*lead*), utilizado antiguamente para separar líneas).

Ahora que hemos ajustado el espaciado vertical y los saltos de página, veamos cómo alinear verticalmente el área de texto en las páginas.

---

### Alineación de la altura del área de texto

Revisemos la Figura 3.9. Mostraba una página donde el texto aparecía estirado: se había insertado espacio vertical adicional entre párrafos y encabezados. Este comportamiento es típico de la clase de documento `book`: en diseños a doble cara, LaTeX alinea el bloque de texto verticalmente para que las páginas enfrentadas tengan la misma altura.

Si bien este equilibrio pretende ser visualmente agradable, a veces puede generar un espaciado incómodo, especialmente si la página contiene poco texto. En tales casos, es posible que prefiera desactivar esta alineación.

LaTeX ofrece dos comandos para controlar la alineación vertical del texto:

- `\raggedbottom` desactiva la alineación vertical, por lo que obtiene menos estiramiento y una altura de página natural.
- `\flushbottom` impone la misma altura de texto en cada página, por lo que LaTeX estira el contenido si es necesario.

Estos comandos se colocan normalmente en el preámbulo para un diseño coherente en todo el documento. Sin embargo, también se pueden utilizar selectivamente dentro del documento para cambiar de estilo cuando sea necesario.

He aquí una directriz práctica:

- Utilice `\flushbottom` para documentos a doble cara ricos en texto, como libros, para lograr una apariencia visual perfecta cuando se abre el libro. Ese es el valor predeterminado con la clase `book`.
- Utilice `\raggedbottom` cuando su contenido varíe en densidad, como cuando tiene muchas figuras y tablas y nota un espaciado no deseado. Ese es el valor predeterminado en las clases de documentos a una sola cara, como `article`, `report`, `letter` y las clases de presentación.

Ahora que hemos terminado de diseñar todo el documento, agreguemos una tabla de contenidos.

---

### Creación de una tabla de contenidos

Un libro suele comenzar con una tabla de contenidos, así que creemos una basada en nuestros encabezados numerados:

1. En nuestro documento anterior, eliminemos las opciones `landscape` y `twocolumn`.
2. Elimine el paquete `setspace`, es decir, elimine esta línea:

```latex
\usepackage[onehalfspacing]{setspace}
```

3. Agregue el comando `\tableofcontents` justo después de `\begin{document}`.

Nuestro código ahora debería verse así:

```latex
\documentclass[a4paper,12pt]{book}
\usepackage[english]{babel}
\usepackage{blindtext}
\usepackage[a4paper, inner=1.5cm, outer=3cm, top=2cm, bottom=3cm, bindingoffset=1cm]{geometry}
\begin{document}
\tableofcontents
\chapter{Exploring the page layout}
In this chapter we will study the layout of pages.
\section{Some filler text}
\blindtext
\section{A lot more filler text}
More dummy text will follow.
\subsection{Plenty of filler text}
\blindtext[10]
\end{document}
```

4. Compile el código dos veces. Después, la primera página de su salida contendrá esta tabla:

> **Figura 3.15** – Tabla de contenidos

El comando `\tableofcontents` le dice a LaTeX que produzca e imprima una tabla de contenidos. Durante una ejecución de composición tipográfica, LaTeX escribe los encabezados en un archivo auxiliar con la extensión de archivo `.toc`. El comando `\tableofcontents` lee ese archivo `.toc` para imprimir la tabla de contenidos.

El proceso de composición tipográfica de LaTeX es lineal; se ejecuta desde el principio hasta el final del código. El comando `\tableofcontents` viene al principio y los encabezados vienen después. Por eso tuvimos que componer tipográficamente dos veces:

1. En la primera ejecución, `\tableofcontents` no conocía ningún encabezado y la tabla de contenidos permaneció vacía. Mientras continuaba ejecutándose, LaTeX colocó los encabezados en el archivo `.toc`.
2. En la segunda ejecución, `\tableofcontents` encontró y leyó el archivo `.toc` para imprimir el contenido.

Es bueno tener esto en cuenta para más adelante: cuando cambia un encabezado y compila el documento, puede ver el cambio en el texto. Pero la tabla de contenidos obtendrá este cambio en la siguiente ejecución del compilador.

Los comandos de sección crean las entradas de la tabla de contenidos. Usamos `\chapter`, `\section` y `\subsection`, y obtuvimos una entrada para cada uno.

Un encabezado puede ser muy largo; podría abarcar dos o más líneas. En ese caso, podríamos desear acortar su entrada correspondiente en la tabla de contenidos. Veamos cómo.

Podemos usar los argumentos opcionales de los comandos de sección para producir entradas más cortas, diferentes de los encabezados reales. Editemos el ejemplo mostrado en la Figura 3.15 insertando títulos más cortos entre corchetes:

```latex
\chapter[Page layout]{Exploring the page layout}
\section[Filler text]{Some filler text}
\section[More]{A lot more filler text}
\subsection[Plenty]{Plenty of filler text}
```

Compile el ejemplo dos veces. Verá que los encabezados siguen siendo los mismos, pero la tabla de contenidos ha cambiado:

> **Figura 3.16** – Entradas de tabla de contenidos abreviadas

Además del argumento obligatorio que produce el encabezado, cada comando de sección entiende un argumento opcional. Si se proporciona un argumento opcional, se utilizará en lugar del encabezado obligatorio para la entrada de la tabla de contenidos.

En el [Capítulo 8](https://subscription.packtpub.com/book/business-and-other/9781805804574/8), *Gestión de contenidos, índices y bibliografía*, examinaremos esto con más detalle y aprenderemos cómo personalizar aún más la tabla de contenidos. Revisemos nuevamente los comandos de sección para las clases `book`, `report` y `article`. Hay siete niveles en esas clases base:

- `\part`: Esto sirve para dividir el documento en unidades principales. La numeración de otras unidades seccionales es independiente de `\part`. Un encabezado de parte utilizará una página entera en documentos `book` y `report`.
- `\chapter`: Esto proporciona un encabezado grande que comenzará en una página nueva, disponible en la clase `book` y en la clase `report`.
- `\section`, `\subsection` y `\subsubsection`: Proporcionan encabezados en negrita y están disponibles en las tres clases.
- `\paragraph` y `\subparagraph`: También disponibles en las tres clases, producen un encabezado integrado (*run-in heading*). Eso significa que el encabezado se extiende directamente en el texto; no hay salto de línea entre el encabezado y el texto siguiente. Además, es un comando de sección y no debe confundirse con los párrafos de texto comunes.

Excepto `\part`, todos los comandos de sección reinician el contador de la sección que está un nivel por debajo en la jerarquía. Por ejemplo, `\chapter` reinicia el contador de sección. De esta manera, las secciones se numerarán por capítulo.

En resumen, estos comandos de sección son fáciles de usar y hacen mucho:

- `\part` y `\chapter` provocan un salto de página antes del encabezado
- Todos generan un número y una presentación para él, algunos dependiendo de los contadores de nivel superior (por ejemplo, la Sección 1 del [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2) generaría 2.1)
- Excepto `\part`, restablecen el contador de la unidad seccional del siguiente nivel para que la unidad del nivel inferior comience con 1
- Producen una entrada en la tabla de contenidos
- Dan formato al encabezado, generalmente en negrita, y cuanto más grande es, más alto está en la jerarquía
- Guardan encabezados internamente para usarlos en el encabezado de una página

Todos los comandos de sección proporcionan una forma con asterisco, de la siguiente manera:

```latex
\section*{title}
```

Si utiliza este formato, la numeración se suprimirá y no habrá ninguna entrada en la tabla de contenidos ni en el encabezado de página. Mire el encabezado *Contents* en nuestro ejemplo; en realidad, se compuso mediante `\chapter*` dentro de la macro `\tableofcontents`.

---

### Resumen

En este capítulo, aprendimos cómo diseñar el diseño general de un documento.

Específicamente, cubrimos la elección de dimensiones de página, márgenes y orientación. Sabemos cómo cambiar a un diseño de dos columnas y cómo ajustar el interlineado. Además, ahora podemos personalizar encabezados y pies de página, añadir notas al pie e incluir una tabla de contenidos en nuestro documento.

Más allá del diseño, cubrimos algunos temas generales, como cambiar las propiedades del documento seleccionando opciones de clase de documento y opciones de paquete, así como redefinir comandos existentes.

Ahora que hemos establecido las bases, es hora de estructurar el contenido en sí. En el próximo capítulo, aprenderemos a crear listas para presentar información de manera clara y organizada.
