# Proyecto Aspiradora - Versión-003-MVC


En esta versión del proyecto, el código fue transformado para adoptar el patrón de diseño Modelo-Vista-Controlador (MVC). Este patrón de arquitectura divide el proyecto en tres componentes interconectados, pero claramente diferenciados, lo cual simplifica la gestión del código y mejora su mantenibilidad, escalabilidad y posibilidad de prueba.

## Descripción del Patrón MVC
El patrón Modelo-Vista-Controlador (MVC) divide la arquitectura del proyecto en tres segmentos interrelacionados pero distintos: Modelo, Vista y Controlador. Esta transformación facilita la gestión del código al separar las responsabilidades de manejo de datos, presentación de la interfaz de usuario y lógica de control.

## Componentes del Patrón MVC

### Modelo
El **Modelo** comprende las clases que manejan la lógica de negocio y los datos del sistema:
- **Aspiradora**: Administra el estado y comportamientos de la aspiradora, como su posición, nivel de batería y su capacidad de basura.
- **Gato**: Encapsula el comportamiento y estado del gato, permitiéndole moverse y ensuciar la habitación.
- **Habitación**: Mantiene la estructura de la habitación, incluyendo ubicaciones de muebles y los azulejos.
- **Posición**: Almacena coordenadas específicas dentro de la habitación para objetos móviles.
- **Batería**: Gestiona el nivel de carga de la aspiradora.
- **CapacidadBasura**: Controla la acumulación de basura en la aspiradora hasta que se requiere su vaciado.
- **Azulejo**: Representa cada segmento del suelo de la habitación, manteniendo su nivel de suciedad.
- **Dimensión**: Define las dimensiones espaciales de la habitación.

### Vista
La **Vista** maneja la presentación de la información, es decir, cómo se muestra el estado del modelo al usuario:
- **VistaAspiradora**: Muestra información sobre el estado actual de la aspiradora, como la carga de la batería y si la bolsa de basura está llena.
- **VistaGato**: Muestra acciones del gato, como la suciedad que deja en la habitación.
- **VistaHabitacion**: Visualiza la disposición de la habitación, incluyendo la posición de la aspiradora, el gato, y la distribución de muebles y suciedad.
- **Consola**: Proporciona una interfaz de línea de comandos para interactuar con el usuario, recogiendo inputs y mostrando resultados.
- **Utils**: Contiene funciones utilitarias que ayudan en tareas comunes dentro de las vistas, como validar entradas del usuario.

### Controlador
El **Controlador** actúa como intermediario entre el modelo y la vista, manejando la entrada del usuario y actualizando el modelo según esta información:
- **ControladorAspiradora**: Gestiona la lógica relacionada con el movimiento y operación de la aspiradora y actualiza el modelo correspondientemente.
- **ControladorGato**: Maneja la lógica para mover al gato dentro de la habitación de acuerdo con las reglas definidas.
- **ControladorHabitacion**: Coordina las interacciones entre la aspiradora, el gato, y la habitación, gestionando el flujo del programa y las actualizaciones necesarias en la vista basadas en el estado del modelo.


Esta separación entre la lógica de negocio, la interfaz de usuario y el control del flujo de la aplicación facilita el mantenimiento y la escalabilidad del código del proyecto, ya que cada componente puede ser modificado independientemente del otro. Además, esta estructura promueve una mayor eficiencia en el desarrollo, permitiendo que diferentes miembros del equipo trabajen en paralelo en distintas partes del proyecto.


# Cambios Específicos en el Código
| Clase                | Versión-003                                                                                                                                         | Versión-003-MVC                                                                                                                                                      |
|---|---|---|
| **Habitacion**       | `Habitacion` gestionaba tanto la estructura como la lógica de impresión y generación de muebles.                                                         | `Habitacion` se centra únicamente en la estructura de la habitación, mientras que la lógica de impresión se delega a `VistaHabitacion` y la generación de muebles y demás lógica a `ControladorHabitacion`.  |
| **Aspiradora**       | `Aspiradora` gestionaba directamente su estado y comportamientos, incluyendo la posición, nivel de batería y capacidad de basura.                        | `Aspiradora` sigue gestionando su estado, pero ahora interactúa con la vista a través de `VistaAspiradora` y la lógica de movimiento se maneja en `ControladorAspiradora`. |
| **Elementos**        | `Elementos` contenía los diferentes elementos de impresión y era una clase simple y poco utilizada.                                                                         | `Elementos` se ha integrado en `Utils`, donde proporciona funciones utilitarias para tareas comunes.                                                              |
| **Gato**             | `Gato` gestionaba su posición y comportamientos directamente dentro de la clase, incluyendo la lógica de movimiento y ensuciar.                          | `Gato` sigue gestionando su posición, pero ahora la lógica de movimiento y ensuciar se maneja en `ControladorGato`.                                               |
| **Dimension**        | La dimensión de la habitación se solicitaba y gestionaba directamente dentro de la clase `Habitacion` a través de un metodo dentro de la clase `Dimension`.                                                    | `Dimensión` ahora es una clase separada que define las dimensiones espaciales de la habitación, y no gestiona la entrada de datos del usuario, mejorando la separación de responsabilidades y la cohesión.        |

