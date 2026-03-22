# Unidad 5
## Bitácora de proceso de aprendizaje

### Actividad 1

* ¿Qué es el encapsulamiento?
  - Es una forma de proteger datos dentro del programa. Ejemplo: hacer una función privada para que otro codigo externo no pueda acceder a ella sin permiso

* ¿Qué es la herencia?
  - Cuando una cla hereda caracteristicas o atributos de otra. Tambien se dice que una clase padre le herede datos a otras clases hijas

* ¿Qué es polimorfismo?
  - Es cuandoun mismo método se pueda comportar de diferentes formas, según el objeto
 
#### Encapsulamiento en el codigo
Tenemos las siguientes dos opciones de encapsulamiento
```csharp
private string nombre;
```
```csharp
public string Nombre
{
    get { return nombre; }
    protected set { nombre = value; }
}
```
* Directo al punto, la segunda es la mas segura, porque permite controlar el acceso al atributo "name" ya que solo se puede leer pero no modificar
* "nombre" es private para que nadie acceda a su valor y Nombre es publico paraque se pueda leer y se tenga un control sobre quien accede o no al valor


#### Herencia en el codigo
```csharp
public class Circulo : Figura
```







## Bitácora de aplicación 


## Bitácora de reflexión
