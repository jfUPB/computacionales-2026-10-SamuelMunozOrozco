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

### Que teniamos que hacer
* Crear dos nuevas funciones de particle, yo cree una que se mueve en espiral o que oscila antes de explotar, la segunda era que cambiaba de color hasta que explota
* Lo segundo, era crear un nuevo tipo de explosion, yo cree una explosion en cruz, que las particulas solo van en horizontal y vertical

### Explicacion codigo 

#### SpiralParticle
```cpp
class SpiralParticle : public Particle {
protected:
	glm::vec2 position;
	glm::vec2 velocity;
	ofColor color;
	float lifetime;
	float age;
	bool exploded;
	float angle;

public:
	SpiralParticle(const glm::vec2& pos, const glm::vec2& vel,
		const ofColor& col, float life)
		: position(pos), velocity(vel), color(col),
		lifetime(life), age(0), exploded(false), angle(0) {}

	void update(float dt) override {
		age += dt;
		angle += dt * 5;

		position.x += cos(angle) * 100 * dt;
		position.y += velocity.y * dt;

		velocity.y += 9.8f * dt * 6;

		float explosionThreshold = ofGetHeight() * 0.15f;

		if (position.y <= explosionThreshold || age >= lifetime) {
			exploded = true;
		}
	}

	void draw() override {
		ofSetColor(color);
		ofDrawCircle(position, 8);
	}

	bool isDead() const override { return exploded; }
	bool shouldExplode() const override { return exploded; }
	glm::vec2 getPosition() const override { return position; }
	ofColor getColor() const override { return color; }
};
```

##### 1. Heredamos de Particle
```cpp
class SpiralParticle : public Particle
```
* Hereda de la clase Particle

<br><br>

##### 2. Atributos
```cpp
glm::vec2 position;
glm::vec2 velocity;
ofColor color;
float lifetime;
float age;
bool exploded;
float angle;
```
* **position:** Donde esta la particula
*  **velocity:** La velocidad de la particula
*  **Color:** Color de la particula
*  **lifetime:** Cuanto dura antes de explotar la particula
*  **age:** cuanto duro antes de explotar
*  **exploded:** Confirma si ya exploto
*  **angle:** Este controla la espiral (**Preguntele mas a chat sobre esta**)
<br><br>

##### 3. Constructor
```cpp
SpiralParticle(const glm::vec2& pos, const glm::vec2& vel,
		const ofColor& col, float life)
		: position(pos), velocity(vel), color(col),
		lifetime(life), age(0), exploded(false), angle(0) {}
```
* Inicializa todo en la clase
<br><br>

##### 4. update()
```cpp
age += dt;
```
* Aumenta el tiempo de vida

<br><br>

```cpp
angle += dt * 5;
```
* Hace que la particula gire
* En cada frame aumenta el angulo
* **Preguntele mas a chat**

<br><br>

```cpp
position.x += cos(angle) * 100 * dt;
```
* Mueve en x usando coseno
* Crea un movimiento lateral, que seria en espiral

<br><br>

```cpp
position.y += velocity.y * dt;
```
* Movimeinto en vertical, solo sube

<br><br>

```cpp
velocity.y += 9.8f * dt * 6;
```
* Gravedad de la particula

<br><br>

```cpp
float explosionThreshold = ofGetHeight() * 0.15f;
```
* Altura donde explota

<br><br>

```cpp
	if (position.y <= explosionThreshold || age >= lifetime) {
			exploded = true;
```
* Condicion de la explocion
  - Si llego a la altura o se acabo su tiempo, explota
 
<br><br>

##### 5. draw()
```cpp
ofDrawCircle(position, 8);
```
* Dibuja la particula

<br><br>

##### 6. Meotodos finales
```cpp
isDead()
shouldExplode()
getPosition()
getColor()
```



### Fase 2

#### Evidencia 1. Herencia en memoria
<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/c193e39a-a19d-475c-b54c-aa0b3546950b" />
* El breakpoint lo ponemos en la linea "particles[i]->update(dt);", porque en ese punto el programa ya creo las particulas, que estan almacenadas en el vector particles
* En la imgen se puede ver lo siguiente: 
  - particles[i]: Que es un puntero de tipo Particle (**Mejor explicacion a chat**)
  - SpiralParticle: Que contiene los atributos de la la clase SpiralParticle
  - Particle: Aparece como parte del objeto, lo que demuestra que contiene la clase base
  - _vfptr: Que es la tabla de funciones virtuales (**Mejor explicacion**)

* Cada atributo en el Autos, pertenece a la clase derivada SpiralParticle, mientras la clase base esta ahi como parte de la jerarquia heredada
* En Autos se demuestra que la memoria tiene la clase base particle y los atributos de la clase derivada SpiralParticle. Esto demuestra que la herencia se esta aplicando, organizando los datos en la memoria, como una combinacion de la clase base y la clase derivada, todo dentro de un mismo objeto


<br><br>

#### Evidencia 2. La _vtable de tu nuevo tipo
<img width="1919" height="1146" alt="image" src="https://github.com/user-attachments/assets/b52b49ea-2de7-46d2-8cd0-e09c3e2070c1" />
* Volvemos a poner el breakpoint aqui ya que necesitamos una particula creada, y nos permite revisar las funciones virtuales
* Ahora vamos a "particles[i]" y expandimos "_vfptr"
* En el campo "_vfptr" es un puntero de la tabla de funciones virtuales "vtable". Al expandirlo podemos ver uan lista de direcciones que corresponden a los metodos virtuales del objeto
  - update()
  - draw()
  - isDead()
  - shouldExplode()
  - getPosition()
  - getColor()

* Estas funciones pertenecen a la implementacion especifica de la clase del objeto, que en este caso es SpiralParticle

##### Comparacion con RisingPaticle
<img width="1919" height="1142" alt="image" src="https://github.com/user-attachments/assets/99e96ea5-99ee-4291-862b-13c49f4358a8" />
* Hacemos lo mismo que en el anterior, pero ahora sacamos un tipo diferente de particula, en este caso RisingParticle usando la tecla "**q**"






## Bitácora de reflexión
