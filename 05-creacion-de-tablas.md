# LaTeX Beginner's Guide
## Capítulo 5: Creación de Tablas

Los documentos científicos y técnicos a menudo contienen más que texto plano; también incluyen datos estructurados. En el capítulo anterior, analizamos formas de organizar la información con diferentes tipos de listas y cómo personalizar su diseño. Ahora, nos dedicaremos a presentar datos en tablas.

Cubriremos los siguientes temas:

- Alineación de texto con tabulaciones
- Creación de tablas básicas
- Mejora de la apariencia de las tablas
- Adición de leyendas a las tablas
- Mejora de tablas con paquetes adicionales

Comenzaremos simplemente organizando el texto en columnas.

---

### Alineación de texto con tabulaciones

¿Recuerda haber usado tabulaciones en máquinas de escribir o en los primeros programas de procesamiento de texto para crear columnas de texto alineadas? LaTeX ofrece un mecanismo similar con el entorno `tabbing` para alinear texto prolijamente en columnas.

Creemos una descripción general compacta de LaTeX. Mostraremos un elemento por línea, alineando partes clave del texto, siguiendo estos pasos:

1. Comience un nuevo documento y abra un entorno `tabbing`:

```latex
\documentclass{article}
\begin{document}
\begin{tabbing}
```

2. Escriba la primera línea de texto. Use `\=` para establecer tabulaciones y `\\` para terminar la línea:

```latex
\emph{Info:} \= Software \= : \= \LaTeX \\
```

3. Añada más líneas; use `\>` para saltar a la siguiente tabulación y nuevamente termine la línea con `\\`:

```latex
\> Author \> : \> Leslie Lamport \\
\> Website \> : \> www.latex-project.org
```

4. Cierre el entorno `tabbing` y finalice el documento:

```latex
\end{tabbing}
\end{document}
```

5. Haga clic en el botón **Typeset** para compilar el documento y observe el resultado:

> **Figura 5.1** – Texto alineado de forma simple

El entorno `tabbing` comienza automáticamente una nueva línea. Usamos tres comandos básicos para controlar la alineación:

- `\=` establece una posición de tabulación. Puede colocar varias tabulaciones en una sola línea. Por lo general, hacemos eso en la primera fila.
- `\\` finaliza una fila.
- `\>` salta a la siguiente tabulación definida.

Si bien las tabulaciones generalmente se establecen en la primera fila, también puede redefinirlas en líneas posteriores usando `\=`. Por ejemplo, si ya usamos dos comandos `\>` en una línea de texto para navegar a través de dos tabulaciones, insertar otro comando `\=` establece o ajusta una tercera tabulación en esa línea.

