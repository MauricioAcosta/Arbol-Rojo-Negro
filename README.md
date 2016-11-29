# Arbol-Rojo-Negro
Un árbol rojo-negro es un tipo abstracto de datos. Concretamente, es un árbol binario de búsqueda equilibrado, una estructura de datos utilizada en informática y ciencias de la computación.


Todo nodo es o bien rojo o bien negro.
La raíz es negra.
Todas las hojas (NULL) son negras.
Todo nodo rojo debe tener dos nodos hijos negros.
Cada camino desde un nodo dado a sus hojas descendientes contiene el mismo número de nodos negros.

Rotación

Para conservar las propiedades que debe cumplir todo árbol rojo-negro, en ciertos casos de la inserción y la eliminación será necesario reestructurar el árbol, si bien no debe perderse la ordenación relativa de los nodos. Para ello, se llevan a cabo una o varias rotaciones, que no son más que reestructuraciones en las relaciones padre-hijo-tío-nieto.

Las rotaciones que se consideran a continuación son simples; sin embargo, también se dan las rotaciones dobles.

Búsqueda

La búsqueda consiste acceder a la raíz del árbol y comparar su valor con el valor buscado. Si el elemento a localizar coincide con el de la raíz, la búsqueda ha concluido con éxito. Si el elemento es menor, se busca en el subárbol izquierdo; si es mayor, en el derecho. Si se alcanza un nodo hoja y el elemento no ha sido encontrado se supone que no existe en el árbol. Cabe destacar que la búsqueda en este tipo de árboles es muy eficiente y representa una función logarítmica. La búsqueda de un elemento en un ABB (Árbol Binario de Búsqueda) en general, y en un árbol rojo-negro en particular, se puede realizar de dos formas: iterativa y recursiva.

Inserción
La inserción comienza añadiendo el nodo como lo haríamos en un árbol binario de búsqueda convencional y pintándolo de rojo. Lo que sucede después depende del color de otros nodos cercanos. El término tío nodo será usado para referenciar al hermano del padre de un nodo, como en los árboles familiares humanos. Conviene notar que:

La propiedad 3 (Todas las hojas, incluyendo las nulas, son negras) siempre se cumple.
La propiedad 4 (Ambos hijos de cada nodo rojo son negros) está amenazada solo por añadir un nodo rojo, por repintar un nodo negro de color rojo o por una rotación.
La propiedad 5 (Todos los caminos desde un nodo dado hasta sus nodos hojas contiene el mismo número de nodos negros) está amenazada solo por repintar un nodo negro de color rojo o por una rotación.

Nota: En los esquemas que acompañan a los algoritmos, la etiqueta N será utilizada por el nodo que está siendo insertado, P para los padres del nodo N, G para los abuelos del nodo N, y U para los tíos del nodo N. Notamos que los roles y etiquetas de los nodos están intercambiados entre algunos casos, pero en cada caso, toda etiqueta continúa representando el mismo nodo que representaba al comienzo del caso. Cualquier color mostrado en el diagrama está o bien supuesto en el caso o implicado por dichas suposiciones.


Caso 1: El nuevo nodo N es la raíz del árbol. En este caso, es repintado en color negro para satisfacer la propiedad 2 (la raíz es negra). Como esto añade un nodo negro a cada camino, la propiedad 5 (todos los caminos desde un nodo dado a sus hojas contiene el mismo número de nodos negros) se mantiene.

Caso 2: El padre del nuevo nodo (esto es, el nodo P) es negro, así que la propiedad 4 (ambos hijos de cada nodo rojo son negros) se mantiene. En este caso, el árbol es aun válido. La propiedad 5 (todos los caminos desde cualquier nodo dado a sus hojas contiene igual número de nodos negros) se mantiene, porque el nuevo nodo N tiene dos hojas negras como hijos, pero como N es rojo, los caminos a través de cada uno de sus hijos tienen el mismo número de nodos negros que el camino hasta la hoja que reemplazó, que era negra, y así esta propiedad se mantiene satisfecha.

Caso 3: Si el padre P y el tío U son rojos, entonces ambos nodos pueden ser repintados de negro y el abuelo G se convierte en rojo para mantener la propiedad 5 (todos los caminos desde cualquier nodo dado hasta sus hojas contiene el mismo número de nodos negros). Ahora, el nuevo nodo rojo N tiene un padre negro. Como cualquier camino a través del padre o el tío debe pasar a través del abuelo, el número de nodos negros en esos caminos no ha cambiado. Sin embargo, el abuelo G podría ahora violar la propiedad 2 (la raíz es negra) o la 4 (ambos hijos de cada nodo rojo son negros), en el caso de la 4 porque G podría tener un padre rojo. Para solucionar este problema, el procedimiento completo se realizará de forma recursiva hacia arriba hasta alcanzar el caso 1.

