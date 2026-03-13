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
















## Bitácora de reflexión









