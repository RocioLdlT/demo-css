# Comienzo con CSS

El style dentro metemos nuestro css debe ir en head por accesibilidad, en general no está mal así pero lo mejor es crearse un archivo css, que se llamará style.css si solo hay uno.

Lo común es crear ese archivo de CSS y poner en nuestro html(por ejemplo) link rel="stylesheet" href="style.css" con la ruta del archivo en href, ./style.css si por ejemplo está en otra carpeta.

La especificidad es lo más importante a la hora de tener en cuenta CSS,
aunque hay que tenerla en cuenta la herencia también.
Para "calcular" la especificidad se puede entender que los valores de especificidad son:

1. (1, 0, 0, 0, 0) !important
2. (0, 1, 0, 0, 0) estilo inline (está escrito en el propio código)
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
body p.p1 {} 
Vas añadiéndole elementos y le estás generando mayor especificidad
.p1.p1 {}
.p1 {!important}
```

### RESETS CSS

Para un reset más moderno, aunque no lo apliquemos entero, por ejemplo el de Josh Comeau, podemos aplicar algo similar entendiéndolo, claro.

Lo mejor es tener un par de hojas de css si el proyecto es mayor.
La siguiente hoja de css podría ser nuestra Guía de style donde incluimos nuestras variables definidas.
La tercera podría ser nuestra hoja de style personal.
Y después podríamos añadir más hojas por ejemplo para los estilos de una hoja de contactos
En nuestro html añadimos los links en nuestro <head></head>

Si es un proyecto pequeño, podemos meter nuestro reset, variables, si es que creamos, y la especificaciones a continuación con separaciones de comentarios si así lo creemos necesario para nuestra organización.


Otra opción para redirigir nuestro css al html (por ejemplo) es:
```css
@import url(./style.css)
```
No suele usarse pero es práctico y más actual.


### VARIABLES CSS (Custom properties)

Le damos un valor mediante -- y para aplicarla luego usamos "var".
Ejemplo:

--scala: 1.2 (lo que va a subiendo)
--base: 1rem (valor)

--size-normal: var (--base)
--size-medium: calc(var(--size-normal) _ var (--scala))
--size-large: calc(var(--size-medium) _ var (--scala))

De este modo al cambiar el dato --base o la --scala ya podremos modificar toda la página o páginas a las que queramos aplicarle los nuevos detalles sin tener revisar la mayor parte del código. Así, será proporcional.

### UNIDADES DE CSS

Hay unidades absolutas como el metro y las relativas como "rem" o "em" por ejemplo.
El pixel es una unidad que vamos a llamar fija, porque ni es del todo absoluta pero tampoco relativa.

- `em ` y `rem` son unidades relativas a font-size

Por defecto 1 rem (normalmente son 16px).

DATO: Es mala práctica definir tamaños fijos en las fuentes.

Los `em` directos del padre del contenedor y los `rem` van asociados a :root. Los `em` son más específicos para líneas, por ejemplo, una parte que está contenida dentro de un contenedor.
*Ejemplo en apuntes CSS Unidades.css y unidades.html*

- `vw` viewport (lo que nos enseña el navegador) * width ( para el ancho del navegador con contar la línea del navegador)
- `vh` viewport * height (para el alto del navegador con la linea de scroll, la barra vaya jaja)

Existen las misma pero sin contar la línea de scroll (revisar apuntes o buscar).

*Para otros valores relativos del estilo a los anteriores, revisar apuntes*

### BOX MODEL (MODELO DE CAJA)

El Box Model tienen un modelo de cajas dentro de cajas donde el margen está rodeado por el borde, y éste a su vez contiene los padding y dentro tenemos nuestro contenido.

Lo primero que realizamos es quitar los valores por defecto dentro de nuestra caja con:

```css
* { 
    box-sizing: border-box;
}
```
Esto nos servirá porque, por ejemplo en dos span juntos, con este tipo de modelo al añadirle al primer <span> width, borde, y margin, y luego indicarle al segundo span su padding, quizá ocupase demasiado el ancho de ambos en nuestra web por "culpa" de width ya que por defecto, contaba (desde los inicios de css)demasiado el contenido de dentro de la propia caja....

Hay que tener en cuenta que box-sizing no se hereda por lo que tenemos que ponerle ese * para que afecte a cada elemento y no nos entorpezca la herencia y la cascada acabando por no aplicarse.

Con este `border-box`lo que estamos haciendo es que width incorpore el borde dentro de su contenido (no el margen) pero con éste detalle estamos solventando el dilema que se nos presenta con `content-box`.


DATO: El * no incluye ::after y ::before por lo que para incluir todo, todo y todo, pondríamos;
```css
*,
*::before,
*::after {
    box-sizing: border-box;
}
```

- Los márgenes verticales (margin) entre elementos no se suman. En vez de sumar los dos los márgenes se colapsan y siempre cogerá el valor % más grande de los dos elementos en cuestión. Sin embargo, en los margenes horizontales sí se suman, no se colapsan.

- Los display: más comunes son `block` (que suele venir por defecto y que ocupa el ancho de la página sin que la siguiente etiqueta intente colarse en ese espacio) e `inline` (siempre va ocupar su propio contenido y podrá añadirse otro elemento si el ancho de la página lo permite. Por ejemplo, dos títulos quedarían en la misma línea).
Block sirve para que los títulos, por ejemplo, no se le añada visualmente el siguiente elemento.

DATO: Los <span>, (como también les pasa a imágenes, vídeos, pictures, svg, button, inputs) tienen por defecto un `display inline`, por eso se les indica , si es lo que se busca, un `display: inline-block`, que es un comportamiento híbrido, para que se adecue en nuestros <span>

- Estos display son los más comunes pero los flex o grid serán mucho más potentes.

### LAYOUT

El layout es la disposición general de mis elementos. Cómo quiero que se coloquen mis cajas, las 20 o 30 que tenga. 
Normalmente por defecto viene el que esté "en línea".

- Propiedades lógicas (diferentes de Custom properties):
(a) Padding-block es la dirección del bloque(arriba y abajo en nuestro idioma).
(b)Padding-inline es la dirección de lectura (izq. y derecha en nuestro idioma). Pero en chino y árabe, por ejemplo, estas direcciones pueden ser diferentes. Utilizar estas dos ultimas si estamos aplicándolo para un cliente internacional será lo más responsable, además nos ayudará a entender la forma en la que trabajar con flex o grid, que utilizan 4 ejes.

#### FLEXBOX





## DATOS SUELTOS

1. 
```html
<p>Ejemplo de poner html en un .md</p>
```
2. `max.width` , para una imagen que quiero que sea fluida y flexible. Normalmente los textos fluyen en nuestra web pero las imágenes se comportan de diferente modo.

3. En html no se ponen unidades en width o height por ejemplo, pero en css si le aclaramos las unidades (px, vh, vw, rem, em).




