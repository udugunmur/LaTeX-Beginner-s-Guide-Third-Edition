# LaTeX Beginner's Guide
## Capítulo 14: Resolución de Problemas

Ahora que hemos creado documentos completos y presentaciones enteras, es hora de ver qué sucede cuando las cosas no funcionan como se esperaba. Tarde o temprano, todo proyecto de LaTeX se encuentra con errores o advertencias. Eso es perfectamente normal y a menudo se debe a problemas menores, como errores tipográficos en los nombres de comandos o llaves desequilibradas. Incluso los usuarios profesionales de LaTeX lidian con errores a diario; ellos saben cómo manejarlos de manera eficiente. Aprendamos a hacer eso también.

En este capítulo, veremos cómo lidiar con problemas comunes en LaTeX, incluyendo lo siguiente:

- Comprensión y corrección de errores
- Manejo de advertencias
- Cómo evitar clases y paquetes obsoletos
- Resolución general de problemas

Comencemos viendo cómo resolver errores.

---

### Comprensión y corrección de errores

Cuando el motor de LaTeX encuentra un problema, informa de un error. Estos mensajes están destinados a ayudar, por lo que vale la pena leerlos con atención. Junto con el número de línea donde ocurrió el problema, LaTeX proporciona un breve mensaje de diagnóstico que describe lo que salió mal.

Concéntrese en el primer mensaje de error que vea. Si continúa compilando, los errores siguientes suelen ser solo efectos secundarios del problema original que confundió al compilador.

Creemos un pequeño documento de prueba. Es posible que conozca el clásico ejemplo "Hello world!" del aprendizaje de lenguajes de programación; haremos lo mismo en LaTeX. Aunque estamos familiarizados con las mayúsculas especiales utilizadas en las palabras TeX y LaTeX, veamos qué sucede si intentamos utilizar el comando `\Latex` en su lugar:

1. Cree un nuevo documento con estas líneas:

```latex
\documentclass{article}
\begin{document}
\Latex\ says: Hello world!
\end{document}
```

2. Compile el documento. LaTeX se detendrá e informará este mensaje de error:

```text
! Undefined control sequence.
l.3 \Latex
           \ says: Hello world!
```

3. Haga clic en el botón Cancelar (*Cancel*) para detener la compilación; en TeXworks, es el icono de Cancelar en la esquina superior izquierda.

4. En nuestro código del paso 1, vaya a la línea 3 y reemplace `\Latex` con `\LaTeX`. Luego compile de nuevo. Esta vez, LaTeX produce una salida sin errores:

> **Figura 14.1** – La salida del documento corregido

Los comandos de LaTeX distinguen entre mayúsculas y minúsculas (*case-sensitive*). Como no respetamos esa regla, LaTeX tuvo que lidiar con una macro llamada `\Latex`, que simplemente no conoce. Dado que un comando de LaTeX también se denomina secuencia de control (*control sequence*), el mensaje de error informa `Undefined control sequence`.

Cuando LaTeX encuentra un error, detiene el procesamiento y espera la entrada del usuario. Sin embargo, puede presionar la tecla Enter para continuar, pero esto a menudo da como resultado una salida incompleta o incorrecta. En la mayoría de los casos, es mejor cancelar la compilación y corregir el error de inmediato.

Desglosemos el mensaje de error en sus partes principales:

- Un mensaje de error comienza con un signo de exclamación, seguido de una breve descripción del problema
- A continuación, LaTeX indica el número de línea de entrada donde ocurrió el error y resalta la parte de esa línea que lo causó
- Después de un salto de línea, LaTeX imprime la parte restante de la línea de entrada para dar contexto

Así que no se queda adivinando. LaTeX le dice precisamente lo que necesita saber:

- El tipo de error
- La ubicación precisa donde ocurrió

La mayoría de los editores muestran el número de línea o le permiten saltar al número de línea que ingrese. Como ahora puede encontrar fácilmente el punto problemático en el código fuente, solo necesita saber por qué LaTeX se queja; eso es lo que veremos en las siguientes secciones.

Si está utilizando Overleaf, hay una pequeña advertencia: Overleaf oculta los mensajes de error, continúa compilando y muestra la salida incluso cuando ocurre un error. La siguiente captura de pantalla muestra cómo se ve nuestro documento en Overleaf con el error presente:

> **Figura 14.2** – Un error de código visto en Overleaf

A primera vista, nuestro documento parece compilarse. Pero en una inspección más cercana, notamos lo siguiente:

- Al principio, falta la palabra LaTeX
- Aparece un pequeño número rojo sobre la salida

Ese pequeño número rojo indica un error y no debe ignorarse. De lo contrario, como vimos aquí, podemos obtener un documento con una salida faltante o incorrecta, y en un documento grande, eso podría ser difícil de notar.

