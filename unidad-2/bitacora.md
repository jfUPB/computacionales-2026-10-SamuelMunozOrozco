# Unidad 2

## Bitácora de proceso de aprendizaje

### Actividad 1
<img width="1509" height="815" alt="image" src="https://github.com/user-attachments/assets/485e63c0-8452-424e-838f-a4603fa1017e" />

<img width="1248" height="483" alt="image" src="https://github.com/user-attachments/assets/45e0538c-b63a-4686-aef3-318a697e5b34" />

### Actividad 2
<img width="1250" height="477" alt="image" src="https://github.com/user-attachments/assets/e157f4df-13da-4c2a-8e35-54745eeed335" />

<img width="1498" height="815" alt="image" src="https://github.com/user-attachments/assets/1856a050-9c8a-4132-a644-b88eb3abf4d5" />



### Actividad 3
<img width="1287" height="792" alt="image" src="https://github.com/user-attachments/assets/365b93c5-eb38-4358-b7d3-d65bd30669d2" />

<img width="1514" height="571" alt="image" src="https://github.com/user-attachments/assets/4f36b95a-a052-4b85-8fec-71ce2b2eaa09" />

<img width="1742" height="662" alt="image" src="https://github.com/user-attachments/assets/469d043b-ade5-4a6f-aa24-cc7cafd79b76" />

### Actividad 5
<img width="1600" height="827" alt="image" src="https://github.com/user-attachments/assets/25db83ee-75bd-4b8c-a665-552c06e05be1" />

<img width="1254" height="751" alt="image" src="https://github.com/user-attachments/assets/8373457e-2836-479c-9c60-07ccd7d3d8c6" />


<img width="1585" height="802" alt="image" src="https://github.com/user-attachments/assets/d1db9866-f6d0-4cf3-af2b-9d6280cfa99f" />

<img width="1270" height="653" alt="image" src="https://github.com/user-attachments/assets/1d13e5d6-9e3f-4e5d-87cf-5af73b09dd84" />

### Actividad 6

### Actividad 7

## Bitácora de aplicación 

### Actividad 8
#### Capturas codigos
<img width="1491" height="805" alt="image" src="https://github.com/user-attachments/assets/c23dc0e3-2e76-4f91-b402-35d619748f70" />
* Primero se creamos las variables las cuales guardaran los valores 10 y 20, que seran "a" y "b" y guardamos si posicion en la RAM
  
* Luego procedemos a darles estos valores a las variables

<img width="1496" height="807" alt="image" src="https://github.com/user-attachments/assets/86d416d7-574a-412c-b821-bc611e4dc64b" />
* Ahora hacemos la logica del intercambio o swap
  
* Hacemos que A guarde la direccion de "a" y hacemos que D tome esa direccion
  
* Ponemos R0 y y igualamos M=D para que asi esa direccion se guarde en R0
  
* Y hacemos exactamente lo mism con "b", es exactamente lo mismo, lo unico que cambiamos es "a" por "b" y R0 por R1
  
* Luego guardamos la direccion del retorno, que valga la redundancia, es lo mismo, solo cambiamos "a" por "returnFromSwap" y R0 por R15
<img width="1491" height="802" alt="image" src="https://github.com/user-attachments/assets/26a67687-bf50-405a-972b-3ff2fbcfa0b5" />
* A carga la direccion guardada en R0

* D=M carga el valor de "a"

* Luego ponemos R13 como registro temporal y igualamos M=D para que guarde el valor de "a temporalmente mientras hacemos el cambio"

* Luego A carga la direccion de "b" y la ponemos en D

* Luego ponemos R0 y cargamos la direccion de "a" en la memoria

* Y por ultimo al igualar M=D cargamos el valor de "b" en "a"
<img width="1485" height="306" alt="image" src="https://github.com/user-attachments/assets/e4b24468-0421-482e-a250-dd8f2955a26b" />
* Por ultimo seleccionamos la memoria temporal R13

* Copiamos el valor temporal en el registro D y seleccionamos R1 para que luego A tenga la direccion de "b"

* Y por ultimo igualamos M=D para asi guardar el valor temporal en b. Y asi se intercambian los valores de a y b

