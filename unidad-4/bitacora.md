# Unidad 4

## Bitácora de proceso de aprendizaje

### Codigo
Este es el esqueleto que se nos dio para realizar la tarea
#### ofApp.h
```cpp
#pragma once
#include "ofMain.h"

// Nodo de la cola
struct Node {
    float x, y;
    float radius;
    ofColor color;
    float opacity;
    Node* next;

    Node(float _x, float _y, float _radius, ofColor _color, float _opacity)
        : x(_x), y(_y), radius(_radius), color(_color), opacity(_opacity), next(nullptr) {
    }
};

// Implementación manual de una cola (FIFO)
class BrushQueue {
public:
    Node* front;
    Node* rear;
    int size;
    int maxSize;

    BrushQueue(int _maxSize);
    ~BrushQueue();

    void enqueue(float x, float y, float radius, ofColor color, float opacity);
    void dequeue();
    void clear();
    bool isEmpty();
};


// Constructor
BrushQueue::BrushQueue(int _maxSize) : front(nullptr), rear(nullptr), size(0), maxSize(_maxSize) {}

// Destructor
BrushQueue::~BrushQueue() {
    clear();
}

// Implementa aquí `enqueue()`
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {
    // TODO: crear un nuevo nodo y agregarlo al final de la cola.
    // Si la cola supera `maxSize`, eliminar el nodo más antiguo con `dequeue()`.
}

// Implementa aquí `dequeue()`
void BrushQueue::dequeue() {
    // TODO: eliminar el nodo más antiguo si la cola no está vacía.
}

// Implementa aquí `clear()`
void BrushQueue::clear() {
    // TODO: eliminar todos los nodos de la cola.
}

// Implementa aquí `isEmpty()`
bool BrushQueue::isEmpty() {
    // TODO: retornar si la cola está vacía.
}


class ofApp : public ofBaseApp {
public:
    BrushQueue strokes; // Cola de trazos
    float backgroundHue = 0;

    ofApp() : strokes(50) {} // Tamaño máximo de la cola

    void setup();
    void update();
    void draw();
    void keyPressed(int key);
};
```

ofApp.cpp
```cpp
#include "ofApp.h"

//--------------------------------------------------------------
void ofApp::setup() {
    ofBackground(0);
}

//--------------------------------------------------------------
void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    // TODO: agregar un nuevo trazo si el mouse está presionado.
    // Usa strokes.enqueue(x, y, radius, color, opacity);
}

//--------------------------------------------------------------
void ofApp::draw() {
    // Fondo con gradiente dinámico
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    // TODO: dibujar los trazos almacenados en la cola.
    // Recorre los nodos desde strokes.front hasta nullptr y usa ofDrawCircle().
}

//--------------------------------------------------------------
void ofApp::keyPressed(int key) {
    if (key == 'c') {
        // TODO: limpiar la cola de trazos.
    }
    if (key == 'a') {
        // TODO: alternar entre 50 y 100 trazos.
    }
    else if (key == 's') {
        // TODO: guardar el frame actual.
    }
}
```

#### Lo que se agrego en los TODO

##### Primero enqueue()
```cpp
void BrushQueue::enqueue(float x, float y, float radius, ofColor color, float opacity) {

    Node* newNode = new Node(x, y, radius, color, opacity);

    if (rear == nullptr) {
        front = rear = newNode;
    }
    else {
        rear->next = newNode;
        rear = newNode;
    }

    size++;

    if (size > maxSize) {
        dequeue();
    }
}
```
* Primero se crea un nodo nuevo
```cpp
Node* newNode = new Node(x, y, radius, color, opacity);
```
Se crea un nodo con los datos del trazo. Posicion: x, y. radius, color y opacity

* Revisamos si la cola esta vacia
```cpp
if (rear == nullptr)
```
Si rear es nullptr es que no hay nodos en la cola

* Primer nodo de la cola
```cpp
front = rear = newNode;
```
Como es el primer elemento, entonces es frente y final al mismo tiempo; front y rear

* Si la cola ya tiene nodos
```cpp
 else {
        rear->next = newNode;
        rear = newNode;
    }
```
Lo que hace es conectar el ultimo nodo con el nuevo y hace que rear tome la direcicon de memoria de ese nuevo nodo

* La cola aumenta de tamaño
```cpp
size++;
```
Esto actualiza los nodos en la cola