Haga clic en el número rojo para abrir una ventana con el mensaje de error:

> **Figura 14.3** – Un mensaje de error en Overleaf

Ahora podemos ver el mensaje de error completo, la explicación y la ubicación exacta en la línea 3. En la Figura 14.2, la línea problemática 3 está marcada con una cruz roja. Puede ver el archivo de registro completo con información detallada, errores y advertencias haciendo clic en **View Raw Logs** en la esquina inferior izquierda.

A continuación, analizaremos más de cerca los mensajes de error comunes de TeX y LaTeX. Los repasaremos paso a paso en las siguientes secciones, comenzando con los errores que ocurren en el preámbulo.

#### Manejo del preámbulo y del cuerpo del documento

El preámbulo contiene todas las configuraciones para todo el documento. Aquí es donde elegimos la clase de documento, cargamos paquetes, establecemos opciones y definimos comandos. El comando `\begin{document}` marca el final del preámbulo y el comienzo del cuerpo del documento, donde va el contenido real. Si algo sale mal con esta estructura, LaTeX normalmente informará uno de los siguientes errores:

- `Missing \begin{document}`: En muchos casos, eso simplemente significa que se olvidó el comando `\begin{document}`. Sin embargo, el error también puede aparecer si el comando está presente. Una razón común es que un carácter o comando en el preámbulo produce salida; puede detectarlo y eliminarlo. Solo recuerde que la salida no está permitida antes de `\begin{document}`.
- `Can be used only in preamble`: Este mensaje de error indica que se usó un comando destinado a usarse en el preámbulo después de `\begin{document}`. Un ejemplo típico es el comando `\usepackage`. Mueva el comando hacia arriba en su preámbulo o elimínelo si no pertenece allí.
- `Option clash for package`: Ocurre un conflicto de opciones (*option clash*) cuando LaTeX carga un paquete más de una vez pero con opciones diferentes. Eso puede suceder si tiene dos líneas `\usepackage{…}` para el mismo paquete en el preámbulo de su documento. Si hizo eso, generalmente es mejor reducirlo a una sola llamada a `\usepackage` con las opciones deseadas. A veces la causa es menos obvia: una clase o un paquete ya puede cargar el paquete junto con algunas opciones. Si desea cargar el paquete también, pero con diferentes opciones, LaTeX se queja.

Puede resolver un conflicto de opciones omitiendo la recarga del paquete y especificando las opciones deseadas en las opciones de la clase de documento. Recuerde, los paquetes heredan las opciones de la clase. Algunos paquetes y clases incluso ofrecen comandos para establecer opciones después de cargar. Por ejemplo, el paquete `hyperref` proporciona `\hypersetup{options}` y, de manera similar, el paquete `caption` ofrece `\captionsetup`.

En las siguientes secciones, veremos problemas comunes en el cuerpo del documento.

#### Uso de comandos y entornos

Los nombres de los comandos se pueden escribir mal o utilizar incorrectamente con facilidad. Veamos las quejas habituales de LaTeX:

- `Undefined control sequence`: Al igual que en nuestro ejemplo de la sección anterior, LaTeX se topó con un nombre de comando desconocido. Hay dos razones posibles:
  - El nombre del comando puede estar mal escrito. En ese caso, solo necesita corregirlo y reiniciar la composición tipográfica.
  - El nombre del comando es correcto, pero está definido por un paquete que no cargó. Agregue un comando `\usepackage` a su preámbulo para cargar el paquete requerido.
- `Environment undefined`: Esto es similar a `Undefined control sequence`, pero esta vez comenzamos un entorno desconocido. Nuevamente, esto puede deberse a un error tipográfico o a un paquete faltante; ya sabe cómo corregirlo.
- `Command already defined`: Esto sucede cuando crea un comando con un nombre que ya se usa, por ejemplo, con `\newcommand` o `\newenvironment`. Simplemente elija un nombre diferente. Si realmente desea anular ese comando, use `\renewcommand` o `\renewenvironment` en su lugar, pero tenga cuidado al redefinir un comando existente: si LaTeX o los paquetes ya lo usan internamente, cambiarlo puede causar efectos secundarios.
- `Missing control sequence inserted`: Se esperaba una secuencia de control pero no apareció. Una causa común es usar `\newcommand`, `\renewcommand` o `\providecommand` sin especificar un nombre de comando como primer argumento.
- `\verb illegal in command argument`: El comando `\verb` para producir texto literal (*verbatim*) es delicado; no se puede utilizar dentro de argumentos de comandos o entornos. El paquete `examplep` ofrece comandos para usar texto literal en tales lugares.

