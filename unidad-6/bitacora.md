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








<br><br>



## Bitácora de aplicación 


## Bitácora de reflexión
