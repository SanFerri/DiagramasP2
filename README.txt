Al proponernos empezar a armar los diagramas UML primero nos habiamos
dispuesto a hallar las clases mas basicas struct que son aquellas
que mas que tener parte de la logica del programa practicamente solo contienen
informacion (Estas siendo User, UserContainer, GameContainer), ya que estas son las
mas faciles de hallar, y que a partir de ellas podiamos empezar a ver otras clases que
ademas de contener datos los usen y tengan la logica del programa. 

Uno de los temas que al principio nos complico era la idea de como podiamos conectar 
a dos jugadores y si esto era necesario que estuviera en una clase en especifica o podria 
estar dentro de una de las clases que ya sabiamos eran necesarias y precisariamos (especificamente game),
decidimos localizarla aparta ya que la logica que pueda tener dentro de esta no esta relacionada 
directamente con las responsabilidades de game, a su vez gracias al documento (NOSE) 
pudimos identificar que nuestro pensamiento era el correcto ya que en el texto se habla de 
las lases coordinators que son especificas para tener la logica de coordinacion en un proyecto.
Asi llegamos a crear la clase Organizer, que se encarga de unir a dos jugadores mediante 
la creacion de un game, para hacerlo nos fijamos en la lista de usuarios esperando y 
dependiendo del gamemode que halla seleccionado.

Una caracteristica que consideramos importante o al menos que resalta en nuestro 
equipo, es que todos somos alumnos que recursamos la materia, gracias a esto el descifrar 
que clases deben hacer la logica de recibir los mensajes y a partir de ellos no solo 
responder si no que provocar cambios como crear instancias o cambiar valores en clases, deben de
ser los Handlers, cabe destacar que esta idea surgio a partir de la pagina Refactoring guru, que dedica una seccion
a el funcionamiento y las ventajas del uso de Handlers.

Una implementacion e idea que nos parecia necesaria y correcta para el codigo, es que no 
debe haber una espera indefinida en el turno de un usario, es decir, si es el turno de un
usuario1 y este no juega ni hace ningun movimiento en un tiempo x, entonces el turno del usuario1
debe acabarse y el turno pasar a ser del usuario2. Con esto tambien se nos viene a mente una 
segunda funcionalidad que podria ser positiva para evitar que los jugadores se cansen de esperar
a que se cancele el turno de un usuario1 AFK, luego de una cierta cantidad de turnos cancelados
automaticamente se termina el juego, siendo el resultado una victoria para el usuario2 y derrota
para el usuario1 AFK.

Para hacer posible la funcionalidad explicada previamente tuvimos que buscar como funciona el
concepto de Timer en C#, resulta ser que en C# existe una clase Timer a la que se pueda acceder
mediante el espacio de nombres System.Timers.