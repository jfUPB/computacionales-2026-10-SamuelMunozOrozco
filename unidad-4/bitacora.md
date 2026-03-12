# Unidad 4

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### Evidencia 1: inserción del primer nodo en una cola vacía (enqueue)

#### Pantallazo 1
<img width="1919" height="1139" alt="image" src="https://github.com/user-attachments/assets/a11fcc87-56ba-4f08-977a-acf493f1cbaf" />
Explicacion de las variables

#### Pantallazo 2
<img width="1919" height="1143" alt="image" src="https://github.com/user-attachments/assets/612ac53a-da04-4eb7-9952-10d3200b68cb" />
Aqui las variables importantes son "front", "rear" y "size". Que tienen los siguientes valores:

front = NULL

rear = NULL

size = 0

Esto demuestra que la cola esta vacia antes de insertarla, ya que al tener front y rear, en NULL, eso significa que no hay ningun nodo y el size=0, es porque como no hay nodos, pues no hay como ponerle valor a size

#### Pantallazo 3
<img width="1919" height="1137" alt="image" src="https://github.com/user-attachments/assets/93eca487-8b1b-496a-bac3-71cdbadc6dbb" />
Al ejecutar la linea:
```cpp
Node * newNode = new Node(x, y, radius, color, opacity);
```
#### Pantallazo 4
Se crea un nuevo node, que se puede evidenciar en el Autos que se guardo correctamente en la memoria
<img width="1844" height="145" alt="image" src="https://github.com/user-attachments/assets/3141317a-665e-463d-80cd-623d0f6b0ba5" />

#### Pantallazo 5
En el siguiente pantallazo se puede ver que ahora front y rear tienen la misma direccion, lo que evidencia que apuntan al mismo nodo
<img width="1918" height="1143" alt="image" src="https://github.com/user-attachments/assets/368ba9df-cbe4-4c82-b37c-86e4ea69cb93" />

#### Pantallazo 5
Y en el siguiente, si lo expandimos a front, rear y newNode, podemos ver que tienen los mismos valores en x, y, radius, color, etc.
<img width="1820" height="464" alt="image" src="https://github.com/user-attachments/assets/6dafcfb4-2ca1-4ea3-a450-7d45f4f3e721" />














## Bitácora de reflexión


