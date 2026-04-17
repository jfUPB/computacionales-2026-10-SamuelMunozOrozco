# Unidad 6

## Bitácora de proceso de aprendizaje

### Actividad 2

#### INVESTIGACIÓN DEL PATRÓN OBSERVER

Ponemos un breakpoint en la siguiente parte:
```cpp
void Subject::notify(const std::string & event) {
    for (Observer * observer : observers) {   // 🔴 BREAKPOINT AQUÍ
        observer->onNotify(event);
    }
}
```
Lo que podemos ver en la ventana Autos es lo siguiente:

<br><br>

<img width="1836" height="432" alt="image" src="https://github.com/user-attachments/assets/5b13e7df-4573-4b4f-96a9-67a9bcb9deeb" />

<br><br>

##### preguntas 

* ¿Cuántos elementos tiene?
  - Tiene 115 elementos

<br><br>
*  ¿Qué tipo de objetos son?
  - En el pantallazo aparece algo como "Observer* {Particle}"
  - Lo que significa que son punteros que apuntan al objeto **Particle**

<br><br>
* ¿A qué direcciones de memoria apuntan?
  - Apuntan a las direcciones de memoria de cada **Particle**

<br><br>
<br><br>

Ahora para la siguiente evidencia ponemos el breakpoint en la siguiente parte del codigo:

<br><br>
```cpp
void Particle::onNotify(const std::string & event) {  // 🔴 breakpoint
	if (event == "attract") {
		setState(new AttractState());
	} else if (event == "repel") {
		setState(new RepelState());
	} else if (event == "stop") {
		setState(new StopState());
	} else if (event == "normal") {
		setState(new NormalState());
	}
}
```
<br><br>
<br><br>

* ¿Cuál es la dirección de memoria del objeto this que recibe la llamada?
  - La siguiente:
    <img width="782" height="49" alt="image" src="https://github.com/user-attachments/assets/83d024f1-6784-4393-a06b-901dead4f729" />

	<br><br>
* ¿Puedes encontrar esa misma dirección en el vector observers que observaste antes?
  - Si, si puedo, es la primer particula
  <img width="1280" height="221" alt="image" src="https://github.com/user-attachments/assets/a793f1f7-05dc-4b94-bd3d-628c516f2f11" />

<br><br>
* ¿Qué concluyes sobre cómo el Subject sabe a quién notificar?
  - Sabe a quien notificar porque almacena punteros tipo "(Observers*)" en el vector **Observers**, lo que contiene las direcciones de memoria de los objetos **Particle**. Al recorrer el vector llama la funcion **"onNotify"** sobre cada puntero y el subject se encarga de recorrer esas direcciones y que cada objeto ejecute su funcion
  - Sabe a quien notificar porque se almacenan punteros de tipo (Observers*) en el vector "observers", lo que contiene las direcciones de memoria de cada objeto "Particle", al el "Subject" recorrer el vector "observers", tiene las direcciones de cada objeto y mediante losp unteros ejecuta la funcion **onNotify** en cada objeto, para que asi cada objeto reaccione cuando ocurra un evento

<br><br>
<br><br>

#### Investigación del patrón State

Ponemos el breakpoint en la siguiente parte
```cpp
void Particle::setState(State * newState) {
    if (state) {                     // 🔴 BREAKPOINT AQUÍ
        state->onExit(this);
        delete state;
    }
    state = newState;
    if (state) {
        state->onEnter(this);
    }
}
```
* Presionamos la letra "a" que corresponde a "attract" y miramos lo que sae en Autos

<br><br>
<img width="1807" height="305" alt="image" src="https://github.com/user-attachments/assets/34a2a94f-11e4-4d98-9d03-aff428444fa3" />
* Si nos fijamos en la parte "state" podemos ver que las particulas estan en estado normal, a pesar de haber hundido la tecla "a" que corresponde a "attract", esto significa que aun no ha entrado en ese estado
* Luego avanzamos en el programa hundiendo F10 hasta la linea
```cpp
state = newState;
```
Pasando primero por la linea 
```cpp
delete state;
```
* Al llegar a la linea de "delete" esto hace que se elimine el estado anterior para asi poder pasar al siguiente
* Entonces esto se ve cuando llegamos a la linea de "state = newState;" y la ejecutamos
<img width="1918" height="950" alt="image" src="https://github.com/user-attachments/assets/0db7dd9e-90d2-45d3-a0c4-4737d718a2dd" />
* En la imagen podemos ver que el state cambio y ahora no es Normal, sino attract

<br><br>
<br><br>

