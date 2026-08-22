# LaTeX Beginner's Guide
## Capítulo 16: Explorando la Tecnología: De Motores a IA

Después de trabajar a lo largo de 15 capítulos y construir una comprensión sólida de LaTeX, es un buen momento para dar un paso atrás y ver qué hay bajo el capó. En este capítulo final, exploraremos la tecnología detrás de LaTeX en sí, echaremos un vistazo a TeX específicamente y a los desarrollos modernos, y señalaremos otros libros y recursos que vale la pena revisar.

Este capítulo cubre los siguientes temas:

- Una mirada a los motores TeX
- Comprensión de los formatos TeX
- Selección de motor y formato
- Uso de inteligencia artificial
- Lecturas complementarias

Como dicen antes de una carrera en NASCAR o IndyCar: pilotos, enciendan sus motores.

---

### Una mirada a los motores TeX

Un motor TeX es el programa que realiza la composición tipográfica real. Lee su archivo de entrada, comprende los comandos, expande las macros, divide el texto en líneas y páginas y produce la salida final. Cuando presiona **Typeset** o **Compile**, el motor convierte su código fuente en un documento terminado.

Existen diferentes motores TeX porque los requisitos para la composición tipográfica cambiaron con el tiempo. El TeX original se diseñó mucho antes de que Unicode se convirtiera en el estándar para representar texto, con soporte para muchos sistemas de escritura. Al mismo tiempo, las fuentes modernas suelen venir en formato OpenType. Las fuentes OpenType admiten grandes conjuntos de caracteres y funciones tipográficas avanzadas, como versalitas reales, ligaduras, variantes estilísticas y glifos específicos del idioma. Los motores TeX más nuevos se diseñaron teniendo en cuenta estas capacidades para que puedan manejar texto Unicode y fuentes OpenType de forma mucho más natural.

Repasemos los motores disponibles con un poco más de detalle.

#### El motor TeX clásico y la salida DVI

El motor TeX original no creaba archivos PDF. En su lugar, producía un archivo `.dvi`. DVI es la abreviatura de *Device Independent* (Independiente del dispositivo). Este archivo describe el diseño del documento sin dirigirse a ninguna impresora o pantalla específica. Programas independientes pueden convertir el archivo `.dvi` a formatos imprimibles o visualizables.

Internamente, TeX construye páginas a partir de pequeños bloques de construcción, llamados cajas (*boxes*), y utiliza un espaciado flexible, a menudo llamado pegamento (*glue*), para lograr saltos de línea y de página de alta calidad. En la práctica, los archivos DVI rara vez fueron el resultado final. Los usuarios solían convertirlos a PDF utilizando herramientas adicionales. Un flujo de trabajo común era convertir primero el archivo DVI a un archivo PostScript utilizando la herramienta `dvips`. PostScript es un lenguaje de descripción de páginas que las impresoras y los visores comprenden bien. Este archivo PostScript luego se convertía en un PDF usando el programa `ps2pdf`.

La herramienta `ps2pdf` es parte de Ghostscript, un paquete de software ampliamente utilizado que procesa y convierte archivos PostScript y PDF. En algunas configuraciones, los usuarios también pueden usar `dvipdf` o la herramienta más moderna `dvipdfmx`, que convierte un archivo DVI directamente a PDF sin un paso intermedio de PostScript.

La mayoría de los usuarios nunca llaman a `dvipdf` o `dvipdfmx` directamente. Los editores y las distribuciones de TeX eligen automáticamente la herramienta adecuada. Por lo general, solo presiona **Typeset** y el paso de conversión correcto ocurre en segundo plano.