En [https://latexguide.org/tabbing](https://latexguide.org/tabbing), puede ver varios ejemplos usando estas etiquetas.

El entorno `tabbing` proporciona una forma rápida de crear columnas alineadas a la izquierda. Si las filas del entorno `tabbing` alcanzan el final de una página, continuará automáticamente en la página siguiente. Eso lo convierte en una forma básica pero eficiente de crear tablas que cruzan saltos de página o incluso abarcan varias páginas.

¿Pero qué sucede si el texto excede el ancho y sobrepasa la tabulación? Veamos cómo manejar eso a continuación.

En el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*, exploramos varios comandos y declaraciones de fuentes. Es posible que recuerde una tabla que enumeraba estos comandos junto con su salida. Creemos ahora nosotros mismos una tabla de este tipo, de la siguiente manera:

1. Comience un nuevo documento, similar al paso 1 de nuestro ejemplo anterior, pero esta vez defina un comando para poner el texto del encabezado en negrita:

```latex
\documentclass{article}
\newcommand{\head}[1]{\textbf{#1}}
\begin{document}
\begin{tabbing}
```

2. Defina tabulaciones en la primera fila usando `\=` y use `\>` para saltar a las tabulaciones. Use el comando `\verb|…|` que aprendió en el capítulo anterior para mostrar código LaTeX literalmente:

```latex
\= \head{Command} \= \head{Declaration} \= \head{Example}\\
\> \verb|\textrm{...}| \> \verb|\rmfamily| \> \rmfamily text\\
\> \verb|\textsf{...}| \> \verb|\sffamily| \> \sffamily text\\
\> \verb|\texttt{...}| \> \verb|\ttfamily| \> \ttfamily text
```

3. Finalice el entorno `tabbing` y el documento:

```latex
\end{tabbing}
\end{document}
```

4. Compile el documento y examine el resultado:

> **Figura 5.2** – Texto alineado superpuesto

Como podemos ver, las tabulaciones son demasiado estrechas en este punto, lo que hace que las columnas se superpongan. Lo corregiremos. Cree una nueva fila de encabezado que contenga las tabulaciones, pero esta vez terminaremos la línea con `\kill` para ocultar esa línea. Utilice texto de relleno para especificar el ancho entre las tabulaciones, como el texto más largo de la columna. Complételo con más comandos de fuentes. El código de `tabbing` ahora se ve así:

```latex
\begin{tabbing}
\= \verb|\textrm{...}| \= \head{Declaration} \= \head{Example}\kill
\> \head{Command}      \> \head{Declaration} \> \head{Example}\\
\> \verb|\textrm{...}| \> \verb|\rmfamily|   \> \rmfamily text\\
\> \verb|\textsf{...}| \> \verb|\sffamily|   \> \sffamily text\\
\> \verb|\texttt{...}| \> \verb|\ttfamily|   \> \ttfamily text
\end{tabbing}
```

5. Compile de nuevo para obtener el resultado final:

> **Figura 5.3** – Texto alineado corregido

Después de darnos cuenta de que nuestras tabulaciones eran demasiado estrechas, agregamos una nueva primera fila que contenía las tabulaciones. Consiste en palabras que representan las entradas más anchas de cada columna. Para evitar que esta fila adicional aparezca en la salida, usamos el comando `\kill` justo al final de la línea; `\kill` al final de una línea omite la impresión de la línea pero aún así registra las tabulaciones.

Hay otros comandos útiles que resultan prácticos si trabaja frecuentemente con textos tabulados:

- `\+` al final de una línea (antes de `\\`) mueve el margen izquierdo de las líneas subsiguientes una tabulación hacia la derecha. Úselo dos veces, `\+\+`, para moverlo dos tabulaciones hacia la derecha, y así sucesivamente.
- `\-` al final de una línea mueve el margen izquierdo de las líneas subsiguientes una tabulación hacia la izquierda. También aquí, `\-\-` movería dos tabulaciones hacia la izquierda. `\-` sirve básicamente para cancelar el efecto de una sangría previa realizada por un comando `\+` anterior.
- `\<` cancela el efecto de un comando `\+` precedente solo para esa línea. Mueve el margen izquierdo una tabulación hacia la izquierda. Solo debemos usarlo al principio de una línea. Repítalo para mover dos tabulaciones a la izquierda.

Estos comandos le brindan un control sólido sobre el entorno `tabbing`. Para obtener una lista completa de funciones, consulte el manual de referencia: [https://latex2e.org/tabbing](https://latex2e.org/tabbing).

Dentro de un entorno `tabbing`, las declaraciones son locales al elemento actual. Un comando `\=`, `\>`, `\\` o `\kill` subsiguiente detendría el efecto.

Además, los entornos `tabbing` no se pueden anidar.

Eso concluye cómo alinear texto en columnas de forma rápida. A continuación, veamos cómo construir tablas con líneas de alineación y separación.

---

### Creación de tablas básicas

A veces necesitamos estructuras y formatos más complejos, como centrado dentro de columnas, inserción de líneas divisorias horizontales o incluso creación de estructuras anidadas. LaTeX proporciona el entorno `tabular` para construir tablas tanto simples como complejas.

Recreemos la tabla de comandos de familias de fuentes de nuestro ejemplo anterior, esta vez con columnas centradas. También agregaremos algunas líneas horizontales para visualizar el borde de la tabla y el encabezado. Siga estos pasos:

1. Cree un nuevo documento. Defina un comando para establecer la fuente para la fila del encabezado:

```latex
\documentclass{article}
\newcommand{\head}[1]{\textnormal{\textbf{#1}}}
\begin{document}
```

2. Comience un entorno `tabular`. Como argumento obligatorio, proporcione `ccc`, que representa tres columnas centradas:

```latex
\begin{tabular}{ccc}
```

3. Escriba la fila de encabezado de la tabla, use el carácter `&` para separar las entradas de las columnas y termine con `\\` para finalizar las filas. Use `\hline` para insertar líneas horizontales:

```latex
\hline
\head{Command} & \head{Declaration} & \head{Output}\\
\hline
```

4. Continúe con el cuerpo de la tabla y finalice el entorno y el documento. Para componer los comandos de LaTeX literalmente, escriba `\verb|\command|`:

```latex
\verb|\textrm| & \verb|\rmfamily| & \rmfamily Example text\\
\verb|\textsf| & \verb|\sffamily| & \sffamily Example text\\
\verb|\texttt| & \verb|\ttfamily| & \ttfamily Example text\\
\hline
\end{tabular}
\end{document}
```

5. Compile el documento para ver la tabla:

> **Figura 5.4** – Una tabla simple

En el paso 2, especificamos una lista de caracteres en el argumento obligatorio. Cada carácter define cómo se formateará una columna. Como usamos tres caracteres, obtuvimos tres columnas. La letra `c` representa una alineación centrada, por lo que las entradas de todas las columnas se han centrado.

En los pasos 3 y 4, las entradas de las columnas se separan mediante un carácter ampersand (`&`), mientras que `\\` termina una fila. Para mejorar la legibilidad, es una buena idea alinear los ampersands, `&`, en el código fuente.

Dentro de las entradas de las columnas, puede usar tanto texto plano como comandos de LaTeX. Al igual que en el entorno `tabbing`, las declaraciones son locales a la celda actual.

Además, el entorno `tabular` tiene un argumento de posicionamiento opcional al igual que el entorno `minipage`. La definición completa se ve así:

```latex
\begin{tabular}[position]{column specifiers}
row 1 col 1 entry & row 1 col 2 entry ... & row 1 col n entry\\
...
\end{tabular}
```

El argumento opcional `[position]` establece la alineación vertical de toda la tabla:

- `t` se alinea en la fila superior de la tabla
- `b` se alinea en la fila inferior
- `c` centra la tabla verticalmente, que es el valor predeterminado

Este argumento opcional puede resultar útil si desea colocar dos tablas una al lado de la otra o junto a una imagen u otro texto.

En las siguientes secciones, analizaremos formas de personalizar tablas, como dibujar líneas; alinear a la izquierda, a la derecha o al centro; y combinar celdas a través de múltiples columnas o filas.

#### Dibujo de líneas en tablas

Dentro de un entorno `tabular`, podemos usar tres tipos de líneas:

- `\hline` dibuja una línea horizontal que abarca todo el ancho de la tabla.
- `\cline{m-n}` dibuja una línea horizontal que comienza en la columna `m` y termina en la columna `n`. Ambos números son obligatorios: incluso si esta línea debe cubrir solo una columna en particular, por ejemplo, solo la columna 3, debemos escribirla como `\cline{3-3}`.
- `\vline` dibuja una línea vertical a lo largo de toda la altura de la fila actual.

Haremos uso del comando `\hline` en las próximas secciones.

#### Comprensión de los argumentos de formato

Hay muchas más opciones de formato. Eche un vistazo a esta tabla de ejemplo, donde agregamos `l`, `c`, `r` y `p` como especificadores de columna, para demostrar cada tipo de alineación:

```latex
\begin{tabular}{|l|c|r|p{1.7cm}|}
\hline
left & centered & right & a fully justified paragraph cell\\
\hline
l & c & r & p\\
\hline
\end{tabular}
```

Este código genera la siguiente tabla:

> **Figura 5.5** – Una tabla con diferentes alineaciones

Las opciones entendidas por el entorno `tabular` son las siguientes:

- `l` alinea el contenido a la izquierda.
- `c` centra el contenido.
- `r` alinea el contenido a la derecha.
- `p{width}` es para una celda de "párrafo" de ancho fijo. Si coloca varias columnas `p` una al lado de la otra, sus celdas se alinearán en su línea superior. Se comporta como usar `\parbox[t]{width}` dentro de una celda.
- `@{code}` inserta código en lugar de espacio vacío antes o después de una columna. El código también puede ser algún texto, o se puede dejar vacío para suprimir este espacio por completo, como `@{}`. Haremos un uso frecuente de esto más adelante en esta sección.
- `*{n}{options}` repite las opciones especificadas `n` veces. `n` es un entero positivo y las opciones pueden consistir en uno o más especificadores de columna, incluido `*` también.
- `|` dibuja una línea vertical a lo largo de la columna.

Es mejor evitar el uso de líneas verticales en las tablas. Las líneas deben proporcionar una guía visual sutil sin interferir con la legibilidad. Leer filas de izquierda a derecha es más fácil sin líneas de separación. Muchas pautas de redacción científica recomiendan este enfoque e incluso algunas revistas lo exigen.

El paquete `array` ofrece muchas funciones adicionales. Después de cargarlo con `\usepackage{array}`, puede utilizar las siguientes opciones para `tabular`:

- `m{width}` es similar a `\parbox{width}`: la línea de base está en el medio.
- `b{width}` se comporta como `\parbox[b]{width}`: la línea de base está en la parte inferior.
- `!{code}` inserta código. A diferencia de `@{…}`, el espacio entre columnas no se suprimirá.
- `>{code}` se puede usar antes de una opción `l`, `c`, `r`, `p`, `m` o `b`, e inserta código justo al comienzo de cada entrada de esa columna. Usaremos esta función con frecuencia para insertar comandos de fuentes.
- `<{code}` se puede utilizar después de una opción `l`, `c`, `r`, `p`, `m` o `b`, e inserta código directamente al final de la entrada de esa columna.

Este ejemplo muestra la carga del paquete `array` y demuestra el efecto de `@{}` y los argumentos de alineación `p`, `m` y `b`:

```latex
\documentclass{article}
\usepackage{array}
\begin{document}
\begin{tabular}{@{}lp{1.2cm}m{1.2cm}b{1.2cm}@{}}
\hline
baseline & aligned at the top & aligned at the middle & aligned at the bottom\\
\hline
\end{tabular}
\end{document}
```

La tabla de salida es la siguiente:

> **Figura 5.6** – Una tabla con diferentes alineaciones verticales

Observe la última columna en la Figura 5.6; el texto no está visualmente alineado con la parte inferior de la celda de la tabla. Es importante entender esto: la opción `b` significa que la línea de base del texto de la celda será la línea inferior. Luego, LaTeX alinea todas las líneas de base en el mismo nivel vertical. Por lo tanto, para alinear el texto donde la línea de base es su línea inferior con las otras líneas de base, el texto debe desplazarse hacia arriba. Puede pensar en las líneas de base como líneas de anclaje; todas las celdas alinean su contenido según estos puntos de anclaje compartidos.

---

### Mejora de la apariencia de las tablas

Veamos ahora cómo ajustar detalles y combinar celdas.

#### Aumento de la altura de la fila

Es posible que haya notado que las líneas horizontales de una tabla pueden quedar incómodamente cerca de las letras mayúsculas. Para solucionar esto, el paquete `array` introduce una longitud llamada `\extrarowheight`. Es `0` por defecto, pero si la establece en un valor positivo, esto agrega espacio vertical adicional encima de cada fila de la tabla.

El siguiente ejemplo, después del primerísimo ejemplo de este capítulo, muestra cómo aumentar la altura de la fila en la línea resaltada. También muestra el efecto de otras opciones de formato de `array`, de la siguiente manera:

```latex
\documentclass{article}
\usepackage{array}
\setlength{\extrarowheight}{4pt}
\begin{document}
\begin{tabular}{@{}>{\itshape}ll!{:}l<{.}@{}}
\hline
Info: & Software & \LaTeX\\
      & Author   & Leslie Lamport\\
      & Website  & www.latex-project.org\\
\hline
\end{tabular}
\end{document}
```

El resultado es el siguiente:

> **Figura 5.7** – Una tabla estirada

Aquí, aplicamos `>{\itshape}` para cambiar la fuente de una columna a cursiva. La construcción `>{...}` se usa a menudo para insertar una declaración de alineación como `\centering`. Sin embargo, hay un problema sutil: declaraciones como el comando `\centering` pueden cambiar el significado interno de `\\`, que es un atajo para `\tabularnewline` dentro de las tablas. Pero el paquete `array` ofrece un comando para repararlo. En tales casos, simplemente agregue el comando `\arraybackslash`, como en el siguiente ejemplo:

```latex
\begin{tabular}{>{\centering\arraybackslash}p{5cm}}
```

Sin esto, el texto en las celdas de párrafo definidas por `p`, `m` o `b` permanecerá completamente justificado.

También puede insertar espacio vertical adicional después de una fila específica utilizando un argumento opcional para `\\`, como `\\[10pt]`.

Incluso puede estirar una tabla completa: el comando `\arraystretch` contiene un factor de estiramiento con un valor predeterminado de 1. Puede redefinirlo para aumentarlo. Por ejemplo, `\renewcommand{\arraystretch}{1.5}` aumentará la altura de las filas en un factor de 1.5, lo que significa agregar un 50 por ciento de espacio. A diferencia de `\extrarowheight`, agrega espacio tanto por encima como por debajo de la fila. Para mantener el efecto limitado, coloque el comando dentro de un grupo o entorno. Alternativamente, puede restablecerlo al valor predeterminado con `\renewcommand{\arraystretch}{1}`.

#### Embellecimiento de tablas

Es posible que nuestras tablas todavía no se vean tan pulidas como las de los libros compuestos profesionalmente. En particular, podríamos mejorar las líneas y sus distancias con respecto al contenido del texto. El paquete `booktabs` ayuda con eso. Al utilizar este paquete, puede mejorar en gran medida la apariencia de sus tablas con nuevos comandos que reemplazan a `\hline` y `\cline`.

He aquí cómo:

1. Utilizando nuestro ejemplo anterior de la Figura 5.4, cargue el paquete `booktabs`:

```latex
\usepackage{booktabs}
```

2. Use los nuevos comandos `\toprule`, `\midrule` y `\bottomrule` en lugar de `\hline`. Puede especificar el grosor como argumento opcional. El código de la tabla se convierte en el siguiente:

```latex
\begin{tabular}{ccc}
\toprule[1.5pt]
\head{Command} & \head{Declaration} & \head{Output}\\
\midrule
\verb|\textrm| & \verb|\rmfamily| & \rmfamily Example text\\
\verb|\textsf| & \verb|\sffamily| & \sffamily Example text\\
\verb|\texttt| & \verb|\ttfamily| & \ttfamily Example text\\
\bottomrule[1.5pt]
\end{tabular}
```

3. Compile para ver la diferencia:

> **Figura 5.8** – Una tabla estirada

Especialmente en la composición tipográfica británica, el término *rule* (regla/filete) se utiliza comúnmente para referirse a una línea. El desarrollador de `booktabs` adoptó esta terminología para los comandos del paquete. Estas son sus definiciones:

- `\toprule[thickness]` dibuja una línea horizontal en la parte superior de la tabla. Si lo desea, se puede especificar un valor de grosor, como `1pt` o `0.5mm`.
- `\midrule[thickness]` crea una línea divisoria horizontal entre las filas de la tabla.
- `\bottomrule[thickness]` dibuja una línea horizontal para rematar una tabla.
- `\cmidrule[thickness](trim){m–n}` dibuja una línea horizontal desde la columna `m` hasta la columna `n`. El argumento `(trim)` es opcional, similar al argumento de grosor. Puede ser `(l)` o `(r)` para recortar la línea en su extremo izquierdo o derecho. Escriba `(lr)` para recortar en ambos extremos. Incluso puede especificar un ancho de recorte como en `(l{10pt})`.

El paquete `booktabs` evita intencionadamente definir líneas verticales. Ni las líneas verticales ni las dobles se recomiendan para tablas limpias y profesionales. De hecho, ambas se consideran generalmente un estilo tipográfico deficiente. En su lugar, confíe en `\toprule`, `\midrule` y `\bottomrule`. Puede utilizarlos sin argumentos opcionales; veamos cómo hacerlo a continuación.

#### Personalización del grosor y espaciado de líneas

Mencionamos anteriormente el comando `\setlength` en la sección *Aumento de la altura de la fila* de este capítulo. En lugar de especificar el grosor de línea con un argumento opcional para `\toprule`, `\midrule`, `\cmidrule` o `\bottomrule`, siempre podemos omitirlo. En su lugar, lo configuramos globalmente, una vez para todo nuestro documento, utilizando `\setlength` en el preámbulo.

Por lo tanto, por ejemplo, después de `\usepackage{booktabs}`, puede escribir lo siguiente:

```latex
\setlength{\heavyrulewidth}{1.5pt}
```

Ahora simplemente use `\toprule` y `\bottomrule` sin argumento, y siempre tendrán 1.5 pt de grosor.

Se pueden ajustar las siguientes longitudes del paquete `booktabs`:

- `\heavyrulewidth`: El grosor de las líneas superior e inferior con `\toprule` y `\bottomrule`
- `\lightrulewidth`: El grosor de las líneas intermedias con `\midrule`
- `\cmidrulewidth`: El grosor de `\cmidrule`
- `\cmidrulekern`: El recorte en `\cmidrule`
- `\abovetopsep`: El espacio encima de la línea superior; el valor predeterminado es `0pt`
- `\belowbottomsep`: El espacio debajo de la línea inferior; el valor predeterminado es `0pt`
- `\aboverulesep`: El espacio encima de `\midrule`, `\cmidrule` y `\bottomrule`
- `\belowrulesep`: El espacio debajo de `\midrule`, `\cmidrule` y `\toprule`

Siéntase libre de experimentar con estas configuraciones. Los valores predeterminados están bien equilibrados, pero puede cambiarlos. Los ajustes realizados en su preámbulo se aplicarán a todas las tablas de su documento.

#### Expansión de entradas a través de múltiples columnas

Para agrupar columnas relacionadas bajo un encabezado compartido, podemos combinar celdas de la tabla usando el comando `\multicolumn`.

En nuestro ejemplo, tanto los comandos como las declaraciones representan entradas (*input*), mientras que la tercera columna contiene salidas (*output*). Para reflejar esta estructura, revisaremos la fila del encabezado para abarcar columnas de la siguiente manera:

1. Con base en nuestro ejemplo anterior, inserte una nueva fila de encabezado. Use `*{3}l` para definir tres columnas alineadas a la izquierda. Ponga `@{}` antes y después para eliminar el espacio entre columnas. Aplique el comando `\multicolumn` para combinar celdas. Ajuste el argumento de formato de columna y la línea central. Los cambios se resaltan aquí:

```latex
\begin{tabular}{@{}*{3}l@{}}
\toprule[1.5pt]
\multicolumn{2}{c}{\head{Input}} & \multicolumn{1}{c}{\head{Output}}\\
\head{Command} & \head{Declaration} & \\
\cmidrule(r){1-2}\cmidrule(l){3-3}
\verb|\textrm| & \verb|\rmfamily| & \rmfamily Example text\\
\verb|\textsf| & \verb|\sffamily| & \sffamily Example text\\
\verb|\texttt| & \verb|\ttfamily| & \ttfamily Example text\\
\bottomrule[1.5pt]
\end{tabular}
```

2. Compile y examine el resultado:

> **Figura 5.9** – Una tabla con celdas combinadas

Usamos el comando `\multicolumn` dos veces: una para combinar dos celdas y, sorprendentemente, otra vez para una sola celda; veremos en un segundo por qué. Veamos primero su definición:

```latex
\multicolumn{number of columns}{formatting options}{entry text}
```

El número de columnas a abarcar puede ser un número entero positivo o simplemente 1. Las opciones de formato se aplicarán en lugar de las opciones especificadas en la definición de `tabular` para esta celda.

Aprovechamos esto cuando usamos `\multicolumn{1}{c}{…}`, anulando la opción `l` de la columna con una opción `c` para centrar solo esta celda.

El otro cambio que hicimos concierne a `\cmidrule`. Lo usamos en lugar de `\midrule`, junto con la opción de recorte, para obtener un espacio entre la columna de entrada y la de salida para mejorar la claridad visual.

#### Inserción de código por columnas

Hay muchos más comandos de fuentes que nos gustaría agregar a la tabla. Sin embargo, escribir comandos `\verb|…|` en cada celda rápidamente se volvería tedioso. En su lugar, podemos aprovechar la construcción `>{…}` del paquete `array` para aplicar formato a columnas enteras.

Actualicemos nuestra definición de `tabular` para establecer nuestras columnas de entrada en la fuente tipográfica de máquina de escribir (*typewriter*). También agregaremos una nueva columna a la izquierda para describir el tipo de comando. Vamos allá:

1. Extienda el preámbulo de nuestro ejemplo definiendo una macro `\normal`. Utilizará el comando `\multicolumn` para generar una celda `l`, sin importar cuál sea el formato de la columna:

```latex
\documentclass{article}
\usepackage{array}
\usepackage{booktabs}
\newcommand{\head}[1]{\textnormal{\textbf{#1}}}
\newcommand{\normal}[1]{\multicolumn{1}{l}{#1}}
\begin{document}
```

2. Como el comando `\verb` no se puede utilizar en los encabezados de tablas, usaremos `\ttfamily` para obtener la fuente de máquina de escribir. También usaremos `\textbackslash` aquí para evitar repetir esa larga frase de comando dentro de las celdas. Use `*{2}>{…}` para insertarlo dos veces. Luego, agregue `<{Example text}` a la última columna para ahorrar trabajo de escritura:

```latex
\begin{tabular}{@{}l*{2}{>{\ttfamily\textbackslash}l}l%
<{Example text}@{}}
\toprule[1.5pt]
& \multicolumn{2}{c}{\head{Input}} & \multicolumn{1}{c}{\head{Output}}\\
```

3. Usaremos nuestra macro `\normal` para evitar el formato de máquina de escribir en el encabezado:

```latex
& \normal{\head{Command}} & \normal{\head{Declaration}} & \normal{}\\
\cmidrule(lr){2-3}\cmidrule(l){4-4}
```

4. Ahora continuamos enumerando los nombres de los comandos de fuentes:

```latex
Family & textrm & rmfamily & \rmfamily\\
       & textsf & sffamily & \sffamily\\
       & texttt & ttfamily & \ttfamily\\
\bottomrule[1.5pt]
\end{tabular}
\end{document}
```

5. Compile y luego observe el resultado:

> **Figura 5.10** – Una tabla con comandos de formato de columna

Al escribir `>{\textbackslash\ttfamily}l`, definimos una columna alineada a la izquierda, donde cada entrada comienza automáticamente con una barra invertida y aparece en fuente de máquina de escribir. Escribimos `*{2}{…}` para definir dos columnas de este estilo. Dado que el texto de ejemplo se insertó según la definición de nuestra tabla con `<{…}>`, solo necesitamos colocar las declaraciones en la última columna sin repetir el texto real.

#### Expansión de contenido a través de múltiples filas

Hemos visto cómo distribuir texto a lo largo de varias columnas. ¿Pero qué pasa con abarcar filas? Si bien LaTeX en sí no ofrece un comando integrado para esto, el paquete `multirow` proporciona exactamente lo que necesitamos.

Centremos la palabra "Family" verticalmente, abarcando tres filas. He aquí cómo:

1. En nuestro ejemplo anterior, cargue adicionalmente el paquete `multirow`:

```latex
\usepackage{multirow}
```

2. Reemplace la palabra `Family` con `\multirow{3}{*}{Family}`:

```latex
\multirow{3}{*}{Family} & textrm & rmfamily & \rmfamily\\
```

3. Compile para ver el pequeño cambio:

> **Figura 5.11** – Celdas combinadas verticalmente

Usamos el comando `\multirow` para abarcar tres filas. Su definición es la siguiente:

```latex
\multirow{number of rows}{width}{entry text}
```

La entrada abarcará ese número de filas a partir de la fila en la que se utiliza `\multirow`. Si el número es negativo, abarcará las filas anteriores.

Puede especificar un ancho o simplemente escribir `*` para usar el ancho natural. Si establece un ancho, LaTeX ajustará el texto para que quepa.

El comando `\multirow` comprende más argumentos opcionales para ajustes finos. La documentación en [https://texdoc.org/pkg/multirow](https://texdoc.org/pkg/multirow) describe esto.

Ahora que dominamos el diseño de tablas, veamos cómo agregar texto de leyenda o título.

---

### Adición de leyendas a las tablas

Cuando se trabaja en documentos más extensos donde nuestro texto hace referencia a las tablas, resulta útil agregar leyendas y números a nuestras tablas. Numerar las tablas permite hacer referencias cruzadas fácilmente, mientras que las leyendas brindan a los lectores contexto sobre el contenido de la tabla. LaTeX tiene soporte integrado para ambos.

Finalicemos ahora nuestra tabla de fuentes. Ampliaremos la tabla enumerando comandos de fuentes adicionales. Usaremos la primera columna para describir la categoría de los comandos de fuentes, como familia, peso y forma (*family*, *weight* y *shape*). Luego, agregaremos otra columna para demostrar el efecto de combinar comandos de fuentes.

Para terminar, centraremos la tabla y proporcionaremos un número y una leyenda. Para hacer eso, colocaremos un entorno `table` alrededor de nuestra tabla de ejemplo, usaremos el comando `\centering` dentro de él e insertaremos un comando `\caption` al final del entorno `table`. Agregaremos más comandos de fuentes y añadiremos otra columna a la derecha, que contiene más ejemplos. Desglosemos esto en los siguientes pasos:

1. Comience con la clase `article` y cargue los paquetes `array`, `booktabs` y `multirow`:

```latex
\documentclass{article}
\usepackage{array}
\usepackage{booktabs}
\usepackage{multirow}
```

2. Defina una macro para formatear las celdas del encabezado y una macro para celdas normales, que queremos que estén alineadas a la izquierda:

```latex
\newcommand{\head}[1]{\textnormal{\textbf{#1}}}
\newcommand{\normal}[1]{\multicolumn{1}{l}{#1}}
```

3. Comience el documento:

```latex
\begin{document}
```

4. Ahora, crearemos la tabla, centraremos el contenido y escribiremos todas las filas:

```latex
\begin{table}
\centering
\begin{tabular}{@{}l*{2}{>{\textbackslash\ttfamily}l}%
                l<{Example text}l@{}}
\toprule[1.5pt]
& \multicolumn{2}{c}{\head{Input}} & \multicolumn{2}{c}{\head{Output}}\\
& \normal{\head{Command}} & \normal{\head{Declaration}} & \normal{\head{Single use}} & \head{Combined}\\
\cmidrule(lr){2-3}\cmidrule(l){4-5}
\multirow{3}{*}{Family} & textrm & rmfamily & \rmfamily & \\
                        & textsf & sffamily & \sffamily& \\
                        & texttt & ttfamily & \ttfamily& \\
\cmidrule(lr){2-3}\cmidrule(lr){4-4}
\multirow{2}{1.1cm}{Weight} & textbf & bfseries & \bfseries & \multirow{2}{1.8cm}{\sffamily\bfseries Bold and sans-serif}\\
                            & textmd & mdseries & \mdseries & \\
\cmidrule(lr){2-3}\cmidrule(lr){4-4}
\multirow{4}{*}{Shape} & textit & itshape & \itshape & \\
                       & textsl & slshape & \slshape & \multirow{2}{1.8cm}{\sffamily\slshape Slanted and sans-serif}\\
                       & textsc & scshape & \scshape & \\
                       & textup & upshape & \upshape & \\
\cmidrule(lr){2-3}\cmidrule(lr){4-4}
Default & textnormal & normalfont & \normalfont & \\
\bottomrule[1.5pt]
\end{tabular}
\caption{\LaTeX\ font selection}
\end{table}
```

5. Finalice el documento:

```latex
\end{document}
```

6. Compile, y nuestra tabla ya está lista:

> **Figura 5.12** – Una tabla con una leyenda

Envolvimos el entorno `tabular` dentro de un entorno `table`. Se utiliza de esta manera junto con el comando `\caption`:

```latex
\begin{table}[placement options]
table body
\caption{table title}
\end{table}
```

El entorno `table` es un entorno flotante (*floating environment*). A diferencia del texto normal, puede aparecer en otro lugar distinto del definido por su posición en el código fuente. El argumento de ubicación opcional determina dónde puede aparecer la tabla. Sin embargo, LaTeX posicionará una tabla dentro del texto para lograr buenos saltos de página sin demasiado espacio vacío al final de una página. Pasaremos algún tiempo discutiendo entornos flotantes en el próximo capítulo, específicamente en el contexto de la ubicación de gráficos, y los mismos principios se aplican aquí. Como veremos con las figuras en el próximo capítulo, `\begin{table}[htbp!]` es la opción más flexible.

`\caption` también entiende un argumento opcional. Si escribe `\caption[short text]{long text}`, entonces el texto corto aparecerá en una lista de tablas y el texto largo en el cuerpo del documento. Esto resulta útil si necesita leyendas descriptivas muy largas.

Las tablas se numeran automáticamente. Hablemos del posicionamiento y formato de las leyendas en las siguientes dos secciones.

#### Colocación de leyendas encima de las tablas

En la composición tipográfica profesional, es muy común colocar leyendas encima de las tablas en lugar de debajo. Podemos lograr esto escribiendo `\caption` antes del cuerpo de la tabla. Sin embargo, LaTeX asume que la leyenda siempre estará debajo, lo que resulta en una apariencia apretada de la tabla. Habrá muy poco espacio entre la leyenda y la tabla siguiente. Por lo tanto, es posible que desee agregar algo de espacio, por ejemplo, introduciendo `\vspace{10pt}` directamente después de una leyenda superior.

¿Recuerda el paquete `booktabs`? Si comienza las tablas con `\toprule`, simplemente especifique la longitud `\abovetopsep`, como en el siguiente ejemplo:

```latex
\setlength{\abovetopsep}{10pt}
```

Al colocar esta línea en su preámbulo, se agregará un espacio de 10 pt debajo de la leyenda y encima de la línea superior de la tabla.

#### Personalización de leyendas

De forma predeterminada, las leyendas se ven como texto de cuerpo regular; no hay diferencia visual. ¿Le gustaría tener un ligero cambio en el tamaño de fuente, un formato diferente de la etiqueta, algunos márgenes o sangría, o cualquier otra personalización? El paquete `caption` ofrece una solución potente.

Al utilizar unas pocas opciones, puede mejorar la apariencia visual de todas sus leyendas. Pruebe lo siguiente:

```latex
\usepackage[font=small,labelfont=bf,margin=1cm]{caption}
```

Esta configuración hace que sus leyendas sean un poco más pequeñas que el texto normal, muestra la etiqueta en negrita y garantiza que no sea tan ancha como el texto normal, agregando un margen de 1 cm a cada lado de la leyenda. El paquete proporciona muchas características de personalización, tanto para configuraciones en todo el documento como para ajustar leyendas individuales. Su documentación es extensa y útil. Visite [https://texdoc.org/pkg/caption](https://texdoc.org/pkg/caption) o escriba `texdoc caption` en la línea de comandos para obtener más información.

Hay varios paquetes para el diseño y la apariencia de tablas. En la siguiente sección, conoceremos dichos paquetes.

---

### Mejora de tablas con paquetes adicionales

Al crear tablas en LaTeX, podemos enfrentar varios desafíos de formato. Por ejemplo, es posible que necesitemos ajustar anchos de columnas, insertar saltos de página dentro de tablas, aplicar colores, rotar tablas y lograr una alineación específica. En las siguientes secciones, examinaremos paquetes adicionales diseñados para abordar estas necesidades.

Puede encontrar tablas de ejemplo y enlaces a la documentación en [https://latexguide.org/tables](https://latexguide.org/tables) para cada una de las siguientes secciones.

#### Ajuste automático de columnas al ancho de la tabla

Las columnas `l`, `c` y `r` se ajustan al ancho de su contenido. Para las columnas `p`, usted establece un ancho fijo. De esta manera, es difícil predecir el ancho real de la tabla. ¿No sería una buena idea especificar el ancho de la tabla y dejar que LaTeX decida qué tan anchas pueden ser las columnas? Eso es exactamente lo que hace el paquete `tabularx`. Úselo de la siguiente manera:

```latex
\usepackage{tabularx}
...
\begin{tabularx}{width}{column specifiers}
...
\end{tabularx}
```

El nuevo entorno `tabularx` toma un argumento adicional: el ancho deseado de la tabla. Introduce un nuevo tipo de columna, `X`. Se comporta como una columna `p`, pero las columnas `X` se estiran automáticamente para llenar el espacio disponible. Una columna `X` tomaría todo el espacio disponible. Si usa varias columnas `X`, compartirán el espacio por igual. Por lo tanto, podría escribir, por ejemplo, lo siguiente:

```latex
\begin{tabularx}{0.6\textwidth}{lcX}
```

De esta manera, obtendría una tabla que ocupa el 60 por ciento del ancho del texto: una columna alineada a la izquierda y una centrada tan anchas como su contenido, y una columna de párrafo tan ancha como sea posible hasta alcanzar el 60 por ciento.

A pesar de su simplicidad, la documentación de `tabularx` proporciona más ejemplos, explica los tipos derivados y ofrece consejos, como evitar entradas `\multicolumn` que crucen cualquier columna `X`. Lea la documentación en [https://texdoc.org/pkg/tabularx](https://texdoc.org/pkg/tabularx) o ejecute `texdoc tabularx` en la línea de comandos.

Existen dos enfoques relacionados. LaTeX estándar proporciona una versión con asterisco del entorno `tabular`:

```latex
\begin{tabular*}{width}[position]{column specifiers}
```

La tabla se ajusta al ancho modificando el espacio entre columnas. `tabularx` ha sido desarrollado para satisfacer esta necesidad de una manera más útil.

El paquete `tabulary` proporciona otro entorno tabular sofisticado que toma el ancho total. Pondera el ancho de cada columna según el ancho natural de la celda más ancha de la columna.

En general, el paquete `tabularx` es una excelente opción para ajustar el ancho de la tabla al ancho del texto y es probablemente el paquete tabular más popular.

#### Generación de tablas de varias páginas

Todos los entornos tabulares que hemos visto hasta ahora no pueden extenderse a través de los límites de página. El entorno `tabbing` es una excepción, ya que funciona de manera diferente.

Cuando una tabla contiene una gran cantidad de datos, necesitamos otro enfoque. Existen varios paquetes que ofrecen diferentes formas de manejarlo:

- `longtable` proporciona un entorno con el mismo nombre que es como una versión de varias páginas de `tabular`. Proporciona comandos para configurar leyendas de tabla, leyendas continuadas y encabezados y pies de página especiales cuando ocurre un salto de página. Es probablemente la forma más fácil para tablas de varias páginas y, por lo tanto, es la más popular. La documentación del paquete describe todo lo que necesita. En combinación con el paquete `booktabs`, obtendrá excelentes resultados. Este es el paquete más utilizado.
- `ltxtable` proporciona una combinación de `longtable` y `tabularx`.
- `ltablex` es otro enfoque para combinar las características de `longtable` y `tabularx`.
- `supertabular` ofrece otra extensión de varias páginas del entorno `tabular` utilizado internamente, proporcionando colas y encabezados de tabla opcionales donde ocurren los saltos de página. Se recomienda para documentos de dos columnas.
- `xtab` amplía `supertabular` y reduce algunas de sus debilidades.
- `stabular` implementa una forma sencilla de utilizar saltos de página en `tabular` sin mayores complicaciones.

Si necesita que las tablas puedan extenderse a lo largo de varias páginas, puede consultar los manuales de los paquetes en [https://texdoc.org/](https://texdoc.org/), o utilizar el comando `texdoc` en su computadora. Entre ellos, el paquete `longtable` es probablemente la opción más popular.

#### Coloreado de tablas

Hablamos sobre cómo colorear texto en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*. Para colorear tablas, use el paquete `colortbl`. Podemos combinar todo esto usando la opción `table` con el paquete `xcolor`:

```latex
\usepackage[table]{xcolor}
```

El paquete permite colorear columnas, filas, entradas individuales y líneas de muchas maneras. La documentación del paquete puede brindarle más información; encuéntrela en [https://texdoc.org/pkg/xcolor](https://texdoc.org/pkg/xcolor).

#### Uso de orientación horizontal

Si una tabla es demasiado ancha para caber en modo vertical, puede rotarla a la orientación horizontal. El paquete `rotating` ofrece un entorno llamado `sidewaystable`, que se comporta como el entorno `table` normal pero rota toda la tabla y su leyenda 90 grados, colocándola en su propia página. El paquete incluye más entornos y comandos relacionados con la rotación.

#### Alineación de columnas en el punto decimal

Las columnas que contienen números son más legibles cuando las entradas están alineadas en el punto decimal o en un exponente si está presente. Varios paquetes ayudan con esto:

- `siunitx` es un paquete muy moderno y desarrollado activamente, diseñado principalmente para componer valores con unidades de manera coherente, de acuerdo con las convenciones científicas. Proporciona un tipo de columna tabular para dicha alineación decimal de números.
- `dcolumn` ofrece un tipo de columna para alinear en una coma, un punto u otro carácter específico.
- `rccol` define un tipo de columna donde los números están centrados a la derecha: están centrados en relación con otras entradas pero alineados a la derecha entre sí. De esta manera, los dígitos correspondientes se alinean a lo largo de la columna. Sin embargo, `siunitx` sería la mejor opción.

A diferencia de `dcolumn` y `rccol`, el paquete `siunitx` es más nuevo y muy potente.

#### Manejo de columnas estrechas

El texto en columnas muy estrechas puede requerir atención especial porque la justificación puede resultar difícil si hay espacio limitado. He aquí algunos consejos:

- Asegure una correcta separación silábica. Si es necesario, mejórela como lo hicimos en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*. TeX no divide en sílabas la primera palabra de una línea, una caja o una entrada de tabla. Por lo tanto, una palabra larga puede cruzar el límite de la columna. Para forzar la división de palabras, inserte una palabra vacía: escriba `\hspace{0pt}` directamente al principio.
- Cargue el paquete `microtype` para mejorar la justificación. Tiene un efecto significativo, especialmente en columnas estrechas.
- La justificación completa en columnas `p` y similares puede verse mal porque pueden aparecer grandes espacios en blanco. Considere usar `>{\raggedright\arraybackslash}` para dichas columnas.
- Desde el paquete `ragged2e`, usar el comando `\RaggedRight` puede dar resultados aún mejores y no requiere `\arraybackslash`.

Estas estrategias ayudan a evitar espacios no deseados y mejoran la apariencia general de sus tablas.

---

### Resumen

En este capítulo, ha aprendido a crear y formatear tablas. Cubrimos métodos para organizar texto en columnas, agregar leyendas, combinar filas y columnas, usar paquetes para ajustar columnas automáticamente y crear tablas coloreadas, horizontales e incluso de varias páginas.

Puede abrir la documentación de cualquier paquete mencionado ejecutando `texdoc nombre_paquete` en la línea de comandos o visitando `https://texdoc.org/pkg/<nombre_paquete>`.

LaTeX también puede generar una lista de tablas, como una tabla de contenidos. Veremos eso en el [Capítulo 8](https://subscription.packtpub.com/book/business-and-other/9781805804574/8), *Gestión de contenidos, índices y bibliografía*.

LaTeX numera nuestras tablas automáticamente. Podemos usar estos números para hacer referencia a las tablas. El [Capítulo 7](https://subscription.packtpub.com/book/business-and-other/9781805804574/7), *Uso de referencias cruzadas*, está dedicado a hacer referencia a secciones y objetos, incluidas tablas.

El mismo principio se aplica a figuras con imágenes, que es el tema del próximo capítulo.
