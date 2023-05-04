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
