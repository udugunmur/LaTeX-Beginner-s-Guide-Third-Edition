# LaTeX Beginner's Guide
## Capítulo 4: Creación de Listas

En los capítulos anteriores, nos enfocamos en el formateo, tanto a nivel de texto como a lo largo de páginas completas. Ahora, nos dirigimos a estructurar el contenido de manera más precisa. A lo largo de los dos capítulos siguientes, analizaremos cómo organizar la información mediante listas y tablas. Comenzaremos con las listas.

Las listas son una forma eficaz y amigable para el lector de presentar información. Puede resaltar puntos clave en un formato que sea fácil de escanear y comprender. Los tres tipos de listas más comunes son los siguientes:

- **Listas con viñetas**: Se utilizan para enfatizar puntos distintos que destacan del texto principal
- **Listas numeradas**: Ideales para presentar puntos en un orden específico
- **Listas de definiciones**: Se utilizan para explicar términos o conceptos de manera estructurada

En este capítulo, aprenderá a crear cada uno de estos tipos de listas. Cubriremos lo siguiente:

- Construcción de listas
- Personalización de listas

Comenzaremos creando listas básicas y luego pasaremos a personalizar su apariencia y estructura.

---

### Construcción de listas

Comenzaremos con listas desordenadas utilizando viñetas para organizar los elementos. A continuación, trataremos con listas ordenadas que utilizan números o letras para indicar una secuencia. Por último, veremos las listas de definiciones para presentar palabras clave junto con sus correspondientes explicaciones.

#### Creación de una lista con viñetas

Comencemos con el tipo de lista más básico: una lista con viñetas. Contiene solo los elementos sin números, donde cada elemento está marcado con un símbolo de viñeta. Esa es una forma mucho más clara de presentar puntos clave que comprimirlos en una oración larga dentro del texto de un párrafo.

Como ejemplo, crearemos una lista de paquetes de LaTeX relacionados con el diseño introducidos en el capítulo anterior. Siga estos pasos:

1. Cree un nuevo documento con algo de texto introductorio:

```latex
\documentclass{article}
\begin{document}
\section*{Useful packages}
LaTeX provides several packages for designing the layout:
```

2. Ahora añada la lista, utilizando un entorno `itemize` y comandos `\item`:

```latex
\begin{itemize}
  \item geometry
  \item typearea
  \item fancyhdr
  \item scrpage-scrlayer
  \item setspace
\end{itemize}
```

3. Eso fue fácil. Ahora podemos terminar el documento:

```latex
\end{document}
```

4. Haga clic en **Typeset** y observe el resultado:

> **Figura 4.1** – Una lista con viñetas

Comenzamos con un encabezado de sección seguido de algo de texto introductorio. Para crear la lista en sí, utilizamos un entorno llamado `itemize`. Como ya aprendió sobre los entornos en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*, `\begin{itemize}` lo inicia y `\end{itemize}` lo finaliza. El comando `\item` le indica a LaTeX que agregue un nuevo elemento a la lista. `\item` funciona solo dentro de un entorno de lista. Cada elemento puede incluir texto de cualquier longitud e incluso abarcar múltiples párrafos. Bueno, eso es bastante fácil.

Cuando una lista crece, podríamos mejorar la claridad dividiéndola. Podemos crear listas dentro de una lista. Es aconsejable utilizar diferentes viñetas para distinguir fácilmente entre los niveles de la lista. LaTeX hace esto por nosotros automáticamente.

Para ilustrar esto con nuestro ejemplo, mejoremos nuestra lista de paquetes agrupando elementos relacionados en categorías temáticas. He aquí cómo:

1. Modifique el entorno `itemize` de nuestro ejemplo de la siguiente manera: cree una lista `itemize` para cada tema e inclúyala dentro de un `\item`. El código actualizado se ve así:

```latex
\begin{itemize}
  \item Page layout
    \begin{itemize}
      \item geometry
      \item typearea
    \end{itemize}
  \item Headers and footers
    \begin{itemize}
      \item fancyhdr
      \item scrpage-scrlayer
    \end{itemize}
  \item Line spacing
    \begin{itemize}
      \item setspace
    \end{itemize}
\end{itemize}
```