Para la siguiente parte ponemos dos breakpoints en las siguientes partes
```cpp
void NormalState::update(Particle * particle) {   // 🔴 BREAKPOINT
    particle->position += particle->velocity;
}
```
```cpp
void AttractState::update(Particle * particle) {   // 🔴 BREAKPOINT
    ofVec2f mouse(ofGetMouseX(), ofGetMouseY());
    steer(particle, mouse, 0.05f, 3.0f, 0.2f);
}
```

<br><br>
 ¿A cuál llega el depurador primero en cada caso?
 * En la ventana Autos podemos ver que al hundir "n" llega primero a NormalState
<img width="1919" height="1137" alt="image" src="https://github.com/user-attachments/assets/df834223-f561-4777-b7ff-b0455fe8b779" />

<br><br>
* Cuando hundimos a se puede ver como dentro de "this", State cambia a AttractState
<img width="1913" height="1140" alt="image" src="https://github.com/user-attachments/assets/1b552c24-a47c-4272-b2ed-b654a82b8ac3" />

<br><br>
¿Cómo demuestra esto que el patrón State usa polimorfismo para cambiar el comportamiento en tiempo de ejecución?
* Por la siguiente linea:
```cpp
state->update(this);
```
* Esta es la encargada de hacer que el estado actual cumpla su funcion y dependiendo de la tecla que presione, esta linea actualizara el comportamiento de las particulas en tiempo de ejecucion
* "state" lo que hace es apuntar a la funcion que se debe ejecutar. Ejemplo, si estamos en NormalState, apunta a NormalState:update y lo mismo en AttractState, si estamos ahi, se apunta a AttractState:update
* Tambien en el depurador podemos observar que _vptr apunta a la _vtable correspondiente a un tipo real del objeto

<br><br>
<br><br>

#### Investigación del patrón Factory

<br><br>

<img width="1918" height="1146" alt="image" src="https://github.com/user-attachments/assets/6a1f1a6d-9ecc-4ea8-beeb-77b96597572e" />
* Aqui podemos ver como el objeto se acaba de crear pero no ha sido inicializado, por eso no tiene una direccion de memoria, por asi decirlo, normal

<br><br>

<img width="1918" height="1139" alt="image" src="https://github.com/user-attachments/assets/abd8d301-799f-4292-9187-b3e520ba96ca" />
* Ya tenemos la direccion de memoria y su tipo, que es "star"
* El objeto ya tiene datos validos y fue configurado segun su tipo

<br><br>

<img width="1919" height="1138" alt="image" src="https://github.com/user-attachments/assets/c058d0a2-0b9b-485c-b888-ddc7e604d9b7" />
* Aqui tenemos la direccion de p que es igual a la que tenemos en factory
*
¿Qué relación tienen las direcciones de los objetos creados con los elementos del vector?
* R/= La direccion creada en "ParticleFactory::createParticle" es la misma que se almacena en el vector "particles en ofApp::setup"
* Esto demuestra que no se crean copias del objeto, sino que se trabaja con puntero a la misma instancia en memoria

<br><br>

## Bitácora de aplicación 

### Evidencia 1 — Tu nueva partícula en la Factory
<img width="1919" height="954" alt="image" src="https://github.com/user-attachments/assets/08387b4f-a52f-4ee8-a719-7a07b25028fd" />

* Como podemos ver en la imagen, en el Autos, podemos ver que la variable type tiene de valor "comet", lo que significa que se creo correctaente la particula
* Tambien en la parte de arriba al extender particles, podemos ver todos los valores de la nueva particula 

<br><br>
### Evidencia 2 — Tu nuevo estado en la _vtable
<img width="1919" height="1138" alt="image" src="https://github.com/user-attachments/assets/0f9c5e36-90b3-48cf-bcf2-11cdbf599289" />



<br><br>

<img width="1916" height="1139" alt="image" src="https://github.com/user-attachments/assets/d0df56fa-90d5-4dac-93dc-902052a65b34" />


<br><br>
* En cada pantallazo podemos ver en la ventana Autos, al expandir this, que la variable "_vptr" tienen direcciones de memoria diferentes, lo que indica que cada uno apunta a una tabla virtual diferente
* La entrada que cambia en la "_vtable" es la del metodo "update()" ya que cada estado cambia como se implementa este metodo
* Una entrada es una posicion en la tabla virtual que guarda la direccion de una funcion

<br><br>
### Evidencia 3 — La cadena Observer → State completa
<img width="1919" height="1141" alt="image" src="https://github.com/user-attachments/assets/64137237-c6fa-428a-99f8-7535974c22c9" />
* En este primer pantallazo, podemos evidenciar como el nuevo evento llega a onNotify














## Bitácora de reflexión
