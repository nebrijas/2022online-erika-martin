# Ejercicio de programación literaria con Python
Esta tercera actividad dirigida consiste en realizar un ejercicio de programación literaria haciendo uso de un código de programación con Python ya existente, en el que llevamos a cabo web scraping. El archivo de documento trabajado en el cuaderno Jupyter también [está colgado dentro de la carpeta "docs"](docs/ad3).

## Librerías
Para comenzar, tal y como hemos visto en clases, tendremos que asegurarnos de que todas las librerias necesarias para comenzarla tarea de web scraping estén correctamente instaladas. Para ello, vamos a intentar llamarlas utilizando una serie de variables.


```python
import requests
import time
import csv
import re
from bs4 import BeautifulSoup
import os
import pandas as pd
from termcolor import colored
```


    ---------------------------------------------------------------------------

    ModuleNotFoundError                       Traceback (most recent call last)

    ~\AppData\Local\Temp\ipykernel_18868\1800187364.py in <module>
          6 import os
          7 import pandas as pd
    ----> 8 from termcolor import colored
    

    ModuleNotFoundError: No module named 'termcolor'


En caso de percibir errores, es probable que estemos ante un problema que denota que las bibliotecas no han sido instaladas. Si no se cono la naturaleza de cada librería, y por lo tanto no se sabe cómo instalar, tendríamos que acudir al navegador web a buscarlo.

### Requests
Según la página web especializada en Python [J2logo](j2logo.com), esta es una librería que facilita el trabajo con peticiones HTTP. 
En caso de querer instalar esta librería, habrá que utilizar la siguiente función valiendose del gestor de paquetes pip:


```python
!pip install requests
```

    Requirement already satisfied: requests in c:\users\erika\anaconda3\lib\site-packages (2.28.1)
    Requirement already satisfied: idna<4,>=2.5 in c:\users\erika\anaconda3\lib\site-packages (from requests) (3.3)
    Requirement already satisfied: certifi>=2017.4.17 in c:\users\erika\anaconda3\lib\site-packages (from requests) (2022.9.14)
    Requirement already satisfied: charset-normalizer<3,>=2 in c:\users\erika\anaconda3\lib\site-packages (from requests) (2.0.4)
    Requirement already satisfied: urllib3<1.27,>=1.21.1 in c:\users\erika\anaconda3\lib\site-packages (from requests) (1.26.11)
    

En caso de querer hacer una petición, habrá que invocar la función get(), tal y como vemos en el bloque de código del que hablabamos al comienzo del ejercicio.