Tenga en cuenta que cerramos cuidadosamente cada entorno.

2. Compile el documento para ver la nueva lista:

> **Figura 4.2** – Una lista con viñetas con dos niveles

Aquí, colocamos listas dentro de un punto `\item` dentro de una lista, creando una lista anidada. LaTeX admite hasta cuatro niveles de anidamiento. Si excediéramos este límite, LaTeX generaría un error:

```latex
! LaTeX Error: Too deeply nested.
```

Los siguientes son los valores predeterminados:

- Los elementos de primer nivel usan viñetas
- Los elementos de segundo nivel usan guiones anchos
- Los elementos de tercer nivel están marcados con un símbolo de asterisco (*)
- Los elementos de cuarto nivel usan puntos centrados

Las listas profundamente anidadas rara vez se utilizan; tales estructuras complicadas pueden ser difíciles de seguir. Si su lista se vuelve demasiado compleja, considere reestructurarla o dividirla.

En el código fuente de nuestro ejemplo, sangramos cada línea dentro del entorno `itemize`. Cuando hay otro entorno `itemize` dentro de un entorno `itemize` circundante, las líneas `\item` están aún más sangradas. Esto facilita identificar el nivel de anidamiento de un vistazo. Si bien LaTeX no requiere sangría, una sangría adecuada dentro de los entornos ayuda a mantener el código, ya que mejora significativamente su legibilidad y estructura. Puede ver rápidamente dónde comienzan y terminan los entornos. Sangrar las líneas de código fuente dentro de un entorno es un muy buen hábito en general. También puede sangrar líneas de código para indicar que pertenecen a alguna línea principal, como con un punto `\item` que abarca varias líneas, lo que veremos en la siguiente sección.

El uso de espacios o tabulaciones para sangrar el código fuente mejora la legibilidad del código. Eso no tiene ningún impacto en el resultado, ya que LaTeX trata los múltiples caracteres de espacio en blanco en una línea de código como un solo espacio.

En la siguiente sección, veremos cómo listar puntos clave en una secuencia específica y numerarlos.

#### Construcción de una lista numerada

Las listas con viñetas funcionan bien cuando el orden de los elementos no importa. Sin embargo, si el orden es esencial, podríamos organizar los elementos dándoles números y creando una lista ordenada. De esta manera, guía al lector para seguir la progresión lógica fácilmente.

Preparemos un breve tutorial paso a paso para configurar el diseño de la página utilizando una lista numerada. Siga estos pasos:

1. Abra un nuevo documento e introduzca el siguiente código:

```latex
\documentclass{article}
\begin{document}
\begin{enumerate}
  \item State the paper size by an option to the document class
  \item Determine the margin dimensions using one of these packages:
    \begin{itemize}
      \item geometry
      \item typearea
    \end{itemize}
  \item Customize header and footer by one of these packages:
    \begin{itemize}
      \item fancyhdr
      \item scrpage-scrlayer
    \end{itemize}
  \item Adjust the line spacing for the whole document
    \begin{itemize}
      \item by using the setspace package
      \item or by the command \verb|\linespread{factor}|
    \end{itemize}
\end{enumerate}
\end{document}
```

2. Haga clic en **Typeset** para compilar y generar estas instrucciones:

> **Figura 4.3** – Una lista numerada con listas con viñetas

Utilizamos un entorno `enumerate` de manera muy similar al entorno `itemize`, con cada entrada de la lista comenzando con el comando `\item`. La principal diferencia es que cada línea `\item` en nuestro entorno `enumerate` se numera automáticamente en lugar de tener solo una viñeta delante. Nuevamente, anidamos dos listas, demostrando esta vez que podemos hacerlo incluso cuando las listas son de diferentes tipos. El anidamiento mixto puede extenderse más allá de cuatro niveles, pero cuatro es el máximo para cada tipo de lista, y se permite un total de seis niveles para listas mixtas.

