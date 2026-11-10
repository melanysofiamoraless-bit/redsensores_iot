# Decisiones de diseño — Semana 3

## 1. Punto de entrada

El proyecto mantiene un único punto de entrada:

```text
IngestaSensores.main()
```

No se crean aplicaciones independientes por semana.

`BancoDePruebas` es una clase auxiliar y no contiene `main`.

## 2. Búsqueda por timestamp

Se utilizan dos estrategias:

- Búsqueda lineal: no requiere ordenamiento.
- Búsqueda binaria: requiere que el arreglo esté ordenado por timestamp.

Los datos sintéticos de `GeneradorDatos` se generan en orden cronológico, por lo que la búsqueda binaria por timestamp cumple su precondición.

## 3. Búsqueda por PM2.5

No se asume que los datos estén ordenados por PM2.5.

Por tanto, la búsqueda binaria por PM2.5 se conserva como experimento para demostrar el efecto de una precondición incumplida.

## 4. Comparación de String

Los identificadores de estación se comparan mediante:

```java
equals()
```

y no mediante:

```java
==
```

porque se necesita comparar contenido.

## 5. Medición

La comparación principal entre algoritmos utiliza el número de comparaciones.

El tiempo en milisegundos se conserva como evidencia experimental, pero no es la única medida utilizada.

## 6. Evolución del proyecto

La Semana 3 agrega una nueva capacidad a la misma plataforma:

```text
Sensores
   ↓
Ingesta
   ↓
Repositorio
   ↓
Búsqueda
   ↓
Medición de eficiencia
```

La Semana 4 podrá extender esta misma arquitectura para estudiar ordenamiento.
Semana 5: Listas enlazadas
1. ¿Por qué insertar al inicio es más económico en una lista enlazada que en un arreglo?
   Porque en la lista enlazada solo creas el nodo nuevo y le cambias la flecha para que apunte al primero; eso se hace rapidísimo sin importar cuántos datos tenga. En el arreglo te toca mover uno por uno todos los elementos hacia un lado para hacer espacio, y si se llena, toca crear otro más grande y pasar todo, lo que gasta un montón de recursos.
2. ¿Por qué el acceso a una posición arbitraria es más costoso en una lista?
   Porque a diferencia de un arreglo donde uno llega directo al número de la casilla, en la lista enlazada no hay índices directos en la memoria. Toca empezar a caminar desde el primer nodo y pasar por cada uno (uno por uno) hasta llegar a la posición que buscas, y eso se vuelve pesado si el dato está muy al fondo.
3. ¿Qué diferencia existe entre un experimento de rendimiento y una prueba unitaria?
   La prueba unitaria es la que verifica que el código sirva bien y no tenga baches haciendo pruebas con casos específicos. En cambio, el experimento (como el de BancoDeListas) es más para medir números, ver cuántos saltos da la computadora o comparar qué tan rápido o pesado se comporta cada estructura con muchos datos.
4. Qué caso límite consideras más importante probar en eliminar() y por qué?
   Para mí, el más clave es cuando vas a eliminar el único elemento que le queda a la lista. Si borras ese y no actualizas bien tanto el principio (primero) como el final (ultimo) para que queden en null, la lista queda descuadrada y el tamaño real ya no va a coincidir con los nodos que de verdad existen.
5. Para el histórico de lecturas de sensores, ¿qué estructura elegirías si predominan las inserciones al inicio? ¿Qué elegirías si predominan las consultas por posición? Justifica ambas decisiones.
   Si lo que más se hace es meter datos nuevos al comienzo, sin duda elegiría la lista enlazada porque es súper flexible para eso. Pero si el sistema se la pasa buscando y consultando datos específicos por su posición todo el tiempo, ahí sí me voy por el arreglo, ya que te ahorra tener que recorrer toda la cadena desde el principio.