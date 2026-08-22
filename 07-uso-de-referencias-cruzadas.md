# LaTeX Beginner's Guide
## Capítulo 7: Uso de Referencias Cruzadas

En los capítulos anteriores, creamos figuras y tablas y les agregamos leyendas. LaTeX se encarga automáticamente de la numeración. Los documentos también pueden incluir muchos otros elementos numerados, como páginas, secciones y elementos de lista. Y hay más: si está escribiendo contenido matemático, es posible que desee numerar también ecuaciones, teoremas, definiciones y otros elementos.

La numeración no es solo para contar; también nos permite hacer referencia a estos elementos en otras partes del documento. Por ejemplo, en este capítulo, si quisiera dirigirlo a la tercera figura, escribiría "Vea la Figura 7.3". Si inserta otra figura, LaTeX actualizará la numeración de todas las figuras siguientes. ¿Pero qué pasa con las referencias? LaTeX gestiona todas nuestras referencias cruzadas y las actualizará. Por lo tanto, no debemos escribir una referencia simple manualmente como 7.3, sino asignar etiquetas internas a las que podamos hacer referencia cruzada más adelante.

En este capítulo, cubriremos lo siguiente:

- Establecimiento de etiquetas y referencias
- Uso de referencias avanzadas
- Hacer referencia a etiquetas en otros documentos
- Comprobación de etiquetas y referencias
- Convertir referencias en hipervínculos interactivos

Trabajaremos en esto mediante ejemplos prácticos.

---

### Establecimiento de etiquetas y referencias

Para hacer referencia a una parte específica de su documento, primero debe marcarla mediante una etiqueta (*label*). El nombre que asigne a esta etiqueta es el que usará más adelante para hacer referencia a ella.

