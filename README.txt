Al proponernos empezar a armar los diagramas UML primero nos habíamos
dispuesto a hallar las clases más básicas information holder que son aquellas
que más que tener parte de la lógica del programa prácticamente solo contienen
información (Estas siendo User, UserContainer, GameContainer), ya que estas son las
más fáciles de hallar, y que a partir de ellas podíamos empezar a ver otras clases que
además de contener datos los usen y tengan la lógica del programa, comprender como puede
funcionar la lógica de un programa se hace más sencillo si tenemos las bases que contienen
la información. 

A su vez encontramos una clase que era necesaria para el programa, la clase Game. Esta la identficiamos
como un structurer ya que mantiene las relaciones entre User y Boards, guardando informacion
de su relacion, como por ejemplo saber si la primera Board es la del User o es una representacion
de las tiradas al user rival.

Uno de los temas que al principio nos complico era la idea de cómo podíamos conectar 
a dos jugadores y si esto era necesario que estuviera en una clase en especifica o podría 
estar dentro de una de las clases que ya sabíamos eran necesarias y precisaríamos (específicamente game),
decidimos localizarla aparte ya que la lógica que pueda tener dentro de esta no está relacionada 
directamente con las responsabilidades de game, a su vez gracias al documento "Object Design. 
Responsabilities and Collaborations" pudimos identificar que nuestro pensamiento era el correcto ya que en el texto se habla de 
las clases coordinators que son específicas para tener la lógica de coordinación en un proyecto.
Así llegamos a crear la clase Organizer, que se encarga de unir a dos jugadores mediante 
la creación de un game, para hacerlo nos fijamos en la lista de usuarios esperando y 
dependiendo del gamemode que haya seleccionado. Esta clase a partir del evento 
StartGame de que ocasiona un User trata de unir a dos Users, al delegar a la clase Game o GameContainer
la tarea de crear dicho game.

Otro patron dado en clase que aplicamos a los Containers es Singleton, tanto de Container<T>, como en
GameContainer y UserContainer se guarda una instancia privada de _instance, y un metodo estatico
para obtener dicha instancia, de esta forma podemos asegurarnos que en verdad GameContainer y UserContainer
funcionen con una unica instancia.

Una característica que consideramos importante o que al menos resalta en nuestro 
equipo, es que todos somos alumnos que recursamos la materia, gracias a esto el descifrar 
que clases deben hacer la lógica de recibir los mensajes y a partir de ellos no solo 
responder si no que provocar cambios como crear instancias o cambiar valores en clases, deben de
ser los Handlers, cabe destacar que esta idea surgió a partir de la página Refactoring guru, que dedica 
una sección al funcionamiento y las ventajas del uso de Handlers.

Una implementación e idea que nos parecía necesaria y correcta para el código, es que no 
debe haber una espera indefinida en el turno de un usuario, es decir, si es el turno de un
usuario1 y este no juega ni hace ningún movimiento en un tiempo x, entonces el turno del usuario1
debe acabarse y el turno pasar a ser del usuario2. Con esto también se nos viene a mente una 
segunda funcionalidad que podría ser positiva para evitar que los jugadores se cansen de esperar
a que se cancele el turno de un usuario1 AFK, luego de una cierta cantidad de turnos cancelados
automáticamente se termina el juego, siendo el resultado una victoria para el usuario2 y derrota
para el usuario1 AFK.

Para hacer posible la funcionalidad explicada previamente tuvimos que buscar cómo funciona el
concepto de Timer en C#, resulta ser que en C# existe una clase Timer a la que se pueda acceder
mediante el espacio de nombres System.Timers.

A la hora de asignar responsabilidades tuvimos en cuenta los patrones y principios dados en clase,
cuyo autor es Robert C. Martin, en su conocida teoría "Design Principles and Design Patterns".
Los container, tanto UserContainer como GameContainer, guardan todas las instancias de User y Game
respectivamente, según el patrón Creator esta es razón suficiente para darle la responsabilidad a
dichos Container de crear las instancias de las clases que guardan.

En los handlers también se puede destacar la existencia del principio OCP, que básicamente
dicta que una clase debe ser cerrada a la modificación y abierta a la extensión. Esto 
se ve en el atributo Next de cada handler, si en un futuro es necesario agregar nuevas funcionalidades
a la hora de recibir mensajes, se puede simplemente agregar nuevos IHandler que hereden de Basehandler
y no tener que modificar los Handlers que ya existen. A su vez la idea de depender de una abstracción
de un handler en vez del handler mismo encapsula mejor las clases, ya que un handler no conoce en verdad
el funcionamiento del handler que guarda en el atributo Next.

Uno de los patrones más conocidos del libro de Robert es el patrón Expert, este se puede hallar fácilmente
en todo el diagrama, por ejemplo, si los container son aquellos que conocen la lista donde se guardan
instancias de un elemento, también tienen la responsabilidad de agregar y remover elementos de la lista
ya que son los expertos en la información respecto a ella. Otra funcionalidad que cumple con Expert es en
user el GetHitPercentage y GetMissPercentage, ya que user conoce la cantidad total de misses e hits, es
experto en la información necesaria para calcular los porcentajes de cada uno. Y más ejemplos se pueden encontrar
en el resto de las clases, por ejemplo, que sea Organizer quien una a dos usuarios ya que conoce los usuarios
esperando para ser unidos y a que gamemode quieren jugar.

En él los diagramas también tenemos previsto la reutilización de código, esta se puede ver en las clases que heredan
de otras, como en los container, boards, boats, y handlers, usar herencia permite reutilizar código gracias
a que hay código que se toma de la clase ancestro, a menos de que sea escrito con una especificación override.
