# Proyecto Aspiradora - Versión 3 Diseño Modular

## Descripción General

Este proyecto implementa una simulación de una aspiradora automática. El objetivo principal es crear una estructura modular y mantenible que permita extender fácilmente las funcionalidades en el futuro.

## Diseño Modular

### Cohesión

La cohesión entre clases y su relación entre sí, en nuestro diseño:
- La clase `Aspiradora` tiene métodos que se centran en el movimiento y la limpieza, que son sus responsabilidades principales.
- La clase `Azulejo` se encarga de gestionar el nivel de suciedad y la presencia de muebles en una posición específica.
- Las clases auxiliares (`Bateria`, `CapacidadBasura`, `Posicion`, `Habitacion`) están diseñadas para gestionar aspectos específicos del comportamiento de la aspiradora.

### Clases Alternativas con Diferentes Interfaces
Para mejoras de un código escalable, podrían existir distintas versiones de una aspiradora con interfaces alternativas para distintas estrategias de limpieza o movimiento.

### Envidia de Características
Se debe evitar que una clase dependa excesivamente de los métodos de otra clase. Actualmente, la clase `Aspiradora` delega responsabilidades específicas a clases como `Bateria` y `CapacidadBasura`, manteniendo la responsabilidad distribuida de manera equitativa.

### Clase de Datos
Algunas clases como `Posicion` y `CapacidadBasura` pueden considerarse clases de datos, ya que su principal función es almacenar y proporcionar acceso a datos específicos. `Azulejo` también puede considerarse una clase de datos, ya que gestiona el nivel de suciedad y la presencia de muebles en una posición específica.

### Cambios Divergentes
Este concepto se refiere a cuando una clase se modifica por múltiples razones. Aquí, las modificaciones en `Aspiradora` están relacionadas principalmente con sus métodos de movimiento y limpieza.

### Cirugía a Escopetazos
Ocurre cuando un pequeño cambio requiere modificar muchas clases. Aquí, la modularidad del diseño ayuda a minimizar este problema, pero hay dependencia directa entre `Aspiradora`, `Bateria`, y `CapacidadBasura`.

### Grupo de Datos
La clase `Habitacion` contiene un grupo de datos relacionado con la estructura y contenido de la habitación, agrupando adecuadamente estos datos.

### Obsesión por Tipos Primitivos
En lugar de usar tipos primitivos, se han creado clases específicas como `Posicion` y `CapacidadBasura` para manejar la lógica y los datos, lo cual mejora la legibilidad y la mantenibilidad. La clase `Azulejo` maneja los niveles de suciedad y la presencia de muebles, evitando el uso de tipos primitivos directamente.

### Clases Perezosas
Actualmente, todas las clases tienen una responsabilidad definida. No existen clases perezosas en este diseño.

## Acoplamiento

### Inapropiada Intimidad
El acoplamiento se mantiene bajo control al asegurar que las clases interactúan a través de interfaces bien definidas y no acceden directamente a los campos privados de otras clases.

### Clase de Biblioteca Incompleta
En este diseño no se utiliza ninguna clase de biblioteca incompleta. Todas las clases tienen las funcionalidades necesarias para cumplir con sus responsabilidades.

## Granulado

### Listas de Parámetros Largas
El constructor de la clase `Aspiradora` toma sólo los parámetros necesarios (`Bateria` y `capacidadBasura`). Se ha evitado listas de parámetros largas.

### Métodos Largos
El método `mover` en `Aspiradora` es relativamente largo y podría ser refactorizado para mejorar la legibilidad y la mantenibilidad. Podrían extraerse métodos adicionales para encapsular la lógica de movimiento y recarga de la batería.

### Clase Grande
La clase `Aspiradora` maneja varias responsabilidades, conforme vaya escalando el proyecto se gestionará la necesidad de separar las responsabilidades de la funcionalidad de la Aspiradora.

### Campos Temporales
En este diseño no se usan campos temporales inadecuadamente.

```java
import java.util.Random;

public class Aspiradora {
    private int pasosRealizados;
    private int limpiezaRealizada;
    private CapacidadBasura capacidadBasura;
    private Bateria bateria;
    private Posicion posicion;
    private int esperaRecarga;

    public Aspiradora(Bateria bateria, int capacidadBasura) {
        this.pasosRealizados = 0;
        this.limpiezaRealizada = 0;
        this.bateria = bateria;
        this.capacidadBasura = new CapacidadBasura(capacidadBasura);
        this.posicion = new Posicion(0, 0);
        this.esperaRecarga = 0;
    }

    public Posicion getPosicion() {
        return posicion;
    }

    public int getPasosRealizados() {
        return pasosRealizados;
    }

    public int getLimpiezaRealizada() {
        return limpiezaRealizada;
    }

    public void mover(Habitacion habitacion) {
        Random random = new Random();

        if (esperaRecarga > 0) {
            esperaRecarga--;
            return;
        }

        int dx = random.nextInt(3) - 1;
        int dy = random.nextInt(3) - 1;

        int nuevaX = posicion.getX() + dx;
        int nuevaY = posicion.getY() + dy;

        if (nuevaX >= 0 && nuevaX < habitacion.getDimension().getAncho() &&
            nuevaY >= 0 && nuevaY < habitacion.getDimension().getLargo()) {
            if (!habitacion.getMuebles()[nuevaX][nuevaY] && !bateria.estaDescargada()) {
                posicion.setX(nuevaX);
                posicion.setY(nuevaY);
                limpiarCasilla(habitacion, posicion);
                bateria.descargar();
                capacidadBasura.incrementar();
                if (capacidadBasura.estaLlena()) {
                    System.out.println("¡La bolsa de basura de la aspiradora está llena!");
                }
                System.out.println("Nivel de bateria de la aspiradora: " + bateria.getNivelBateria());
                pasosRealizados++;
            } else {
                System.err.println("Bateria agotada, no se mueve. Entrando en recarga");
                esperaRecarga = 5;
                bateria.recargar();
            }
        }
    }

    private void limpiarCasilla(Habitacion habitacion, Posicion posicion) {
        if (habitacion.getSuperficie()[posicion.getX()][posicion.getY()].getNivelSuciedad() > 0) {
            habitacion.getSuperficie()[posicion.getX()][posicion.getY()].setNivelSuciedad(0);
            limpiezaRealizada++;
            System.out.println("La aspiradora limpió la casilla en las coordenadas: (" + posicion.getX() + ", " + posicion.getY() + ")");
        }
    }
}
```