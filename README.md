
# README — Evaluación

**Curso:** ALGORITMO Y ESTRUCTURA DE DATOS BASADOS EN INTELIGENCIA ARTIFICIAL
**Código:** 30710
**Evaluación:** PA3
**Equipo:** Grupo 3

## 1. Integrantes

| Integrante | Rol | Aporte principal |
|---|---|---|
| Milisé Garcia Quezada | Desarrollo de actividades 1, 2, 3, 4 | Desarrollo de actividades 1, 2, 3, 4 |
| Nombre 2 | Rol | Aporte |
| Nombre 3 | Rol | Aporte |
| Nombre 4 | Rol | Aporte |
| Nombre 5 | Rol | Aporte |

---



## 2. Descripción y objetivo

**Problema:**

Una unidad de servicios académicos necesita implementar dos mecanismos diferentes para gestionar sus procesos. El primero debe permitir deshacer acciones en el orden inverso al que fueron registradas, mientras que el segundo debe atender solicitudes respetando el orden en que llegaron.

Para resolver estas necesidades se requiere utilizar dos estructuras de datos: una pila, que funciona bajo el principio LIFO, y una cola, que funciona bajo el principio FIFO.

**Objetivo:**

Aplicar estructuras de datos lineales mediante pilas y colas para gestionar acciones y solicitudes dentro de una unidad de servicios académicos, implementando las operaciones de apilar, desapilar, encolar y desencolar, así como la consulta de elementos y la verificación de estructuras vacías.

**Solución desarrollada:**

Se desarrollaron dos estructuras de datos en Java mediante el uso de arreglos. La primera corresponde a una pila que permite registrar acciones académicas y recuperarlas en orden inverso, mientras que la segunda corresponde a una cola circular que permite almacenar y atender solicitudes respetando su orden de llegada.

Cada estructura cuenta con sus respectivos atributos, constructores y métodos para realizar las operaciones principales. Además, se incluyeron representaciones gráficas, ejemplos de ejecución y explicaciones sobre su funcionamiento.

También se analizaron diferentes situaciones del caso propuesto para identificar cuándo corresponde utilizar una pila o una cola, justificando técnicamente cada elección.

## 3. Cómo ejecutar o revisar

1. Ingresar al repositorio de GitHub.

2. Revisar el archivo README.md para conocer el desarrollo de la evaluación.

## Actividad 1. Pila LIFO
1.1. Expliquen qué caracteriza a una estructura LIFO y desarrollen una representación gráfica de una pila para el caso propuesto.

Una pila es una estructura de datos lineal que funciona bajo el principio LIFO (Last In, First Out), que significa último en entrar, primero en salir.
Esto quiere decir que el último elemento que se agrega a la pila será el primero en retirarse. 

En el caso de la unidad de servicios académicos, se utilizará una pila para registrar las acciones realizadas por un usuario dentro del sistema. De esta manera, cuando necesite deshacer alguna acción, podrá recuperar primero la última operación realizada.

Representación gráfica:

Como ejemplo se registran cinco acciones dentro del sistema académico.

                   TOPE
                    ↓
             +----------------+
             | Modificar      |
             | matrícula      |
             +----------------+
             | Registrar  |
             | correo         |
             +----------------+
             | Registrar  |
             | dirección      |
             +----------------+
             | Registrar      |
             | estudiante     |
             +----------------+
             | Crear          |
             | matrícula      |
             +----------------+

El último elemento ingresado se encuentra en el tope de la pila. Si se realiza una operación de desapilar, se retirará primero la acción «Modificar matrícula».

Orden de ingreso:

Crear matrícula.
Registrar estudiante.
Registrar dirección.
Registrar correo.
Modificar matrícula.

Orden de salida:

Modificar matrícula.
Registrar correo.
Registrar dirección.
Registrar estudiante.
Crear matrícula.

1.2. Diseñen algoritmos para apilar, desapilar, visualizar el elemento del tope y verificar si la pila está vacía.

