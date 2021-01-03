 # El estándar SPICE
 **SPICE** es una abreviabiación de *Simulation Program with Integrated Circtuit Emphasis*.
 Se trata básicamente de un método estándar para describir circuitos usando texto plano en
 lugar de una representación gráfica (o *esquemática*). A esta descripción en texto se
 la llama también **netlist** y básicamente se corresponde con la *lista* de los componentes del circuito y cómo estos están conectados entre sí, es decir, de los nodos de unión.
 Los ficheros netlist pueden tener extensiones `.cir`, `.net`, `.ckt`, ó `.sp` y es muy común encontrárselos con cualquiera de estas.

 Existen en el mercado muchas variantes (intérpretes) de Spice, aunque el original fue descrito
 en la Universidad de Berkeley. En la lista de intérpretes de Spice tenemos desde esfuerzos y proyectos comerciales hasta *open source* y regidos por distintas comunidades de usuarios y programadores.

> **Pregunta:** Enumera todos los intérprete de Spice que puedas encontrar. Crea una tabla en Markdown con varias columnas (para el nombre, fabricante, versión actual, licencia y alguna característica sobresaliente). Aquí tienes un ejemplo del que puedes partir y seguir completando:

| Intérprete |  Licencia  | Fabricante                                                       | Características           |
| :--------- | :--------: | :-----------------                                               | :----------------         |
| Ahkab      |     GPL    | Giuseppe Venturini                                               | Basado en Python          |
| Ngspice    |     GPL    | Desarollado por comunidad de usuarios                            | Opensource                |
| Spice OPUS |     GPL    | Faculty of Electrical Engineering at the University of Ljubljana | Existe PyOPUS para Phyton |
| LTspice    |     GPL    | Linear Technology                                                | No es opensource          |
| PySPICE    |     GPL    | Fabrice Salvaire                                                 | Se basa en CSPICE         |



 > **Pregunta:** ¿Qué comparación puedes efectuar entre C y Spice como estándares (lenguajes) y sus respectivas implementaciones en software? ¿Qué implementaciones reales (compiladores) del lenguaje C conoces? 

La principal diferencia entre estos lenguajes es que **C** es un lenguaje con el que utilizamos compiladores con la finalidad de traducir sus líneas escritas a un ejecutable que contiene directamente ordenes que puede ejecutar el procesador, en cambio, **Spice** es un lenguaje "interpretado", es decir, precisa de intérpretes de software para poder ejecutarse.

Con **Spice** necesitamos interpretar nuestro código cada vez que queremos ejecutar el programa y con **C** podemos ejecutar el fichero ejecutable sin tener que interpretar el lenguaje.