De esta lista, el primer error es probablemente el que ocurre con mayor frecuencia, ya que los errores de escritura ocurren con tanta facilidad como olvidarse de cargar un paquete.

#### Escritura de fórmulas matemáticas

Cuando LaTeX encuentra un error durante la composición tipográfica de expresiones matemáticas, puede ocurrir uno de los siguientes mensajes de error:

- `Missing $ inserted`: Muchos comandos solo se pueden usar en modo matemático. Piense en los símbolos; la mayoría de ellos requieren el modo matemático. Si LaTeX no está en modo matemático y encuentra dicho símbolo, se detiene e imprime ese error. Por lo general, podemos resolver tales errores insertando ese `$` faltante. Olvidar iniciar o finalizar el modo matemático es uno de los errores más frecuentes. Además, recuerde que no puede utilizar saltos de párrafo dentro de una expresión matemática. Esto significa que las líneas en blanco dentro de una expresión matemática son ilegales; tenemos que terminar el modo matemático antes de la línea en blanco.
- `Command invalid in math mode`: Algunos comandos no son aplicables dentro de fórmulas matemáticas. En ese caso, use el comando fuera del modo matemático.
- `Double subscript, double superscript`: No se pueden compilar dos subíndices o superíndices consecutivos. Por ejemplo, en `$a_n_1$`, LaTeX no puede decidir si `a_n` debe tener un subíndice 1, o si `a` debe tener un subíndice `n_1`. Para corregir eso, agrúpelos entre llaves, como en `$a_{n_1}$`.
- `Bad math environment delimiter`: Esto puede resultar de un anidamiento ilegal del modo matemático. No debe iniciar el modo matemático si ya está dentro de él. Por ejemplo, no use `\[` dentro de un entorno `equation`. Del mismo modo, no debe finalizar el modo matemático antes de iniciarlo. Asegúrese de que los delimitadores de modo matemático coincidan y que las llaves estén equilibradas.