Repasemos un ejemplo práctico. Compondremos una lista de los paquetes de LaTeX más utilizados, según una encuesta realizada en [https://latex.org](https://latex.org/). Usando el comando `\label`, marcaremos las posiciones a las que queremos hacer referencia más adelante usando el comando `\ref`. He aquí cómo:

1. Comience un nuevo documento de tipo `book`:

```latex
\documentclass{book}
\begin{document}
```

2. Inicie un capítulo y una sección, y agregue una etiqueta a esta sección:

```latex
\chapter{Statistics}
\section{Most used packages by LaTeX.org users}
\label{sec:packages}
```

3. Agregue algo de texto en el cuerpo y una nota al pie:

```latex
The Top Five packages, used by LaTeX.org members\footnote{according to the 2021 survey on LaTeX.org\label{fn:project}}:
```

4. Escriba una lista enumerada y coloque una etiqueta en algunos elementos:

```latex
\begin{enumerate}
  \item graphicx\label{item:graphicx}
  \item babel
  \item amsmath\label{item:amsmath}
  \item geometry
  \item hyperref
\end{enumerate}
```

5. Agregue otro capítulo con una etiqueta:

```latex
\chapter{Mathematics}
\label{maths}
```

6. Finalice con algo de texto y haga referencia a los elementos anteriores mediante los comandos `\ref` y `\pageref`:

```latex
\emph{amsmath}, on position \ref{item:amsmath} of the top list in section~\ref{sec:packages} on page~\pageref{sec:packages}, is indispensable to high-quality mathematical typesetting in \LaTeX. \emph{graphicx}, on position \ref{item:graphicx}, is for including images. See also the footnote \ref{fn:project} on page~\pageref{fn:project}.
\end{document}
```

7. Compile el documento y examine el resultado. La página 1 comienza con encabezados y una lista con viñetas:

> **Figura 7.1** – Primer capítulo

La página 1 termina con una nota al pie:

> **Figura 7.2** – Nota al pie

La página 2 está vacía ya que el Capítulo 2 comienza en una página de la derecha, que es la página 3:

> **Figura 7.3** – Referencias no resueltas

¿Ve los signos de interrogación? Aquí todavía faltan las referencias. Compile de nuevo y compare:

> **Figura 7.4** – Referencias resueltas

Creamos referencias cruzadas utilizando estos tres comandos:

- `\label` marca la posición
- `\ref` imprime el número del elemento asociado con una etiqueta
- `\pageref` imprime el número de página donde aparece esa etiqueta

Cada uno de estos comandos toma el nombre de la etiqueta como argumento. Podemos definir los nombres libremente.

Tuvimos que compilar dos veces porque LaTeX requiere una ejecución para generar las referencias que puede leer durante la siguiente ejecución de compilación. Si LaTeX aún no puede resolver una referencia, verá dos signos de interrogación en la salida.

Veamos ahora más de cerca cómo crear etiquetas de anclaje y hacer referencia a ellas de manera efectiva.

#### Asignación de una etiqueta

El comando `\label{name}` asigna la posición actual en el documento al nombre de la etiqueta. Precisamente, hace lo siguiente:

- Si utiliza el comando `\label` en texto regular, la etiqueta se refiere a la unidad seccional actual, como el capítulo o la sección
- Si el comando `\label` se utiliza dentro de un entorno numerado, como una figura, tabla o lista numerada, la etiqueta se referirá a ese entorno o elemento

Por lo tanto, no podemos etiquetar una sección dentro de un entorno de tabla. Para evitar problemas debidos a una ubicación potencialmente inadecuada, una buena regla general es colocar el comando `\label` justo después de la posición a la que nos gustaría hacer referencia. Por ejemplo, colóquelo directamente después del comando `\chapter` o `\section` correspondiente.

En los entornos de figuras o tablas, el comando `\caption` es implícitamente responsable de la numeración. Por eso `\label` debe colocarse después de `\caption`, no antes.

Los entornos flotantes pueden verse como sigue:

```latex
\begin{figure}[htbp!]
\centering
\includegraphics{filename}
\caption{Test figure}\label{fig:name}
\end{figure}
```

Así es como puede verse una tabla con una etiqueta:

```latex
\begin{table}[htbp!]
\centering
\caption{table descripion}\label{tab:name}
\begin{tabular}{cc}
…
\end{tabular}
\end{table}
```

Los nombres de las etiquetas pueden incluir letras, números y signos de puntuación, y distinguen entre mayúsculas y minúsculas (*case-sensitive*).

En documentos más extensos, el número de etiquetas podría ser muy elevado y la gestión de etiquetas se vuelve esencial. Para evitar conflictos de nombres, es una buena idea anteponer prefijos a las etiquetas según el tipo de entorno que representan. Se ha convertido en una práctica común etiquetar ecuaciones con `eq:name`, figuras con `fig:name`, tablas con `tab:name` y secciones con `sec:name`, con enfoques similares en otros casos. Tenga en cuenta que etiquetas como `fig:1` anulan el propósito, ya que la idea es evitar por completo establecer números manualmente.

En las siguientes secciones, analizaremos varias formas de hacer referencia a etiquetas.

#### Referencia directa a una posición etiquetada

Después de asignar una etiqueta con un nombre, podemos hacer referencia a ese nombre. Para esto, usamos el comando `\ref{name}`. Este comando imprime el número asociado con esa etiqueta, `name`, que puede ser, por ejemplo, el número de un entorno, un elemento de lista o un elemento de sección. Incluso podemos usar `\ref{name}` antes de que el comando `\label{name}` correspondiente aparezca en el código.

Aunque el mecanismo es simple, es bastante potente. Cada vez que compilamos un documento, LaTeX comprueba las etiquetas y reasigna los números, reflejando todos los cambios en la numeración. Si LaTeX detecta etiquetas modificadas, imprimirá un mensaje indicando que se requiere otra ejecución del compilador para actualizar las etiquetas correspondientes. En caso de duda, compile dos veces.

#### Referencia a una página

El comando `\pageref{name}` funciona de manera similar a `\ref`, pero en lugar de devolver un número para un elemento, como un entorno o una sección, imprime el número de página donde se estableció la etiqueta.

¿Seguirían siendo precisas todas las referencias si cambiáramos los números de sección y de página? Probemos eso. Inserte una sección ficticia y un salto de página al principio de nuestro capítulo, resaltado aquí:

```latex
\chapter{Statistics}
\section{Introduction}
\newpage
\section{Most used packages by LaTeX.org users}
\label{sec:packages}
```

Haga clic en **Typeset** una vez. LaTeX lo compilará, pero mostrará un mensaje:

```latex
LaTeX Warning: Label(s) may have changed. Rerun to get cross-references right.
```

¡Eso es lo que haremos! Haga clic en **Typeset** por segunda vez, y ahora todos los números se han ajustado correctamente a la sección 1.2 y la página 2:

> **Figura 7.5** – Referencias ajustadas automáticamente

Puede combinar ambos comandos. Si desea hacer referencia tanto a la sección como al número de página en una sola oración, puede escribir lo siguiente:

```latex
See figure~\ref{fig:name} on page~\pageref{fig:name}.
```

Como sabe cómo definir un comando, podría facilitar dicha referenciación:

```latex
\newcommand{\fullref}[1]{\ref{#1} on page~\pageref{#1}}
…
See figure~\fullref{fig:name}.
```

Esto le da una referencia completa, como *See Figure 4.2 on page 32*. Sin embargo, si la referencia, como la de una figura, aparece en la misma página, escribir el número de página parece un poco extraño. ¿Cómo podemos evitar eso? El paquete `varioref` ofrece una solución elegante. Nos centraremos en dichas referencias avanzadas en las siguientes secciones.

---

### Uso de referencias avanzadas

LaTeX ayuda a automatizar todo tipo de referencias. No se limita a la numeración. LaTeX incluso puede generar nombres y frases. Profundizaremos en eso aquí.

#### Producción de referencias de página inteligentes

El paquete `varioref` ofrece comandos para agregar "en la página anterior" (*on the preceding page*), "en la página siguiente" (*on the following page*) o el número de página a una referencia, según el contexto.

Utilizaremos los dos comandos de `varioref` para introducir referencias variables, `\vref` y `\vpageref`, para lograr textos de referencia mejorados, de la siguiente manera:

1. Abra nuestro ejemplo actual de la primera sección. Agregue el paquete `varioref` al preámbulo. Use la opción de paquete `nospace`, que asegura que `varioref` no inserte espacio adicional no deseado antes o después de una referencia:

```latex
\usepackage[nospace]{varioref}
```

2. Modifique el contenido del segundo capítulo en nuestro código de ejemplo:

```latex
\emph{amsmath}, on position \vref{item:amsmath} of the top list in section~\vref{sec:packages}, is indispensable to high-quality mathematical typesetting in \LaTeX. \emph{graphicx}, on position \vref{item:graphicx}, is for including images. See also the footnote \vref{fn:project}, that is, \vpageref{fn:project}.
```

3. Compile dos veces y observe el resultado:

> **Figura 7.6** – Una imagen en la parte inferior de la página

El comando `\vref` verificó la distancia desde la etiqueta de la sección referenciada. Como la etiqueta está en la página enfrentada (aquí, en la página anterior en un diseño a dos caras), `\vref` escribió *1.2 on the preceding page*.

`\vpageref` hace referencia a la página enfrentada al final del párrafo.

`\vref{name}` funciona de la siguiente manera:

- Si la referencia y `\label{name}` están en la misma página, se comporta exactamente como `\ref` y omite el número de página.
- Si la referencia y el `\label` correspondiente están en páginas adyacentes, `\vref` imprime el número referido y, adicionalmente, *on the preceding page*, *on the following page* o *on the facing page*. Elegirá esta última si el documento es a dos caras, es decir, si `\label` y la referencia caen en una doble página abierta.
- Si están más alejados, imprimirá tanto `\ref` como `\pageref`.

`\vpageref` es similar a `\pageref` pero se comporta como `\vref` en lo que respecta a la referencia de página.

`varioref` alterna entre diferentes redacciones para tener un poco de variación. Puede decir *following page* o *next page*, *preceding page* o *previous page*, *this page* o *current page*. Y en un diseño de doble página, cambia entre *facing page* y *preceding page* o *next page*. Con tal variación, el texto se lee de forma más natural. Puede ver esta redacción alterna en la Figura 7.6.

Incluso cuando use `varioref`, aún puede utilizar los comandos estándar `\ref` y `\pageref` junto con los nuevos comandos.

#### Ajuste fino de las referencias de página

Cuando una etiqueta y su referencia se encuentran cerca una de la otra, pueden caer en la misma página, pero no siempre. En tales casos, normalmente sabemos si la etiqueta aparece arriba o abajo de la referencia. El paquete `varioref` permite indicar esto mediante un argumento opcional para el comando `\vpageref`, como se muestra a continuación:

```latex
see the figure \vpageref[above]{fig:name}
```

Esto imprimirá lo siguiente:

- *see the figure above*, si la figura está en la misma página
- *see the figure on the page before*, si la figura está en la página anterior

Mientras que con el siguiente código, tendremos una salida diferente:

```latex
see the footnote \vpageref[below]{fn:name}
```

Esto en su lugar imprimirá lo siguiente:

- *see the footnote below*, si la nota al pie está en la misma página
- *see the footnote on the following page*, si la nota al pie está en la página siguiente

El comando `\vpageref` comprende dos argumentos opcionales. Mientras que en el primer argumento opcional podemos indicar una frase si la etiqueta y la referencia caen en la misma página, en el segundo argumento opcional podemos dar una frase para el caso en que la etiqueta y la referencia caigan en páginas diferentes. Por lo tanto, podríamos incluso escribir lo siguiente:

```latex
see the \vpageref[above figure][figure]{fig:name}
```

Esto imprimiría lo siguiente:

- *see the above figure*, si la figura está en la misma página
- *see the figure on the previous page*, si la figura está en la página anterior

Todo esto puede parecer un poco elaborado, pero sus exigencias pueden aumentar con el tiempo, requiriendo referencias más sofisticadas para que estas funciones puedan resultar útiles algún día.

#### Referencia a rangos de páginas

`varioref` ofrece dos comandos más:

- `\vpagerefrange[opt]{label1}{label2}`, donde `label1` y `label2` denotan un rango (como una secuencia de figuras desde `fig:a` hasta `fig:c`). Si ambas etiquetas caen en la misma página, el resultado es el mismo que con `\vpageref`. De lo contrario, la salida será un rango, como *on pages 32-36*. `opt` se usaría si ambas etiquetas caen en la página actual.
- `\vrefrange[opt]{label1}{label2}` es análogo a `\vref`: `see figures \vrefrange{fig:a}{fig:c}` puede dar como resultado *see figures 4.2 to 4.4 on pages 36-37*.

Visite [https://latexguide.org/chapter-07](https://latexguide.org/chapter-07) para ver ejemplos.

Puede encontrar más información sobre la personalización en el manual del paquete. Como de costumbre, puede abrirlo en el símbolo del sistema escribiendo `texdoc varioref` o visitando [https://texdoc.org/pkg/varioref](https://texdoc.org/pkg/varioref).

#### Uso de nombres de referencia automáticos

¿Cansado de escribir repetidamente `figure~\ref{fig:name}` y `table~\ref{tab:name}`? ¿No sería fantástico si LaTeX pudiera determinar automáticamente el tipo de elemento al que se refiere `\ref{name}` e insertar automáticamente el texto de referencia correcto con el nombre y número del elemento por usted? ¿Qué pasa si queremos abreviar, por ejemplo, `fig.~\ref{fig:name}` en todo el documento? El paquete `cleveref` lo hace fácil. Detecta automáticamente el tipo de referencia cruzada y el contexto en el que se utiliza.

Puede utilizar `\cref` o `\Cref` en lugar de `\ref`; elija este último si desea escribir con mayúscula inicial. Los comandos de rango correspondientes son `\crefrange` y `\Crefrange`.

Reescribamos nuestro primer ejemplo para hacer referencia usando `cleveref`. Para verificar que el paquete actúa bien, omitimos intencionalmente los prefijos en los nombres de etiquetas para `\label` y `\cref`, como se muestra aquí:

1. Modifique nuestro primer ejemplo de este capítulo de la siguiente manera. Las líneas modificadas están resaltadas:

```latex
\documentclass{book}
\usepackage{cleveref}
\crefname{enumi}{position}{positions}
\begin{document}
\chapter{Statistics}
\label{stats}
\section{Most used packages by LaTeX.org users}
\label{packages}
The Top Five packages, used by LaTeX.org members\footnote{according to the 2021 survey on LaTeX.org\label{project}}:
\begin{enumerate}
  \item graphicx\label{graphicx}
  \item babel
  \item amsmath\label{amsmath}
  \item geometry
  \item hyperref
\end{enumerate}
\chapter{Mathematics}
\label{maths}
\emph{amsmath}, on \cref{amsmath} of the top list in \cref{packages} of \cref{stats}, is indispensable to high-quality mathematical typesetting in \LaTeX. \emph{graphicx}, on \cref{graphicx}, is for including images. See also the \cref{project} on \cpageref{project}.
\end{document}
```

2. Haga clic en **Typeset** dos veces y compruebe que las referencias tengan los nombres correctos:

> **Figura 7.7** – Referencias automatizadas

Como podemos ver, no necesitamos especificar a qué objeto nos referimos. `\cref` siempre elige el nombre correcto y el número correcto para nosotros. Eso es realmente útil.

Usamos el comando `\crefname` para indicarle a `cleveref` qué nombre debe usar para los elementos enumerados. La definición de `\crefname` es la siguiente:

```latex
\crefname{type}{singular}{plural}
```

`type` puede ser uno de `chapter`, `section`, `figure`, `table`, `enumi`, `equation`, `theorem` u otros tipos que aún no hemos visto. `cleveref` usa la forma singular para referencias individuales y la versión plural para múltiples. Si necesita versiones en mayúsculas, use `\Crefname`. Por lo tanto, un uso típico puede ser el siguiente:

```latex
\crefname{figure}{fig.}{figs.}
\Crefname{figure}{Fig.}{Figs.}
```

También aquí podemos hacer referencia a rangos utilizando estos comandos:

- `\crefrange{label1}{label2}` para hacer referencia a un rango de referencias
- `\cpagerefrange{label1}{label2}` para hacer referencia a un rango de páginas

Quedará más claro con un ejemplo. Agreguemos esta línea a nuestro ejemplo actual:

```latex
See \crefrange{graphicx}{amsmath} and \cpagerefrange{stats}{maths}.
```

Esto nos da: *See positions 1 to 3 and pages 1 to 3*.

Podemos resumir los beneficios de la siguiente manera:

- Reduce la cantidad de escritura.
- Podríamos utilizar nombres de etiquetas arbitrarios. El paquete `fancyref` hace un trabajo similar pero depende de prefijos como `chap`, `fig` o `tab`.
- Si decidimos cambiar la redacción de la referencia, solo tenemos que hacerlo una vez en el preámbulo y se aplicará de manera coherente en todo el documento.

Dicho esto, sigue siendo una buena idea utilizar un prefijo como `fig:` o `sec:` para indicar el tipo de elemento referenciado. De esta manera, su código será más comprensible; por eso se considera una mejor práctica.

#### Combinación de referencias inteligentes con nomenclatura automática

Dado que el paquete `cleveref` es totalmente compatible con `varioref`, puede utilizar ambos para aprovechar al máximo sus características. `cleveref` redefine los comandos de `varioref` para utilizar internamente `\cref`. Por lo tanto, puede utilizar las funciones avanzadas de referencia de páginas de `varioref` junto con la automatización inteligente de nombres.

Simplemente cargue `varioref` antes de `cleveref`, como se muestra aquí:

```latex
\usepackage{varioref}
\usepackage{cleveref}
```

Ahora, puede usar `\vref`, `\cref`, `\ref` u otros comandos, el que mejor se adapte a sus necesidades.

#### Referenciación de nombres de secciones y leyendas

Hasta ahora, nuestras referencias solo han mostrado números. Si desea mostrar los nombres en su lugar, puede usar el paquete `nameref`. Comience cargándolo:

```latex
\usepackage{nameref}
```

Luego, use el comando `\nameref` en lugar de `\ref` o `\pageref`, o junto a estos comandos. En el primer ejemplo de este capítulo, puede escribir esto:

```latex
See section~\ref{sec:packages}, \nameref{sec:packages}, on page~\pageref{sec:packages}.
```

Esto le da: *See section 1.1, Most used packages by LaTeX.org users, on page 1*.

El comando `\nameref` funciona con comandos de sección regulares, incluidos `\part` y `\chapter`, así como con leyendas de figuras y tablas, elementos de listas de descripción y nombres de teoremas.

También podemos usar referencias a páginas, secciones y más en diferentes documentos. Echemos un vistazo más de cerca a esto en la siguiente sección.

---

### Hacer referencia a etiquetas en otros documentos

Cuando trabaje en múltiples documentos relacionados que se refieren entre sí, es posible que desee utilizar referencias a etiquetas de otro documento. El paquete llamado `xr` (abreviatura de *external references*) implementa esto. Primero, cargue el paquete `xr`:

```latex
\usepackage{xr}
```

Si necesita hacer referencia a secciones o entornos en un documento externo, digamos, `doc.tex`, inserte este comando en su preámbulo:

```latex
\externaldocument{doc}
```

Esto le permite hacer referencia adicionalmente a cualquier elemento al que se le haya asignado una etiqueta en `doc.tex`. Puede hacer esto para varios documentos. Si necesita evitar conflictos cuando un documento externo usa el mismo `\label` que el documento principal, declare un prefijo usando el argumento opcional de `\externaldocument`, que puede usar para agregar un prefijo. Por ejemplo, podemos usar `D-` como prefijo:

```latex
\externaldocument[D-]{doc}
```

De esta manera, todas las referencias de `doc.tex` tendrían el prefijo `D-`, y usted podría escribir `\ref{D-name}` para hacer referencia a `name` en `doc.tex`. En lugar de `D-`, puede elegir cualquier prefijo que haga que sus etiquetas sean únicas.

---

### Comprobación de etiquetas y referencias

Con el tiempo, su documento puede crecer, lo que dificulta recordar todos los nombres de las etiquetas y dónde hizo referencia a ellas. Afortunadamente, algunas herramientas facilitan su inspección y seguimiento.

#### Visualización de etiquetas

El paquete `showlabels` muestra las etiquetas que definió en su salida PDF para que pueda verlas junto a su texto. Simplemente cárguelo:

```latex
\usepackage{showlabels}
```

Cuando compile el mismo documento que usamos para la Figura 7.1, verá los nombres de las etiquetas para secciones, elementos y notas al pie directamente en la salida:

> **Figura 7.8** – Etiquetas mostradas

Esto puede resultar muy útil al escribir un documento más extenso. Solo asegúrese de eliminarlo o comentarlo antes de compilar y entregar su versión final.

Puede personalizar la apariencia de las etiquetas, como esto, por ejemplo, para verlas en rojo y negrita:

```latex
\renewcommand{\showlabelfont}{\small\bfseries\color{red}}
```

Otra opción es utilizar el paquete `showkeys`:

```latex
\usepackage{showkeys}
```

También muestra las etiquetas en el margen, donde las definió, pero adicionalmente muestra los nombres donde hace referencia a ellas, como esto:

> **Figura 7.9** – Referencias cruzadas mostradas

Esto también puede ayudarle a desarrollar su documento.

#### Identificación de etiquetas duplicadas

Las etiquetas están destinadas a ser identificadores únicos para que LaTeX pueda decidir de manera confiable a qué objeto debe apuntar un `\ref` o `\pageref`. Si usa el mismo nombre de etiqueta más de una vez, LaTeX emite una advertencia como *Label name multiply defined*. La consecuencia de tales etiquetas duplicadas es que las referencias cruzadas pueden apuntar silenciosamente a la sección, figura, tabla o ecuación incorrecta. LaTeX no detiene la compilación, pero el resultado puede ser incoherente o engañoso.

La advertencia se escribe en el archivo `.log` y cualquier editor de LaTeX serio mostrará las etiquetas duplicadas como advertencias, lo que facilita su localización y corrección.

Anteponer a las etiquetas su tipo (`sec:`, `fig:`, `tab:`, `eq:`), como se mencionó anteriormente en este capítulo, reduce drásticamente las colisiones en documentos más extensos.

#### Verificación de referencias

Para verificar si todas las etiquetas y referencias en su documento se están utilizando realmente, puede cargar el paquete `refcheck`. Le ayuda a identificar etiquetas no utilizadas, ecuaciones no referenciadas y referencias faltantes. Digamos que agregó `\label{item:hyperref}`, pero nunca hizo referencia a ella.

Simplemente cargue el paquete:

```latex
\usepackage{refcheck}
```

Verá los nombres de las etiquetas utilizadas, y cualquier etiqueta no utilizada aparecerá con signos de interrogación, lo que facilita su detección:

> **Figura 7.10** – Resaltado de etiquetas sin referencia

En la siguiente sección, veremos cómo hacer que las referencias sean interactivas para que los lectores puedan saltar directamente al elemento referenciado.

---

### Convertir referencias en hipervínculos interactivos

El formato PDF puede incluir enlaces interactivos y marcadores. ¿Qué tal explorar eso? Hay un paquete sobresaliente que ofrece soporte para hipervínculos: el paquete `hyperref`.

Pruébelo cargando `hyperref` justo antes de `cleveref`. Este orden es esencial para que las referencias funcionen porque `cleveref` detecta si se ha cargado `hyperref` y convierte las referencias en hipervínculos. Incluso sin opciones ni comandos, su documento tendrá todos los hipervínculos posibles debido a lo siguiente:

- Todas las referencias se convierten en hipervínculos. Haga clic en cualquiera de esos números para saltar a la tabla, elemento de lista, sección o página referenciada.
- Cada marca de nota al pie es un hipervínculo al texto de la nota al pie. Haga clic en ella para saltar allí.
- Si inserta `\tableofcontents`, obtendrá una lista de marcadores para los documentos, capítulos y secciones enumerados en una barra de navegación de su lector de PDF.

`hyperref` puede hacer aún más por usted: vincular entradas de índice a pasajes de texto, referencias inversas de entradas bibliográficas y más. Puede personalizar finamente el comportamiento mediante opciones como, por ejemplo, elegir el color o los marcos para los hipervínculos. Por lo tanto, debe tener en cuenta este valioso paquete. En el [Capítulo 12](https://subscription.packtpub.com/book/business-and-other/9781805804574/12), *Uso de hipervínculos y diseño de encabezados*, volveremos a este tema.

Por un lado, `hyperref` detecta muchos otros paquetes, como `varioref`, y puede convertir sus comandos en hipervínculos; por eso debemos cargar `hyperref` después de la mayoría de los demás paquetes. Por otro lado, algunos paquetes excepcionales, como `cleveref`, detectan funciones de `hyperref` y se basan en ellas; en tales casos, debemos cargarlos después de `hyperref`. Por lo tanto, si combina `varioref`, `cleveref` y `hyperref`, el orden de carga de paquetes debe ser el siguiente:

```latex
\usepackage[nospace]{varioref}
\usepackage{hyperref}
\usepackage{cleveref}
```

El manual del paquete `hyperref` tiene una sección completa sobre la compatibilidad con otros paquetes y el orden de carga requerido. Ábralo ingresando `texdoc hyperref` en el símbolo del sistema o visite [https://texdoc.org/pkg/hyperref](https://texdoc.org/pkg/hyperref). La mayoría de las veces, `hyperref` debe cargarse en último lugar, con algunas excepciones mencionadas en el manual.

---

### Resumen

En este capítulo, analizamos cómo hacer referencia a capítulos, secciones, notas al pie y entornos por su número o por el número de la página correspondiente.

Al utilizar etiquetas y nombres para hacer referencias, no necesitamos especificar un número nosotros mismos; LaTeX determina el número de página, número de sección, número de nota al pie o número de entorno correcto por nosotros.

También aprendió algunas formas innovadoras de manejar referencias según el contexto.

En el próximo capítulo, pasaremos a trabajar con listas, que consisten principalmente en referencias: tablas de contenidos, listas de figuras y tablas, y bibliografías.
