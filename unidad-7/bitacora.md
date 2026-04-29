# Unidad 7

## Bitácora de proceso de aprendizaje


## Bitácora de aplicación 

### Evidencias

#### Evidencia 1

La secuencia de inicializacion comienza con GLFW, porque es la libreria encargada de crear la ventana de la aplicacion y el contexto OpenGL. EL contexto es necesario para que el rpograma pueda usar funciones graficas y comunicarse correctamente con la GPU.

* Primero se ejecuta glfwInit();. Esta funcion inicializa GLFW y prepara la libreria para crear ventanas y manejar eventos
* Se crea la ventana con glfwCreateWindow(...);
* Despues de activa el contexto OpenGl asociado a esa ventana usando glfwMakeContextCurrent(mainWindow);
* Solo cuando el contexto OpenGL esta activo se puede ejecutar gladLoadGLLoader(...);

<br><br>

GLAD debe salir despues de GLFW, porque es el encargado de cargar las direcciones de ;as funciones de OpenGL, y para poder obtener esas funciones, necesita un contexto de OpenGL ya activo. GLFW se encarga de crear la ventana, manejar el contexto de OpenGL, procesar entradas de teclado y eventos.


#### Evidencia 2

<img width="850" height="843" alt="image" src="https://github.com/user-attachments/assets/334b2f7c-b670-49cc-93af-0c60b2d842e6" />
* Aca en el arreglo de vertices se puede ver como almacena las coordenadas del triangulo y cada grupo de tres representa un vertice formado

<br><br>

<img width="837" height="1084" alt="image" src="https://github.com/user-attachments/assets/568113ad-626b-4751-b6fb-95dedf1e5b17" />
* glBufferData copia los datos del arreglo vertices hacia la memoria de la GPU usando el VBO (decirle a chat que explique esto mejor, que porque se ven los numeros rojos y que son esos VBO y VAO)

<br><br>

<img width="952" height="1113" alt="image" src="https://github.com/user-attachments/assets/c5f38dca-0a7c-43d5-a6a8-79d4880df816" />
* (Mandarle a chat las imagenes y preguntare si si es buena evidencia y si que explique ciertos conceptos, como las funciones del vertex shader y eso )
* glVertexAttribPointer define cómo OpenGL debe interpretar los datos del VBO y los asocia con el atributo location 0 del vertex shader.

<br><br>

<img width="954" height="962" alt="image" src="https://github.com/user-attachments/assets/008929b8-2305-4a38-ab15-0ec25db6cdda" />
* glDrawArrays envía la orden de dibujo a la GPU utilizando los datos previamente configurados en el VAO y el VBO. (Lo mismo, que te explique bien la evidencia y lo que se muestra en el depurador y si eso ecuenta como evidencia)

* El flujo de datos inicia en el arreglo vertices definido en C++. Posteriormente, glBufferData copia esa información al VBO en la GPU.

* Luego, glVertexAttribPointer especifica cómo deben interpretarse esos datos y los conecta con el atributo aPos del vertex shader mediante el location 0.

* Finalmente, glDrawArrays utiliza esa configuración para ejecutar el pipeline gráfico y dibujar el triángulo.


#### Evidencia 3

<img width="955" height="1144" alt="image" src="https://github.com/user-attachments/assets/e572aeb8-d847-411b-8865-26cd00740aa1" />
* El arreglo vertices mantiene valores constantes durante toda la ejecución del programa.

<br><br>

<img width="953" height="1141" alt="image" src="https://github.com/user-attachments/assets/161266e8-22b9-40bc-a201-1d956836a48a" />
* El uniform offset recibe valores dinámicos calculados con glfwGetTime(), permitiendo modificar la posición del triángulo sin alterar el VBO. (preguntarle a chat si es suficiente, como los valores de x y Y demuestran que no cambian los valores de los vertices en el arreglo)

<br><br>

<img width="959" height="1137" alt="image" src="https://github.com/user-attachments/assets/1b990059-c386-4a1c-9997-b529306b39db" />
* El uniform ourColor modifica el color del fragment shader dinámicamente usando valores calculados con funciones seno y coseno. (Lo mismo, dime como justifica esto como evidencia si no muestra nada de el arreglo)

<br><br>

<img width="1919" height="1141" alt="image" src="https://github.com/user-attachments/assets/83c256c6-79ce-43f7-9ce3-4f4dfa89edba" />
* Color antes

* 

<img width="1366" height="754" alt="image" src="https://github.com/user-attachments/assets/6e039605-ce1e-4541-b503-ea394fbadff3" />
* Color despues

<br><br>

* Aunque el arreglo de vértices nunca cambia, el resultado visual sí cambia porque los uniforms permiten enviar nuevos valores a los shaders en cada frame.

* Los uniforms permiten modificar variables del shader sin alterar los datos almacenados en el VBO. 

* En este proyecto, el VBO conserva siempre las mismas coordenadas del triángulo, pero los uniforms offset y ourColor cambian continuamente durante la ejecución.

* Esto permite modificar la posición y el color del triángulo en tiempo real sin necesidad de volver a cargar los vértices en la GPU.

(Pedir a chat que explique bien estas evidencias, y por el amor de Dios, pongalo en sus palabras)





```
```

<br><br>




## Bitácora de reflexión
