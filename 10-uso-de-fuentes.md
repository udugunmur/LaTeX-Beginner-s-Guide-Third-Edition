# LaTeX Beginner's Guide
## Capítulo 10: Uso de Fuentes

Con la composición tipográfica matemática cubierta, ahora podemos ver las fuentes que definen el aspecto de un documento. Este capítulo presenta las opciones de fuentes de LaTeX y muestra cómo funcionan juntas las fuentes de texto y de matemáticas. La fuente base que elija moldea fuertemente la apariencia general. Puede seleccionar una fuente clara y fácil de leer para un documento extenso o una fuente decorativa y caligráfica para una tarjeta de felicitación. Su carta de solicitud de empleo podría beneficiarse de una fuente profesional muy limpia. Por el contrario, un artículo matemático requiere fuentes con una amplia gama de símbolos y una fuente de texto que los complemente.

Hasta ahora, nos hemos centrado en las propiedades lógicas de las fuentes. Aunque siempre hemos utilizado la fuente estándar de LaTeX, cambiamos de estilos romanos a sans-serif y de máquina de escribir (*typewriter*), y aprendimos cómo poner el texto en negrita, cursiva e inclinado en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*. Sin embargo, todavía no hemos ido más allá del conjunto de fuentes estándar.

En este capítulo, veremos los siguientes temas:

- Uso de paquetes integrales de fuentes
- Elección de familias de fuentes específicas
- Escritura con fuentes de sistema TrueType y OpenType

Si bien examinaremos la apariencia del texto, también veremos cómo se ven las fórmulas matemáticas junto con la fuente del texto.

