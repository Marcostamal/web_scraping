# **Web scraping**
<p align="center">
<img src="/imagenes/5ede498db760540004f2c5e4.png"  height="400">
</p>
UMAAAAAAI!! Hola soy Rengoku el donitas bimbo y hoy te enseñare lo que es web scraping y como utilizarlo para que puedas agregar mas data a tus proyectos.
El web scraping se refiere al proceso de extracción de contenidos y datos de sitios web mediante software.

## **¿Como hacer web scraping?**
Para extraer datos de una web, se puede utilizar código de Python o recurrir a otras opciones, como utilizar una API o herramientas específicas para estas tareas.

*Nota*: una API es una interfaz de programación de aplicaciones, que permite la comunicación entre dos aplicaciones de software a través de un conjunto de reglas.

Algunos sitios web, como Twitter, facilitan directamente una API para poder acceder a sus datos. El problema es que la mayoría de los sitios web no tienen API o, incluso cuando sí que tienen, los datos que permiten obtener no son los que nosotros necesitamos. En estos casos, crear un rastreador web con Python es una buena solución.

## **Conceptos previos de paginas web**

Cuando visitamos una página web, nuestro navegador manda una solicitud a un servidor web para obtener archivos de dicho servidor. El servidor devuelve archivos que le indican a nuestro navegador cómo debe mostrar la página. Básicamente, estos archivos pueden ser:
- De tipo HTML, que contienen el contenido principal de una página.
- De tipo CSS, que agregan estilos de colores y formatos a la página.
- De tipo JS (Javascript), que agregan interactividad a las páginas web.
- De imagen, como JPG y PNG, que permiten que las páginas web muestren imágenes.

En principio, nos interesa el contenido principal de la página web, por lo que nuestro objetivo es extraer datos del archivo HTML.
