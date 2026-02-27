# Unidad 3

## Bitácora de proceso de aprendizaje

### Actividad 1 
#### Notas
```cpp
#include <iostream>

int sum(int a, int b)
{
    return a + b;
}

int main()
{
    int a = 5;
    int b = 7;
    std::cout << "La suma de " << a << " y " << b << " es " << sum(a, b) << "\n";
}
```
#### Parte 1
```cpp
int sum(int a, int b)
{
    return a + b;
}
```
* El int antes del sum indica el tipo de dato que devuelve
* "Return" termina la funcion y envia el resultado a donde fue llamada, que ene ste caso seria el main

#### Pate 2
```cpp
std::cout << "La suma de " << a << " y " << b << " es " << sum(a, b) << "\n";
```
* Se ejecuta primero la funcion de "sum", antes de imprimir en la pantalla

#### Parte 3
Se coloca un breakpoint en:
```cpp
int a = 5;
```
* Cuando presiono F10 estando detenido en la linea anterior, lo que pasa es que se ejecuta esa linea y luego el depurador pasa a la siguiente. En corto, esta ejecutando paso a paso

Lo que pasa en el Autos es lo siguiente:
* Muestra las variables locales del contexto actual, es decir, las que pertenecen a la funcion en la que esta detenido el breakpoint
* En este caso, mostrar a y b del main
* Si estuviera en sum, mostraria los parametros de sum

##### 1. ¿Para qué sirven los breakpoints?
R/= Los breakpoint detienen el programa en un punto especifico y dejan analizar el estado actual del programa antes que continue

##### 2. ¿Para qué se usa la ventana de depuración Autos?
R/= La ventana de Autos muestra las variables locales del punto que esta detenido por el breakpoint en el programa. Y permite observar como cambian sus valores mientras se ejecuta paso a paso



```cpp
#include <iostream>

using namespace std;

// Función que modifica el parámetro pasado por valor
void modificarPorValor(int n) {
    cout << "Dentro de modificarPorValor, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorValor, valor modificado: " << n << endl;
}

// Función que modifica el parámetro pasado por referencia
void modificarPorReferencia(int& n) {
    cout << "Dentro de modificarPorReferencia, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorReferencia, valor modificado: " << n << endl;
}

// Función que modifica el parámetro utilizando punteros
void modificarPorPuntero(int* n) {
    cout << "Dentro de modificarPorPuntero, valor inicial: " << *n << endl;
    *n += 5;
    cout << "Dentro de modificarPorPuntero, valor modificado: " << *n << endl;
}

int main() {
    int a = 10;
    int b = 10;
    int c = 10;

    cout << "Valor inicial de a (paso por valor): " << a << endl;
    cout << "Valor inicial de b (paso por referencia): " << b << endl;
    cout << "Valor inicial de c (paso por puntero): " << c << endl;

    cout << "\nLlamando a modificarPorValor(a)..." << endl;
    modificarPorValor(a);
    cout << "Después de modificarPorValor, valor de a: " << a << endl;

    cout << "\nLlamando a modificarPorReferencia(b)..." << endl;
    modificarPorReferencia(b);
    cout << "Después de modificarPorReferencia, valor de b: " << b << endl;

    cout << "\nLlamando a modificarPorPuntero(&c)..." << endl;
    modificarPorPuntero(&c);
    cout << "Después de modificarPorPuntero, valor de c: " << c << endl;

    return 0;
}
```

