# Trabajo final
## Metodología aplicada a las actividades
Esta actividad final consiste en explicar cómo he realizado las tareas propuestas en la clase de periodismo de datos II. Para poder conocer más sobre nuestro aprendizaje, en este documento se explicará la metodología llevada a cabo para realizar cada una de las actividades dirigidas individuales.
Es importante comenzar señalando las herramientas que hemos utilizado a lo largo de este proceso:
* GitHub: Esta plataforma ha servido como repositorio para contener todos los trabajos realizados. Cuenta con su propio lenguaje, Markdown, el cual se basa en el uso de texto plano. Una de las primeras tareas de la asignatura fue la creación de un repositorio contenido en "nebrijas", el cual tenía que tener disponible la opción de GitHub pages activada para la creación de una sencilla página web final. 
* Anaconda/Jupyter: La poderosa herramienta Anaconda nos permitió acceder al cuaderno de Jupyter, necesario para completar la tercera y la cuarta actividad. En este se puede redactar tanto en Markdown como en Python, por lo que es perfecto para probar código y redactar trabajos de programación literaria.
* Pandas: esta librería permite manejar y analizar datos de manera más sencilla. Se basa en las estructuras de datos que mantiene la librería NumPy, y dispone de tres estructuras distintas: Series, DataFrame y Panel. 
Estas son las actividades realizadas a lo largo de la asignatura.
***
### Actividad Dirigida 1
Para poder completar esta actividad, comencé realizando un comentario crítico sobre una pieza de periodismo de datos. Por ello, seleccione una pieza de el periodico online **eldiario.es**, titulado "El mapa de las cesáreas en España: los hospitales que abusan de los partos quirúrgicos".
En un primer momento, lo pudimos compartir a través de un pad llamado "Riseup". Tras redactarlo con sintaxis Markdown, el lenguaje que utiliza Github, nuestra tarea fue pasarlo a nuestro repositorio en la web. Para conocer más sobre este lenguaje, utilicé internet para encontrar manuales que detallaran el lenguaje, como [la que dejó el profesor](https://flowsta.github.io/markdown) en la página de la asignatura en Blackboard. 
Estas son las etiquetas que utilicé a lo largo del texto:
* Encabezados de diferente nivel con almohadillas (#).
* Negrita, utilizando dos asteriscos (**) al principio y al final del texto que quería remarcar.
* Enlaces, con el texto a enlazar entre corcheas y el propio url entre paréntesis.
Para analizar correctamente los elementos que aparecían en la noticia, utilicé de referencia lo aprendido en ambas clases de periodismo de datos.
La actividad, que exigía el uso de entre 300 y 500 palabras, fue una precursora al resto de actividades que realizaríamos a lo largo de las clases. Esta fue un adecuado ejercicio introductorio, ya que facilitó el aprendizaje del Markdown, haciendo que nos sintieramos más comodos con su uso para posteriores actividades.
Actualmente se aloja [en este enlace](https://github.com/nebrijas/2022online-erika-martin/blob/main/ad1.md). Como se puede observar, se encuentra dentro de un repositorio de GitHub nombrada con el año en el que se ha cursado la asignatura y mi nombre de usuario, facilitando la localización dentro de la vista general.
***
### Actividad Dirigida 2
Una vez más, este consistiría de un comentario crítico que ocupara entre 500 y 700 palabras. Para la redacción de este ejercicio, escogí el títular "La “tripledemia”, una nueva amenaza", como variante del original "‘Tripledemia’ de toses y fiebres: bronquiolitis y gripes se adelantan con una covid en ligero ascenso". 
Escogí el artículo de Newtral debido a unas deficiencias a la hora de representar gráficamente el texto. Para poder identificarlas correctamente, acudí al material proporcionado en clase, cogiendo como referencia las seis claves de Edward Tufte. Estas son las siguientes: 
* La representación de los números, tal y como se miden físicamente en la superficie del gráfico, debe ser proporcional a las cantidades representadas.
* Los diseños únicamente pueden mostrar variaciones de datos, sin motivos ocultos.
* Hay que utilizar un etiquetado claro, detallado y minucioso, evitando así cualquier distorsión gráfica y ambigüedad posibles.
* Es importante mostrar la variación de los datos, no del diseño.
* En representación de series temporales de dinero, las unidades de medida monetaria deflactadas y estandarizadas son casi siempre mejores que las nominales.
* El número de distorsiones de información representada no debe superar el número de dimensiones de los datos. 
Gracias al primer ejercicio, pude realizar este de manera individual, sin ayuda de ningún apunte de Markdown. Aun así, decidí introducir algunos códigos nuevos para probar más características que GitHub puede ofrecer.
Cabe destacar que gráficos como el mostrado posteriormente no cumplen las características necesarias para ser considerados un buen trabajo gráfico, ya que no resulta claro para el lector.
![Segundo gráfico propuesto por Newtral](https://www.newtral.es/wp-content/uploads/2022/11/vrs-21-22_1.gif?x63937)
El paso final, como en todas las actividades dirigidas, fue añadirlo a nuestro repositorio personal para posteriormente crear una página web completa con GitHub Pages.
Esta segunda actividad está alojada [en este enlace](https://github.com/nebrijas/2022online-erika-martin/blob/main/ad2.md). 
***
### Actividad Dirigida 3
La tercera actividad fue dirigida a la programación literaria con Python, para el cual había que realizar la tarea de web scraping. Esta fue sin lugar a dudas una de las más complicadas para mi, ya que no estaba familiarizada con ninguno de estos términos. 
Para llevar a cabo este trabajo tuvimos que instalar Anaconda, un software conocido por ser una de las plataformas de ciencia de datos más populares. Uno de los programas que puede ser accedido desde Anaconda es Jupyter Notebook, el cual utilizamos para generar un cuaderno que mezcla el uso de Markdown con códigos de Python. Este editor tiene una interfaz relativamente sencilla, por lo que no fue muy complicado aprender a manejarlo de manera eficiente.
La Universidad Europea considera que el web scraping o 'raspado de páginas' es "una técnica que consiste en usar un software programado (bot, crawler o spider) para rastrear uno o varios sitios web y extraer automáticamente la información, los contenidos y otros datosque contienen". Es utilizado para analizar la competencia de un negocio a tiempo real, mejorar páginas webs de empresas, mejorar el posicionamiento SEO y la reputación una marca, identificar tendencias o para crear bases de datos. Nuestro profesor nos ofreció un archivo Python, de extensión .py, con la información necesaria para realizar la actividad. Esta se extendería en cinco pasos diferentes.
#### Comprobación de las librerías
Antes de comenzar con el web scraping fue necesario comprobar que se tienen todas las librerías necesarias. 
Para ello se llamó a la instalación de los siguientes módulos a través del comando "!pip":
* Request: su instalación está predeterminada, facilita el trabajo con peticiones HTTP.
* Pandas: utiliza estructuras de datos de la librería NumPy para manejar, analizar y procesar datos.
* Time: su instalación está predeterminada, realiza funciones relacionadas con el tiempo.
* Termacolor: permite imprimir texto con colores diferentes.
* CSV: su instalación está predeterminada, importa y exporta bases de datos.
* BS4: también conocido como Beautiful Soup, esta librería es utilizada para realizar trabajos de web scraping.
* Re: su instalación está predeterminada, proporciona operaciones de coincidencia de expresiones regulares.
```python
timport requests
import time
import csv
import re
from bs4 import BeautifulSoup
import os
import pandas as pd
from termcolor import colored
```
Una vez importadas a través del código "import", se llamó a la página de resultados con la variable "resultados = []", utilizando la función type para organizar los datos en una lista.
```python
resultados = []
type(resultados)
```
#### Accediendo a los datos de El País
El medio de comunicación investigado fue El País, del cual logramos obtener el resultado mejor posicionado en cada uno de sus apartados según la popularidad de sus etiquetas.
Para poder solicitar la información pertinente, se realizó una llamada con el método "get" a la variable "req", especificando una condicional con el cual reconocer si el valor es igual a 200.
```python
req = requests.get("https://resultados.elpais.com")
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup = BeautifulSoup(req.text, 'html.parser')
```
A partir de este momento ya se pudieron buscar todas las etiquetas posibles a través de la siguiente función, la cual pudo recopilar todas aquellas que cumplieran la condición de ser un encabezado "h2". Además, lo imprimiremos con "print".
```python
tags = soup.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```
#### Web scraping en otras secciones
Para poder completar esta actividad fue necesario repetir esta acción con las siguientes secciones:
* Internacional
* Opinión
* España
* Economía
* Sociedad
* Educación
* Clima y medio ambiente
* Ciencia
* Cultura
* Babelia
* Deportes
* Tecnología
* Gente
* Televisión
* EPS
#### Conocer más sobre el estilo del periódico
Finalmente, tras realizar el trabajo de impresión correspondiente en todas las secciones, se limpiaron los resultados para mejorar la visualización con esta función:
```python
os.system("clear")
```
Y lo último que se trabajó fue el uso del atributo "colored", el cual facilita la distinción de los titulares a través de un cambio en el estilo de la fuente. Para ello podría utilizarse la siguiente función:
```python
print(colored("A continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:", 'blue', attrs=['bold']))
print(colored("Feminismo", 'green', attrs=['bold']))
str_match = [s for s in resultados if "feminismo" in s]
print("\n".join(str_match))
```
Gracias al condicional "if", podremos limitar los resultados a aquellos que cumplan las condiciones señaladas en la variable "str_match". Es decir, todos aquellos titulares que contengan la palabra "feminismo" pasaran a ser verdes y contar con el estilo de negrita. En el ejercicio, repetimos el proceso con las siguientes palabras:
* Igualdad
* Mujeres
* Mujer
* Brecha salarial
* Machismo
* Violencia
* Maltrato
* Homicidio
* Género
* Asesinato
* Sexo.
Esta segunda actividad está alojada [en este enlace](https://github.com/nebrijas/2022online-erika-martin/blob/main/ad3.md). 
***
### Actividad Dirigida 4
Esta fue la última actividad dirigida, y fue realizada paso a paso en clase. Bajo de mi punto de vista, se trata de una de las más provechosas, ya que aprendimos a utilizar "Pandas", la librería de Python que conocimos en el ejercicio pasado, para trabajar con datos y crear una visualización.
La información fue cogida de una API pública del Covid-19, y [fue llevada a cabo en el cuaderno de Jupyter](https://github.com/nebrijas/2022online-erika-martin/blob/main/docs/ad4.ipynb). Tal y como ocurrió con la tercera actividad, esta sería construída mediante una serie de pasos.
#### Instalación y configuración de Pandas
Ya que en la tercera actividad ya instalmos Pandas, esta vez no fue necesario realizarlo. Aun así, en caso de no haberlo hecho previamente, se habría utilizado el comando "!pip" tal y como se ve en el siguiente cuadro de comandos:
```python
!pip install pandas
```
Para llamarlo, se utilizó la convención "pd" como abreviatura para llevarlo a la librería.
```python
import pandas as pd
```
#### Crear la variable
Para crear la variable, se utilizó el símbolo "=" junto al enlace entrecomillado, introduciendo el término "miurl" el cual resultó ser igual a la url propuesta. Para conocer que se trata de una cadena de caracteres, utilizamos el comando "type".
```python
miurl = "https://api.covid19api.com/countries"
type(miurl)
```
#### Construir el dataframe
Para aclarar cuál es el valor de lo que tenía que leer, se utilizó la función "read:json()" a través del siguiente código:
```python
df = pd.read_json (miurl)
```
Así, este se convirtió en un cuadro de alojamiento para la información, la cual podrá ser llamada con el objeto "df".
#### Explorar la tabla
Para poder conocer un poco más sobre los resultados, utilizamos las siguientes funciones:
* Para poder conocer los primeros seís países según su posición.
```python
df.head(6)
```
* Para conocer los seis últimos países según su posición.
```python
df.tail(6)
```
* Para saber más información sobre las variables que se encuentran en el dataframe.
```python
df.info()
```
* Para mostrar la variable del país.
```python
df['Country']
```
#### Realizar un gráfico con los nuevos datos
Finalmente, pudimos explorar un poco más los datos de países en concreto. En el caso de Colombia, por ejemplo, guardamos los datos dentro de "df_co" a través de este código:
```python
url_co = 'https://api.covid19api.com/country/colombia/status/confirmed/live'
df_co = pd.read_json(url_co)
df_co
```
Tras realizar las pertinentes búsquedas con las variables "head", "columns", "tail", "info" y "describe", pudimos elaborar un gráfico lineal sencillo desde cero. Este contenía la fecha en el eje X y los casos confinados en el eje Y. Para invocarlo, lanzamos un código que filtró las entradas por fecha.
```python
df_co.set_index('Date')
```
Posteriormente, añadimos los casos de confinamiento con el siguiente comando:
```python
df_co.set_index('Date')['Cases']
```
Y finalmente crearemos el gráfico impreso con la función "plot", la cual generará el producto final.
```python
df_co.set_index('Date')['Cases'].plot()
```
Para darle un toque más profesional, añadimos un título fácilmente con el atributo "title".
```python
df_co.set_index('Date')['Cases'].plot(title= "Casos de Covid-19 en Colombia")
```
Este ejercicio se completó continuando estos pasos más en profundidad con Ecuador, República Dominicana y España. Esta segunda actividad está alojada [en este enlace](https://github.com/nebrijas/2022online-erika-martin/blob/main/ad4.md). 
***
### Conclusiones
La asignatura Periodismo de Datos II, perteneciente al Máster en Periodismo Digital y de Datos, ha resultado ser una asignatura muy interesante. Dicho esto, creo que le hubieramos podido sacar más partido con un mayor conocimiento previo de herramientas web (GitHub, editores de texto online) y lenguajes de programación (Python). Algunas clases resultaron muy pesadas por nuestra falta de práctica, sobre todo relacionada con el aspecto más técnico de la asignatura.
Considero que esta clase me ha aportado conocimientos extra en GitHub, Jupyter Notebook y lenguajes como Python y Markdown. Además, pude conocer la importancia de la exactitud a la hora de redactar código, ya que un pequeño error puede afectar a la visualización de toda la actividad.