El estilo de numeración predeterminado para el entorno `enumerate` es el siguiente:

- **Primer nivel**: 1., 2., 3., 4., …
- **Segundo nivel**: (a), (b), (c), (d), …
- **Tercer nivel**: i., ii., iii., iv., …
- **Cuarto nivel**: A., B., C., D., …

El comando `\item` también puede tomar un argumento opcional. Si escribe `\item[texto]`, LaTeX imprimirá el texto en lugar del número predeterminado o una viñeta. De esta manera, podría usar cualquier numeración y cualquier símbolo para reemplazar la viñeta.

Ahora que hemos cubierto las listas con viñetas y numeradas, veamos un tipo de lista que podemos usar para componer tipográficamente descripciones de múltiples elementos.

#### Producción de una lista de definiciones

Pasaremos ahora al tercer tipo de lista, a saber, las listas de definiciones, también conocidas como listas de descripciones. En este formato, cada elemento de la lista comienza con un término o frase, seguido de su correspondiente explicación.

Para ilustrar esto, volveremos a nuestro tema familiar de paquetes de LaTeX. Esta vez, en lugar de simplemente listar los paquetes, proporcionaremos una breve descripción de cada uno. Escojamos algunos de [https://ctan.org/topic/list](https://ctan.org/topic/list), que es una colección de paquetes relacionados con listas. Esto también nos servirá en la siguiente sección, *Personalización de listas*, donde trabajaremos con los mismos paquetes para demostrar las características de personalización.

Comencemos escribiendo un breve resumen de lo que puede hacer cada paquete. Siga estos pasos:

1. Usaremos un entorno `description`. Cree un documento con el siguiente código:

```latex
\documentclass{article}
\begin{document}
\begin{description}
  \item[paralist] provides compact lists and list versions that can be used within paragraphs, helps to customize labels and layout.
  \item[enumitem] gives control over labels and lengths in all kind of lists.
  \item[mdwlist] is useful to customize description lists, it even allows multi-line labels. It features compact lists and the capability to suspend and resume.
  \item[desclist] offers more flexibility in definition list.
  \item[multenum] produces vertical enumeration in multiple columns.
\end{description}
\end{document}
```

2. Compile el documento para obtener la lista de definiciones:

> **Figura 4.4** – Una lista de definiciones

Utilizamos el entorno `description` de la misma manera que los otros entornos de listas, excepto que usamos el argumento opcional de `\item` entre corchetes. En el entorno `description`, LaTeX muestra automáticamente este argumento en negrita.

En comparación con una lista con viñetas, los símbolos de viñeta se reemplazan con palabras clave o términos en negrita.

También podemos ajustar el espaciado de nuestras listas, seleccionar símbolos de viñetas y modificar el estilo de numeración. Veamos esto en la siguiente sección.

---

### Personalización de listas

De forma predeterminada, las listas de LaTeX vienen con configuraciones sensatas de espaciado, sangría y símbolos. Sin embargo, en algunos casos, es posible que desee ajustar el estilo de enumeración, cambiar los símbolos de viñeta o afinar el interlineado y la sangría. Algunos paquetes ayudan a ahorrar espacio y a personalizar la apariencia de la lista. Comencemos mirando el espaciado.

#### Obtención de listas compactas

Una pregunta común al escribir con LaTeX es cómo hacer que las listas ocupen menos espacio. Por defecto, LaTeX deja un espaciado generoso dentro y alrededor de las listas, lo que puede parecer excesivo. Ahora veremos cómo reducirlo.

Reduzcamos el espaciado en nuestra lista de la Figura 4.3. Eliminaremos el espacio adicional entre los elementos de la lista y alrededor de toda la lista. Siga estos pasos:

1. En nuestro ejemplo de lista numerada que produjo la Figura 4.3, incluya el paquete `paralist` y reemplace `enumerate` por `compactenum`, e `itemize` por `compactitem`:

```latex
\documentclass{article}
\usepackage{paralist}
\begin{document}
\begin{compactenum}
  \item State the paper size by an option to the document class
  \item Determine the margin dimensions using one of these packages:
    \begin{compactitem}
      \item geometry
      \item typearea
    \end{compactitem}
  \item Customize header and footer by one of these packages:
    \begin{compactitem}
      \item fancyhdr
      \item scrpage-scrlayer
    \end{compactitem}
  \item Adjust the line spacing for the whole document
    \begin{compactitem}
      \item by using the setspace package
      \item or by the command \verb|\linespread{factor}|
    \end{compactitem}
\end{compactenum}
\end{document}
```

2. Compile y compare el espaciado:

> **Figura 4.5** – Una lista compacta

3. Ahora extienda el elemento de lista resaltado para `setspace` de la siguiente manera:

```latex
\item by using the setspace package and one of its options:
  \begin{inparaenum}
    \item singlespacing
    \item onehalfspacing
    \item double spacing
  \end{inparaenum}
```

4. Compile y observe el cambio en el tema del interlineado:

> **Figura 4.6** – Una lista dentro de un párrafo

El paquete `paralist` proporciona varios entornos de listas alternativos diseñados para componerse dentro de párrafos o con un aspecto muy compacto. Cargamos este paquete y reemplazamos los entornos estándar con sus contrapartes compactas: `enumerate` por `compactenum`, e `itemize` por `compactitem`. Si bien la sintaxis es básicamente la misma, los nuevos entornos no producen espacio en blanco vertical adicional antes ni después de una lista. Tampoco agregan espacio vertical alrededor de los elementos de la lista, lo que resulta en un diseño más ajustado. Las listas y los elementos se utilizan con el mismo interlineado que el texto normal. Finalmente, se ve mucho más compacto y ahorra espacio. En el paso 3, usamos el nuevo entorno `inparaenum`, donde los elementos están numerados pero permanecen integrados (*inline*) dentro del mismo párrafo.

Para cada tipo de lista estándar, el paquete `paralist` ofrece tres entornos alternativos compactos correspondientes.

Para listas con viñetas, introduce los siguientes entornos:

- `compactitem`: Una alternativa que ahorra espacio al entorno `itemize` que elimina el espacio vertical antes y después de la lista, y entre sus elementos
- `inparaitem`: Una lista con viñetas formateada en línea dentro de un párrafo, rara vez vista impresa
- `asparaitem`: Cada elemento de la lista se formatea como un párrafo regular de LaTeX separado, pero comienza con una viñeta

Para listas numeradas, proporciona los siguientes tipos de lista:

- `compactenum`: Una versión compacta del entorno `enumerate`, sin espacio vertical adicional antes o después de la lista ni entre sus elementos
- `inparaenum`: Una lista enumerada que aparece en línea dentro de un párrafo
- `asparaenum`: Cada elemento de la lista se distribuye como un párrafo regular de LaTeX, pero está numerado

Para listas de descripciones, añade los siguientes tipos:

- `compactdesc`: Una versión compacta del entorno `description`, eliminando el espacio vertical adicional antes y después de la lista y entre sus elementos
- `inparadesc`: Una lista de descripciones que cabe dentro de un párrafo
- `asparadesc`: Cada elemento de la lista se formatea como un párrafo regular de LaTeX, comenzando con la palabra clave o término en negrita, como en una lista de descripciones

Ahora que hemos ajustado el espaciado, veamos cómo modificar los símbolos de viñeta y los estilos de numeración.

#### Elección de viñetas y formato de numeración

Para cumplir con las convenciones lingüísticas o pautas de formato específicas, es posible que desee numerar los elementos de la lista utilizando números romanos o letras, encerrarlos entre paréntesis o seguirlos con puntos. Algunos usuarios también prefieren usar guiones en lugar de las viñetas predeterminadas. El paquete `enumitem` ofrece funciones flexibles para lograr todo esto.

Trabajemos en esto y cambiemos el estilo de numeración. Aplicaremos una numeración alfabética con letras en círculos. Además, cambiaremos el símbolo de viñeta predeterminado por un guion. Para lograr esto, siga estos pasos:

1. Ahora usaremos el paquete `enumitem` en lugar de `paralist`. Utilizaremos una sangría adecuada dentro de los entornos y volveremos a la sintaxis de lista estándar. Sin embargo, para mantener el diseño compacto, agregaremos la opción `nosep` a las listas:

```latex
\documentclass{article}
\usepackage{enumitem}
\setlist{nosep}
\setitemize[1]{label=---}
\setenumerate[1]{label=\textcircled{\scriptsize\Alph*}, font=\sffamily}
\begin{document}
\begin{enumerate}
  \item State the paper size by an option to the document class
  \item Determine the margin dimensions using one of these packages:
    \begin{itemize}
      \item geometry
      \item typearea
    \end{itemize}
  \item Customize header and footer by one of these packages:
    \begin{itemize}
      \item fancyhdr
      \item scrpage-scrheader
    \end{itemize}
  \item Adjust the line spacing for the whole document
    \begin{itemize}
      \item by using the setspace package
      \item or by the command \verb|\linespread{factor}|
    \end{itemize}
\end{enumerate}
\end{document}
```

2. Compile y compruebe el resultado:

> **Figura 4.7** – Una lista enumerada personalizada

Usamos comandos del paquete `enumitem` para personalizar el comportamiento de las listas. Miremos más de cerca:

- `\setlist{nosep}`: El comando `\setlist` aplica propiedades válidas para todos los tipos de listas. Aquí, especificamos la opción `nosep` para lograr listas muy compactas similares al entorno compacto de `paralist`. Esa configuración elimina todo el espaciado vertical adicional.
- `\setitemize[1]{label=---}`: El comando `\setitemize` personaliza las listas con viñetas. Aquí, elegimos un guion largo (*em dash*) (`---`) como etiqueta para obtener un guion ancho inicial.
- `\setenumerate[1]{label=\textcircled{\scriptsize\Alph*}, font=\sffamily}`: El comando `\setenumerate` personaliza las listas numeradas. Lo usamos para establecer una etiqueta y una fuente para la etiqueta. El comando `\Alph*` significa enumeración en letras mayúsculas.

También podemos aplicar estas opciones localmente entre corchetes. Otros ejemplos son los siguientes:

- `\begin{itemize}[noitemsep]` genera una lista con viñetas compacta sin ningún espacio adicional entre elementos y párrafos
- `\begin{enumerate}[label=\Roman*.,start=3]` hace que la lista se numere con III., IV., y así sucesivamente
- `\begin{enumerate}[label=\alph*)],nolistsep]` produce una lista muy compacta numerada como a), b), c), y así sucesivamente

