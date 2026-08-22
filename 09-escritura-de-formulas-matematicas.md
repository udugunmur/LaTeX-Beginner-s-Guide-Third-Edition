# LaTeX Beginner's Guide
## Capítulo 9: Escritura de Fórmulas Matemáticas

Al principio de este libro, en el [Capítulo 1](https://subscription.packtpub.com/book/business-and-other/9781805804574/1), *Primeros pasos con LaTeX*, prometimos que LaTeX ofrece una calidad excelente para la composición tipográfica matemática. Ahora, es el momento de demostrarlo. Al final de este capítulo, podrá escribir textos matemáticos claros y elegantes.

Para aprovechar al máximo las capacidades matemáticas de LaTeX, trabajaremos en los siguientes temas:

- Escritura de fórmulas básicas
- Composición tipográfica de fórmulas multilínea
- Exploración de la gran variedad de símbolos matemáticos
- Construcción de estructuras matemáticas

Es una tarea importante, así que comencemos.

---

### Escritura de fórmulas básicas

LaTeX proporciona tres modos de escritura:

- **Modo párrafo (*Paragraph mode*)**: El texto se compone como una secuencia de palabras dispuestas en líneas, párrafos y páginas. Eso es lo que hemos utilizado a lo largo de los capítulos anteriores.
- **Modo de izquierda a derecha (*Left-to-right mode*)**: El texto se establece como una secuencia continua de palabras sin saltos de línea. Por ejemplo, el argumento del comando `\mbox` se compone en este modo, por lo que podemos usarlo para evitar que una frase se divida con guiones.
- **Modo matemático (*Math mode*)**: Aquí, LaTeX trata las letras como símbolos matemáticos. Aparecerán en cursiva, como es práctica común para las variables. Muchos símbolos solo están disponibles en modo matemático, como raíces, signos de sumatoria, símbolos de relación, acentos matemáticos, flechas y varios delimitadores, como paréntesis, corchetes y llaves. LaTeX ignora los caracteres de espacio normales entre letras y símbolos en el modo matemático. En cambio, el espaciado está determinado por el tipo de símbolo, por lo que el espaciado alrededor de los signos de relación es diferente del espaciado alrededor de los delimitadores de apertura o cierre. Cualquier expresión matemática debe escribirse en este modo.

Ahora entraremos en el modo matemático por primera vez.

Nuestro primer texto matemático tratará sobre las soluciones de ecuaciones cuadráticas. Compondremos fórmulas con constantes y variables, usaremos superíndices para los cuadrados y subíndices para las soluciones, e incluiremos un símbolo de raíz. Finalmente, agregaremos referencias cruzadas a fórmulas. Hay bastante que cubrir, así que dividámoslo en los siguientes pasos:

1. Comience un nuevo documento. Por ahora, no necesitamos ningún paquete:

```latex
\documentclass{article}
\begin{document}
\section*{Quadratic equations}
```

2. Enuncie la ecuación cuadrática con sus condiciones. Use un entorno `equation` para la fórmula. Rodee pequeños fragmentos de matemáticas dentro del texto usando `\(` y `\)`:

```latex
The quadratic equation
\begin{equation}
  \label{quad}
  ax^2 + bx + c = 0,
\end{equation}
where \( a, b \) and \( c \) are constants and \( a \neq 0 \), has two solutions for the variable \( x \):
```

3. Escriba otra ecuación para las soluciones. El comando para una raíz cuadrada es `\sqrt`, y para una fracción, use el comando `\frac`:

```latex
\begin{equation}
  \label{root}
  x_{1,2} = \frac{-b \pm \sqrt{b^2-4ac}}{2a}.
\end{equation}
```

4. Introduzcamos el discriminante y discutamos el caso cuando es cero. Para obtener una ecuación mostrada no numerada, rodeamos la fórmula con `\[` y `\]`:

```latex
If the \emph{discriminant} \( \Delta \) with
\[
  \Delta = b^2 - 4ac
\]
is zero, then the equation (\ref{quad}) has a double solution: (\ref{root}) becomes
\[
  x = - \frac{b}{2a}.
\]
\end{document}
```

5. Compile el documento. Las referencias de las ecuaciones no están resueltas en la primera ejecución y aparecerán como (?). Compile nuevamente para permitir que LaTeX las resuelva, luego observe la salida final:

> **Figura 9.1** – Un ejemplo de texto matemático

Como se mencionó en el [Capítulo 1](https://subscription.packtpub.com/book/business-and-other/9781805804574/1), *Primeros pasos con LaTeX*, escribir fórmulas a menudo se siente similar a programar. Construimos expresiones a partir de comandos; algunos toman argumentos, como los de raíces y fracciones, mientras que otros son comandos de símbolos simples, como los de letras griegas. La mayoría de estos símbolos solo funcionan en entornos matemáticos, no en texto normal. Este capítulo le ayudará a dominarlo y los resultados valdrán la pena.

El entorno `equation` creó una fórmula mostrada en bloque (*displayed formula*). LaTeX la centró horizontalmente y agregó algo de espacio vertical arriba y abajo. Además, numeró estas fórmulas de forma consecutiva.

Sin embargo, `\[ … \]` y `\( … \)` son también, en realidad, entornos. Veámoslos más de cerca en las siguientes secciones.

#### Incrustación de expresiones matemáticas dentro del texto

LaTeX proporciona el entorno `math` para fórmulas dentro del texto (*inline*):

```latex
\begin{math} expression \end{math}
```

Dado que puede resultar tedioso escribir este entorno para cada pequeña expresión o símbolo, LaTeX ofrece una forma más corta que se comporta igual:

```latex
\( expression \)
```

También puede colocarlo todo en una sola línea, como `\( expression \)`.

Una tercera forma es utilizar un atajo de TeX: `$expression$`. Una desventaja de este último es que los símbolos de apertura y cierre son los mismos, lo que puede provocar fácilmente errores. Aún así, es mucho más rápido de escribir, por lo que sigue siendo popular entre los usuarios de LaTeX y su uso es perfectamente válido.

Las fórmulas en línea ahorran espacio y ayudan a mantener la fluidez de las explicaciones, por lo que se recomiendan para expresiones matemáticas breves dentro del texto.

#### Fórmulas mostradas en bloque

Para fórmulas centradas y mostradas en bloque (*displayed*), LaTeX proporciona el entorno `displaymath`:

```latex
\begin{displaymath} expression \end{displaymath}
```

Con este entorno, cuando finaliza el párrafo, sigue un espacio vertical, luego LaTeX muestra la fórmula centrada y agrega espacio vertical después. Debido a que este entorno ya gestiona el espaciado, evite dejar líneas vacías antes o después de él, ya que esto crearía espacio vertical adicional a partir de los saltos de párrafo adicionales.

También existe una forma abreviada para este entorno. Aquí es con corchetes, en lugar de paréntesis:

```latex
\[ expression \]
```

Colocar los atajos `\[` y `\]` en sus propias líneas hace que el código sea más fácil de leer.

En tutoriales antiguos y en Internet, es posible que encuentre la forma de TeX `$$...$$` para fórmulas mostradas. No use esto con LaTeX, ya que conduce a un espaciado vertical incorrecto.

Dichas fórmulas mostradas se destacan más porque están centradas y rodeadas de espacio adicional. Elija el estilo que mejor respalde la legibilidad de su texto.

Durante el resto de este capítulo, todos los fragmentos de código utilizarán el modo matemático. Entraremos explícitamente a un entorno matemático o asumiremos que ya estamos en modo matemático para fragmentos de código cortos.

#### Numeración de ecuaciones

Las ecuaciones y las fórmulas, en general, se pueden numerar. Sin embargo, esto solo se aplica a las fórmulas mostradas en bloque. El entorno `equation` maneja esto:

```latex
\begin{equation} \label{key} expression \end{equation}
```

Se parece a `displaymath`, pero esta vez está numerado. El número se mostrará entre paréntesis en el lado derecho de la ecuación, como se muestra en la Figura 9.1. Puede usar `key` para hacer referencia cruzada a la ecuación con el comando `\ref`, como hicimos en el capítulo anterior. Si no necesita una referencia, puede omitir el comando `\label`. En general, tiene sentido numerar únicamente las ecuaciones a las que planea hacer referencia.

Si carga el paquete `amsmath`, que usaremos más adelante, puede escribir ecuaciones sin numerar con el entorno con asterisco `equation*`.

#### Adición de subíndices y superíndices

Dado que los exponentes y los índices se utilizan con tanta frecuencia, LaTeX proporciona comandos concisos para ellos. Un guión bajo, `_`, crea un subíndice, que a menudo se usa como índice:

```latex
{expression}_{subscript}
```

Un signo de intercalación (*caret*), `^`, produce un superíndice utilizado para exponentes:

```latex
{expression}^{superscript}
```

Como vemos aquí, usamos llaves para definir la parte relevante de la expresión. En el caso de letras, números o símbolos individuales, puede omitir las llaves.

Los subíndices y superíndices se pueden anidar. Si utiliza tanto subíndices como superíndices en la misma expresión, el orden de `^` y `_` no importa. Veamos un ejemplo:

```latex
\[ x_1^2 + x_2^2 = 1, \quad 2^{2^x} = 64 \]
```

Esto nos da la siguiente salida:

> **Figura 9.2** – Subíndices y superíndices

Tenga en cuenta que el exponente de nivel superior es más pequeño que el inferior. Cuando anidamos subíndices o superíndices, el tamaño de la fuente interna se vuelve más pequeño.

El nombre del comando `\quad` proviene de la tipografía tradicional en metal, donde se insertaba una pieza cuadrada para agregar espacio horizontal. `\quad` crea un pequeño espacio de aproximadamente el ancho de la letra M. El comando `\qquad` produce el doble de esa cantidad. Ambos comandos son útiles para ajustes rápidos de espaciado.

#### Uso de operadores

Las funciones trigonométricas, logarítmicas y otras funciones analíticas y algebraicas se escriben comúnmente con letras romanas verticales, en contraste con las variables, que se escriben en cursiva. Simplemente escribir `log` se vería como un producto de las tres variables: `l`, `o` y `g`. LaTeX proporciona comandos para muchas funciones comunes, a menudo llamadas operadores. Aquí hay una lista alfabética de los predefinidos: `\arccos`, `\arcsin`, `\arctan`, `\arg`, `\cos`, `\cosh`, `\cot`, `\coth`, `\csc`, `\deg`, `\det`, `\dim`, `\exp`, `\gcd`, `\hom`, `\inf`, `\ker`, `\lg`, `\lim`, `\liminf`, `\limsup`, `\ln`, `\log`, `\max`, `\min`, `\Pr`, `\sec`, `\sin`, `\sinh`, `\sup`, `\tan` y `\tanh`.

Puede escribir la función módulo de dos formas: utilice `\bmod` para una relación binaria o utilice `\pmod{argument}` para una expresión de módulo entre paréntesis.

Algunos operadores toman subíndices, que aparecen debajo del operador en las fórmulas mostradas en bloque:

```latex
\[ \lim_{n=1, 2, \ldots} a_n \qquad \max_{x<X} x \]
```

La salida es la siguiente:

> **Figura 9.3** – Operadores con subíndices

Los superíndices se colocarían encima del operador.

Cuando los operadores se utilizan en línea dentro del texto, es ligeramente diferente:

```latex
Within text, we have \( \lim_{n=1, 2, \ldots} a_n \) and \( \max_{x<X} x \).
```

La salida ahora es la siguiente:

> **Figura 9.4** – Subíndices

Esto es para evitar un espaciado excesivo entre líneas.

Además, las Figuras 9.30 y 9.31 muestran la posición y el tamaño de los subíndices y superíndices para los operadores.

En el [Capítulo 10](https://subscription.packtpub.com/book/business-and-other/9781805804574/10), *Escritura de matemáticas avanzadas*, en *LaTeX Cookbook*, puede leer cómo definir sus propios operadores y cómo afinar los subíndices y superíndices para una alineación perfecta.

#### Composición tipográfica de raíces

Nuestro primer ejemplo en este capítulo contenía una raíz cuadrada escrita como `\sqrt{value}`. Debido a que este comando también admite raíces de orden superior, acepta un argumento opcional que especifica el orden. La definición completa es la siguiente:

```latex
\sqrt[order]{value}
```

Las raíces se pueden anidar. Podemos verlo en este ejemplo:

```latex
\sqrt[64]{x} = \sqrt{\sqrt{\sqrt{\sqrt{\sqrt{\sqrt{x}}}}}}
```

Esto produce lo siguiente:

> **Figura 9.5** – Raíces anidadas

LaTeX ajusta automáticamente el tamaño del símbolo de raíz a la altura y el ancho de la expresión `value`. Por eso las raíces exteriores parecen más grandes que las interiores.

#### Escritura de fracciones

Para fórmulas en línea, puede simplemente usar una barra diagonal, `/`, para escribir fracciones, como `\( (a+b)/2 \)`. Para fracciones más grandes, use el comando `\frac`:

```latex
\frac{numerator}{denominator}
```

He aquí un ejemplo:

```latex
\[ \frac{n(n+1)}{2} \quad \frac{\frac{\sqrt{x}+1}{2}-x}{y^2} \]
```

La salida es la siguiente:

> **Figura 9.6** – Fracciones y fracciones anidadas

LaTeX ajusta automáticamente la línea de separación para que coincida con el ancho del numerador y del denominador.

#### Escritura de letras griegas

Los matemáticos suelen utilizar letras griegas, por ejemplo, para denotar constantes. Para obtener una letra griega minúscula, escriba el nombre como un comando con una barra invertida. Aquí están las letras griegas minúsculas con sus correspondientes comandos de LaTeX:

> **Figura 9.7** – Letras griegas minúsculas

Para algunas letras, hay variantes disponibles:

> **Figura 9.8** – Variantes alternativas para algunas letras griegas

Como el ómicron se parece a la letra o, no existe ningún comando para él. Lo mismo se aplica a la mayoría de las letras griegas mayúsculas, que parecen idénticas a sus contrapartes romanas. Por ejemplo, no existen comandos `\Alpha` o `\Beta`; simplemente escriba A o B en su lugar. Las letras griegas mayúsculas que difieren de las letras romanas se pueden escribir de la siguiente manera:

> **Figura 9.9** – Letras griegas mayúsculas

Puede ver que las letras griegas minúsculas se componen en cursiva y las letras griegas mayúsculas se escriben verticales (*upright*). Esta convención refleja la composición matemática tradicional. La frugalidad de usar solo letras minúsculas en cursiva y un número limitado de letras griegas verticales se debe a las limitaciones de espacio en las tablas de caracteres en los primeros días de TeX.

Si desea tener letras griegas verticales, puede agregar `\usepackage{upgreek}` y luego usar los siguientes comandos:

> **Figura 9.10** – Letras griegas minúsculas verticales

Las siguientes variantes adicionales también están disponibles:

> **Figura 9.11** – Variantes verticales alternativas para algunas letras griegas

Las letras griegas verticales se toman de la fuente Euler y no de las fuentes Computer Modern predeterminadas.

#### Escritura de letras caligráficas (*script*)

Para las 26 letras mayúsculas A, B, C, …, Z, existe una forma caligráfica, producida por `\mathcal`:

```latex
\[ \mathcal{A}, \mathcal{B}, \mathcal{C}, \ldots, \mathcal{Z} \]
```

Así es como se ven:

> **Figura 9.12** – Letras caligráficas

Varios paquetes ofrecen fuentes caligráficas alternativas, como `zapfino` y `xits`.

#### Producción de puntos suspensivos (*ellipsis*)

Ya sabe que el comando `\ldots` produce puntos suspensivos bajos. También funciona en modo matemático. Usamos los puntos suspensivos bajos principalmente entre letras y comas. Entre símbolos de operación y de relación, son más comunes los puntos suspensivos centrados. Además, una matriz puede requerir puntos suspensivos diagonales o verticales. He aquí cómo podemos producirlos:

> **Figura 9.13** – Puntos suspensivos en varias posiciones

Para puntos suspensivos diagonales en la dirección opuesta, puede escribir `\reflectbox{$\ddots$}`. El comando `\reflectbox` requiere `\usepackage{graphicx}` en su preámbulo.

#### Cambio de fuente, estilo y tamaño

En el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*, vimos formas de modificar la fuente del texto. En modo matemático, podemos usar comandos adicionales para cambiar el estilo de fuente, como sigue:

> **Figura 9.14** – Comandos de fuentes matemáticas

Por ejemplo, una vez que agregue `\usepackage{dsfont}` al preámbulo de su documento, puede escribir `\mathds{Z}` para obtener una letra Z de trazo doble (*double-stroke*).

Aunque las letras en modo matemático están en cursiva de forma predeterminada, LaTeX las trata como símbolos separados, lo que da como resultado un espaciado diferente al de una palabra en cursiva. Por ejemplo, en modo matemático, `fi` puede representar el producto de las variables `f` e `i`, pero no la ligadura `fi`. Compare estas dos versiones:

```latex
\(Definition\) and \textit{Definition}
```

Esto nos da lo siguiente:

> **Figura 9.15** – Escritura matemática simple versus texto en cursiva

La versión de la derecha es claramente mejor.

Además, `\textit` compone sus argumentos utilizando la fuente matemática en cursiva, no la fuente de texto estándar. Para texto dentro de fórmulas, lea la sección *Inserción de texto en fórmulas* más adelante en este capítulo.

Para poner una expresión matemática completa en negrita, use la declaración `\boldmath` antes de la expresión, es decir, fuera del modo matemático. La declaración `\unboldmath` vuelve a cambiar al tipo de letra estándar. Esta última también se utiliza fuera del modo matemático.

Para poner solo una parte de una fórmula en negrita, puede cambiar al modo de izquierda a derecha con el comando `\mbox` y usar `\boldmath` en su argumento.

Hay cuatro estilos matemáticos diferentes disponibles que determinan la composición tipográfica y el tamaño de fuente. Puede utilizar estos comandos dentro del modo matemático:

- `\textstyle`: impone el estilo en línea para los tamaños de símbolos y la posición de subíndices y superíndices, incluso cuando se utiliza en una fórmula mostrada en bloque
- `\displaystyle`: trata los tamaños de símbolos, subíndices y superíndices como en una fórmula mostrada en bloque, incluso cuando se utiliza en línea en el texto
- `\scriptstyle`: cambia a un tamaño de fuente más pequeño, como para subíndices y superíndices
- `\scriptscriptstyle`: utiliza un tamaño de fuente mucho más pequeño para el estilo de subíndices anidados (*nested script style*)

`\textstyle` se diferencia de `\displaystyle` principalmente en dos aspectos: con `\textstyle`, los símbolos de tamaño variable son más pequeños, y los subíndices y superíndices generalmente se colocan al lado de la expresión en lugar de debajo y arriba, respectivamente. De lo contrario, el tamaño de fuente es el mismo.

LaTeX cambia de estilo automáticamente. Si escribe un exponente simple, se compondrá en estilo *script* con un tamaño de fuente más pequeño.

Puede forzar el estilo deseado utilizando uno de los cuatro comandos enumerados aquí. Así, por ejemplo, puede insertar `\displaystyle` en una fórmula, de modo que incluso dentro del texto aparezca como en una fórmula mostrada en bloque: fracción más grande y signos de sumatoria más grandes. Además, los subíndices se colocan abajo y los superíndices arriba. Tenga en cuenta que esto aumenta el interlineado.

#### Personalización de fórmulas mostradas en bloque

Dos opciones de clase de documento pueden cambiar cómo aparecen las fórmulas mostradas:

- `fleqn` para ecuaciones alineadas a la izquierda (*flush left equations*): LaTeX alineará todas las fórmulas mostradas en el margen izquierdo
- `leqno` para números de ecuación a la izquierda (*left equation numbers*): todas las fórmulas numeradas obtendrán los números en el lado izquierdo en lugar del derecho

Las ecuaciones y fórmulas suelen formar parte de una estructura más amplia en lugar de estar aisladas. Podemos encontrarnos con situaciones como las siguientes:

- Una fórmula es demasiado larga para caber en una línea
- Varias fórmulas deben enumerarse una tras otra
- Una ecuación debe transformarse paso a paso
- Una cadena de desigualdades abarca varias líneas
- Varias fórmulas deben alinearse en sus símbolos de relación

También podemos encontrarnos con situaciones en las que necesitemos escribir ecuaciones de varias líneas, a menudo con algún tipo de alineación. El paquete `amsmath` proporciona entornos especializados para casi todas estas situaciones, que será el tema de nuestra siguiente sección.

---

### Composición tipográfica de fórmulas multilínea

Usaremos el paquete `amsmath` para componer una fórmula muy larga y un sistema de ecuaciones:

1. Comience un nuevo documento. Aquí, usamos el tamaño de papel A6 para trabajar con un ancho de texto más pequeño:

```latex
\documentclass{article}
\usepackage[a6paper]{geometry}
```

2. Cargue el paquete `amsmath` y comience el documento:

```latex
\usepackage{amsmath}
\begin{document}
```

3. Use el entorno `multline` para distribuir una ecuación larga en tres líneas. Termine cada línea con una barra invertida doble, `\\`, excepto la última:

```latex
\begin{multline}
\sum = a + b + c + d + e \\
     + f + g + h + i + j \\
     + k + l + m + n
\end{multline}
\end{document}
```

4. Compile y observe la ecuación:

> **Figura 9.16** – Una fórmula que abarca tres líneas

5. Ahora, manejamos un sistema de ecuaciones. Use el entorno `gather` para agregar estas ecuaciones. Nuevamente, termine todas las líneas con `\\`, excepto la última:

```latex
\begin{gather}
  x + y + z = 0 \\
  y - z = 1
\end{gather}
```

6. Compile nuevamente y observe las ecuaciones, que aparecen centradas horizontalmente entre sí:

> **Figura 9.17** – Un sistema con dos ecuaciones

7. Los sistemas de ecuaciones suelen estar alineados en el signo igual. Hagamos esto. Use el símbolo de unión (*ampersand*), `&`, para marcar el punto donde deseamos alinear:

```latex
\begin{align}
  x + y + z &= 0 \\
  y - z     &= 1
\end{align}
```

8. Compile nuevamente; ahora las ecuaciones están alineadas como se deseaba:

> **Figura 9.18** – Un sistema con dos ecuaciones alineadas

Debido a que cargamos el paquete `amsmath`, ahora tenemos acceso a varios entornos matemáticos de varias líneas. Cada línea en dicho entorno termina con `\\`, excepto la última. De lo contrario, si agregamos `\\` a la última línea, LaTeX asumiría una nueva línea y la numeraría, incluso si la línea está vacía.

La alineación depende del entorno. Aquí hay una lista de los entornos multilínea de `amsmath`:

- `multline`: La primera línea está alineada a la izquierda, la última línea está alineada a la derecha y todas las demás están centradas
- `gather`: Cada línea está centrada
- `align`: Use `&` para marcar un símbolo donde desea alinear las fórmulas; use otro símbolo `&` para terminar una columna si necesita varias columnas alineadas
- `flalign`: Es similar a `align`, pero las columnas se alinean a ras con los márgenes izquierdo y derecho, respectivamente
- `alignat`: Permite la alineación en varios lugares, cada uno de los cuales debe marcarse con `&`
- `split`: Es similar a `align`, pero se puede usar dentro de otro entorno matemático
- `aligned`, `gathered` y `alignedat`: Se utilizan para un bloque alineado dentro de un entorno matemático, que puede ser matemáticas mostradas en bloque o en línea

Los últimos entornos, incluido `split`, a menudo se colocan dentro de un entorno `equation` externo para que varias líneas compartan un solo número de ecuación.

La numeración se puede ajustar de la siguiente manera.

#### Numeración de líneas en fórmulas multilínea

En entornos matemáticos de varias líneas, cada línea se numera como una ecuación normal. Si desea suprimir el número de una línea específica, coloque el comando `\notag` antes del final de la línea. A menudo es mejor numerar solo las líneas a las que planea hacer referencia.

Si prefiere un estilo particular de numeración, como un símbolo o un nombre como etiqueta para una fórmula, puede usar el comando `\tag`, como `\tag{$\star$}` para marcarlo con una estrella, o `\tag{name}` para etiquetarlo como (name).

Si desea evitar la numeración por completo, utilice una versión con asterisco, como `align*` o `gather*`.

#### Inserción de texto en fórmulas

Para colocar texto normal en una fórmula, el LaTeX estándar proporciona el comando `\mbox{text}`. El paquete `amsmath` añade opciones más flexibles:

- `\text{words}` inserta palabras en la fuente del texto regular dentro de una fórmula matemática y ajusta su tamaño al estilo matemático actual. `\text` produce texto más pequeño dentro de subíndices o superíndices.
- `\intertext{text}` suspende la fórmula, imprime el texto como su propio párrafo y luego reanuda la fórmula de varias líneas preservando la alineación. Esto es útil para anotaciones más largas.

Estos comandos son útiles cuando desea incluir texto dentro de entornos matemáticos.

Veamos ahora los símbolos matemáticos.

---

### Exploración de la gran variedad de símbolos matemáticos

Vayamos más allá de escribir variables y operadores matemáticos básicos. La escritura matemática a menudo requiere una amplia gama de símbolos: signos de relación, operadores unarios y binarios, operadores tipo función, símbolos de suma e integral, flechas y muchos otros. LaTeX y paquetes adicionales proporcionan miles de símbolos para estos propósitos.

En esta sección, veremos una selección de símbolos matemáticos y los comandos que los producen. Cubriremos muchos de los símbolos disponibles en el LaTeX estándar; el paquete `latexsym` agrega algunos más. Paquetes adicionales, como el paquete `amssymb`, ofrecen una colección aún mayor.

#### Símbolos de operaciones binarias

Junto con más y menos, LaTeX admite una variedad de otros operadores binarios:

> **Figura 9.19** – Símbolos de operaciones binarias

Debe incluir `\usepackage{latexsym}` en el preámbulo de su documento para usar los símbolos de la última fila.

#### Símbolos de relación

Los valores de las expresiones pueden ser iguales, en cuyo caso solo necesita un signo igual, pero son posibles muchas otras relaciones. Por ejemplo, los objetos pueden ser congruentes, paralelos o pueden tener cualquier otra relación:

> **Figura 9.20** – Símbolos de relación binaria

Puede negar cualquier relación insertando `\not` antes de ella. Por lo tanto, para *no equivalente*, use `\not \equiv` para crear un símbolo `\equiv` tachado.

#### Símbolos de relación de desigualdad

Si las expresiones no son iguales, podemos expresarlo de varias maneras. Los más simples son los símbolos básicos `<` y `>`, pero también hay relaciones como menor o igual y mayor o igual:

> **Figura 9.21** – Símbolos de relación de desigualdad

Aquí, `\neq` se ve exactamente como lo que se obtiene cuando se escribe `\not=`, como en la sección anterior.

#### Símbolos de subconjunto y superconjunto

LaTeX proporciona muchos símbolos para describir cómo se relacionan los conjuntos entre sí:

> **Figura 9.22** – Símbolos de subconjunto y superconjunto

Nuevamente, puede usar `\not` para negar dicha relación de conjuntos.

#### Flechas

LaTeX proporciona una amplia gama de símbolos de flecha:

> **Figura 9.23** – Flechas

Las flechas se utilizan en muchos contextos: para implicaciones, asignaciones entre conjuntos, límites, secuencias, notación vectorial y diversas expresiones descriptivas.

#### Arpones (*harpoons*)

LaTeX proporciona un tipo especial de símbolo de flecha llamado arpones, que parecen puntas de flecha de un solo lado:

> **Figura 9.24** – Arpones

Los arpones se utilizan, por ejemplo, en fórmulas de reacciones químicas.

#### Símbolos derivados de letras

Las matemáticas utilizan varios símbolos que se asemejan a letras estilizadas:

> **Figura 9.25** – Símbolos derivados de letras

Los matemáticos suelen utilizar `\in`, `\forall` y `\exists` en sus declaraciones.

#### Símbolos diversos

Aquí hay algunos símbolos de LaTeX que no encajan en las categorías mencionadas anteriormente:

> **Figura 9.26** – Símbolos adicionales de LaTeX

La *Comprehensive LaTeX Symbol List* enumera más de 20.000 símbolos ordenados en categorías en un solo documento PDF. Si necesita buscar un símbolo, este documento es el mejor lugar para comenzar. Con TeX Live, puede abrirlo en el símbolo del sistema de la siguiente manera:

```bash
texdoc symbols
```

O puede visitar [https://texdoc.org/pkg/symbols](https://texdoc.org/pkg/symbols) para explorarlo.

Otro enfoque fascinante es el reconocimiento de símbolos escritos a mano. Dibuja un símbolo con el ratón o con el dedo en una pantalla táctil y el software intenta reconocerlo y le indica su código. Echemos un vistazo rápido:

1. Visite [https://detexify.kirelabs.org](https://detexify.kirelabs.org/).
2. Dibuje el símbolo en el cuadro blanco. No importa si es un boceto tembloroso con el ratón, como este:

> **Figura 9.27** – Símbolo manuscrito

3. Después de un momento, la herramienta muestra sugerencias de símbolos junto con los comandos de LaTeX correspondientes:

> **Figura 9.28** – Sugerencias de símbolos y código

Detexify también ofrece una búsqueda basada en nombres. Haga clic en el botón **Symbols** en la parte superior, ingrese una frase en el filtro y Detexify mostrará los símbolos y comandos que coinciden con su consulta.

#### Escritura de unidades

Al escribir unidades en el texto, no deben parecer variables. Por ejemplo, `m` para metros no debería verse exactamente como una variable `m`, y `s` puede significar segundos, pero no una variable `s`. Una convención tipográfica es utilizar una forma de fuente vertical (*upright*) para las unidades, mientras que las variables se escriben en cursiva. También es común colocar un espacio fino entre el valor y la unidad. Por lo tanto, para 10 metros, puede escribir `10\,\mathrm{m}`. En física, química e ingeniería, tenemos unidades mucho más complejas, como metros por segundo al cuadrado (m/s²) para la aceleración. El paquete `siunitx` admite la composición tipográfica correcta y coherente de dichas unidades. Requiere leer cierta documentación antes de poder usarlo, pero vale la pena el esfuerzo. Ejecute `texdoc siunitx` en el símbolo del sistema o visite [https://texdoc.org/pkg/siunitx](https://texdoc.org/pkg/siunitx).

#### Operadores de tamaño variable

Para sumas, productos, integrales y operaciones de conjuntos, LaTeX proporciona símbolos de operadores que ajustan su tamaño automáticamente: aparecen más grandes en estilo de bloque (*display style*) y más pequeños en estilo de texto (*text style*).

> **Figura 9.29** – Operadores de tamaño variable

Aquí hay una ecuación en estilo de texto (*text style*):

```latex
\( \int_a^b \! f(x) \, dx = \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{n} f(x_i) \,\Delta x_i \)
```

Este código nos da lo siguiente:

> **Figura 9.30** – Ecuación en estilo de texto en línea

Y aquí está la misma ecuación en estilo de bloque (*displayed style*):

```latex
\[ \int_a^b \! f(x) \, dx = \lim_{\Delta x \rightarrow 0} \sum_{i=1}^{n} f(x_i) \,\Delta x_i \]
```

Esta vez, obtenemos lo siguiente:

> **Figura 9.31** – Ecuación en estilo mostrado en bloque

Como puede ver, los símbolos de operador son notablemente más grandes en el estilo mostrado en bloque.

#### Delimitadores de tamaño variable

Delimitadores como paréntesis, corchetes y llaves pueden cambiar de tamaño según la expresión que encierren. Los siguientes son tales delimitadores de LaTeX:

> **Figura 9.32** – Delimitadores de tamaño variable

LaTeX proporciona comandos especiales para ajustarlos automáticamente. Si coloca un comando `\left` o `\right` justo antes de dicho delimitador, LaTeX hace coincidir automáticamente su tamaño con la altura de la expresión adjunta. Tenemos que usar estas macros de tamaño en parejas. Para hacer coincidir un par, si no desea un segundo delimitador, use `\left.` o `\right.` para obtener un delimitador invisible en un lado.

El ajuste automático de delimitadores es especialmente útil para estructuras más grandes, como matrices, así que veamos esas a continuación.

---

### Construcción de estructuras matemáticas

Las variables y las constantes son sencillas, pero la escritura matemática a menudo involucra objetos más complejos, como coeficientes binomiales, vectores y matrices. En esta sección, veremos cómo componer tales estructuras.

Comencemos con matrices simples (*arrays*).

#### Creación de matrices con array

Para organizar expresiones matemáticas dentro de una expresión más grande, puede usar el entorno `array`. Funciona de manera muy similar a un entorno `tabular`, pero es para modo matemático, y todas sus entradas también están escritas en modo matemático.

Por ejemplo, puede colocar un `array` dentro de paréntesis de tamaño variable:

```latex
\[ A = \left( \begin{array}{cc} a_{11} & a_{12} \\ a_{21} & a_{22} \end{array} \right) \]
```

Esto produce una matriz:

> **Figura 9.33** – Un array simple

También existen comandos dedicados para matrices, que veremos a continuación.

#### Composición tipográfica de matrices

El paquete `amsmath` proporciona varios entornos de matrices. Una matriz estándar se puede producir con el entorno `pmatrix`:

```latex
\documentclass{article}
\usepackage{amsmath}
\begin{document}
\[
  A = \begin{pmatrix}
        a_{11} & a_{12} \\
        a_{21} & a_{22}
      \end{pmatrix}
\]
\end{document}
```

Esto produce lo siguiente:

> **Figura 9.34** – Una matriz simple

Puede notar que los paréntesis se sitúan más cerca de las entradas de la matriz que en el ejemplo de `array` de la sección anterior. Este espaciado más ajustado es parte del estilo `amsmath`.

Aquí están los entornos de matriz de `amsmath` y sus delimitadores:

- `matrix`: Sin delimitadores
- `pmatrix`: Paréntesis, `( )`
- `bmatrix`: Corchetes, `[ ]`
- `Bmatrix`: Llaves, `{ }`
- `vmatrix`: `| |`
- `Vmatrix`: `|| ||`
- `smallmatrix`: Más compacto, sin delimitadores; puede agregarlos manualmente si es necesario

El entorno compacto `smallmatrix` es útil para matrices que aparecen dentro del texto normal.

#### Escritura de coeficientes binomiales

Podría escribir coeficientes binomiales utilizando un `array` junto con delimitadores, pero el paquete `amsmath` proporciona un comando más corto y limpio: `\binom` para coeficientes binomiales. Pruebe esto:

```latex
\binom{n}{k} = \frac{n!}{k!(n-k)!}
```

El resultado es el siguiente:

> **Figura 9.35** – Un coeficiente binomial en una ecuación

Esta sintaxis es mucho más simple que usar un `array` o una matriz para una expresión tan pequeña.

#### Subrayado y sobrelineado

El comando `\overline` coloca una línea sobre su argumento:

```latex
\overline{\Omega}
```

Esto produce lo siguiente:

> **Figura 9.36** – Un símbolo omega sobrelineado

El comando correspondiente para colocar una línea debajo es `\underline`.

También puedes usar llaves en lugar de líneas. Los comandos `\underbrace` y `\overbrace` crean llaves debajo o encima de una expresión:

```latex
N = \underbrace{1 + 1 + \cdots + 1}_n
```

Esto da lo siguiente:

> **Figura 9.37** – Una llave inferior debajo de una expresión

Un subíndice colocado en un `\underbrace` se escribe debajo de él, y un superíndice colocado en un `\overbrace` aparece arriba.

#### Establecimiento de acentos

En el [Capítulo 2](https://subscription.packtpub.com/book/business-and-other/9781805804574/2), *Formateo de texto y creación de macros*, ya hemos visto cómo escribir acentos en modo texto. Para el modo matemático, necesitamos comandos diferentes. Podemos aplicarlos a cualquier letra. Aquí está la lista de acentos matemáticos mostrados usando la letra minúscula `a` como ejemplo:

> **Figura 9.38** – Varios acentos matemáticos

Los acentos extensibles (*extensible accents*), también llamados acentos anchos (*wide accents*), se ajustan automáticamente al ancho de sus argumentos.

#### Poner un símbolo encima o debajo de otro

Más allá del entorno `array`, `amsmath` proporciona comandos para apilar expresiones directamente:

- `\underset{expression below}{expression}` coloca una expresión debajo de otra, usando texto del tamaño de un subíndice
- `\overset{expression above}{expression}` coloca una expresión encima de otra, usando texto del tamaño de un superíndice

Este es un ejemplo de cómo podemos usar estos comandos:

```latex
\underset{\circ}{\cap} \neq \overset{\circ}{\cup}
```

Esto nos da lo siguiente:

> **Figura 9.39** – Poner un símbolo encima o debajo de otro

Otro comando útil es `\stackrel{expression above}{relation}`. Vea la siguiente fórmula, por ejemplo:

```latex
X \stackrel{\text{def}}{=} 0
```

Esto da como resultado lo siguiente:

> **Figura 9.40** – Texto sobre un símbolo de relación

`\stackrel` coloca una expresión encima de un símbolo de relación.

#### Escritura de teoremas y definiciones

LaTeX proporciona entornos dedicados para teoremas, definiciones y declaraciones similares. Volviendo a nuestro primer ejemplo en este capítulo, podríamos usar el comando `\newtheorem` para definir un entorno de Teorema, `thm`, de la siguiente manera:

```latex
\newtheorem{thm}{Theorem}
```

A continuación, podemos declarar un entorno de Definición. Llamémoslo `dfn` aquí:

```latex
\newtheorem{dfn}[thm]{Definition}
```

Podemos usar un argumento opcional que se refiere a un entorno existente (en este caso, `thm`). Esto hace que el nuevo entorno use el mismo contador que el entorno ya existente. En nuestro caso aquí, esto significa que después de Theorem 1 sigue Definition 2.

Podemos utilizar estos entornos de la siguiente manera:

```latex
\begin{dfn}
A quadratic equation is an equation of the form
\begin{equation}
  \label{quad}
  ax^2 + bx + c = 0,
\end{equation}
where \( a, b \) and \( c \) are constants and \( a \neq 0 \).
\end{dfn}
\begin{thm}
A quadratic equation (\ref{quad}) has two solutions for the Variable \( x \):
\begin{equation}
  \label{root}
  x_{1,2} = \frac{-b \pm \sqrt{b^2-4ac}}{2a}.
\end{equation}
\end{thm}
```

Eche un vistazo a la salida:

> **Figura 9.41** – Una definición y un teorema

En la salida, dichos entornos están numerados y etiquetados como *Definition* y *Theorem*, respectivamente. En el [Capítulo 11](https://subscription.packtpub.com/book/business-and-other/9781805804574/11), *Desarrollo de documentos grandes*, utilizaremos este enfoque para crear un documento completo que contenga definiciones, teoremas y lemas.

Hay dos paquetes especiales que ofrecen mucha más flexibilidad:

- `amsthm` proporciona varios estilos, permite una personalización detallada e incluye un entorno de demostración `proof`
- `ntheorem` ofrece funciones similares pero maneja de mejor manera las marcas finales tradicionales de *quod erat demonstrandum* (lo que se quería demostrar) para las demostraciones

Si desea utilizar dichos entornos, consulte su documentación y compare las funciones relevantes para decidir qué paquete es mejor para usted. Como de costumbre, ejecute `texdoc amsthm` y `texdoc ntheorem` en el símbolo del sistema, o visite [https://texdoc.org/pkg/amsthm](https://texdoc.org/pkg/amsthm) y [https://texdoc.org/pkg/ntheorem](https://texdoc.org/pkg/ntheorem).

Elija uno de esos paquetes estrechamente relacionados; no cargue ambos.

#### Herramientas matemáticas extendidas

Eche un vistazo a todas las opciones de composición tipográfica de matemáticas en `amsmath` ingresando `texdoc amsmath` en la línea de comandos o visitando [https://texdoc.org/pkg/amsmath](https://texdoc.org/pkg/amsmath).

El paquete `mathtools` amplía `amsmath` y añade muchas funciones. Si busca algo que el LaTeX estándar o `amsmath` no ofrecen, `mathtools` es el siguiente lugar al que acudir. Estas son algunas de sus características:

- Herramientas para afinar la composición matemática, como estilos de superíndices más compactos
- Alineación vertical de límites para operadores consecutivos
- Ajuste del ancho de los operadores
- Control mejorado sobre las etiquetas (*tags*), incluida la modificación de su apariencia y la visualización de etiquetas solo para ecuaciones a las que se ha hecho referencia
- Símbolos extensibles: más flechas con ajuste automático de ancho, así como corchetes y llaves extensibles para colocar debajo o sobre expresiones
- Nuevos entornos matemáticos para matrices más flexibles, casos (*cases*), fórmulas multilínea mejoradas y flechas entre expresiones alineadas
- Espaciado más estrecho para un `\intertext` más corto
- Declaración de delimitadores emparejados
- Símbolos adicionales, como dos puntos centrados verticalmente, junto con combinaciones de símbolos de relación con dos puntos y atajos para paréntesis de tamaño automático
- Técnicas para distribuir líneas en fórmulas multilínea, establecer subíndices y superíndices izquierdos, componer matemáticas dentro de texto en cursiva y crear fracciones multilínea

Consulte la documentación de este valioso paquete y descubra qué comandos se pueden aplicar para lograr los estilos y alineaciones enumerados aquí. Ábralo ejecutando `texdoc mathtools` en la línea de comandos o vaya a [https://texdoc.org/pkg/mathtools](https://texdoc.org/pkg/mathtools).

En el [Capítulo 10](https://subscription.packtpub.com/book/business-and-other/9781805804574/10), *Escritura de matemáticas avanzadas*, en *LaTeX Cookbook*, puede encontrar muchos ejemplos que muestran mejoras con el paquete `mathtools`. Visite [https://latex-cookbook.net/tag/mathematics/](https://latex-cookbook.net/tag/mathematics/) para ver y ejecutar ejemplos en línea que incluyen el ajuste fino de fórmulas matemáticas, el salto automático de líneas en ecuaciones, el trazado de funciones y el dibujo de diagramas e imágenes geométricas.

---

### Resumen

Ahora puede escribir fórmulas matemáticas complejas y tiene las herramientas esenciales para escribir textos científicos. Trabajamos con el paquete `amsmath`, que nos brinda muchas características adaptadas a la composición tipográfica matemática tradicional.

Puede encontrar más ejemplos de código en el [Capítulo 10](https://subscription.packtpub.com/book/business-and-other/9781805804574/10), *Escritura de matemáticas avanzadas*, de *LaTeX Cookbook*, con código compilable en el sitio web del libro en [https://latex-cookbook.net/chapter-10](https://latex-cookbook.net/chapter-10).

En este punto, ahora puede ajustar expresiones matemáticas, alinear y numerar ecuaciones y trabajar con una amplia gama de símbolos matemáticos de varias fuentes de símbolos. En el próximo capítulo, veremos las fuentes en general.
