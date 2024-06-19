# Proyecto Aspiradora - Versión 1(Diseño)

+ En esta version se explica como fue que se empezó a crear la idea de la aspiradora, teniendo en cuenta el enunciado y sus requerimientos, se fue creando un modelo del dominio para tener una imagen mas clara de como se abordaría el problema.

+ Tambien se crearon las diferentes relaciones que existen entre todas las clases

## Explicación más a fondo

### Estrategias de clasificación

#### Descripcion informal del problema
Imagina que tienes un cuarto de 25x10 con zonas limpias y sucias (hasta 4 niveles de suciedad). Queremos poner una aspiradora que se mueva al azar en todas las direcciones sin atravesar paredes ni muebles.La aspiradora limpiará las zonas sucias al pasar sobre ellas, reduciendo la suciedad nivel por nivel. Además, contará con una batería limitada que le permite moverse y una bolsa de basura que, al llenarse, requiere vaciarse antes de seguir limpiando.De vez en cuando, aparecerá un gato que ensuciará el área mientras camina al azar y luego desaparecerá.El juego termina hasta que la aspiradora termine de limpiar por completo la habitación.

#### Análisis clásico y modelo del dominio 
[Modelo del dominio](https://github.com/MRSergio21/23-24-IdSw2-SDD/tree/feature/version001/img#modelo-del-dominio-aspiradora-version-001)

#### Análisis de comportamiento 
- **Aspiradora**:Representa la aspiradora que está en la habitacion.Sus responsabilidades son:
     - **Obtener** su posicion, sus pasos realizados y el nivel de bateria.
     - **Asignar** la bateria y los pasos realizados.
     - **Limpiar** la suciedad que haya en la habitación.
- **Azulejo**:Representa todos los azulejos que hay en la habitacion, limpios o sucios.Sus responsabilidades son:
     - **Obtener** su nivel de suciedad.
     - **Asignar** su nivel de suciedad.
- **Elements**:Almacena todas los elementos que pueden existir en la habitación.Sus responsabilidades son:
     - **Obtener** el valor de cada elemento.
- **Gato**:Representa el gato que está en la habitacion.Sus responsabilidades son:
     - **Obtener** su posicion y sus pasos realizados.
     - **Asignar** los pasos realizados.
     - **Pasear** alrededor de la habitación y ensuciar.
 - **Habitación**:Representa la habitación.Sus responsabilidades son:
     - **Obtener** la matriz.
 - **Posición**:Gestiona la posición de cada elemento adentro de la habitación.Sus responsabilidades son:
     - **Obtener** su posicionX y posicionY.
     - **Asignar** la posicionX y la posicionY.
#### Interacciones y Flujo de Trabajo
- **Inicialización**:El sistema inicia creando una matriz con los parámetros ya definidos, en la que podemos definir como la habitación.
- **Cierre**:El sistema para de crear la matriz una vez se terminó su creación.

### Relaciones entre clase
Una clase que contiene las 4 relaciones de colaboración es la clase Azulejo:
- **Composición**:Una Habitacion está compuesta por múltiples Azulejo. Si una Habitacion es destruida, todos los Azulejo que contiene también se destruirán.
- **Agregación**:Un Azulejo puede tener un Elemento asociado. Azulejo y Elementos pueden existir independientemente.
- **Asociación**:Un Azulejo tiene una relación con Gato,indicando que un Gato puede estar en un Azulejo específico.
- **Uso**:Un Azulejo depende de Posicion para saber dónde está ubicado en la Habitacion.



  