Estos son comandos de etiquetado útiles para personalizar listas numeradas:

- `\arabic*`: 1, 2, 3, 4, …
- `\alph*`: a, b, c, d, …
- `\Alph*`: A, B, C, D, …
- `\roman*`: i, ii, iii, iv, …
- `\Roman*`: I, II, III, IV, …

El asterisco `*` representa el valor actual del contador de la lista. Puede agregar libremente paréntesis, puntuación u otras decoraciones. Más adelante en este libro, verá cómo seleccionar entre miles de símbolos para etiquetas y viñetas.

Por conveniencia, también existe una sintaxis corta: si carga el paquete `enumitem` con la opción `shortlabels`, puede usar una sintaxis compacta como `\begin{enumerate}[(i)]`, `\begin{enumerate}[(1)]` donde `1`, `a`, `A`, `i` e `I` corresponden a `\arabic*`, `\alph*`, `\Alph*`, `\roman*` y `\Roman*`, respectivamente. Esto permite una rápida personalización. Sin embargo, considere usar comandos globales para mantener un formato coherente en todo el documento.

En este ejemplo, el comando `\verb|code|` compone el código literalmente (*verbatim*), "tal como es", sin interpretarlo como código LaTeX. En lugar de `|`, podemos elegir cualquier carácter como delimitador. Tenga en cuenta que `\verb` no se puede utilizar en argumentos de comandos como `\section` y `\footnote`, ni en encabezados de tablas. Para bloques más largos de dicho texto literal, use el entorno `verbatim`.

