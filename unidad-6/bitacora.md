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



## Bitácora de aplicación 


## Bitácora de reflexión