Dado que este libro está impreso y distribuido electrónicamente con imágenes de mapa de bits, no verá la calidad original de LaTeX en las muestras de fuentes de este capítulo. Visite [https://latexguide.org/chapter-10](https://latexguide.org/chapter-10) para ver las fuentes en la calidad original de LaTeX y PDF. Puede ver los ejemplos de fuentes en un tamaño más grande para resaltar fácilmente los detalles finos y las diferencias.

Comencemos con un ejemplo. Servirá como base para nuestro trabajo con fuentes a lo largo de este capítulo.

---

### Uso de paquetes integrales de fuentes

Comenzamos con los paquetes de fuentes más completos. Para probar fuentes, resulta útil utilizar un pangrama. Esta palabra proviene del griego *pan gramma*, que significa cada letra. Representa una oración que utiliza todas las letras del alfabeto. Los pangramas son ideales para mostrar cómo maneja una fuente su conjunto completo de caracteres.

Imprimiremos una famosa frase pangrama utilizando la familia de fuentes Latin Modern. Latin Modern es muy similar a la fuente predeterminada de LaTeX, Computer Modern. Sin embargo, Latin Modern incluye muchos caracteres adicionales, especialmente los acentuados. Debido a esta cobertura más amplia y su alta calidad, a menudo se considera la sucesora natural de la fuente estándar. Veamos cómo se ve en varias familias y formas de fuentes, junto con una fórmula matemática:

1. Comience un nuevo documento:

```latex
\documentclass{article}
```

2. Cree una macro para el pangrama e incluya números adicionales. Tomará un argumento, que será el comando de selección de familia o forma de fuente. Agregaremos un salto de párrafo al final, como se muestra:

```latex
\newcommand{\pangram}[1]{{#1 The quick brown fox jumps over the lazy dog. 1234567890\par}}
```

3. Cargue el paquete `fontenc` y elija la codificación de fuentes T1:

```latex
\usepackage[T1]{fontenc}
```

4. Cargue el paquete `lmodern` para obtener la fuente Latin Modern:

```latex
\usepackage{lmodern}
```

5. Comience el documento y elija un tamaño de fuente grande para que los detalles sean fáciles de ver:

```latex
\begin{document}
\large
```

6. Ahora, usamos nuestra macro `\pangram` varias veces con diferentes configuraciones de fuente:

```latex
\pangram{\rmfamily}
\pangram{\sffamily}
\pangram{\ttfamily}
\pangram{\itshape}
\pangram{\slshape}
```

7. Agregue un ejemplo de fuente matemática; use el código que escribimos para la Figura 9.29 en el [Capítulo 9](https://subscription.packtpub.com/book/business-and-other/9781805804574/9), *Escritura de fórmulas matemáticas*:

```latex
\[ \int_a^b \! f(x) \, dx = \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{n} f(x_i) \,\Delta x_i \]
\end{document}
```

8. Compile y observe los ejemplos de fuentes:

> **Figura 10.1** – Ejemplos de fuentes Latin Modern

En nuestra definición de la macro `\pangram`, teníamos otro par de llaves. En nuestro argumento `{{ … }}`, las llaves exteriores contienen el argumento para `\newcommand`, y las llaves interiores limitan nuestros comandos para restringir el efecto del cambio de fuente.

Recuerde, la macro `\pangram` es solo una pequeña macro de demostración para nosotros, por lo que no tendremos que repetir la oración de demostración para cada familia de fuentes. En sus documentos cotidianos, cargue el paquete de fuentes y escriba su texto. Si es necesario, puede cambiar entre familias de fuentes como `\sffamily`, `\ttfamily` o `\rmfamily`, al igual que en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*.

En el paso 3, seleccionamos una codificación de fuentes. Técnicamente, las codificaciones son asignaciones de códigos de caracteres a símbolos en una fuente. Para el inglés y la mayoría de los idiomas de Europa occidental, se recomienda la codificación de fuentes T1. También se la conoce como codificación Cork porque se desarrolló en la ciudad de Cork, Irlanda, durante una conferencia del grupo de usuarios de TeX.

La codificación de fuentes predeterminada de LaTeX se llama OT1. En comparación con OT1, la codificación T1 utiliza tablas de codificación más grandes que manejan los caracteres acentuados mucho mejor.

Por ejemplo, con la codificación histórica predeterminada OT1, el carácter acentuado `ö` se construye a partir del glifo `o` y puntos separados, para imprimirse en el archivo PDF. Con T1, una `ö` es un solo glifo de la fuente actual, por lo que LaTeX también puede aplicar correctamente las reglas de separación silábica a las palabras que contienen caracteres acentuados. La función de búsqueda de un lector de PDF también funciona con esos caracteres, y copiar y pegar desde el archivo PDF los conserva. Con la codificación OT1 predeterminada, copiar y pegar el carácter `ö` daría como resultado puntos y un carácter `o`.

Si nota una caída en la calidad de la fuente predeterminada con la codificación T1, es posible que a su instalación le falten fuentes. En ese caso, instale el paquete `cm-super` usando el administrador de paquetes, o cambie a una de las fuentes con soporte T1 descritas en las siguientes secciones.

Lo que hemos discutido hasta ahora es la codificación de salida (*output encoding*). También puede encontrar el término codificación de entrada (*input encoding*). Los sistemas operativos y editores modernos admiten UTF-8 (Unicode), una codificación de texto estándar de la industria que amplía el envejecido código ASCII, que solo puede manejar 128 caracteres. LaTeX admite UTF-8 de forma nativa, por lo que no necesitaremos hacer nada. Por lo tanto, si encuentra el paquete `inputenc` en libros más antiguos o en código en Internet, puede omitirlo. Una buena práctica es utilizar UTF-8 con cualquier editor.

Ahora, echaremos un vistazo a algunas fuentes recomendadas con ejemplos. Todas ellas admiten la codificación T1, por lo que antes de cargar una fuente, use el siguiente comando:

```latex
\usepackage[T1]{fontenc}
```

En las siguientes secciones, exploraremos las diferentes fuentes.

#### Latin Modern: un reemplazo para la fuente estándar

Latin Modern fue diseñada para parecerse a la fuente predeterminada de LaTeX, pero la codificación se ha mejorado y también ha recibido refinamientos adicionales. Latin Modern contiene muchos caracteres diacríticos como glifos individuales, mientras que Computer Modern construye dichos caracteres acentuados a partir de letras simples y acentos.

Latin Modern tiene 72 fuentes de texto y 20 fuentes matemáticas bajo el capó, admitiendo todas las familias, formas y pesos de fuentes.

En la Figura 10.1 vimos cómo se ve.

#### Kp-Fonts: otro conjunto extenso de fuentes

La colección Kp-Fonts del proyecto Johannes Kepler proporciona fuentes serif, sans-serif y monoespaciadas, así como fuentes de símbolos matemáticos en varias formas y pesos. Incluso incluye negrita extendida y combinaciones como versalitas serif inclinadas.

Simplemente cargue el paquete para usar esas fuentes:

```latex
\usepackage{kpfonts}
```

El ejemplo anterior cambiará a lo siguiente:

> **Figura 10.2** – Ejemplos de fuentes Kepler

Kp-Fonts también proporciona versiones ligeras (*light*) con las mismas métricas de fuente. Las versiones ligeras pueden verse bien impresas, pero pueden parecer un poco delgadas para la lectura en pantalla.

Para cambiar a las versiones ligeras, cargue el paquete con la opción `light`:

```latex
\usepackage[light]{kpfonts}
```

El aspecto será diferente ahora:

> **Figura 10.3** – Fuente Kepler como versión light

Ahora, veamos paquetes de fuentes más especializados que proporcionan un solo estilo.

---

### Elección de familias de fuentes específicas

Ahora veremos varias fuentes de TeX que tienen su propio carácter y estilo. Como antes, usaremos nuestra macro `\pangram` de la sección anterior combinada con el comando de familia de fuentes correspondiente para realizar pruebas.

#### Fuentes con serifa (Serif)

Una pequeña línea o trazo adherido a los extremos de un trazo más grande en una letra o símbolo se llama serifa (*serif*). Una fuente que utiliza tales serifas se llama fuente con serifa o tipografía serif.

La fuente serif predeterminada se llama Computer Modern Roman. Latin Modern ofrece un aspecto muy similar y ya conoce la fuente serif de Kp-Fonts. Otros paquetes se especializan en fuentes serif y ahora veremos algunos de ellos.

##### Times Roman

El paquete `newtx` define una fuente de texto de estilo Times junto con una fuente matemática a juego. El paquete está dividido en dos partes para que los componentes de texto y matemáticas se puedan cargar de forma independiente, lo cual es útil cuando desea combinar Times con una fuente matemática diferente. Por eso lo cargamos de esta manera:

```latex
\usepackage{newtxtext}
\usepackage{newtxmath}
```

Con `\pangram{\rmfamily}` y nuestra fórmula matemática, obtenemos lo siguiente:

> **Figura 10.4** – Una fuente Times Roman

Como puede ver, Times es una fuente muy estrecha que funciona bien en texto de varias columnas, como en periódicos, pero no es adecuada para texto de una sola columna. Las líneas de texto anchas con demasiados caracteres no son ideales.

##### Palatino

El paquete `newpx` proporciona una fuente de texto de estilo Palatino y una fuente matemática coincidente. Este paquete también se divide en dos partes para uso independiente, por lo que las cargamos por separado:

```latex
\usepackage{newpxtext}
\usepackage{newpxmath}
```

Esto nos da lo siguiente:

> **Figura 10.5** – Una fuente Palatino

Podemos ver que Palatino es notablemente más ancha que Times, lo que le da una apariencia más abierta y relajada.

##### Charter

Charter es similar a la fuente predeterminada Computer Modern pero tiene una apariencia ligeramente más pesada. La cargamos así:

```latex
\usepackage{charter}
```

Para una compatibilidad matemática adecuada, cargue el paquete `mathdesign` con la opción `charter` en lugar de cargar `charter` directamente:

```latex
\usepackage[charter]{mathdesign}
```

Esto produce lo siguiente:

> **Figura 10.6** – Fuentes Charter y mathdesign

Además de Charter, el paquete `mathdesign` también puede cargar la fuente Utopia:

```latex
\usepackage[utopia]{mathdesign}
```

Y esto carga la fuente Garamond:

```latex
\usepackage[garamond]{mathdesign}
```

##### New Century Schoolbook

El paquete `newcent` proporciona la tipografía serif de fácil lectura New Century Schoolbook:

```latex
\usepackage{newcent}
```

Para emparejarla con una fuente matemática adecuada, puede cargar las fuentes matemáticas Fourier:

```latex
\usepackage{fouriernc}
```

Aquí están juntas:

> **Figura 10.7** – Fuentes New Century Schoolbook y Fourier

`nc` en el paquete `fouriernc` significa New Century porque está diseñado como complemento.

##### Concrete Roman

Es posible que la fuente Concrete Roman no se vea ideal en la pantalla, pero ofrece una excelente calidad de impresión. Simplemente cargue el paquete `concrete`:

```latex
\usepackage{concrete}
```

Un complemento matemático a juego está disponible a través del paquete `concmath`:

```latex
\usepackage{concmath}
```

Juntos, producen el siguiente resultado:

> **Figura 10.8** – Fuente Concrete Roman con soporte matemático

Con su signo integral vertical y su símbolo de suma sin serifas, Concrete Roman tiene una apariencia distintiva.

##### Bookman

Bookman es una fuente serif de estilo antiguo, proporcionada a través del paquete `bookman`, cargada mediante el siguiente comando:

```latex
\usepackage{bookman}
```

La fuente Kerkis es una extensión de Bookman con soporte matemático; puede cargarla en su lugar:

```latex
\usepackage{kmath}
\usepackage{kerkis}
```

Obtenemos lo siguiente:

> **Figura 10.9** – Kerkis, también conocida como Bookman, con soporte matemático

Una fuente inspirada en Bookman aún más mejorada está disponible con el nombre TeX Gyre Bonum. Sin embargo, esta, especialmente con soporte matemático, se utiliza mejor como fuente OpenType. En la última sección de este capítulo, trataremos esto.

Las fuentes con el mismo diseño o similar a menudo aparecen con diferentes nombres. A menudo, esto se debe a razones legales, ya que los nombres de las fuentes pueden estar protegidos incluso cuando el diseño en sí es de uso gratuito.

#### Fuentes sin serifa (Sans-Serif)

Las fuentes sans-serif son simplemente fuentes en las que no se utilizan serifas. Suelen verse más claras, lo que las convierte en una opción popular para presentaciones de diapositivas y otros contenidos basados en pantallas.

Debido a que las fuentes sans-serif no parecen tan pesadas en negrita, funcionan bien para los encabezados. Sin embargo, muchos creen que los pasajes de texto más largos son mucho más legibles con serifas tradicionales. Esa es la razón por la que las clases de KOMA-Script utilizan una fuente serif en el cuerpo del texto del documento y una fuente sans-serif para los encabezados de forma predeterminada.

Si es necesario, la fuente del cuerpo principal podría mostrarse en sans-serif mediante este comando:

```latex
\renewcommand{\familydefault}{\sfdefault}
```

Ya sabemos que Latin Modern y Kp-Fonts proporcionan variantes sans-serif. Echemos ahora otro vistazo a algunas fuentes sans-serif dedicadas.

##### Arev

Arev es una fuente sans-serif diseñada para presentaciones de diapositivas. El nombre es Vera escrito al revés, ya que extiende la fuente Vera Sans, basada a su vez en la fuente Frutiger. Arev también incluye soporte matemático a juego. Cárguela así:

```latex
\usepackage{arev}
```

El texto y las matemáticas se convierten en lo siguiente:

> **Figura 10.10** – Arev, una fuente similar a Frutiger

Tenga en cuenta que los signos de integral y sumatoria aún conservan serifas, como es muy común.

##### Computer Modern Bright

Computer Modern Bright (CM Bright) se deriva de Computer Modern Sans Serif para producir una variante más ligera. El paquete `cmbright` proporciona esta fuente junto con una fuente de máquina de escribir ligera y una fuente matemática sans-serif. Cárguela de la siguiente manera:

```latex
\usepackage{cmbright}
```

La salida de nuestro código de muestra será como esta:

> **Figura 10.11** – La fuente CM Bright

En comparación con otras fuentes sans-serif, es menos negrita y más discreta. Debido a su peso ligero, se combina mejor con fuentes de texto de ligereza similar en lugar de con fuentes serif más pesadas.

##### Kurier

Muchas fuentes sans-serif se ven similares a primera vista, pero sus diferencias las distinguen. Mire la fuente Kurier en la Figura 10.12, por ejemplo; puede notar diferencias, especialmente en la forma de la letra `g` y los símbolos matemáticos. Cárguela de la siguiente manera:

```latex
\usepackage{kurier}
```

Podemos habilitar el soporte matemático usando la opción `math`:

```latex
\usepackage[math]{kurier}
```

Compilar nuestro código de ejemplo nos da lo siguiente:

> **Figura 10.12** – La fuente Kurier

En esta familia de fuentes, incluso los símbolos de integral y sumatoria aparecen sin serifas.

##### Helvetica

La clásica fuente sans-serif Helvetica es simple, limpia y ampliamente reconocida. Probablemente conozca a su descendiente de Microsoft, Arial. Cargue la fuente de esta manera:

```latex
\usepackage{helvet}
```

Use la opción `scaled` si la fuente parece demasiado grande, especialmente cuando está al lado de una fuente serif. Por ejemplo, para reducirla un poco, puede escribir lo siguiente:

```latex
\usepackage[scaled=0.95]{helvet}
```

Helvetica no incluye soporte matemático directo, pero el paquete `sfmath` puede ayudar:

```latex
\usepackage{sfmath}
```

Cuando cargue el paquete `sfmath` en el preámbulo de su documento, LaTeX también utilizará la fuente de texto sans-serif actual dentro de las fórmulas matemáticas. Colóquelo después de otros paquetes de fuentes, para que tenga la oportunidad de detectar la fuente. Se pueden encontrar más explicaciones, ejemplos, opciones y un enfoque alternativo utilizando el paquete `sansmath` en el [Capítulo 3](https://subscription.packtpub.com/book/business-and-other/9781805804574/3), *Ajuste de fuentes*, de *LaTeX Cookbook*, con el código fuente en [https://latex-cookbook.net/chapter-03](https://latex-cookbook.net/chapter-03).

Cargar `helvet` y `sfmath` como en esta sección produce la siguiente salida:

> **Figura 10.13** – Ejemplo de Helvetica

Puede encontrar más información en la página de inicio del autor de `sfmath` en [https://dtrx.de/od/tex/sfmath.html](https://dtrx.de/od/tex/sfmath.html).

#### Fuentes de máquina de escribir (Typewriter)

Las fuentes de máquina de escribir, también conocidas como fuentes monoespaciadas, se utilizan comúnmente para el código fuente, como en este libro. Veamos tres variantes excelentes.

##### Courier

Courier es una fuente de máquina de escribir de trazado muy ancho. Cárguela con esto:

```latex
\usepackage{courier}
```

Luego, con `\ttfamily` o `\texttt`, obtendremos lo siguiente:

> **Figura 10.14** – La fuente Courier

Si parece demasiado grande en comparación con la fuente principal del documento, puede cargar el paquete `couriers` en su lugar (tenga en cuenta la `s` para *scaled*) con una opción `scaled`, como aquí:

```latex
\usepackage[scaled=0.95]{couriers}
```

Esto reduce la fuente Courier al 95% de su tamaño original."

##### Inconsolata

Inconsolata es una fuente monoespaciada bien diseñada, hecha específicamente para listados de código fuente. Es más compacta y más fácil de leer que Courier. Cárguela de la siguiente manera:

```latex
\usepackage{inconsolata}
```

El resultado demuestra que las fuentes monoespaciadas pueden ser elegantes:

> **Figura 10.15** – La fuente Inconsolata

A diferencia de Courier, es sans-serif. También admite una opción de escalado si necesita ajustar su tamaño.

##### Bera Mono

Bera Mono es otra fuente de máquina de escribir sans-serif. Cárguela así:

```latex
\usepackage{beramono}
```

Así es como se ve:

> **Figura 10.16** – La fuente Bera Mono

Aquí también puede especificar una opción `scaled`.

#### Fuentes caligráficas

Las fuentes caligráficas son tipografías manuscritas (*script*) con trazos fluidos similares a la escritura a mano. Funcionan muy bien para invitaciones, encabezados decorativos o cualquier texto que necesite un toque elegante. Elijamos dos hermosas fuentes manuscritas para examinarlas más de cerca.

##### Calligra

Cargamos la fuente de la forma habitual:

```latex
\usepackage{calligra}
```

Para cambiar a la fuente, podemos usar el comando `\calligra` en el texto. Como sabemos, los comandos de cambio locales son válidos hasta que finaliza el entorno o grupo circundante, `{ … }`. También funciona con nuestra macro `\pangram`, así:

```latex
\pangram{\calligra}
```

Esto imprime lo siguiente:

> **Figura 10.17** – La fuente manuscrita Calligra

Las letras mayúsculas se ven particularmente vivas y divertidas.

##### Miama Nueva

Las partes de las letras que se extienden por encima de la altura normal de la letra se llaman ascendentes (*ascenders*), mientras que las que caen por debajo de la línea base se llaman descendentes (*descenders*). Miama Nueva es una elegante fuente manuscrita con ascendentes y descendentes especialmente gráciles. Cárguela como de costumbre:

```latex
\usepackage{miama}
```

Luego, el comando `\fmmfamily` cambia a esa fuente. Nuevamente, úselo dentro de un grupo, `{ … }`, o un entorno si desea limitar la elección de fuente a solo un fragmento de texto. Podemos utilizar nuestra macro `\pangram` nuevamente:

```latex
\pangram{\fmmfamily}
```

La escritura es un placer de leer:

> **Figura 10.18** – La fuente manuscrita Miama Nueva

Miama Nueva es muy encantadora, por ejemplo, en tarjetas de invitación de bodas.

Probablemente el mejor lugar para explorar las fuentes de LaTeX sea *The LaTeX Font Catalogue*. Puede visitarlo en línea en [https://www.tug.org/FontCatalogue](https://www.tug.org/FontCatalogue). El sitio tiene como objetivo presentar todas las fuentes disponibles gratuitamente para LaTeX. Está basado en TeX Live. Muestra muestras visuales, el código requerido y más información útil. Elija una categoría, explore las vistas previas y haga clic en una fuente para ver algunos ejemplos, notas de uso y el código requerido.

También puede utilizar fuentes que LaTeX no admite directamente, y eso es lo que veremos a continuación.

---

### Escritura con fuentes de sistema TrueType y OpenType

LaTeX también puede utilizar muchos miles de fuentes que ni siquiera fueron preparadas para LaTeX. Eso incluye fuentes del sistema operativo, fuentes TrueType y fuentes modernas OpenType.

Probemos esto con fuentes disponibles en una computadora con Microsoft Windows. Para los usuarios de macOS, veremos un ejemplo después.

#### Selección de la fuente principal

Podemos abrir **Configuración | Fuentes** a través del menú Inicio de Windows o buscar en la carpeta `C:\Windows\Fonts` para ver las fuentes instaladas. La fuente Segoe UI aparece disponible con varios nombres, así que elijamos Segoe UI Semilight. Veamos qué fácil es de usar:

1. Comience un nuevo documento:

```latex
\documentclass{article}
```

2. Cargue el paquete `fontspec`, que proporciona los comandos de selección de fuentes:

```latex
\usepackage{fontspec}
```

3. Establezca la fuente principal:

```latex
\setmainfont{Segoe UI Semilight}
```

4. Escriba el cuerpo del documento con un texto grande:

```latex
\begin{document}
\large
The quick brown fox jumps over the lazy dog. 1234567890
\end{document}
```

5. Esta vez, elija **LuaLaTeX** o **XeLaTeX** como motor de compilación. En TeXworks, esta es una lista desplegable justo al lado del botón **Typeset**, como se muestra aquí:

> **Figura 10.19** – Selección de LuaLaTeX

6. Compile y vea lo que obtenemos:

> **Figura 10.20** – Segoe UI Semilight de Microsoft Windows 10

Esa selección de fuente fue sencilla: cargar un paquete y usar un comando. Ahora hagámoslo con múltiples fuentes en un documento.

#### Selección de múltiples familias de fuentes

Windows ya viene con varias fuentes. Podemos elegir algunas en **Configuración | Fuentes** en el menú Inicio de Windows, o mirando en la carpeta `C:\Windows\Fonts`. Esta vez, elegiremos lo siguiente:

- Cambria como la fuente serif principal
- Segoe UI como la fuente sans-serif
- Lucida Console como la fuente de máquina de escribir
- Cambria Math como la fuente matemática

Todas estas son fuentes estándar de Windows.

Armemos un documento que muestre las cuatro fuentes:

1. Comience un nuevo documento e ingrese nuestra macro `\pangram` nuevamente para realizar pruebas fáciles:

```latex
\documentclass{article}
\newcommand{\pangram}[1]{{#1 The quick brown fox jumps over the lazy dog. 1234567890\par}}
```

2. Cargue el paquete `fontspec` y el paquete `unicode-math`. Este último nos permite seleccionar la fuente matemática:

```latex
\usepackage{fontspec}
\usepackage{unicode-math}
```

3. Establezca las fuentes según lo planeado utilizando un argumento opcional que escala automáticamente las fuentes, de modo que la altura de sus letras minúsculas coincida con la altura de las letras minúsculas de la fuente principal, de la siguiente manera:

```latex
\setmainfont{Cambria}
\setsansfont{Segoe UI}[Scale=MatchLowercase]
\setmonofont{Lucida Console}[Scale=MatchLowercase]
\setmathfont{Cambria Math}[Scale=MatchLowercase]
```

4. Luego, vuelva a escribir el cuerpo de un documento de prueba para ver las fuentes disponibles:

```latex
\begin{document}
\large
\pangram{\rmfamily}
\pangram{\sffamily}
\pangram{\ttfamily}
\[ \int_a^b \! f(x) \, dx = \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{n} f(x_i) \,\Delta x_i \]
\end{document}
```

5. Compile con LuaLaTeX o XeLaTeX y eche un vistazo:

> **Figura 10.21** – Varias fuentes de Microsoft Windows

Cambria se convirtió en la fuente de texto principal, y siempre que cambiamos a sans-serif, obtenemos Segoe UI, y cuando escribimos listados de código en fuente de máquina de escribir, aparece Lucida Console. Además, las fórmulas matemáticas ahora se imprimen en Cambria Math en lugar de en la fuente Computer Modern predeterminada. Esta fácil selección de fuentes es en realidad toda una evolución en LaTeX, y vale la pena considerar LuaLaTeX o XeLaTeX solo por el soporte extendido de fuentes. Ambos admiten fuentes OpenType y TrueType, pero ninguno funciona todavía con pdfLaTeX.

XeLaTeX se desarrolló pensando en el acceso directo a las fuentes del sistema, algo que pdfLaTeX no ofrece. LuaLaTeX se introdujo como una extensión de LaTeX que agregó el lenguaje de secuencias de comandos Lua y desde entonces ha obtenido un mejor soporte para fuentes. Sin ocuparnos de sus funciones avanzadas, simplemente podemos elegir una de ellas para fuentes cuando no tenemos un paquete para pdfLaTeX.

Hoy en día, XeLaTeX tiene menos mantenimiento y se recomienda utilizar LuaLaTeX.

#### Selección de una fuente localmente

Como prometimos anteriormente, también trabajaremos con macOS. Esta vez, elijamos la fuente Zapfino, que está preinstalada en macOS. Es una hermosa fuente caligráfica que aplicaremos solo a un fragmento de texto específico, en lugar de cambiar la fuente para todo el documento. Siga estos pasos:

1. Comience con un documento pequeño, al igual que en las secciones anteriores. Como antes, asegúrese de cargar el paquete `fontspec`:

```latex
\usepackage{fontspec}
```

2. Defina una nueva familia de fuentes, con el nombre que elija, y establézcala en Zapfino:

```latex
\newfontfamily{\calligraphicfont}{Zapfino}
```

3. Defina una macro de formato personalizada, como hicimos en el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*:

```latex
\newcommand{\calligraphic}[1]{{\calligraphicfont #1}}
```

4. Ahora, puede utilizar este comando en cualquier lugar del texto de su documento para darle formato caligráfico:

```latex
\calligraphic{A graceful Zapfino typography example}
```

5. Verifique la salida de esta macro:

> **Figura 10.22** – Selección de una fuente caligráfica

Aquí, los ascendentes y descendentes se exageran intencionalmente para verse más elegantes. Este cambio afecta solo al texto seleccionado.

---

### Resumen

Ahora sabe cómo elegir y combinar diferentes fuentes de texto y matemáticas, por lo que sus documentos ya no tienen que depender del aspecto predeterminado de LaTeX.

Exploramos conjuntos de fuentes completos, fuentes individuales y varios buenos paquetes de fuentes. Para conocer algunas técnicas avanzadas de fuentes con ejemplos listos para usar, puede consultar el [Capítulo 3](https://subscription.packtpub.com/book/business-and-other/9781805804574/3), *Ajuste de fuentes*, en *LaTeX Cookbook*, y visitar el sitio web del libro con código compilable en línea en [https://latex-cookbook.net/chapter-03](https://latex-cookbook.net/chapter-03).

Ahora, pasemos de las fuentes a LaTeX en general, y aprenderemos cómo desarrollar y gestionar documentos más grandes en el próximo capítulo.
