# LaTeX Beginner's Guide
## Capítulo 8: Gestión de Contenidos, Índices y Bibliografía

Hasta ahora, ha aprendido cómo estructurar y formatear documentos, crear tablas e imágenes y conectar sus partes mediante referencias cruzadas. Este capítulo muestra cómo LaTeX se basa en eso recopilando y presentando automáticamente el contenido de un documento en tablas de contenidos, figuras, tablas, índices y bibliografías. LaTeX facilita la creación de todo tipo de listas con referencias cruzadas. Por ejemplo, ya hemos visto que usar simplemente el comando `\tableofcontents` le brinda una tabla de contenidos (TOC) limpia y bien formateada. Recopila automáticamente los encabezados de capítulos y secciones, junto con sus números de página, y genera una lista ordenada.

Una tabla de contenidos y un índice ayudan a los lectores a navegar por un documento. Una lista de tablas y una lista de figuras funcionan de la misma manera. Los artículos académicos y los libros a menudo incluyen una lista de otras obras para citar sus fuentes o respaldar el tema. Si esta lista contiene solo obras citadas, a menudo la llamamos lista de referencias; si también contiene obras no citadas pero relevantes, la llamamos bibliografía.

Al final de este capítulo, sabrá cómo crear y personalizar todas estas listas.

Esto es lo que cubriremos:

- Personalización de la tabla de contenidos
- Generación de un índice
- Creación de una bibliografía
- Adición de un glosario
- Cambio de los encabezados

Comencemos con los contenidos.

---

### Personalización de la tabla de contenidos

Simplemente escribir el comando `\tableofcontents` produce una lista de contenidos prediseñada. Pero LaTeX también nos permite afinar su apariencia y estructura. Veamos cómo.

Crearemos un breve documento de ejemplo que sirva como nuestro archivo de prueba a lo largo de este capítulo. Contendrá algunos encabezados para que podamos experimentar con la tabla de contenidos y aprender a ajustarla. Lo modificaremos para que sea más matizado e incluya entradas adicionales.