Para implementar la pila se utilizará un arreglo de tipo String que almacenará las acciones registradas. También se utilizará una variable denominada tope, que permitirá identificar la posición del último elemento ingresado, y otra variable para controlar el tamaño máximo de la estructura.




```java
public class PilaVector {

    private String[] vector;
    private int tope;
    private int tamanio;

    public PilaVector(int tamanio) {
        if (tamanio <= 0) {
            throw new IllegalArgumentException("El tamaño debe ser mayor que cero");
        }

        this.tamanio = tamanio;
        vector = new String[tamanio];
        tope = -1;
    }

    public void push(String dato) {
        if (tope == tamanio - 1) {
            System.out.println("Error: La pila está llena");
            return;
        }

        vector[++tope] = dato;
        System.out.println("Elemento agregado: " + dato);
    }

    public String pop() {
        if (isEmpty()) {
            System.out.println("Error: La pila está vacía");
            return null;
        }

        String dato = vector[tope];
        vector[tope] = null;
        tope--;

        return dato;
    }

    public String peek() {
        if (isEmpty()) {
            System.out.println("Error: La pila está vacía");
            return null;
        }

        return vector[tope];
    }

    public boolean isEmpty() {
        return tope == -1;
    }

    public void mostrar() {
        if (isEmpty()) {
            System.out.println("La pila está vacía");
            return;
        }

        for (int i = tope; i >= 0; i--) {
            System.out.println(vector[i]);
        }
    }
}
```



1.3. Indiquen una aplicación concreta del caso donde la pila sea la estructura más adecuada.

Una aplicación concreta de la pila dentro de la unidad de servicios académicos sería el registro de las acciones realizadas por un trabajador en el sistema.

Por ejemplo, si un trabajador crea una matrícula, modifica la dirección de un estudiante y posteriormente regsitra su correo electrónico, estas acciones se almacenan en la pila según el orden en que fueron realizadas.

Si necesita deshacer la última operación, el sistema ejecutará pop() para recuperar primero el registro del correo electrónico.

Por esta razón, la pila es la estructura adecuada para implementar la función de deshacer acciones, debido a que su funcionamiento LIFO permite recuperar los elementos en orden inverso al de su ingreso.

## Actividad 2. Cola FIFO

2.1. Expliquen qué caracteriza a una estructura FIFO y desarrollen una representación gráfica de una cola para el caso propuesto.

Una cola es una estructura de datos lineal que funciona bajo el principio FIFO (First In, First Out), que significa primero en entrar, primero en salir.

Esto quiere decir que el primer elemento que ingresa será también el primero en salir. 

Representación gráfica:

Ejemplo: ingresan cinco solicitudes de atención.

FRENTE                                             FINAL
   ↓                                                  ↓
+----------------+----------------+----------------+----------------+----------------+
| Solicitud A    | Solicitud B    | Solicitud C    | Solicitud D    | Solicitud E    |
+----------------+----------------+----------------+----------------+----------------+
                    ORDEN DE ATENCIÓN  →

La primera solicitud que ingresó se encuentra en el frente de la cola. Cuando se realiza una operación de desencolar, se retira primero la solicitud A.

Orden de ingreso:

1. Solicitud A.
2. Solicitud B.
3. Solicitud C.
4. Solicitud D.
5. Solicitud E.

Orden de atención:

1. Solicitud A.
2. Solicitud B.
3. Solicitud C.
4. Solicitud D.
6. Solicitud E.



2.2. Diseñen algoritmos para encolar, desencolar, visualizar el frente de la cola y verificar si la cola está vacía.


