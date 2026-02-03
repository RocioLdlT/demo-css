# Comienzo con CSS

El style dentro metemos nuestro css debe ir en head por accesibilidad, en general no está mal así pero lo mejor es crearse un archivo css, que se llamará style.css si solo hay uno.

Lo común es crear ese archivo de CSS y poner en nuestro html(por ejemplo) link rel="stylesheet" href="style.css" con la ruta del archivo en href, ./style.css si por ejemplo está en otra carpeta.

La especificidad es lo más importante a la hora de tener en cuenta CSS,
aunque hay que tenerla en cuenta la herencia también.
Para "calcular" la especificidad se puede entender que los valores de especificidad son:

1. (1, 0, 0, 0, 0)!important
2. (0, 1, 0, 0, 0)Estilo inline (está escrito en el propio código)
3. (0, 0, 1, 0, 0) para ID´s o
4. (0, 0, 0, 1, 0) para clases o pseudo clases
5. (0, 0, 0, 0, 1) para etiquetas, elementos o pseudo elementos

- :not, es negación , es la única pseudo clase que no puntúa en especificidad.

por ejemplo:
form input [type] color rojo (0,1,2) son dos etiquetas y un atributo [] que cuenta como clase
o
form .info color verde (0,1,1) los tres últimos son los que más se van a usar

Por tanto el más específico será el rojo y será el que se aplicará

Hay que tener en cuenta que si la especificidad es igual,
imaginemos que solo hay una clase o una etiqueta en el ejemplo anterior entonces aquí entra en juego tener en cuenta la cascada
(sino hay nada inline o !important ojo),
Esta propiedad nos dice que el último indicado con el mismo valor de especificidad será el que ejecute

### AUMENTAR LA ESPECIFICIDAD

```css
.p1 {}
p.p1 {}
body p.p1 {} Vas añadiéndole elementos y le estás generando mayor especificidad
.p1.p1 {}
.p1 {!important}
```

```html
<p>Ejemplo de poner html en un .md</p>
```

### RESETS CSS

Para un reset más moderno, aunque no lo apliquemos entero, por ejemplo el de Josh Comeau, podemos aplicar algo similar entendiéndolo, claro.

Lo mejor es tener un par de hojas de css si el proyecto es mayor.
La siguiente hoja de css podría ser nuestra Guía de style donde incluimos nuestras variables definidas.
La tercera podría ser nuestra hoja de style personal.
Y después podríamos añadir más hojas por ejemplo para los estilos de una hoja de contactos
En nuestro html añadimos los links en nuestro <head></head>

Si es un proyecto pequeño, podemos meter nuestro reset, variables, si es que creamos, y la especificaciones a continuación con separaciones de comentarios si así lo creemos necesario para nuestra organización.

### VARIABLES CSS (Custorm properties)

Le damos un valor mediante -- y para aplicarla luego usamos "var".
Ejemplo:

--scala: 1.2 (lo que va a subiendo)
--base: 1rem (valor)

--size-normal: var (--base)
--size-medium: calc(var(--size-normal) _ var (--scala))
--size-large: calc(var(--size-medium) _ var (--scala))

De este modo al cambiar el dato --base o la --scala ya podremos modificar toda la página o páginas a las que queramos aplicarle los nuevos detalles sin tener revisar la mayor parte del código.

### UNIDADES DE CSS

Hay unidades absolutas como el metro y las relativas como "rem"
