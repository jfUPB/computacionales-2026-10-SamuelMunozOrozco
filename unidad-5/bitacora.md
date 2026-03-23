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
* La parte "Figura:" significa que hereda los atributos y funciones de la clase "Figura"
* Ejemplo: El circulo hereda el atributo Nombre de la clase Figura

#### Polimorfismo en el codigo
```csharp
foreach (Figura fig in misFiguras)
{
    fig.Dibujar();
}
```
* **fig** es tipo **Fidura**
* Pero puede ser Circulo o Rectangulo

Como sabe el prohrama que figura dibujar?

* El programa guarda en la memoria el *8tipo real del objeto**, no el tipo de variable

Ejemplo:
```csharp
Figura fig = new Circulo(5.0);
```
* Lo que pasa es que en la **memoria** se crea un objeto tipo Circulo
* Aunque la variable sea "Figura" el objeto sigue siendo un circulo

Entonces cuando se llama a:
```csharp
fig.Dibujar();
```
* El programa mira el objeto en la memoria
* Ve que ese objeto dice "Circulo"
* Y ejecuta: "**Circulo.Dibujar()**"


#### Parte 3

##### 1. Memoria y Herencia
Cuando creas un objeto Rectangulo, este tiene Base, Altura y también Nombre. ¿Cómo te imaginas que se organizan esos tres datos en la memoria del computador para formar un solo objeto?

* R/= La memoria lo guarda todo en un mismo grupo, no los pone separados como un lado altura en otro base. Se crea el bloque de memoria con el nombre y este contiene los atributos de la figura que sea; esto tambien incluye a los atributos heredados

#### 2. El mecanismo del polimorfismo

Pensemos de nuevo en la llamada fig.Dibujar(). El compilador solo sabe que fig es una Figura. ¿Cómo decide el programa, mientras se está ejecutando, si debe llamar al Dibujar del Circulo o al del Rectangulo? Lanza algunas ideas o hipótesis.
* R/= Cuando hay varios objetos. Ejemplo:
```csharp
List<Figura> misFiguras = new List<Figura>();

misFiguras.Add(new Circulo(5.0));
misFiguras.Add(new Rectangulo(4.0, 6.0));
misFiguras.Add(new Circulo(10.0));
```
* Decide usando el:
```csharp
foreach (Figura fig in misFiguras)
{
    fig.Dibujar();
}
```
* El programa lo que hace es ejecutar lo que este dentro del ciclo, como dentro del ciclo hay tres figuras, ejecuta esas tres figuras en el orden que esten escritas en el codigo







## Bitácora de aplicación 


## Bitácora de reflexión
