# JAVASCRIPT MANIPULACIÓN DOM
* Acceso a elementos del DOM
```javascript
// Obtiene un elemento por id
document.getElementById('someid');

// Obtinee una lista con los elementos que tienen esa clase
document.getElementsByClassName('someclass');

// Obtiene una HTMLCollection con los todos los elementos 'li'
document.getElementsByTagName('LI');

// Devuelve el primer elemento del documento que cumpla la selección (la notación es como en CSS)
document.querySelector('.someclass');

// Devuelve una lista de elementos que cumplen con la selección (notación como en CSS)
document.querySelectorAll('div.note, div.alert');

```
* Acceder a hijos/padres de un elemento
```javascript
// Obtener los hijos de un elemento
var elem = document.getElementById('someid');
var hijos = elem.childNodes;

// Su nodo padre
var padre = elem.parentNode;

```
* Crear nuevos elementos en el DOM
```javascript
// Para crear elementos llamamos a createElement con el nombre del elemento
var nuevoH1 = document.createElement('h1');
var nuevoParrafo = document.createElement('p');

// Crear nodos de texto para un elemento
var textoH1 = document.createTextNode('Hola mundo!');
var textoParrafo = document.createTextNode('lorem ipsum...');

// Añadir el texto a los elementos
nuevoH1.appendChild(textoH1);
nuevoParrafo.appendChild(textoParrafo);

// también podemos asignar directamente el valor a la propiedad innerHTML
nuevoH1.innerHTML = textoH1
nuevoParrafo.innerHTML = textoParrafo

// los elementos estarían listos para añadirlos al DOM, ahora mismo solo existen en memoria, pero no serán visibles hasta que no los añadamos a un elemento del DOM

```
* Añadir elementos al DOM
```javascript
// seleccionamos un elemento
var cabecera = document.getElementById('cabecera');

// Añadir elementos hijos a un elemento
cabecera.appendChild(nuevoH1);
cabecera.appendChild(nuevoParrafo);

// También podemos añadir elementos ANTES del elemento seleccionado

// Tomamos el padre
var padre = cabecera.parentNode;

// Insertamos el h1 antes de la cabecera
padre.insertBefore(nuevoH1, cabecera);


```
* Añadir/eliminar/modificar Clases
```javascript
// Tomamos un elemento
var cabecera = document.getElementById('cabecera');

// elimina una clase del elemento
cabecera.classList.remove('foo');

// Añade una clase si no existe
cabecera.classList.add('otra');

// añade o elimina varias clases a la vez
cabecera.classList.add('foo', 'bar');
cabecera.classList.remove('foo', 'bar');

// Si la clase existe la elimina, si no existe, la crea
cabecera.classList.toggle('visible');

// Devuelve true si el elemento contiene esa clase
cabecera.classList.contains('foo');

```