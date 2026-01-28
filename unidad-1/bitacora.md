# Unidad 1

### Actividad 1
### Experimento 1
#### Que sucede?
El programa suma valores, 1 y 2, guarda un determinado resultado en la RAM y luego entre an un bucle infinito

#### Que valor se almacena en la direccion de memoria 16?
Se almacena el valor 3

#### Por que es ese valor?
Porque en el programa, igualamos A con D, dandole a D el valor de A, que era 1, luego hicimos la siguiente suma, D = D + 2, lo que nos termino dando 3, por ultimo igualamos M = D, y recordemos que antes de esa igualdad habias escrito @16, lo que hace es guardar la direccion de memoria 16 en A. Por eso el numero 3 sale en la memoria numero 16

#### Que instrucciones se ejecutan en cada ciclo Fetch-Decode-Execute?
En Fetch el PC indica la instruccion en la ROM y la CPU lo carga. En Decode la CPU interpreta si las instrucciones son de tipo A o tipo C, si hay salto y si hay una operacion ALU. Por ultimo en Execute, Asigna los valores a A y D, luego los suma, guarda uno en la memoria y hace un salto

#### Qué cambios observas en el contenido de la memoria y los registros?
Durante la ejecucion del programa, A y D van teniendo distintos valores, hasta que A queda con 7 por la instruccion @7 y D con r, por la suma que se habia hecho. Por ultimo en la memoria RAM se almacena el numero 3 en la posicion 16. Y ya la memoria y los registros dejan de cambiar debido al bucle


#### Experimento 2
<img width="1358" height="265" alt="image" src="https://github.com/user-attachments/assets/8ad78037-4c7a-411d-b737-c165f1ce0399" />

<img width="1542" height="610" alt="image" src="https://github.com/user-attachments/assets/5b808950-7dc7-4cf1-9860-df4f3fa7735b" />


### Actividad 2
#### Identifica una de las instrucciones que use ALU y explica que hace
D = D-A. Toma un valor ya almacenado en el registro D y lo resta con otro almacenado en el registro A, y por ultimo, ese resultado queda almacenado en el registro D, reemplazando el anterior

#### ara que sirve el registro PC?
Sirve para indicar la direccion de la instruccion que la CPU debe ejecutar en la memoria ROM

#### Cual es la diferencia entre @i y @READKEYBOARD?
@i es una variable almacenada en la memoria RAM que se usa para guardar y acceder a datos datos, en este caso un puntero en la pantalla
@READKEYBOARD es una etiqueta en el programa, que es una direccion en la memoria ROM donde comienza una instruccion. Se usa para controlar el flujo del programa mediante saltos

#### Describe qué se necesita para leer el teclado y mostrar información en la pantalla
Para leer el teclado se usa KBD, porque, valga la redundancia, es la direccion del teclado y se usa para saber si hay una tecla presionada o no. 
Para mostrar algo en la pantalla se usa SCREEN, ya que al guardar valores en esta memoria se encienden o apagan pixeles en la pantalla.

#### Identifica un bucle en el programa y explica su funcionamiento
READKEYBOARD. Este bucle es para que el programa  lea el teclado de forma indefinida para que lea si se esta presionando una tecla o no, sin detener el programa

#### Identifica una condición en el programa y explica su funcionamiento
@KEYPRESSED
D;JNE
Esta condicion mira el valor que tenga el registro D y dice que si D es igual a cero, significa que no hay una tecla presionada y el programa no hace el salto y sigue con la otra instruccion. Y si D es diferente de cero, hay una tecla presionada y el programa salta a la etiqueta KEYPRESSED


### Actividad 3

<img width="702" height="732" alt="image" src="https://github.com/user-attachments/assets/b7f44fe7-a04c-427e-9619-e5288f89810b" />

<img width="1375" height="537" alt="image" src="https://github.com/user-attachments/assets/dfd51a46-21e3-4a02-af51-d59dd55a8894" />





## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 



## Bitácora de reflexión



