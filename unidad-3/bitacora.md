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
* a y v, son alias, o tras formas de llamar a "x" y "y"
* 


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


## Bitácora de aplicación 



## Bitácora de reflexión