```java
public class ColaVector {

    private String[] vector;
    private int frente;
    private int finalCola;
    private int tamanio;
    private int cantidad;

    public ColaVector(int tamanio) {
        if (tamanio <= 0) {
            throw new IllegalArgumentException("El tamaño debe ser mayor que cero");
        }

        this.tamanio = tamanio;
        vector = new String[tamanio];
        frente = 0;
        finalCola = -1;
        cantidad = 0;
    }

    public void enqueue(String dato) {
        if (cantidad == tamanio) {
            System.out.println("Error: La cola está llena");
            return;
        }

        finalCola = (finalCola + 1) % tamanio;
        vector[finalCola] = dato;
        cantidad++;

        System.out.println("Solicitud agregada: " + dato);
    }

    public String dequeue() {
        if (isEmpty()) {
            System.out.println("Error: La cola está vacía");
            return null;
        }

        String dato = vector[frente];
        vector[frente] = null;

        frente = (frente + 1) % tamanio;
        cantidad--;

        if (cantidad == 0) {
            frente = 0;
            finalCola = -1;
        }

        return dato;
    }

    public String peek() {
        if (isEmpty()) {
            System.out.println("Error: La cola está vacía");
            return null;
        }

        return vector[frente];
    }

    public boolean isEmpty() {
        return cantidad == 0;
    }

    public void mostrar() {
        if (isEmpty()) {
            System.out.println("La cola está vacía");
            return;
        }

        for (int i = 0; i < cantidad; i++) {
            System.out.println(vector[(frente + i) % tamanio]);
        }
    }
}
```



2.3. Indiquen una aplicación concreta del caso donde la cola sea la estructura más adecuada.

Una aplicación concreta de la cola dentro de la unidad de servicios académicos sería la administración de solicitudes realizadas por los estudiantes.

Por ejemplo, cuando diferentes estudiantes solicitan constancias de estudios, certificados o modificaciones de sus datos académicos, sus solicitudes se registran en una cola.

El personal encargado atenderá primero la solicitud que llegó antes y continuará con las siguientes respetando el orden de ingreso.

Por esta razón, la cola es la estructura más adecuada para gestionar las solicitudes pendientes, debido a que su funcionamiento FIFO garantiza una atención organizada y secuencial.



## Actividad 3. Selección de estructura para situaciones reales

3.1. Determinen si corresponde usar pila o cola en las siguientes situaciones: registro de acciones recientes para revertir cambios; atención de solicitudes en orden de llegada; procesamiento donde el último ingresado debe atenderse primero; flujo de espera de trámites pendientes.

Para cada situación se selecciona la estructura de datos que mejor se adapta al orden en que deben procesarse los elementos.


Situación                                                        | Estructura seleccionada    |   Principio
 
Registro de acciones recientes para revertir cambios.            | Pila                       |   LIFO

Atención de solicitudes en orden de llegada.                     | Cola                       |   FIFO

Procesamiento donde el último ingresado debe atenderse primero.  | Pila                       |   LIFO

Flujo de espera de trámites pendientes.                          | Cola                       |   FIFO



3.2. Justifiquen técnicamente cada elección.

a. Registro de acciones recientes para revertir cambios.

Se utiliza una pila porque las acciones deben deshacerse en orden inverso al que fueron realizadas. La última acción registrada será la primera en recuperarse, cumpliendo con el principio LIFO.

b. Atención de solicitudes en orden de llegada.

Se utiliza una cola porque las solicitudes deben procesarse respetando el orden en que fueron registradas. La primera solicitud ingresada será la primera en ser atendida, cumpliendo con el principio FIFO.

c. Procesamiento donde el último ingresado debe atenderse primero.

Se utiliza una pila porque permite acceder primero al último elemento agregado. Esta característica facilita el procesamiento de elementos en orden inverso a su ingreso.

d. Flujo de espera de trámites pendientes.

Se utiliza una cola porque permite organizar los trámites según su llegada. De esta manera, el personal académico puede atender primero los trámites más antiguos y continuar con los siguientes.




## Actividad 4. Comparación y argumentación

4.1. Elaboren una comparación académica entre pila y cola considerando principio de funcionamiento, operaciones principales, forma de acceso y ventajas en contextos de aplicación.

