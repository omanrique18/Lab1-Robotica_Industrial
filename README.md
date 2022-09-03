# Lab1-Robotica_Industrial
## Herramienta
### Requerimientos

- Se considera que el proceso de escribir sobre un tablero no demanda mayor fuerza por parte del robot, por ende no es necesario disenar una pieza muy robusta. Ademas, con el fin de proteger el plato de herramientas, se desea que la herramienta sea de un material que se quiebre primero en caso de una colision con el terreno.

- Desde un inicio se planeo el uso de manufactura aditiva para la construccion de la herramienta, por ello a fin de tener una pieza que pueda manufacturarse rapidamente se disena un ensamble por modulos independientes, en lugar de un cuerpo extremadamente largo que cubra todo el marcador y demande mas material y tiempo.

- Como requerimiento adicional, se planteo la posibilidad de usar cualquier marcador.

### Diseno

1. Se obtienen las medidas del plato.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255761-7a032375-5bba-4724-a306-019b0d183db9.png" width="350" />
</p>

2. Se disena una base que se pueda acoplar a el. Se introduce un chaflan para aliviar los esfuerzos en el cambio de seccion. Los cuatro orificios de la parte superior se usan para introducir tornillos que permitan sujetar y centrar el marcador.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255705-3b2e7c10-181e-4e69-9842-74887cd20712.png" width="350" />
</p>
  
2. Se disena una pieza capaz de centrar el marcador desde su base y que se deslice por el interior de la pieza anterior. Se introduce una esponja en el espacio hueco a fin de que funcione como resorte, evitando que la punta se hunda a lo largo de las rutinas del robot.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255706-8d5e0051-c4dd-4eff-bee2-130795648ac2.png" width="350" />
</p>

3. La Ultima pieza es para centrar la punta del marcador. Los cuatro orificios se unen mediante elasticos a los 4 tornillos que centran el marcador.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255710-2c1b5f1a-7eed-4356-8156-d73d78be2a66.png" width="350" />
</p>

4. Se ensamblan todas las piezas, completando la herramienta.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255713-7929af34-80ef-4e43-b921-f9b3ba3759f3.jpeg" width="350" />
  <img src="https://user-images.githubusercontent.com/51519737/188255830-32e11ec3-5663-4ac4-9709-f4cfb4c19a05.jpeg" width="350" />
</p>

## Modelado de las letras

Se modela una placa donde se hace un bajo relieve con las iniciales de los miembros del grupo Juan y Oscar. Posteriormente esta se traslada a robot estudio donde se generan las rutas que dibujan los contornos de las letras.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255854-99336b9f-5b1c-4f6a-bb84-96dc97885940.png" width="350" />
</p>

## RobotStudio

Se definen 3 rutas, una dibuja la jota en su totalidad, y las otras dos las O, siendo una el contorno interno y la otra el externo. Adicionalmente se define una herramienta que solo tiene un desfase en z respecto al marco del plato.

Al momento de definir la ruta, primero se crea el objeto de trabajo y su marco de referencia segun la posicion de la pieza de grabado insertada, luego se alinean los puntos de la trayectoria de tal suerte que el marcador siembre es normal a la superficie. 

Por ultimo se define un punto de Home, nosotros definimos (0,0,0,0,30,0). Anteriormente se define (0,0,0,0,0,0) pero se presentan problemas de ejecucion como se evidenciara posteriormente.

Luego sincronizamos el programa y en el main se llaman los bloques que dibujan cada una de las trayectorias mencionadas, finalmente se pone la orden de Home al inicio y final del main y se hace la simulacion antes de pasar a un entorno real.

/Lab1-Robotica_Industrial/videos/SimulacionRS.mp4

## Calibracion de la herramienta

1. Se instala la herramienta en el plato del manipulador.

2. Haciendo uso del FlexPendant, mediante movimientos lineales en una orientacion dada se acerca la punta de la herramienta a un soporte metalico ubicado en el suelo y se registra el punto obtenido.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255880-ec82ff74-9d91-4114-b305-385c01687ac0.png" width="350" />
</p>

3. Se repite el procedimiento 3 veces mas en diferentes orientaciones y se guardan los puntos obtenidos.

4. Se guarda la herramienta y se registra en el FlexPendant bajo el nombre de "Panfilo"

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255908-d5d108c9-888c-4ab2-b9c0-9e5e5b6c1318.png" width="350" />
</p>

## WorkObject

1. Se fija la superficie sobre la cual se va a sibujar al piso con cinta adhesiva.

2. Se acerca la punta de la herramienta a la esquina superior izquierda de la superficie y se guarda el punto. Se repite el procedimiento con la esquina superior e inferior derecha en ese orden.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255926-1c874e9a-70d8-4813-88aa-b257abcb82ab.png" width="350" />
  <img src="https://user-images.githubusercontent.com/51519737/188255927-079497fd-90d1-43fa-866c-01c8df465a1f.png" width="350" />
  <img src="https://user-images.githubusercontent.com/51519737/188255928-3ec0adde-eb71-4beb-b33d-09024d390b53.png" width="350" />
</p>

3. Se guarda el WorkObject obtenido.

## Ejecucion de rutina

Se descarga el programa RAPID en el FlexPendant mediante una USB y se da inicio a la rutina. En el primer intento el marcador se seco, por lo que fue necesario reemplazarlo. Dado que no se tenia un destornillador en el momento de la practica el segundo marcador quedo flojo y por eso se evidencia una deformacion en las letras dibujadas.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255952-6888dff8-966c-4103-aca6-d0e9a14d6de0.png" width="350" />
</p>


En el segundo intento se realizo una modificacion a la rutina, creando una ruta al home (0,0,0,0,0,0). Esto genero inconvenientes durante la ejecucion a causa de la singularidad que genera este punto, causando mensajes de advertencia en el FlexPendant y pausando la rutina repetidas veces.

<p align="center">
  <img src="https://user-images.githubusercontent.com/51519737/188255954-2c7621d2-cfb5-41f4-9934-1f2bf700a651.png" width="350" />
</p>


## Integrantes
- Juan Andres Bueno Hortua
- Oscar Javier Manrique Merchan

## Profesores
- Ricardo Emiro Ramirez Heredia
- Jhoan Sebastian Rodriguez Rodriguez