En el [Capítulo 9](https://subscription.packtpub.com/book/business-and-other/9781805804574/9), *Escritura de fórmulas matemáticas*, aprendimos cómo evitar tales errores.

#### Trabajo con archivos

Si LaTeX no puede abrir un archivo para usted, puede generar uno de los siguientes errores:

- `File not found`: LaTeX intentó abrir un archivo inexistente. Posiblemente, hizo una de las siguientes acciones:
  - Usó `\include` o `\input` para incluir un archivo `.tex`, pero no existe un archivo con el nombre especificado
  - El archivo tiene espacios o caracteres especiales en el nombre; es mejor evitarlo
  - Intentó usar un paquete inexistente o escribió mal el nombre del paquete
  - Usó una clase de documento que no existe o tiene un nombre diferente
  Simplemente corrija el nombre del archivo en su documento de entrada o cámbiele el nombre.
- `\include cannot be nested`: Aprendimos en el [Capítulo 11](https://subscription.packtpub.com/book/business-and-other/9781805804574/11), *Desarrollo de documentos grandes*, que no podemos usar el comando `\include` dentro de un archivo que se está incluyendo a sí mismo. En su lugar, usamos `\input` dentro de dichos archivos.

Es bueno evitar caracteres especiales y espacios en los nombres de archivo. Tanto LaTeX como el sistema operativo pueden tener problemas con caracteres inusuales en los nombres de archivos, por lo que es bueno limitarse a letras comunes, dígitos, guiones y guiones bajos.

#### Creación de tablas y matrices

Es cierto que los entornos `tabular` y `array` no tienen la sintaxis más sencilla. Esos `&` y `\\` pueden extraviarse fácilmente, lo que hace que LaTeX se queje. Además, debemos tener cuidado con el formateo de los argumentos. Estos son los posibles errores que puede ver con respecto a los argumentos del entorno:

- `Illegal character in array arg`: En el argumento de un entorno `tabular` o `array`, puede especificar el formato de columna. Alinea caracteres como `l`, `c`, `r`, `p`, `@` y argumentos de ancho como `{1cm}`. Si utiliza algún carácter que no tenga ese significado, LaTeX se lo indicará. Lo mismo se aplica al argumento de formato de `\multicolumn`.
- `Missing p-arg in array arg`: Un poco más específico que el mensaje anterior, este nos dice que falta el argumento de ancho para la opción `p`. Complemente `p` con un ancho como `{1cm}` o cambie `p` a otra opción, como `l`, `c` o `r`.
- `Missing @-exp in array arg`: Falta la expresión después de la opción `@`. Solo necesita agregarla, entre llaves, o eliminar la opción `@`.

Ahora echaremos un vistazo a los posibles mensajes de error relacionados con el cuerpo de la tabla:

- `Misplaced alignment tab character &`: Como sabe, el carácter ampersand tiene el significado especial de separar columnas en una fila de un entorno `tabular` o `array`. Si lo usa accidentalmente en texto normal, aparecerá este error. Escriba `\&` si desea un símbolo de ampersand en la salida.
- `Extra alignment tab has been changed to \cr`: Esto sucede si usa demasiados caracteres de tabulación de alineación `&`, que sirven para dividir columnas. Por ejemplo, con dos columnas, no podemos tener cuatro caracteres `&` como divisores de columna. Tal error puede ocurrir si nos olvidamos de agregar `\\`, que finaliza una fila.

En el [Capítulo 5](https://subscription.packtpub.com/book/business-and-other/9781805804574/5), *Creación de tablas*, discutimos la sintaxis adecuada para evitar tales errores.

#### Trabajo con listas

Las listas siguen una estructura específica y no se pueden anidar infinitamente. En algún momento, LaTeX puede quejarse, como en los siguientes mensajes de error:

- `Too deeply nested`: Podemos anidar hasta cuatro niveles de una lista. Si mezclamos tipos de listas, podemos llegar hasta seis niveles. Pero si vamos más allá de lo que acepta LaTeX, recibiremos este mensaje de error. Piense si realmente necesita un anidamiento tan profundo. Si este es el caso, considere usar comandos de sección como `\paragraph` o `\subsubsection` para niveles externos.
- `Something’s wrong--perhaps a missing \item`: Falta un comando `\item`. Es posible que tengamos texto simple en una lista `itemize` o `enumerate`. Luego necesitamos insertar un comando `\item` antes de ese texto.

En el [Capítulo 4](https://subscription.packtpub.com/book/business-and-other/9781805804574/4), *Creación de listas*, aprendimos la sintaxis adecuada para listas.

#### Trabajo con figuras y tablas flotantes

En el [Capítulo 5](https://subscription.packtpub.com/book/business-and-other/9781805804574/5), *Creación de tablas*, y el [Capítulo 6](https://subscription.packtpub.com/book/business-and-other/9781805804574/6), *Inclusión de imágenes*, aprendimos cómo insertar figuras y tablas y ajustar su ubicación. Si usa muchos objetos flotantes, es decir, figuras o tablas, puede encontrar este error: `Too many unprocessed floats`.

Si usa un objeto flotante y LaTeX no encuentra un lugar apropiado (por ejemplo, puede que no haya espacio), guarda el objeto para colocarlo más adelante. Si eso sucede a menudo, el espacio de LaTeX para objetos flotantes puede llenarse, causando este error. Se puede resolver de la siguiente manera:

- Agregando opciones de ubicación, como `[htbp!]`, a los entornos `figure` y `table`, reduciendo así sus requisitos de ubicación
- Insertando `\clearpage` para vaciar los flotantes en un lugar adecuado, o quizás aún más ingenioso: `\afterpage{\clearpage}` con el paquete `afterpage`

En la sección final, examinamos otros posibles escenarios de error.

#### Errores generales de sintaxis

Al igual que con cualquier lenguaje de marcado o programación, los documentos de LaTeX deben seguir una sintaxis. Por ejemplo, las llaves y los delimitadores deben coincidir. Si hay un error, LaTeX lo señalará:

- `Missing { inserted, missing } inserted`: Aunque se lee como si las llaves desequilibradas pudieran causarlo, puede deberse a que TeX se confunde. Lo más probable es que el error haya ocurrido antes del punto donde LaTeX lo informa. Por lo tanto, verifique minuciosamente la sintaxis utilizada.
- `Extra }, or forgotten $`: Esta vez, hay un problema con llaves no balanceadas, o los delimitadores del modo matemático no coinciden correctamente. Necesita corregir la coincidencia.
- `There’s no line here to end`: El uso de `\\` o `\newline` entre párrafos en modo vertical no tiene sentido y provoca este error. No intente obtener más espacio vertical escribiendo `\\`. Utilice `\vspace` en su lugar, u otros comandos de salto como `\bigskip`, `\medskip` o `\smallskip`. Por ejemplo, podemos producir una línea en blanco con `\vspace{\baselineskip}`.

La lista de preguntas frecuentes sobre TeX y LaTeX, llamada TeX FAQ, enumera los mensajes de error junto con explicaciones y sugerencias. Está disponible en [https://texfaq.org/#errors](https://texfaq.org/#errors).

Una vez que corregimos todos los errores, es posible que todavía haya algunos defectos en el documento. LaTeX imprime advertencias si ve un problema potencial. En la siguiente sección, veremos cómo lidiar con ellas.

---

### Manejo de advertencias

Los mensajes de advertencia son para su información. No siempre apuntan a un problema grave, pero a menudo es una buena idea leer estos consejos con atención y actuar en consecuencia. Esto puede mejorar su documento.

Probaremos esto ahora. Digamos que queremos enfatizar texto que está en una fuente sans-serif. Esperamos texto sans-serif en cursiva como resultado.

Intentemos esto:

1. Tome nuestro ejemplo "Hello world!" y modifíquelo de esta manera:

```latex
\documentclass{article}
\renewcommand{\familydefault}{\sfdefault}
\begin{document}
\emph{Hello world!}
\end{document}
```

2. Compile. LaTeX imprimirá una advertencia en el archivo de registro:

```text
LaTeX Font Warning: Font shape `OT1/cmss/m/it' in size <10> not available
(Font)              Font shape `OT1/cmss/m/sl' tried instead on input line 4.
```

3. Verifique la salida:

> **Figura 14.4** – Forma inclinada en lugar de forma en cursiva

La macro `\familydefault` representa la familia de fuentes predeterminada utilizada en el documento de LaTeX. Para esta macro, especificamos el valor `\sfdefault`, que es la fuente sans-serif predeterminada. Esto significa que sans-serif es ahora la opción predeterminada, independientemente de la fuente elegida. Como puede imaginar, otros valores posibles son `\rmdefault` y `\ttdefault`. Al cambiar `\familydefault`, no tenemos que escribir `\sffamily` repetidamente.

Pero luego enfatizamos nuestro texto y recibimos una advertencia. El mensaje significa que no hay ninguna fuente Computer Modern Sans Serif (CMSS) en la codificación de fuentes predeterminada OT1, en peso medio (`m`) y forma de cursiva (`it`) en tamaño de 10pt. Además, LaTeX nos dijo cómo intentó reparar el problema: en lugar de cursiva, eligió una forma inclinada (*slanted*). Eso no está tan mal: al menos se ve similar y se produce la salida.

Esto es básicamente lo que sucede cuando ocurren advertencias: LaTeX nos informa de un problema o desventaja potencial, luego intenta elegir la mejor alternativa y continúa con la composición tipográfica. No es raro que un documento más largo produzca docenas de advertencias, la mayoría de las veces relacionadas con la justificación horizontal o vertical.

A menudo, no pasa nada si ignora las advertencias que no parecen muy graves, aunque darles seguimiento es un buen hábito. Cualquiera que desee tener un documento perfecto corrige todas las advertencias. De esta manera, no podemos pasar por alto un problema potencial.

En las siguientes secciones, abordaremos situaciones frecuentes con advertencias.

#### Justificación de texto

De forma predeterminada, LaTeX alinea el texto tanto en el margen izquierdo como en el derecho. LaTeX hace esto ajustando el espacio entre palabras y letras. Eso se llama justificación completa.

Si LaTeX no puede lograr eso, podemos recibir una de las siguientes advertencias:

- `Overfull \hbox`: Una línea es demasiado larga y no se ajusta al ancho del texto. Esto puede hacer que el texto se extienda más allá del margen. Esto puede deberse a problemas de separación silábica, que podemos solucionar utilizando `\hyphenation` o insertando `\-`, como aprendió en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*. Podría romper la línea manualmente o pulir sus palabras de otra manera.
- `Underfull \hbox`: Lo opuesto a la advertencia anterior; una línea no es lo suficientemente ancha para ajustarse al ancho del texto, por lo que LaTeX no pudo lograr la justificación completa. Esto podría ser causado por `\linebreak`, si no hay suficiente texto en la línea. Además, `\\` o `\newline` pueden causarlo, como `\\\\`, ya que se ha interrumpido la justificación del texto.
- `Overfull \vbox`: La página es demasiado larga porque TeX no pudo dividirla en consecuencia. El texto puede sobresalir más allá del margen inferior.
- `Underfull \vbox`: No hay suficiente texto en la página. TeX tuvo que dividir la página demasiado pronto.

En el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*, aprendimos cómo mejorar la justificación, reduciendo tales advertencias. Recuerde, simplemente cargar el paquete `microtype` puede ayudar.

La declaración `\sloppy` cambia a un tipo de composición tipográfica bastante relajado, evitando así muchas de estas advertencias. Su contraparte es `\fussy`, que vuelve al comportamiento predeterminado. Suponga que alguna vez desea utilizar `\sloppy` porque una composición tipográfica relajada con un espaciado posiblemente más estirado está bien para usted; entonces es mejor mantenerla local agrupando o utilizando el entorno correspondiente: `\begin{sloppypar} … \end{sloppypar}`.

Además, consulte las recomendaciones y alternativas sobre `\sloppy` en `l2tabu`, mencionado en el [Capítulo 11](https://subscription.packtpub.com/book/business-and-other/9781805804574/11), *Desarrollo de documentos grandes*.

#### Referencias

Muchas advertencias tienen que ver con las referencias. Los errores comunes incluyen etiquetas o claves de citas faltantes, claves duplicadas o simplemente la necesidad de otra ejecución de composición tipográfica.

Pueden ocurrir las siguientes advertencias:

- `Label multiply defined`: `\label` o `\bibitem` se ha utilizado con un nombre de etiqueta que ya se ha utilizado. Haga que los nombres de las etiquetas sean únicos; recuerde lo que hicimos en el [Capítulo 7](https://subscription.packtpub.com/book/business-and-other/9781805804574/7), *Uso de referencias cruzadas*.
- `There were multiply-defined labels`: Como la advertencia anterior, pero después de procesar el documento completo, dos comandos `\label` han definido la misma etiqueta.
- `Labels may have changed. Rerun to get cross-references right`: Simplemente vuelva a componer tipográficamente para permitir que LaTeX corrija las referencias.
- `Reference ... on page ... undefined`: Se ha utilizado `\ref` o `\pageref` sin una definición `\label` correspondiente. Inserte un comando `\label` en un lugar adecuado.
- `Citation ... on page ... undefined`: Un comando `\cite` no tenía un comando `\bibitem` correspondiente, o ninguna clave de BibTeX en el archivo `.bib`.
- `There were undefined references or citations`: Resumiendo después del procesamiento: cualquier comando `\ref` o `\cite` no tenía un comando `\label` o `\bibitem` correspondiente.

Siempre que reciba advertencias sobre referencias, es una buena idea volver a ejecutar la composición tipográfica. A menudo, dichas advertencias desaparecen porque LaTeX no pudo resolver todas las referencias durante la primera ejecución.

#### Elección de fuentes

Cuando LaTeX no puede utilizar una fuente según sea necesario, puede imprimir una de las siguientes advertencias:

- `Font shape … in size <…> not available`: Eligió una fuente que no está disponible. Esto puede ser el resultado de combinar comandos de fuentes que producen una fuente inexistente. Además, simplemente podría no estar disponible en ese tamaño. LaTeX elegirá una fuente o tamaño diferente y le informará sobre esa elección en detalle.
- `Some font shapes were not available, defaults substituted`: LaTeX imprime esto después de procesar todo el documento si alguna de las fuentes elegidas no estaba disponible.

Compruebe dónde se produce dicha advertencia para ver si el tamaño y la forma de la fuente son adecuados para usted. De lo contrario, puede considerar usar otra fuente, como hicimos en el [Capítulo 10](https://subscription.packtpub.com/book/business-and-other/9781805804574/10), *Uso de fuentes*.

#### Colocación de figuras y tablas

Incluso si no hay errores, es posible que LaTeX no pueda colocar una figura o tabla correctamente. En tal caso, LaTeX puede mostrar una de las siguientes advertencias:

- `Float too large for page`: Una figura o tabla es demasiado grande para caber en la página. Se imprimiría, pero la página se volvería demasiado grande.
- `h float specifier changed to ht`: Si especificó una opción `h` para una figura o tabla flotante que no cabe allí, se colocaría en la parte superior de la página siguiente y se emitiría esa advertencia. Lo mismo puede ocurrir para `!h` y `!ht`.

El uso de todas las opciones de ubicación disponibles, como en `\begin{figure}[!htbp]` o `\begin{table}[!htbp]`, como se mencionó en el [Capítulo 6](https://subscription.packtpub.com/book/business-and-other/9781805804574/6), *Inclusión de imágenes*, puede evitar muchos problemas de ubicación.

#### Personalización de la clase de documento

LaTeX puede emitir una advertencia que dice `Unused global option(s)` si utiliza una opción de clase no válida. Esto significa que especificó una opción para `\documentclass` que es desconocida para la clase y para cualquier paquete cargado. Esto podría ser, por ejemplo, un tamaño de fuente base que no es compatible. Simplemente verifique la opción de la que se queja LaTeX.

Además, los paquetes mismos pueden imprimir advertencias si prevén problemas. Todas estas advertencias tienen como objetivo ayudarle a diseñar su documento, por lo que es bueno mirar cada una de ellas.

Incluso si obtiene un documento sin errores ni advertencias, es posible que aún sea imperfecto si utiliza paquetes o clases que ya no se actualizan. Veremos algunos paquetes obsoletos bien conocidos en la siguiente sección.

---

### Cómo evitar clases y paquetes obsoletos

Al final del [Capítulo 11](https://subscription.packtpub.com/book/business-and-other/9781805804574/11), *Desarrollo de documentos grandes*, discutimos los peligros de la información desactualizada. LaTeX ha existido durante décadas, y también tutoriales, ejemplos, paquetes y plantillas. Muchos están totalmente obsoletos y algunos incluso se refieren al antiguo estándar LaTeX 2.09, cuando las clases de documentos no existían. Señalamos la guía definitiva, `l2tabu`, que viene al rescate.

Muchos problemas surgen del uso de paquetes obsoletos. Por ejemplo, algunos que ya no se mantienen pueden entrar en conflicto con paquetes más nuevos. A menudo, necesita encontrar el sucesor recomendado de un paquete obsoleto y usarlo.

Para ayudarle en este asunto, aquí hay una breve lista que muestra los paquetes obsoletos y sus respectivos sucesores recomendados:

> **Figura 14.5** – Paquetes obsoletos y sucesores recomendados

Eso no está escrito en piedra. Por supuesto, aún puede utilizar los llamados paquetes obsoletos. Pueden funcionar bien incluso hoy en día. Pero consulte su descripción en la página principal de su paquete en CTAN. Por lo general, hay comentarios sobre si los paquetes siguen siendo relevantes o están obsoletos, y también enumera los paquetes alternativos recomendados. Puede visitar la página de inicio del paquete en la URL que comienza con [https://ctan.org/pkg/](https://ctan.org/pkg/), seguida del nombre del paquete, como [https://ctan.org/pkg/geometry](https://ctan.org/pkg/geometry) para el paquete `geometry`.

Puede encontrar una versión actualizada de esa lista en [https://latexguide.org/obsolete](https://latexguide.org/obsolete).

Además, continuaremos con algunos consejos generales en la siguiente sección.

---

### Resolución general de problemas

Puede haber situaciones en las que no podamos resolver un problema simplemente leyendo y actuando sobre las advertencias o los mensajes de error. Imagine un error misterioso, una ubicación de error imposible de rastrear, referencias irresolubles o simplemente mensajes poco claros de clases o paquetes.

Localizar la causa por el número de línea impreso por LaTeX, o sabiendo lo que hemos hecho desde la ejecución de composición tipográfica anterior, generalmente ayuda. Una vez que hemos encontrado una línea o fragmento problemático, podemos eliminarlo o corregirlo. De lo contrario, podría resultar difícil.

Estos son los primeros pasos generales que podemos seguir:

- **Compilar varias veces**: Esto puede ser necesario para una correcta referenciación, la colocación adecuada de figuras flotantes y la creación de una tabla de contenidos, bibliografías y listas de tablas y figuras.
- **Verificar el orden en el que carga los paquetes**: Algunos paquetes, como `hyperref`, no funcionan bien si se cargan antes o después de paquetes específicos. Puede intercambiar algunas líneas para corregir o probar eso.
- **Eliminar archivos auxiliares**: Si algo sale mal, a veces es una buena idea eliminar todos los archivos generados por LaTeX durante el proceso de compilación. Estos archivos tienen el mismo nombre que el documento principal pero con extensiones como `.aux`, `.toc`, `.lot`, `.lof`, `.bbl`, `.idx` o `.nav`, entre otras.

Si el problema persiste, podríamos intentar aislar la causa de la siguiente manera:

1. Cree una copia de su documento. Si es necesario, copie la carpeta completa. A partir de ahora, trabaje en la copia.
2. Elimine las partes del documento que probablemente no sean relevantes para el problema. Puede comentar líneas agregando un símbolo `%` al principio.
3. Realice la composición tipográfica para asegurarse de que el problema persista. Si es así, regrese al paso 2 y elimine otra parte del documento. Si el problema desaparece, lo ha aislado a la parte que acaba de eliminar. En este último caso, restaure la parte eliminada ya que contiene el problema. Si esa parte del documento sigue siendo demasiado grande para identificar el error, puede volver al paso 2 e intentar de nuevo eliminando partes más pequeñas.

Después de algunas repeticiones de este proceso, habrá localizado el problema. Si no lo encontró, reduzca la cantidad de paquetes cargados y repita los pasos 2 y 3.

Terminará con un documento de ejemplo pequeño pero completo que reproduce el error. A esto lo llamamos un ejemplo de trabajo mínimo (*minimal working example*, MWE).

Eliminar o reescribir esa parte identificada de su documento podría ayudar. ¿Qué pasa si realmente desea utilizar esa parte y le gustaría corregir ese error? Ahora que puede mostrar el problema con un ejemplo de código corto, puede publicar ese problema en un foro de LaTeX en línea y pedir ayuda.

No depende solo de los errores y advertencias que le muestra su editor. LaTeX realiza un seguimiento de toda la información, cada advertencia y cada error. Estos se recopilarán en un archivo con el nombre de su documento principal, con la extensión `.log`. Este es un archivo de texto ordinario que podemos abrir en cualquier editor, incluido su editor de LaTeX.

Por ejemplo, el archivo de registro para nuestro ejemplo "Hello world" al principio de este capítulo comienza con información sobre las versiones de formato de TeX y LaTeX y se ve así:

```text
This is pdfTeX, Version 3.141592653-2.6-1.40.22 (TeX Live 2021) (preloaded format=pdflatex 2021.6.25)  12 JUL 2021 00:47
entering extended mode
 restricted \write18 enabled.
 %&-line parsing enabled.
**document
(./document.tex
LaTeX2e <2021-06-01> patch level 1
L3 programming layer <2021-06-18>
```

Continúa con información sobre la clase de documento, su versión y el archivo `.clo` de opciones de clase utilizado:

```text
(/usr/local/texlive/2021/texmf-dist/tex/latex/base
/article.cls
Document Class: article 2021/02/12 v1.4n Standard LaTeX document class
(/usr/local/texlive/2021/texmf-dist/tex/latex/base
/size10.clo
File: size10.clo 2021/02/12 v1.4n Standard LaTeX file (size option)
)
```

Luego muestra los paquetes y definiciones cargados (no muchos, en nuestro caso):

```text
(/usr/local/texlive/2021/texmf-dist/tex/latex/l3backend
/l3backend-pdftex.def
File: l3backend-pdftex.def 2021-05-07 L3 backend support: PDF output (pdfTeX)
\l__color_backend_stack_int=\count190
\l__pdf_internal_box=\box50
)
```

Nos dice cuándo usa o abre un archivo:

```text
No file document.aux.
\openout1 = `document.aux'.
```

Nos proporciona información sobre fuentes:

```text
LaTeX Font Info:    Checking defaults for OML/cmm/m/it on input line 2.
LaTeX Font Info:    ... okay on input line 2.
```

Contiene todos los errores y advertencias:

```text
! Undefined control sequence.
l.3 \Latex
           \ says: Hello world!
? 
! Emergency stop.
```

Una vez que corregimos el error en el paso 4 de la sección *Comprensión y corrección de errores*, LaTeX agrega información sobre el rendimiento y la memoria de LaTeX al archivo de registro:

```text
Here is how much of TeX's memory you used:
 385 strings out of 478510
 6981 string characters out of 5849585
 301299 words of memory out of 5000000
 18443 multiletter control sequences out of 15000+600000
 403430 words of font info for 27 fonts, out of 8000000 for 9000
 1141 hyphenation exceptions out of 8191
 34i,5n,41p,139b,107s stack positions out of 5000i,500n,10000p,200000b,80000s
</usr/local/texlive/2021/texmf-dist/fonts/type1/public/
amsfonts/cm/cmr10.pfb></usr/local/texlive/2021
/texmf-dist/fonts/type1/public/amsfonts/cm/cmr7.pfb>
```

El archivo de registro finaliza indicando el tamaño de salida así como algunas estadísticas:

```text
Output written on document.pdf (1 page, 22454 bytes).
PDF statistics:
 18 PDF objects out of 1000 (max. 8388607)
 10 compressed objects within 1 object stream
 0 named destinations out of 1000 (max. 500000)
 1 words of extra memory for PDF output out of 10000 (max. 10000000)
```

Consulte los archivos de registro de algunos de los documentos que ha elaborado hasta ahora. La información contenida en ellos parece muy técnica, pero esto podría ayudarle mucho en la resolución de problemas.

---

### Resumen

Este capítulo nos preparó para resolver problemas que podrían ocurrir en nuestro documento de LaTeX.

Específicamente, aprendimos cómo localizar y corregir errores, comprender los mensajes de advertencia y analizar el archivo de registro de composición tipográfica de LaTeX.

Corregir errores es necesario. Recuerde consultar [https://texfaq.org/#errors](https://texfaq.org/#errors) para obtener ayuda. Lidiar con las advertencias es un valioso extra. Si encuentra algún problema que no puede resolver por su cuenta, no dude en pedir ayuda en un foro de Internet de LaTeX como [https://latex.org](https://latex.org/). En ese foro, tenemos una sección dedicada a este libro, *LaTeX Beginner’s Guide*, donde estaré encantado de responder a sus preguntas.

Para los amigos de LaTeX que están en línea, a menudo es una tarea fácil utilizar esta información para resolver su problema. Definitivamente, muchos entusiastas de LaTeX se divierten ayudando a otros usuarios de LaTeX. El siguiente capítulo analizará los foros de LaTeX en Internet y otros recursos en línea.
