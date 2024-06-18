# Proyecto Aspiradora - Versión 2

## Estrategias de clasificación
En esta rama **Feature/Version002** se continuó trabajando en la refactorizacion del modelo de dominio y el diagrama de estados generado con anterioridad en la version 1, tomando como base el *Análisis clásico* de las *estrategias de clasificación*, ademas la primera etapa de desarrollo de practicas de *clean code*. Para esta refactorizacion se tomaron en cuenta cosas, objetos físicos o grupos de objetos, lugares físicos y sitios que son tangibles para diagramar apropiadamente las clases. 


## Relaciones entre clases por colaboración

### Relación entre Gato y Posicion:
**Antigua**:  ```Gato --> Posicion```
Esta relación era una relación de uso (dependencia), lo que indica que Gato utiliza la clase Posicion pero no la posee.

**Actualizada**:  ```Gato -- Posicion```
Esta relación es una asociación simple, lo que indica que hay una relación más fuerte entre Gato y Posicion en comparación con la relación de uso. Esto indica que Gato tiene una referencia directa y permanente a Posicion, ya que el gato necesita tener una posicion dentro de la habitación.

Además de los cambios en las relaciones por colaboración, se realizaron modificaciones significativas en las clases mismas. 

| Clase                | Versión Antigua                                                                                                                                          | Versión Actualizada                                                                                                                                             |
|----------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Habitacion**       | ```class Habitacion { Azulejo [][] superficie boolean [][] muebles int ancho int largo } ```                                                     | ```class Habitacion { Habitacion(int ancho, int largo) void imprimir(Aspiradora aspiradora, Gato gato) void imprimirBordeHorizontal() boolean generarMuebles(boolean[][] muebles) Azulejo[][] generarSuperficie(int ancho, int largo, int porcentajeSuciedad) } ``` |
| **Azulejo**          | ```class Azulejo { int nivelSuciedad Posicion posicion boolean tieneMueble } ```                                                                | ```class Azulejo { Azulejo(int nivelSuciedad) int getNivelSuciedad() void setNivelSuciedad(int nivelSuciedad) } ```                                     |
| **Aspiradora**       | ```class Aspiradora { int pasosRealizados int limpiezaRealizada CapacidadBasura capacidadBasura Bateria bateria Posicion posicion } ```          | ```class Aspiradora { Aspiradora() Posicion getPosicion() void mover(Habitacion habitacion) void limpiarCasilla(Habitacion habitacion, int x, int y) } ``` |
| **Elementos**        | ```class Elementos { String value } ```                                                                                                          | ```class Elementos { Elementos(String value) String getElement() void setElement(String elemento) } ```                                                |
| **Gato**             | ```class Gato { Posicion posicion int pasosRealizados } ```                                                                                     | ```class Gato { Gato(int x, int y) Posicion getPosicion() void mover(Habitacion habitacion) } ```                                                      |
| **Posicion**         | ```class Posicion { int x int y } ```                                                                                                            | ```class Posicion { Posicion(int x, int y) int getX() int getY() void setPosicion(int x, int y) void setX(int x) void setY(int y) } ```                |
| **Bateria**          | ```class Bateria { int nivelBateria } ```                                                                                                        | ```class Bateria { void descarga() void carga() int getNivelBateria() int setNivelBateria() } ```                                                      |
| **CapacidadDeBasura**| ```class CapacidadDeBasura { int nivelBasura int maximoNivelBasura } ```                                                                        | ```class CapacidadBasura { CapacidadBasura(int maximoNivelBasura) void rellenarBolsa() void vaciarBolsa() int getNivelBasura() } ```                    |

Para esta version se tomaron en cuenta los siguientes pasos para realizar la segunda iteracion del modelo de dominio propuesto:

1. Listar las clases conceptuales candidatas.
2. Representarlas en el modelo de dominio de partida.
3. Añadir las asociaciones necesarias para registrar las relaciones.
4. Añadir los atributos que satisfagan los requisitos de información.
5. Iterar... 

### Clean Code

Se realizaron diversas mejoras significativas en el código base del proyecto. En la clase Aspiradora, se mejoró la legibilidad adoptando nombres más descriptivos y eliminando código muerto. En **CapacidadBasura**, se mantuvo consistencia con estándares de nomenclatura y estructura de clase. **Gato** experimentó mejoras en la claridad del código al refactorear métodos para evitar duplicaciones y mantener la coherencia. La clase **Posicion** se actualizó para mejorar el formato y la legibilidad del código relacionado con la gestión de posiciones en el contexto de la habitación. Finalmente, en **Habitacion**, se implementaron estándares consistentes de formato y se eliminaron fragmentos de código obsoleto, mejorando la mantenibilidad y claridad general del código.


| Buenas Prácticas       | Detalles de Mejora                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------------|
| **Legibilidad**        | Mejora del formato, eliminamos comentarios innecesarios y adoptamos nombres descriptivos.                     |
| **Nombrado**           | Utilización de nombres descriptivos, estándar CamelCase, evitando ambigüedades.         |
| **Formato**            | Se establecieron estándares de formato y nomenclatura consistentes en todo el código. Mantuvimos indentación y espacios en blanco consistentes, declaramos variables cerca de su uso. |
| **Estandares**         | Especificamos normas para la estructura del código y la nomenclatura, facilitando la consistencia.         |
| **Consistencia**       | Mantuvimos estándares a lo largo del proyecto para asegurar coherencia en el estilo de codificación.       |
| **Código Muerto**      | Eliminamos fragmentos de código obsoleto y comentarios innecesarios.                                      |
| **DRY (Don't Repeat Yourself)** | Refactorizacion para reutilizar código y evitar duplicaciones. |
| **YAGNI (You Aren't Gonna Need It)** | Evitamos agregar funcionalidades no requeridas, manteniendo el enfoque en los requisitos actuales.       |


# Versiones

<div align=center>

|pyAspiradora|Ver Versiones|
|-|:-:|
|Version 1|[👁️📒](https://github.com/MRSergio21/23-24-IdSw2-SDD/tree/feature/version001)|
|Version 3|[👁️📒](https://github.com/MRSergio21/23-24-IdSw2-SDD/tree/feature/version003)|
|Version 3 - MVC|[👁️📒](https://github.com/MRSergio21/23-24-IdSw2-SDD/tree/feature/version003-mvc)|
|Version 4|[👁️📒](https://github.com/MRSergio21/23-24-IdSw2-SDD/tree/main)|

</div>
