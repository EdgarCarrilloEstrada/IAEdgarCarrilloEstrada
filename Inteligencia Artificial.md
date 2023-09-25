## Algoritmo para ganar, empatar o nunca perder en el juego tic tac toe (también llamado Gato o 3 en línea)

Para la solución de este algoritmo tenemos dos opciones iniciales: Que sea el agente quien inicie el juego, o que el contrincante inicie el juego.

Como idea inicial, podemos decir que quien inicie el juego esta jugando a la ofensiva y el que inicia en segundo lugar juega a la defensiva.

Para empezar vamos describiendo el tablero de juego: el tablero es una cuadricula construida por 2 lineas horizontales paralelas que se intersectan con 2 lineas verticales paralelas generando 9 espacios. Para poder identificar cada uno de estos espacios, los numeraremos de forma que el cuadro superior izquierdo sea el numero 1, el cuadro superior central sea el numero 2, el cuadro superior derecho sea el numero 3, el cuadro central izquierdo sea el numero 4 y así sucesivamente.

El juego consiste en colocar 3 figuras en línea vertical, horizontal o en diagonal. Normalmente representadas por medio de una cruz y un circulo. Debido a que debemos buscar un acomodo específico con las figuras, las cuadrículas del tablero de juego tienen un peso diferente debido a la cantidad de combinaciones que pueden generar. Las cuadriculas de mayor valor son la central y las esquinas de nuestro tablero, mientras que los centros laterales son los recuadros con menos valor por lo limitado que se vuelve el juego desde estos origenes. Por lo tanto, debemos de priorizar el uso de las esquinas y del centro para que el juego resulte ganador. 

Para la explicación estaremos refiriendonos al jugador 1 y al jugador 2 como  el agente y el contrincante, respectivamente. Con estos antecedentes, podemos empezar.

Supongamos que el agente es el primero en iniciar, por lo que es muy recomendable iniciar en alguna de las esquinas. Si el contrincante coloca su primera pieza en una cuadricula lateral central tenemos prácticamente el juego ganado. Nuestra segunda figura tendrá que ser en una segunda esquina que no esté en forma diagonal con nuestra primera figura, es decir, que se encuentre de forma vertical u horizontal pero que la primera pieza del contrincante no esté en medio de las nuestras. El siguiente tiro del contrincante deberá tapar la cuadricula media entre las dos piezas del agente ya que si no hace esto, en el siguiente turno ganariamos. Al momento de que el contrincante haga su tiro, nosotros procederemos a poner nuestra pieza en una esquina que esté en diagonal con respecto a una de nuestras piezas y en forma horizontal o vertical sin que alguna pieza del contrincante interfiera. En el momento en que nosotros hacemos eso, tenemos dos vectores de solución en los que si el contrincante nos bloquea uno de ellos, podemos lograr nuestro objetivo con la segunda opción.

Ahora, supongamos que el agente es el primero en iniciar y tira de nuevo en una esquina, y si nuestro contrincante pone su primera ficha en una esquina, debemos de seguir con la estrategia de poner el segundo simbolo en otra esquina pero ahora que sea en forma diagonal como prioridad, y si esto no es posible, entonces que sea en una esquina de forma vertical u horizontal. Al hacer esto, el contrincante esta obligado a bloquear esta jugada. Como tercer tiro, debemos colocar la pieza en la ultima esquina restante y esto volverá a generar que existan 2 formas de ganar y el contrincante solamente pueda bloquear una.

Por último, si el agente tira en una esquina y el contrincante en el centro, el juego terminará en empate seguramente ya que nos podemos dedicar a mutuamente a bloquear la jugada del contrincante y ninguno ganará.


##  Secuencia de percepción y medida de rendimiento

### Ejercicio 1
El primer ejercicio para realizar esta actividad dice lo siguiente:

> Un arriero se encuentra en el borde de un rio llevando un puma, una cabra y una lechuga. Debe cruzar a la otra orilla por medio de un bote con capacidad para dos (el arriero y alguna de sus pertenecias). La dificultad es que si el puma se queda solo con la cabra la devorará, y lo mismo sucederá si la cabra se queda sola con la lechuga. ¿Cómo cruzar sin perder ninguna pertenencia?

Solución:

Para la solución del problema debemos de definir unas cuantas cosas antes de dar una respuesta.

#### Representación de las configuraciones del universo del problema

Basta precisar la situación antes o después de cruzar. El arriero y cada una de sus pertenencias tienen que estar en alguna de las dos orillas. La representación del estado debe entonces indicar en que lado se encuentra cada uno de ellos. Para esto se puede utilizar un término simbólico con la siguiente sintáxis: estado(A,P,C,L), en que A, P, C y L son variables que representan, respectivamente, la posición del arriero, el puma, la cabra y la lechuga. Las variables pueden tomar dos valores: i y d, que simbolizan respectivamente el borde izquierdo y el borde derecho del rio. Por convención se elige partir en el borde izquierdo. El estado inicial es entonces estado(i,i,i,i). El estado objetivo es estado(d,d,d,d).

#### Definición de las reglas de transición

El arriero tiene cuatro acciones posibles: cruzar solo, cruzar con el puma, cruzar con la cabra y cruzar con la lechuga. Estas acciones están condicionadas a que ambos pasajeros del bote estén en la misma orilla y a que no queden solos el puma con la cabra o la cabra con la lechuga. El estado resultante de una acción se determina intercambiando los valores i y d para los pasajeros del bote.

#### Generación del espacio de estados

En la tabla siguiente se muestran los posibles estados de este problema:

|Estado			 |Movidas		    |Movidas        |Movidas        |Movidas        |
|---------------	 |------         |---            |---            |---            |
|					 |**cruza solo** |**con puma**   |**con cabra**  |**con lechuga** |
|estado(i,i,i,i)  |problema       |problema       |estado(d,i,d,i)|problema       |
|estado(d,i,d,i)  |estado(i,i,d,i)|imposible      |estado(i,i,i,i)|imposible      |
|estado(i,i,d,i)  |estado(d,i,d,i)|estado(d,d,d,i)|imposible      |estado(d,i,d,d)|
|estado(d,d,d,i)  |problema       |estado(i,i,d,i)|estado(i,d,i,i)|imposible      |
|estado(d,i,d,d)  |problema       |imposible      |estado(i,i,i,d)|estado(i,i,d,i)|
|estado(i,d,i,i)  |problema       |imposible      |estado(d,d,d,i)|estado(d,d,i,d)|
|estado(i,i,i,d)  |problema       |estado(d,d,i,d)|estado(d,i,d,d)|imposible      |
|estado(d,d,i,d)  |estado(i,d,i,d)|estado(i,i,i,d)|imposible      |estado(i,d,i,i)|
|estado(i,d,i,d)  |estado(d,d,i,d)|imposible      |estado(d,d,d,d)|imposible      |
|estado(d,d,d,d)  |problema       |problema       |estado(i,d,i,d)|problema       |




### Ejercicio 2
El segundo ejercicio menciona lo siguiente:

> Se tienen 3 monjes y 3 caníbales en el margen Oeste de un río. Existe una canoa con capacidad para dos personas como máximo. Se desea que los seis pasen al margen Este del río, pero hay que considerar que no debe haber más caníbales que monjes en ningún sitio porque entonces los caníbales se comen a los monjes. Además, la canoa siempre debe ser conducida por alguien.

Solución:
Para la solución del problema debemos de definir unas cuantas cosas antes de dar una respuesta.

#### Definición de las reglas de transición

Las reglas que se pueden aplicar son:

* Viajan un monje y un caníbal de O a E:

Si (Mo, Co, Me, Ce, O) AND Mo>=1 AND Co>=1 AND Ce+1<=Me+1 => (Mo-1, Co-1, Me+1, Ce+1, E)

* Viajan un monje y un caníbal de E a O:

Si (Mo, Co, Me, Ce, E) AND Me>=1 AND Ce>=1 AND Co+1<=Mo+1=> (Mo+1, Co+1, Me-1, Ce-1,O)

* Viajan dos monjes de O a E:

Si (Mo, Co, Me, Ce, O) AND Mo>=2 AND (Mo-2=0 OR Co<=Mo-2) AND Ce<=Me+2=> (Mo-2, Co, Me+2, Ce, E)

* Viajan dos monjes de E a O:

Si (Mo, Co, Me, Ce, E) AND Me>=2 AND (Me-2=0 OR Ce<=Me-2) AND Co<=Mo+2 => (Mo+2, Co, Me-2, Ce, O)

* Viajan dos caníbales de O a E:

Si (Mo, Co, Me, Ce, O) AND Co>=2 AND (Me=0 OR Ce+2<=Me) => (Mo, Co-2, Me, Ce+2, E)

* Viajan dos caníbales de E a O:

Si (Mo, Co, Me, Ce, E) AND Ce>=2 AND (Mo=0 OR Co+2<=Mo) => (Mo, Co+2, Me, Ce-2, O)

* Viaja un monje de O a E:

Si (Mo, Co, Me, Ce, O) AND Mo>=1 AND (Mo-1=0 OR Co<=Mo-1) AND Ce<= Me+1 => (Mo-1, Co, Me+1, Ce, E)

* Viaja un monje de E a O:

Si (Mo, Co, Me, Ce, E) AND Me>=1 AND (Me-1=0 OR Ce<=Me-1) AND Co<=Mo+1 => (Mo+1, Co, Me-1, Ce,O)

* Viaja un caníbal de O a E:

Si (Mo, Co, Me, Ce, O) AND Co>=1 AND (Me=0 OR Ce+1<=Me) => (Mo, Co-1, Me, Ce+1, E)

* Viaja un caníbal de E a O:

Si (Mo, Co, Me, Ce, O) AND Ce>=1 AND (Mo=0 OR Co+1<=Mo) => (Mo, Co+1, Me, Ce-1, E)

#### Generación del espacio de estados

(3,3,0,0,O) => (3,1,0,2,E) => 
(3,2,0,1,O) => (3,0,0,3,E) => 
(3,1,0,2,O) => (1,1,2,2,E) => 
(2,2,1,1,O) => (0,2,3,1,E) => 
(0,3,3,0,O) => (0,1,3,2,E) => 
(0,2,3,1,O) => (0,0,3,3,E)



### Ejercicio 3
El tercer ejercicio consiste en que existen 3 ranas rojas del lado izquierdo y 3 ranas azules del lado derecho. Existen 7 espacios en donde pueden estar éstas ranas y hay un espacio en medio de los dos grupos de ranas. El objetivo es que las ranas del lado izquierdo terminen en el lado derecho y viceversa. Las ranas solamente pueden moverse en dirección de su destino y no pueden retroceder una vez que ya saltaron.

Solución:

Para este problema debemos de tomar en cuenta el proceso es el mismo ya sea si inicias de la derecha o la izquierda, sigue el mismo patrón de solución debido a que es simétrico.

Debemos iniciar numerando las posiciones donde se encuentran las ranas, empezando de izquierda a derecha por el numero 1 y terminando en la derecha por el numero 7.

El orden para mover estas ranas es el siguiente, tomando en cuenta la numeración anteriormente establecida:

3 - 5 - 6 - 4 - 2 - 1 - 3 - 5 - 7 - 6 - 4 - 2 - 3 - 5 - 4

De esta forma, las ranas pueden cambiar de posicion sin interferir o bloquear las posibilidades de movimiento de las demás y lograr el objetivo final.


 