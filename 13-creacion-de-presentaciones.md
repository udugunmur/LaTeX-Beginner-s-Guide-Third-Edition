# LaTeX Beginner's Guide
## Capítulo 13: Creación de Presentaciones

En el capítulo anterior, usamos hipervínculos para navegar como lectores. Cuando realiza una presentación, necesita navegación para el orador. Hasta ahora en este libro, nos hemos centrado en documentos destinados a ser leídos en papel. Presentar en vivo, en proyectores o pantallas, en charlas académicas o en sesiones de Zoom o Microsoft Teams, requiere un enfoque diferente para el diseño visual y las herramientas de navegación. Precisamente para este propósito, LaTeX ofrece una clase de presentación dedicada con soporte incorporado para diseño de diapositivas, navegación y presentación, priorizando el hablar sobre el leer. Se llama la clase `beamer`, nombrada según el término tradicional para un proyector de video que emite (*beams*) luz sobre una pantalla.

En este capítulo, usaremos esta clase y trabajaremos a través de los temas clave necesarios para crear presentaciones con LaTeX. Cubriremos los siguientes temas:

- Primeros pasos con la clase beamer
- Uso de superposiciones (*overlays*) y revelaciones incrementales
- Disposición de columnas
- Uso de bloques
- Generación de un folleto (*handout*)

Comencemos configurando nuestra primera presentación.

---

### Primeros pasos con la clase beamer

Construiremos una pequeña presentación paso a paso para ver cómo funciona la clase `beamer` en la práctica. Representará una charla ficticia de Till Tantau, el creador de la clase `beamer`, con reflexiones sobre las mejores prácticas.

Siga estos pasos en su editor:

1. Comience el documento utilizando la clase `beamer`:

```latex
\documentclass{beamer}
```

2. Elija un tema que defina el diseño visual. Aquí, usamos el tema `Warsaw`, que proporciona un diseño bastante rico y estructurado:

```latex
\usetheme{Warsaw}
```

3. A continuación, agregue algunos metadatos para la presentación, como el título, el autor, la fecha y la afiliación:

```latex
\title{How to Give a Presentation}
\subtitle{And Keep Everyone Awake}
\author{Prof. Dr. Till Tantau}
\institute{Universität zu Lübeck}
\date{April 1, 2026}
```

4. Comience el documento:

```latex
\begin{document}
```

5. A partir de este punto, cada diapositiva reside dentro de un entorno `frame`. Comenzamos con una página de título:

```latex
\begin{frame}
\titlepage
\end{frame}
```

6. Agregue una diapositiva con una tabla de contenidos para darle a la audiencia una visión general:

```latex
\begin{frame}
\frametitle{Overview}
\tableofcontents
\end{frame}
```

7. Declare una sección y una subsección:

```latex
\section{Planning the talk}
\subsection{Things That Work}
```

8. Ahora agregue algo de contenido real. Mantenga el texto breve y enfocado. Las listas funcionan particularmente bien en presentaciones. Nuevamente, todo va dentro de un entorno `frame`, y puede darle tanto un título como un subtítulo:

```latex
\begin{frame}
\frametitle{Favor the main message over details}
\framesubtitle{Define the overall structure early}
\begin{itemize}
  \item Plan around the available time
  \item Favor the main message over details
  \item Keep section titles self-explanatory
  \item Follow a clear logical flow
  \item Start by stating the topic and goal
  \item End with a short, clear summary
\end{itemize}
\end{frame}
```

9. Agregue otra subsección y marco (`frame`):

```latex
\subsection{Things That Don't}
\begin{frame}
\frametitle{What to Avoid}
\framesubtitle{How to not mess it up}
\begin{itemize}
  \item Don't read slide text out loud
  \item Don't talk too fast
  \item Never overload slides with content
  \item Avoid subsubsections
  \item Don't speak to the slides, talk to the audience
  \item Cut details, put them into the appendix
\end{itemize}
\end{frame}
```

10. Para tener una mejor idea de la estructura y la navegación, agregue algunas secciones más:

```latex
\section{Structuring the Presentation}
\section{Building the Presentation}
```

11. Termine el documento con un marco más para que la última sección no esté vacía; de lo contrario, las secciones sin contenido posterior se ignorarían:

```latex
\begin{frame}
More text
\end{frame}
\end{document}
```

12. Compile el documento al menos dos veces para que LaTeX tenga la oportunidad de generar la tabla de contenidos y las entradas de navegación.

Mire el resultado. Esta es la primera diapositiva:

> **Figura 13.1** – La diapositiva de título

Obtuvimos una diapositiva de título bien diseñada con todos los metadatos incluidos. Puede ver la navegación de secciones en la parte superior y los símbolos de navegación en la parte inferior. Acerquémonos a la barra de botones de navegación:

> **Figura 13.2** – La barra de botones de navegación

Hacer clic en esos símbolos interactivos le permite avanzar y retroceder diapositivas y saltar entre secciones. Esto funciona en cualquier visor de PDF que admita enlaces, como Adobe Acrobat Reader.

Así es como funcionan, de izquierda a derecha:

- Un clic en el primer rectángulo, un icono de diapositiva, le permite ingresar el número de diapositiva al que desea saltar. Las flechas izquierda y derecha le permiten saltar una diapositiva hacia adelante o hacia atrás.
- Los rectángulos apilados representan un marco con varias diapositivas en una superposición (*overlay*). Hacer clic en la flecha izquierda salta al principio del marco, la flecha derecha lo mueve al final del marco, omitiendo la revelación paso a paso en esa diapositiva.
- Las flechas junto al icono de subsección se utilizan para navegar al principio o al final de una subsección.
- El siguiente símbolo parece una sección resaltada con subsecciones; aquí, las flechas lo mueven a la primera o última diapositiva de una sección.
- Luego tenemos el símbolo de la tabla de contenidos. Al hacer clic en su lado izquierdo se salta al principio, y al hacer clic en el lado derecho se pasa a la última diapositiva. En caso de que tenga un apéndice, aparecerá otro símbolo similar que hace lo mismo para el apéndice, saltando a la diapositiva inicial o final.
- El símbolo de la lupa es el icono de "buscar" (*search* o *find*), donde puede ingresar una cadena de texto para buscar en toda la presentación. Las flechas situadas a su lado se utilizan para desplazarse entre las diapositivas visitadas anteriormente.

Una vez que haya hecho una pequeña presentación, pruebe esta navegación. Por supuesto, también puede utilizar la navegación estándar de su lector de PDF, incluidas las teclas de flecha. Admito que normalmente elijo el camino fácil simplemente usando las teclas de flecha hacia adelante y hacia atrás.

Tenga en cuenta que puede eliminar la barra de navegación de `beamer` desactivándola en el preámbulo de la siguiente manera:

```latex
\setbeamertemplate{navigation symbols}{}
```

La segunda diapositiva es nuestra tabla de contenidos que muestra las secciones y subsecciones:

> **Figura 13.3** – La tabla de contenidos

Las siguientes diapositivas son el contenido real. Eche un vistazo, especialmente a la parte superior de la diapositiva:

> **Figura 13.4** – Una diapositiva con contenido

En la parte superior, puede ver la sección actual resaltada en el lado izquierdo y la subsección actual resaltada en el lado derecho. Puede hacer clic en el título de la sección o subsección para ir directamente a esa sección o subsección.

A medida que pasa a la siguiente diapositiva, observe el cambio en el resaltado en el área superior derecha:

> **Figura 13.5** – Una diapositiva de la siguiente subsección

Puede mostrar su presentación utilizando cualquier lector de PDF en su computadora portátil conectada a un proyector o en una pantalla compartida en una sesión de Zoom o Teams.

La relación de aspecto predeterminada de las diapositivas de `beamer` es 4:3. Sin embargo, muchos proyectores y pantallas modernos utilizan 16:9. Puede cambiar a ese formato agregando una opción a la clase de documento:

```latex
\documentclass[aspectratio=169]{beamer}
```

Tenga en cuenta que la opción no utiliza dos puntos (`:`). Beamer espera una palabra clave numérica, no una proporción escrita como 16:9. Establece la relación de aspecto dando dígitos, y `beamer` los interpreta según cuántos haya:

- Dos dígitos: `aspectratio=43` significa 4:3
- Tres dígitos: `aspectratio=128` significa 12:8
- Cuatro dígitos: `aspectratio=1610` significa 16:10

En resumen, pasa la proporción como dígitos y `beamer` hace los cálculos para calcular el ancho de la diapositiva, siempre en formato horizontal (*landscape*). Internamente, la clase `beamer` también elige un tamaño de papel adecuado para que los tamaños de fuente se vean bien en pantalla.

---

### Uso de superposiciones y revelaciones incrementales

Cuando escucho una charla con diapositivas, a menudo me sorprendo leyendo por adelantado. Mientras el orador todavía está explicando el primer punto, mis ojos ya están en la última viñeta. Esto dificulta seguir la explicación hablada, especialmente cuando la diapositiva se puede leer más rápido de lo que se puede explicar. Si bien una diapositiva muestra todo a la vez, a menudo puede preferir que partes de ella aparezcan solo cuando comience a hablar de ellas.