Nota: En los casos restantes, se asume que el nodo padre P es el hijo izquierdo de su padre. Si es el hijo derecho, izquierda y derecha deberían ser invertidas a partir de los casos 4 y 5. El código del ejemplo toma esto en consideración.

Caso 4: El nodo padre P es rojo pero el tío U es negro; también, el nuevo nodo N es el hijo derecho de P, y P es el hijo izquierdo de su padre G. En este caso, una rotación a la izquierda que cambia los roles del nuevo nodo N y su padre P puede ser realizada; entonces, el primer nodo padre P se ve implicado al usar el caso 5 de inserción (re etiquetando N y P ) debido a que la propiedad 4 (ambos hijos de cada nodo rojo son negros) se mantiene aún incumplida. La rotación causa que algunos caminos (en el sub-árbol etiquetado como “1”) pasen a través del nuevo nodo donde no lo hacían antes, pero ambos nodos son rojos, así que la propiedad 5 (todos los caminos desde cualquier nodo dado a sus hojas contiene el mismo número de nodos negros) no es violado por la rotación, después de completado este caso, se puede notar que aún se incumple la propiedad número 4 (ambos hijos de cada nodo rojo son de color negro), esto se resuelve pasando al caso 5.

Caso 5: El padre P es rojo pero el tío U es negro, el nuevo nodo N es el hijo izquierdo de P, y P es el hijo izquierdo de su padre G. En este caso, se realiza una rotación a la derecha sobre el padre P; el resultado es un árbol donde el padre P es ahora el padre del nuevo nodo N y del inicial abuelo G. Este nodo G ha de ser negro, así como su hijo P rojo. Se intercambian los colores de ambos y el resultado satisface la propiedad 4 (ambos hijos de un nodo rojo son negros). La propiedad 5 (todos los caminos desde un nodo dado hasta sus hojas contienen el mismo número de nodos negros) también se mantiene satisfecha, ya que todos los caminos que iban a través de esos tres nodos entraban por G antes, y ahora entran por P. En cada caso, este es el único nodo negro de los tres

Eliminación[editar]
En un árbol binario de búsqueda normal, cuando se borra un nodo con dos nodos internos como hijos, tomamos el máximo elemento del subárbol izquierdo o el mínimo del subárbol derecho, y movemos su valor al nodo que es borrado (como se muestra aquí). Borramos entonces el nodo del que copiábamos el valor que debe tener menos de dos nodos no hojas por hijos. Copiar un valor no viola ninguna de las propiedades rojo-negro y reduce el problema de borrar en general al de borrar un nodo con como mucho un hijo no hoja. No importa si este nodo es el nodo que queríamos originalmente borrar o el nodo del que copiamos el valor.

Resumiendo, podemos asumir que borramos un nodo con como mucho un hijo no hoja (si solo tiene nodos hojas por hijos, tomaremos uno de ellos como su hijo). Si borramos un nodo rojo, podemos simplemente reemplazarlo con su hijo, que debe ser negro. Todos los caminos hasta el nodo borrado simplemente pasarán a través de un nodo rojo menos, y ambos nodos, el padre del borrado y el hijo, han de ser negros, así que las propiedades 3 (todas las hojas, incluyendo las nulas, son negras) y 4 (los dos hijos de cada nodo rojo son negros) se mantienen. Otro caso simple es cuando el nodo borrado es negro y su hijo es rojo. Simplemente eliminar un nodo negro podría romper las propiedades 4 (los dos hijos de cada nodo rojo son negros) y 5 (todos los caminos desde un nodo dado hasta sus hojas contienen el mismo número de nodos negros), pero si repintamos su hijo de negro, ambas propiedades quedan preservadas.

El caso complejo es cuando el nodo que va a ser borrado y su hijo son negros. Empezamos por reemplazar el nodo que va a ser borrado con su hijo. Llamaremos a este hijo (en su nueva posición) N, y su hermano (el otro hijo de su nuevo padre) S. En los diagramas de debajo, usaremos P para el nuevo padre de N, SL para el hijo izquierdo de S, y SR para el nuevo hijo derecho de S (se puede mostrar que S no puede ser una hoja).

Nota: Entre algunos casos cambiamos roles y etiquetas de los nodos, pero en cada caso, toda etiqueta sigue representando al mismo nodo que representaba al comienzo del caso. Cualquier color mostrado en el diagrama es o bien supuesto en su caso o bien implicado por dichas suposiciones. El blanco representa un color desconocido (o bien rojo o bien negro).






