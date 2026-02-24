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
* 


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

### Actividad 2
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