* Controlar el tamaño maximo de la cola
```cpp
if (size > maxSize)
{
    dequeue();
}
```
Si el size supera al maxSize se ejecuta la funcion  dequeue(); que es la encargada de borrar los nodos

##### Segundo dequeue()
```cpp
void BrushQueue::dequeue() {

    if (front == nullptr) return;

    Node* temp = front;

    front = front->next;

    if (front == nullptr) {
        rear = nullptr;
    }

    delete temp;
    size--;
}
```

* Verificar si no hay nodos
```cpp
if (front == nullptr) return;
```
Si no hay nodos, pues no hay nada que eliminar y no se ejecuta la funcion

* Guardar el nodo que se va a borrar
```cpp
Node* temp = front;
```
Se guarda el nodo mas viejo en temp

* Mover el frnto al siguiente nodo
```cpp
front = front->next;
```
Hace que el front cambio de direccion de memoria al siguiente nodo en la cola

* En el caso de que solo haya un nodo
```cpp
if (front == nullptr)
{
    rear = nullptr;
}
```
Si el frnete en Null, entonces el final tambien

* Liberamos la memoria
```cpp
delete temp;
```
Asi eliminamos la variable temporal temp y liberamos la memoria para evitar memoryleak

* Actualizamos el tamaño
```cpp
size--;
```
La cola disminuye

#### Tercero clear()
```cpp
void BrushQueue::clear() {

    while (front != nullptr) {
        dequeue();
    }

}
```
Como ya tenemos una funcion que usa un nodo, pues la reutilizamos usando un while que recorra toda la cola preguntando si front es null, hasta que sea null y se elimine toda la cola


#### Cuarto isEmpty()
```cpp
bool BrushQueue::isEmpty() {
    return front == nullptr;
}
```
Esto solo responde a la pregunta de si la cola esta vacia o no.


#### Quinto update()
```cpp
void ofApp::update() {
    backgroundHue += 0.2;
    if (backgroundHue > 255) backgroundHue = 0;

    if (ofGetMousePressed()) {

        float x = ofGetMouseX();
        float y = ofGetMouseY();

        float radius = ofRandom(5, 20);

        ofColor color;
        color.setHsb(ofRandom(255), 200, 255);

        float opacity = ofRandom(50, 200);

        strokes.enqueue(x, y, radius, color, opacity);
    }
}
```
* Detectar si el mouse es presionado
```cpp
if (ofGetMousePressed())
```
Permite dibujar mientras se presiona el mouse

* Posicion del mouse
```cpp
float x = ofGetMouseX();
float y = ofGetMouseY();
```
La posicion del circulo que se dibuja

* Rdio aleatorio del circulo
```cpp
float radius = ofRandom(5, 20);
```

* Color aleatorio del circulo
```cpp
ofColor color;
color.setHsb(ofRandom(255), 200, 255);
```

* Opacidad
```cpp
float opacity = ofRandom(50, 200);
```

* Guardar el trazo en la cola
```cpp
strokes.enqueue(x, y, radius, color, opacity);
```
Cada movimiento del mouse crea un nuevo nodo en la cola

#### Sexto draw()
```cpp
void ofApp::draw() {
    // Fondo con gradiente dinámico
    ofColor color1, color2;
    color1.setHsb(backgroundHue, 150, 240);
    color2.setHsb(fmod(backgroundHue + 128, 255), 150, 240);
    ofBackgroundGradient(color1, color2, OF_GRADIENT_LINEAR);

    Node* current = strokes.front;

    while (current != nullptr) {

        ofSetColor(current->color, current->opacity);

        ofDrawCircle(current->x, current->y, current->radius);

        current = current->next;
    }
}
```

* Empezamos con el primer nodo de la cola
```cpp
Node* current = strokes.front;
```
Apunta al nodo mas antiguo

* Recorremos la cola
```cpp
while(current != nullptr)
```
Sigue hasta llegar al final de la cola

* Usamos el color guardado del nodo
```cpp
ofSetColor(current->color, current->opacity);
```
Le da a cada nodo un color y una opacidad

* Dibujamos el circulo
```cpp
ofDrawCircle(current->x, current->y, current->radius);
```
Usamos los datos guardados en el nodo

* Avanzamos al siguiente nodo
```cpp
current = current->next;
```
Recorre toda la cola


