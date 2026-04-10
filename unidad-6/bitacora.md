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
* Presionamos la tecla a para que se pare en el breakpoint

<br><br>
<br><br>


Y extendemos la parte observers que se ven en la ventana Autos
<br><br>
<img width="848" height="183" alt="image" src="https://github.com/user-attachments/assets/639f589b-2da9-44db-a995-5e91e3d3cbd5" />
<br><br>
**¿Cuántos elementos tiene?**
* Hay 115 elementos
<br><br>
**¿Qué tipo de objetos son**
* Son de tipo 0x...
<br><br>
**¿A qué direcciones de memoria apuntan?**
<img width="344" height="355" alt="image" src="https://github.com/user-attachments/assets/a0d10f9e-fe58-45de-8cf0-075e2358584a" />
<br><br>
* En la imagen podemos ver el **tipo de cada elemento dentro del vector** "observers"
* Lo que significa que estos elementos son un puntero a **Observers**, pero en realidad apuntan a un objeto de tipo **Particle**
* En resumen, apuntan a la direccion de memoria donde esta almacenado el objeto tipo **Particle**
<br><br>
<br><br>

mnvorwhbrio[s



<br><br>



## Bitácora de aplicación 


## Bitácora de reflexión