### Time
La [página web de Python](https://docs.python.org/es/3/library/time.html) señala que se trata de un "módulo (que) proporciona varias funciones relacionadas con el tiempo". Esta permitiría acceder a conversiones horarias. 
Al formar parte de la librería estandar del lenguaje de programación, no es necesario instalarla. 

### CVS
Según la [página web de Python](https://docs.python.org/es/3/library/cvs.html), este es "el formato más común de importación y exportación de hojas de cálculo y bases de datos". Este módulo del lenguaje de programación "implementa clases para leer y escribir datos tabulares en formato CSV".
Al formar parte de la librería estandar del lenguaje de programación, no es necesario instalarla.

### Re
La [página web de Python](https://docs.python.org/es/3/library/re.html) señala que este módulo "proporciona operaciones de coincidencia de expresiones regulares similares a las encontradas en Perl". Todas ellas utilizarán el carácter de barra inversa para indicar formas especiales o permitir el uso de carácteres especiales.
Al formar parte de la librería estandar del lenguaje de programación, no es necesario instalarla. 

### BS4
Tal y como indica la página web especializada en Python [J2logo](https://j2logo.com/python/web-scraping-con-python-guia-inicio-beautifulsoup/), la librería BS4 también es conocida como Beautiful Soup. Es muy utilizada para realizar web scraping, técnica que se puede utilizar en proyectos de Big Data o Machine Learning.
En caso de querer instalar esta librería, habrá que utilizar la siguiente función valiendose del gestor de paquetes pip:


```python
!pip install beautifulsoup4
```

    Requirement already satisfied: beautifulsoup4 in c:\users\erika\anaconda3\lib\site-packages (4.11.1)
    Requirement already satisfied: soupsieve>1.2 in c:\users\erika\anaconda3\lib\site-packages (from beautifulsoup4) (2.3.1)
    

Además, también se podría instalar a la vez el parser "lxml" utilizando a su vez el mismo gestor de paquetes. 


```python
!pip install lxml
```

    Requirement already satisfied: lxml in c:\users\erika\anaconda3\lib\site-packages (4.9.1)
    

### Pandas
La [página web de Hubspot](https://blog.hubspot.es/website/que-es-pandas-python) señala que esta es una de las librerías más utilizadas para el manejo, anális y procesamiento de datos. Se basa en las estructuras de datos que mantiene la librería NumPy, y dispone de tres estructuras distintas: Series, DataFrame y Panel.
En caso de querer instalar esta librería, habrá que utilizar la siguiente función valiendose del gestor de paquetes pip:


```python
!pip install pandas
```

    Requirement already satisfied: pandas in c:\users\erika\anaconda3\lib\site-packages (1.4.4)
    Requirement already satisfied: pytz>=2020.1 in c:\users\erika\anaconda3\lib\site-packages (from pandas) (2022.1)
    Requirement already satisfied: numpy>=1.18.5 in c:\users\erika\anaconda3\lib\site-packages (from pandas) (1.21.5)
    Requirement already satisfied: python-dateutil>=2.8.1 in c:\users\erika\anaconda3\lib\site-packages (from pandas) (2.8.2)
    Requirement already satisfied: six>=1.5 in c:\users\erika\anaconda3\lib\site-packages (from python-dateutil>=2.8.1->pandas) (1.16.0)
    

### Termcolor
Según indica [la página web Replit](https://replit.com/talk/learn/How-to-Use-Termcolor-In-Python/24684), el módulo termcolor permite imprimir texto con colores. 
En caso de querer instalar esta librería, habrá que utilizar la siguiente función valiendose del gestor de paquetes pip:


```python
!pip install --upgrade termcolor
```

    Collecting termcolor
      Downloading termcolor-2.1.1-py3-none-any.whl (6.2 kB)
    Installing collected packages: termcolor
    Successfully installed termcolor-2.1.1
    

## Comienzo del ejercicio
Como primer paso, volvemos a importar las librerías necesarias, ahora que tenemos todas las necesarias. Para ello utilizaremos la siguiente función, tal y como hicimos al comienzo del documento:


```python
import requests
import time
import csv
import re
from bs4 import BeautifulSoup
import os
import pandas as pd
from termcolor import colored
```

Posteriormente llamamos a la página de resultados con la siguiente variable.


```python
resultados = []
```

Para poder organizar correctamente los datos, utilizaremos la función "type".


```python
type(resultados)
```




    list



## Acceder a los datos de El País
Es en este momento cuando realizamos la primera petición de obtención de datos a través de la variable "req". Tal y como se muestra en la siguiente función, esto marcaría el uso de la librería requests.


```python
req = requests.get("https://resultados.elpais.com")
```

A continuación haremos uso de un condicional, con el que conoceremos si el valor es igual a 200, y lanzará un error en caso de que sea otro.


```python
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup = BeautifulSoup(req.text, 'html.parser')
```

Tras realizar esta acción, comenzará a trabajar la librería BS4 o Beautiful Soup. Este comando es el encargado de comenzar con el web scraping. Comenzamos buscando todas las etiquetas posibles con la función "tags", lo que dará una serie de tutulares que cumplan la condición de ser "h2".


```python
tags = soup.findAll("h2")
```

Es entonces cuando utilizaremos "print" para imprimir la información que le estamos solicitando.


```python
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Última hora
    El calendario
    Universo Mundial
    Las predicciones
    La ‘newsletter’
    La policía interceptó en  La Moncloa un sobre con material pirotécnico dirigido a Sánchez
    La censura del Congreso a Marlaska por Melilla deja su futuro en manos de la Fiscalía
    La Eurocámara presionará para que el ministro dé explicaciones sobre la tragedia 
    Superviviente de una mara hondureña: “No me enteré de que a mi hija la violaron a punta de pistola hasta que llegué a España”
    Cómo detectar una crisis de ansiedad y qué hacer
    ‘As bestas’, de Rodrigo Sorogoyen, lidera la carrera a los Goya con 17 nominaciones
    Empecinamiento sobre Melilla 
    Abolir la prostitución
    Bildu como ‘síntoma’ generacional
    Carta de socorro
    Las píldoras de Enzensberger
    España se ve lanzada  
    Joshua Kimmich bajo vigilancia
    Marruecos, ante el mayor desafío histórico desde el 86
    ¿Qué opciones tiene cada selección de pasar a octavos?
    La pensión máxima subirá un 3% hasta 2050 y la cotización más alta lo hará un 35%
    Malestar en el Gobierno y el PSOE con Montero por acusar al PP de promover la cultura de la violación
    Todo el PP en ‘El escaño de Satanás’
    Ayuso se compromete con Vox a borrar la autodeterminación de género de las leyes en Madrid
    Las 72 horas de crisis en Ciudadanos: Villacís sufre la primera gran baja en Madrid y Almeida se frota las manos
    El desafío de envejecer con VIH: “Las personas de largo recorrido sufrimos depresión y ansiedad”
    Solo el 44% de los adolescentes con conductas suicidas ha recibido tratamiento psicológico en los últimos tres años
    Elon Musk asegura que en seis meses se implantará el primer chip en un cerebro humano con Neuralink
    El historiador Serhii Plokhy: “El destino de la guerra está claro: Rusia se debilita y Ucrania será independiente”
    Vídeo | ¿Qué hay en la cabeza de un soldado de la guerra? Estas son sus heridas mentales
    Condenada por hurto en supermercados: “Lo mejor que me podía haber pasado fue ir a prisión”
    La SER se consolida como la radio más escuchada con 4.161.000 oyentes
    Carlos Navarro, ‘El Yoyas’, en busca y captura para ingresar en prisión por maltratar a su expareja e hijos
    Cepsa invertirá 3.000 millones en el mayor proyecto de hidrógeno verde de Europa
    La empresa detrás de Conga, el robot aspirador que revolucionó los hogares españoles y que hoy factura 300 millones de euros
    El tiempo en el puente de diciembre: primero frío y, después, lluvias generalizadas
    Shakira y Piqué sellan su acuerdo de separación en Barcelona ante el juez
    Estas son las mejores series de diciembre
    Aló Comidista: “Si dejas la piña boca abajo, ¿se pone más dulce?”
    Convierta su comunidad en ‘Aquí sí hay quien viva’ (gracias al cubo de basura)
    Kevin de Bruyne, entre la frustración y el miedo ante el día decisivo de Bélgica contra Croacia
    México se queda a un gol del pase 
    Argentina se gana los octavos 
    Olga Viza: “Llevé la copa del Mundial de España 82 de copiloto en mi coche con la L en el cristal”
    Los vídeos de los goles y el resumen de la jornada 11
    Catarí que te vi: cómo llenar el depósito de gasolina por 22 euros en Qatar
    Ramón Besa, periodista de EL PAÍS: “Nadie juega como España”
    Busquets: “Me sorprendió el talento de Gavi y Pedri cuando llegaron al equipo”
    La historia de una niña que soñó con ser pianista
    Pon nombre a lo que te pasa para sentirte mejor
    Volver a empezar
    Temporeros de Jaén duermen a la intemperie aunque los albergues están semivacíos
    ‘Mujeres de armas tomar’: la historia de la víctima, que desesperada por justicia, se vengó de sus violadores
    Encontrados 170 escritos inéditos del poeta Miguel Hernández
    El euríbor cierra noviembre en su mayor nivel desde 2008: la cuota de los que revisen ahora su pago crecerá un 44%
    Estos picos han enamorado al chef José Andrés y están hasta en las mesas de Corea del Sur
    La primera simulación cuántica de un agujero de gusano abre una nueva puerta para entender el universo
    Del referéndum de Cataluña a #Cuéntalo: los archiveros guardan tuits que han hecho historia
    Ninguneo administrativo al ciudadano: recibos del IBI que no llegan, llamadas sin respuesta y fallos técnicos
    Hungría evita la confrontación con Bruselas y confía en desbloquear los fondos europeos en 2023
    La ONU advierte de que una de cada 23 personas requerirá ayuda humanitaria en 2023
    ‘Podcast’ | China pide libertad, no democracia
    Videonálisis | Así pueden afectar las protestas al Gobierno chino
    El número de españoles en cárceles extranjeras repunta un 15% tras el fin de la pandemia
    ¿Qué beneficios aportan los alimentos húmedos a las mascotas?
    Juana Dolores, la nueva ‘enfant terrible’ de la cultura catalana: “Hay mucho silencio y autocensura en la literatura”
    La respuesta a la guerra en Ucrania también es literaria
    Felix Klieser: un virtuoso de la trompa (sin brazos)
    Muere Christine McVie, cantante y teclista de la legendaria banda Fleetwood Mac
    Glashütte, el pueblo alemán convertido en capital mundial de los relojes con denominación de origen
    Al norte del Norte: por la remota Ruta de la Costa Ártica de Islandia 
    Vídeo | La canción de Antonio Carmona a su padre sobre el alzhéimer: “La escuchó antes de morir”
    Restaurante El Señor Martín, el paraíso marinero también está en Madrid
    Club Welnia, el programa que nos acompaña en todo momento
    El papel de Marruecos y España en las muertes del 24-J
    Luisita, contra el Estado por la herencia de seis millones de una prima con la que ni hablaba
    Los médicos privados se sienten “humillados”: los técnicos cobran 60 euros por arreglar una lavadora y los sanitarios, 10 por consulta
    La guerra bajo cero en Ucrania: ‘congelarse’ o emigrar
    La respuesta de la primera ministra de Nueva Zelanda a una pregunta machista: “¿Os reunís por tener una edad parecida?”
    
    Irene Montero, al PP en el Congreso: “Ustedes promueven la cultura de la violación”
    ‘Tu opinión es una mierda’: la campaña que alerta sobre los peligros de la polarización
    La educación financiera se convierte en la llave de la inclusión
    ‘La mirada del paciente’: historias sin filtro detrás de las personas
    Hacia un 2025 más justo, más conectado y más sostenible
    Nicolás Maduro condiciona la celebración de elecciones libres al levantamiento de sanciones 
    Alemania suaviza su ley de inmigración para atraer trabajadores extranjeros de fuera de la UE
    Una globalización centrada en los seres humanos
    Defensa invertirá 80 millones en su futuro Sistema de Combate en el Ciberespacio
    Xavier Trias ficha a Alsina, Calvet y Tremosa para la candidatura de Junts al Ayuntamiento de Barcelona
    Yolanda Díaz apuesta por “tender la mano” al Gobierno mexicano
    Prisa presenta el plan para redoblar su apuesta por la sostenibilidad
    ‘Los desafíos al proceso de transición ecológica’, por José Donoso
    Arabia Saudí encarga otros cinco buques de guerra a Navantia 
    PSOE y Unidas Podemos aplazan el debate sobre la autodeterminación de género en la ‘ley trans’
    Un plan de choque de 356 millones para intentar salvar Doñana de su creciente declive 
    Cataluña afronta el invierno de la crisis energética con solo 42 contadores sociales de luz
    El retraso en resolver contratos predoctorales deja en el limbo a cientos de jóvenes: “Es la desesperación” 
    El estrés académico lastra el aprendizaje de los niños de nivel socioeconómico bajo
    ‘Phishing’, ‘malware’ o ‘ransomware’: el reto de formar en ciberseguridad tras la pandemia
    La prohibición del maíz transgénico abre un nuevo foco de tensión entre EE UU y México
    Un plan de choque de 356 millones para intentar salvar Doñana de su creciente declive 
    Portugal, el secreto de un país sin bicicletas que se convirtió en el mayor fabricante europeo
    75 años de la muerte de G.H. Hardy, un matemático excéntrico y brillante
    Hallan en Transilvania una nueva especie de dinosaurio enano herbívoro que vivió hace 70 millones de años
    Un fármaco experimental contra el alzhéimer confirma efectos positivos, pero puede estar detrás de la muerte de dos pacientes 
    Ronna, ronto, quetta y quecto, los nuevos prefijos para magnitudes extraordinarias
    La Policía de San Francisco contará con robots con capacidad de matar
    Damian Burns, director de Twitch Europa: “No me importaría que mi hija fuera ‘streamer’”
    Jugar para tu país
    ‘Mi tío Ricardo y la antena de la tele’, por Rafa Cabeleira
    Pelé se mantiene estable tras ser hospitalizado de manera inesperada en São Paulo
    El Sónar 2023 anuncia a Richie Hawtin, Laurent Garnier o The Blessed Madonna entre sus primeros artistas invitados
    ¿Quedan cines de barrio? ¿Toda España se hizo artista en el confinamiento? ¿Importan los premios? Los números responden
    El arte reivindica la belleza y la fragilidad del vidrio
    Borja Cobeaga: “Tardé más en sacarme el carné que en hacer esta serie”
    ‘El presidente: juego de la corrupción’, los entresijos del fútbol’, por Ángel Sánchez-Harguindey
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    Buckingham fuerza la dimisión de una asistente de la reina Camila por sus comentarios racistas
    Los príncipes de Gales emulan en su viaje a Boston la visita que la reina Isabel II hizo a la ciudad en 1976
    Spotify Wrapped, el selfi musical que monopoliza la conversación en Twitter y acaricia el ego
    La economía solidaria: un nuevo modelo financiero contra la desigualdad y la emergencia climática
    Alima tiene bronquiolitis, pero no hay oxígeno para evitar su asfixia en el hospital de Etiopía
    Muchos hombres, una sola mujer
    El misterio de Manuel Carrasco: cómo salir de una barriada de pescadores y acabar siendo un cantante que llena estadios
    El lamentable caso de Anne Hathaway o por qué se odia a algunas famosas sin justificación ninguna
    Samantha Hudson: “Me va bien económicamante, pero no soy Paula Echevarría”
    “Tobogán de piojos”, “genocida de oxígeno”... Por qué cada Mundial recuerda el poderío del español como idioma para insultar
    Alejandro Jato, el actor que será Camilo Sesto: “Da pena la imagen que los jóvenes tienen de él, con lo grande que fue”
    Una apasionante ruta por el patrimonio español en peligro de desaparecer
    Nuevos estadios, edificios de premios Pritzker y los zocos de Doha: Qatar, sede de la arquitectura mundial
    La polarización es como las drogas: engancha
    Descansar está mal visto: el arte perdido del reposo
    Madrid, la nueva Miami: así se han hecho con la capital los ricos latinoamericanos
    Si no tiene ahorros, esta es una de las pocas alternativas para comprar casa
    Roe Ethridge, el fructífero intercambio entre el arte y el comercio
    ‘La última vez’, de Guillermo Martínez: un laberinto con final milagrosamente imprevisible
    Cómo será el descuento de 20 céntimos en la gasolina en 2023
    El coche que se anticipa al declive de los SUV 
    Pollo asado con pomelo y dátiles
    Para qué sirve cada tipo de cebolla (y un truco para no llorar al picarla)
    Francesc Cambó i Jordi Pujol davant del mirall
    En teoria, és progressista
    Pilar Bonet dedica a los periodistas que cubren la guerra de Ucrania el premio Francisco Cerecedo de periodismo 
    Taller de ‘podcast’ narrativo
    La cubertería dorada ideal para esta Navidad: elegante, de 30 piezas y en oferta
    Los mejores termostatos inteligentes último modelo con los que ahorrar en calefacción
    11 protectores autoadhesivos de paredes y esquinas del garaje para aparcar tranquilo
    Siete gorros de invierno para hombre por menos de 20 euros
     Este árbol de Navidad, que arrasa en Amazon, tiene efecto brillo y se vende en cuatro tamaños
    Hildalgo pide más dinero por Air Europa y retrasa la venta
    El emotivo mensaje de un padre a los médicos que salvaron a su hijo: “Me han dado la vida”
    Antón Losada explica en qué se diferencia lo que ha hecho Irene Montero de lo que hace siempre Vox
    João ya tiene precio: 100 millones
    ¿Sirve para algo el boicot personal e intransferible al Mundial de Qatar?
    Confirmados los juegos gratis de PS Plus en diciembre de 2022 para PS5 y PS4
    

## El trabajo continúa con otras secciones
Este trabajo explora otras secciones de la página web de el diario El País. Por lo tanto, repetiremos este proceso con la url de la sección de internacional. 
Una vez más, limitaremos el valor a 200 y solicitaremos el acceso a través de la librería requests. La variable pasa a ser "req2".


```python
req2 = requests.get("https://elpais.com/internacional")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup2 = BeautifulSoup(req2.text, 'html.parser')
```

De nuevo, buscaremos todas las etiquetas "h2" y las imprimimos.


```python
tags = soup2.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    El historiador Serhii Plokhy: “El destino de la guerra ya está claro: Ucrania será independiente y Rusia queda tremendamente debilitada”
    Hungría evita la confrontación con Bruselas y confía en desbloquear los fondos europeos en 2023 
    Bruselas promueve un tribunal especial para juzgar a la cúpula de Putin por sus crímenes en Ucrania
    Una globalización centrada en los seres humanos
    Autocracia en crisis
    “¿De qué color es el hambre, mamá?”
    China: una protesta nacional
    Publicar no es un delito
    Bruselas exige congelar fondos europeos a Hungría por las violaciones del Estado de derecho
    Hungría acelera las medidas anticorrupción para rebajar la magnitud del castigo europeo
    China relaja las medidas anticovid en Guangzhou para frenar nuevas protestas
    Nicolás Maduro condiciona la celebración de elecciones libres al levantamiento de sanciones 
    Muere el expresidente de China Jiang Zemin
    La doble respuesta de China a las protestas: acelerar la vacunación de los mayores y descabezar las manifestaciones 
    La selección del jurado popular marca el inicio del juicio por los atentados yihadistas de 2016 en Bruselas
    La OTAN redobla su alerta sobre una China en ebullición
    La tragedia de los menores en zona de guerra: 230 millones de niños viven en los conflictos más cruentos del mundo
    Macron viaja a Washington para “resincronizarse” con Biden ante el impacto de la guerra en Ucrania
    Rusia culpa a EE UU de la cancelación del encuentro bilateral sobre control de armas nucleares
    Quince periodistas e integrantes de ‘El Faro’ demandan al fabricante del software espía Pegasus 
    La hija de Hugo Chávez califica de “grotesco” un video oficialista en homenaje a su padre
    Nueva York internará en psiquiátricos contra su voluntad a las personas sin hogar con trastornos mentales graves
    El líder del grupo ultraderechista Oath Keepers, culpable de sedición por el asalto al Capitolio
    Estados Unidos prepara una ley para evitar una huelga de ferrocarriles en vísperas de Navidad
    

Realizaremos el mismo trabajo con las secciones de opinión, España, economía, sociedad, educación, clima y medio ambiente, ciencia, cultura, babelia, deportes, tecnología, gente, televisión y eps. Estas serian las funciones a lanzar. 

### Opinión


```python
req3 = requests.get("https://elpais.com/opinion")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup3 = BeautifulSoup(req3.text, 'html.parser')

tags = soup3.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Empecinamiento sobre Melilla 
    Proteger al Constitucional
    República federal laica
    Abolir la prostitución
    ‘A compás’
    Las píldoras de Enzensberger
    Bildu como ‘síntoma’ generacional
    Pedro Sánchez pasará a la historia
    Autocracia en crisis
    Las sombras de TikTok
    Carta de socorro
    Planes para frenar el suicidio
    Brasil en transición
    La celebración de dar gracias
    Cadáveres exquisitos
    El Roto
    Flavita Banana
    Riki Blanco
    Peridis
    Sciammarella
    Envía tu carta
    La salud es más importante que la báscula
    Así funciona la corrupción
    Mucho texto
    Noticias positivas en tiempos caóticos
    Bomba nuclear en Barcelona
    Una maldita lista en tiempos airados
    El defensor del lector contesta
    

### España


```python
req4 = requests.get("https://elpais.com/espana/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup4 = BeautifulSoup(req4.text, 'html.parser')

tags = soup4.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    La censura del Congreso a Marlaska por la tragedia de Melilla deja su futuro en manos de la Fiscalía
    La Eurocámara presionará para que Marlaska dé explicaciones sobre la tragedia de Melilla
    Malestar en el Gobierno y el PSOE con Montero por acusar al PP de promover la cultura de la violación
    Alberto Núñez Feijóo, nacionalista
    La caverna
    Aunque nos tiemble la barbilla
    Orfandad representativa
    Otra forma de violencia política
    El número de españoles en cárceles extranjeras repunta un 15% tras el fin de la pandemia
    Defensa invertirá 80 millones en su futuro Sistema de Combate en el Ciberespacio
    Temporeros de Jaén duermen a la intemperie aunque los albergues están semivacíos
    Todos los partidos coinciden en acusar a Marlaska de mentir y engañar en su versión sobre la tragedia de Melilla el 24-J
    Nueva trifulca en el Congreso: Irene Montero pasa de atacada a provocadora
    El embajador de Ucrania y una empresa de armas reciben sendas cartas con sustancias deflagrantes
    Acnur cuestiona la legalidad de las devoluciones a Marruecos durante la tragedia de Melilla 
    El Constitucional rechaza celebrar ya un pleno para examinar a los dos magistrados designados por el Gobierno
    Lambán afirma que “mejor le habría ido a España” si Javier Fernández hubiese liderado al PSOE
    Los ciberataques más peligrosos a las redes públicas casi se duplican en España durante el último año
    Los tres polizones llegados a Gran Canaria piden asilo 
    Los hermanos que impulsaron una revolución tecnológica desde Valencia
    Hay casi 4.000 cervezas artesanas españolas. ¿Cómo probarlas todas?
    

### Economía


```python
req5 = requests.get("https://elpais.com/economia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup5 = BeautifulSoup(req5.text, 'html.parser')

tags = soup5.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    La pensión máxima subirá un 3% hasta 2050 y la cotización más alta, un 35%
    El euríbor cierra noviembre en su mayor nivel desde 2008: la cuota de los que revisen ahora su pago crecerá un 44%
    Cepsa invertirá 3.000 millones en el mayor proyecto de hidrógeno verde de Europa
    Transportes reforzará en 2023 la inspecciones para garantizar que los camioneros no trabajen a pérdidas
    Los desafíos al proceso de transición ecológica
    La moda de la sostenibilidad
    Impuesto erróneo a la banca
    Sufrimientos evitables
    El coste de la vida
    Cosecha de ingresos en las constructoras y concesionarias: facturan 6.000 millones más hasta septiembre
    Arabia Saudí encarga otros cinco buques de guerra a Navantia 
    Los ingresos tributarios hasta octubre ya superan lo recaudado en todo 2021
    Prisa presenta el plan para redoblar su apuesta por la sostenibilidad
    Estos picos han enamorado al chef José Andrés y están hasta en las mesas de Corea del Sur
    El BBVA gana a Merlin el arbitraje sobre la Operación Chamartín
    Breton exige a Musk que refuerce su política de moderación de contenidos y desinformación en Twitter
    Una celestina solar para instalar paneles
    España, en el podio de países de la OCDE con mayor alza de la presión fiscal en una década
    El gigante chino Alibaba lanza en España una nueva plataforma de comercio electrónico
    Powell sugiere que la Reserva Federal frenará el ritmo de subidas de tipos en diciembre
    Madrid, la nueva Miami: así se han hecho con la capital los ricos latinoamericanos
    Si no tiene ahorros, esta es una de las pocas alternativas para comprar casa
    Los efectos de una economía de andar por casa
    Caballos al galope: un negocio con un impacto económico de 7.400 millones de euros
    Los impuestos que se necesitan para construir la sociedad del futuro
    Hildalgo pide más dinero por Air Europa y retrasa la venta
    Órdago de los agentes sociales a Escrivá: sin acuerdo político no negocian el cálculo de la pensión
    Telefónica estudiará nuevas medidas de ahorro ante el escenario inflacionario
    Barceló irrumpe en la venta de Hotelatelier con una oferta de 200 millones de euros
    Por primera vez un juez declara nulo un contrato de alquiler por aplicación de la perspectiva de género
    Visitas a centros de acogida y muchas horas de estudio: así se forman los jueces en materia de género
    La justicia obliga a Iberia a controlar el peso de las maletas para que los azafatos no se lesionen
    ‘Phishing’, ‘malware’ o ‘ransomware’: el reto de formar en ciberseguridad tras la pandemia
    La difícil tarea de recuperar el talento investigador que un día hizo las maletas
    Descubre las formaciones de marketing ‘online’ más buscadas de 2023
    Logística de ida y vuelta, cuando la solución está en reciclar menos y reutilizar más
    Logística y digitalización, el manual de supervivencia para pymes
    Empleados satisfechos, empresas de éxito
    Diez claves del bienestar corporativo para empresas de éxito
    Las aventuras de un par de calcetines que dan empleo a todo un pueblo
    Cultura financiera como punto de partida para volver a empezar
    Cómo aplicar el ‘design thinking’ a cualquier negocio
    Las soluciones digitales que necesita mi negocio 
    Alexia Putellas, un Balón de Oro a base de “esfuerzo, constancia, disciplina y saber reinventarse”
    El método Muñoz para triunfar en cada reto que se propone
    ¿Por qué muchos inversores están volviendo a confiar en Japón?
    ¿Por qué se está enfriando la economía china?
    No una, sino cinco ‘startups’ para la esperanza
    Si tú lo imaginas, yo te lo imprimo
    Cómo garantizar la seguridad en un mundo de amenazas híbridas
    ¿Cuáles son los dilemas éticos del uso de la inteligencia artificial?
    Una alianza para que vuelvan a sonreír los más desfavorecidos
    Publicidad responsable y menos azúcar para un entorno alimentario saludable
    Barcelona, punta de lanza de la nueva filosofía de los polígonos industriales
    Cómo conseguir ayudas a la digitalización para autónomos y pymes con Kit Digital
    Un brindis con vino español por la sostenibilidad, la economía y el empleo
    

### Sociedad


```python
req6 = requests.get("https://elpais.com/sociedad/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup6 = BeautifulSoup(req6.text, 'html.parser')

tags = soup6.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    El retraso en resolver contratos predoctorales deja en el limbo a cientos de jóvenes: “Es la desesperación” 
    Condenada por hurto en supermercados: “Lo mejor que me podía haber pasado fue entrar en prisión”
    Así fue el ataque con ácido sulfúrico de ‘El Melillero’: “Perra, mongola, tonta”
    Qué es la cultura de la violación de la que habla Irene Montero
    La caja de resonancia de la angustia vital
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    Los secretos atronadores del secretario general
    PSOE y Unidas Podemos aplazan el debate sobre la autodeterminación de género en la ‘ley trans’
    Un plan de choque de 356 millones para intentar salvar Doñana de su creciente declive 
    España gana medio millón de habitantes en una década, pero siete de cada 10 municipios pierden población 
    El Senado de Estados Unidos aprueba una ley para blindar el matrimonio homosexual
    Solo el 44% de los adolescentes con conductas suicidas ha recibido tratamiento psicológico en los últimos tres años
    Bruselas quiere que todos los embalajes de la UE sean reciclables para 2030
    Qué es la cultura de la violación de la que habla Irene Montero
    ¿Adiós a los anuncios con coches para niños y cocinas para niñas? Los jugueteros pactan desterrar los estereotipos sexistas en la publicidad
    Portugal, el secreto de un país sin bicicletas que se convirtió en el mayor fabricante europeo
    Claves de la ley de trata: centrada en las víctimas y protección integral
    El estrés académico lastra el aprendizaje de los niños de nivel socioeconómico bajo
    Unas gafas que cambian la forma de ver el mundo
    Cambia tu relación con los papeles de la cocina
    Social, clínica y en primera persona. Tres visiones del VIH 
    Enfermería, los profesionales de las ‘curas invisibles’ en las personas con VIH
    Sostenibilidad y... ¡acción! 
    La huella de carbono, el rastro que marca el futuro del planeta
    Psoriasis, en las profundidades de la piel
    Contar para sanar
    Qué hacer con tres millones de colchones
    La nueva revolución agrícola 
    Lo lejos que se puede llegar con otra metodología educativa 
    Cuando el empleo se convierte en la mejor terapia 
    A solas con la obesidad
    Freno y marcha atrás en la obesidad infantil
    “La ópera, como la naturaleza, está viva, y debe evolucionar para ser eterna” 
    ¿Hasta dónde puede llegar el ser humano? El viaje a la oscuridad más absoluta
    El futuro de la alimentación se encuentra en el agua
    Acuicultura: la importancia de comer ‘azul’ para vivir en verde
    El futuro de la aviación verde
    En busca de la eficiencia energética en los aeropuertos
    Un día en el servicio de ayuda a domicilio
    Trabajadores esenciales. Los que nunca paran
    Añadir comida húmeda a la dieta de perros y gatos: beneficios palpables
    Consejos para alimentar correctamente a los animales de compañía
    Combatir el desperdicio alimentario desde la cesta de la compra
    Kilómetro cero para llenar la despensa
    Acompañamiento, el modelo alternativo de acogida de refugiados
    El metro como refugio. De los andenes de Madrid en 1936 a los de Kiev en 2022
    Yogures con menos azúcar, paso firme hacia la alimentación infantil del futuro
    Invisible, pero vital: el ciclo de las aguas subterráneas
    La bomba de calor, el sistema de climatización más sostenible y eficiente
    

### Educación


```python
req7 = requests.get("https://elpais.com/educacion/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup7 = BeautifulSoup(req7.text, 'html.parser')

tags = soup7.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    El retraso en resolver contratos predoctorales deja en el limbo a cientos de jóvenes: “Es la desesperación” 
    El estrés académico lastra el aprendizaje de los niños de nivel socioeconómico bajo
    ‘Phishing’, ‘malware’ o ‘ransomware’: el reto de formar en ciberseguridad tras la pandemia
    La escuela concertada matricula a la mitad del alumnado desfavorecido que le correspondería
    El Gobierno dará un subsidio de 400 euros anuales a los alumnos con necesidades especiales
    La expulsión de una clase en un colegio de Palma tras colocar una bandera de España deriva en graves amenazas a una profesora 
    Pobreza en el Olimpo académico de EE UU: la huelga en la Universidad de California es ya una de las más grandes del país
    El primer Mundial en horario lectivo y con ‘smartphones’ se juega también en los institutos
    El cabecilla de los cánticos machistas del Elías Ahuja vuelve al colegio mayor pese a anunciarse su expulsión definitiva
    La nueva ley de enseñanzas artísticas endurecerá los requisitos para ser profesor y hará más homogéneas las pruebas de acceso del alumnado
    Una madre denuncia insultos homófobos a su hija en un colegio de Madrid: “Su tutor nos dijo que tenemos que respetar la opinión de los demás”
    Evaluar competencias
    La Selectividad a los 50: ¿cirugía mayor o estiramiento facial?
    La libertad de elección de centro educativo y los cheques escolares en Madrid
    Selectividad: Desatar el nudo gordiano
    El nuevo sistema para evaluar los conocimientos digitales de los profesores valdrá en toda España
    Ofrecer comedor gratis en todos los colegios públicos es “alcanzable y urgente”: costaría 1.664 millones al año, según la ONG Educo  
    Una fórmula para que la escuela pública compita mejor con la concertada
    La pérdida de alumnos por el descenso de la natalidad está afectando con más fuerza a la escuela pública que a la concertada
    La disparidad de resultados entre autonomías en la EVAU se origina en la escuela, no en el examen 
    Las autonomías del PP critican la nueva Selectividad porque no prevé un examen único para todo el Estado
    La escalada vertiginosa de notas en Bachillerato: los sobresalientes de los que llegan a Selectividad se doblan en seis años
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    El techo de cristal del grado medio de FP: candidatos demasiado preparados se quedan con los puestos
    César Rendueles: “Hay universidades privadas que son como academias de conducir con pretensiones”
    La fuga de miles de médicos agrava el déficit de especialistas en España
    Jóvenes tutelados en la Universidad: “Tu pasado no tiene por qué condicionar tu futuro”
    Si tu familia está desahogada estudiarás Medicina y dobles grados, si no, Óptica o Educación 
    La historia de una niña que soñó con ser pianista
    Pon nombre a lo que te pasa para sentirte mejor
    Volver a empezar
    

### Clima y medio ambiente


```python
req8 = requests.get("https://elpais.com/clima-y-medio-ambiente/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup8 = BeautifulSoup(req8.text, 'html.parser')

tags = soup8.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Un plan de choque de 356 millones para intentar salvar Doñana de su creciente declive 
    La deforestación de la Amazonia cae un 11% en el último balance anual de la era Bolsonaro
    Portugal, el secreto de un país sin bicicletas que se convirtió en el mayor fabricante europeo
    Bruselas quiere que todos los embalajes de la UE sean reciclables para 2030
    La misteriosa llegada del pájaro parecido a un pingüino que preocupa en las costas mediterráneas
    Alex Rafalowicz, abogado: “Los combustibles fósiles son una amenaza existencial como las armas nucleares”
    El problema con los suelos: un mundo vivo, desconocido y muy desprotegido
    Los agujeros legales de las finanzas sostenibles: así acaba el dinero de los fondos de inversión más verdes en empresas contaminantes
    Gobierno y Junta chocan por Doñana mientras se agrava el deterioro ecológico 
    Linces y águilas imperiales se refugian en fincas privadas que se alían con conservacionistas  
    ¿Podré matar a una rata que entre en mi casa? Claves de la reforma del Código Penal para castigar más el maltrato animal
    El cambio climático perjudica su salud
    Por qué comer animales puede ayudar a luchar contra el cambio climático
    Por qué hay que dejar de comer animales para luchar contra el cambio climático
    Bombas de carbono 
    Crisis de los insectos: esto no es un armagedón sino una debacle provocada por los humanos
    El quebrantahuesos reconquista los cielos 
    Un año de crisis climática sin fin
    Ríos imposibles: las 171.000 barreras que rompen el curso de agua en España
    La historia de una niña que soñó con ser pianista
    Pon nombre a lo que te pasa para sentirte mejor
    Volver a empezar
    

### Ciencia


```python
req9 = requests.get("https://elpais.com/ciencia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup9 = BeautifulSoup(req9.text, 'html.parser')

tags = soup9.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    75 años de la muerte de G.H. Hardy, un matemático excéntrico y brillante
    Elon Musk asegura que en seis meses se implantará el primer chip en un cerebro humano con Neuralink
    El desafío de envejecer con VIH: “Las personas de largo recorrido sufrimos depresión, ansiedad y deterioro cognitivo”
    Un meteorito provoca un fuerte estruendo sentido en toda Gran Canaria
    Hallan en Transilvania una nueva especie de dinosaurio enano herbívoro que vivió hace 70 millones de años
    La primera simulación cuántica de un agujero de gusano abre una nueva puerta para entender el universo
    Un fármaco experimental contra el alzhéimer confirma efectos positivos, pero puede estar detrás de la muerte de dos pacientes 
    Escrito en las estrellas, ¿qué hemos aprendido de ellas?
    El problema con los suelos: un mundo vivo, desconocido y muy desprotegido
    Los hogares más pobres reducen su consumo de refrescos casi 11 litros en un año por la subida del IVA
    Ronna, ronto, quetta y quecto, los nuevos prefijos para magnitudes extraordinarias
    Por qué unas personas resisten el estrés mejor que otras 
    Joseph Henrich, antropólogo evolutivo: “El mejor antídoto contra el supremacismo blanco es más ciencia y discutir ideas”
    “Houston, tenemos un nuevo récord”: ‘Orion’ llega más lejos que ninguna otra nave diseñada para llevar astronautas
    En busca de una solución para los dolores que se creían inventados
    Un parásito ‘elige’ qué lobo será el líder de la manada
    Escrito en las estrellas, ¿qué hemos aprendido de ellas?
    75 años de la muerte de G.H. Hardy, un matemático excéntrico y brillante
    Hilda Hudson, la primera conferenciante en el gran congreso internacional de matemáticas
    Por qué el entrelazamiento cuántico revoluciona nuestro entendimiento de la naturaleza
    La órbita del telescopio ‘James Webb’ y el problema de los tres cuerpos
    Sangaku
    El tamiz de Apolonio
    La respuesta a la gran pregunta
    El aroma de la inspiración y la piedra de la locura
    ‘Los hijos de Hansen’ y la marginación social provocada por la lepra
    Los fractales y su estructura narrativa como parte del relato
    El amanecer de todo y el dinosaurio como animal modernista
    Los universos paralelos de un visionario científico llamado Philip K. Dick
    ¿Por qué son rocosos los satélites de los planetas gaseosos?
    ¿Es nueva la producción de alimentos en macrogranjas? 
    ¿Cómo se ve el cielo nocturno desde el ecuador?
    ¿Por qué las olas van siempre hacia la playa?
    Listeria: el patógeno que trae de cabeza a la industria alimentaria
    Ciencia para derrumbar el mito de que la soja es mala para prevenir el cáncer de mama
    Cuidado con las conservas caseras: es importante hacerlas bien
    Una propuesta alternativa, barata y saludable a la nueva cesta de la compra
    Aditivos, propiedades saludables y fechas de caducidad: guía para entender las etiquetas alimentarias
    

### Cultura


```python
req10 = requests.get("https://elpais.com/cultura/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup10 = BeautifulSoup(req10.text, 'html.parser')

tags = soup10.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    ‘As bestas’, de Rodrigo Sorogoyen, lidera la carrera a los Premios Goya 2023 con 17 nominaciones
    Todas las nominaciones a los Premios Goya 2023
    Muere Christine McVie, cantante y teclista de la legendaria banda Fleetwood Mac, a los 79 años
    ¿Cómo empezó?
    ‘Company’ y el olor de la gran manzana
    Charlie Watts: el bicho más raro de The Rolling Stones
    Meter la mano en la vaca 
    La respuesta a la guerra en Ucrania también es literaria
    Juana Dolores, la nueva ‘enfant terrible’ de la cultura catalana: “Hay mucho silencio y autocensura en la literatura”
    Una investigación saca a la luz 170 escritos inéditos de Miguel Hernández
    El Sónar 2023 anuncia a Richie Hawtin, Laurent Garnier o The Blessed Madonna entre sus primeros artistas invitados
    Nace el Centro Nacional de la Fotografía: lo tenemos más fácil por ser los últimos
    El arte reivindica la belleza y la fragilidad del vidrio
    Daniel López Valle: “Nos da miedo pensar en el poder que tiene el azar en nuestras vidas”
    El toque manual de campana español, declarado Patrimonio Cultural Inmaterial por la Unesco
    Lo más escuchado en Spotify en 2022: solo Rosalía se coloca en España en una lista dominada por hombres latinos
    ¿Quedan cines de barrio? ¿Toda España se hizo artista en el confinamiento? ¿Importan los premios? Los números responden
    ¿Se imaginan a la Generalitat criticando el día de Sant Jordi?
    Almodóvar, en la lectura de la obra de Paco Bezerra: “Nunca imaginé que iba a asistir hoy a un acto contra la censura”
    Un tatuaje y un bebé en el nombre de Mircea Cărtărescu
    Santo Estevo, el monasterio al que todos le tienen fe
    La Calahorra de siempre, más viva que nunca
    La novela negra del siglo XXI no existe (sin Michael Connelly)
    Disfruta en familia de 'El pequeño Mozart'
    El MET Opera en Cine Yelmo a través de +Que Cine
    Descubre la exposición 'Hijas del Nilo'
    'Un animal en mi almohada' en el Teatro Fernán Gómez
    La temida voltereta de la abolición de los toros en el sur de Francia quedó en un susto
    Las obras de mejora de la plaza de toros de Las Ventas comienzan en diciembre
    Actos a favor y en contra de los toros en Francia antes de que se debata su prohibición
    Luis Miguel Leiro, picador premiado y desencantado: “Amo y respeto a los animales, pero el toro ha nacido para la lidia”
    

### Babelia


```python
req11 = requests.get("https://elpais.com/babelia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup11 = BeautifulSoup(req11.text, 'html.parser')

tags = soup11.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Roe Ethridge, el fructífero intercambio entre el arte y el comercio
    Lo nuevo de Rihanna, Bruce Springsteen, Niño de Elche (con Rosalía) y otras canciones de noviembre
    ‘La última vez’, de Guillermo Martínez: un laberinto con final milagrosamente imprevisible
    La lección magistral de Bob Dylan sobre Elvis
    Cuando la furia de Twitter empaña un (interesante) debate narrativo
    La curva de la semana: sube Cristina Morales, está aquí Aldo Manucio, baja Rosalía
    Las nuevas coordenadas culturales de Latinoamérica
    Las más bellas cartas de amor en castellano, las memorias de Marguerite Duras y otros libros de la semana
    Amor mío queridísimo: la delicadeza sentimental de Felisberto Hernández
    Ellas fueron modernas: cuatro artistas alemanas en la vorágine del cambio de siglo
    Anacrónicas y audaces: las cantautoras latinas que renuevan la música de raíz
    Lo que jode es la respuesta: la diferencia entre crítica, cancelación y censura
    Edmonia, Frida y Amrita: tres mestizas
    La basura se lee con anteojos
    Mi otoño alemán
    ‘Percusión’: una novela del pasado para recordar el futuro
    Pere Gimferrer dentro del laberinto
    ‘La brecha’: cómo cambiar un mundo mal hecho
    ‘Tu sueño imperios han sido’: la historia boca arriba
    Nona Fernández: “En Chile intentan que conciliemos el sueño otra vez”
    Cristina Lucas: “Todo lo que se publicita está sobrevalorado”
    Enrique Gracián: “Hay infinitos más grandes que otros”
    Àlex Brendemühl: “La serie sobre el rey emérito no te deja indiferente”
    Marta Etura: “De no ser actriz, habría sido matrona”
    

### Deportes


```python
req12 = requests.get("https://elpais.com/deportes/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup12 = BeautifulSoup(req12.text, 'html.parser')

tags = soup12.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Última hora
    El calendario
    Vídeo en directo
    Las predicciones
    La ‘newsletter’
    Argentina se gana los octavos 
    “Si Lewandowski fuera argentino, igual mete cinco”
    México se queda a un gol del pase 
    Sí, se puede ser feliz por una clasificación a octavos de final
    Mi tío Ricardo y la antena de la tele
    Jugar para tu país
    El mejor Messi juega, no golea 
    España se ve lanzada  
    Morata encuentra su paz
    Japón y el dios del pie buscan al mejor Kamada
    Joshua Kimmich bajo vigilancia
    Kevin de Bruyne, entre la frustración y el miedo ante el día decisivo de Bélgica contra Croacia
    Marruecos, ante su mayor desafío histórico desde el 86
    Olga Viza: “Llevé la copa del Mundial de España 82 de copiloto en mi coche con la L en el cristal”
    Tata Martino lleva a México a su gran fracaso en el Mundial
    ¡Viva mi desgracia!
    Túnez desnuda a los suplentes de Francia
    Una indesmayable Australia acaba con la insustancial Dinamarca y se mete en octavos
    Resumen de la jornada 11 del Mundial de Qatar 2022
    Pelé se mantiene estable tras ser hospitalizado de manera inesperada en São Paulo
    Última hora del Mundial de Qatar: vídeo en directo
    Catarí que te vi: Cómo llenar el depósito de gasolina por 22 euros en Qatar
    Última hora del Mundial de Qatar | Día 11
    La moneda que cambió para siempre el destino de España en los Mundiales
    Cómo no perderte ni un solo minuto del Mundial
    Las promesas del baloncesto español piden consejo a Sergio Scariolo
    A toda mecha hacia el mundial de la consagración
    Cómo disfrutar de la montaña con todas las garantías
    El mejor Messi juega, no golea 
    Los vídeos de los goles y el resumen de la jornada 11 del Mundial de Qatar 2022
    Argentina se gana los octavos 
    La jornada 11 del Mundial de Qatar en imágenes
    Los 97 goles del Mundial de Qatar 2022 hasta el momento
    ¿Qué opciones tiene cada selección de pasar a octavos de final del Mundial?
    Última hora del Mundial de Qatar | Día 11
    Así hemos contado la victoria de Túnez ante Francia en el Mundial de Qatar 2022
    

### Tecnología


```python
req13 = requests.get("https://elpais.com/tecnologia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup13 = BeautifulSoup(req13.text, 'html.parser')

tags = soup13.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Elon Musk asegura que en seis meses se implantará el primer chip en un cerebro humano con Neuralink
    Del referéndum de Cataluña a #Cuéntalo: los archiveros guardan tuits que han hecho historia
    La primera simulación cuántica de un agujero de gusano abre una nueva puerta para entender el universo
    La Policía de San Francisco contará con robots con capacidad de matar
    Ronna, ronto, quetta y quecto, los nuevos prefijos para magnitudes extraordinarias
    El problema de la cultura ‘brogrammer’: “Se está excluyendo la mirada femenina de las soluciones tecnológicas que van a modelar el futuro”
    Los ciberdelincuentes aprovechan el caos en Twitter para lanzar campañas de ‘phishing’
    Damian Burns, director de Twitch Europa: “No me importaría que mi hija fuera ‘streamer’”
    Adrian Hon, diseñador de videojuegos: “Las empresas y gobiernos usan juegos para controlarnos”
    Mastodon: qué es y cómo funciona la red social en la que los usuarios deciden qué está permitido
    Así serán las nuevas marcas de verificación en Twitter: azul, oro y gris
    Gafas con funciones de un móvil, ‘Photoshop’ instantáneo y otros inminentes avances gracias a los nuevos chips
    Elon Musk ya edita tuits y Twitter no se ha hundido aún, ¿qué hará en el futuro?
    Elon Musk declara una “amnistía general” en Twitter para las cuentas suspendidas
    Así está fallando Twitter: racismo, derechos de autor y desprotección en dictaduras
    La banca confía en tumbar en los tribunales el nuevo impuesto al sector
    Los cuatro coches que llegaron a España en el año de los Juegos y la Expo
    Ocho mil millones de cursis
    Guía de viaje a la nube: una aventura con escalas
    Árboles tuiteros contra la ceguera botánica
    De Baudelaire a Midjourney: los nuevos “enemigos mortales del arte”
    


```python
req14 = requests.get("https://elpais.com/tecnologia/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup14 = BeautifulSoup(req14.text, 'html.parser')

tags = soup14.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Elon Musk asegura que en seis meses se implantará el primer chip en un cerebro humano con Neuralink
    Del referéndum de Cataluña a #Cuéntalo: los archiveros guardan tuits que han hecho historia
    La primera simulación cuántica de un agujero de gusano abre una nueva puerta para entender el universo
    La Policía de San Francisco contará con robots con capacidad de matar
    Ronna, ronto, quetta y quecto, los nuevos prefijos para magnitudes extraordinarias
    El problema de la cultura ‘brogrammer’: “Se está excluyendo la mirada femenina de las soluciones tecnológicas que van a modelar el futuro”
    Los ciberdelincuentes aprovechan el caos en Twitter para lanzar campañas de ‘phishing’
    Damian Burns, director de Twitch Europa: “No me importaría que mi hija fuera ‘streamer’”
    Adrian Hon, diseñador de videojuegos: “Las empresas y gobiernos usan juegos para controlarnos”
    Mastodon: qué es y cómo funciona la red social en la que los usuarios deciden qué está permitido
    Así serán las nuevas marcas de verificación en Twitter: azul, oro y gris
    Gafas con funciones de un móvil, ‘Photoshop’ instantáneo y otros inminentes avances gracias a los nuevos chips
    Elon Musk ya edita tuits y Twitter no se ha hundido aún, ¿qué hará en el futuro?
    Elon Musk declara una “amnistía general” en Twitter para las cuentas suspendidas
    Así está fallando Twitter: racismo, derechos de autor y desprotección en dictaduras
    La banca confía en tumbar en los tribunales el nuevo impuesto al sector
    Los cuatro coches que llegaron a España en el año de los Juegos y la Expo
    Ocho mil millones de cursis
    Guía de viaje a la nube: una aventura con escalas
    Árboles tuiteros contra la ceguera botánica
    De Baudelaire a Midjourney: los nuevos “enemigos mortales del arte”
    

### Gente


```python
req15 = requests.get("https://elpais.com/gente/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup15 = BeautifulSoup(req15.text, 'html.parser')

tags = soup15.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Shakira y Piqué sellan su acuerdo de separación en Barcelona ante el juez
    Spotify Wrapped, el selfi musical que monopoliza la conversación en Twitter y acaricia el ego
    Los príncipes de Gales emulan en su viaje a Boston la visita que la reina Isabel II hizo a la ciudad en 1976
    Buckingham fuerza la dimisión de una asistente de la reina Camila por sus comentarios racistas
    Los actores de ‘Love Actually’ se reencuentran: ¿qué ha sido de ellos 19 años después?
    El último desfile de Antonio Alvarado se expone en el Museo del Traje
    Antonio Alvarado, el museo como pasarela: su restrospectiva, en fotos
    Tres reinas, una princesa y dos primeras damas se reúnen en Buckingham contra la violencia de género
    Acuerdo de divorcio entre Kim Kardashian y Kanye West: custodia compartida y 200.000 dólares de pensión
    La ‘baguette’ francesa, declarada patrimonio inmaterial de la Unesco
    Los chocolates y bombones de Jordi Roca ponen un pie en Barcelona con una tienda efímera de Casa Cacao en un hotel de lujo
    ¿Se puede ahorrar energía colocando alfombras, cortinas o mantas en el sofá? Los expertos responden
    Xuso Jones: “Tengo muchos más seguidores por mis ‘tips’ de limpieza que por mi música. Y me encanta”
    Una selección imprescindible de productos con descuento: comprar en Black Friday nunca fue tan fácil
    Achilles Ion Gabriel, el surrealista de Camper: “No hago zapatos para museos, sino para la gente” 
    El regreso discreto de Mario Testino: “A mi edad, no creo que mi percepción de la moda sea la correcta ni la que el mundo necesita”
    Manuel Outumuro toca cumbre
    Diane de Beauvau-Craon, la última princesa rebelde: “Me drogué mucho, bebí mucho alcohol, me acosté con muchos gais y aquí sigo”
    En los secaderos ancestrales del pimentón de la Vera, el oro rojo de Cáceres
    Las abuelas que han viralizado el arte de elaborar la pasta italiana 
    Humaredas mediáticas, monotonía, discursos vacíos y otras amenazas y retos de la gastronomía 
    Sumer, el ‘kebab’ artesano de barrio en Madrid que acoge tertulias filosóficas
    El robot de cocina más famoso del mundo ha conquistado ya tres millones de hogares españoles
    

### Televisión


```python
req16 = requests.get("https://elpais.com/television/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup16 = BeautifulSoup(req16.text, 'html.parser')

tags = soup16.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    La SER se consolida como la radio más escuchada con 4.161.000 oyentes
    Series de diciembre de 2022: ‘Alice in Borderland’ en Netflix, ‘Fácil’ en Movistar Plus+ y otros estrenos
    Lorena Castell, ganadora de ‘MasterChef Celebrity’: “Me gusta trabajar bajo presión, me pone las pilas”
    Omar Montes y el experimento del gorila
    ‘El presidente: juego de la corrupción’, los entresijos del fútbol
    ‘No me gusta conducir’: en qué se parece hacer una serie a aprender a conducir
    ‘Ummo’, un guirigay intergaláctico
    Borja Cobeaga: “Tardé más en sacarme el carné que en hacer esta serie”
    Lorena Castell, ganadora de ‘MasterChef Celebrity 7’
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    Eliseo, ‘el encargado’ corrupto que seduce y repele en Argentina 
    ‘Masterchef Celebrity’ ya tiene a sus dos finalistas, tras la “rendición” de Patricia Conde
    ‘The Peripheral’, realidad, ficción y un futuro ciberpunk con los creadores de ‘Westworld’
    El ‘bon vivant’ acorralado de la FIFA que grabó a sus amigos
    Leonor Lavado: “Somos como hablamos: la voz es nuestro ADN psicológico”
    ¿Qué ocurre tras la edad de oro de la televisión? El mismo oro, aunque enterrado bajo una oferta masiva
    ‘La Sagrada Familia’ rescata el mito Pujol y disecciona su caída
    ¿Qué ver hoy en TV? Jueves 1 de diciembre de 2022
    Las series de agosto de 2022: ‘La casa del dragón’ en HBO Max; ‘Sandman’ en Netflix y otras
    Nueve capítulos para recordar ‘The Wire’ en su 20º aniversario
    Harry Palmer: el tercer vértice del mágico triángulo de espías británicos
    Las series de junio de 2022: ‘The Boys’ en Amazon Prime Video; ‘Peaky Blinders’ en Netflix y otras
    

### Eps


```python
req17 = requests.get("https://elpais.com/eps/")
# Si el estatus code no es 200 no se puede leer la página
if (req.status_code != 200):
 raise Exception("No se puede hacer Web Scraping en"+ URL)
soup17 = BeautifulSoup(req17.text, 'html.parser')

tags = soup17.findAll("h2")
for h2 in tags:
    print(h2.text)
    resultados.append(h2.text)
```

    Felix Klieser: un virtuoso de la trompa (sin brazos)
    Anna Lluch, experta en cáncer de mama: “El sistema público de salud se decide en las urnas”
    ¿A qué sabe un vino de 160 años? Apuntes de una cata histórica en Marqués de Riscal
    Las abuelas que han viralizado el arte de elaborar la pasta italiana 
    David LaChapelle, en busca de Dios
    El lugar en el que convergen moda, arte y arquitectura
    Muchos hombres, una sola mujer
    El misterio de Manuel Carrasco: cómo salir de una barriada de pescadores y acabar siendo un cantante que llena estadios
    Ishida, los ‘dioses’ de la cocina japonesa: “Tenemos que dejar de desear tantas cosas, y hay que hacerlo ya”  
    Los guardianes de la ensaladilla rusa, la tapa popular que subió a los altares ‘gourmet’ 
    Humaredas mediáticas, monotonía, discursos vacíos y otras amenazas y retos de la gastronomía 
    Narcisistas, ansiosos, pasivo-agresivos… Cinco claves para tratar con personas difíciles
    Al fondo, invisibles, las pirámides
    El coche que se anticipa al declive de los SUV
    El milagro alemán
    Consuelo
    Sin tiempo
    La bióloga que se propuso repoblar los bosques de Brasil
    Un parche para conseguir que las vacunas sean más baratas y accesibles
    Cerdo pío negro, el inesperado rival del ibérico
    Ishida, los ‘dioses’ de la cocina japonesa: “Tenemos que dejar de desear tantas cosas, y hay que hacerlo ya”  
    El secreto del maíz gigante mexicano que bajó del volcán
    ‘Mis primeros recuerdos’, por Daniel Barenboim
    El indómito espíritu creativo de Picasso
    Medio siglo sin Picasso
    Paloma Picasso se confiesa con Nuccio Ordine
    El amigo de Picasso sin el que no estaría en España el ‘Guernica’
    Tommy Hilfiger: “Muchos de nuestros clientes van a vivir en el metaverso. De hecho, ya lo hacen”
    Storm Pablo: el estilista que convirtió a Bad Bunny en icono también de la moda
    El hombre que cultiva las flores más caras para los perfumes más especiales
    Una casa junto al lago Como que es pura diversión 
    Desayuno a la mexicana entre hípsters de mañaneo y polis con más apetito que buena fama
    El misterio Picasso
    Isabel II: el reinado de la imagen
    Un día en la vida de un país: San Sebastián-Cádiz en 16 horas
    Luces y sombras de Robert Mapplethorpe
    

### Estilo de El País
Nada más acabar con el trabajo de impresión, será necesario limpiar los resultados para obtener una visualización optima tras haber realizado el web scrapping. Para ello, se utilizará la siguiente función.


```python
os.system("clear")
```




    1



El uso del siguiente atributo nos ayudará a dar una distinción de color a cada uno de los titulares que contengan la palabra "Feminismo". En este caso, pasarán a ser verdes y tendrán estilo de negrita.


```python
print(colored("A continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:", 'blue', attrs=['bold']))
print(colored("Feminismo", 'green', attrs=['bold']))
```

    A continuación se muestran los titulares de las páginas principales del diario El País que contienen las siguientes palabras:
    Feminismo
    

Gracias a la siguiente función, podremos asegurarnos gracias al condicional "if" que todos los resultados que concuerden con esa palabra repintan esta acción. Esto se hace a través de la variable "str_match".


```python
str_match = [s for s in resultados if "feminismo" in s]
print("\n".join(str_match))
```

    
    

Este mismo proceso se repetirá con las siguientes palabras: igualdad, mujeres, mujer, brecha salarial, machismo, violencia, maltrato, homicidio, género, asesinato y sexo. 


```python
print(colored("Igualdad", 'green', attrs=['bold']))
str_match = [s for s in resultados if "igualdad" in s]
print("\n".join(str_match))
```

    Igualdad
    La economía solidaria: un nuevo modelo financiero contra la desigualdad y la emergencia climática
    El caso de Georgia, en EE UU: becar sin importar la renta agranda la desigualdad
    


```python
print(colored("Mujeres", 'green', attrs=['bold']))
str_match = [s for s in resultados if "mujeres" in s]
print("\n".join(str_match))
```

    Mujeres
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    


```python
print(colored("Mujer", 'green', attrs=['bold']))
str_match = [s for s in resultados if "mujer" in s]
print("\n".join(str_match))
```

    Mujer
    Muchos hombres, una sola mujer
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    Muchos hombres, una sola mujer
    


```python
print(colored("Brecha salarial", 'green', attrs=['bold']))
str_match = [s for s in resultados if "brecha salarial" in s]
print("\n".join(str_match))
```

    Brecha salarial
    
    


```python
print(colored("Machismo", 'green', attrs=['bold']))
str_match = [s for s in resultados if "machismo" in s]
print("\n".join(str_match))
```

    Machismo
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    Radiografía de ‘El hormiguero’: entretenimiento blanco de éxito… y polémicas por machismo
    


```python
print(colored("Violencia", 'green', attrs=['bold']))
str_match = [s for s in resultados if "violencia" in s]
print("\n".join(str_match))
```

    Violencia
    Otra forma de violencia política
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    Tres reinas, una princesa y dos primeras damas se reúnen en Buckingham contra la violencia de género
    


```python
print(colored("Maltrato", 'green', attrs=['bold']))
str_match = [s for s in resultados if "maltrato" in s]
print("\n".join(str_match))
```

    Maltrato
    ¿Podré matar a una rata que entre en mi casa? Claves de la reforma del Código Penal para castigar más el maltrato animal
    


```python
print(colored("Homicidio", 'green', attrs=['bold']))
str_match = [s for s in resultados if "homicidio" in s]
print("\n".join(str_match))
```

    Homicidio
    
    


```python
print(colored("Género", 'green', attrs=['bold']))
str_match = [s for s in resultados if "género" in s]
print("\n".join(str_match))
```

    Género
    Ayuso se compromete con Vox a borrar la autodeterminación de género de las leyes en Madrid
    PSOE y Unidas Podemos aplazan el debate sobre la autodeterminación de género en la ‘ley trans’
    Por primera vez un juez declara nulo un contrato de alquiler por aplicación de la perspectiva de género
    Visitas a centros de acogida y muchas horas de estudio: así se forman los jueces en materia de género
    Para acabar con la violencia de género, necesitamos más mujeres en posiciones de poder 
    PSOE y Unidas Podemos aplazan el debate sobre la autodeterminación de género en la ‘ley trans’
    Tres reinas, una princesa y dos primeras damas se reúnen en Buckingham contra la violencia de género
    


```python
print(colored("Asesinato", 'green', attrs=['bold']))
str_match = [s for s in resultados if "asesinato" in s]
print("\n".join(str_match))
```

    Asesinato
    
    


```python
print(colored("Sexo", 'green', attrs=['bold']))
str_match = [s for s in resultados if "sexo" in s]
print("\n".join(str_match))
```

    Sexo
    
    