### Actividad 2 Notas
### Paso por valor y paso por referencia
```cpp
#include <iostream>

using namespace std;

// Función que modifica el parámetro pasado por valor
void modificarPorValor(int n) {
    cout << "Dentro de modificarPorValor, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorValor, valor modificado: " << n << endl;
}

// Función que modifica el parámetro pasado por referencia
void modificarPorReferencia(int &n) {
    cout << "Dentro de modificarPorReferencia, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorReferencia, valor modificado: " << n << endl;
}

// Función que modifica el parámetro utilizando punteros
void modificarPorPuntero(int *n) {
    cout << "Dentro de modificarPorPuntero, valor inicial: " << *n << endl;
    *n += 5;
    cout << "Dentro de modificarPorPuntero, valor modificado: " << *n << endl;
}

int main() {
    int a = 10;
    int b = 10;
    int c = 10;

    cout << "Valor inicial de a (paso por valor): " << a << endl;
    cout << "Valor inicial de b (paso por referencia): " << b << endl;
    cout << "Valor inicial de c (paso por puntero): " << c << endl;

    cout << "\nLlamando a modificarPorValor(a)..." << endl;
    modificarPorValor(a);
    cout << "Después de modificarPorValor, valor de a: " << a << endl;

    cout << "\nLlamando a modificarPorReferencia(b)..." << endl;
    modificarPorReferencia(b);
    cout << "Después de modificarPorReferencia, valor de b: " << b << endl;

    cout << "\nLlamando a modificarPorPuntero(&c)..." << endl;
    modificarPorPuntero(&c);
    cout << "Después de modificarPorPuntero, valor de c: " << c << endl;

    return 0;
}
```
#### Parte 1 – Paso por valor
Tenemos esta funcion
```cpp
void modificarPorValor(int n) {
    cout << "Dentro de modificarPorValor, valor inicial: " << n << endl;
    n += 5;
    cout << "Dentro de modificarPorValor, valor modificado: " << n << endl;
}
```
Y esta llamada desde el main
```cpp
int a = 10;
modificarPorValor(a);
```
Despues de ejecutar "modificarPorValor(a)"
##### ¿el valor de a en main cambia o sigue siendo 10?
R/= No cambia
En: 
```cpp
void modificarPorValor(int n)
```
* El parametro "n" es una copia del valor que se envia
Cuando haces:
```cpp
n += 5;
```
* Estas modificando la copia, no la variable original "a"
* Entonces dentro de la funcion pasa de 10 a 15
* Fuera de la funcion "a" sigue siendo 10

Si dentro de la función se modifica una copia,
##### ¿por qué la variable original no se ve afectada?
R/= Porque la copia esta en una direccion de memoria diferente, como sellama la direccion de la copia, por eso cambia la copia y no la original
* En resumen, son dos variables distintas, tienen ubicaciones distintas y cambiar una no cambia la otra


#### Parte 2 – Paso por referencia
Ahora mira esta función:
```cpp
void modificarPorReferencia(int &n) {
    n += 5;
}
```
Observa el detalle:
```cpp
int &n
```
* Esto es una referencia, para darle otro nombre a la misma variable
* Entonces si modificamos n, tambien modificamos la variable a la que hace referencia
##### ¿Aquí se crea una copia o no se crea copia?
R/= No se crea una copia

Cuando usas:
```cpp
int &n
```
* "n" se convierte en una alias de la variable originla, es como ponerle oto nombre, pero sigue siendo la misma variable

Pregunta concreta:

Si b = 10 en main y llamas:
```cpp
modificarPorReferencia(b);
```
Después de la llamada…
##### ¿Cuánto vale b?
R/= Valdria 15. Porque como no se creo una copia, y recordemos que "n" es otra forma de llamar a "b", al hacer:
```cpp
n += 5;
```
* Estamos modificando directamente a "b"

#### Parte 3 - Paso por puntero
Ahora mira esta función:
```cpp
void modificarPorPuntero(int *n) {
    *n += 5;
}
```
Y la llamada:
```cpp
modificarPorPuntero(&c);
```
Pregunta directa:
##### ¿Qué se está enviando realmente cuando usamos &c?
R/= Se esta mandando la direccion de memoria de "c"

Dentro de la función:
```cpp
*n += 5;
```
##### El *n significa:
* Ve a la direccion que me enviaron y modifica el valor que esta ahi

Pregunta directa para cerrar esta parte:

Si c = 10 antes de la llamada,
después de ejecutar modificarPorPuntero(&c);
##### ¿Cuánto vale c?
R/= 
* Se paso a la direccio de "c"
* Dentro de la funcion se modifico e valor en esa direccion
* Por eso cambia directamente "c"

