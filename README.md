# Proyecto Aspiradora - Versión 2 (Continuación de Diseño - Relaciones y Clean Code)

## Estrategias de clasificación
En esta rama **Feature/Version002** se continuó trabajando en la refactorizacion del modelo de dominio y el diagrama de estados generado con anterioridad en la version 1, tomando como base el *Análisis clásico* de las *estrategias de clasificación*, ademas la primera etapa de desarrollo de practicas de *clean code*. Para esta refactorizacion se tomaron en cuenta cosas, objetos físicos o grupos de objetos, lugares físicos y sitios que son tangibles para diagramar apropiadamente las clases. 


## Relaciones entre clases por colaboración

### Relación entre Gato y Posicion:
**Antigua**:  ```Gato --> Posicion```
Esta relación era una relación de uso (dependencia), lo que indica que Gato utiliza la clase Posicion pero no la posee.

**Actualizada**:  ```Gato -- Posicion```
Esta relación es una asociación simple, lo que indica que hay una relación más fuerte entre Gato y Posicion en comparación con la relación de uso. Esto indica que Gato tiene una referencia directa y permanente a Posicion, ya que el gato necesita tener una posicion dentro de la habitación.

Además de los cambios en las relaciones por colaboración, se realizaron modificaciones significativas en las clases mismas. 

### Habitacion
**Versión Antigua**
```java
class Habitacion {
    Azulejo [][] superficie;
    boolean [][] muebles;
    int ancho;
    int largo;
}
```

**Versión Actualizada**
```java
class Habitacion {
    Habitacion(int ancho, int largo);
    void imprimir(Aspiradora aspiradora, Gato gato);
    void imprimirBordeHorizontal();
    boolean generarMuebles(boolean[][] muebles);
    Azulejo[][] generarSuperficie(int ancho, int largo, int porcentajeSuciedad);
}
```

### Azulejo

**Versión Antigua**
```java
class Azulejo {
    int nivelSuciedad;
    Posicion posicion;
    boolean tieneMueble;
}

```
**Versión Actualizada**
```java
class Azulejo {
    Azulejo(int nivelSuciedad);
    int getNivelSuciedad();
    void setNivelSuciedad(int nivelSuciedad);
}
```
### Aspiradora
**Versión Antigua**
```java
class Aspiradora {
    int pasosRealizados;
    int limpiezaRealizada;
    CapacidadBasura capacidadBasura;
    Bateria bateria;
    Posicion posicion;
}
```

**Versión Actualizada**
```java
class Aspiradora {
    Aspiradora();
    Posicion getPosicion();
    void mover(Habitacion habitacion);
    void limpiarCasilla(Habitacion habitacion, int x, int y);
}
```
### Elementos
**Versión Antigua**
```java
class Elementos {
    String value;
}

```

**Versión Actualizada**
```java
class Elementos {
    Elementos(String value);
    String getElement();
    void setElement(String elemento);
}
```

### Gato
**Versión Antigua**
```java
class Gato {
    Posicion posicion;
    int pasosRealizados;
}


```

**Versión Actualizada**
```java
class Gato {
    Gato(int x, int y);
    Posicion getPosicion();
    void mover(Habitacion habitacion);
}

```


### Posicion
**Versión Antigua**
```java
class Posicion {
    int x;
    int y;
}
```

**Versión Actualizada**
```java
class Posicion {
    Posicion(int x, int y);
    int getX();
    int getY();
    void setPosicion(int x, int y);
    void setX(int x);
    void setY(int y);
}
```

### Bateria
**Versión Antigua**
```java
class Bateria {
    int nivelBateria;
}
```

**Versión Actualizada**
```java
class Bateria {
    void descarga();
    void carga();
    int getNivelBateria();
    int setNivelBateria();
}
```

### CapacidadDeBasura
**Versión Antigua**
```java
class CapacidadDeBasura {
    int nivelBasura;
    int maximoNivelBasura;
}
```

**Versión Actualizada**
```java
class CapacidadBasura {
    CapacidadBasura(int maximoNivelBasura);
    void rellenarBolsa();
    void vaciarBolsa();
    int getNivelBasura();
}
```

Para esta version se tomaron en cuenta los siguientes pasos para realizar la segunda iteracion del modelo de dominio propuesto:

1. Listar las clases conceptuales candidatas.
2. Representarlas en el modelo de dominio de partida.
3. Añadir las asociaciones necesarias para registrar las relaciones.
4. Añadir los atributos que satisfagan los requisitos de información.
5. Iterar... 

### Clean Code

Se realizaron diversas mejoras significativas en el código base del proyecto. En la clase [**Aspiradora**](https://github.com/MRSergio21/23-24-IdSw2-SDD/commit/b48729fd7982bb3e25edac652efcb2b941b062dd), se mejoró la legibilidad adoptando nombres más descriptivos y eliminando código muerto. En **CapacidadBasura**, se mantuvo consistencia con estándares de nomenclatura y estructura de clase. **Gato** experimentó mejoras en la claridad del código al refactorear métodos para evitar duplicaciones y mantener la coherencia. La clase **Posicion** se actualizó para mejorar el formato y la legibilidad del código relacionado con la gestión de posiciones en el contexto de la habitación. Finalmente, en **Habitacion**, se implementaron estándares consistentes de formato y se eliminaron fragmentos de código obsoleto, mejorando la mantenibilidad y claridad general del código.

| Buenas Prácticas       | Detalles de Mejora                                                                                      |
|------------------------|--------------------------------------------------------------------------------------------------------|
| **Legibilidad**        | Se adoptaron nombres más descriptivos y significativos para variables y métodos, también se eliminaron comentarios innecesarios y confusos, favoreciendo un [código autoexplicativo](https://github.com/MRSergio21/23-24-IdSw2-SDD/commit/2c7a354d416bf2a5cb0359e63549729542af9b62). Ademas, se establecieron estándares de formato consistentes, como la indentación y el uso adecuado de espacios en blanco|
| **Estándares**         | Especificamos normas para la estructura del código y la nomenclatura, facilitando la consistencia.         |
| **Consistencia**       | Mantuvimos estándares a lo largo del proyecto para asegurar coherencia en el estilo de codificación.       |
| **Código Muerto**      | Se eliminaron fragmentos de código obsoleto, como métodos no utilizados y [comentarios innecesarios](https://github.com/MRSergio21/23-24-IdSw2-SDD/commit/8bbe4647851099af8b41f097e9c39efd7fa95cb8). Las clases fueron simplificadas, eliminando atributos y métodos que ya no eran necesarios.|
| **DRY (Don't Repeat Yourself)** | Se refactorizaron métodos para evitar la duplicación de código y promover la reutilización. Se crearon métodos específicos para funcionalidades compartidas, como la generación de muebles en la clase **Habitacion**. |
| **YAGNI (You Aren't Gonna Need It)** | Evitamos agregar funcionalidades no requeridas, manteniendo el enfoque en los requisitos actuales. Se eliminaron variables y métodos que no contribuían directamente a las funcionalidades principales del sistema.|

Estas prácticas no solo benefician el desarrollo de la versión actual del proyecto, sino que también sientan las bases para las futuras versiones y mantenimientos, asegurando que el código permanezca robusto y escalable a medida que evoluciona el proyecto.