#### Septima keyPressed()
```cpp
void ofApp::keyPressed(int key) {

    if (key == 'c') {
        strokes.clear();
    }

    if (key == 'a') {

        if (strokes.maxSize == 50) {
            strokes.maxSize = 100;
        }
        else {
            strokes.maxSize = 50;
        }
    }

    else if (key == 's') {
        ofSaveFrame();
    }
}
```
La logica de las teclas

* Tecla C
```cpp
strokes.clear();
```
Llama a la funcion que elimina todos los nodos de la cola

* Tecla A
```cpp
if (strokes.maxSize == 50)
    strokes.maxSize = 100;
else
    strokes.maxSize = 50;
```
Hace que la cola cambia de tamaño, entre 50 a 100 y de 100 a 50

* Tecla S
```cpp
ofSaveFrame();
```
Toma una captura de pantalla del programa







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


### Evidencia 5: recorrido de la cola sin destruirla (draw)
<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/fbddd712-f79e-4201-bd36-1d6ac777f960" />
Se pone el breakpoint en esa linea ya que es el punto donde empieza el recorrido de la cola en el draw(). Aqui el sistema toma el puntero front que apunta al primer nodo y lo asigna a un puntero temporal llamado current, que sera utilizado para recorrer todos los nodos de la cola, mediante un ciclo:
```cpp
while(current != nullptr)
```

<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/dcb9a507-13c5-44cb-8d9d-2161fe9c8a8e" />
Se coloco el breakpoint en es alinea para ver el estado de la cola antes de iniciar el recorrido. El pantallazo demuestra que el recorrido empieza desde el primer nodo ya que front tiene una direccion de memoria valida. Y atmbien tenemos el size de valor 50 que confirma que existen nodos almacenados

<img width="1919" height="1138" alt="image" src="https://github.com/user-attachments/assets/c5823182-429e-4815-8336-40a1569fc635" />
El pantallazo muestra que draw() recorre la cola nodo por nodo usando el puntero temporal current. Como se puede ver, current tiene la misma direccion de memoria que front, lo que nos muestra que el recorrido comienza desde el primer nodo. Y con e ciclo "while(current != nullptr)" nos deja recorrer cada nodo de la cola


<img width="1919" height="1137" alt="image" src="https://github.com/user-attachments/assets/42e9795e-793f-40a2-b860-0c8d1285404c" />
En este pantallazo ejecutamos hasta la linea "current = current->next;" y aun seguimos en el ciclo while, lo que significa que el programa esta recorriendo cada nodo de la cola. En el panel de Autos, se puede observar que current apunta a un nodo y que current->next apunta al siguiente, lo que indica que el recorrido funciona correctamente

Ademas podemos ver que los punteros front y rear se mantienen igual, con las mismas direcciones, lo que demuestra que el recorrido funciona sin destruir o eliminar nigun nodo


### Evidencia 6: limpieza total de la memoria (clear)
Ponemos un breakpoint en la linea "	while (front != nullptr) {" para asi cuando creemos la cola en la pantalla e intentemos borrarla con c, se detenga ahi el programa
<img width="1919" height="1143" alt="image" src="https://github.com/user-attachments/assets/6ec3dfbb-ea9b-4a51-9445-9d65f35dfe2a" />
En el pantallazo podemos ver a front y rear cpn direcciones de memoria validas, y size con un valor valido, esto demuestra que hay nodos en la cola antes de borrarlos

Luego hundimos F10 para estar encima de la linea "dequeue()" y hundimos F11 para entrar a la funcion donde esta toda la logica de borrado y volvemos a hundir F10
<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/ad5e1bae-1a88-432c-aa5d-db42b1187e62" />
Ahi ya podemos ver que front y rear tienen una direccion de memoria valida y size vale 50 lo que indica que hay un trazo creado

Luego hundimos hasta ejecurar las siguientes dos lineas
```cpp
	delete temp;
	size--;
```
Que son las que borraran un nodo y reduciran el tamaño de la cola
<img width="1919" height="1145" alt="image" src="https://github.com/user-attachments/assets/a9a3f2dd-1549-4644-ad40-6d10beba81b6" />
Como se puede ver front tiene una direccion diferente y size disminuyo a 49, lo que nos demuestra que el nodo fue eliminado y la memoria liberada






 


## Bitácora de reflexión