Desde mi punto de vista, para MAC el más utilizado seria GCC y para Windows el más utilizado es C++.


 ## Unidades en SPICE

 Las unidades de las magnitudes características del circuito son siempre [unidades
 del Sistema Internacional](https://en.wikipedia.org/wiki/SI_electromagnetism_units) y no es necesario indicarlo explícitamente en el netlist.

 La forma de especificar múltiplos de estas cantidades es añadiendo una letra.
 Básicamente las que nos interesan y las que suelen aparecer mayoritariamente son `k` para "kilo-," `m` para "mili?" y `u` para "micro?".

 > **Pregunta:** Crea una tabla en Markdown con todos los prefijos de múltiplos que puedas, su abreviatura y su equivalencia numérica.

| Prefijo | Abreviatura | Equivalencia |
| :------ | :---------: | :----------- |
| exa     |      E      | $10^{18}$    |
| peta    |      P      | $10^{15}$    |
| tera    |      T      | $10^{12}$    |
| giga    |      G      | $10^{9}$     |
| mega    |      Z      | $10^{6}$     |
| kilo    |      k      | $10^{3}$     |
| hecto   |      h      | $10^{2}$     |
| deca    |      da     | $10^{1}$     |
| -       |      -      | $10^{0}$     |
| deci    |      d      | $10^{-1}$    |
| centi   |      c      | $10^{-2}$    |
| mili    |      m      | $10^{-3}$    |
| micro   |     $µ$     | $10^{-6}$    |
| nano    |      n      | $10^{-9}$    |
| pico    |      p      | $10^{-12}$   |
| femto   |      f      | $10^{-15}$   |
| atto    |      a      | $10^{-18}$   |


 > **Pregunta**: ¿qué unidades del Sistema Internacional relacionadas con la asignatura –y los circuitos en general– conoces? Responde aquí mismo en una celda de Markdown con una tabla.

| Unidad    | Símbolo | Magnitud                          |
| :-        | :-----: | :-                                |
| Amperio   | A       | Intensidad de corriente eléctrica |
| Voltio    | V       | Potencial eléctrico               |
| Ohmio     | Ω       | Resistencia eléctrica             |
| Faradio   | F       | Carga del condensador             |
| Henrio    | H       | Inductancia eléctrica             |
| Hercio    | Hz      | Frecuencia                        |
| Vatio     | W       | Potencia eléctrica                |
| Culombio  | C       | Carga eléctrica                   |
| Julio     | J       | Energía                           |
| kilogramo | kg      | Masa                              |
| Metro     | m       | Longitud                          |
| Segundo   | s       | Tiempo                            |



  ## Comandos SPICE para circuitos en corriente continua

  > **Pregunta**: Hasta lo que has visto del lenguaje Spice, ¿dentro de qué tipo o conjunto de lenguajes encajaría? ¿Funcionales? ¿Específicos de dominio? ¿Procedurales? ¿Estructurados? ¿Orientado a Objetos ¿Funcionales? Justifica tu respuesta. 

Es un lenguaje específico de dominio ya que, es un lenguaje de programación dedicado a resolver un problema en particular, en este caso, ha sido creado con el objetivo concreto de facilitar la codificación e investigación de circuitos eléctricos realizando simulaciones.

 > **Pregunta**: El parámetro `uic` puede tener varios valores y cada uno significa una cosa. Detállalo usando un celda Markdown y consultando la [documentación de Ahkab](https://buildmedia.readthedocs.org/media/pdf/ahkab/latest/ahkab.pdf).

UIC (Use Initial Conditions): Este parametro se utiliza para especificar el estado del tiempo del circuito. Si no usamos este parametro el analisis se realizara desde el punto estable del circuito, pero muchas veces necesitamos analizar el funcionamiento del circuito en el tiempo, por ejemplo, la carga de un condensador, el incremento de temperatura de un resistivo...

Los valores disponibles son 0, 1, 2 o 3.

• uic = 0: se supondrá que todos los voltajes y corrientes de los nodos a través de las fuentes v / h / e / son cero en t = tstart.

• uic = 1: el estado en 't = tstart es el último resultado de un análisis OP.

• uic = 2: el estado en t = tstart es el último resultado de un análisis OP en el que se establecen los valores de corrientes a través de inductores y voltajes en condensadores especificados en su ic. Esto se hace de manera muy aproximada, se recomienda verificar.

• uic = 3: carga un ic proporcionado por el usuario. Esto requiere una directiva .ic en algún lugar de la lista de conexiones y un nombre .ic y ic_label deben coincidir.


 ## Intérprete SPICE que vamos a usar: Ahkab
 Tras un estándar siempre hay una o varias implementaciones. Ahkab no deja de ser una implmentación más en Python del estándar Spice.
 
 > **Pregunta:** Comenta las distintas implementaciones de lenguajes y estándares que conozcas. Hazlo usando una tabla en Markdown. [Aquí](https://www.markdownguide.org/extended-syntax/#tables) tienes un poco de ayuda (aunque antes ya se ha puesto el ejemplo de una tabla).
 
| Intérprete |  Licencia  | Fabricante                                                       | Características           |
| :--------- | :--------: | :-----------------                                               | :----------------         |
| Ahkab      |     GPL    | Giuseppe Venturini                                               | Basado en Python          |
| Ngspice    |     GPL    | Desarollado por la comunidad de usuarios                         | Opensource                |
| Spice OPUS |     GPL    | Faculty of Electrical Engineering at the University of Ljubljana | Existe PyOPUS para Phyton |
| LTspice    |     GPL    | Linear Technology                                                | No es opensource          |
| PySPICE    |     GPL    | Fabrice Salvaire                                                 | Se basa en CSPICE         |

 
 > **Pregunta:** Describe brevemente este software (creador, objetivos, versiones, licencia, características principales, dependencias, etc.).

Ahkab es un simulador de circuitos eléctricos implementado en python, su creador fue Giuseppe Venturini fallecido en el 2015, actualmente esta en la versión 0.18 lanzada el 12 de julio de 2015.

Nació con el proposito de simplificar la codificación y simulación de circuitos de forma parecida a Spice.

Dependencias: Python 3, Numpy, Scipy, Sympy, Tabulate. Para la graficacion es recomendable Matplotlib y Nose como suite de pruebas.

 # Trabajo práctico
 Ahora vamos a definir circuitos y ejecutar simulaciones sobre los mismos gracias a Ahkab.

 ## Instalación de bibliotecas necesarias

Podemos instalar Ahkab directamente desde este mismo notebook:


```python
!pip install ahkab
```

Como vamos a pintar algunas gráficas, necesitamos instlar [matplotlib](https://matplotlib.org). Al igual que con Ahkab, esto lo podemos hacer directamente desde este mismo notebook. Si hemos usado Anaconda: 


```python
!conda install -y -c conda-forge matplotlib
```


```python
#Importamos las librerias de matplotlib como plt.
import pylab as plt
import ahkab
```

    W: Locale appears not set! please export LANG="en_US.UTF-8" or equivalent, 
    W: or ahkab's unicode support is broken.


 > **Pregunta:** ¿Qué es y para qué sirve PyLab?

PyLab forma parte de la suite Matplotlib, es una API que nos permite dibujar gráficas y trabajar con arrays de una forma parecida a la de MatLab.


 ## Circuitos sencillos para trabajar con la ley de Ohm:

 La *mal llamada* ley de Ohm reza que el voltaje (la *energía por unidad de carga*) que se disipa en un tramo de un circuito eléctrico es equivalente a la intensidad ($I$) de la corriente (es decir, cuántos electrones circulan por unidad de tiempo) por la resistencia del material ($R$) en el que está desplazándose dicha corriente. Matemáticamente:

 $$
 V = I\cdot R
 $$

 > **Pregunta:** comprueba que la ecuación anterior está ajustada a nivel dimensional, es decir, que la naturaleza de lo que está a ambos lados del signo igual es la misma. Realiza este ejercicio con LaTeX en una celda Markdown.

* $ \large V = I \cdot R \rightarrow V = \frac {W}{Q} \rightarrow [V] = \frac {[W]}{[Q]} = \frac {[F] \cdot [d]}{I \cdot T} = \frac {[m] \cdot [a] \cdot [d]}{I \cdot T} = \frac {M \cdot L \cdot T^{-2} \cdot L}{I \cdot T} = M \cdot L^2 \cdot T^{-3} \cdot I^{-1} $

* $ \large [I] = I $

* $ \large R = \frac {V}{I} \rightarrow [R] = \frac {[V]}{[I]} \rightarrow R = \frac {M \cdot L^2 \cdot T^{-3} \cdot I^{-1}}{I} = M \cdot L^2 \cdot T^{-3} \cdot I^{-2} $

Si lo juntamos todo podemos observar que las dimensines son iguales a ambos lados de la ecuación:

* $ M \cdot L^2 \cdot T^{-3} \cdot I^{-1} = I \cdot M \cdot L^2 \cdot T^{-3} \cdot I^{-1}$

* $ M \cdot L^2 \cdot T^{-3} \cdot I^{-1} = M \cdot L^2 \cdot T^{-3} \cdot I^{-1}$

Video explicativo del [Análisis Dimensional](https://www.youtube.com/watch?v=933pHbCkTrw) de la ley de Ohm.

 Comencemos con el circuito más sencillo posible de todos:

 ![](https://raw.githubusercontent.com/JMPinillos/CIRCUITOS_ELECTRICOS/main/primer%20circuito.svg?sanitize=true)

 Vamos a escribir su contenido (componentes o *netlist*) en disco con el nombre `circuito sencillo.sp`. Esto lo podemos lograr directamente y en tiempo real desde una celda de Jupyter gracias a los *comandos mágicos* de este entorno de programación literaria. En concreto vamos a utilizar `%%writefile` que guarda los contenidos de una celda como un fichero. 


```python
%%writefile "circuito sencillo.sp"
* Este es un circuito sencillo
r1 1 0 100
v1 0 1 type=vdc vdc=9
.op
.dc v1 start=0 stop=9 step=1
.end

```

    Overwriting circuito sencillo.sp


Leemos su descripción con Ahkab, interpretar y ejecutar las simulaciones que en él estén descritas.


```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit('circuito sencillo.sp')
```

 Separamos la información del netlist (componentes) de los análisis (uno de tipo `op` y otro de tipo `dc`):


```python
circuito = circuito_y_análisis[0]
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
print(lista_de_análisis)

```

    [{'type': 'op', 'guess': True, 'x0': None}, {'type': 'dc', 'source': 'v1', 'start': 0.0, 'stop': 9.0, 'step': 1.0, 'sweep_type': 'LIN'}]


> **Pregunta:** ¿qué tipo de estructura de Python es `lista_de_análisis`?

Es una estructura de datos tipo lista.

 Las simulaciones que implican listas de datos (`.dc`, `.tran`, etc.) necesitan de un fichero temporal (`outfile`)
 donde almacenar los resultados. Para ello tenemos que definir la propiedad `outfile`.


```python
lista_de_análisis[1]['outfile'] = "simulación dc.tsv"

```

 > **Pregunta:** escribe el código Python necesario para identificar qué análisis de `lista_de_análisis`
 son de tipo `dc` ó `tran` y sólo añadir la propiedad `outfile` en estos casos.
Aquí tenéis un post de Stackoverflow con algo de [ayuda](https://stackoverflow.com/questions/49194107/how-to-find-index-of-a-dictionary-key-value-within-a-list-python).
 Un poco más de ayuda: el siguiente código (sí, una única línea) devuelve el índice de la simulación que es de tipo `dc`. Para simplificar un poco el ejercicio, suponed que, como máximo, habrá un análisis de tipo `tran` y/o `dc`.


```python
lista_de_análisis[[i for i, d in enumerate(lista_de_análisis) if "dc" in d.values() or "tran" in d.values()] [0]]['outfile'] = "simulación dc.tsv"
```

Una vez que ya hemos separado netlists de simulaciones, ejecutamos las segundas (¡todas a la vez!) gracias al método `.run` de Ahkab: 


```python
resultados = ahkab.run(circuito, lista_de_análisis)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)
    Starting DC analysis:
    Solving...  done


### Resultados de la simulación `.dc`
Imprimimos información sobre la simulación de tipo `.dc`:


```python
print(resultados['dc'])
```

    <DC simulation results for '* este es un circuito sencillo' (netlist circuito sencillo.sp). LIN sweep of V1 from 0 to 9 V. Run on 2021-01-03 13:11:38, data file simulación dc.tsv>


 Veamos qué variables podemos dibujar para el caso del análisis `dc`.


```python
print(resultados['dc'].keys())
```

    ['V1', 'V1', 'I(V1)']


Y ahora graficamos el resultado del análisis anterior. Concretamente vamos a representar el voltaje en el borne 1 (`V1`) con respecto a la intensidad del circuito (`I(V1)`).


```python
figura = plt.figure()
plt.title("Prueba DC")
plt.plot(resultados['dc']['V1'], resultados['dc']['I(V1)'], label="Voltaje (V1)")
plt.xlabel("Voltaje (V)")
plt.ylabel("Intensidad (A)")
plt.legend()
```




    <matplotlib.legend.Legend at 0x11f419b80>




    
![svg](output_23_1.svg)
    


> **Pregunta:** comenta la gráfica anterior… ¿qué estamos viendo exactamente? Etiqueta los ejes de la misma convenientemente. Así como ningún número puede *viajar* solo sin hacer referencia a su naturaleza, ninguna gráfica puede estar sin sus ejes convenientemente etiquetados. Algo de [ayuda](https://matplotlib.org/3.1.0/gallery/pyplots/fig_axes_labels_simple.html). ¿Qué biblioteca estamos usando para graficar? Una [pista](https://matplotlib.org).

Usando matplotlib graficamos los resultados del circuito simple con corriente continua.

La gráfica nos muestra como varía la Intensidad en el circuito a medida que aumenta el Voltaje de la pila.

Si usamos la ley de Ohm, conociendo el valor constante de la resistencia (100Ω) y modificando el voltaje de 0V hasta 9V de un en un Voltio:

$ \large I = \frac  {V}{R} $

| Voltaje | Resistencia | Intensidad |
|   :-:   |     :-:     |     :-:    |
|   0V    |     100Ω    |    0,00A   |
|   1V    |     100Ω    |    0,01A   |
|   2V    |     100Ω    |    0,02A   |
|   3V    |     100Ω    |    0,03A   |
|   4V    |     100Ω    |    0,04A   |
|   5V    |     100Ω    |    0,05A   |
|   6V    |     100Ω    |    0,06A   |
|   7V    |     100Ω    |    0,07A   |
|   8V    |     100Ω    |    0,08A   |
|   9V    |     100Ω    |    0,09A   |

 ### Resultados de la simulación `.op` 
 El método `.results` nos devuelve un diccionario con los resultados de la simulación.


```python
print(resultados['op'].results)
```

    {V1: -9.0, I(V1): -0.09}


 > **Pregunta:** justifica el sencillo resultado anterior (análisis `op`).

 El resultado anterio viene de aplicar la ley de Ohm como para hayar la intensidad del circuito:

 $ \large I = \frac  {V}{R} = \frac  {9V}{100Ω} = 0,09A$

Ahora vamos a resolver el cálculo con Sympy.


```python
from sympy import solve, symbols, Eq 
from sympy.physics.units.systems import SI
from sympy.physics import units as u

V = 9 * u.volts
R = 100 * u.ohms
I = u.Quantity('I')
I.set_dimension(u.current)
ley_ohm = Eq(V, I * R)
solucion = solve(ley_ohm, I)
print (u.convert_to(solucion[0], [u.amperes]).n(2))
```

    0.09*ampere


## Resolución del mismo circuito pero con LTspice
Ahora importamos el "lts" según el Sistema Operativo que estamos utilizando.


```python
import platform
%alias lts /Applications/LTspice.app/Contents/MacOS/LTspice -ascii -b
if platform.system() == "Windows":
    %alias lts "C:\Program Files\LTC\LTspiceXVII\XVIIx64.exe" -ascii -b
```

**Pregunta**: ¿Qué significan las opciones `-b` y `-ascii`? Algo de ayuda [aquí](http://ltwiki.org/LTspiceHelp/LTspiceHelp/Command_Line_Switches.htm).

"-b" ejecuta en modo por lotes y deja los archivos en ".raw"

"-ascii" utiliza los archivos ".raw" y reduce significativamente el rendimiento del programa.

También tenemos que cambiar ligeramente la sintaxis. Para LTspice, vamos a reservar la extensión `.net`:


```python
%%writefile "circuito sencillo.net"
* Este es un circuito sencillo adaptado para LTspice
r1 1 0 100
v1 0 1 9
.op
* Comentamos el análisis .dc para centrarnos primero en el .op
* .dc v1 1 10 
.end
```

    Overwriting circuito sencillo.net


Ejecutamos LTspice con el circuito (de la misma manera que antes habíamos hecho con Ahkab).


```python
lts "circuito sencillo.net"
```

Vemos el contenido de la simulación.


```python
%pycat circuito sencillo.log
```

    [0mC[0m[0;31m [0m[0mi[0m[0;31m [0m[0mr[0m[0;31m [0m[0mc[0m[0;31m [0m[0mu[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m*[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mE[0m[0;31m [0m[0ms[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0;31m [0m[0;31m [0m[0me[0m[0;31m [0m[0ms[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mu[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mc[0m[0;31m [0m[0mi[0m[0;31m [0m[0mr[0m[0;31m [0m[0mc[0m[0;31m [0m[0mu[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0mo[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0me[0m[0;31m [0m[0mn[0m[0;31m [0m[0mc[0m[0;31m [0m[0mi[0m[0;31m [0m[0ml[0m[0;31m [0m[0ml[0m[0;31m [0m[0mo[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ma[0m[0;31m [0m[0md[0m[0;31m [0m[0ma[0m[0;31m [0m[0mp[0m[0;31m [0m[0mt[0m[0;31m [0m[0ma[0m[0;31m [0m[0md[0m[0;31m [0m[0mo[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mp[0m[0;31m [0m[0ma[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mL[0m[0;31m [0m[0mT[0m[0;31m [0m[0ms[0m[0;31m [0m[0mp[0m[0;31m [0m[0mi[0m[0;31m [0m[0mc[0m[0;31m [0m[0me[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mD[0m[0;31m [0m[0mi[0m[0;31m [0m[0mr[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mN[0m[0;31m [0m[0me[0m[0;31m [0m[0mw[0m[0;31m [0m[0mt[0m[0;31m [0m[0mo[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mo[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mf[0m[0;31m [0m[0mo[0m[0;31m [0m[0mr[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m.[0m[0;31m [0m[0mo[0m[0;31m [0m[0mp[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mp[0m[0;31m [0m[0mo[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0mu[0m[0;31m [0m[0mc[0m[0;31m [0m[0mc[0m[0;31m [0m[0me[0m[0;31m [0m[0me[0m[0;31m [0m[0md[0m[0;31m [0m[0me[0m[0;31m [0m[0md[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mO[0m[0;31m [0m[0mp[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0mg[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mB[0m[0;31m [0m[0mi[0m[0;31m [0m[0ma[0m[0;31m [0m[0ms[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mP[0m[0;31m [0m[0mo[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mS[0m[0;31m [0m[0mo[0m[0;31m [0m[0ml[0m[0;31m [0m[0mu[0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mo[0m[0;31m [0m[0mn[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mV[0m[0;31m [0m[0;34m([0m[0;31m [0m[0;34m)[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m-[0m[0;31m [0m[0;36m9[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0mv[0m[0;31m [0m[0mo[0m[0;31m [0m[0ml[0m[0;31m [0m[0mt[0m[0;31m [0m[0ma[0m[0;31m [0m[0mg[0m[0;31m [0m[0me[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mI[0m[0;31m [0m[0;34m([0m[0;31m [0m[0mR[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m)[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m-[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;36m9[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0md[0m[0;31m [0m[0me[0m[0;31m [0m[0mv[0m[0;31m [0m[0mi[0m[0;31m [0m[0mc[0m[0;31m [0m[0me[0m[0;31m [0m[0m_[0m[0;31m [0m[0mc[0m[0;31m [0m[0mu[0m[0;31m [0m[0mr[0m[0;31m [0m[0mr[0m[0;31m [0m[0me[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mI[0m[0;31m [0m[0;34m([0m[0;31m [0m[0mV[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m)[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m-[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;36m9[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0md[0m[0;31m [0m[0me[0m[0;31m [0m[0mv[0m[0;31m [0m[0mi[0m[0;31m [0m[0mc[0m[0;31m [0m[0me[0m[0;31m [0m[0m_[0m[0;31m [0m[0mc[0m[0;31m [0m[0mu[0m[0;31m [0m[0mr[0m[0;31m [0m[0mr[0m[0;31m [0m[0me[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mD[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mS[0m[0;31m [0m[0mu[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mJ[0m[0;31m [0m[0ma[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;36m4[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mT[0m[0;31m [0m[0mo[0m[0;31m [0m[0mt[0m[0;31m [0m[0ma[0m[0;31m [0m[0ml[0m[0;31m [0m[0;31m [0m[0;31m [0m[0me[0m[0;31m [0m[0ml[0m[0;31m [0m[0ma[0m[0;31m [0m[0mp[0m[0;31m [0m[0ms[0m[0;31m [0m[0me[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mm[0m[0;31m [0m[0me[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mo[0m[0;31m [0m[0mn[0m[0;31m [0m[0md[0m[0;31m [0m[0ms[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mn[0m[0;31m [0m[0mo[0m[0;31m [0m[0mm[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m7[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mm[0m[0;31m [0m[0mp[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m7[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mm[0m[0;31m [0m[0me[0m[0;31m [0m[0mt[0m[0;31m [0m[0mh[0m[0;31m [0m[0mo[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mp[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mo[0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mn[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mn[0m[0;31m [0m[0mp[0m[0;31m [0m[0mo[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0ms[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0ma[0m[0;31m [0m[0mc[0m[0;31m [0m[0mc[0m[0;31m [0m[0me[0m[0;31m [0m[0mp[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mr[0m[0;31m [0m[0me[0m[0;31m [0m[0mj[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mm[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0mi[0m[0;31m [0m[0mx[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0mi[0m[0;31m [0m[0mz[0m[0;31m [0m[0me[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mf[0m[0;31m [0m[0mi[0m[0;31m [0m[0ml[0m[0;31m [0m[0ml[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0ms[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0ms[0m[0;31m [0m[0mo[0m[0;31m [0m[0ml[0m[0;31m [0m[0mv[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mN[0m[0;31m [0m[0mo[0m[0;31m [0m[0mr[0m[0;31m [0m[0mm[0m[0;31m [0m[0ma[0m[0;31m [0m[0ml[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mM[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0mi[0m[0;31m [0m[0mx[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mC[0m[0;31m [0m[0mo[0m[0;31m [0m[0mm[0m[0;31m [0m[0mp[0m[0;31m [0m[0mi[0m[0;31m [0m[0ml[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;36m6[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mo[0m[0;31m [0m[0mb[0m[0;31m [0m[0mj[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mc[0m[0;31m [0m[0mo[0m[0;31m [0m[0md[0m[0;31m [0m[0me[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0mi[0m[0;31m [0m[0mz[0m[0;31m [0m[0me[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mM[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0mi[0m[0;31m [0m[0mx[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mC[0m[0;31m [0m[0mo[0m[0;31m [0m[0mm[0m[0;31m [0m[0mp[0m[0;31m [0m[0mi[0m[0;31m [0m[0ml[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m9[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mo[0m[0;31m [0m[0mp[0m[0;31m [0m[0mc[0m[0;31m [0m[0mo[0m[0;31m [0m[0md[0m[0;31m [0m[0me[0m[0;31m [0m[0ms[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m[0;34m[0m[0m


Ahora repetimos lo mismo para el análisis `.dc`:


```python
%%writefile "circuito sencillo.net"
* Este es un circuito sencillo adaptado para LTspice
r1 1 0 100
v1 0 1 9
* Ahora obviamos el análisis .op
* .op
.dc v1 1 10 
.end

```

    Overwriting circuito sencillo.net



```python
lts "circuito sencillo.net"
```

Al ejecutar esta simulación, se genera un fichero `.raw` con los resultados. Es muy parecido al `outfile` que hemos empleado antes con Ahkab. Para leer este fichero, tenemos que usar el paquete [ltspice de Python](https://github.com/DongHoonPark/ltspice_pytool), el cual podéis instalar directamente desde Jupyter o desde el propio notebook:


```python
!pip install ltspice
```

Dibujamos la gráfica con los datos obtenidos.


```python
import ltspice
l = ltspice.Ltspice("circuito sencillo.raw")
l.parse()
time = l.get_time()
V1 = l.get_data('V(1)')
plt.title("Interpretación gráfica dc circuito sencillo con CC")
plt.plot(time, V1, label="Voltaje (V1)")
plt.ylabel("Voltaje (V)")
plt.xlabel("Tiempo (s)")
plt.legend()
```




    <matplotlib.legend.Legend at 0x11f990d90>




    
![svg](output_45_1.svg)
    


** En resumen: ** hemos usado dos *compiladores* Spice distintos para hacer el mismo ejercicio. De igual manera podríamos haber usado [Ngspice](http://ngspice.sourceforge.net) u otro. De hecho, podíamos haber usado Ahkab en modo comando. Si tenemos correctamente instalado este framework, en princpio podemos invocarlo [directamente desde línea de comandos](https://ahkab.readthedocs.io/en/latest/help/Command-Line-Help.html):


```python
!ahkab "circuito sencillo.sp"
```

    W: Locale appears not set! please export LANG="en_US.UTF-8" or equivalent, 
    W: or ahkab's unicode support is broken.
    2021-01-03 13:15:22
    ahkab v. 0.18 (c) 2006-2015 Giuseppe Venturini
    
    Operating Point (OP) analysis
    
    Netlist: circuito sencillo.sp
    Title: * este es un circuito sencillo
    At 300.00 K
    Options:
    	vea = 1.000000e-06
    	ver = 0.001000
    	iea = 1.000000e-09
    	ier = 0.001000
    	gmin = 0.000000e+00
    
    Convergence reached in 2 iterations.
    
    ========
    RESULTS:
    ========
    
    Variable    Units      Value        Error    %
    ----------  -------  -------  -----------  ---
    V1          V          -9     9.00001e-12    0
    I(V1)       A          -0.09  0              0
    
    ========================
    ELEMENTS OP INFORMATION:
    ========================
    
    Part ID      R [Ω]    V(n1,n2) [V]    I(n1->n2) [A]    P [W]
    ---------  -------  --------------  ---------------  -------
    R1             100              -9            -0.09     0.81
    
    Part ID      V(n1,n2) [V]    I(n1->n2) [A]    P [W]
    ---------  --------------  ---------------  -------
    V1                      9            -0.09    -0.81
    
    Total power dissipation: 0.81 W
    
    #V1	V1	I(V1)
    0.000000000000000000e+00	0.000000000000000000e+00	0.000000000000000000e+00
    1.000000000000000000e+00	-1.000000000000000000e+00	-1.000000000000000021e-02
    2.000000000000000000e+00	-2.000000000000000000e+00	-2.000000000000000042e-02
    3.000000000000000000e+00	-3.000000000000000000e+00	-2.999999999999999889e-02
    4.000000000000000000e+00	-4.000000000000000000e+00	-4.000000000000000083e-02
    5.000000000000000000e+00	-5.000000000000000000e+00	-5.000000000000000278e-02
    6.000000000000000000e+00	-6.000000000000000000e+00	-5.999999999999999778e-02
    7.000000000000000000e+00	-7.000000000000000000e+00	-7.000000000000000666e-02
    8.000000000000000000e+00	-8.000000000000000000e+00	-8.000000000000000167e-02
    9.000000000000000000e+00	-9.000000000000000000e+00	-8.999999999999999667e-02


**Ejercicio premium**: Graficar los datos anteriores con [Gnuplot](http://www.gnuplot.info). 


```python
!brew install gnuplot # Comentar en WINDOWS esta linea.
!pip install gnuplot_kernel
%load_ext gnuplot_kernel
!pip install pandas
```


```python
#Guardamos los datos con Numpy y evitamos declarar un subproceso en Python 
import pandas as pd

data = pd.DataFrame({'time': time,'v1': V1})
data['v1'] = data['v1'] * -1
data.to_csv("data.csv", sep=';' ,index = False)
```


```python
%%gnuplot
reset session
set title 'Interpretación gráfica dc circuito sencillo con CC'
set xlabel 'time (s)'
set ylabel 'Voltaje (V)'
set datafile separator ';'
set grid
plot "data.csv" using 2:1 notitle with linespoints 
```


    
![png](output_51_0.png)
    


    Warning: The prompt is currently set to '2004hgnuplot> '



    [?2004l
    [?[?2004l
    [?[?2004l
    [?[?2004l
    [?[?2004l
    [?[?2004l
    [?[?2004l
    [?[?2004l
    [?[?2004l
    [?


 ## Análisis de circuito con resistencias en serie

Vamos a resolver (en punto de operación) el siguiente circuito:

![](https://raw.githubusercontent.com/JMPinillos/CIRCUITOS_ELECTRICOS/main/resistencias%20en%20serie.svg?sanitize=true)

Grabamos el netlist en disco.


```python
%%writefile "resistencias en serie.net"
* circuito con tres resistencias en serie
v1 1 0 type=vdc vdc=9
R1 1 2 3k
R2 2 3 10k  
R3 3 0 5k
* análisis del circuito
.op
.end
```

    Writing resistencias en serie.net



```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit('resistencias en serie.net')
circuito = circuito_y_análisis[0]       
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
resultados = ahkab.run(circuito, lista_de_análisis)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)


Imprimos los resultados del análisis `.op`:


```python
print(resultados['op'])
```

    OP simulation results for '* circuito con tres resistencias en serie'(netlist resistencias en serie.net).
    Run on 2021-01-03 13:16:40, data file None.
    Variable    Units      Value     Error    %
    ----------  -------  -------  --------  ---
    V1          V         9       -9e-12      0
    V2          V         7.5     -7.5e-12    0
    V3          V         2.5     -2.5e-12    0
    I(V1)       A        -0.0005   0          0


Los cantidades `V1`, `V2` y `V3` hacen referencia a los distintos valores del potencial que se ha perdido en cada uno de los bornes que has elegido para describir el netlist (`1`, `2`, etc.). Por ejemplo, podemos calcular el *potencial consumido* por la resistencia `R1` y verás que coincide con el del punto `V2` devuelto por Ahkab.

**Ejercicio**: compruébalo tú mismo y refléjalo por escrito.

$ VT = 9V $

$ RT = R_{1} + R_{2} + R_{3} = 3K\Omega + 10K\Omega + 5K\Omega = 18K\Omega = 18000\Omega $

$ IT = I_{1} = I_{2} = I_{3} = \frac{9V}{18000\Omega} = 0,0005A $

$ V_{1} = I_{1} \cdot R_{1} = 0,0005A \cdot 3000\Omega = 1,5V $

$ V_{2} = I_{2} \cdot R_{2} = 0,0005A \cdot 10000\Omega = 5V $

$ V_{3} = I_{3} \cdot R_{3} = 0,0005A \cdot 5000\Omega = 2,5V $

Si comparamos nuestros resultados con los obtenidos por el programa no coincide porque nosotros calculamos los potenciales de cada resistencia y el programa obtiene los potenciales entre distintos nodos, los cuales serían los siguientes:

$ V_{Nodo(0,1)} = I_{Nodo(0,1)} \cdot R_{3} = 0,0005A \cdot 5000\Omega = 2,5V $

$ V_{Nodo(0,2)} = I_{Nodo(0,2)} \cdot (R_{3} + R_{2}) = 0,0005A \cdot (5000\Omega + 10000\Omega) = 7,5V $

$ V_{Nodo(0,3)} = I_{Nodo(0,3)} \cdot (R_{3} + R_{2} + R_{1}) = 0,0005A \cdot (5000\Omega + 10000\Omega + 3000\Omega) = 9V $

Cargamos primero todo lo relacionado con Sympy:


```python
from sympy.physics.units import ohms, amperes, volts
from sympy.physics.units import convert_to
```


```python
r1 = 3E3*ohms
intensidad_ahkab = resultados['op']['I(V1)'][0][0]*amperes
v2 = convert_to(intensidad_ahkab*r1, [volts])
v2
```




$\displaystyle - 1.5 \text{V}$



 > **Pregunta**: reproduce el resto de los valores anteriores de manera *manual* mediante Sympy (es decir, aplicando la ley de Ohm, pero con un *toque computacional*). Te pongo aquí un ejemplo del que puedes partir… En él sólo calculo la corriente que circula por el circuito (sí, justo la que antes Ahkab ha devuelto de manera automática). Para ello necesito previamente computar la resistencia total (`r_total`). Faltarían el resto de resultados y convertirlos a unidades más *vistosas* (mediante la orden `convert_to` y `.n()`).


```python
from sympy.physics.units import kilo
from sympy import solve, symbols, Eq
from sympy.physics import units as u

v1 = 9*volts
r1 = 3*kilo*ohms
r2 = 10*kilo*ohms
r3 = 5*kilo*ohms
r_total = r1 + r2 + r3
intensidad = symbols('i')
ley_ohm = Eq(v1, intensidad*r_total)
solucion_para_intensidad = solve(ley_ohm, intensidad)
IT = convert_to(solucion_para_intensidad[0], [amperes]).n(2)
print(convert_to(solucion_para_intensidad[0], [u.ampere]).n(2))
print(convert_to(solve(Eq(v1, IT*r1), v1)[0], [volts]).n(2))
print(convert_to(solve(Eq(v1, IT*r2), v1)[0], [volts]).n(2))
print(convert_to(solve(Eq(v1, IT*r3), v1)[0], [volts]).n(2))
```

    0.0005*ampere
    1.5*volt
    5.0*volt
    2.5*volt


> **Pregunta**: Demuestra que se cumple la Ley de Kirchhoff de la energía en un circuito, es decir, que la suma de la energía suministrada por las fuentes (pilas) es igual a la consumida por las resistencias. Realiza la operación con Sympy.

Como podemos observar, las leyes de Krichoff se cumplen, ya que las tensiones de entrada del circuito (pila de 9 Voltios) es igual a la suma de la caida de tensión en cada una de las resistencias del circuito.

$ V_{r1} + V_{r2} + V_{r3} = V_{total} \rightarrow 1,5V + 5V + 2,5V = 9V $



$$
\sum_i^N V_{\text{fuentes}} = \sum_j^M V_{\text{consumido en resistencias}}
$$

## Análisis `.op` de circuitos con resistencias en paralelo

Ahora vamos añadiendo elementos en paralelo.

 > **Pregunta**: realiza los análisis `.op` de los siguientes circuitos.
 Para ello crea un netlist separado para cada uno donde queden correctamente descritos
 junto con la simulación (`.op`). Comenta los resultados que devuelve Ahkab (no imprimas los resultados de las simulaciones *sin más*).

 ![](https://raw.githubusercontent.com/JMPinillos/CIRCUITOS_ELECTRICOS/main/resistencias%20en%20paralelo.svg?resize=true)


```python
%%writefile "resistencias en paralelo 1.cir"
* resistencias en paralelo
vdd 1 0 vdc=12 type=vdc
r2 1 2 1k
r3 2 3 220
r4 3 0 1.5k
r5 2 0 470
.op
.end
```

    Writing resistencias en paralelo 1.cir



```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit('resistencias en paralelo 1.cir')
circuito = circuito_y_análisis[0]       
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
resultados = ahkab.run(circuito, lista_de_análisis)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)


Imprimimos los resultados del análisis .op.

Ahkab sólo reporta la intensidad de corriente en las ramas en las que hay una pila (en este caso, la rama donde está la pila VDD).


```python
print(resultados['op'])
```

    OP simulation results for '* resistencias en paralelo'(netlist resistencias en paralelo 1.cir).
    Run on 2021-01-03 13:17:20, data file None.
    Variable    Units          Value         Error    %
    ----------  -------  -----------  ------------  ---
    V1          V        12           -1.2e-11        0
    V2          V         3.23533     -3.23533e-12    0
    V3          V         2.8215      -2.82151e-12    0
    I(VDD)      A        -0.00876467   0              0


Realizamos los calculos con Sympy y los mostramos en pantalla.


```python
# CIRCUITO PARALELO 1

from sympy.physics.units import kilo, volts, ohms, convert_to
from sympy import solve, symbols, Eq
from sympy.physics import units as u

v1 = 12*volts
r1 = 1*kilo*ohms
r2 = 470*ohms
r3 = 220*ohms
r4 = 1000*ohms

r3_4 = r3 + r4
r2_3_4 =  (r2 * r3_4) / (r2 + r3_4)
r_total = r1 + r2_3_4

intensidad = symbols('i')
ley_ohm = Eq(v1, intensidad*r_total)
solucion_para_intensidad = solve(ley_ohm, intensidad)

print ("R1 =",(convert_to(r1, [u.ohms]).n(4)))
print ("R2 =",(convert_to(r2, [u.ohms]).n(4)))
print ("R3 =",(convert_to(r3, [u.ohms]).n(4)))
print ("R4 =",(convert_to(r4, [u.ohms]).n(4)))
print ("R3 + R4 =",(convert_to(r3_4, [u.ohms]).n(4)))
print ("R2 + R3 + R4 =",(convert_to(r2_3_4, [u.ohms]).n(4)))

print ("\nV_R1 =",(convert_to(solucion_para_intensidad[0] * r1, [u.volts]).n(2)))
print ("V_R2 =",(convert_to(solucion_para_intensidad[0] * r2_3_4, [u.volts]).n(2)))
print ("V_R3 =",(convert_to(solucion_para_intensidad[0] * r2_3_4 / r3_4 * r3, [u.volts]).n(2)))
print ("V_R4 =",(convert_to(solucion_para_intensidad[0] * r2_3_4 / r3_4 * r4, [u.volts]).n(2)))

print ("\nI_R1 =",(convert_to(solucion_para_intensidad[0], [u.amperes]).n(2)))
print ("I_R2 =",(convert_to(solucion_para_intensidad[0] * r2_3_4 / r2, [u.amperes]).n(2)))
print ("I_R3 =",(convert_to(solucion_para_intensidad[0] * r2_3_4 / r3_4, [u.amperes]).n(2)))
print ("I_R4 =",(convert_to(solucion_para_intensidad[0] * r2_3_4 / r3_4, [u.amperes]).n(2)))

print ("\nTension Total =", v1 )
print ("Resistencia Total =",(convert_to(r_total, [u.ohms]).n(6)))
print ("Intensidad Total =",(convert_to(solucion_para_intensidad[0], [u.amperes]).n(2)))
```

    R1 = 1000.0*ohm
    R2 = 470.0*ohm
    R3 = 220.0*ohm
    R4 = 1000.0*ohm
    R3 + R4 = 1220.0*ohm
    R2 + R3 + R4 = 339.3*ohm
    
    V_R1 = 9.0*volt
    V_R2 = 3.0*volt
    V_R3 = 0.55*volt
    V_R4 = 2.5*volt
    
    I_R1 = 0.009*ampere
    I_R2 = 0.0065*ampere
    I_R3 = 0.0025*ampere
    I_R4 = 0.0025*ampere
    
    Tension Total = 12*volt
    Resistencia Total = 1339.29*ohm
    Intensidad Total = 0.009*ampere


Ahora seguiremos analizando el resto de circuitos, pero antes de nada vamos a dibujar los nodos de cada uno de los circuitos. Esto nos servirá de gran ayuda para poder introducir los datos correctamente y más rapidamente, además de para entender las conexiones de nuestros elementos del circuito.

![](https://raw.githubusercontent.com/JMPinillos/CIRCUITOS_ELECTRICOS/main/resistencias%20en%20paralelo%20con%20nodos.svg?resize=true)


```python
%%writefile "resistencias en paralelo 2.cir"
* resistencias en paralelo
vdd 1 0 vdc=9 type=vdc
vdd 3 0 vdc=1.5 type=vdc
r1 1 2 47
r2 2 4 220
r3 2 3 180
r4 4 5 1000
r5 5 0 560
.op
.end
```

    Writing resistencias en paralelo 2.cir



```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit('resistencias en paralelo 2.cir')
circuito = circuito_y_análisis[0]       
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
resultados = ahkab.run(circuito, lista_de_análisis)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)


Imprimimos los resultados del análisis .op. Como puedes comprobar, Ahkab sólo reporta la intensidad de corriente en las ramas en las que hay una pila (en este caso, la rama donde está la pila VDD).


```python
print(resultados['op'])
```

    OP simulation results for '* resistencias en paralelo'(netlist resistencias en paralelo 2.cir).
    Run on 2021-01-03 13:17:55, data file None.
    Variable    Units        Value         Error    %
    ----------  -------  ---------  ------------  ---
    V1          V        9          -8.99997e-12    0
    V3          V        1.5        -1.50001e-12    0
    V2          V        7.29441    -7.29442e-12    0
    V4          V        6.39285    -6.39285e-12    0
    V5          V        2.29487    -2.29487e-12    0
    I(VDD)      A        0.0321912   0              0
    I(VDD)      A        0.0321912   0              0


Realizamos los calculos con Sympy y los mostramos en pantalla.


```python
# CIRCUITO PARALELO 2

from sympy.physics.units import kilo, volts, ohms, convert_to
from sympy import solve, symbols, Eq
from sympy.physics import units as u

v1 = 9*volts
v2 = 1.5*volts
r1 = 47*ohms
r2 = 220*ohms
r3 = 180*ohms
r4 = 1*kilo*ohms
r5 = 560*ohms
r_2_4_5 = r2 + r4 + r5
r_2_3_4_5 = (r3 * r_2_4_5) / (r3 + r_2_4_5)

r_total = r1 + r_2_3_4_5

intensidad = symbols('i')
ley_ohm = Eq(v1, intensidad*r_total)
solucion_para_intensidad = solve(ley_ohm, intensidad)

v_r3_v2 = (solucion_para_intensidad[0] * r_2_3_4_5)

i_r2_r4_r5 =  v_r3_v2 / r_2_4_5

print ("V1 =",v1)
print ("V2 =",v2)

print ("\nR1 =",convert_to(r1, [u.ohms]).n(5))
print ("R2 =",convert_to(r2, [u.ohms]).n(4))
print ("R3 =",convert_to(r3, [u.ohms]).n(4))
print ("R4 =",convert_to(r4, [u.ohms]).n(4))
print ("R5 =",convert_to(r5, [u.ohms]).n(4))
print ("R2 + R4 + R5 =",convert_to(r_2_4_5, [u.ohms]).n(4))
print ("R2 + R3 + R4 + R5 =",convert_to(r_2_3_4_5, [u.ohms]).n(4))

print ("\nV_R1 =",convert_to(solucion_para_intensidad[0] * r1, [u.volts]).n(4))
print ("V_R2 =",convert_to((i_r2_r4_r5 * r2), [u.volts]).n(4))
print ("V_R3 =",convert_to((solucion_para_intensidad[0] * r_2_3_4_5) - v2 , [u.volts]).n(4))
print ("V_R4 =",convert_to((i_r2_r4_r5 * r4), [u.volts]).n(4))
print ("V_R5 =",convert_to((i_r2_r4_r5 * r5), [u.volts]).n(4))

print ("\nI_R1 =",convert_to(solucion_para_intensidad[0], [u.amperes]).n(2))
print ("I_R2 =",convert_to(v_r3_v2 / r_2_4_5, [u.amperes]).n(2))
print ("I_R3 =",convert_to(v_r3_v2 / r3, [u.amperes]).n(2))
print ("I_R4 =",convert_to(v_r3_v2 / r_2_4_5, [u.amperes]).n(2))
print ("I_R5 =",convert_to(v_r3_v2 / r_2_4_5, [u.amperes]).n(2))

print ("\nTension Total =", v1)
print ("Resistencia Total =",convert_to(r_total, [u.ohms]).n(6))
print ("Intensidad Total =",convert_to(solucion_para_intensidad[0], [u.amperes]).n(2))
```

    V1 = 9*volt
    V2 = 1.5*volt
    
    R1 = 47.0*ohm
    R2 = 220.0*ohm
    R3 = 180.0*ohm
    R4 = 1000.0*ohm
    R5 = 560.0*ohm
    R2 + R4 + R5 = 1780.0*ohm
    R2 + R3 + R4 + R5 = 163.5*ohm
    
    V_R1 = 2.01*volt
    V_R2 = 0.864*volt
    V_R3 = 5.49*volt
    V_R4 = 3.927*volt
    V_R5 = 2.199*volt
    
    I_R1 = 0.043*ampere
    I_R2 = 0.0039*ampere
    I_R3 = 0.039*ampere
    I_R4 = 0.0039*ampere
    I_R5 = 0.0039*ampere
    
    Tension Total = 9*volt
    Resistencia Total = 210.469*ohm
    Intensidad Total = 0.043*ampere


> **Pregunta:** inserta dos *pilas virtuales* de 0 voltios en el resto de ramas del circuito (`Vdummy1` en la rama donde está `R5` y `Vdummy2` en la rama donde está `R3` y `R4`) para que Ahkab nos imprima también la corriente en las mismas. Es muy parecido al tercer circuito que tienes que resolver, donde `V1`, `V2` y `V3` tienen cero voltios. Estas *pilas nulas* son, a todos los efectos, *simples cables*. Una vez que ya tienes las corrientes en todas las ramas, comprueba que se cumple la Ley de Kirchhoff para las corrientes:

$$
I_{\text{entrante}} = \sum_i^{N} I_{\text{salientes}}
$$


```python
%%writefile "resistencias en paralelo 2_dummy.cir"
* resistencias en paralelo
vdd 1 0 vdc=9 type=vdc
vdd2 3 0 vdc=1.5 type=vdc
Vdummy1 6 7 vdc=0 type=vdc
Vdummy2 2 5 vdc=0 type=vdc
r1 1 2 47
r2 2 4 220
r3 5 3 180
r4 4 6 1000
r5 7 0 560
.op
.end
```

    Writing resistencias en paralelo 2_dummy.cir



```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit('resistencias en paralelo 2_dummy.cir')
circuito = circuito_y_análisis[0]       
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
resultados = ahkab.run(circuito, lista_de_análisis)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)



```python
print(resultados['op'])
```

    OP simulation results for '* resistencias en paralelo'(netlist resistencias en paralelo 2_dummy.cir).
    Run on 2021-01-03 13:18:28, data file None.
    Variable    Units          Value         Error    %
    ----------  -------  -----------  ------------  ---
    V1          V         9           -9e-12          0
    V3          V         1.5         -1.49999e-12    0
    V6          V         2.29487     -2.29487e-12    0
    V7          V         2.29487     -2.29487e-12    0
    V2          V         7.29441     -7.29444e-12    0
    V5          V         7.29441     -7.29442e-12    0
    V4          V         6.39285     -6.39285e-12    0
    I(VDD)      A        -0.0362891    0              0
    I(VDD2)     A         0.0321912    0              0
    I(VDUMMY1)  A         0.00409798   0              0
    I(VDUMMY2)  A         0.0321912    0              0


Como podemos observar, las leyes de Krichoff se cumplen, ya que las intensidades de entrada del circuito a la rama en paralelo es igual a la intensidad de salida de dicho circuito, es decir, si sumamos las intensidad que circula en la rama de R3 y la de la rama de R2, R4 y R5, el resultado es idéntico a la intendiad que circula por R1.

$ I(VDUMMY1) + I(VDUMMY2) = I(VDD) \rightarrow 0,00409798A + 0,0321912A = 0,03628918A $

$$
I_{\text{entrante}} = \sum_i^{N} I_{\text{salientes}}
$$


```python
%%writefile "resistencias en paralelo 3.cir"
* resistencias en paralelo
vdd 0 1 vdc=9 type=vdc
Vdummy1 1 2 vdc=0 type=vdc
Vdummy2 1 3 vdc=0 type=vdc
Vdummy3 1 4 vdc=0 type=vdc
r1 2 0 10k
r2 3 0 2k
r3 4 0 1k
.op
.end
```

    Writing resistencias en paralelo 3.cir



```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit('resistencias en paralelo 3.cir')
circuito = circuito_y_análisis[0]       
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
resultados = ahkab.run(circuito, lista_de_análisis)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)


Imprimimos los resultados del análisis `.op`. Como puedes comprobar, Ahkab sólo reporta la intensidad de corriente en las ramas en las que hay una pila (en este caso, la rama donde está la pila `VDD`).


```python
print(resultados['op'])
```

Realizamos los calculos con Sympy y los mostramos en pantalla.


```python
# CIRCUITO PARALELO 3

from sympy.physics.units import kilo, volts, ohms, convert_to
from sympy import solve, symbols, Eq
from sympy.physics import units as u

v1 = 9*volts
# No colocamos el resto de pilas porque estan descargadas y en paralelo con la pila principal, así que no afectan a nuestros cálculos del circuito.
r1 = 10000*ohms
r2 = 2000*ohms
r3 = 1*kilo*ohms

r_total = (r1 * r2 * r3) / (r2*r3+r1*r3+r1*r2)

intensidad = symbols('i')
ley_ohm = Eq(v1, intensidad*r_total)
solucion_para_intensidad = solve(ley_ohm, intensidad)

print ("R1 =",(convert_to(r1, [u.ohms]).n(5)))
print ("R2 =",(convert_to(r2, [u.ohms]).n(4)))
print ("R3 =",(convert_to(r3, [u.ohms]).n(4)))

print ("\nV_R1 =",v1)
print ("V_R2 =",v1)
print ("V_R3 =",v1)

print ("\nI_R1 =",(convert_to(v1 / r1, [u.amperes]).n(2)))
print ("I_R2 =",(convert_to(v1 / r2, [u.amperes]).n(2)))
print ("I_R3 =",(convert_to(v1 / r3, [u.amperes]).n(2)))

print ("\nTension Total =", v1)
print ("Resistencia Total =",(convert_to(r_total, [u.ohms]).n(6)))
print ("Intensidad Total =",(convert_to(solucion_para_intensidad[0], [u.amperes]).n(2)))
```

    R1 = 10000.0*ohm
    R2 = 2000.0*ohm
    R3 = 1000.0*ohm
    
    V_R1 = 9*volt
    V_R2 = 9*volt
    V_R3 = 9*volt
    
    I_R1 = 0.0009*ampere
    I_R2 = 0.0045*ampere
    I_R3 = 0.009*ampere
    
    Tension Total = 9*volt
    Resistencia Total = 625.0*ohm
    Intensidad Total = 0.014*ampere


 # Circuitos en DC que evolucionan con el tiempo

 ## Carga de un condensador
 Vamos a ver qué le pasa a un circuito de corriente continua cuando tiene un condensador
 en serie.

 ![](https://raw.githubusercontent.com/JMPinillos/CIRCUITOS_ELECTRICOS/main/condensador%20en%20continua.svg?sanitize=true)

 Primero guardamos el circuito en un netlist externo:


```python
%%writefile "condensador en continua.ckt"
* Carga condensador
v1 0 1 type=vdc vdc=6
r1 1 2 1k
c1 2 0 1m ic=0
.op
.tran tstep=0.1 tstop=8 uic=0
.end
```

    Writing condensador en continua.ckt


> **Pregunta:** ¿qué significa el parámetro `ic=0`? ¿qué perseguimos con un análisis de tipo `.tran`?

Con el parametro `ic=0` indicamos que queremos que los voltajes e intensidades sean 0 al inicio en todo el circuito.

Con un análisis de tipo .tran realizamos un análisis temporal de variables de salida: Se pueden especificar distintas excitaciones: pulsos, exponenciales, sinusoidales, etc.

Leamos el circuito:


```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit("condensador en continua.ckt")
```

 Separamos el netlist de los análisis y asignamos un fichero de almacenamiento de datos (`outfile`):


```python
circuito = circuito_y_análisis[0]
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
lista_de_análisis[1]['outfile'] = "simulación tran.tsv"
```

 Ejecutamos la simulación:


```python
resultados = ahkab.run(circuito, lista_de_análisis)
print(resultados['op'])
print(resultados['tran'].keys())
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)
    Starting transient analysis: 
    Selected method: TRAP
    Solving...  done.
    Average time step: 0.0869565
    OP simulation results for '* carga condensador'(netlist condensador en continua.ckt).
    Run on 2021-01-03 13:19:24, data file None.
    Variable    Units      Value    Error    %
    ----------  -------  -------  -------  ---
    V1          V             -6    6e-12    0
    V2          V             -6    6e-12    0
    I(V1)       A              0    0        0
    ['T', 'V1', 'V2', 'I(V1)']


 Dibujamos la gráfica de carga del condensador con el tiempo, centrándonos en la intensidad que circula por la pila. 


```python
figura = plt.figure()
plt.title("Carga de un condensador")
plt.plot(resultados['tran']['T'], resultados['tran']['I(V1)'], label="Intensidad de carga")
plt.ylabel('Intensidad (A)')
plt.xlabel('Tiempo')
plt.legend()
```




    <matplotlib.legend.Legend at 0x1215c0820>




    
![svg](output_100_1.svg)
    


En la gráfica podemos observar la intensidad que circula el en circuito a medida que pasa el tiempo y se va cargando el condensador.
Como hemos visto en el temario, un condensador es capaz de almacenar carga y cuando esta completamente cargado vemos que la intensidad disminuye hasta llegar a 0, esto se debe a que deja de haber circulación de electrones en el circuito porque el condensador se ha cargado completamente.

La curva sería instantanea si no hubiera conectada una resistencia, esto es porque el tiempo de carga del condensador es directamente proporcional a la resistencia del circuito.

$ T = R \cdot C $

En caso de desconectar la pila y conectar los bornes del circuito en una superficie metálica, se observaría una curva de descarga en el tiempo, también directamente proporcional a la resistencia del circuito.

> **Pregunta:** Etiqueta los ejes convenientemente y comenta la gráfica. Dibuja otra gráfica con el voltaje en el borne `V1`. ¿Por qué son *opuestas*? ¿Qué le ocurre al voltaje a medida que evoluciona el circuito en el tiempo? Dibuja las gráficas en un formato estándar de representación vectorial (SVG, por ejemplo). Algo de ayuda [aquí](https://ipython.readthedocs.io/en/stable/api/generated/IPython.display.html#IPython.display.set_matplotlib_formats). ¿Qué valores devuelve el análisis de tipo `.op`? Justifícalo.


```python
figura = plt.figure()
plt.title("Carga de un condensador")
plt.plot(resultados['tran']['T'], resultados['tran']['V2'], label="Voltaje del condensador")
plt.xlabel('Tiempo')
plt.ylabel('Voltaje del condensador (V)')
plt.legend()
```




    <matplotlib.legend.Legend at 0x12161d7c0>




    
![svg](output_103_1.svg)
    


En esta gráfica podemos observar la variación de voltaje en el condensador a medida que pasa el tiempo.

Podemos observar que la gráfica actual es opuesta a la anterior, esto se debe a que a medida que el condensador se va cargando, el voltaje del condensador aumenta, pero la intensidad que circula por el circuito disminuye porque el condensador va absorviendo esa carga.

Como hemos dicho anteriormente este tiempo de carga del condensador viene limitado por la resistencia del circuito.

## Carrera de condensadores

Ahora tenemos un circuito con dos condensadores en paralelo: 

![](https://raw.githubusercontent.com/JMPinillos/CIRCUITOS_ELECTRICOS/main/condensadores%20en%20paralelo.svg?sanitize=true)

> **Pregunta:** Crea el netlist de este circuito e identifica qué condensador se satura primero. Dibuja la evolución de la intensidad en ambas ramas de manera simultánea. [Aquí](https://matplotlib.org/gallery/api/two_scales.html) tienes un ejemplo de cómo se hace esto en Matplotlib. Recuerda que para que Ahkab nos devuelva la corriente en una rama, debe de estar presente una pila. Si es necesario, inserta pilas virtuales de valor nulo (cero voltios), tal y como hemos comentado antes. Grafica también los voltajes (en otra gráfica, pero que aparezcan juntos). 


```python
%%writefile "carrera en condensadores.ckt"
* Carga condensador
v0 0 1 type=vdc vdc=10
r1 0 2 3k
c1 2 3 47u ic=0
v1dummy 3 1 type=vdc vdc=0
c2 2 4 22u ic=0
v2dummy 4 1 type=vdc vdc=0
.op
.tran tstep=0.01 tstart=6.5 tstop=7.5 uic=0
.end
```

    Writing carrera en condensadores.ckt



```python
circuito_y_análisis = ahkab.netlist_parser.parse_circuit("carrera en condensadores.ckt")
circuito = circuito_y_análisis[0]       
análisis_en_netlist = circuito_y_análisis[1]
lista_de_análisis = ahkab.netlist_parser.parse_analysis(circuito, análisis_en_netlist)
lista_de_análisis[1]['outfile'] = "simulación tran carrera condensadores.tsv"
resultados = ahkab.run(circuito, lista_de_análisis)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)
    Starting transient analysis: 
    Selected method: TRAP
    Solving...  done.
    Average time step: 0.00900901



```python
figura = plt.figure()
plt.title("Carrera de condensadores")
plt.xlim(6.65, 7.5)
plt.ylim(0.0, 0.0005)
plt.grid()
plt.plot(resultados['tran']['T'], resultados['tran']['I(V1DUMMY)'],label="Intensidad en C1")
plt.plot(resultados['tran']['T'], resultados['tran']['I(V2DUMMY)'],label="Intensidad en C2")
plt.xlabel('Tiempo')
plt.ylabel('Intensidad(V)')
plt.legend()
```




    <matplotlib.legend.Legend at 0x121717be0>




    
![svg](output_108_1.svg)
    


## Circuitos en corriente alterna

** Ejercicio **: Simula este circuito con LTspice y representa el voltaje y la intensidad en función del tiempo. Traduce este ejercicio a la versión Spice de Akhab y haz la misma representación.


```python
%%writefile "corriente alterna.net"
* Circuito en corriente alterna
v1 1 0 sin(0 120 60 0 0)
r1 0 1 10k
.op
.tran 1
.end
```

    Overwriting corriente alterna.net



```python
lts "corriente alterna.net"
```

Mostramos los datos del archivo corriente alterna.log


```python
%pycat corriente alterna.log
```

    [0mC[0m[0;31m [0m[0mi[0m[0;31m [0m[0mr[0m[0;31m [0m[0mc[0m[0;31m [0m[0mu[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m*[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mC[0m[0;31m [0m[0mi[0m[0;31m [0m[0mr[0m[0;31m [0m[0mc[0m[0;31m [0m[0mu[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0mo[0m[0;31m [0m[0;31m [0m[0;31m [0m[0me[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mc[0m[0;31m [0m[0mo[0m[0;31m [0m[0mr[0m[0;31m [0m[0mr[0m[0;31m [0m[0mi[0m[0;31m [0m[0me[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ma[0m[0;31m [0m[0ml[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0mn[0m[0;31m [0m[0ma[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0mO[0m[0;31m [0m[0mP[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mp[0m[0;31m [0m[0mo[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mf[0m[0;31m [0m[0mo[0m[0;31m [0m[0mu[0m[0;31m [0m[0mn[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mb[0m[0;31m [0m[0my[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0ms[0m[0;31m [0m[0mp[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mo[0m[0;31m [0m[0mn[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mD[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mS[0m[0;31m [0m[0mu[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mJ[0m[0;31m [0m[0ma[0m[0;31m [0m[0mn[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;36m4[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;36m5[0m[0;31m [0m[0;36m5[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mT[0m[0;31m [0m[0mo[0m[0;31m [0m[0mt[0m[0;31m [0m[0ma[0m[0;31m [0m[0ml[0m[0;31m [0m[0;31m [0m[0;31m [0m[0me[0m[0;31m [0m[0ml[0m[0;31m [0m[0ma[0m[0;31m [0m[0mp[0m[0;31m [0m[0ms[0m[0;31m [0m[0me[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mm[0m[0;31m [0m[0me[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;36m8[0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mo[0m[0;31m [0m[0mn[0m[0;31m [0m[0md[0m[0;31m [0m[0ms[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mn[0m[0;31m [0m[0mo[0m[0;31m [0m[0mm[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m7[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mm[0m[0;31m [0m[0mp[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m7[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mm[0m[0;31m [0m[0me[0m[0;31m [0m[0mt[0m[0;31m [0m[0mh[0m[0;31m [0m[0mo[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mm[0m[0;31m [0m[0mo[0m[0;31m [0m[0md[0m[0;31m [0m[0mi[0m[0;31m [0m[0mf[0m[0;31m [0m[0mi[0m[0;31m [0m[0me[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mp[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mo[0m[0;31m [0m[0mt[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m4[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m8[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mn[0m[0;31m [0m[0mi[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m4[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m8[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0ma[0m[0;31m [0m[0mn[0m[0;31m [0m[0mp[0m[0;31m [0m[0mo[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0mt[0m[0;31m [0m[0ms[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;36m6[0m[0;31m [0m[0;36m5[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0ma[0m[0;31m [0m[0mc[0m[0;31m [0m[0mc[0m[0;31m [0m[0me[0m[0;31m [0m[0mp[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;36m5[0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mr[0m[0;31m [0m[0me[0m[0;31m [0m[0mj[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mt[0m[0;31m [0m[0me[0m[0;31m [0m[0md[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m5[0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mm[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0mi[0m[0;31m [0m[0mx[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0mi[0m[0;31m [0m[0mz[0m[0;31m [0m[0me[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mf[0m[0;31m [0m[0mi[0m[0;31m [0m[0ml[0m[0;31m [0m[0ml[0m[0;31m [0m[0mi[0m[0;31m [0m[0mn[0m[0;31m [0m[0ms[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0ms[0m[0;31m [0m[0mo[0m[0;31m [0m[0ml[0m[0;31m [0m[0mv[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;34m=[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mN[0m[0;31m [0m[0mo[0m[0;31m [0m[0mr[0m[0;31m [0m[0mm[0m[0;31m [0m[0ma[0m[0;31m [0m[0ml[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mM[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0mi[0m[0;31m [0m[0mx[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mC[0m[0;31m [0m[0mo[0m[0;31m [0m[0mm[0m[0;31m [0m[0mp[0m[0;31m [0m[0mi[0m[0;31m [0m[0ml[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m3[0m[0;31m [0m[0;36m6[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mo[0m[0;31m [0m[0mb[0m[0;31m [0m[0mj[0m[0;31m [0m[0me[0m[0;31m [0m[0mc[0m[0;31m [0m[0mt[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mc[0m[0;31m [0m[0mo[0m[0;31m [0m[0md[0m[0;31m [0m[0me[0m[0;31m [0m[0;31m [0m[0;31m [0m[0ms[0m[0;31m [0m[0mi[0m[0;31m [0m[0mz[0m[0;31m [0m[0me[0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;34m/[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m/[0m[0;31m [0m[0;34m[[0m[0;31m [0m[0;36m0[0m[0;31m [0m[0;34m.[0m[0;31m [0m[0;36m1[0m[0;31m [0m[0;34m][0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0mM[0m[0;31m [0m[0ma[0m[0;31m [0m[0mt[0m[0;31m [0m[0mr[0m[0;31m [0m[0mi[0m[0;31m [0m[0mx[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mC[0m[0;31m [0m[0mo[0m[0;31m [0m[0mm[0m[0;31m [0m[0mp[0m[0;31m [0m[0mi[0m[0;31m [0m[0ml[0m[0;31m [0m[0me[0m[0;31m [0m[0mr[0m[0;31m [0m[0;36m2[0m[0;31m [0m[0;34m:[0m[0;31m [0m[0;31m [0m[0;31m [0m[0mo[0m[0;31m [0m[0mf[0m[0;31m [0m[0mf[0m[0;31m [0m[0;34m[0m
    [0;34m[0m[0;31m [0m[0;34m[0m[0;34m[0m[0m


Dibujamos la gráfica con los datos obtenidos


```python
import ltspice
l = ltspice.Ltspice("corriente alterna.raw")
l.parse()
time = l.get_time()
V1 = l.get_data('V(1)')
plt.title("Interpretación gráfica dc circuito sencillo con AC")
plt.plot(time, V1, label="Voltaje (V1)")
plt.ylabel("Voltaje (V)")
plt.xlabel("Tiempo")
plt.legend()
```




    <matplotlib.legend.Legend at 0x122d5fdf0>




    
![svg](output_115_1.svg)
    


La gráfica nos muestra una onda de corriente alterna de 120 V y 60 Hz.


```python
%%writefile "corriente alterna ahkab.net"
v1 1 0 type=sin 0 120 60 0 0
R1 0 1 10k
.op
.tran tstep=.1n tstop=10n method=trap uic=0
.end
```

    Overwriting corriente alterna ahkab.net



```python
circuito_y_análisis_alterna_ahkab=ahkab.netlist_parser.parse_circuit("corriente alterna ahkab.net")
```


```python
circuito_alterna_ahkab = circuito_y_análisis_alterna_ahkab[0]
análisis_en_netlist_alterna_ahkab = circuito_y_análisis_alterna_ahkab[1]
lista_de_análisis_alterna_ahkab = ahkab.netlist_parser.parse_analysis(circuito_y_análisis_alterna_ahkab, análisis_en_netlist_alterna_ahkab)
print(lista_de_análisis_alterna_ahkab)
```

    [{'type': 'op', 'guess': True, 'x0': None}, {'type': 'tran', 'tstep': 1.0000000000000002e-10, 'tstop': 1e-08, 'method': 'trap', 'tstart': 0, 'x0': None}]



```python
lista_de_análisis_alterna_ahkab[1]['outfile'] = "simulación ac.tsv"
```


```python
lista_de_análisis_alterna_ahkab[[i for i, d in enumerate(lista_de_análisis_alterna_ahkab) if "op" in d.values() or "tran" in d.values()] [0]]['outfile'] = "simulación ac.tsv"
resultados_ahkab = ahkab.run(circuito_alterna_ahkab, lista_de_análisis_alterna_ahkab)
```

    Starting op analysis:
    Calculating guess: skipped. (linear circuit)
    Solving...   done.
    Solving...   done.
    Difference check within margins.
    (Voltage: er=0.001, ea=1e-06, Current: er=0.001, ea=1e-09)
    Starting transient analysis: 
    Selected method: TRAP
    Solving...  done.
    Average time step: 9.25926e-11



```python
print(resultados_ahkab['tran'])
```

    <TRAN simulation results for 'v1 1 0 type=sin 0 120 60 0 0' (netlist corriente alterna ahkab.net), from 0 s to 1e-08 s. Diff. method TRAP. Run on 2021-01-03 13:25:20, data file simulación ac.tsv>



```python
print(resultados_ahkab['tran'].keys())
```

    ['T', 'V1']