Pasemos a otra característica útil del paquete.

#### Suspensión y continuación de listas

El paquete `enumitem` que usamos anteriormente también le permite continuar con la numeración de listas. Desarrollemos el ejemplo anterior para ver cómo funciona:

1. Justo encima de la línea de código resaltada (`\item Adjust the line spacing...`), inserte estas líneas para finalizar el entorno `enumerate` y continuar con algo de texto normal:

```latex
\end{enumerate}
\noindent\textbf{Tweaking the line spacing:}
```

2. A continuación, reinicie el entorno `enumerate` con esta línea:

```latex
\begin{enumerate}[resume]
```

3. Deje el resto del código, incluidos los otros elementos, sin cambios. Compile el documento para ver el resultado:

> **Figura 4.8** – Una lista reanudada

En el paso 1, terminamos temporalmente la lista y continuamos con texto regular. En el paso 2, reiniciamos la lista utilizando la opción `resume`, que le indica a `enumitem` que continúe la lista anterior con el siguiente número. La versión con asterisco, `resume*`, también utilizaría las opciones de la lista anterior, si se proporcionaron.

#### Examen del diseño de listas

LaTeX proporciona diseños predeterminados sensatos para las listas; sin embargo, puede haber ocasiones en las que desee modificar este diseño, como ajustar los márgenes o la sangría de los elementos. Todas las dimensiones del diseño están determinadas por macros de LaTeX, las llamadas longitudes (*lengths*).