##### Un pequeño resumen
* Paso por valor. Genera una copia de la variable original y se modifica el valor de esa copia
* Paso por referencia. Se le crea un nuevo nombre a la variable y cuando se le cambia el valor a esa referencia, cambia el valor de la variable original
* Paso por puntero. El puntero guarda la direccion donde esta el valor de la variable, y luego va a la direccion donde dice el puntero y cambia el valor que este ahi

#### Parte final de reflexion - Implementacion de "swap"
##### swap por Paso por valor
Si intentas hacer un swap usando paso por valor…
##### ¿Crees que las variables originales en main se intercambiarán realmente o no?
R/=
* No porque se crean copias de los valores
* El intercambio ocurre solo dentro de la funcion de "swap"
* Al regresar a "main", las variables originales siguen igual

Imagina esta función (paso por valor):
```cpp
void swapPorValor(int a, int b)
{
    int temp = a;
    a = b;
    b = temp;
}
```
Pregunta concreta:

Si en main tienes:
```cpp
int x = 3;
int y = 8;
swapPorValor(x, y);
```
##### Después de la llamada, ¿cuáles serán los valores de x y y en main?
R/=
* Seguirian teniendo el mismo valor
* El "swapPorValor" crea copias del main, que serian "a" y "b"
* Por ende los que intercambian serian "a" y "b", DENTRO DE LA FUNCION "swapPorValor"
##### El intercambio ocurre AQUI (Solo de las copias)
```cpp
int temp = a;
a = b;
b = temp;
```

##### swap por referencia
Si hacemos el swap por referencia:
```cpp
void swapPorReferencia(int &a, int &b)
{
    int temp = a;
    a = b;
    b = temp;
}
```
Pregunta directa:

Si en main tienes:
```cpp
int x = 3;
int y = 8;
swapPorReferencia(x, y);
```
##### Después de la llamada, ¿cuáles serán los valores de x y y?
R/=
* x=8 y y=3, en el main.
* Porque no se hacen copias
* a y b, son alias, o tras formas de llamar a "x" y "y"
* Por eso el intercambio ocurre directamente sobre las variables originales

##### swap por puntero
Si la función es así:
```cpp
void swapPorPuntero(int *a, int *b)
{
    int temp = *a;
    *a = *b;
    *b = temp;
}
```
Y en main llamas:
```cpp
int x = 3;
int y = 8;
swapPorPuntero(&x, &y);
```
Pregunta final:
##### Después de la llamada, ¿cuáles serán los valores de x y y?
R/=
* x= 8 y y=3
* Se envian las direcciones de x y y
* *a y *b acceden a los valores originales
* El intercambio afecta directamente al main

#### Resumen
##### 1. ¿Qué pasa en paso por valor?
* Se crwan copias de las variables en el main
* Los cambios de valor o intercambio ocurren DENTRO de la funcion de "PasoPorValor"
* Las variables originales no cambian

##### 2. ¿Qué pasa en paso por referencia?
* Se crean alias, o sea, se le ponen otros nombres a las variables originales, pero SIGUEN SIENDO LAS MISMAS
* Los cambios de valor o intercambios ocurren DENTRO de la funcion "PasoPorReferencia" y esto afecta las variables originales

##### 3. ¿Qué pasa en paso por puntero?
* Se pasan las direccin=ones de las variables originales
* Usando el operador "*" se accede al valor en esa direccion
* Las modificaciones en los valores ocurren dentro de la funcion "PasoPorpuntero" y esto afecta directamente el main




```cpp
#include <iostream>

using namespace std;


void swapPorValor(int a, int b) {

    int c = b;
    b = a;
    a = c;

}


void swapPorReferencia(int& a, int& b) {
    
    int c = b;
    b = a;
    a = c;

}


void swapPorPuntero(int* a, int* b) {

    int c = *b;
    *b = *a;
    *a = c;


}

int main() {
    int a = 10;
    int b = 30;

    swapPorValor(a, b);

    cout << "a: " << a << endl;
    cout << "b: " << b << endl;

    return 0;
}
```


### Notas Y conceptos Importantes

#### Que es el Stack?
* Region de memoria que se gestiona automaticamente
* Guarda variables locales
* Guarda parametros de funciones
  -  Los parametros son lo que la funcion espera recibir
