# Unidad 4

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### Evidencia 1: inserción del primer nodo en una cola vacía (enqueue)

#### Pantallazo 1
<img width="1919" height="1139" alt="image" src="https://github.com/user-attachments/assets/a11fcc87-56ba-4f08-977a-acf493f1cbaf" />
Se puso el breakpoint aca ya que queremos ver el estado del programa antes de que se modifique la estructura de datos, o sea, ver como esta la cola antes de poner el primer nodo

#### Pantallazo 2
<img width="1919" height="1143" alt="image" src="https://github.com/user-attachments/assets/612ac53a-da04-4eb7-9952-10d3200b68cb" />
Aqui las variables importantes son "front", "rear" y "size". Que tienen los siguientes valores:

front = NULL

rear = NULL

size = 0

Esto demuestra que la cola esta vacia antes de insertarla, ya que al tener front y rear, en NULL, eso significa que no hay ningun nodo y el size=0, indica que la cola no tiene nodos ahora mismo


#### Pantallazo 3
<img width="1919" height="1137" alt="image" src="https://github.com/user-attachments/assets/93eca487-8b1b-496a-bac3-71cdbadc6dbb" />


#### Pantallazo 4

Al ejecutar la linea:

```cpp
Node * newNode = new Node(x, y, radius, color, opacity);
```
Se crea un nuevo node "newNode". Se puede ver que se guardo correctamente en la memoria por la direccion de memoria que podemos ver, y si lo expandimos se pueden observar sus atributos
<img width="1844" height="145" alt="image" src="https://github.com/user-attachments/assets/3141317a-665e-463d-80cd-623d0f6b0ba5" />


#### Pantallazo 5
<img width="1918" height="1143" alt="image" src="https://github.com/user-attachments/assets/368ba9df-cbe4-4c82-b37c-86e4ea69cb93" />
En este pantallazo se puede evidenciar que le front y el rear tienen la misma direccion de memoria, lo que quiere decir que ambos apuntan al mismo nodo


### Evidencia 2: mantenimiento del orden FIFO al insertar más nodos (enqueue)
Ponemos el breakpoint en el mismo lugar
<img width="1919" height="1137" alt="image" src="https://github.com/user-attachments/assets/01e8923a-76e3-46d0-9685-58330b23c529" />
Lo que hacemos en entrar en enqueue, ya al estar ahora en la linea "void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {". Avanzamos por el codigo usando F10 hasta ejecutar la linea "front = rear = newNode;". Luego volvemos a hundir F5, para volver a entrar a la funcion y ejecutamos la linea "Node* newNode = new Node(...)"
<img width="1808" height="105" alt="image" src="https://github.com/user-attachments/assets/8d862b5f-dc4f-43ad-9f93-fe487e39d8e7" />
Aqui podemos evidenciar la direccion de memoria de front y rear que apuntan al nodo y al size con el valor 1 que es el nodo que hay en el momento.

Asi se ve en la pantalla del programa funcionando
<img width="1018" height="764" alt="image" src="https://github.com/user-attachments/assets/b2d3b2a6-b90d-45cd-ae29-fe5784c3757d" />

Luego hundimos F10 hasta ejecutar la linea "if (rear == nullptr)", como ya hay un nodo y rear ya no es NULL, se ira a else en el codigo y podemos evidenciar lo siguiente:
<img width="1914" height="1141" alt="image" src="https://github.com/user-attachments/assets/1b707ce2-102e-4143-91c5-4369c9ebeb48" />
Como se puede ver, el rear ya tiene direccion de memoria, por ende apunta a un nodo, y mas a vajo se puede ver que next es NULL, o sea, que el nodo que hay es el unico en la cola

Ahora para conectar los nodos, presionamos F10 sobre la linea "rear->next = newNode;" luego otra vez F10 sonbre "rear = newNode;" para actualizar el rear para que ahora el nuevo nodo sea el ultimo de la cola

<img width="1919" height="1140" alt="image" src="https://github.com/user-attachments/assets/1d4df7ba-2d82-41a4-abd4-69fd20c8db42" />
Aqui al mirar a front y rear podemos evidenciar que ya tienen diferentes direcciones de memoria, lo que significan que no apuntan a lo mismo, y tambien que el newNode tiene la misma direccion que rear, lo que quiere decir que ya el nuevo nodo esta al final de la cola


### Evidencia 3: comportamiento de eliminación y prevención de fugas (dequeue)
<img width="1919" height="1139" alt="image" src="https://github.com/user-attachments/assets/f95d4c8b-6c3c-4c04-9c34-9c8cb3c4cd70" />
Dejamos el breakpoint ahi para que el programa me permita generar nodos en la pantalla, asi esa linea identifique los nodos que va a eliminar

<img width="1919" height="1144" alt="image" src="https://github.com/user-attachments/assets/41d571a4-3031-4fbc-8c85-bdf0dc06a456" />
Como podemos ver en este pantallazo el front tiene las variables x, y, radius, net, lo que significa que ahi esta el nodo mas viejo. Tambien podemos ver que el size esta en 51, que es el maxSize de la cola y ya podemos eliminar un nodo

Ahora volvemos a hundir F10 para ejecutar la linea "Node* temp = front;" para que asi se guarde la direccion del nodo que vamos a eliminar en temp
<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/41ee0ffb-a203-46b3-8fbb-b302ad06d6f3" />
Como podemos ver, ahora front y temp tienen la misma direccion, lo que demuestra que se guardo el nodo que va a ser eliminado, en temp

Ahora ejecutamos la linea "front = front->next;" Esto para que el front cambie por el siguiente nodo a el que se va a eliminar
<img width="1919" height="1138" alt="image" src="https://github.com/user-attachments/assets/72a42a39-8c98-4f92-8d8a-9747ffbf8e64" />
En este pantallazo podemos ver que front y front->next tienen direcciones diferentes, eso quiere decir que front esta el nodo viejo y en front->next el siguiente nodo. Por ultimo vemos que size=51 y maxSize=50, que demuestra que la cola supero el tamaño maximo y se ejecuto dequeue()

Ahora ejecutamos la linea "delete temp;" para liberar la memoria del nodo eliminado y evitar memoryleak. Luego ejecutamos la linea "size--;" para reducir el tamaño y el size vuelva a 50
<img width="1919" height="1139" alt="image" src="https://github.com/user-attachments/assets/d4244bc1-1464-4b44-91b3-61f108c5e825" />
En este pantallazo se puede evidenciar que despues de ejecutar la linea "size--;" el size volvio a ser 50, lo que demuestra que se elimino el nodo correctamente


### Evidencia 4: control del tamaño máximo de la cola (maxSize)
<img width="1919" height="1140" alt="image" src="https://github.com/user-attachments/assets/8b4ba0e9-c2a5-4dd4-b28e-526e628af44e" />
Ponemos el siguiente breakoint en ofApp.h en la linea "if (size > maxSize)" porque aqui es donde se verifica si la cola supero el limite de su tamaño

En el mismo pantallazo podemos evidenciar la primera evidencia. En el Autos podemos ver dos variables, size y maxSize, en donde size tiene 51 de valor y maxSize 50, lo que nos indica que la cola a pasado el limite permitido


<img width="1919" height="1141" alt="image" src="https://github.com/user-attachments/assets/61685530-b98d-4395-a157-e876e2538205" />
Luego oprimirmos F10 para estar sobre la linea "dequeue();" y luego hundimos F11 para entrar a la funcion dequeue();. Lo que nos evidencia que cuando se supera el limite permitido de la cola se llama automaticamente a la funcion encargada de eliminar los nodos, que es dequeue()








## Bitácora de reflexión