#### Capturas CPU Emulator
##### Aqui evidenciamos los resultados del codigo
<img width="1548" height="823" alt="image" src="https://github.com/user-attachments/assets/62932b1e-91b5-4023-823f-c6560b9af431" />
* Podemos ver en las direcciones de memoria RAM 16 y 17 que tienen los valores respectivos de a y b
<img width="1546" height="827" alt="image" src="https://github.com/user-attachments/assets/24a0bc2e-7a89-482f-a3ad-d8372aa3d11e" />
* En esta, en la direccion numero 13, podemos ver la memoria temporal que guarda el valor de a
<img width="1548" height="793" alt="image" src="https://github.com/user-attachments/assets/34312339-63a8-414b-93b1-2963dbf0bd95" />
* Aqui vemos como en la direccion 16, toma el valor de b
<img width="1549" height="829" alt="image" src="https://github.com/user-attachments/assets/275e4cce-1203-48c6-b506-9cecbc4aa92c" />
* Por ultimo, se ev idencia el cambio, ahora a tiene el valor de b y b tiene el valor de a

## Bitácora de reflexión

### Actividad 9
<img width="1552" height="799" alt="image" src="https://github.com/user-attachments/assets/6366de09-37a8-4b55-a73f-1f21c6ed47ca" />
* Se puede ver en el SCREEN que se dibuja la figura, no se ve en el pantallazo, por pronlemas tecnicos, pero esta habilitado el poder oprimir las teclas, cuando se oprime la tecla d sale el codigo 100
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/8a7a6ee2-fe3a-4916-855c-0f14fe1df292" />
* lafigura esta en la esquina superior izquierda
<img width="1543" height="848" alt="image" src="https://github.com/user-attachments/assets/326c7af2-d2ee-4b34-a2fc-9ecbafe0405c" />
* Aqui se puede ver como desaparece la figura y igual, esta habilitado el teclado y cuando se oprime e sale el codigo 101
<img width="1280" height="960" alt="image" src="https://github.com/user-attachments/assets/e1e8d65d-59a3-4925-9b86-6e81214ac1b7" />

#### La imagen de la figura
<img width="1707" height="853" alt="image" src="https://github.com/user-attachments/assets/3907ab4a-9706-4a8d-ba2b-5fc4e0ee51d8" />

#### Codigo del Bitmap
```jack
function void draw(int location) {
	var int memAddress; 
	let memAddress = 16384+location;
	// column 0
	do Memory.poke(memAddress, 4);
	do Memory.poke(memAddress +32, 14);
	do Memory.poke(memAddress +64, 31);
	do Memory.poke(memAddress +96, 14);
	do Memory.poke(memAddress +128, 4);
	return;
}
```

#### Codigo ensamblador
```asm
// PROGRAMA PRINCIPAL
// d = dibujar
// e = borrar

(START)
    @LOOP
    0;JMP

// LOOP PRINCIPAL
(LOOP)
    @24576        // KBD
    D=M

    // tecla 'd' (ASCII 100)
    @100
    D=D-A
    @DRAW
    D;JEQ

    @24576        // volver a leer teclado
    D=M

    // tecla 'e' (ASCII 101)
    @101
    D=D-A
    @ERASE
    D;JEQ

    @LOOP
    0;JMP

// RUTINA DIBUJAR BITMAP (5 filas)
(DRAW)
    // memAddress = SCREEN (16384)
    @16384
    D=A
    @addr
    M=D

    // Fila 1 -> 4
    @4
    D=A
    @addr
    A=M
    M=D

    // Fila 2 -> 14
    @addr
    D=M
    @32
    D=D+A
    @addr
    M=D
    @14
    D=A
    @addr
    A=M
    M=D

    // Fila 3 -> 31
    @addr
    D=M
    @32
    D=D+A
    @addr
    M=D
    @31
    D=A
    @addr
    A=M
    M=D

    // Fila 4 -> 14
    @addr
    D=M
    @32
    D=D+A
    @addr
    M=D
    @14
    D=A
    @addr
    A=M
    M=D

    // Fila 5 -> 4
    @addr
    D=M
    @32
    D=D+A
    @addr
    M=D
    @4
    D=A
    @addr
    A=M
    M=D

    @LOOP
    0;JMP

// RUTINA BORRAR BITMAP (5 filas)
(ERASE)
    @16384
    D=A
    @addr
    M=D

    @5            // número de filas
    D=A
    @counter
    M=D

(CLEAR_LOOP)
    @addr
    A=M
    M=0

    // addr += 32
    @addr
    D=M
    @32
    D=D+A
    @addr
    M=D

    @counter
    M=M-1
    D=M
    @CLEAR_LOOP
    D;JGT

    @LOOP
    0;JMP

```




