El motor TeX clásico solo admite imágenes externas en formato EPS, en lugar de formatos comunes como PNG o JPEG, como vio en el [Capítulo 6](https://subscription.packtpub.com/book/business-and-other/9781805804574/6), *Inclusión de imágenes*.

Si desea ver cómo comenzó TeX y cómo se ve Plain TeX en su núcleo, eche un vistazo a *The TeXbook* de Donald Knuth en [https://ctan.org/pkg/texbook](https://ctan.org/pkg/texbook). Puede compilarlo usted mismo o comprar el libro. Otro gran libro es *TeX by Topic* de Victor Eijkhout, disponible gratuitamente en [https://www.eijkhout.net/tex/tex-by-topic.html](https://www.eijkhout.net/tex/tex-by-topic.html).

`eTeX` amplía el motor TeX clásico con un pequeño conjunto de características que ayudan principalmente a escribir macros más robustas y mejoran algunos comportamientos internos. Para la mayoría de los usuarios, `eTeX` se siente como el TeX clásico, por lo que los documentos existentes continúan funcionando sin cambios. Hoy en día, las extensiones de `eTeX` son parte de todos los motores TeX modernos, que veremos a continuación.

#### pdfTeX: el caballo de batalla de hoy

`pdfTeX` es el motor con el que comienzan muchos usuarios de LaTeX. Produce archivos PDF directamente y admite formatos de imagen comunes como PNG y JPEG.

Viene con un excelente soporte para la tipografía clásica, incluidas características microtipográficas. Su principal limitación es el manejo de fuentes. `pdfTeX` se limita a las fuentes PostScript tradicionales y a las fuentes de mapa de bits rara vez utilizadas; no funciona directamente con fuentes modernas del sistema. Aun así, todavía se utiliza ampliamente porque es fiable, rápido y más que suficiente para la mayoría de los documentos.

Para obtener detalles sobre `pdfTeX`, sus características y sus limitaciones, comience aquí:

- Página oficial del proyecto pdfTeX: [https://tug.org/applications/pdftex](https://tug.org/applications/pdftex)
- El manual de pdfTeX en CTAN: [https://ctan.org/pkg/pdftex](https://ctan.org/pkg/pdftex)

#### XeTeX: Unicode y fuentes del sistema

`XeTeX` está diseñado para funcionar con texto Unicode y fuentes modernas. Internamente, utiliza Unicode en todas partes y le permite acceder a las fuentes del sistema directamente, lo cual es una mejora importante con respecto a `pdfTeX`.

Esto hace que `XeTeX` sea una buena opción para documentos multilingües o textos que utilizan escrituras no latinas. Es fácil de usar y resuelve los problemas de fuentes de forma limpia, pero no se centra en la programabilidad ni en la automatización avanzada.

El nombre fue elegido para sugerir una versión extendida (*eXtended*) de `eTeX`. Dado que admite escrituras de derecha a izquierda como el árabe y el hebreo, un nombre que se lee igual en ambas direcciones parecía una elección adecuada y divertida.

Si desea obtener más información sobre `XeTeX`, la compatibilidad con Unicode y las fuentes del sistema, visite la página del proyecto `XeTeX` en [https://xetex.sourceforge.net](https://xetex.sourceforge.net/).

#### LuaTeX: extensibilidad y programabilidad

`LuaTeX` va un paso más allá al integrar el lenguaje de programación Lua directamente en el motor. Esto permite que el código Lua interactúe con el proceso de composición tipográfica y sea utilizado por los autores.

Eso se vuelve útil cuando los documentos ya no son estáticos. Con `LuaTeX`, puede generar contenido dinámicamente, procesar datos o implementar lógica compleja durante la compilación. Al igual que `XeTeX`, es totalmente compatible con Unicode y fuentes modernas. Si bien compila un poco más lento que los otros motores, tiene un mejor mantenimiento que `XeTeX` y está más estrechamente integrado, y sus características y programabilidad lo convierten en el motor TeX más flexible disponible en la actualidad.

Si usa `LuaLaTeX` y nota que se está utilizando `LuaHBTeX`, es simplemente una variante de `LuaTeX`: las letras HB representan HarfBuzz, un motor de modelado de texto que convierte el texto Unicode en glifos colocados correctamente y maneja escrituras complejas, ligaduras y funciones de fuentes modernas.

Echemos un vistazo breve a cómo podemos usar Lua en nuestros documentos. Repasaremos un ejemplo muy pequeño que implementa el algoritmo de Euclides para calcular el máximo común divisor (MCD / GCD) de dos números enteros:

1. Comience un nuevo documento. Use cualquier clase de documento que desee:

```latex
\documentclass{article}
```

2. Cargue el paquete `luacode`:

```latex
\usepackage{luacode}
```

3. Use un entorno `luacode` para implementar una función de Lua `GCD` con dos argumentos, `a` y `b`:

```latex
\begin{luacode}
function GCD(a,b)
  if b ~= 0 then
    return GCD(b, a % b)
  else
    return a
  end
end
\end{luacode}
```

4. Comience el documento:

```latex
\begin{document}
```

5. Escriba algo de texto que use el comando `\directlua` para hacer un cálculo:

```latex
The greatest common divisor of 96 and 36 is \directlua{tex.sprint(GCD(96,36))}.
```

6. Termine el documento:

```latex
\end{document}
```

7. Compile el documento. Recibirá esta salida:

```text
The greatest common divisor of 96 and 36 is 12.
```

El paquete `luacode` proporciona una forma segura de incrustar código Lua directamente en un documento de LaTeX sin preocuparse por cómo TeX manejaría los caracteres y el espaciado. El entorno con el mismo nombre ejecuta código Lua y puede acceder a él mediante el comando `\directlua`.

Con respecto a esa función: mientras `b` no sea 0, la función se ejecuta nuevamente con los argumentos `b` y `a%b`, que es lo que queda cuando `a` se divide por `b`. Esto mantiene el mismo MCD y reduce los números cada vez hasta que el proceso finalmente se detiene. Se puede encontrar una buena explicación en [https://en.wikipedia.org/wiki/Greatest_common_divisor](https://en.wikipedia.org/wiki/Greatest_common_divisor).

`tex.sprint` envía texto desde Lua de regreso a LaTeX, como si hubiera escrito ese texto directamente en su documento.

Es realmente un documento simple para demostrar que puede realizar incluso cálculos complejos usando Lua directamente dentro de LaTeX. Aquí puede ver ejemplos que creé utilizando cálculos más complejos para trazar fractales, sistemas caóticos definidos por ecuaciones diferenciales y otros algoritmos: [https://pgfplots.net/tag/luatex](https://pgfplots.net/tag/luatex).

Para obtener más información, visite [https://www.luatex.org](https://www.luatex.org/) y [https://www.lua.org](https://www.lua.org/).

#### LuaMetaTeX: combinación de TeX, Lua y MetaPost

`LuaMetaTeX` es un motor TeX que integra estrechamente Lua, Unicode, soporte para fuentes modernas y la funcionalidad del lenguaje de gráficos MetaPost. Como sucesor de `LuaTeX`, es el motor utilizado por el formato moderno ConTeXt, del que aprenderemos en la siguiente sección.

También existen motores para idiomas específicos. El motor `pTeX` es para la composición tipográfica japonesa y `upTeX` es su sucesor moderno basado en Unicode.

---

### Comprensión de los formatos TeX

Un formato TeX es un conjunto predefinido de macros construidas sobre un motor TeX. Mientras que el motor se encarga de la composición tipográfica de bajo nivel, el formato define los comandos que estructuran los documentos y que usted, como autor, utiliza.

Puede pensar en ello de esta manera: el motor es la maquinaria, mientras que el formato es la interfaz de usuario. Veamos los formatos más importantes que encontrará.

#### Plain TeX

Plain TeX es el formato original; es pequeño y está muy cerca del motor TeX subyacente. Le brinda control total pero muy poca comodidad. No hay una estructura de documento incorporada, por lo que incluso cosas simples como secciones y referencias requieren más trabajo. Hoy en día, Plain TeX es principalmente de interés histórico y lo utilizan unos pocos expertos que desean el máximo control.

#### LaTeX

LaTeX se basa en Plain TeX y agrega un amplio conjunto de comandos de alto nivel para la estructura del documento. Le dice qué es algo, como una sección, una figura o una tabla, y LaTeX se encarga del diseño. Lo ha visto en este libro; no se necesitan más palabras.

LaTeX tiene un enorme ecosistema de paquetes y funciona bien tanto para documentos simples como complejos. Combinado con el nombre del motor subyacente, llamamos a los diferentes sabores `pdfLaTeX`, `XeLaTeX`, `LuaLaTeX`, `pLaTeX` y `upLaTeX`.

#### ConTeXt

ConTeXt es un formato TeX con un enfoque diferente al de LaTeX. Es un sistema coherente todo en uno donde muchas funciones están integradas en lugar de agregarse a través de paquetes separados.

Ofrece potentes funciones de diseño y tipografía de inmediato, pero tiene una base de usuarios y un ecosistema muy reducidos. Los usuarios a menudo eligen ConTeXt para un control preciso sobre el diseño dentro de un único marco.

Una de las diferencias más visibles entre ConTeXt y LaTeX es cómo se escriben los entornos. En LaTeX, los entornos usan `\begin{...}` y `\end{...}`. En ConTeXt, la misma idea se expresa con comandos coincidentes `\start...` y `\stop...`.

Echemos un vistazo rápido a un documento de muestra de ConTeXt similar a lo que escribimos en el [Capítulo 12](https://subscription.packtpub.com/book/business-and-other/9781805804574/12):

```latex
\setuppapersize[A4]
\starttext
\startchapter[title={Equations}, reference=ch:eq]
\startsection[title={Quadratic equations}, reference=sec:quad]
A quadratic equation is an equation of the form
\placeformula[eq:quad]
\startformula
ax^2 + bx + c = 0
\stopformula
where $a$, $b$, and $c$ are constants and $a\neq 0$.
As shown in \in{equation}[eq:quad], quadratic equations
are discussed in \in{section}[sec:quad] of \in{chapter}[ch:eq].
\stopsection
\stopchapter
\stoptext
```

Mientras que LaTeX utiliza comandos para capítulos y un sistema de entornos genérico, ConTeXt utiliza el mismo patrón de inicio y parada (*start-and-stop*) en todas partes, incluidas las estructuras de alto nivel como capítulos y secciones. Al igual que en LaTeX, estos bloques se pueden anidar.

Si desea explorar ConTeXt más a fondo, los mejores puntos de partida son estos:

- El sitio web oficial de ConTeXt en [https://www.contextgarden.net](https://www.contextgarden.net/)
- Los manuales de ConTeXt en [https://www.pragma-ade.nl/general/manuals](https://www.pragma-ade.nl/general/manuals/mp-cb-nl.pdf)

---

### Selección de motor y formato

Primero, como pauta práctica:

- Utilice `pdfLaTeX` para documentos clásicos con fuentes estándar y un flujo de trabajo estable
- Elija `LuaLaTeX` si desea fuentes del sistema o necesita programación en Lua
- Utilice `XeLaTeX` si una plantilla lo requiere o si sus funciones de derecha a izquierda se ajustan mejor a sus necesidades; el desarrollo actual se centra más en `LuaLaTeX`
- Pruebe `ConTeXt` cuando desee una composición tipográfica basada en Lua con control de diseño integrado y esté listo para ir más allá de LaTeX con una sintaxis diferente, que sigue siendo TeX

Los editores de LaTeX le permiten seleccionar fácilmente el motor. Por ejemplo:

- En TeXworks, elija el motor del menú desplegable junto al botón **Typeset**, como ve en la Figura 10.19
- En TeXstudio, vaya a **Options | Configure TeXstudio | Build | Default Compiler**
- En Overleaf, abra **Menu/File | Settings | Compiler** y seleccione `pdfLaTeX`, `XeLaTeX` o `LuaLaTeX`

Si trabaja en la línea de comandos, en una ventana de terminal, seleccione el motor ejecutando su nombre (en minúsculas), como uno de estos comandos:

```bash
pdflatex filename.tex
xelatex filename.tex
lualatex filename.tex
context filename.tex
```

---

### Uso de inteligencia artificial

La inteligencia artificial (IA) es un software que no sigue instrucciones fijas como los programas tradicionales. En cambio, aprende analizando grandes cantidades de datos. Procesa información, incluida su entrada, utilizando lógica, estadísticas y algoritmos entrenados.

La IA ha avanzado rápidamente en los últimos años y se ha hecho ampliamente conocida con el surgimiento de ChatGPT. ChatGPT es un chatbot: usted introduce una pregunta o instrucción y responde según lo que ha aprendido durante el entrenamiento. Se hizo popular porque interactuar con él se siente muy natural, casi como hablar con una persona. Puede hacer preguntas de seguimiento, refinar respuestas e incluso ajustar aspectos como el tono, el estilo de escritura o el nivel de detalle.

A veces la salida es exactamente lo que necesita. A veces solo suena correcta y pueden ocurrir errores. Pero con bastante frecuencia, el resultado es lo suficientemente bueno como para ser realmente útil. Así que veamos cómo podemos hacer que funcione para nosotros.

Hay muchos chatbots de IA disponibles en la actualidad, creados por diferentes empresas y grupos de investigación. La mayoría de ellos funcionan de manera similar; las principales diferencias son la interfaz y los datos de entrenamiento subyacentes.

Aquí hay una lista de chatbots de IA actualmente populares y dónde encontrarlos:

- ChatGPT de OpenAI: [https://chat.openai.com](https://chat.openai.com/)
- Claude de Anthropic: [https://claude.ai](https://claude.ai/)
- Gemini de Google: [https://gemini.google.com](https://gemini.google.com/)
- Copilot de Microsoft: [https://copilot.microsoft.com](https://copilot.microsoft.com/)
- Perplexity de Perplexity AI: [https://www.perplexity.ai](https://www.perplexity.ai/)
- Meta AI de Meta: [https://www.meta.ai](https://www.meta.ai/)
- Grok de X.ai: [https://x.ai](https://x.ai/)

Todos ellos son útiles y no existe una única "mejor" opción. Personalmente, recomiendo usar ChatGPT. Es fácil comenzar a usarlo y está ampliamente extendido, y funciona muy bien para tareas centradas en texto, como generar código fuente de LaTeX.

ChatGPT ofrece una versión gratuita con la que es perfecto comenzar. Viene con límites de uso y le da acceso a modelos más pequeños con menos funciones. Hay una versión de pago que brinda acceso a modelos más capaces, respuestas más rápidas, límites de uso más altos y un mejor razonamiento. Si comienza a usarlo con frecuencia, puede valer la pena.

En *LaTeX Cookbook*, Capítulo 13, *Uso de inteligencia artificial con LaTeX*, escribí varias instrucciones paso a paso junto con respuestas de ChatGPT. Aquí, mantengámoslo un poco más breve y centrémonos en consejos generales, ya que las interfaces técnicas y las características de los bots de IA cambian rápidamente.

A continuación se explica cómo utilizar ChatGPT:

1. Abra el sitio web, [https://chat.openai.com](https://chat.openai.com/), en su navegador.
2. Haga clic en **Sign up** (Registrarse) para registrarse con una dirección de correo electrónico y una contraseña, o use rápidamente una cuenta de Google, Microsoft o Apple ID.
3. OpenAI le enviará un correo electrónico para confirmar su dirección. Haga clic en el botón **Verify email address** (Verificar dirección de correo electrónico) en ese mensaje.
4. Después de crear su cuenta, use **Log in** (Iniciar sesión) para continuar.
5. Una vez que haya iniciado sesión, estará listo para comenzar a chatear. Puede hacer preguntas o dar instrucciones y ChatGPT responderá.

Primero, hablemos de su entrada a la IA.

#### Trabajar con IA de manera eficiente

Cuando utiliza un chatbot de IA, el texto que escribe en él se llama *prompt*. Esa es la entrada que le da a un sistema de IA, que puede ser una pregunta, una instrucción o un fragmento de texto para analizar. Hace que la IA genere una respuesta.

Los *prompts* son la clave para un uso eficiente. Puede ser preciso: ingrese el tema, el contexto, el propósito, la situación, el nivel de la audiencia y cualquier restricción importante. Cuanto más claro sea el *prompt*, mejor será el resultado. Le dice a la IA qué hacer, para quién y bajo qué condiciones.

A continuación se muestran ejemplos de *prompts* sólidos:

- **Sea explícito**: "Explica cómo funciona la colocación de flotantes en LaTeX, centrándote en el posicionamiento preciso, y utiliza un lenguaje claro y sencillo para principiantes avanzados."
- **Proporcione contexto**: "Explica cómo funcionan juntos biblatex y biber, para un usuario con conocimientos básicos de LaTeX, que trabaja en macOS, incluidas las restricciones y los aspectos de compatibilidad."
- **Defina restricciones**: "Resume el siguiente texto en menos de 150 palabras, prosa continua, voz activa, tono de tutorial amigable sin entusiasmo excesivo, evita viñetas, prefiere comas o paréntesis en lugar de rayas em." (luego pegue el texto)
- **Itere**: "Reescribe tu respuesta anterior, hazla más corta y un poco más formal, manteniendo todos los detalles técnicos."

Ciertamente puede preguntar en frases breves y espontáneas, pero los *prompts* más largos y deliberados suelen conducir a mejores resultados, especialmente si planea reutilizarlos una y otra vez.

Veamos algunas ideas de lo que puede introducir.

#### Hacer preguntas relacionadas con LaTeX

Puede hacer cualquier pregunta sobre LaTeX que se le ocurra, como las siguientes:

- "¿Qué clase de documento es adecuada para una presentación? Da razones y muéstrame un pequeño ejemplo completo de código LaTeX."
- "¿Cuál es la diferencia entre LuaLaTeX y pdfLaTeX? Proporciona una guía de decisión."

Puede ver que es recomendable agregar lo que espera de una respuesta. Los resultados suelen ser sorprendentemente buenos, aunque la IA puede tener dificultades con temas específicos de nicho. Una vez que obtenga una respuesta, puede hacer preguntas de seguimiento para obtener aclaraciones, alternativas o una explicación más profunda.

#### Sugerir paquetes y soluciones alternativas

Puede pedirle al asistente de IA que le recomiende paquetes de LaTeX adecuados y describa enfoques alternativos para resolver un problema. Cuando existen varias soluciones, esto le ayuda a comparar opciones y decidir cuál se adapta mejor a su documento, a menudo más rápido que buscar en manuales o foros. Puede comenzar con una pregunta como esta: "¿Qué paquete es mejor para manejar referencias y citas en un documento largo? Compara las opciones principales y explica cuándo usar cada una."

#### Generar código LaTeX

Déle a un chatbot una instrucción clara y podrá generar código LaTeX para usted, ahorrándole tiempo y esfuerzo. Esto es especialmente útil para tablas complejas, donde escribir código `tabular` a mano puede ser tedioso. Puede describir cómo debería verse la tabla y el chatbot le dará un punto de partida sólido. También puede ayudar a crear entradas de BibTeX a partir de información básica, configurar entornos de figuras o redactar bloques de código más largos que pueda ajustar fácilmente. Esto funciona para casi cualquier estructura sintáctica compleja, incluidas presentaciones con superposiciones: usted describe lo que necesita, obtiene el código completo y luego lo refina. El código generado por IA aún puede requerir ajustes antes de que se compile limpiamente o se ajuste perfectamente a su documento.

He aquí un ejemplo de un *prompt* sólido:

"Genera un documento LaTeX mínimo pero completo que cree una tabla de aspecto profesional adecuada para una tesis científica. La tabla debe tener cinco columnas, colores de fila alternos, números alineados en la primera columna, un título (caption) y una etiqueta de referencia. Utiliza paquetes bien establecidos y explica brevemente tus opciones de diseño."

El *prompt* define claramente el diseño, establece el contexto, solicita opciones de paquetes y solicita una breve explicación para que comprenda qué hace realmente el código.

#### Explicar mensajes de error y advertencia

Los mensajes de error y advertencia de LaTeX pueden parecer crípticos a primera vista. Un asistente de IA puede traducirlos a un lenguaje sencillo. Puede pegar el mensaje en el chat y preguntar qué significa normalmente, dónde ocurre habitualmente y qué parte de su documento debe inspeccionar.

También puede enumerar causas comunes y sugerir pasos prácticos para resolver el problema. Esto hace que la depuración sea más rápida y mucho menos frustrante.

He aquí un ejemplo de *prompt*:

"Obtengo el siguiente error de LaTeX. Explica qué significa este error en términos sencillos, qué lo causa habitualmente y da instrucciones paso a paso sobre cómo localizarlo y corregirlo. Mensaje de error: Undefined control sequence."

Admito que a menudo mantengo mis *prompts* mucho más breves. Suelo tener suerte con los resultados, pero un *prompt* más detallado aumenta claramente las posibilidades de obtener exactamente lo que necesito.

#### Resolución de problemas y depuración

Un asistente de IA puede guiarle a través de la resolución de problemas paso a paso. Describa qué sale mal, qué esperaba en su lugar y pegue un fragmento de código. En base a eso, puede sugerir causas probables y correcciones prácticas, lo que le ayudará a delimitar el problema rápidamente.

Piense en ello como un compañero de discusión para la depuración. Pega el código relevante, incluye el mensaje exacto de error o advertencia y explica brevemente el contexto. A partir de ahí, puede iterar: probar la sugerencia, informar y refinar la solución.

#### Mejorar y pulir el texto existente

Un asistente de IA puede ayudarle a refinar el texto que ya ha escrito. Pegue un párrafo y pida una redacción más clara, una fluidez más suave o explicaciones más sencillas. Puede detectar problemas gramaticales, reducir la repetición y ajustar el tono mientras conserva su significado original.

Esto es especialmente útil cuando desea coherencia en un documento más largo. Puede especificar el tono deseado de antemano, como informal, técnicamente preciso, apto para principiantes o neutral, y luego solicitar una revisión basada en ese estilo.

He aquí un ejemplo de *prompt*:

"Revisa el siguiente párrafo. Mantén el significado técnico sin cambios. Utiliza un tono de tutorial claro e informal. Evita el lenguaje entusiasta y exagerado. Prefiere la voz activa y las oraciones cortas. Reduce la repetición y mejora la fluidez lógica." (Pegue su párrafo aquí)

Tenga en cuenta que esto ayuda a controlar el tono, ya que las respuestas de la IA tienden a sonar demasiado entusiastas de forma predeterminada.

También puede utilizar un asistente de IA para la traducción. A menudo he usado ChatGPT para comunicarme con colegas japoneses de LaTeX, traduciendo mensajes y luego pidiéndole que explique la redacción paso a paso para poder verificar que todo fuera preciso.

Para la revisión gramatical, también confío con frecuencia en ChatGPT. Sin embargo, para correcciones puras de gramática y estilo, encuentro más eficientes herramientas especializadas como Grammarly Pro. A veces utilizo ambas y luego decido si mantener mi redacción original o adoptar una de las revisiones sugeridas.

#### Lluvia de ideas sobre estructura, títulos e ideas de secciones

Un asistente de IA puede ser muy útil cuando está atascado o quiere planificar más rápido. Si la página todavía está en blanco, puede pedirle que sugiera una estructura de documento, un esquema de sección o posibles títulos. Esto le ayuda a superar el bloqueo del escritor y obtener un marco inicial. No tiene que aceptar el resultado tal cual, pero a menudo proporciona un punto de partida sólido para seguir adelante.

He aquí un ejemplo de *prompt*:

"Estoy escribiendo un documento sobre el soporte de IA en la redacción técnica basada en LaTeX. Propón un esquema detallado para un capítulo sobre depuración de documentos LaTeX asistida por IA. Incluye títulos de sección sugeridos, un flujo lógico, argumentos clave y posibles ejemplos o experimentos. Mantenlo académicamente riguroso pero práctico."

Usando esto, ChatGPT 5.2 me dio un esquema de 12 secciones con puntos clave y explicaciones que me dieron un buen comienzo para escribir mis propios pensamientos.

#### Usar la IA de manera responsable y cuidadosa

No animo a utilizar la IA para generar contenido directamente sin supervisión. La responsabilidad sigue siendo suya como autor. Las sugerencias, reformulaciones o ideas estructurales deben tratarse como borradores, no como resultados terminados. Revise todo cuidadosamente, verifique los hechos, asegure la integridad y asegúrese de que la redacción refleje su intención y se adapte a su audiencia. La IA puede acelerar partes del proceso y ayudarle a pensar, pero usted decide qué entra en última instancia en el documento.

Tenga cuidado al compartir información confidencial o sensible con herramientas de IA. El texto que envíe puede ser almacenado o procesado por el proveedor y quedar accesible para otros. Evite cargar datos privados, credenciales o material no publicado. Si utiliza soporte de IA en tales casos, anonimice nombres y detalles, y reduzca el contenido a lo estrictamente necesario.

#### Una mirada al futuro de la IA y LaTeX

Es difícil predecir el futuro en detalle, pero ya se vislumbran algunas tendencias.

Primero, los chatbots de IA están cambiando la forma en que las personas buscan ayuda. Para muchas preguntas cotidianas, ahora compiten directamente con los foros web tradicionales y los sitios de preguntas y respuestas. Los bots responden al instante, tienen paciencia y suelen ser técnicamente correctos. Eso los hace más atractivos que preguntar a humanos y esperar respuestas. Las plataformas comunitarias siguen desempeñando un papel importante, pero algunos sitios comerciales de preguntas y respuestas están bajo presión a medida que disminuyen el tráfico y los ingresos. Continuaré administrando foros impulsados por la comunidad como LaTeX.org para la discusión humana, pero el panorama claramente está cambiando.

En segundo lugar, la IA se está convirtiendo en parte de las herramientas que ya utilizamos. Los editores y las plataformas integran cada vez más la IA directamente en el flujo de trabajo de escritura. Overleaf es un ejemplo y están apareciendo nuevas herramientas.

Una de esas herramientas es Prism ([https://prism.openai.com](https://prism.openai.com/)), un editor de LaTeX basado en web con asistencia de IA incorporada. Se ejecuta completamente en línea y le permite escribir, editar y colaborar sin una configuración local de LaTeX. La diferencia clave es que la IA trabaja dentro del editor y comprende la estructura de su documento, el código fuente y el contexto. Puede solicitar mejoras de redacción, sugerencias estructurales o explicaciones sin salir de LaTeX.

Para los investigadores y redactores técnicos, esto puede ahorrar tiempo en la configuración, el formato y la revisión. La IA puede ayudar a pulir el texto y acelerar el proceso de redacción mientras usted mantiene el control del documento.

Nuevamente, un recordatorio importante: cuando comparte texto con un servicio de IA, ese contenido puede almacenarse, reutilizarse para entrenamiento o aparecer en respuestas a otros usuarios. Si eso es aceptable para su caso de uso, bien. Si no, sea precavido.

---

### Lecturas complementarias

Hemos llegado al final de este libro. En cada capítulo, quise contarle aún más. A menudo me referí a otros libros que escribí, así que veamos por qué y qué puede encontrar en ellos.

#### LaTeX Cookbook: más de 100 soluciones prácticas y avanzadas de LaTeX

Después de escribir la primera edición de *LaTeX Beginner's Guide*, me quedó claro que había mucho más de lo que podía cubrir un tutorial para principiantes. Así que trabajé en un conjunto de ejemplos para varios tipos de documentos, incluidos CVs, cartas, folletos y carteles, todos más allá del alcance de este libro, y escribí muchos consejos avanzados sobre varios temas, con soluciones específicas. Fue entonces cuando creé el *LaTeX Cookbook*. Se diferencia de *LaTeX Beginner's Guide*, que introduce conceptos paso a paso y explica los fundamentos en una secuencia de aprendizaje. Un libro de recetas presupone una familiaridad básica y se centra en soluciones concretas para problemas específicos. Cada sección es en gran medida independiente, con breves explicaciones seguidas de ejemplos prácticos que se pueden adaptar directamente a documentos reales.

Permítame resumir este libro. Comienza con clases de documentos, ajuste de texto y selección de fuentes, mostrando cómo se configuran los diferentes tipos de documentos y cómo las decisiones tipográficas afectan la salida. Los siguientes capítulos se centran en los elementos centrales del contenido: tablas, imágenes, gráficos y componentes de diseño. Cubren técnicas prácticas de diseño, alineación, objetos flotantes y mejoras visuales más allá del texto estándar.

Sigue la estructura y salida de todo el documento, incluidas tablas de contenidos, listas, bibliografías, glosarios, índices y funciones de PDF como metadatos, formularios, combinación y optimización. Las secciones avanzadas abordan la composición tipográfica matemática y las aplicaciones científicas, incluidas fórmulas, teoremas, gráficos, diagramas y ejemplos de ciencia y tecnología.

Los capítulos finales cubren el soporte externo y los flujos de trabajo modernos, con orientación sobre recursos en línea y el uso controlado de herramientas de IA para ayudar en el trabajo con LaTeX.

Puede encontrar información detallada en [https://latex-cookbook.net/contents](https://latex-cookbook.net/contents). Debido a la gran demanda, el libro fue traducido y publicado en japonés; el sitio web del libro es [https://tex.jp](https://tex.jp/).

#### LaTeX Graphics with TikZ: dibujo de imágenes

Escribí el *LaTeX Cookbook* con muchos ejemplos gráficos, incluidos varios tipos de diagramas, que son fáciles de crear. Entendí que, para una cobertura seria de las funciones de LaTeX para dibujar imágenes, se necesita un libro completamente nuevo. Así que escribí el primer libro de la historia sobre cómo dibujar imágenes en LaTeX con TikZ.

Este libro introduce TikZ paso a paso, desde conceptos básicos hasta gráficos avanzados y automatización. Comienza explicando qué es TikZ, cómo encaja en LaTeX y cómo se construyen los dibujos a partir de coordenadas, formas y colores. Los primeros capítulos establecen la sintaxis central y el modelo de dibujo. Luego, el enfoque se traslada a los gráficos estructurados basados en nodos y aristas. Aprende a colocar y alinear nodos, conectarlos con líneas y flechas y controlar el etiquetado, los estilos y la dirección.

A continuación, el libro introduce la abstracción y la reutilización. Los estilos, los alcances (*scopes*) y los componentes de imagen reutilizables se combinan con estructuras de nivel superior, como árboles, gráficos, mapas mentales y diseños de matrices. Le sigue el refinamiento visual, que cubre rellenos, recortes, sombreados, decoraciones de rutas, capas, superposiciones y transparencia, incluida la integración de gráficos de TikZ con el resto del documento.

Los capítulos avanzados tratan a TikZ como un motor de cálculo y geometría, mostrando cálculos de coordenadas, intersecciones, bucles, transformaciones y técnicas para dibujar curvas suaves. Las secciones finales se centran en la visualización de datos y la generación de diagramas, incluidos gráficos en 2D y 3D y enfoques basados en paquetes para crear diagramas completos, antes de concluir con ejemplos creativos de la comunidad de TikZ.

Puede encontrar más información sobre el libro en [https://tikz.org](https://tikz.org/). El libro también ha sido publicado en japonés; su sitio web es [https://tikz.jp](https://tikz.jp/).

#### The LaTeX Companion

*The LaTeX Companion*, en su tercera edición, se publica en dos volúmenes y sirve como una referencia detallada para LaTeX y su ecosistema.

El Volumen I se centra en la construcción del documento principal. Cubre la estructura del documento, el formato de texto, el diseño de página, tablas, flotantes, gráficos y selección de fuentes, explicando cómo funcionan e interactúan las funciones estándar de LaTeX y los paquetes ampliamente utilizados.

El Volumen II aborda temas avanzados y especializados. Incluye una amplia cobertura de composición tipográfica matemática, símbolos, Unicode y soporte multilingüe, bibliografías y citas, índices, personalización y aspectos seleccionados de la programación de LaTeX y el diseño de paquetes.

Este libro no es un tutorial para principiantes ni se basa en recetas; es más adecuado como referencia a largo plazo para usuarios experimentados de LaTeX que desean explicaciones detalladas y orientación autorizada.

---

### Resumen

Dimos un paso atrás respecto al uso diario de LaTeX y analizamos lo que se ejecuta debajo de nuestros documentos. Aprendió qué hacen los motores TeX, por qué existen diferentes motores y cómo los formatos TeX se basan en ellos.

También vimos cómo la IA puede respaldar el flujo de trabajo de LaTeX, ayudando con la generación de código, explicaciones de errores, resolución de problemas, refinamiento de texto y planificación, permitiéndole al mismo tiempo mantener el control.

Con los 16 capítulos completados, ahora tiene una base sólida. Cerramos viendo otros libros si desea profundizar más.