Para esto sirven las superposiciones (*overlays*). Un marco (*frame*) en el archivo fuente puede producir varias diapositivas. Partes del contenido pueden aparecer, desaparecer o cambiar de una diapositiva a la siguiente. Las superposiciones controlan cuándo algo se vuelve visible, por ejemplo, al revelar elementos de una lista paso a paso o al construir una fórmula por etapas. Comenzaremos con las superposiciones más simples y luego pasaremos a un control más preciso.

#### Pausa de contenido

El comando `\pause` es la forma más sencilla de crear superposiciones. Permite que un marco se despliegue paso a paso. Dentro de un marco, todo lo anterior a un `\pause` se muestra en la diapositiva actual; todo lo posterior se retrasa hasta que avance a la siguiente. Cada `\pause` adicional agrega otro paso. Todo esto sucede dentro de un solo entorno `frame`.

Puede colocar `\pause` casi en cualquier lugar, incluso dentro de entornos como `itemize`, como se muestra aquí:

```latex
\begin{frame}
\begin{itemize}
  \item Keep one clear idea per slide
  \pause
  \item Use short phrases, not full sentences
  \pause
  \item Use large, readable fonts
\end{itemize}
\end{frame}
```

Esto produce tres diapositivas, cada una revelando un punto adicional, y la diapositiva final muestra los tres.

#### Uso de especificaciones incrementales

Puede utilizar corchetes angulares `< >` para proporcionar información de sincronización. Rara vez se utilizan en texto normal, por lo que destacan claramente sin estorbar.

Por ejemplo, `<2-3>` significa que el contenido es visible en las superposiciones 2 y 3 del marco actual. Los números le dicen a `beamer` cuándo aparece el contenido y hasta cuándo permanece visible. A esto lo llamamos una especificación de superposición (*overlay specification*).

Más práctica para el uso diario, la sintaxis abreviada `<1->` simplemente significa desde la superposición 1 en adelante. El número le dice a `beamer` cuándo aparece el contenido por primera vez, y el guion solo significa que permanece visible en todas las superposiciones siguientes del marco. Por lo tanto, en lugar de usar el comando `\pause`, puede escribir una lista como esta, funcionando de la misma manera:

```latex
\begin{itemize}
  \item<1-> Use a consistent color scheme throughout the slides
  \item<2-> Ensure sufficient contrast for readability
  \item<3-> Keep visual elements balanced on the slide
\end{itemize}
```

#### Uso de atajos

Escribir números de superposición explícitos le brinda un control total, pero puede volverse tedioso para listas largas. `beamer` puede contar superposiciones por usted. Si usa un `+` dentro de una especificación de superposición en lugar de un número, `beamer` avanza automáticamente el contador de superposiciones. Cada `+` representa la siguiente superposición. Existen estos atajos:

- `\item<+->` produce un punto para la siguiente superposición que permanece visible
- `\item<+>` muestra un punto solo en la siguiente superposición, no visto en superposiciones posteriores

De esa manera, ya no necesita renumerar los elementos cuando inserta o elimina líneas.

Puede hacer esto aún más corto: en lugar de agregar una especificación de superposición a cada `\item`, puede colocarla en el entorno de la lista en sí:

```latex
\begin{itemize}[<+->]
```

De esa manera, `beamer` aplica `<+->` a cada elemento automáticamente. Cada elemento aparece en la siguiente superposición y permanece visible después. Esta suele ser la forma más limpia de crear listas incrementales.

Para mostrar la tabla de contenidos una sección a la vez mediante superposiciones, use `\tableofcontents[pausesections]`. Con `\tableofcontents[pausesubsections]`, se aplica lo mismo a nivel de subsección.

---

### Disposición de columnas

Algunas diapositivas funcionan mejor cuando el contenido se coloca uno al lado del otro, por ejemplo, texto junto a una figura o dos listas. Con `beamer`, puede dividir un marco en áreas verticales usando columnas. Cada columna contiene su propio contenido, mientras todo permanece alineado. Están diseñadas como entornos de LaTeX y ayudan a mantener las diapositivas claras y estructuradas.

Echemos un vistazo a una diapositiva de ejemplo simple, usando algo de contenido solo por diversión:

```latex
\begin{frame}
\begin{columns}
  \begin{column}{0.55\textwidth}
    What I don’t want to say:
    \begin{itemize}
      \item This slide looked better yesterday
      \item Just believe this
      \item I’ll skip this quickly
      \item Time is running out
    \end{itemize}
  \end{column}
  \begin{column}{0.4\textwidth}
    \includegraphics[width=4cm]{ctanlion.pdf}
  \end{column}
\end{columns}
\end{frame}
```

El entorno `columns` agrupa múltiples columnas dentro de un marco. No toma un ancho propio. El ancho se da como el argumento obligatorio de cada entorno `column`. Como se muestra aquí, es conveniente especificarlo como una fracción de `\textwidth`.

Así es como se ve la diapositiva:

> **Figura 13.6** – Una diapositiva con disposición en columnas

Ambos entornos también pueden tomar un argumento de alineación opcional, como este:

```latex
\begin{columns}[t]
\begin{column}[t]{0.5\textwidth}
```

Esto controla cómo se alinean las columnas verticalmente y cómo se alinea el contenido dentro de la columna en relación con las otras columnas:

- `t`: alineado en la parte superior (*top-aligned*)
- `c`: centrado verticalmente (*vertically centered*)
- `b`: alineado en la parte inferior (*bottom-aligned*)

---

### Uso de bloques

Para enfatizar puntos clave, puede utilizar bloques. Separan una idea importante del texto circundante y son útiles para definiciones, declaraciones clave, ejemplos, conclusiones breves o advertencias.

La clase `beamer` proporciona tres tipos de bloques estándar:

- `block` para énfasis neutral; por ejemplo:

```latex
\begin{block}{Using blocks}
You give the block a title and place the content inside it.
\end{block}
```

- `exampleblock` para ejemplos o demostraciones, como este:

```latex
\begin{exampleblock}{You see}
That’s how a block looks in a positive way.
\end{exampleblock}
```

- `alertblock` para contenido importante o de tipo advertencia, como aquí:

```latex
\begin{alertblock}{Warning}
Use blocks sparingly and intentionally. Not like on this slide.
\end{alertblock}
```

Todos funcionan igual y solo se diferencian en su estilo visual. Con el tema `Warsaw`, la diapositiva se verá así:

> **Figura 13.7** – Tipos de bloques

Con otro tema, los bloques pueden verse diferentes, ya que cada tema tiene su propio estilo visual y estructural. Tomemos otro tema en la siguiente sección.

---

### Generación de un folleto (handout)

Después de una charla, la audiencia puede querer algo que pueda leer a su propio ritmo. Para eso sirve un folleto (*handout*): una versión estática de su presentación sin superposiciones, a menudo dispuesta para que quepan varias diapositivas en una página para imprimir.

La clase `beamer` puede generar dicho folleto directamente desde el mismo archivo fuente, utilizando superposiciones que se aplanan para leer en lugar de presentar. Eso se hace rápidamente de esta manera:

1. Agregue la opción `handout` a la clase de documento:

```latex
\documentclass[handout]{beamer}
```

2. Cargue el paquete `pgfmorepages` para colocar varias diapositivas en una página:

```latex
\usepackage{pgfmorepages}
```

3. Elija un diseño: aquí, cuatro diapositivas en una página, ligeramente reducidas:

```latex
\pgfpagesuselayout{4 on 1}[a4paper, border shrink=0.25cm, landscape]
```

4. Usemos un tema diferente para que vea cuánto pueden cambiar el aspecto y la estructura. Obtendremos la navegación de secciones y la metainformación en el lado izquierdo en lugar de en la parte inferior, y viñetas cuadradas en lugar de viñetas redondas:

```latex
\usetheme{Berkeley}
```

5. Compile y eche un vistazo al archivo PDF. Esta es la primera página, papel A4 en orientación horizontal (*landscape*):

> **Figura 13.8** – Un folleto (handout) para imprimir

Puede tener hasta 16 diapositivas en una página y diferentes disposiciones. Para obtener más información, visite [https://texdoc.org/pkg/pgfmorepages](https://texdoc.org/pkg/pgfmorepages).

---

### Resumen

Este capítulo ofreció una introducción rápida a la creación de su propia presentación, utilizando la menor sintaxis técnica posible. La clase `beamer` es muy potente y viene con muchas características y detalles para explorar. Si desea profundizar más, consulte el manual en [https://texdoc.org/pkg/beamer](https://texdoc.org/pkg/beamer) o ejecute `texdoc beamer` en la línea de comandos.

El *LaTeX Cookbook* muestra algunos ejemplos y soluciones útiles en el [Capítulo 1](https://subscription.packtpub.com/book/business-and-other/9781805804574/1), *Exploración de varias clases de documentos*. Puede encontrar el código de los ejemplos con capturas de pantalla en [https://latex-cookbook.net/chapter-01](https://latex-cookbook.net/chapter-01).

Para explorar la variedad de temas de beamer, visite [https://latex-beamer.net](https://latex-beamer.net).

Si desea consultar una clase de presentación más nueva y aún experimental, visite [https://texdoc.org/pkg/ltx-talk](https://texdoc.org/pkg/ltx-talk). Es menos compleja y se centra en la accesibilidad con el etiquetado moderno de PDF.

Durante nuestro trabajo, podemos encontrar errores y advertencias. Eso también es común para los usuarios avanzados de LaTeX. El siguiente capítulo nos preparará para la resolución de problemas.