Existe un paquete que es excelente para visualizar diseños, que presenta estas macros de longitud. Se llama `layouts`. Usémoslo para examinar las dimensiones de las listas de LaTeX. Usaremos este breve documento:

```latex
\documentclass[12pt]{article}
\usepackage{layouts}
\begin{document}
\listdiagram
\end{document}
```

Simplemente compilándolo, obtendremos el siguiente diagrama:

> **Figura 4.9** – El diseño de listas

¿No es impresionante? El paquete `layouts` puede hacer aún más, de lo cual puede leer en su documentación en [https://texdoc.org/pkg/layouts](https://texdoc.org/pkg/layouts) o ejecutando `texdoc layouts` en la línea de comandos.

Utilice el comando de LaTeX `\setlength` para personalizar esas longitudes; por ejemplo, `\setlength{\labelwidth}{2cm}`. Aplicarlas a listas individuales y a ciertas profundidades de anidamiento es difícil. Si necesita modificar el diseño de la lista, el paquete `enumitem` vuelve a ser de gran ayuda. Podemos usar sus comandos, como `\setlist` y su interfaz `clave=valor`, para ajustar las longitudes, como se muestra en el diagrama anterior.

Por ejemplo, si quisiéramos eliminar el espacio entre los elementos de la lista en el entorno `description` y reducir el margen izquierdo, podríamos cargar el paquete `enumitem` y escribir lo siguiente:

```latex
\setdescription{itemsep=0cm,parsep=0cm,leftmargin=0.5cm}
```

Tenga en cuenta que no usamos la barra invertida para las claves. De manera similar, `\setitemize`, `\setenumerate` y `\setlist` se pueden usar para afinar detalles. Intente asignar valores usted mismo y pruebe el efecto en nuestros ejemplos. Si desea obtener más información, eche un vistazo a la documentación de `enumitem` en [https://texdoc.org/pkg/enumitem](https://texdoc.org/pkg/enumitem) o ejecutando `texdoc enumitem` en el símbolo del sistema.

---

### Resumen

En este capítulo, exploramos las listas como un medio para organizar nuestro contenido. Específicamente, cubrimos cómo crear listas con viñetas, listas numeradas y listas de definiciones. Además, trabajamos con versiones compactas y personalizadas de dichas listas, incluidos ajustes de espaciado, así como interrupción y reanudación.

Dichas listas pueden ayudar a clarificar y presentar sus ideas de manera más efectiva. A continuación, dirigiremos nuestra atención a las tablas para componer datos estructurados en filas y columnas.