* Guarda objetos creados "normalmente"
  - Ej: Persona p1 (Objeto creado normalmente)
  - p1 es un objeto directo (No guarda la direccion de memoria, pero si el objeto completo. El       objeto ocupa la memoria directamente)
  - No usamos new
  - Se guarda en el Stack
  - Se destruye automaticamente cuando termina el bloque
* Se limpia solo cuando sales del bloque o de la funcion
Ejemplo:
```cpp
int x = 10;
```
x vive en el stack
Si haces:
```cpp
void f() {
    int y = 5;
}
```
"y" existe solo mientras f() se está ejecutando. Cuando f() termina desaparece automáticamente.

#### Que es el Heap
* Region de memoria que se gestiona manualmente
* Se usa con new
* NO se limpia automaticamente
* Existe hasta que hagas delete
Ejemplo:
```cpp
int* p = new int;
```
* Aqui "p" vive en el stack
* El "int" creado vive en el heap
Si no haces:
```cpp
delete p;
```
* La memoria queda ocupada
* Eso es una fuga de memoria (Cuando el espacio de memoria queda ocupado y no se libera con el "delete")

#### Diferencias entre objeto stack y objeto heap
##### Objeto en Stack
```cpp
Personaje heroe("Aragorn", 100, 20, 15);
```
Aquí:
* Heroe es el objeto
* Vive en el Stack
* Se destruye automaticamente al salir del bloque
* El destructor se llama solo

##### Objeto en heap
```cpp
Personaje* heroe = new Personaje("Aragorn", 100, 20, 15);
```
Aquí:
* Heroe es un puntero (Puntero guarda la direccion de memoria de otra variable)
* El objeto real vive en Heap
* No se destruye solo
* Hay que hacer:
```cpp
delete heroe;
```

#### Que hace el "new" en C++?
* Reserva memoria en el Heap y devulve la direccion
Ejemplo:
```cpp
int* p = new int;
```
¿Qué ocurre aquí?
* Se reserva espacio en el Heap para un "int"
* "new" devuelve la direccion de esa memoria
* Esa direccion se guarda en "p"
* "p" vive en el Stack
* El "int" vive en el Heap
Visualmente:
```
STACK:          HEAP:
p  --------->   [ ??? ]
```
Si luego haces:
```cpp
*p = 50;
```
Ahora en heap tienes:
```
STACK:          HEAP:
p  --------->   [ 50 ]
```

##### Con objeto
```cpp
Punto* p = new Punto(10, 20);
```
Aquí:
* "p" (puntero) existe en el Stack
* El objeto (Punto) existe en el Heap
* El constructor se ejecuta
* El objeto no se destruira solo

#### Que pasa si no haces "delete"?
Si haces:
```cpp
int* p = new int;
```
pero nunca haces:
```cpp
delete p;
```
Entonces:
* La memoria queda ocupada
* El programa pierde la direccion
* Ya no se puede acceder a ella
* Esa memoria no se puede volver a utilizar
* Se produce una fuga de memoria
Ejemplo:
```cpp
void f() {
    int* p = new int;
}
```
Cuando la función termina:
* "p" desaparece del Stack
* Pero el "int" en Heap sigue ahi
* Ya no tienes como acceder a el
* Fuga de memoria

#### Que es la fuga de memoria?
Ocurre cuando:
* Se reserva memoria en el Heap y se pierde la direccion (Cuando no se libera usando delete)
Ejemplo:
```cpp
for(int i = 0; i < 1000; i++) {
    int* p = new int;
}
```
Cada iteración:
* Reserva memoria
* Nunca la librera
Resultado:
* El programa consume cada vez mas RAM
* Puede volverse lento y colapsar el programa
* Crashear al computador
##### Diferencias importantes
Esto NO es fuga:
```cpp
int x = 5;
```
* Porque "x" vive en el STACK y se borra solo
Esto SÍ puede ser fuga:
```cpp
int* p = new int;
```
* Si no haces "delete"
##### Regla fundamental
* Su usas "new" debes usar "delete"
* Si usas new[], debes usar delete[]
Ejemplo correcto:
```cpp
int* arr = new int[5];
delete[] arr;
```

