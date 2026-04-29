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
* glBufferData copia los datos del arreglo vertices hacia la memoria de la GPU usando el VBO
* El VBO es el bloque de memoria dentro de la GPU donde se guardan los vertices
* Esos vertices son esos numeros en rojo que se ven en el depurador

<br><br>

<img width="952" height="1113" alt="image" src="https://github.com/user-attachments/assets/c5f38dca-0a7c-43d5-a6a8-79d4880df816" />
* glVertexAttribPointer define cómo OpenGL debe interpretar los datos del VBO y los asocia con el atributo location 0 del vertex shader
* En este caso, cada vertice esta formado por 3 valores float correspondientes a las coordenadas x,y,z

<br><br>

<img width="954" height="962" alt="image" src="https://github.com/user-attachments/assets/008929b8-2305-4a38-ab15-0ec25db6cdda" />

* glDrawArrays envía la orden de dibujo a la GPU utilizando los datos previamente configurados en el VAO y el VBO ( glDrawArrays, es quien da la orden final a la GPU de dibujar)

* El flujo de datos inicia en el arreglo vertices, luego glBufferData copia esa información al VBO en la GPU

* Luego, glVertexAttribPointer especifica cómo deben interpretarse esos datos y los conecta con el atributo aPos del vertex shader mediante el location 0

* Finalmente, glDrawArrays utiliza esa configuración para ejecutar el pipeline gráfico y dibujar el triángulo

* GL_TRIANGLES indica wue lo vertices son un triangulo


#### Evidencia 3

<img width="951" height="1143" alt="image" src="https://github.com/user-attachments/assets/1c7e9be8-bd2f-445e-a6e6-dbd6c43e2546" />

* El arreglo vertices mantiene valores constantes durante toda la ejecución del programa.

<br><br>

<img width="953" height="1141" alt="image" src="https://github.com/user-attachments/assets/161266e8-22b9-40bc-a201-1d956836a48a" />

* El uniform offset recibe valores dinámicos calculados con glfwGetTime(), permitiendo modificar la posición del triángulo sin alterar el VBO
* En la segunda imagen vemos esto:
```
float x = sin(time) * 0.5f;
float y = cos(time) * 0.5f;

Y luego esto

glUniform2f(offsetLoc, x, y);
```
* Lo que significa que el triangulo se esta moviendo, porque X y Y cambia, por los valores de X y Y que se ven en la ventana autos
* El movimiento de X y Y no viene del arreglo de vertices, solo se hace un desplazamiento, pero los vertices siguen siendo los mismo, porque si cambiara, la figura del triangulo cambiaria

<img width="960" height="1103" alt="image" src="https://github.com/user-attachments/assets/1e859378-5807-4bee-b839-610704acb32e" />

* Un ejemplo de como cambian si sigo avanzando en el programa


<br><br>

<img width="959" height="1137" alt="image" src="https://github.com/user-attachments/assets/1b990059-c386-4a1c-9997-b529306b39db" />

* El uniform ourColor modifica el color del fragment shader dinámicamente usando valores calculados con funciones seno y coseno
* En la ventana autos se pueden ver los valores r y g como cmabian constantemente, eso demuestra el cambio visual mediante uniforms y no modificando el arreglo de ninguna manera

<img width="952" height="1138" alt="image" src="https://github.com/user-attachments/assets/f6066b98-9d24-4350-be76-ebfe244f8af0" />

* Estos eran los valores de g y r antes de llegar al breakpoint, lo que demuestra que van cambiado por cada loop


<br><br>

<img width="1919" height="1141" alt="image" src="https://github.com/user-attachments/assets/83c256c6-79ce-43f7-9ce3-4f4dfa89edba" />
* Color antes

* 

<img width="1366" height="754" alt="image" src="https://github.com/user-attachments/assets/6e039605-ce1e-4541-b503-ea394fbadff3" />
* Color despues

<br><br>

* Los uniforms permiten modificar variables del shader sin alterar los datos almacenados en el VBO. El VBO conserva siempre las mismas coordenadas del triángulo, pero los uniforms offset y ourColor cambian continuamente durante la ejecución. Esto permite modificar la posición y el color del triángulo en tiempo real sin necesidad de volver a cargar los vértices en la GPU  


#### Evidencia 4

<img width="1919" height="883" alt="image" src="https://github.com/user-attachments/assets/cbc84e04-56cd-4d7e-be33-36c7a8dfac47" />

* Esta "layout(location = 1)" lo que nos esta diciendo es que quiere recibir los vertices por el canal 1, per el VBO "glVertexAttribPointer(0, ...)" dice que envia los datos por el canal 0. Lo que pasa es que el shader y el VBO ya no se comunian por el mismo canal
* El shader nunca recibe las coordenadas de x,y y z, por lo que no puede construir el triagulo

* Esperaba que el triángulo dejara de renderizarse correctamente porque el atributo del vertex shader ya no coincide con el location configurado en glVertexAttribPointer.

* Por ende es obvio decir que los canales o locations deben coincidir entre el shader y la configuración del VAO/VBO. 


#### Evidencia 5

<img width="715" height="501" alt="image" src="https://github.com/user-attachments/assets/612ff4b4-bf18-42cf-96a4-086d4b0aaf57" />

<img width="521" height="576" alt="image" src="https://github.com/user-attachments/assets/83ddb97a-52b6-4de2-a966-0088297f766f" />

* Se decidio utilizar uniforms proque el triangulo si iba a mantener igual durante todo el funcionamiento del sistema, solo se moveria al rededor del canvas y cambiaria de color dinamicamente durante ese tiempo, pero los vertices y la forma del triangulo se mantendrian iguales
* Los atributos se usan cuando los verties neesitan datos distintos, mientras que los uniform son variables globales para hacer cambios en el shader



```
```

<br><br>




## Bitácora de reflexión
