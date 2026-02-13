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
<img width="1548" height="823" alt="image" src="https://github.com/user-attachments/assets/62932b1e-91b5-4023-823f-c6560b9af431" />
<img width="1546" height="827" alt="image" src="https://github.com/user-attachments/assets/24a0bc2e-7a89-482f-a3ad-d8372aa3d11e" />
<img width="1549" height="829" alt="image" src="https://github.com/user-attachments/assets/275e4cce-1203-48c6-b506-9cecbc4aa92c" />


















## Bitácora de reflexión









