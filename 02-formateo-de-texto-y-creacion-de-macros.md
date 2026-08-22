# LaTeX Beginner's Guide
## Capítulo 2: Formateo de Texto y Creación de Macros

En el capítulo anterior, instalamos LaTeX y escribimos nuestro primer documento utilizando tanto el editor TeXworks como Overleaf. Ahora, analizaremos más de cerca la estructura del texto, centrándonos en el formato y en el ajuste fino de los detalles.

En este capítulo, cubriremos lo siguiente:

- Uso del formato lógico
- Comprensión de cómo LaTeX procesa su entrada
- Modificación de fuentes de texto
- Uso del color
- Limitación del ancho de párrafo
- Saltos de línea y párrafos
- Cambio de alineación del texto
- Visualización de citas
- Creación de comandos
- Creación de entornos
- Uso de una sintaxis alternativa

A través de ejemplos prácticos y experimentando con las características, aprenderá algunos conceptos esenciales de LaTeX. Al final de este capítulo, se sentirá cómodo trabajando con comandos y entornos y será capaz de definir comandos personalizados.

Recuerde que puede editar y compilar todos los ejemplos en línea en la página web del libro. El código de este capítulo se puede encontrar en [https://latexguide.org/chapter-02](https://latexguide.org/chapter-02) y en el proyecto de GitHub del libro.

A medida que comience a trabajar más ampliamente, es posible que ocasionalmente encuentre mensajes de error. Si eso sucede, consulte el [Capítulo 14](https://subscription.packtpub.com/book/business-other/9781805804574/14), *Resolución de problemas*, para obtener orientación y posibles soluciones.

---

### Uso del formato lógico

Dentro de un documento LaTeX, debemos evitar aplicar formato físico, como poner palabras en negrita o cursiva o elegir diferentes tamaños de fuente. En su lugar, debemos utilizar el formato lógico, como declarar un título y el autor, y luego asignar un encabezado de sección. LaTeX se encarga de la apariencia visual, como imprimir el título en un tamaño de fuente grande y mostrar los encabezados de sección en negrita.

En algunos ejemplos más adelante en este capítulo, utilizaremos comandos de formato físico, como poner palabras en negrita o cursiva. Sin embargo, eso es para practicar con los comandos de fuente. El objetivo final es definir nuestros propios comandos lógicos utilizando comandos de fuente.

En un buen documento LaTeX, el formato físico solo se utilizaría dentro de la definición de comandos de formato lógico. Si necesita un estilo específico, como para resaltar palabras clave, puede definir un comando lógico para ello en el preámbulo del documento. Luego, a lo largo del cuerpo de su documento, solo utilizará ese comando lógico. Esto garantiza un formato coherente en todo el texto. Siempre que cambie de opinión sobre los detalles de formato, puede modificar los comandos lógicos en el preámbulo; sin necesidad de revisar todo el documento.

Para comenzar, examinemos un breve ejemplo que ilustra la estructura típica de un documento.

#### Creación de un documento con título y encabezado

Construyamos un ejemplo breve que utilice algún formato básico. El documento incluirá un título, el nombre del autor, la fecha, un encabezado de sección y algo de texto normal.

Siga estos pasos:

1. Escriba el siguiente código en su editor para comenzar un documento pequeño:

```latex
\documentclass[a4paper,11pt]{article}
```

2. Especifique el título, el autor y la fecha:

```latex
\title{Example 2}
\author{My name}
\date{May 5, 2021}
```

3. Comience el documento:

```latex
\begin{document}
```

4. Deje que LaTeX imprima el título completo, que incluirá el autor y la fecha:

```latex
\maketitle
```

5. Agregue un encabezado de sección y escriba algo de texto, luego finalice el documento:

```latex
\section{What's this?}
This is our second document. It contains a title and a section with text.
\end{document}
```

6. Guarde el documento haciendo clic en el botón **Save** (o presionando `Ctrl + S`). Asígnele un nombre, como `example2.tex`.
7. Compile el documento haciendo clic en el botón **Typeset** (o presionando `Ctrl + T`); esto convierte su código en un archivo PDF.
8. Vea la salida:

> **Figura 2.1** – Texto con un encabezado

En el editor TeXworks, la vista previa en PDF aparece automáticamente después de presionar el botón *Typeset*. Al mismo tiempo, se crea un archivo PDF. En este caso, se llama `example2.pdf` y se almacena en la misma carpeta que su archivo de código original, `example2.tex`.

En el primer capítulo, hablamos sobre el formato lógico; veamos ahora este ejemplo con eso en mente. Esto es lo que le dijimos a LaTeX:

- El tipo de documento es `article` y se imprimirá en papel A4 con un tamaño de fuente base de 11 puntos
- El título del documento es *Example 2*
- El documento muestra el nombre del autor
- La fecha del documento está establecida en *May 5, 2021*

En cuanto al contenido del documento, declaramos lo siguiente:

- El documento comienza con un título
- La primera sección se titula *What's this?*
- La sección contiene el siguiente texto: *This is our second document. It contains a title and a section with text.*

Observe que no elegimos el tamaño de fuente del título o del encabezado de sección, ni pusimos nada en negrita o centrado. LaTeX maneja todo ese formato. No obstante, usted es libre de personalizar la apariencia de las cosas.

Una vez que haya guardado un documento, no es necesario volver a presionar el botón *Save*. TeXworks lo guarda automáticamente cada vez que hace clic en el botón *Typeset*.

#### Exploración de la estructura del documento

Echemos un vistazo más de cerca al ejemplo que acabamos de crear. Un documento LaTeX no existe de forma aislada; normalmente, se basa en una plantilla reutilizable llamada clase. Una clase proporciona una estructura general, junto con características personalizables, típicamente adaptadas a un propósito específico. Hay clases para varios tipos de materiales, incluidos libros, artículos de revistas, cartas, presentaciones y pósteres. Encontrará cientos de clases confiables en archivos en línea e incluso en su computadora después de haber instalado TeX Live. En nuestro ejemplo, elegimos la clase `article`, una clase estándar de LaTeX muy adecuada para documentos más cortos.

La primera línea comienza con `\documentclass`. Esta palabra comienza con una barra invertida; dicha palabra se llama comando o macro. Ya hemos utilizado algunos comandos de este tipo para especificar la clase y declarar los metadatos del documento en nuestro primer ejemplo en este capítulo: `\title`, `\author` y `\date`. Estos comandos almacenan las propiedades; no producen una salida visible.

La primera parte del documento se llama **preámbulo** (*preamble*). Aquí es donde elegimos la clase, especificamos propiedades y, en general, realizamos definiciones para todo el documento.

`\begin{document}` marca el final del preámbulo y el comienzo del documento real. `\end{document}` marca el final del documento. Cualquier cosa que siga sería ignorada por LaTeX. Generalmente, una pieza de código de este tipo enmarcada por un par de comandos `\begin` y `\end` se denomina **entorno** (*environment*).

Dentro del entorno del documento, utilizamos el comando `\maketitle` para imprimir el título, el autor y la fecha en un diseño con un formato atractivo. Con el comando `\section`, produjimos un encabezado, más grande y en negrita que el texto estándar. Finalmente, agregamos un párrafo corto. Para que quede claro: el preámbulo nunca producirá ninguna salida. Solo se imprimirá lo que esté en el entorno `document`.

Ahora que ha visto cómo funcionan los comandos, echemos un vistazo más de cerca a la sintaxis de comandos de LaTeX.

#### Uso de comandos de LaTeX

Los comandos de LaTeX comienzan con una barra invertida, seguida de letras, generalmente en minúsculas, a veces mezcladas con mayúsculas. Por lo general, se nombran descriptivamente, aunque con excepciones: más adelante, encontrará comandos que consisten solo en una barra invertida y un único carácter especial.

Los comandos pueden tomar parámetros. Estas son opciones que determinan cómo realiza su trabajo el comando. Los valores de los parámetros pasados a los comandos se denominan **argumentos**. Los argumentos aparecen entre llaves cuando son obligatorios, o entre corchetes cuando son opcionales.

Por lo tanto, verá comandos utilizados de varias maneras, normalmente como una de estas:

```latex
\command
\command{argument}
\command[optional argument]
\command[optional argument]{argument}
\command{argument}{another argument}
```

Ve que algunos comandos pueden tomar múltiples argumentos, con cada uno de ellos encerrado entre llaves o corchetes. Veamos más de cerca cómo funciona.

Si un comando requiere un argumento por definición, ese argumento debe proporcionarse; es obligatorio, indicado por llaves. Por ejemplo, llamar a `\documentclass` sin especificar un nombre de clase no tendría sentido.

Los comandos pueden admitir argumentos sin requerirlos estrictamente, por lo que se denominan opcionales. Puede especificarlos, pero no es una obligación. Si no se proporciona un argumento opcional, el comando utilizará uno predeterminado. Encierre dichos argumentos entre corchetes.

Veamos el primer ejemplo en el [Capítulo 1](https://subscription.packtpub.com/book/business-other/9781805804574/1), *Primeros pasos con LaTeX*. Escribimos `\documentclass{article}` para elegir la clase `article`. Como omitimos un argumento opcional, este documento fue compuesto con un tamaño de fuente base de 10 puntos porque este es el tamaño de fuente base predeterminado de la clase. En el segundo documento, escribimos `\documentclass[a4paper,11pt]{article}`; aquí, anulamos los valores predeterminados, por lo que ahora el documento se ajustará para papel A4 con un tamaño de fuente base de 11 puntos.

La mayoría de los comandos de LaTeX, incluidos los que definimos nosotros mismos, constan de otros comandos. Es por eso que los comandos de LaTeX también se denominan **macros**, y los términos macro y comando se usan indistintamente. Un comando o macro que no imprime algo sino que simplemente cambia la configuración actual, como la forma de la fuente o la alineación del texto, también se llama **declaración**.

Hay un tipo de comando que aplica cambios solo dentro de un ámbito limitado, como unas pocas líneas o un bloque de código. Eso se llama un **entorno**. Veamos su sintaxis.

#### Uso de entornos de LaTeX

Los entornos de LaTeX son bloques de código que comienzan con `\begin` y terminan con `\end`. Ambos comandos requieren el nombre del entorno como argumento.

Un entorno simple puede verse así:

```latex
\begin{name} … \end{name}
```

Dichos entornos también se pueden utilizar para una declaración existente llamada `\name`, limitando el efecto del comando `\name`.

Al igual que los comandos, los entornos pueden tomar argumentos. Nuevamente, los argumentos obligatorios van entre llaves mientras que los argumentos opcionales van entre corchetes. Por lo tanto, puede encontrar un entorno escrito de esta manera:

```latex
\begin{name}{argument} … \end{name}
```

O bien, podría ver un argumento opcional adicional:

```latex
\begin{name}[optional argument]{argument} … \end{name}
```

Puede pensar en los entornos como declaraciones con un ámbito (*scope*) integrado. Cuando se llama a `\begin`, el entorno cambia algo en particular, como el diseño, la fuente u otras propiedades. Ese cambio permanece vigente hasta que se alcanza un comando `\end`, momento en el que se cancela el cambio. El impacto del entorno `name` se limita a la porción de código entre `\begin{name}` y `\end{name}`.

Además, el efecto de todas las declaraciones locales para comandos de formato utilizados dentro de un entorno también terminará cuando finalice el entorno circundante.

Ahora que hemos cubierto la sintaxis de los comandos y entornos de LaTeX, veamos cómo entiende LaTeX nuestro código.

---

### Comprensión de cómo LaTeX procesa su entrada

Antes de continuar escribiendo, veamos cómo entiende LaTeX lo que escribimos:

- Además de las letras básicas del alfabeto latino, puede escribir directamente (o copiar y pegar) caracteres acentuados, como ä, ü y ö, así como caracteres de otros idiomas, como griego o cirílico.
- Un solo espacio en el código de entrada aparece como un espacio en el documento de salida, mientras que varios espacios consecutivos se tratan como un solo espacio.
- Un salto de línea en el código fuente se trata como un espacio.
- Una línea vacía en el código fuente se trata como un salto de párrafo.

Algunos caracteres tienen significados especiales, como vio antes:

- Una barra invertida, `\`, inicia un comando de LaTeX o una macro de LaTeX.
- Las llaves y los corchetes se utilizan para los argumentos de los comandos.
- Un signo de dólar, `$`, inicia y finaliza el modo matemático, que exploraremos en el [Capítulo 9](https://subscription.packtpub.com/book/business-other/9781805804574/9), *Escritura de fórmulas matemáticas*.
- Un signo de porcentaje, `%`, le dice a LaTeX que ignore el resto de la línea.

Ampliemos ese último punto: el signo de porcentaje inicia un comentario. Todo lo que siga a un signo de porcentaje hasta el final de la línea será ignorado por LaTeX y no se imprimirá. Esto le permite insertar notas en su documento. A menudo se utiliza en plantillas de LaTeX para informar al usuario sobre lo que hace la plantilla o lo que requiere que el usuario haga en un momento determinado. Tenga en cuenta que el final de la línea, que normalmente se comporta como un espacio, también se ignorará después de un signo de porcentaje. Esa es la razón por la que a menudo se puede ver un signo `%` al final de las líneas en el código de otras personas: para evitar que el final de la línea actúe como un espacio.

Si desea deshabilitar un comando o una línea de código temporalmente, a menudo es mejor insertar un signo de porcentaje en lugar de eliminar el comando. De esa manera, podrá deshacer este cambio fácilmente simplemente eliminando el signo de porcentaje.

Si así es como funciona el signo de porcentaje, ¿qué debemos hacer si queremos escribir algo como 100% en nuestro texto? ¿Y qué pasa con los otros símbolos especiales? Averigüemos cómo manejar tales casos en la siguiente sección.

#### Impresión de símbolos especiales

La mayoría de las veces, puede simplemente escribir letras, dígitos y signos de puntuación directamente en su documento LaTeX. Sin embargo, algunos caracteres están reservados para los comandos de LaTeX y no se pueden usar tal cual en el texto. Ya hemos visto tales caracteres, como el signo de porcentaje y las llaves. Para incluir estos caracteres en su salida, LaTeX proporciona comandos especiales para imprimir dichos símbolos.

Escribamos un ejemplo muy breve que imprima una cantidad en dólares, un porcentaje y algunos otros símbolos especiales:

1. Cree un nuevo documento e introduzca las siguientes líneas:

```latex
\documentclass{article}
\begin{document}
Statement \#1: 50\% of \$100 equals \$50.
More special symbols are \&, \_, \{ and \}.
\end{document}
```

2. Haga clic en el botón **Typeset** para compilar el documento.
3. Compruebe la salida:

> **Figura 2.2** – Símbolos especiales

Al colocar una barra invertida delante de un carácter especial, lo convertimos en un comando de LaTeX. El único propósito de este comando es imprimir ese símbolo.

Quizás se pregunte cómo imprimir una barra invertida. Para hacer esto, use el comando `\textbackslash`. Dos barras invertidas consecutivas, `\\`, se utilizan como atajo para un salto de línea. Eso puede parecer un poco contraintuitivo, pero los saltos de línea ocurren con frecuencia, mientras que las barras invertidas rara vez se imprimen en la salida, por lo que se ha elegido este atajo.

Hay una gran variedad de símbolos adicionales que podemos usar para fórmulas matemáticas, notación de ajedrez, signos del zodíaco, partituras musicales y más. No necesitaremos ocuparnos de esos símbolos por ahora, pero volveremos a ese tema en el [Capítulo 9](https://subscription.packtpub.com/book/business-other/9781805804574/9), *Escritura de fórmulas matemáticas*, cuando necesitemos símbolos para componer fórmulas matemáticas.

Ahora que sabemos cómo introducir texto plano, pasemos a dar formato a nuestro texto.

---

### Modificación de fuentes de texto

LaTeX aplica algún formato automáticamente; por ejemplo, hemos visto que los encabezados de sección son más grandes que el texto normal y están en negrita. Ahora aprenderemos a cambiar la apariencia del texto nosotros mismos.

#### Ajuste de la forma de la fuente

En este ejemplo, enfatizaremos una palabra importante en nuestro texto, y veremos cómo hacer que las palabras aparezcan en negrita, cursiva o inclinadas. También descubriremos cómo resaltar palabras dentro de una sección de texto que ya está enfatizada.

Echemos un vistazo:

1. Cree un nuevo documento que contenga el siguiente código:

```latex
\documentclass{article}
\begin{document}
Text can be \emph{emphasized}.
Besides from \textit{italics}, words can be \textbf{bold}, \textsl{slanted}, or typeset in \textsc{Small Caps}.
Such commands can be \textit{\textbf{nested}}.
\emph{See how \emph{emphasizing} looks when nested.}
\end{document}
```

2. Haga clic en **Typeset** y eche un vistazo a la salida:

> **Figura 2.3** – Enfatizando frases

Al principio, usamos el comando `\emph`, pasando una palabra como argumento. Esta palabra se compondrá en cursiva porque LaTeX usa cursiva para enfatizar el texto.

La mayoría de los nombres de comandos de formato de texto siguen el patrón `\text**{argument}`, donde `**` representa una abreviatura de dos letras, como `bf` para negrita (*bold face*), `it` para cursiva (*italics*) y `sl` para inclinada (*slanted*). El texto del argumento se formateará en consecuencia. Después del comando, LaTeX continúa componiendo el texto subsiguiente en el estilo utilizado anteriormente.

Anidamos los comandos `\textit` y `\textbf` para combinar estilos, de modo que el texto aparezca tanto en cursiva como en negrita.

Vale la pena señalar que la mayoría de los comandos de fuente mostrarán el mismo efecto si se aplican repetidamente, como `\textbf{\textbf{words}}`. Aquí, las palabras seguirán teniendo el mismo estilo en negrita que con `\textbf{words}`, no más negrita.

Sin embargo, el comando `\emph` se comporta de manera diferente. Hemos visto que `\emph` cambia el texto a cursiva, pero si usamos `\emph` en un fragmento de texto que ya está en cursiva, volverá de cursiva a fuente recta (*upright*). Imagine un teorema vital compuesto completamente en cursiva y le gustaría resaltar una palabra dentro de este teorema. Esa palabra no debería estar en cursiva porque debería distinguirse del texto circundante, por lo que se formatea en una fuente recta nuevamente. En otras palabras, el comando `\emph` alterna entre fuente recta y cursiva.

Utilice los cambios de fuente con cuidado. La combinación simultánea de formas de fuente, como grande, negrita y cursiva, puede resultar visualmente abrumadora y percibirse como un estilo deficiente. Utilice los estilos de fuente disponibles con prudencia y aplíquelos de forma coherente en todo el documento.

#### Elección de la familia tipográfica

De forma predeterminada, LaTeX utiliza una fuente con serifa (*serif*), también llamada fuente romana (*Roman*). Estas fuentes tienen pequeñas líneas o trazos unidos a las letras, llamados serifas. Las fuentes sin tales serifas son fuentes sin serifa (*sans-serif*), utilizando la palabra francesa *sans*, que significa sin.

Compare las dos líneas de la Figura 2.4. Mire de cerca la primera letra T; notará claramente la diferencia entre las fuentes con serifa y sin serifa:

> **Figura 2.4** – Fuente con serifa versus fuente sin serifa

Estos diferentes tipos de fuentes se denominan **familias tipográficas** (*font families*) o tipos de letra (*typefaces*).

Otro tipo de letra disponible es el monoespaciado (*monospaced*), donde todas las letras tienen el mismo ancho. Estas fuentes también se denominan fuentes de máquina de escribir (*typewriter*).

Cambiemos de familia tipográfica en un breve documento de ejemplo. Comenzaremos con texto en negrita, pero usar texto en negrita con serifa puede parecer muy pesado. Por lo tanto, utilizaremos texto en negrita sin serifa en su lugar. El siguiente texto contendrá una dirección de Internet y elegiremos una fuente de máquina de escribir para distinguirla.

Siga estas instrucciones:

1. Cree un documento LaTeX con el siguiente código:

```latex
\documentclass{article}
\begin{document}
\textsf{\textbf{Get help on the Internet}}
\texttt{https://latex.org} is a support forum for \LaTeX.
\end{document}
```

2. Haga clic en **Typeset** y observe el resultado:

> **Figura 2.5** – Texto con una URL

Aquí nos encontramos con más comandos de fuentes. Al usar `\textsf`, hemos elegido una fuente sin serifa en la línea del encabezado, y aplicamos el comando `\texttt` para obtener una fuente de máquina de escribir para la dirección de Internet. Estos comandos funcionan igual que los comandos de fuentes que hemos visto anteriormente.

Las serifas, esos pequeños detalles decorativos en los extremos de los trazos de una letra, mejoran la legibilidad al guiar los ojos del lector a lo largo de la línea. Por eso a menudo se prefieren en libros y periódicos impresos.

Los encabezados, sin embargo, a menudo se establecen sin serifas. Las fuentes sin serifa también son una buena opción para el texto en pantalla debido a su mejor legibilidad en pantallas de menor resolución o pantallas más pequeñas, como las de los teléfonos móviles. Por esta razón, a menudo se prefieren las fuentes sin serifa para el texto en libros electrónicos, en páginas de Internet y, a menudo, para textos técnicos.

Las fuentes monoespaciadas (máquina de escribir) son ideales para mostrar el código fuente de programas informáticos, tanto en documentos impresos como en editores de texto. Como en nuestro ejemplo anterior, este libro generalmente utiliza una fuente de máquina de escribir para distinguir las direcciones de Internet y el código fuente del texto circundante.

Hasta ahora, hemos visto comandos que aplican formato al texto en el argumento entre llaves. LaTeX también ofrece comandos que no toman argumentos y funcionan como interruptores (*switches*).

Siguiendo las siguientes instrucciones, modificaremos el ejemplo anterior, esta vez utilizando comandos de cambio de familia tipográfica:

1. Edite el ejemplo anterior para obtener el siguiente código:

```latex
\documentclass{article}
\begin{document}
\sffamily\bfseries Get help on the Internet
\normalfont\ttfamily https://latex.org\normalfont\ is a support forum for \LaTeX.
\end{document}
```

2. Haga clic en **Typeset** para compilar.
3. Compare la salida con el ejemplo anterior; se ve igual.

Cambiamos a la tipografía sin serifa usando el comando `\sffamily`. El comando `\bfseries` cambió adicionalmente el texto a negrita. Usamos el comando `\normalfont` para volver a la fuente predeterminada de LaTeX y luego aplicamos el comando `\ttfamily` para cambiar a una fuente de máquina de escribir. Después de la dirección de Internet, usamos `\normalfont` nuevamente para volver a la fuente predeterminada.

Estos comandos de cambio no producen ningún resultado visible por sí mismos. Simplemente cambian la forma en que se representa el texto siguiente. Por eso también se llaman **declaraciones**.

Resumamos los comandos de fuentes y sus declaraciones correspondientes junto con sus significados:

> **Figura 2.6** – Comandos de fuentes

La declaración correspondiente al comando `\emph` es `\em`.

#### Limitación del efecto de los comandos

En el ejemplo anterior, escribimos `\normalfont` para volver a cambiar la fuente a la predeterminada de LaTeX, pero hay otra manera. Podemos usar llaves para decirle a LaTeX dónde aplicar un comando y dónde detenerlo:

1. Acorte y modifique nuestro ejemplo de formas de fuente que produjo la Figura 2.3 para obtener este código:

```latex
\documentclass{article}
\begin{document}
Besides from {\itshape italics}, words can be {\bfseries bold}, {\slshape slanted}, or typeset in {\scshape Small Caps}.
\end{document}
```

2. Haga clic en el botón **Typeset** y compruebe la salida:

> **Figura 2.7** – Uso de declaraciones para cambiar el grosor y la forma de la fuente

Cuando quisimos aplicar una declaración para cambiar la fuente, comenzamos con una llave de apertura, `{`, y dejamos que siguiera el comando de declaración de fuente. El efecto de ese comando dura hasta que se detiene mediante la llave de cierre correspondiente, `}`.

Una llave de apertura le dice a LaTeX que comience un **grupo**. Los siguientes comandos son válidos para el texto subsiguiente hasta que una llave de cierre finaliza el grupo. Los grupos también se pueden anidar. He aquí un ejemplo:

```latex
Normal text, {\sffamily sans serif text {\bfseries and bold}}.
```

El área donde un comando es válido se denomina su **ámbito** (*scope*). Debemos tener cuidado de completar cada grupo. Por cada llave de apertura, debe haber una llave de cierre coincidente; de lo contrario, LaTeX producirá un error.

Por lo tanto, en resumen, los grupos se definen mediante llaves y contienen y confinan el efecto de los comandos locales.

#### Exploración de los tamaños de fuente

Probemos todos los tamaños de fuente disponibles a través de los comandos de tamaño de fuente integrados de LaTeX:

1. Cree un documento con el siguiente código:

```latex
\documentclass{article}
\begin{document}
\tiny We \scriptsize start \footnotesize very \small small, \normalsize get \large big \Large and \LARGE bigger, \huge huge, \Huge gigantic!
\end{document}
```

2. Haga clic en **Typeset** y observe la salida:

> **Figura 2.8** – Tamaños de fuente

Utilizamos las 10 declaraciones de tamaño de fuente disponibles, comenzando en pequeño con `\tiny` y terminando con `\Huge`. No hay comandos correspondientes que tomen argumentos, por lo que si desea limitar su ámbito, tendría que usar llaves, tal como aprendimos anteriormente.

El tamaño de fuente real escala con el tamaño de fuente base de su documento. Por lo tanto, si su documento tiene un tamaño de fuente base de 12 puntos, entonces `\tiny` daría como resultado un texto más grande que con una fuente base de 10 puntos.

Utilice el comando `\footnotesize` si desea el mismo tamaño de fuente que utiliza LaTeX para las notas al pie; utilice `\scriptsize` para un tamaño que coincida con los subíndices y superíndices de LaTeX. Las clases de documentos proporcionan pasos de tamaño de fuente cuidadosamente seleccionados y adecuados, por lo que normalmente no es necesario establecer un tamaño físico específico.

Si desea un control detallado o ajustes avanzados, estos se tratan en el [Capítulo 3](https://subscription.packtpub.com/book/business-other/9781805804574/3), *Ajuste de fuentes*, en el *LaTeX Cookbook*, publicado por Packt Publishing.

---

### Uso del color

Si bien el estilo de fuente puede ayudar a diferenciar el texto, un poco de color puede hacer que el contenido se destaque más claramente, para dar énfasis, resaltar o llamar la atención. LaTeX proporciona el paquete básico `color`, pero utilizaremos el paquete más versátil `xcolor` de inmediato.

Comenzamos con un breve ejemplo, resaltando una línea corta de texto en rojo negrita para enfatizar su importancia. Siga estas instrucciones:

1. Cree un documento con el siguiente código:

```latex
\documentclass{article}
\usepackage{xcolor}
\begin{document}
\textcolor{red}{\textbf{Important:}} Always keep backup copies of your documents.
\end{document}
```

2. Haga clic en **Typeset** y observe el resultado:

> **Figura 2.9** – Texto con color

El comando `\textcolor` toma dos argumentos obligatorios: el nombre del color y el texto a colorear. En nuestro ejemplo, escribimos `\textcolor{red}{...}` para colorear la palabra *Important:* en rojo. También pusimos la palabra en negrita usando `\textbf`, mostrando cómo combinar dos comandos de formato. Puede utilizar colores estándar como `red`, `blue`, `green`, `yellow`, `black` e incluso `white`. El paquete `xcolor` proporciona cientos de colores con nombre predefinidos, como `LimeGreen` o `DarkCyan`, con enormes tablas en su manual. Puede abrir ese manual ejecutando `texdoc xcolor` en la línea de comandos o visitar [https://texdoc.org/pkg/xcolor](https://texdoc.org/pkg/xcolor).

Al igual que con los comandos de cambio de fuente, LaTeX también proporciona una versión de tipo declaración para configurar el color del texto en porciones más grandes de texto: el comando `\color` actúa como un interruptor; una vez emitido, afecta a todo el texto posterior hasta el final del grupo o entorno actual. Este código daría como resultado la misma salida que la figura anterior:

```latex
{\color{red}\bfseries Important:}
```

El paquete `xcolor` le permite mezclar colores fácilmente usando una sintaxis simple:

```text
name1!percent1!name2!percent2!...
```

Esto significa: tome `percent1` de `name1`, `percent2` de `name2`, y así sucesivamente. Lo ideal es que el total sume el 100%, pero si falta el último porcentaje, `xcolor` simplemente completa el resto. A continuación, se muestran algunos ejemplos para ilustrar cómo funciona:

- Para un gris claro, puede escribir `\color{black!20}` para obtener un 20% de negro.
- Para mezclar un 30% de rojo con un 70% de amarillo, use `\color{red!30!yellow}`.
- Para combinar un 50% de rojo, un 20% de verde y que el 30% restante de la mezcla sea azul, escriba `\color{red!50!green!20!blue}`.

Por lo general, tomo este camino fácil de mezclar los colores base hasta que se vea como quiero. Puede definir sus propios nombres de color y puede utilizar diferentes modelos de color para especificar valores numéricos como RGB, CMYK o incluso códigos HTML, lo cual se explica en el manual a lo largo de más de 60 páginas; pero lo dejaremos así.

Ahora que hemos visto cómo dar formato a palabras y frases, pasemos a dar formato a párrafos enteros.

---

### Limitación del ancho de párrafo

En la mayoría de los casos, escribimos texto de izquierda a derecha en toda el área de texto. Pero a veces es posible que desee reducir el ancho de un párrafo, por ejemplo, al colocar texto junto a una imagen.

En las siguientes secciones, veremos cómo trabajar con cajas de párrafo (*paragraph boxes*) en LaTeX.

#### Creación de un cuadro de texto estrecho

En este ejemplo, explicaremos el acrónimo TUG en una columna de texto de solo 3 cm de ancho. He aquí cómo:

1. Cree un nuevo documento que contenga estas cuatro líneas:

```latex
\documentclass{article}
\begin{document}
\parbox{3cm}{TUG is an acronym. It means \TeX\ Users Group.}
\end{document}
```

2. Haga clic en **Typeset** y revise la salida. Funciona, pero obtenemos líneas sueltas:

> **Figura 2.10** – Un párrafo estrecho justificado con grandes espacios

En este ejemplo, usamos el comando `\parbox` para crear una columna de ancho fijo. El primer argumento especifica el ancho y el segundo argumento contiene el texto.

`\parbox` formatea el texto del argumento para que se ajuste al ancho especificado. De forma predeterminada, el texto está totalmente justificado; sin embargo, nuestro ejemplo muestra un problema evidente: mantener la justificación completa podría generar espacios incómodos en el texto. Hay algunas opciones para mejorar la apariencia:

- Introducir división de palabras (*hyphenation*), por ejemplo, dividiendo palabras largas como *acronym*.
- Mejorar el comportamiento general de justificación.
- Desactivar la justificación completa y cambiar a la alineación no justificada a la derecha (*ragged-right* / alineada a la izquierda).

Examinaremos estas técnicas en las secciones *Saltos de línea y párrafos* y *Cambio de alineación del texto* más adelante en este capítulo.

Pero primero, echemos un vistazo más de cerca a cómo funciona realmente `\parbox`.

#### Producción de cuadros de párrafo

En la mayoría de los casos, simplemente necesitamos un cuadro de texto con un cierto ancho. Sin embargo, a veces también queremos controlar cómo se alinea con el texto circundante. El comando `\parbox` admite un argumento opcional para la alineación. La forma general del comando `\parbox` es la siguiente:

```latex
\parbox[alignment]{width}{text}
```

Estos son los significados de los parámetros:

- `alignment` es el argumento opcional para la alineación vertical con el texto circundante:
  - `t` alinea en la línea de base de la línea superior de la caja.
  - `b` alinea en la línea de base de su línea inferior.
  - `c` alinea su centro vertical con el centro de la línea de texto adyacente. Ese es el valor predeterminado, por lo que puede omitirlo.
- `width` establece el ancho de la caja. Puede utilizar unidades de longitud estándar sin espacios, como `3cm`, `44mm` o `2in`.
- `text` es el contenido que desea colocar en esa caja. Debe ser un párrafo corto o una frase. Para contenido más complejo o de varios párrafos, considere utilizar el entorno `minipage` en su lugar. Veremos esto en la siguiente sección.

He aquí una demostración del efecto de los parámetros de alineación:

```latex
\documentclass{article}
\begin{document}
Text line
\quad\parbox[b]{1.8cm}{this parbox is aligned at its bottom line}
\quad\parbox{1.5cm}{center-aligned parbox}
\quad\parbox[t]{2cm}{another parbox aligned at its top line}
\end{document}
```

El comando `\quad` produce algo de espacio; lo usamos para separar un poco las cajas. He aquí la salida:

> **Figura 2.11** – Cajas de párrafos alineadas

La Figura 2.11 muestra cómo funcionan los argumentos de alineación. Utilizando el texto anterior como línea de base, las siguientes cajas se alinean, respectivamente, en la línea inferior, la línea superior o el centro.

#### Exploración de características adicionales de los cuadros de párrafo

El comando `\parbox` ofrece aún más control. Si necesita un posicionamiento avanzado, aquí está la sintaxis completa:

```latex
\parbox[alignment][height][inner alignment]{width}{text}
```

Los significados de los nuevos argumentos son los siguientes:

- `height`: De forma predeterminada, la caja tendrá solo la altura natural del texto interior. Utilice este argumento si desea cambiar la altura de la caja para hacerla más grande o más pequeña que el contenido.
- `inner alignment`: Si la altura de la caja es diferente de la altura natural del texto contenido, es posible que desee ajustar la posición del texto. Puede especificar los siguientes valores:
  - `c`: Centrar el texto en la caja verticalmente.
  - `t`: Alinear el texto en la parte superior de la caja.
  - `b`: Alinear el texto en la parte inferior.
  - `s`: Estirar el texto verticalmente para llenar la caja (si es posible).
  - Si omite este argumento, se utilizará el argumento `alignment` aquí como valor predeterminado.

Tome nuestro ejemplo de demostración anterior y pruebe el efecto de los argumentos opcionales. Para ver mejor el efecto, use el comando `\fbox`: si escribe `\fbox{\parbox[...]{...}{text}}`, toda la `parbox` obtendrá un marco.

#### Uso de minipáginas

Si bien `\parbox` funciona bien para pequeñas cantidades de texto, es difícil administrar contenido más largo. Una llave de cierre podría olvidarse o pasarse por alto fácilmente. El entorno `minipage` sería entonces una mejor opción. Una minipágina es una pequeña área en su página principal que LaTeX mantiene junta sin dividirla a través de páginas.

En este ejemplo, utilizaremos el entorno `minipage` en lugar de `\parbox` para obtener una muestra de texto con un ancho de solo 3 cm:

1. Modifique el ejemplo de `parbox` para obtener el siguiente código:

```latex
\documentclass{article}
\begin{document}
\begin{minipage}{3cm}
TUG is an acronym. It means \TeX\ Users Group.
\end{minipage}
\end{document}
```

2. Haga clic en **Typeset** y observe la salida:

> **Figura 2.12** – Un ejemplo de minipágina

Al usar `\begin{minipage}`, iniciamos una "página dentro de una página". Especificamos el ancho de 3 cm como argumento obligatorio. A partir de ese momento, LaTeX ajustará las líneas de texto para que quepan dentro del ancho de 3 cm; se ajustarán automáticamente y estarán completamente justificadas. Terminamos esta restricción con `\end{minipage}`. Cualquier texto siguiente se extendería sobre todo el ancho del cuerpo del texto.

Un entorno `minipage` nunca tendrá un salto de página dentro, por lo que es una forma de evitar saltos de página para el contenido que desea mantener junto. Si el contenido de un entorno `minipage` no cabe en la página actual, LaTeX lo moverá por completo a la página siguiente.

El entorno `minipage` acepta los mismos argumentos que `\parbox` con los mismos significados.

Cuando el texto se ajusta en una caja o simplemente en una línea normal, LaTeX lo ajustará automáticamente al diseño de la página de manera razonablemente adecuada. Sin embargo, es posible que aún deseemos afinar el salto de línea y la justificación. Veamos cómo hacerlo en las siguientes secciones.

---

### Saltos de línea y párrafos

En la mayoría de los casos, no necesita preocuparse por cómo se dividen las líneas mientras escribe. Simplemente escriba su texto en su editor, y LaTeX le dará formato para que se ajuste a la línea y manejará la justificación. Para comenzar un nuevo párrafo, simplemente inserte una línea vacía antes de continuar con el texto para el siguiente párrafo.

Ahora, discutiremos cómo controlar el ajuste de línea. Primero, examinaremos formas de mejorar la división silábica automática (*hyphenation*) y, segundo, aprenderemos comandos para insertar saltos directamente.

#### Mejora de la división de palabras

Si observa documentos más extensos, a menudo notará lo impresionantemente bien que LaTeX justifica los párrafos y distribuye el espaciado entre palabras de manera uniforme. Si es necesario, LaTeX dividirá las palabras con guiones al final de la línea para mejorar la alineación.

LaTeX ya utiliza algoritmos excelentes y muy sofisticados para la división de palabras, pero en casos raros no puede encontrar una manera aceptable de dividir una palabra. El ejemplo anterior señaló este problema: dividir la palabra *acronym* mejoraría el resultado, pero LaTeX no sabe dónde dividirla. Descubriremos cómo resolver eso.

No importa cuán razonable sea la justificación, el texto en columnas muy estrechas es extremadamente difícil de justificar. Para lograr una justificación completa, LaTeX puede insertar espacios significativos entre las palabras, pero queremos evitarlo.

En el siguiente ejemplo, le diremos a LaTeX cómo se podría dividir una palabra, para darle a LaTeX más flexibilidad para la justificación de párrafos:

1. Inserte la siguiente línea en el preámbulo del ejemplo anterior:

```latex
\hyphenation{acro-nym}
```

2. Haga clic en **Typeset** y observe la salida:

> **Figura 2.13** – Un párrafo con división silábica mejorada

Le hemos indicado a LaTeX que la palabra *acronym* se puede dividir entre *acro* y *nym*. Eso le permite a LaTeX insertar un guión después de *acro* al final de la línea y mover *nym* hacia la siguiente línea.

El comando `\hyphenation` le dice a LaTeX dónde se puede dividir una palabra si es necesario. Su argumento puede contener varias palabras separadas por espacios. Para cada palabra, podemos indicar múltiples puntos de corte. Por ejemplo, podríamos ampliar el argumento con más puntos de división y más variantes de palabras, así:

```latex
\hyphenation{ac-ro-nym ac-ro-nym-ic a-cro-nym-i-cal-ly}
```

También podría indicar puntos de división dentro del cuerpo del texto insertando una barra invertida seguida de un guión, como `ac\-ro\-nym`. Sin embargo, al utilizar el comando `\hyphenation` en el preámbulo, puede recopilar todas las reglas allí, asegurándose de que se utilicen de forma coherente. Por lo tanto, utilícelo principalmente en los raros casos en que falla la automatización de LaTeX.

#### Prevención de la división de palabras

A veces, es posible que desee evitar que LaTeX divida con guiones una palabra en particular. Hay varias formas:

- Declárela en el preámbulo utilizándola en el argumento de `\hyphenation` sin ningún punto de división, como `\hyphenation{indivisible}`.
- Envuelva la palabra en un comando `\mbox`, que mantiene toda la palabra junta, así: `The following word is \mbox{indivisible}`.
- Cargar el paquete `hyphenat` nos da más control:
  - `\usepackage[none]{hyphenat}` desactiva la división de palabras por completo.
  - `\usepackage[htt]{hyphenat}` habilita la división de palabras para texto de máquina de escribir; de lo contrario, tales palabras monoespaciadas no se dividirán por defecto, lo cual tiene sentido para URL y palabras clave de código.

Estos argumentos opcionales para `\usepackage` se denominan **opciones de paquete** (*package options*). Configuran el comportamiento de un paquete. Las opciones mencionadas se pueden combinar, separadas por comas, como en `\usepackage[htt,none]{hyphenat}`. Incluso si no utiliza la opción `none`, puede deshabilitar la división de palabras para fragmentos cortos de texto utilizando el comando `\nohyphens{text}`. Pruebe estas características si desea beneficiarse de ellas. La documentación del paquete en [https://texdoc.org/pkg/hyphenat](https://texdoc.org/pkg/hyphenat) proporciona más información sobre características adicionales que pueda necesitar, como la división silábica después de caracteres especiales como números y signos de puntuación.

#### Mejora de la justificación

El compilador de TeX más popular hoy en día es `pdfTeX`, que genera documentos directamente como un PDF. Cuando Hàn Thế Thành desarrolló `pdfTeX`, agregó mejoras microtipográficas, ajustes sutiles que mejoran la apariencia general. Podemos aprovechar estas nuevas características utilizando el paquete `microtype`.

Mejoremos nuestro ejemplo anterior utilizando el paquete `microtype`:

1. Inserte la siguiente línea en el preámbulo del ejemplo anterior:

```latex
\usepackage{microtype}
```

2. Haga clic en **Typeset** y observe la salida:

> **Figura 2.14** – Un párrafo con mejor justificación

¿Qué sucedió? Simplemente cargando el paquete `microtype` sin ninguna opción, activamos sus características predeterminadas. Introduce la expansión de fuentes para ajustar la justificación y utiliza puntuación colgante (*hanging punctuation*) para mejorar la apariencia visual de los márgenes. Esto puede reducir la necesidad de separación silábica y evitar que queden espacios incómodos entre las palabras para lograr una justificación completa. Ha visto su efecto en una columna estrecha, así que imagine la mejora en el texto ancho: ¡téngalo en cuenta y pruébelo más tarde!

Aunque `microtype` proporciona funciones y opciones potentes para el tipógrafo avanzado, por lo general no necesitaremos hacer más que cargarlo para beneficiarnos de él. Hay una extensa documentación del paquete si desea estudiarlo en profundidad: ejecute el comando `texdoc microtype` en la línea de comandos o ábralo en [https://texdoc.org/pkg/microtype](https://texdoc.org/pkg/microtype). `microtype` hace ajustes agradables, pero no es una panacea; aún debemos ocuparnos de la correcta división silábica cuando sea necesario.

#### Saltos de línea manuales

Podemos decidir terminar una línea nosotros mismos, anulando la automatización. Ahora aprenderemos sobre varios comandos con diferentes efectos para terminar una línea.

Compongamos la apertura del famoso poema *Annabel Lee* de Edgar Allan Poe. Dado que el poeta determinó exactamente dónde debe terminar cada verso, insertaremos los saltos manualmente.

Escribamos el comienzo del poema:

1. Cree un documento que contenga estas líneas:

```latex
\documentclass{article}
\begin{document}
\noindent\emph{Annabel Lee}\\
It was many and many a year ago,\\
In a kingdom by the sea,\\
That a maiden there lived whom you may know\\
By the name of Annabel Lee
\end{document}
```

2. Haga clic en **Typeset** y revise la salida:

> **Figura 2.15** – Líneas divididas manualmente

El brevísimo comando `\\` finalizó la línea actual y el texto siguiente se movió a la siguiente línea. Sin embargo, es diferente de un salto de párrafo ya que permanecemos en el mismo párrafo. El comando `\newline` es una alternativa y tiene el mismo efecto.

De forma predeterminada, LaTeX sangra la primera línea del párrafo, lo cual es una convención útil para separar visualmente los párrafos. Usamos el comando `\noindent` para suprimir la sangría del párrafo. No lo necesitará a menudo porque, después de los encabezados, no hay sangría de párrafo de forma predeterminada. Para eliminar la sangría de párrafo en todo el documento y usar espaciado vertical entre párrafos en su lugar, cargue el paquete `parskip`. Puede ver esto en la Figura 2.23 y el código correspondiente.

Tenga en cuenta que aunque insertamos finales de línea, el texto siguió siendo un solo párrafo. Por lo tanto, nuestros saltos de línea no causaron una sangría de párrafo, ya que lógicamente sigue siendo parte del mismo párrafo.

#### Exploración de opciones de salto de línea

El comando `\\` admite los siguientes argumentos opcionales para un ajuste fino:

- `\\[value]` inserta espacio vertical adicional después del salto con el valor solicitado, como `\\[3mm]`.
- `\\*[value]` hace lo mismo pero evita que ocurra un salto de página inmediatamente después.

Intente, por ejemplo, cambiar la apertura de nuestro ejemplo del poema a lo siguiente:

```latex
\emph{Annabel Lee}\\[3mm]
```

Eso inserta un espacio adicional de 3 mm entre esta línea y el fragmento del poema, separándola como un encabezado.

Hay otro comando llamado `\linebreak` que le dice a LaTeX que termine la línea manteniendo la justificación completa. Si es necesario, LaTeX estirará el espacio entre palabras para alcanzar el margen derecho. Esto podría causar espacios desagradables; por eso este comando rara vez se usa, o al menos con un argumento opcional; `\linebreak[number]` se puede utilizar para ajustar el salto de línea. Si el número es 0, se permite un salto de línea; 1 significa que es deseado; 2 y 3 marcan solicitudes más insistentes; y 4 lo forzará. Este último es el comportamiento predeterminado si no se proporciona ningún número.

#### Prevención de saltos de línea

El comando `\linebreak` tiene un opuesto directo: `\nolinebreak`. Este comando evita un salto de línea en la posición actual.

Al igual que su contraparte, toma un argumento opcional para controlar la fuerza de la solicitud. Si escribe `\nolinebreak[0]`, simplemente sugiere no romper la línea aquí. Usar 1, 2 o incluso 3 insiste más y `\nolinebreak[4]` lo prohíbe estrictamente. LaTeX asume esta última opción si no proporciona ningún argumento.

El comando ya mencionado `\mbox{text}` no solo desactiva la división de palabras, sino que también puede usarlo para evitar un salto de línea dentro del texto encerrado.

En lugar de `\nolinebreak`, puede utilizar el atajo `~`, que representa un espacio entre palabras donde no se permite ningún salto de línea. Por ejemplo, si escribe `Dr.~Watson`, LaTeX nunca dejará el título *Dr.* colgando solo al final de una línea.

De forma predeterminada, LaTeX justifica completamente el texto, estirando las líneas para alinearlas con el margen derecho. LaTeX tiene un método excelente para ajustar el espaciado en párrafos enteros, pero a veces puede generar grandes espacios indeseables entre palabras en una línea justificada. Veamos cómo deshabilitar esto si así lo deseamos.

---

### Cambio de alineación del texto

Si bien su texto generalmente se verá bien alineado si se usa la justificación completa, puede haber ocasiones en las que no sea ideal. Por ejemplo, la justificación completa podría resultar desagradable cuando las líneas de texto son cortas; en tal caso, podría ser suficiente alinear solo en el lado izquierdo. Veamos cómo poner esto en práctica, así como cómo alinear a la derecha y crear líneas centradas.

#### Creación de texto alineado a la izquierda (*ragged-right*)

Recuerde nuestro primer ejemplo de `parbox`, donde la justificación completa dio lugar a espacios notables entre las palabras. Esta vez, desactivaremos la justificación del margen derecho para evitar tales espacios:

1. Cree un nuevo documento con las siguientes líneas:

```latex
\documentclass{article}
\begin{document}
\parbox{3cm}{\raggedright TUG is an acronym. It means \TeX\ Users Group.}
\end{document}
```

2. Haga clic en **Typeset** y observe el resultado:

> **Figura 2.16** – Texto alineado a la izquierda

Insertamos la declaración `\raggedright`. A partir de este momento, el texto no estará justificado a la derecha (*ragged-right*). En otras palabras, el texto se moverá hacia el margen izquierdo ("alineado a la izquierda"), dejando el borde derecho irregular. No habrá división silábica.

Como utilizamos esta declaración dentro de una caja, solo afecta al contenido del interior, como dentro de los entornos. Después de la caja, el texto volverá a estar totalmente justificado.

Si desea que todo el documento esté alineado a la izquierda de forma no justificada, puede utilizar `\raggedright` en el preámbulo.

#### Creación de texto alineado a la derecha (*ragged-left*)

En algunos casos, es posible que deseemos lograr el efecto contrario: alinear el texto hacia el margen derecho en su lugar. Podemos hacer esto de manera similar insertando la declaración `\raggedleft`. Puede controlar los saltos de línea utilizando el atajo `\\`.

#### Centrado de texto

Para alinear el texto horizontalmente en el centro de la página, podemos usar la declaración `\centering`. Hagamos esto con unas pocas líneas de ejemplo.

Crearemos manualmente un título de aspecto atractivo para nuestro documento; debe contener el título, el autor y la fecha, todos los cuales estarán centrados:

1. Escriba un documento que contenga este código:

```latex
\documentclass{article}
\pagestyle{empty}
\begin{document}
{\centering
\huge\bfseries Centered text \\
\Large\normalfont written by me \\
\normalsize\today
}
\end{document}
```

2. Haga clic en **Typeset** para ver la salida:

> **Figura 2.17** – Texto centrado

Debido a que solo el título debe estar centrado, usamos un grupo para restringir el efecto de la declaración `\centering`. Todo el texto dentro del grupo se alineará horizontalmente al centro. También insertamos un salto de párrafo con una línea vacía; se recomienda hacer esto antes de finalizar el grupo para aplicar nuestro centrado al párrafo completo. Al usar la llave de cierre, terminamos el grupo. Cualquier texto colocado después de la llave de cierre volverá a la alineación predeterminada, no centrada.

`\centering` se usa a menudo para imágenes y tablas, y en páginas de título.

#### Uso de entornos para la alineación

LaTeX proporciona el entorno `center` que centra el texto y añade espacio vertical a su alrededor.

Probémoslo. Reutilizaremos nuevamente el fragmento del poema de Edgar Allan Poe. Esta vez, centraremos todas las líneas:

1. Inicie un nuevo documento:

```latex
\documentclass{article}
```

2. Ahora, cargue el paquete `url` para que también podamos imprimir un hipervínculo al final:

```latex
\usepackage{url}
```

3. Comience el documento con una línea introductoria:

```latex
\begin{document}
\noindent This is the beginning of a poem by Edgar Allan Poe:
```

4. Ahora, escriba texto en un entorno `center`:

```latex
\begin{center}
\emph{Annabel Lee}
\end{center}
```

5. Nuevamente, escriba texto para el cuerpo del poema:

```latex
\begin{center}
It was many and many a year ago,\\
In a kingdom by the sea,\\
That a maiden there lived whom you may know\\
By the name of Annabel Lee
\end{center}
```

6. Agregue algo de texto, incluida una URL que apunte al poema en Internet, y finalice:

```latex
The complete poem can be read on \url{http://www.online-literature.com/poe/576/}.
\end{document}
```

7. Haga clic en **Typeset** y vea el resultado:

> **Figura 2.18** – Un poema centrado dentro del texto

Comenzamos de nuevo con `\noindent`, evitando la sangría del párrafo. `\begin{center}` inició el entorno `center`, que comienza un nuevo párrafo, con espaciado vertical añadido. `\end{center}` terminó este entorno. Usamos el entorno `center` por segunda vez, donde insertamos `\\` para finalizar los versos. Después de que finaliza el entorno `center`, sigue algo de espacio y el siguiente párrafo comienza en el margen izquierdo.

El entorno correspondiente para texto no justificado a la derecha se llama `flushleft`; aquí, LaTeX empuja todo dentro del entorno hacia la izquierda y deja el lado derecho irregular, y, de manera similar, para texto alineado a la derecha, es el entorno `flushright`.

El centrado es una técnica popular para enfatizar texto. Otra forma es sangrarlo un poco y agregar algo de espacio vertical antes y después del texto. Se utiliza comúnmente para mostrar una cita. Veamos cómo hacer eso a continuación.

---

### Visualización de citas

Al incluir una cita de otro autor, puede ser difícil ver que se trata de una cita cuando está directamente incrustada dentro del texto. Una práctica común y eficaz para mejorar la legibilidad es resaltar visualmente la cita sangrándola tanto en el lado izquierdo como en el derecho. Ilustremos esto con citas de físicos famosos en el siguiente ejemplo:

1. Cree un nuevo documento con algo de texto introductorio:

```latex
\documentclass{article}
\begin{document}
\noindent Niels Bohr said: ``An expert is a person who has made all the mistakes that can be made in a very narrow field.''
Albert Einstein said:
```

2. Muestre la cita utilizando el entorno `quote`:

```latex
\begin{quote}
Anyone who has never made a mistake has never tried anything new.
\end{quote}
```

3. Agregue una frase final y concluya:

```latex
Errors are inevitable. So, let's be brave trying something new.
\end{document}
```

4. Haga clic en **Typeset** para compilar y ver el resultado:

> **Figura 2.19** – Citas

En primer lugar, citamos en línea (*inline*), que está dentro del flujo de texto del párrafo. El atajo ``` ` ``` produce una comilla tipográfica izquierda y el atajo `'` proporciona una comilla derecha. Para obtener comillas dobles, simplemente escribimos dos de estos caracteres. A esto lo llamamos cita en línea.

Luego, usamos el entorno `quote` para mostrar una cita separada del texto circundante. No comenzamos un nuevo párrafo para ello, porque la cita ya está apartada en su propio párrafo. A eso se le llama cita en bloque (*displayed quoting*).

#### Citas de textos más largos

Para citas cortas, el entorno `quote` funciona bien. Sin embargo, cuando cita un pasaje de texto más extenso que abarca varios párrafos, es posible que prefiera mantener la sangría de párrafo predeterminada como en el texto circundante. El entorno `quotation` hará esto por usted.

Citemos algunos beneficios de usar TeX y LaTeX, como se describe en una página web en CTAN:

1. Inicie un nuevo documento con este texto:

```latex
\documentclass{article}
\usepackage{url}
\begin{document}
The authors of the CTAN team listed ten good reasons for using \TeX. Among them are:
\begin{quotation}
\TeX\ has the best output. What you end with, the symbols on the page, is as useable, and beautiful, as a non-professional can produce.
\TeX\ knows typesetting. As those plain text samples show, TeX's has more sophisticated typographical algorithms such as those for making paragraphs and for hyphenating.
\TeX\ is fast. On today's machines \TeX\ is very fast. It is easy on memory and disk space, too.
\TeX\ is stable. It is in wide use, with a long history. It has been tested by millions of users, on demanding input. It will never eat your document. Never.
\end{quotation}
The original text can be found on \url{https://www.ctan.org/what_is_tex.html}.
\end{document}
```

2. Haga clic en **Typeset** y observe la salida:

> **Figura 2.20** – Una sección larga de texto citado

Esta vez, usamos el entorno `quotation` para mostrar múltiples párrafos. Al igual que en el texto normal, las líneas en blanco separan los párrafos; están sangrados a la izquierda en su comienzo, tal como en todo nuestro cuerpo del texto.

¿Pero qué pasa si preferimos no usar esa sangría de párrafo? Veamos una alternativa.

En este ejemplo, evitaremos la sangría de párrafo y en su lugar separaremos los párrafos con algo de espacio vertical. Como texto de relleno, utilizaremos unas pocas frases del ejemplo anterior sobre citas, de la siguiente manera:

1. Cree un pequeño documento con el siguiente código:

```latex
\documentclass{article}
\usepackage{parskip}
\usepackage{url}
\begin{document}
The authors of the CTAN team listed ten good reasons for using \TeX. Among them are:
\TeX\ has the best output. What you end with, the symbols on the page, is as useable, and beautiful, as a non-professional can produce\ldots
The original text can be found on \url{https://www.ctan.org/what_is_tex.html}.
\end{document}
```

2. Haga clic en **Typeset** y vea el efecto:

> **Figura 2.21** – Espaciado vertical entre párrafos

Aquí cargamos el paquete `parskip` para eliminar la sangría del párrafo por completo. En su lugar, este paquete añade espacio vertical entre los párrafos. Sin embargo, este paquete no altera el comportamiento del entorno `quotation`; aún puede usar el entorno `quote`.

Hay dos formas comunes de distinguir párrafos. Una es sangrar la primera línea de cada párrafo, que es el comportamiento predeterminado de LaTeX. La otra es insertar espacio vertical entre párrafos sin sangría. Esto a menudo se prefiere para columnas estrechas, donde la sangría ocuparía un espacio valioso.

Hasta ahora, hemos practicado el uso de muchos comandos físicos predefinidos para personalizar texto y párrafos. El siguiente paso es crear nuestros propios comandos de formato lógico y utilizarlos dentro del cuerpo del texto del documento en su lugar.

---

### Creación de comandos

Si se encuentra utilizando el mismo término repetidamente en su documento, puede resultar tedioso escribirlo cada vez. ¿Qué pasa si luego decide cambiar ese término o su formato? Para evitar buscar y reemplazar el término en todo el documento, LaTeX le permite definir sus propios comandos personalizados en su preámbulo. Eso ahorra tiempo y garantiza la coherencia.

Recuerde: Un comando que se compone de otros comandos o texto se denomina **macro**, y eso es lo que definiremos ahora. Básicamente, elegimos un nuevo nombre de macro y definimos la secuencia de texto o comandos que se utilizarán en esa macro. Luego, cada vez que queramos reutilizar ese contenido o formato, solo necesitamos llamar a la macro por su nombre.

Comenzaremos con macros básicas que funcionan como abreviaturas.

#### Uso de macros para texto simple

Las macros son excelentes para evitar repetir palabras o frases largas y también pueden actuar como marcadores de posición, como para nombres de personas o empresas o cualquier cosa que pueda cambiar en un contexto diferente. Podemos modificar el contenido de la macro para actualizar todo el documento con una versión diferente de esa frase.

En el siguiente ejemplo, definiremos un comando corto para representar el nombre del *TeX Users Group* (TUG):

1. Introduzca el siguiente código en un nuevo documento:

```latex
\documentclass{article}
\newcommand{\TUG}{\TeX\ Users Group}
\begin{document}
\section{The \TUG}
The \TUG\ is an organization for people who use \TeX\ or \LaTeX.
\end{document}
```

2. Haga clic en **Typeset** y observe el resultado:

> **Figura 2.22** – Uso de nuestra primera macro

Llamamos a `\newcommand` en la línea destacada para definir nuestro comando. El primer argumento es el nombre del comando que hemos elegido, y el segundo argumento es el texto al que debe expandirse cada vez que usemos ese comando en el documento.

Ahora, cada vez que escribimos `\TUG` en nuestro documento, LaTeX imprimirá el nombre completo *TeX Users Group*. Si luego decidimos cambiar el nombre o su formato, solo necesitamos cambiar esta línea `\newcommand`. Luego, el cambio de esa macro se aplicará a todo el documento.

Puede utilizar comandos de formato dentro de la definición de su comando. Supongamos que desea cambiar el formato de todas las apariciones de este nombre para que se compongan en versalitas (*small caps*); simplemente cambie la definición por la siguiente:

```latex
\newcommand{\TUG}{\textsc{TeX Users Group}}
```

Observe que hemos utilizado el comando `\TeX`. Este comando de abreviatura simplemente imprime el nombre del sistema de composición tipográfica, formateado de la misma manera que su logotipo. El comando integrado `\LaTeX` funciona de manera similar.

Tenga en cuenta que usamos una barra invertida después de `\TeX`. El espacio siguiente simplemente separaría el comando del texto siguiente; no produciría un espacio en la salida. El uso de la barra invertida seguida de un espacio fuerza la salida de un espacio que de otro modo sería ignorado. Eso también se aplica al comando que acabamos de crear.

Ahora veremos cómo evitar ese espaciado manual.

#### Mejora del espaciado después de los comandos

Es fácil olvidar la barra invertida adicional necesaria para insertar un espacio después de una macro. ¿Podemos automatizar eso? Tareas como esta, que no son manejadas directamente por LaTeX, a menudo se pueden resolver mediante el uso de paquetes, que son colecciones de estilos y comandos.

En este caso, utilizaremos el paquete `xspace`; su único propósito es ajustar automáticamente el espaciado después de la salida de una macro:

1. Inserte esta línea en su preámbulo, antes de `\begin{document}`:

```latex
\usepackage{xspace}
```

2. Agregue el comando `\xspace` al final de la definición de su macro:

```latex
\newcommand{\TUG}{\TeX\ Users Group\xspace}
```

La línea `\usepackage{xspace}` le dice a LaTeX que cargue el paquete `xspace` e importe sus definiciones. Después de `\usepackage`, podemos usar todos los comandos contenidos en ese paquete.

Este paquete proporciona el comando `\xspace`, que inserta un espacio dependiendo de cuál sea el siguiente carácter:

- Si le sigue una letra normal, insertará un espacio después del contenido de la macro.
- Si le sigue un signo de puntuación como un punto, una coma, un signo de exclamación o una comilla, no insertará un espacio.

Esta sencilla solución automatizada funciona bien en texto normal; siempre inserta un espacio si le sigue una letra y lo omite cuando detecta puntuación. En el raro caso de que le siga algo más, como una macro que `xspace` no pueda interpretar, e inserte un espacio, puede evitarlo agregando `{}` justo después del comando `\xspace`. El manual del paquete lo explica claramente; puede encontrarlo en [https://texdoc.org/pkg/xspace](https://texdoc.org/pkg/xspace).

#### Creación de comandos flexibles con argumentos

Suponga que su documento contiene muchas palabras clave que desea que se muestren en negrita. Si usa el comando `\textbf` cada vez, ¿qué sucederá si luego decide usar una forma cursiva en su lugar, o una fuente de máquina de escribir? Tendría que actualizar ese formato para cada instancia de esa palabra clave, lo cual es tedioso y propenso a errores.

Hay una mejor manera: definir una macro personalizada que use `\textbf` internamente.

##### Definición de una macro con argumentos

En esta sección, usaremos `\newcommand` nuevamente, pero esta vez, le daremos un argumento que contendrá nuestra palabra clave. Para nuestro ejemplo, lo aplicaremos a algunos términos que aprendimos anteriormente en este capítulo.

Comencemos:

1. Introduzca el siguiente código en su editor. Nuestro comando se llamará `\keyword`:

```latex
\documentclass{article}
\newcommand{\keyword}[1]{\textbf{#1}}
\begin{document}
\keyword{Grouping} by curly braces limits the \keyword{scope} of \keyword{declarations}.
\end{document}
```

2. Haga clic en **Typeset** y observe cómo aparecen las palabras clave en la salida:

> **Figura 2.23** – Formateo de palabras clave

Veamos la línea `\newcommand` en el código. El número 1 entre corchetes marca el número de argumentos que queremos usar en el comando. `#1` es un marcador de posición y será reemplazado por el valor del primer argumento; `#2` sería reemplazado por el valor del segundo argumento, y así sucesivamente. Ahora, si decide cambiar la apariencia de todas las palabras clave para que estén en cursiva, simplemente modifique la definición de `\keyword` para usar `\textit{#1}`, y el cambio será global.

La primera vez que usamos `\newcommand`, en la sección *Uso de macros para texto simple*, lo usamos con dos argumentos: el nombre de la macro y su definición. En el ejemplo anterior, había tres argumentos; el argumento adicional está encerrado entre corchetes, lo que indica que es un argumento opcional, por lo que se puede proporcionar u omitir. Si se omite, tendría un valor predeterminado.

Anteriormente, ya hemos trabajado con el comando `\documentclass` y argumentos opcionales, pero ¿cómo podemos definir nosotros mismos un comando con argumentos opcionales? Averigüémoslo.

##### Definición de una macro con argumentos opcionales

Revisemos `\newcommand`, pero esta vez le daremos un argumento de formato opcional junto con un argumento de palabra clave obligatorio:

1. Actualice el ejemplo anterior con el siguiente código:

```latex
\documentclass{article}
\newcommand{\keyword}[2][\bfseries]{{#1#2}}
\begin{document}
\keyword{Grouping} by curly braces limits the \keyword{scope} of \keyword[\itshape]{declarations}.
\end{document}
```

2. Haga clic en **Typeset** y compruebe el resultado:

> **Figura 2.24** – Argumentos opcionales

Veamos nuevamente la línea `\newcommand` en el código. Al usar `[\bfseries]` entre corchetes, introdujimos un parámetro opcional; nos referimos a él por `#1`, y su valor predeterminado está establecido en `\bfseries`. Como usamos una declaración esta vez, agregamos un par de llaves para asegurar que solo la palabra clave se vea afectada por la declaración. Más adelante en el documento, pasamos `[\itshape]` al comando `\keyword`, cambiando el formato predeterminado a cursiva.

He aquí la forma general de `\newcommand`:

```latex
\newcommand{command}[arguments][optional]{definition}
```

Estos son los significados de los parámetros para `\newcommand`:

- `command`: El nombre del nuevo comando, que comienza con una barra invertida seguida de letras minúsculas y/o mayúsculas, o una barra invertida seguida de un único símbolo que no sea una letra. El nombre no debe estar ya definido y no puede comenzar con `\end`.
- `arguments`: Un número del 1 al 9 que le indica a LaTeX cuántos argumentos acepta el nuevo comando. Si se omite, el comando no toma ningún argumento.
- `optional`: Si está presente, el primero de los argumentos sería opcional con un valor predeterminado dado aquí. De lo contrario, todos los argumentos son obligatorios.
- `definition`: Cada aparición de `command` será reemplazada por `definition` y cada aparición de la forma `#n` será luego reemplazada por el enésimo argumento.

Utilice `\newcommand` para definir estilos reutilizables para palabras clave, fragmentos de código, direcciones web, nombres, notas, cuadros de información o texto enfatizado de manera diferente. Así es como logramos la estructura coherente de este libro, definiendo y utilizando estilos. Debemos usar comandos de fuentes dentro de nuestras definiciones de macros en lugar de dispersarlos por todo el cuerpo del texto del documento.

Siempre que sea posible, defina sus propias macros para lograr una estructura lógica. Se beneficiará de un formato coherente, cambios globales más sencillos y un código más fácil de mantener. Al definir y utilizar macros, puede asegurarse de que el formato se mantenga coherente en todo el documento.

#### Redefinición de comandos

Puede cambiar las macros existentes de LaTeX usando `\renewcommand` de una manera muy similar:

```latex
\renewcommand{command}[arguments][optional]{definition}
```

Es posible que rara vez lo necesite como principiante, aunque es una forma común de cambiar, por ejemplo, los valores predeterminados de LaTeX. A continuación, se muestran algunos ejemplos con los que puede encontrarse más adelante:

- `\renewcommand{\familydefault}{\sfdefault}` hace que la familia de fuentes predeterminada sea la familia sin serifa predeterminada, de modo que ya no sea una fuente con serifa por defecto.
- `\renewcommand{\arraystretch}{1.5}` estira la altura de fila predeterminada en las tablas por un factor de 1.5.
- `\renewcommand{\thepage}{\Roman{page}}` cambia la visualización del número de página a números romanos en mayúsculas. `\roman` significaría minúsculas.

Este comando es especialmente útil si desea personalizar una macro o comando existente.

---

### Creación de entornos

Así como `\newcommand` nos permite definir nuevos comandos, LaTeX tiene un comando para definir bloques de contenido: `\newenvironment`. Esto es útil cuando queremos marcar secciones más grandes de texto, como notas, cajas, ejemplos u otros patrones de diseño repetidos, con formato y estructura coherentes.

Pasemos inmediatamente a la forma general:

```latex
\newenvironment{name}[arguments][optional]{begin-code}{end-code}
```

Estos son los significados de los parámetros para `\newenvironment`:

- `name`: El nombre del entorno, utilizado más adelante como `\begin{name}` y `\end{name}`.
- `arguments`: Un número opcional del 1 al 9 que indica cuántos argumentos acepta el entorno; 0 por defecto cuando se omite.
- `optional`: Si se proporciona, asigna un valor predeterminado al primer argumento opcional.
- `begin-code`: LaTeX ejecutará este código al inicio del entorno. Utilice `#1`, `#2`, etc., para hacer referencia a los argumentos.
- `end-code`: LaTeX ejecuta este código cuando finaliza el entorno.

Para obtener una especificación muy completa de este y de todos los comandos de definición de macros, consulte la referencia en [https://latex2e.org/Definitions.html](https://latex2e.org/Definitions.html).

He aquí un ejemplo para ilustrarlo en la práctica:

```latex
\documentclass{article}
\newenvironment{note}[1][Note]
  {\begin{quote}\textbf{#1}\itshape}
  {\end{quote}}
\begin{document}
\begin{note}[Hint]
Use high-contrast colors for readability.
\end{note}
\end{document}
```

Este código hace lo siguiente:

- Define un entorno `note` que toma un argumento opcional.
- Se basa en el entorno `quote`.
- Si no se proporciona ningún argumento, imprime *Note* al principio. De lo contrario, comienza con el argumento opcional, como *Hint* aquí.
- Continúa con fuente cursiva para el texto restante en el entorno.

De manera similar a `\renewcommand`, puede usar `\renewenvironment` con exactamente la misma sintaxis para redefinir un entorno existente. Eso es algo que rara vez necesitará, y también puede encontrarlo en [https://latex2e.org](https://latex2e.org/), por lo que concluiremos con esto.

---

### Uso de una sintaxis alternativa

LaTeX ahora proporciona formas adicionales de definir comandos y entornos. Puede continuar usando los comandos clásicos de las secciones anteriores y omitir esta sección por ahora. Si lo desea, echemos un vistazo rápido al enfoque más nuevo. Ahora puede definir comandos de esta manera:

```latex
\NewDocumentCommand{<command name>}{<argument types>}{code}
```

Los tipos de argumentos pueden ser `m` para un argumento obligatorio (*mandatory*), una `o` minúscula para un argumento opcional, o una `O{text}` mayúscula para un argumento opcional con texto predeterminado cuando se omite el argumento. Pero veamos cómo se ve en la práctica.

La definición para la macro de la Figura 2.22 ahora sería la siguiente:

```latex
\NewDocumentCommand{\TUG}{}{\TeX\ Users Group}
```

En la macro para la Figura 2.23, teníamos un argumento obligatorio. Se traduce en lo siguiente:

```latex
\NewDocumentCommand{\keyword}{m}{\textbf{#1}}
```

Para la Figura 2.24, agregamos un argumento opcional con un valor predeterminado. La misma macro también se puede escribir así:

```latex
\NewDocumentCommand{\keyword}{O{\bfseries}m}{{#1#2}}
```

Si tiene curiosidad sobre cómo se puede utilizar la opción `o` para lograr lo mismo, se ve de la siguiente manera:

```latex
\NewDocumentCommand{\keyword}{om}{{%
  \IfNoValueTF{#1}%
    {\bfseries#2}%
    {#1#2}%
}}
```

Aquí, usamos este comando para manejar ambos casos: cuando se proporciona el argumento opcional y cuando no:

```latex
\IfNoValueTF{#1}%
  {Do stuff with argument #2 only}%
  {Do stuff with arguments #1 and #2}%
```

Tenga en cuenta que utilicé el signo de porcentaje (`%`) al final de las líneas para evitar introducir espacios en blanco accidentalmente, ya que los saltos de línea se tratan como espacios. Por eso comenté los saltos de línea.

`TF` significa verdadero (*true*) y falso (*false*). También hay variantes más cortas para casos individuales. Para cubrir simplemente el caso de que no se proporcionó ningún argumento `#1` (*true*), se utiliza lo siguiente:

```latex
\IfNoValueT{#1}{Do stuff with argument #2 only}%
```

Si se proporcionó un argumento `#1` (*false*), se utiliza lo siguiente:

```latex
\IfNoValueF{#1}{Do stuff with arguments #1 and #2}%
```

Puede parecer un poco complejo al principio, pero este sistema le brinda mucha más flexibilidad. Incluso puede definir múltiples argumentos opcionales. Por ejemplo, he aquí una definición más avanzada con cinco argumentos obligatorios y tres opcionales:

```latex
\NewDocumentCommand{\name}{ m m m m m O{#3} O{#4} O{#5} }{ ... }
```

Ve que puede haber espacios entre los especificadores para mayor claridad, y puede usar `#n` para un valor predeterminado con un enésimo argumento dado. Hay más tipos de argumentos, y puede agregar delimitadores para los argumentos, e incluso tiene más comandos similares, como `\RenewDocumentCommand`, `\NewDocumentEnvironment` y `\RenewDocumentEnvironment`, como reemplazos de los comandos respectivos en las secciones anteriores.

Si considera adoptar este nuevo enfoque, eche un vistazo a estos enlaces:

- [https://www.texdev.net/2010/05/23/from-newcommand-to-newdocumentcommand/](https://www.texdev.net/2010/05/23/from-newcommand-to-newdocumentcommand/) – un artículo de blog del desarrollador de LaTeX Joseph Wright con ejemplos claros.
- [https://texdoc.org/pkg/xparse](https://texdoc.org/pkg/xparse) – la documentación completa.
- [https://www.latex-project.org/publications/2021-JAW-TUB-tb130wright-newdoccmd.pdf](https://www.latex-project.org/publications/2021-JAW-TUB-tb130wright-newdoccmd.pdf) – una comparación detallada con otras sintaxis y paquetes, para usuarios avanzados.

¿Por qué querría utilizar este enfoque?

- El equipo del proyecto LaTeX lo recomienda.
- Si bien es fácil de usar para casos simples, puede definir macros más complejas.
- Lo más importante: en contraste con `\newcommand`, sus nuevas macros son **robustas**, también denominadas protegidas (*protected*); no se expanden a su definición inmediatamente cuando LaTeX procesa su código, sino en una etapa posterior.

Así, por ejemplo, si utiliza dicha macro en un título de sección, el nombre de la macro se escribiría en el archivo `.toc` (tabla de contenidos), mientras que una macro definida con `\newcommand` se expandiría inmediatamente y su contenido expandido iría al archivo `.toc`. O, simplemente digamos, los comandos robustos a menudo le ahorran problemas sutiles. Es un tema bastante avanzado; puede leer sobre él en [https://texfaq.org/FAQ-protect](https://texfaq.org/FAQ-protect).

Personalmente, estoy bien con el `\newcommand` original y sus complementos, pero quiero que conozca las alternativas modernas que también verá en el código LaTeX más nuevo en Internet.

---

### Resumen

En este capítulo, exploramos los fundamentos de la edición, organización y formateo de texto. Específicamente, cubrimos la modificación de fuentes y estilos, el uso de comandos y declaraciones con argumentos obligatorios y opcionales, y la definición de comandos y entornos personalizados. También aprendimos cómo formatear párrafos con diferentes alineaciones, como izquierda, derecha o completamente justificado, y cómo incluir citas.

Tenga en cuenta que, aunque utilizamos comandos de formato directamente en el texto para practicar, es mejor utilizarlos en definiciones de comandos en el preámbulo para tener estilos coherentes en todo un documento. A medida que avancemos en este libro, descubrirá más comandos y paquetes útiles para refinar y ampliar su configuración de formato.

Ahora que ha dominado el formato de texto detallado, está listo para pasar al siguiente capítulo, que se centra en el formato y el diseño de páginas completas, incluidos márgenes, encabezados y pies de página.