#### Que es un miembro de una clase?
* Es simplemente una variable que pertenece a la clase
Ejemplo:
```cpp
class Personaje {
public:
    std::string nombre;   // miembro
    int* estadisticas;    // miembro
};
```
* Cada objeto de tipo "Personaje" tendra esos miembros
Por ejemplo, si creas:
```cpp
Personaje p;
```
* Ahora "p" tiene
  - p.nombre
  - p.estadisticas

#### Que pasa cuando copias un objeto que tiene un puntero como miembro?
Supongamos esto:
```cpp
class Ejemplo {
public:
    int* dato;

    Ejemplo(int v) {
        dato = new int(v);
    }
};
```
Y haces:
```cpp
Ejemplo a(10);
Ejemplo b = a;
```
* El compilador crea una copia autoamtica
* PERO copia el puntero, NO copia la memoria apuntada
Entonces:
```
STACK:
a.dato --------\
                 \
                  ----> HEAP: [ 10 ]
                 /
b.dato --------/
```
* Estan apuntando al mismo bloque de memoria

#### Que significa "copia superficial" (shallow copy)?
* Es cuando se copian los valores tal cual
* Incluyendo las direcciones de los punteros
* Pero NO se crea una nueva memoria
Ejemplo:
```cpp
Ejemplo a(10);
Ejemplo b = a;
```
* "b.dato" no tiene su propio "int"
* Solo apunta al mismo "int" de "a"
* Eso es una copia superficial

##### Que seria un copia profunda (deep Copy)?
Sería esto:
```cpp
b.dato = new int(*a.dato);
```
* Ahora cada objeto tiene su propia memoria
* No comparten Heap y son indpendientes uno del otro

#### Que ocurre cuando dos objetos apuntan al mismo bloque de Heap?
##### Problema 1 — Modificación compartida
Si haces:
```cpp
*b.dato = 50;
```
* Tambien cambia "a.dato"
* Porque ambos apuntan al mismo lugar

##### Problema 2 — Double delete
Si agregas destructor:
```cpp
~Ejemplo() {
    delete dato;
}
```
* Se destruye "b" liberando la memoria
* Se destruye "a" liberando la misma memoria y crasheando el codigo

##### Problema 3 — Dangling pointer
* Despues del primer "delete" la memoria ya no es valida
* El segundo objeto tiene un puntero que qpunta a la memoria ya liberada

#### RECORDAR
* Si en una clase tiene un puntero como miembro, el constructor de copia automatica puede ser peligroso, proque  solo copia la direccion de memoria

#### Que pasa cuando una funcion termina (destruccion automatica)?
* Todas las variables locales del Stack se destruyen automaticamente
Ejemplo:
```cpp
void f() {
    int x = 10;
}
```
* Cuando "f()" termina, "x" desaparece
* La memoria del Stack se limpia sola

##### Con objetos
```cpp
void f() {
    Punto p(10, 20);
}
```
* Cunado "f()" termina se llama automaticamente al destructor de "p" y luego se libera la memoria en el Stack

#### Que ocurre si NO defines destructor?
Si tu clase no tiene destructor:
```cpp
class A {
public:
    int x;
};
```
* El compilador crea uno por defecto y destruye los miembros automaticamente
Esto esta bien si:
* Tu clase no usa "new"
* No maneja memoria manual

##### Pero si tu clase usa "ew"
Ejemplo:
```cpp
class A {
public:
    int* p;

    A() {
        p = new int(10);
    }
};
```
Si no defines el destructor:
* La memoria reservada NO sera liberada
* Cada objeto genera una fuga de memoria
* El compilador NO sabe que debe hacer "delete"

#### Que ocurre cuando el compilador genera el constructor de copia por defecto?
Si no defines constructor de copia:
```cpp
A b = a;
```
* El compilador genera uno automaticamente
* El constructor copia miembro por miembro
* Hace copia superficial
* Copia punteros como direcciones
* NO crea nueva memoria
Ejemplo:
```cpp
class A {
public:
    int* p;
};
```
Si haces:
```cpp
A a;
A b = a;
```
Entonces:
* "b.p = a.p"
* Ambos apuntan al mismo bloque







## Bitácora de aplicación 



## Bitácora de reflexión