En el [Capítulo 3](https://subscription.packtpub.com/book/business-and-other/9781805804574/3), *Diseño de páginas*, vimos lo que sucede cuando usamos el comando `\tableofcontents`. LaTeX recopila todas las entradas de los encabezados y las enumera automáticamente. Esta vez, incluiremos encabezados hasta el nivel de subsubsección y agregaremos algunas entradas manuales. Comencemos construyendo el documento base:

1. Comience un nuevo documento de tipo `book`:

```latex
\documentclass{book}
```

2. Establezca el valor de profundidad de la tabla de contenidos en 3 para incluir encabezados hasta el nivel de subsubsección:

```latex
\setcounter{tocdepth}{3}
```

3. Comience el documento:

```latex
\begin{document}
```

4. Imprima la tabla de contenidos al principio:

```latex
\tableofcontents
```

5. Escriba encabezados en todos los niveles que desee. Use `\addcontentsline` o `\addtocontents` para agregar algo a la tabla de contenidos manualmente:

```latex
\part{First Part}
\chapter*{Preface}
\addcontentsline{toc}{chapter}{Preface}
\chapter{First main chapter}
\section{A section}
\section{Another section}
\subsection{A smaller section}
\subsubsection[Deeper level]{This section has an even deeper level}
\chapter{Second main chapter}
\part{Second part}
\chapter{Third main chapter}
```

6. Finalice con un apéndice que tenga sus propios capítulos:

```latex
\appendix
\cleardoublepage
\addtocontents{toc}{\bigskip}
\addcontentsline{toc}{part}{Appendix}
\chapter{Glossary}
\chapter{Symbols}
\end{document}
```

7. Haga clic en **Typeset** para compilar. La primera página mostrará *Contents*, pero no aparecerá ninguna entrada.
8. Haga clic en **Typeset** por segunda vez. Ahora podemos ver la tabla de contenidos:

> **Figura 8.1** – Un ejemplo de tabla de contenidos

Estructuramos un documento utilizando varios comandos de sección. LaTeX lee todos nuestros comandos de sección durante la primera ejecución y crea un archivo `.toc` que almacena todos los encabezados. Durante la primera ejecución, ese archivo aún no existía; por lo tanto, la tabla de contenidos permaneció vacía. La segunda ejecución lee este archivo e imprime la tabla de contenidos final.

En nuestro ejemplo, aumentamos la profundidad de la tabla de contenidos en 1 nivel. Agregamos una entrada tipo capítulo para el prefacio e insertamos un encabezado tipo parte para el comienzo del apéndice, usando el comando `\addcontentsline`. A través del comando `\addtocontents`, insertamos algo de espacio antes del encabezado. En las siguientes secciones, analizaremos más de cerca estos comandos y aprenderemos cómo personalizar la tabla de contenidos.

#### Ajuste de la profundidad de la tabla de contenidos

Cada comando de sección en LaTeX tiene un nivel de TOC asociado. Estos niveles determinan qué encabezados aparecen en la tabla de contenidos. Estos son los valores para los comandos de sección estándar:

- `\part`: -1 en las clases `book` y `report`, y 0 en la clase `article`
- `\chapter`: 0 (excepto en la clase `article`, ya que no hay capítulos con `article`)
- `\section`: 1
- `\subsection`: 2
- `\subsubsection`: 3
- `\paragraph`: 4
- `\subparagraph`: 5

En las clases `book` y `report`, LaTeX crea entradas de tabla de contenidos hasta el nivel 2 (es decir, hasta el nivel `\subsection`). En la clase `article`, LaTeX crea entradas de tabla de contenidos hasta el nivel 3 de forma predeterminada, es decir, hasta el nivel `\subsubsection`. En un libro, esto significa, por ejemplo, que `\subsubsection` no genera una entrada en la tabla de contenidos. Hay una variable que representa el nivel, a saber, `\tocdepth`. Es una variable entera, a la que llamamos contador (*counter*). Para indicarle a LaTeX que incluya subsubsecciones en la tabla de contenidos, tendríamos que aumentar este contador. Hay dos formas básicas de ajustar el valor de un contador:

- `\setcounter{name}{n}` especifica un valor entero `n` para el contador `name`.
- `\addtocounter{name}{n}` suma el valor entero de `n` al valor del contador `name`. Para disminuir un contador, elija un valor negativo para `n`.

Por ejemplo, el siguiente comando hace que LaTeX incluya incluso encabezados de `\subparagraph` en la tabla de contenidos:

```latex
\setcounter{tocdepth}{5}
```

Alternativamente, use el comando `\addtocounter` para subir o bajar el nivel sin necesidad de conocer el valor actual.

A diferencia de los comandos, los nombres de los contadores no comienzan con una barra invertida.

#### Abreviación de entradas de la tabla de contenidos

Como ya aprendió en el [Capítulo 3](https://subscription.packtpub.com/book/business-and-other/9781805804574/3), *Diseño de páginas*, puede elegir un texto para la tabla de contenidos diferente del encabezado en el texto del cuerpo. Cada comando de sección entiende un argumento opcional para la entrada de la tabla de contenidos, lo cual es especialmente útil si desea utilizar un encabezado muy largo pero desea una entrada de tabla de contenidos más corta. En nuestro ejemplo, hicimos esto mediante el siguiente comando:

```latex
\subsubsection[Deeper level]{This section has an even deeper level}
```

El texto del cuerpo muestra el encabezado largo, mientras que la tabla de contenidos muestra el corto. Los títulos impresos en la parte superior de las páginas, llamados encabezados vivos o corrientes (*running headers*), también utilizarían la entrada corta. De esta manera, puede evitar una tabla de contenidos desordenada o encabezados de página desbordados.

#### Adición manual de entradas a la tabla de contenidos

Los comandos de sección con asterisco, como `\chapter*` y `\section*`, se utilizan para imprimir un encabezado sin generar una entrada en la tabla de contenidos. En nuestro ejemplo, agregamos una manualmente usando este comando:

```latex
\addcontentsline{file extension}{sectional unit}{text}
```

Puede utilizar este comando en diferentes situaciones. La extensión del archivo especifica qué lista actualizar, por ejemplo:

- `toc` para la tabla de contenidos
- `lof` para la lista de figuras
- `lot` para la lista de tablas

La unidad seccional determina el formato de la entrada. Por ejemplo, si lo establece en `chapter`, LaTeX formateará la entrada como una entrada de capítulo normal. Lo mismo se aplica a otras unidades seccionales, como `part`, `section` y `subsection`. El tercer argumento contiene el texto de la entrada.

También puede insertar texto o comandos más directamente mediante el siguiente comando:

```latex
\addtocontents{file extension}{entry}
```

A diferencia de `\addcontentsline`, este comando escribe la entrada del argumento directamente en el archivo tal como está, sin aplicar ningún formato adicional. Puede definir libremente cualquier formato que desee.

También puede utilizar el comando `\addtocontents` para diversas personalizaciones. A continuación se muestran algunos ejemplos:

- `\addtocontents{toc}{\protect\enlargethispage{\baselineskip}}` aumenta la altura del texto para que quepa una línea más en la página de contenidos.
- `\addtocontents{toc}{\protect\newpage}` fuerza un salto de página en la tabla de contenidos. Esto puede ser útil si LaTeX divide automáticamente la página en un lugar incómodo, por ejemplo, justo después de una entrada de capítulo, pero antes de las siguientes entradas de sección.
- `\addtocontents{toc}{\protect\thispagestyle{fancy}}` cambia el estilo de página de la página actual de la tabla de contenidos a `fancy`. Dado que la primera página de un capítulo es de estilo `plain` por defecto, la primera página de la tabla de contenidos también sería `plain`, incluso si especificó `\pagestyle{fancy}` anteriormente. Ese comando lo anula.

Coloque dichos comandos donde desee que surtan efecto. Por ejemplo, para afectar la primera página de la tabla de contenidos, colóquelo al principio de su documento. Para insertar un salto de página antes de un capítulo específico, colóquelo justo antes del comando `\chapter` correspondiente.

#### Creación y personalización de listas de figuras

Hay dos comandos para crear listas de figuras y tablas: `\listoffigures` y `\listoftables`. Dependiendo de la clase, producen una lista bien formateada de todas las leyendas, junto con el número de figura o tabla y los números de página correspondientes. Al igual que con la tabla de contenidos, LaTeX maneja esto automáticamente. Aún así, podemos usar las mismas técnicas que con la tabla de contenidos para personalizar las otras listas. Probemos eso.

Supongamos que todas nuestras figuras son diagramas. Reemplazaremos el término *figure* por *diagram*, y agregaremos una lista de diagramas:

1. Abra nuestro ejemplo actual. Agregue estas líneas a su preámbulo:

```latex
\renewcommand{\figurename}{Diagram}
\renewcommand{\listfigurename}{List of Diagrams}
```

2. Justo después de `\tableofcontents`, agregue lo siguiente:

```latex
\listoffigures
```

3. Agregue un diagrama en algún lugar del primer capítulo:

```latex
\begin{figure}
\centering
\fbox{Diagram placeholder}
\caption{Enterprize Organizational Chart}
\end{figure}
```

4. En la segunda parte del tercer capítulo, nos gustaría agregar diagramas de diseño de red. Marquemos eso en la lista de figuras (LOF) y luego incluyamos los diagramas:

```latex
\addtocontents{lof}{Network Diagrams:}
\begin{figure}
\centering
\fbox{Diagram placeholder}
\caption{Network overview}
\end{figure}
\begin{figure}
\centering
\fbox{Diagram placeholder}
\caption{WLAN Design}
\end{figure}
```

5. Haga clic en **Typeset** dos veces para obtener el documento y la lista:

> **Figura 8.2** – Una lista de diagramas

Cambiamos el nombre de las figuras y del encabezado de la lista redefiniendo las macros de LaTeX. Al final de este capítulo, obtendrá una lista de nombres utilizados por las clases de LaTeX que puede redefinir.

Al igual que con la tabla de contenidos, utilizamos el comando `\addtocontents` para insertar un encabezado en negrita en el archivo `.lof`, donde LaTeX almacena las leyendas de las figuras. Funciona de la misma manera que para la tabla de contenidos.

#### Creación de una lista de tablas

Crear y personalizar una lista de tablas (LOT) funciona igual que con las figuras. El archivo donde LaTeX recopila las leyendas de las tablas tiene la extensión `.lot`. Para modificarlo, use `lot` como primer argumento para el comando `\addtocontents`. Todo sigue la misma lógica que antes, al igual que con `\listoftables`, `\tablename` y `\listtablename`.

#### Uso de paquetes para la personalización

Además de los métodos básicos que hemos visto, varios paquetes proporcionan funciones sofisticadas para personalizar la tabla de contenidos y las listas de figuras y tablas:

- `tocloft` brinda un amplio control sobre la tipografía de TOC, LOF y LOT. Incluso puede definir nuevos tipos de listas de este tipo.
- `titletoc` proporciona una gestión conveniente de entradas y es el complemento de `titlesec`, un excelente paquete para personalizar encabezados de sección.
- `multitoc` ofrece un diseño en dos o más columnas utilizando el paquete `multicol`.
- `minitoc` crea pequeñas tablas de contenidos para cada parte, capítulo o sección.
- `tocbibind` puede agregar automáticamente una bibliografía, índice, TOC, LOF y LOT a la tabla de contenidos. Incluso puede numerar estos encabezados y entradas si lo prefiere.

Para obtener más información, utilice la herramienta de línea de comandos `texdoc` o visite [https://texdoc.org](https://texdoc.org/) para leer la documentación del paquete.

Ahora sabe cómo crear listas de contenidos, tablas y figuras que solemos colocar al principio de un documento. Continuemos con las listas que aparecen al final de un documento: un índice de palabras clave y una bibliografía.

---

### Generación de un índice

Los documentos más largos a menudo incluyen un índice alfabético o temático. Es una lista de palabras o frases junto con los números de página que muestran dónde aparecen los temas relacionados en el documento. A diferencia de una función de búsqueda de texto completo, un índice proporciona punteros cuidadosamente seleccionados a la información más relevante.

Una vez que identificamos y marcamos las palabras que queremos incluir en el índice, LaTeX se encarga de recopilarlas y componer tipográficamente el índice.

Digamos que nuestro documento de ejemplo contiene información sobre una empresa, su estructura y el diseño de su red. Marcaremos lugares en el texto donde ocurren estos conceptos. Finalmente, le diremos a LaTeX que genere el índice. Siga estos pasos:

1. Vuelva a nuestro ejemplo. En el preámbulo, cargue el paquete `index` y agregue el comando para crear el índice:

```latex
\usepackage{index}
\makeindex
```

2. En la leyenda de nuestro diagrama de empresa, indexe este punto con la palabra clave `enterprise`:

```latex
\caption{\index{enterprise}Enterprise Organizational Chart}
```

3. En el tercer capítulo, que contiene nuestros diagramas, indexe mediante la palabra clave `network`:

```latex
\index{network}
```

4. Directamente antes de `\end{document}`, cree una entrada para que el índice aparezca en la tabla de contenidos. Para asegurarse de que muestre el número de página correcto, finalice la página justo antes de ella:

```latex
\clearpage
\addcontentsline{toc}{chapter}{Index}
```

5. En la línea siguiente, dígale a LaTeX que componga el índice:

```latex
\printindex
```

6. Si está utilizando TeXworks, elija **MakeIndex** en lugar de **pdfLaTeX** en el cuadro desplegable junto al botón **Typeset**. Luego, haga clic en el botón **Typeset**. Si utiliza otro editor, use su función MakeIndex o escriba lo siguiente en el símbolo del sistema en el directorio del documento, sin una extensión de nombre de archivo:

```bash
makeindex documentname
```

7. Vuelva a cambiar a **pdfLaTeX**. Haga clic en **Typeset** y mire la última página:

> **Figura 8.3** – Un índice

Cargamos el paquete `index`, que mejora las funciones de indexación integradas de LaTeX.

Alternativamente, puede usar el paquete `makeidx`, que es parte del LaTeX estándar. El comando `\makeindex` prepara el índice. Ambos comandos pertenecen al preámbulo, por lo que deben colocarse antes de `\begin{document}`.

El comando `\index` toma solo un argumento, a saber, la palabra o frase que se va a indexar. Escribe esta frase en un archivo con la extensión `.idx`. Si mira dentro de este archivo, encontrará líneas como las siguientes:

```latex
\indexentry {enterprise}{9}
\indexentry {network}{15}
```

Estas representan las entradas del índice y sus correspondientes números de página.

El programa externo `makeindex` procesa ese archivo `.idx` y genera un archivo `.ind`. Este último consta de código LaTeX para crear el índice. Específicamente, contiene el entorno de lista de índice junto con los elementos y aparece de la siguiente manera:

```latex
\begin{theindex}
  \item enterprise, 9

  \indexspace

  \item network, 15

\end{theindex}
```

Los índices más complejos pueden contener subelementos, rangos de páginas y referencias a otros elementos. Veamos cómo producir un índice de este tipo. En el sitio web del libro, [https://latexguide.org/chapter-08](https://latexguide.org/chapter-08), puede encontrar código totalmente compilable que contiene comandos de ejemplo sobre los que aprenderemos en las siguientes secciones. Puede probarlos directamente en la página web.

#### Definición de entradas y subentradas de índice

Hasta ahora, ya hemos creado entradas de índice simples mediante el siguiente comando:

```latex
\index{phrase}
```

Para producir subentradas, especifique el término principal seguido de un signo de exclamación y luego la subentrada. He aquí un ejemplo:

```latex
\index{network!overview}
```

Además, las subentradas pueden tener subentradas; use otro signo de exclamación, por ejemplo:

```latex
\index{enterprise!organization}
\index{enterprise!organization!sales}
\index{enterprise!organization!controlling}
\index{enterprise!organization!operation}
```

LaTeX admite hasta tres niveles de subentradas.

#### Especificación de rangos de páginas

Si varias páginas tratan sobre el mismo tema, puede especificar un rango de páginas para la entrada del índice. Use `|(` donde comienza el rango y agregue `|)` donde termina. Por lo tanto, al comienzo del capítulo de red, agregue `|(` de la siguiente manera:

```latex
\index{network|(}
```

Mientras que, al final de este capítulo, agregue `|)` de esta manera:

```latex
\index{network|)}
```

Esto producirá una entrada de índice como *Network, 15-17*.

#### Uso de símbolos y macros en el índice

De forma predeterminada, `makeindex` ordena todas las entradas alfabéticamente. Si desea incluir símbolos en el índice (por ejemplo, letras griegas, fórmulas químicas o símbolos matemáticos), puede encontrarse con problemas de ordenación. Para solucionar esto, el comando `\index` admite una clave de ordenación (*sort key*). Utilice esta clave como prefijo para la entrada, separada por el símbolo `@`, por ejemplo:

```latex
\index{Gamma@$\Gamma$}
```

Generalmente no se recomienda el uso de macros para entradas de índice. El nombre de la macro, incluida la barra invertida, determinaría la ordenación, aunque la macro se expandiría en el índice. Imagine que tiene una macro `\group` que representa *TeX Users Group*, definida de esta manera:

```latex
\newcommand{\group}{\TeX\ Users Group}
```

Si escribe lo siguiente, la entrada *TeX Users Group* se tratará como `\group` en la ordenación y no aparecerá entre las entradas que comienzan con T:

```latex
\index{\group}
```

Sin embargo, podría solucionar estos problemas agregando una clave de ordenación como prefijo, como aquí:

```latex
\index{TeX@\group}
```

También puede indicar cómo se ordenarán las palabras con caracteres especiales. Aquí, la palabra alemana *schön*, que contiene una diéresis (*umlaut*), se ordenará como la palabra *schon*:

```latex
\index{schon@sch\"{o}n}
```

Dado que los símbolos `|`, `@` y `!` tienen significados especiales dentro de las entradas de índice, necesitamos entrecomillarlos para imprimirlos con sus significados originales. Este es un ejemplo de cómo podemos imprimirlos:

```latex
\index{exclamation ("!)!loud}
```

Podemos imprimir los símbolos `|`, `@` y `!` en el índice entrecomillándolos, utilizando unas comillas dobles `"` precedentes.

#### Hacer referencia a otras entradas del índice

Diferentes palabras pueden representar el mismo concepto. En tales casos, es posible agregar una referencia cruzada a la frase principal sin un número de página. Agregar el código `|see{entry list}` logra eso, por ejemplo:

```latex
\index{wireless|see{WLAN}}
\index{WLAN}
```

Como tales referencias no imprimen un número de página, su posición en el texto no importa. Podría recopilarlas en cualquier lugar de su documento.

#### Ajuste fino de los números de página

Si una entrada de índice hace referencia a varias páginas, debe enfatizar un número de página específico para indicarlo como la referencia principal. Podría definir un comando para enfatizar de la siguiente manera:

```latex
\newcommand{\main}[1]{\emph{#1}}
```

Luego, para la entrada del índice, agregue un símbolo de barra vertical seguido del nombre del comando:

```latex
\index{WLAN|main}
```

Ahora, LaTeX enfatiza el número de página correspondiente. También es posible simplemente escribir `\index{WLAN|emph}` o `\index{WLAN|textbf}`. Sin embargo, definir su propia macro es más coherente: recuerde el concepto de separar forma y contenido.

#### Diseño del formato del índice

Si ampliamos nuestro documento de ejemplo con los comandos de ejemplo mencionados en las secciones anteriores, `\printindex` nos da este diseño, que contiene subentradas, rangos, referencias y entradas enfatizadas:

> **Figura 8.4** – Un índice más complejo

LaTeX viene con varios estilos de índice integrados, llamados `latex` (el predeterminado), `gind`, `din` e `iso`. Para usar otro estilo, especifíquelo usando la opción `-s` del programa `makeindex`, por ejemplo:

```bash
makeindex -s iso documentname
```

Si compila después de esta llamada, el diseño del índice cambia a lo siguiente:

> **Figura 8.5** – Un índice con el estilo iso

Incluso podría definir sus propios estilos. Para obtener más información sobre indexación y `makeindex`, use `texdoc` en el símbolo del sistema:

```bash
texdoc index
```

Para obtener más información sobre la herramienta `makeindex`, use el siguiente comando:

```bash
texdoc makeindex
```

O visite la documentación en línea en [https://texdoc.org/pkg/index](https://texdoc.org/pkg/index) y [https://texdoc.org/pkg/makeindex](https://texdoc.org/pkg/makeindex).

Aunque pueda parecer natural generar el índice mientras se escribe el documento, se recomienda esperar hasta que se termine de escribir y luego decidir qué debe aparecer en el índice.

A continuación, pasaremos a otro tipo de lista: la lista de referencias, es decir, la bibliografía.

---

### Creación de una bibliografía

Los documentos científicos y académicos suelen incluir una lista de referencias o una bibliografía. Veremos cómo componer una bibliografía y citar sus entradas en el texto.

Utilizando las funciones integradas de LaTeX, crearemos una breve lista de referencias que contiene un libro y un artículo de Donald E. Knuth, el creador de TeX. En nuestro texto principal, citaremos ambos:

1. Cree un nuevo documento de la siguiente manera:

```latex
\documentclass{article}
\begin{document}
\section*{Recommended texts}
To study \TeX\ in depth, see \cite{DK86}.
For writing math texts, see \cite{DK89}.
\begin{thebibliography}{8}
  \bibitem{DK86} D.E. Knuth, \emph{The {\TeX}book}, 1986
  \bibitem{DK89} D.E. Knuth, \emph{Typesetting Concrete Mathematics}, 1989
\end{thebibliography}
\end{document}
```

2. Haga clic en **Typeset** y examine el resultado:

> **Figura 8.6** – Una lista de referencias

Aquí, usamos un entorno llamado `thebibliography` para componer la lista de referencias, que es similar a una lista de descripciones, como vio en el [Capítulo 4](https://subscription.packtpub.com/book/business-and-other/9781805804574/4), *Creación de listas*. Cada elemento de esta lista tiene una clave que lo identifica. Para citar en el texto del cuerpo, usamos el comando `\cite` para hacer referencia a esa clave. Veamos más de cerca cómo funcionan estos comandos.

#### Uso del entorno de bibliografía integrado

El entorno predeterminado de LaTeX para bibliografías tiene la siguiente estructura:

```latex
\begin{thebibliography}{widest label}
  \bibitem[label]{key} author, title, year etc.
  \bibitem…
  …
\end{thebibliography}
```

Cada elemento se especifica mediante el comando `\bibitem`. Este comando requiere un argumento obligatorio que determina la clave. Podemos hacer referencia a esta clave con `\cite{key}` o `\cite{key1,key2}`. `\cite` también acepta un argumento opcional que indica un rango de páginas, por ejemplo, `\cite[p.\,18--20]{key}`. Puede elegir una etiqueta mediante el argumento opcional de `\bibitem`. Si no indicamos una etiqueta, LaTeX numerará los elementos consecutivamente entre corchetes, como vimos en la Figura 8.6.

Utilizando etiquetas, el entorno podría verse de la siguiente manera:

```latex
\begin{thebibliography}{Knuth89}
  \bibitem[Knuth86]{DK86} D.E. Knuth, \emph{The {\TeX}book}, 1986
  \bibitem[Knuth89]{DK89} D.E. Knuth, \emph{Typesetting Concrete Mathematics}, 1989
\end{thebibliography}
```

La salida correspondiente es esta:

> **Figura 8.7** – Una lista de referencias

Como puede ver, LaTeX ajustó automáticamente la salida de `\cite` a las nuevas etiquetas. Si desea más control sobre el formato de citas, el paquete `cite` ofrece listas comprimidas y ordenadas de citas numéricas, como `[2,4-6]`, y más opciones de formato para citas dentro del texto.

El argumento obligatorio del entorno debe incluir la etiqueta más ancha para la alineación. Por lo tanto, por ejemplo, si tiene más de 9 pero menos de 100 elementos, puede escribir dos dígitos en el argumento.

#### Uso de bases de datos de bibliografía con BibTeX

Crear manualmente la bibliografía puede resultar tedioso. Especialmente si utiliza referencias en varios documentos, sería mejor utilizar una base de datos y dejar que un programa genere la bibliografía por usted. Esto suena más complicado de lo que realmente es. Probémoslo.

Crearemos un archivo de base de datos separado que contenga las referencias de nuestro ejemplo anterior. Modificaremos nuestro ejemplo para utilizar esa base de datos. Para que esto funcione, tenemos que llamar al programa externo BibTeX:

1. Cree un nuevo documento. Comience escribiendo la entrada para TeXbook:

```bibtex
@book{DK86,
  author    = "D.E. Knuth",
  title     = "The {\TeX}book",
  publisher = "Addison Wesley",
  year      = 1986
}
```

2. A continuación, agregue el artículo, donde especificaremos aún más campos:

```bibtex
@article{DK89,
  author  = "D.E. Knuth",
  title   = "Typesetting Concrete Mathematics",
  journal = "TUGboat",
  volume  = 10,
  number  = 1,
  pages   = "31--36",
  month   = apr,
  year    = 1989
}
```

3. Guarde el archivo y nómbrelo `example.bib`. Abra nuestro documento de ejemplo y modifíquelo de la siguiente manera:

```latex
\documentclass{article}
\begin{document}
\section*{Recommended texts}
To study \TeX\ in depth, see \cite{DK86}.
For writing math texts, see \cite{DK89}.
\bibliographystyle{alpha}
\bibliography{example}
\end{document}
```

4. Haga clic en **Typeset** una vez con pdfLaTeX. Si está utilizando TeXworks, elija **BibTeX** en lugar de **pdfLaTeX**, presente en el cuadro desplegable junto al botón **Typeset**, y luego haga clic en **Typeset**. Si está escribiendo con otro editor, use su opción BibTeX o escriba en el símbolo del sistema en el directorio del documento lo siguiente, sin una extensión de nombre de archivo:

```bash
bibtex documentname
```

5. Haga clic en **Typeset** dos veces con pdfLaTeX. Aquí está el resultado:

> **Figura 8.8** – Una bibliografía basada en un archivo de base de datos

En esta configuración, creamos un archivo de texto que contiene todas las entradas de la bibliografía. Nuestro documento utiliza el estilo `alpha`, que ordena las entradas por los nombres de los autores y utiliza un atajo que consta de las claves de autor y año como etiqueta. Le dijimos a LaTeX que cargue el archivo de bibliografía llamado `example`. La extensión `.bib` se asume automáticamente.

Luego, llamamos al programa externo BibTeX. Este programa sabe por el archivo de ejemplo `.tex` que `example.bib` necesita ser traducido. Por lo tanto, a partir de este archivo `.bib`, crea un archivo `.bbl` que contiene un entorno `thebibliography` de LaTeX y las entradas finales.

Finalmente, tuvimos que compilar dos veces para asegurarnos de que todas las referencias cruzadas fueran correctas.

Aunque este proceso implica algunos pasos adicionales para generar la bibliografía, también hay ventajas: no necesitamos afinar cada entrada, podemos cambiar fácilmente entre estilos y luego podemos reutilizar el archivo `.bib`.

Ahora, miremos el formato del archivo `.bib` más de cerca.

#### Examen de los campos de entrada de BibTeX

BibTeX admite varios tipos de entrada, como vimos con las entradas `book` y `article`. Además, estas entradas contienen campos como autor, título y año. Primero veamos los campos admitidos y, después, discutiremos los diferentes tipos de entradas.

Aquí hay una lista de los campos estándar. Algunos campos son comunes, otros rara vez se usan; los enumeraremos en orden alfabético para mayor exhaustividad:

- `address`: La dirección de la editorial
- `annote`: Una anotación no utilizada por los estilos de bibliografía estándar
- `author`: El nombre(s) del autor(es)
- `booktitle`: El título de un libro si cita una parte de él; también puede usar el campo `title` en su lugar
- `chapter`: Un número de capítulo
- `crossref`: La clave de la entrada de la base de datos a la que se hace referencia cruzada
- `edition`: La edición (primera, segunda, etc.) de un libro; comúnmente está en mayúsculas
- `editor`: El nombre(s) del editor(es)
- `howpublished`: La forma de publicación; la primera palabra debe estar en mayúscula
- `institution`: Podría ser una institución patrocinadora
- `journal`: El nombre de una revista; puede utilizar abreviaturas estándar
- `key`: Se utiliza para alfabetizar, hacer referencias cruzadas y etiquetar si falta la información del autor; no lo confunda con la clave utilizada en el comando `\cite`
- `month`: El mes en que se publicó la obra; a menudo se utiliza una abreviatura de tres letras
- `note`: Cualquier información adicional útil; nuevamente, la primera palabra debe estar en mayúscula
- `number`: El número de una revista u otro tipo de obra en una serie
- `organization`: Puede ser una organización patrocinadora
- `pages`: Un número de página o rango de números de página, como 12-18 o 22+
- `publisher`: El nombre de la editorial
- `school`: Podría ser el nombre de la escuela/universidad donde se escribió el documento
- `series`: El nombre de una serie de libros o su número en un conjunto de varios volúmenes
- `title`: El título de la obra
- `type`: El tipo de publicación
- `volume`: El volumen de una revista o libro de varios volúmenes
- `year`: El año de la publicación

Puede leer la documentación de BibTeX escribiendo `texdoc bibtex` en la línea de comandos o visitando [https://texdoc.org/pkg/bibtex](https://texdoc.org/pkg/bibtex).

#### Citas de recursos de Internet

Hoy en día, es común citar páginas web y otras fuentes de Internet. Para colocar direcciones de Internet en campos de BibTeX, use el comando `\url` del paquete `url` o `hyperref`, por ejemplo:

```bibtex
howpublished = {\url{https://latex.org}}
```

Las bibliografías de algunos estilos incluyen un campo `url` que se puede utilizar para hacer referencia a direcciones de Internet.

#### Comprensión de los tipos de entrada de BibTeX

Por lo general, comienza eligiendo el tipo de entrada adecuado que desea agregar y luego completa los campos. Los diferentes tipos pueden admitir varios campos. Algunos campos son obligatorios, algunos son opcionales y pueden omitirse, y algunos se ignoran cuando el estilo no los admite.

Por lo general, el nombre de la entrada le indica su significado. Estos son los tipos de entrada estándar de BibTeX y sus campos obligatorios y opcionales:

> **Figura 8.9** – Tipos de entrada y campos de BibTeX

Consulte la referencia de BibTeX para obtener más detalles escribiendo lo siguiente en el símbolo del sistema:

```bash
texdoc bibtex
```

Alternativamente, puede visitar [https://texdoc.org/pkg/bibtex](https://texdoc.org/pkg/bibtex).

Si ninguna otra entrada encaja, elija el tipo `misc`. No importa si usa mayúsculas o minúsculas en un tipo; `@ARTICLE` se entiende igual que `@article`. Como muestra el ejemplo, las entradas tienen la siguiente forma:

```bibtex
@entrytype{keyword,
  fieldname      = {field text},
  otherfieldname = {other field text},
  …
}
```

Encierre el texto del campo entre llaves. También puede utilizar comillas rectas en su lugar, como en `"field text"`. Para números, incluso puede omitir las llaves. Si bien las entradas se separan con una coma, nunca ponga una coma después del último campo. De lo contrario, BibTeX asumirá que debe seguir otro campo y puede informar un error.

Algunos estilos cambian las mayúsculas y minúsculas, lo que puede resultar en letras minúsculas no deseadas. Para proteger letras o palabras de convertirse en minúsculas, coloque llaves adicionales a su alrededor. Preferiblemente, hágalo alrededor de una palabra en lugar de solo la letra para mantener las ligaduras y mejorar el espaciado. Por ejemplo, `{WAL}` se ve mejor que `{W}AL`, porque en un flujo de texto estándar, LaTeX acerca una A a una W precedente. Separar con llaves interfiere con las mejoras microtipográficas de LaTeX.

#### Elección del estilo de bibliografía

BibTeX ofrece varios estilos estándar:

- `plain`: Utiliza números arábigos para las etiquetas, ordenados alfabéticamente por los nombres de los autores. El número se escribe entre corchetes, que también aparecen con `\cite`.
- `unsrt`: No hay ordenación. Todas las entradas aparecen en el orden en que fueron citadas en el texto. Aparte de esto, se parece al estilo `plain`.
- `alpha`: La ordenación se basa en los nombres de los autores; las etiquetas son atajos que consisten en el nombre del autor y el año de publicación. Aquí también se utilizan corchetes.
- `abbrv`: Funciona como `plain`, pero abrevia los nombres de pila y otras entradas de campos.

Elija el estilo después de `\begin{document}` pero antes de `\bibliography`. Puede escribir `\bibliographystyle` justo antes de `\bibliography` para mantenerlo junto.

Hay más estilos disponibles en las distribuciones de TeX y en Internet. Por ejemplo, el paquete `natbib` proporciona estilos y la capacidad de citar en un agradable esquema de autor-año. Este paquete además agrega algunos campos, como ISBN, ISSN y URL.

Podría probar el paquete `natbib` y utilizar sus estilos `plainnat`, `abbrvnat` y `unsrtnat`, por ejemplo:

```latex
\usepackage{natbib}
\bibliographystyle{plainnat}
```

El paquete `natbib` reimplementó el comando `\cite` y ofrece variaciones al mismo, con el propósito principal de admitir citas de autor-año. Funciona con la mayoría de los demás estilos disponibles. Introduce el comando de cita, `\citet`, para citas textuales, y el comando `\citep` para citas entre paréntesis. Hay variantes con asterisco que imprimen la lista completa de autores y argumentos opcionales que permiten agregar texto antes y después de la lista.

Consulte la documentación si desea aprovechar este excelente paquete. Como de costumbre, escriba `texdoc natbib` en la línea de comandos o visite [https://texdoc.org/pkg/natbib](https://texdoc.org/pkg/natbib).

El paquete `biblatex` es una reimplementación completa de la funcionalidad bibliográfica de BibTeX. Mientras que BibTeX se basa en un lenguaje de estilo separado basado en pila, `biblatex` es nativo de LaTeX, lo que hace que los estilos de bibliografía sean más fáciles de personalizar y ampliar. Puede encontrar la documentación en [https://texdoc.org/pkg/biblatex](https://texdoc.org/pkg/biblatex).

Funciona en estrecha colaboración con el moderno programa `biber`, que reemplaza al tradicional programa `BibTeX`; consulte [https://texdoc.org/pkg/biber](https://texdoc.org/pkg/biber) para obtener documentación. En *LaTeX Cookbook*, Capítulo 8, *Producción de contenidos, índices y bibliografías*, puede encontrar un ejemplo paso a paso bien explicado utilizando `biblatex` y `biber`.

#### Listar referencias sin citar

De forma predeterminada, BibTeX incluye solo las referencias de la base de datos que se citan en el texto y las imprime. Sin embargo, puede especificar claves para referencias que, no obstante, deberían aparecer. Simplemente escriba lo siguiente para una sola referencia:

```latex
\nocite{key}
```

O escriba lo siguiente para listar la base de datos completa:

```latex
\nocite{*}
```

Asegúrese de eliminar `\nocite{*}` en la versión final del documento si no desea tener referencias en la bibliografía que nunca citó en el documento.

Ahora que sabemos cómo crear tales tablas de contenidos, listas de objetos, índices y bibliografías, echemos un vistazo final a cómo personalizarlas.

---

### Cambio de los encabezados

Como se muestra en la Figura 8.2, puede cambiar fácilmente el encabezado *Contents* si no le gusta. LaTeX almacena el texto del encabezado en la macro de texto `\contentsname`. Por lo tanto, puede redefinirla de la siguiente manera:

```latex
\renewcommand{\contentsname}{Table of Contents}
```

Aquí hay una lista de tales macros y sus valores predeterminados:

- `\contentsname`: Contents
- `\listfigurename`: List of figures
- `\listtablename`: List of tables
- `\bibname`: Bibliography (en las clases `book` y `report`)
- `\refname`: References (en la clase `article`)
- `\indexname`: Index

Además, aquí hay una lista de otras macros para nombres utilizados por LaTeX, con sus valores predeterminados:

- `\figurename`: Figure
- `\tablename`: Table
- `\partname`: Part
- `\chaptername`: Chapter
- `\abstractname`: Abstract
- `\appendixname`: Appendix

¡Esto no es realmente sorprendente! El uso de macros de nombres es especialmente útil cuando escribe en otro idioma. Por ejemplo, el paquete `babel` toma una opción de idioma y redefine todas esas macros de nombres según el idioma elegido.

Sin embargo, también son útiles al elegir abreviaturas, como *Fig.*, o redacciones diferentes, como *Appendices* en lugar de *Appendix*.

---

### Adición de un glosario

Un glosario es una lista estructurada de términos con sus definiciones. Se utiliza habitualmente para explicar vocabulario técnico, abreviaturas y símbolos en tesis, artículos científicos, manuales técnicos y libros, especialmente cuando los términos se repiten a lo largo del texto. Estrechamente relacionadas están las listas de acrónimos y símbolos, que tienen el mismo propósito: ayudar a los lectores a encontrar explicaciones rápidamente sin interrumpir el flujo del documento.

En LaTeX, la solución moderna recomendada es el paquete `glossaries`. Es potente y flexible, y maneja desde una breve lista de abreviaturas hasta grandes glosarios generados automáticamente en documentos complejos. Algunos aspectos destacados de este paquete incluyen compatibilidad con glosarios, acrónimos y símbolos en un único marco; ordenación y formateo automáticos; control preciso sobre la visualización de entradas; integración con herramientas de indexación; y soporte para documentos multilingües.

El paquete está excepcionalmente bien documentado. Viene con una guía para principiantes, un manual de usuario detallado y preguntas frecuentes del autor, todo disponible en [https://ctan.org/pkg/glossaries](https://ctan.org/pkg/glossaries).

Debido a que las guías que lo acompañan son muy completas, no entraremos en detalles aquí. El punto es: si necesita un glosario o una lista de símbolos, este paquete es muy recomendable.

---

### Resumen

En este capítulo, cubrimos muchos tipos de listas. Específicamente, aprendimos a generar y personalizar la tabla de contenidos y las listas de figuras y tablas, producir un índice que señale información relevante para palabras clave y frases, y crear bibliografías, tanto manualmente como utilizando una base de datos de bibliografía.

Estas listas sirven como ayudas de navegación, guiando a los lectores hacia la información que buscan. No son meramente para listar y resumir. A veces, existe el extraño requisito de listar la tabla de contenidos dentro de sí misma. Si no está seguro de un diseño o requisito, eche un vistazo a un buen libro en su campo particular para ver cómo podrían verse las tablas de contenidos, listas e índices ejemplares.

Puede encontrar ejemplos relacionados en *LaTeX Cookbook*, Capítulo 8, *Producción de contenidos, índices y bibliografías*, con ejemplos de código disponibles en el sitio web del libro: [https://latex-cookbook.net/chapter-08](https://latex-cookbook.net/chapter-08).

En el próximo capítulo, analizaremos más de cerca la redacción científica.
