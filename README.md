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

En caso de algun error instala la libreria "lxml"

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

## **Paso 5**
### **Buscar la tabla en la pagina web**

Ok, Akaza quiere vernos, nos quiere dejar ciegos y confusos, pero nosotros no nos dejaremos, lo siguiente podria ser el paso mas tedioso.
Has lo siguiente.
- Posicionate en la pagina web.
- En alguna parte de la pagina da click derecho.
- Selecciona la opcion que dice inspeccionar.
- En la parte derecha deberia abrirse una mini pestaña con codigo, si eso es lo que paso, vamos bien.

Te estaras preguntando que rayos es eso, eso que ves es la pagina web pero en su forma de codigo osea el archivo html, lo mismo que nosotros tenemos ahora mismo en nuestro python.

¿Que es lo que tenemos que hacer?

Buscar la etiqueta que hace referencia a la tabla que queremos y conseguir algo que la identifique, ¿Por que? porque nuestra pagina web tiene 2 tablas, es probable que si tuvieramos una no habria problema, pero al ser dos, debemos poder diferenciarla de la otra para poder obtener los datos.

¿Como haremos eso?
Cada que tu pasas el cursor por el codigo que recien abriste en la pagina web, se sombrea la parte a la que hace referencia.

imagina que mi cursor es la mancha verde.

<p align="center">
<img src="/imagenes/sombra.png"  height="400">
</p>
Si se sombrea la parte de la izquierda de algun color es porque ese codigo hace referencia a esa parte, podemos navegar dentro del codigo hasta encontrar nuestra tabla que en este caso esta con la etiqueta "table".

<p align="center">
<img src="/imagenes/sombra2.png"  height="400">
</p>
LA ENCONTRAMOS!!

Una vez que la encontramos escribimos el siguiente codigo.

~~~
tabla_500 = soup.find("table", attrs={"id": "constituents"})  # attrs una manera de identificar la tabla en la pagina
~~~

creamos una nueva variable la cual contendra la informacion de la tabla (desde "<table.> hasta </table.>" le puse un punto para que se vea) eso lo hacemos con la funcion find() la cual lo que hace es buscar la etiqueta y con un atributo que es el que identifica a la tabla, en la imagen puedes ver que el id tiene el valor "constituents" que es el mismo que estamos pasando como parametro para poder identificar la tabla. Mas abajo en la misma imagen aparece la otra tabla, puedes ver que es diferente.

Ahora mismo estamos listos para sacar la info.

## **Paso 6**
### **Obtener los encabezados de nuestra tabla**

<p align="center">
<img src="https://e1.pxfuel.com/desktop-wallpaper/731/501/desktop-wallpaper-akaza-kimetsu-no-yaiba-kyojuro-rengoku-demon-slayer-kimetsu-no-yaiba-akaza.jpg"  height="400">
</p>

Nuestro enfrentamiento contra Akaza a comenzado, tenemos que encontrar el nombre de las columnas para debilitarlo.

Como hacemos eso?
~~~
encabezados = tabla_500.tbody
linea_encabezado = encabezados.tr
linea_encabezado
~~~

Dentro de nuestra tabla hay una etiqueta llamada tbody la cual contiene el cuerpo de nuestra tabla, la primera linea de el codigo de arriba hace referencia a eso, lo que esta haciendo es tener los datos a partir de ahi, imagina que la tabla es un platano, has de cuenta que lo estas pelando.

La segunda linea esta haciendo lo mismo, la etiqueta se llama tr observa lo que devuelve.

<p align="center">
<img src="/imagenes/encabezados.png"  height="400">
</p>

Dentro de las etiquetas tr se encuentran las etiquetas th que son las que contienen la informacion correspondiente a los nombres de las columnas, que se les ocurre hacer para obtener esa informacion?. EXACTO una iteracion.

~~~
#lista para guardar los nombres de las columnas
columnas = []


for th in linea_encabezado.find_all("th"):  #Busco este valor en mis datos ya que ahi se encuentran los nombres de los encabezados
    columnas.append(th.text.replace("\n", "").strip()) # Limpio el nombre y lo agrego a la lista
    
columnas
~~~

Lo que estamos haciendo es iterar por cada etiqueta th y extrayendo la informacion que nececitamos.

<p align="center">
<img src="/imagenes/encabezados_limpio.png"  height="400">
</p>

## **Paso 7**
### **Obtener los datos de la tabla**

Ya que tenemos el nombre de las columnas ahora toca sacar los datos y para esto haremos algo similar a lo de arriba
<p align="center">
<img src="/imagenes/datos_html.png"  height="400">
</p>

~~~
filas = [] # lista que contendra cada fila

for linea in datos_tabla.find_all("tr"): # Cada que pasemos por un valor tr creamos una lista
    fila = []
    for td in linea.find_all("td"):   # Cada que pasemos por valores td agregamos el texto a la lista que creamos un paso antes
        fila.append(td.text.replace("\n","").strip())
    filas.append(fila)   # Esa lista recien creada la agregamos a la lista llamada filas

filas.remove([]) # Los encabezados no tenian td por lo que no recopilo info pero si genero una lista vacia
~~~

<p align="center">
<img src="/imagenes/datos_limpio.png"  height="400">
</p>

## **Paso 8**
### **Crear un Dataframe**

<p align="center">
<img src="https://www.geekmi.news/__export/1624295721382/sites/debate/img/2021/06/21/akavsren.jpg_423682103.jpg"  height="400">
</p>

Despues de un largo trabajo por fin hemos derrotado a Akaza, ya tenemos nuestros datos y tambien tenemos el nombre de las columnas entonces esa informacion la podemos usar para crear un dataframe 

~~~
df = pd.DataFrame(data=filas, columns=columnas)
df.head()
~~~

<p align="center">
<img src="/imagenes/dataframe.png"  height="200">
</p>




