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


## **Ejemplo practico**

Haremos web scraping a esta pagina: [Click aqui para verla](https://en.wikipedia.org/wiki/List_of_S%26P_500_companies) esta pagina contiene informacion sobre las 500 empresas que pertenecen al indice S&P 500 de Estados Unidos, este indice hace referencia a las mejores 500 empresas que cotizan en la bolsa de valores.

Una vez que mires la pagina te daras cuenta de que no tiene algo como una API ni tampoco un link de descarga para un archivo de texto, csv, json, etc. que nos facilite informacion de alguna de las tablas, ya que esa es la data que nosotros consideramos interesante, asi que no queda mas que hacer web scraping. Como todo buen cazador de demonios que eres ya supongo sabes algo de python asi que esto te resultara facil y si no al terminar esto lo veras de esa manera o eso espero.

## **Paso 1**
### **Importar las librerias**
Para esto necesitamos primero tener instaladas las librerias de requests y beautifulsoup, ademas de la ya famosa libreria de pandas.
Seria perfecto que puedas pasarte por los siguientes links para que veas la info sobre las librerias, en resumen te dire que la libreria de requests se usa para hacer peticiones a paginas web y beautifulsoup sirve para que la info en formato html se vea bonita, pero no te quedes con eso, INVESTIGA.

[libreria requests](https://pypi.org/project/requests/)

[libreria beautifulsoup](https://pypi.org/project/beautifulsoup4/)

Teniendo las librerias instaladas ahora si importamos, recuerda haremos esto en un notebook de python.

~~~
# pip install requests
# pip install beautifulsoup4
import requests
from bs4 import BeautifulSoup
import pandas as pd
~~~

## **Paso 2**
### **Conseguir la url de la pagina**
En una variable que llamaremos url meteremos un string que correspondera al enlace de la pagina a la que haremos web scraping.
~~~
url = "https://en.wikipedia.org/wiki/List_of_S%26P_500_companies"   # Direccion de la pagina con la data que queremos
~~~

## **Paso 3**
### **Hacer la peticion a la pagina con requests**
Lo siguiente que haremos sera usar la funcion .get() de requests, esta funcion hace una peticion a la pagina que pasemos como parametro en este caso nosotros ya antes creamos una variable la cual contiene esa informacion asi que la pasamos mas o menos asi.

~~~
html_content = requests.get(url).text  # Obtenemos la pagina en formato html
~~~
Usamos .text para guardar en la variable la pagina en formato de texto.
<p align="center">
<img src="/imagenes/respuesta_requests.png"  height="200">
</p>
La imagen muestra un ejemplo de lo que podrias ver si tu ejecutas el codigo.

## **Paso 4**
### **Instanciar un objeto de la clase beautifulsoup**
<p align="center">
<img src="https://static.wikia.nocookie.net/kimetsu-no-yaiba/images/e/e1/Akaza_Full_Body_Design_%28Anime%29.png/revision/latest/scale-to-width-down/350?cb=20211013090054"  height="400">
</p>
AY MI MADREE!!! y no es el bicho, se nos ha aparecido Akasa una de las lunas superiores mejor conocido como el panadero, no te preocupes si crees que a ti tambien te hara una dona, tu deber es matarlo y aprender sobre web scraping.
Ahora utilizaremos la libreria de beautifulsoup, crearemos una variable llamada soup en la que instancearemos un objeto de la clase beautifulsoup con el contenido de nuestra pagina web como parametro es decir lo hecho anteriormente.

~~~
soup = BeautifulSoup(html_content)  # creamos una instancia de la libreria que importamos utilizando el contenido de la pagina (el texto html)
~~~

<p align="center">
<img src="/imagenes/vista.png"  height="400">
</p>
Veras que ahora lo que nos devuelve no es solo una linea, lo que nos devuelve ya es un poco mas al orden que tendria el codigo si una persona recien lo estaria escribiendo.


Antes de seguir quiero que mires la segunda linea que imprime el codigo en la imagen de arriba, comienza con "<title>" y termina con algo similar "</title>", esto es porque bueno, si no nos hemos dado cuenta ya es hora de darnos cuenta de que el texto que tenemos, lo que nos devolvio la pagina esta en html, html es un lenguaje que trabaja con etiquetas, estas etiquetas son usadas para referirse a partes de la pagina web, que se muestren y se organizen de una cierta manera, en este caso "title" esta haciendo referencia al titulo de la pagina web. el primer title hace referencia al inicio de esa parte y el segundo title a donde termina.
La funcion de beautifulsoup es convertir esas etiquetas en atributos por asi decirlo, entonces nosotros con eso podemos trabajar mas facil y con lo siguiente ya te estaras dando idea de lo que estaremos haciendo.

Ejemplo:
~~~
soup.title.text # ejemplo de conseguir el titulo de la pagina en este caso .text quita las etiquetas de los lados
~~~

Esto nos devolvera el titulo de la pagina que en este caso es: 'List of S&P 500 companies - Wikipedia' puedes verificarlo mirando el texto que viene en la pestaña de la pagina web.