Característica                          | Pila (LIFO)                                      | Cola (FIFO)

Principio de funcionamiento             | Último en entrar, primero en salir.              | Primero en entrar, primero en salir.

Inserción                               | Apilar (PUSH).                                   | Encolar (ENQUEUE).

Eliminación                             | Desapilar (POP).                                 | Desencolar (DEQUEUE).

Consulta                                | Ver tope (PEEK).                                 | Ver frente (PEEK).

Forma de acceso                         | Inserción y eliminación por                      | Inserción por el final y eliminación por el frente.
                                          el mismo extremo, denominado tope.

Ventaja principal                       | Permite recuperar elementos en orden             | Permite procesar elementos respetando su orden de llegada.
                                          inverso.

Aplicación en el caso                   | Deshacer acciones realizadas en el sistema académico.   | Atender solicitudes de los estudiantes.

Ventajas de la pila:
1. Permite recuperar las últimas acciones realizadas.
2. Facilita la implementación de funciones para deshacer cambios.
3. Mantiene un control ordenado de las operaciones recientes.
4. Sus operaciones principales son sencillas de implementar.

Ventajas de la cola:
1. Permite organizar las solicitudes según su orden de llegada.
2. Facilita la administración de trámites pendientes.
3. Evita alterar el orden de atención de las solicitudes.
4. Permite gestionar procesos de manera secuencial.

4.2. Redacten una conclusión grupal argumentando por qué la selección correcta de la estructura mejora la solución del problema.

La pila, basada en el principio LIFO, resulta adecuada para registrar y deshacer acciones, debido a que permite recuperar primero la última operación realizada. Por otro lado, la cola, basada en el principio FIFO, permite administrar las solicitudes académicas respetando el orden en que fueron registradas.

Ambas estructuras cumplen funciones diferentes, pero complementarias dentro de un sistema de gestión académica.

Por lo tanto, seleccionar correctamente entre una pila y una cola permite organizar mejor la información, mantener el orden de los procesos y desarrollar soluciones algorítmicas más claras y eficientes.




**Pasos de revisión:**
1. Ingresar al repositorio y localizar el archivo PA3.java.
2. Revisar la implementación de las actividades
3. Comparar los resultados obtenidos durante la ejecución con los valores esperados descritos en este README.

## 4. Evidencias

![Evidencia](image/Actividad1.png)
![Evidencia](image/Actividad2.1.png)
![Evidencia](image/Actividad2.2.png)

 
## 5. Matriz de participación

| Integrante | Desarrollo | Pruebas | Documentación | Exposición | Evidencia de participación |
|---|---|---|---|---|---|
| [Milisé GArcia Quezada] | [Alta] | [Alta] | [Alta] | [No] | [Desarrollo de las actividades 1, 2 ,3 ,4] |
| [Nombre 2] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Sí/No] | [Actividades 1, 2, 3, 4] |
| [Nombre 3] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Sí/No] | [Commits, avances, etc.] |
| [Nombre 4] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Sí/No] | [Commits, avances, etc.] |
| [Nombre 5] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Alta/Media/Baja] | [Sí/No] | [Commits, avances, etc.] |

## 6. Video de exposición

**Video público de YouTube:** No se realizó.

## 7. Conclusiones

1. Las pilas permiten almacenar y recuperar elementos siguiendo el principio LIFO, siendo adecuadas para gestionar acciones que deben deshacerse en orden inverso.
2. Las colas permiten organizar y procesar elementos siguiendo el principio FIFO, facilitando la atención de solicitudes según su orden de llegada.
3. La implementación mediante arreglos permite controlar la capacidad de almacenamiento y administrar las posiciones de los elementos.
4. La selección de una estructura de datos depende de las necesidades del problema, ya que cada una presenta características y ventajas diferentes.


**Última actualización:** [03/11/2026]