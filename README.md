# De los Números a la Vida: Análisis Estadístico de Señales Biomédicas
## Descripcion:
Este proyecto abarca el codigo necesario para hacer un analisis determinado de señales fisiologicas, como lo es en este caso una electromiografia (EMG) obtenida mediante la base de datos(Physionet),empleando tecnicas de analisis estadistico simple por medio de Python. Contiene  el desarrollo de calculos estadisticos descrptivos, ademas el estudio de la relacion señal-ruido(SNR) con diferentes tipos de ruido junto a su visualizacion y explicacion, gracias a todo ello se logra comprender mejor ciertas caracteristicas particulares de la EMG como señal biomedica. 
## Descripcion de la señal:
En primera medida se descargo una señal fisiologica de la base de datos Physionet, ya que esta proporciona acceso a señales fisiológicas, como ECG, EEG y EMG, para investigación y desarrollo en el área biomédica. Ofrece herramientas y recursos para el análisis de datos médicos, teniendo esto en cuenta se logro descargar una señal titulada "Electromiograma de reconocimiento de gestos y biometría (GRABMyo)" este es un conjunto de registros de electromiograma (EMG), reunidos de los músculos de la muñeca y el antebrazo mientras los participantes realizaban 16 gestos con las manos. Su objetivo principal es proporcionar datos para la investigación en biometría basada en EMG (identificación y verificación personal) y en reconocimiento de gestos para aplicaciones de neurorrehabilitación y control de dispositivos. Se compone de registros obtenidos de 43 participantes durante tres días, lo que permite analizar la consistencia de las señales EMG a lo largo del tiempo y su resistencia frente a variaciones fisiológicas y ambientales, tales como el sudor, la colocacion de los electrodos o las diferentes actividades de los partcipantes, es por esto que después de la preparación, el participante se sienta cómodamente en la silla con ambas extremidades superiores en posición de descanso y se dio un periodo de descanso para no producir fatiga muscular. 
Un punto a destacar es que GRABMyo es uno de los conjuntos de datos más grandes y se distingue por incluir múltiples sesiones de recolección, lo que permite evaluar la consistencia de las señales EMG a lo largo del tiempo.
Por otro lado, para la obtencion de la señal ellos comentan que hicieron uso de 28 electrodos monopolares sEMG colocados en el antebrazo y la muñeca de los participantes. Los electrodos fueron dispuestos en cuatro anillos: dos en el antebrazo (8 pares bipolares) y dos en la muñeca (6 pares bipolares). Se registraron los datos mientras los participantes realizaban 16 gestos con las manos siguiendo instrucciones visuales en una pantalla, ademas de esto el gesto del reposo. Cada gesto se repitió siete veces(17 gestos x 7 ensayos = 119 contracciones), con cinco segundos de registro por ensayo y un período de descanso de diez segundos. Las señales fueron adquiridas a una frecuencia de muestreo de 2048 Hz mediante un amplificador de bioseñales.

En nuestro caso particular, para obtener la señal descargamos los archivos .dat y .hea del participante 1, correspondientes al gesto número 10 en la prueba 3. Luego, utilizamos Python y la biblioteca wfdb (WaveForm DataBase) para leer y procesar los datos EMG almacenados en estos archivos. La biblioteca wfdb permite cargar la señal, extraer información relevante como la frecuencia de muestreo y los canales registrados, y visualizarla en una interfaz gráfica. Posteriormente,se muestra la señal EMG en una interfaz gráfica utilizando bibliotecas como Matplotlib haciendo que sea facil la interpretacion y posterior analisis. 

![image](https://github.com/user-attachments/assets/c795d03e-88ee-4591-a7a2-9c2b60aa57e8)
*Señal EMG obtenida del paciente 1.* 

Se observa una señal oscilatoria con variaciones en la amplitud, lo que indica la actividad eléctrica de los músculos durante el tiempo registrado. Además, se evidencian picos pronunciados y cambios bruscos, que  representan activaciones musculares. Esta es una característica típica de una señal EMG utilizada para evaluar la actividad muscular durante un gesto o movimiento específico.
Para un análisis más preciso y detallado de la señal, es importante calcular distintos estadísticos que permitan cuantificar sus características de manera más clara, es por esto que calcula: Media de la señal, desviación estándar y coeficiente de variación de dos maneras diferentes, la primera de forma manual o haciendo uso de las formulas ya definidas matematicamente y la segunda usando las funciones definidas directamente de Python y asi se verifica que ambas emiten los mismos resultados, evidenciando la eficacia de los calculos.
Ademas de dichos calculos, se genero un histograma que representa la distribucion de los valores de nuestra señal EMG, facilitando la vision de la frecuencia a diferentes amplitudes de nuestra señal descargada, asi mismo se calculo la funcion de probabilidad, la cual es importante para estudiar que tanto varia la señal y como es la distribucion de forma estadistica de los datos para que asi se vea reflejado un patron en la actividad muscular del paciente 1. 
De acuerdo a todo lo mencionado con anterioridad, se hace una descripcion del codigo realizado en Python y compilado con Google colab para mayor entendimiento practico. 
## Instrucciones y estructura del codigo:
![image](https://github.com/user-attachments/assets/d088a027-7824-4f5a-aa04-b42df873182f)





*Importacion de librerias.*








Estas son las librerias necesarias para que se ejecute el codigo de manera correcta, wfdb sirve para leer los archivos de la señal, numpy para los calculos matematicos, matplotlib para graficar y scipy.stats para estimar la funcion de probabilidad. 
![image](https://github.com/user-attachments/assets/eab4b0d5-86e9-42db-9396-f6f11cc8ea9f)




*Carga de datos.*






En primera medida, teniendo ya los archivos descargados en el formato mencionado debes ingresar el nombre exactamente como esta sin extenciones para asi poderlo leer de la forma correcta, luego de eso se debe hacer la lectura de los datos de la señal registrada para que se pueda ver en la interfaz grafica, por otro lado, se debe seleccionar el canal que deseas analizar puesto que este tipo de señaes viene con una lectra de diversos canales(electrodos), este codigo te permite elegir que canal estudiar posteriormente. 

![image](https://github.com/user-attachments/assets/b9893632-6cfd-4a54-94ea-c9a051bbac31)



*Estadisticos descriptivos: manualmente y con funciones predefinidas.*








Se evidencian las formulas matematicas empleadas para hacer los estadisticos descriptivos de forma manual, donde la media se obtiene de sumar todos los valores de la señal y dividiendo entre la cantidad total de muestras, la varianza sumando el cuadrado de la diferencia entre cada valor y la media, y dividiendo por la cantidad de muestras, la desviacion estandar haciendo la raiz cuadrada de la varianza y el coeficiente de variacion dividiendo la desviacion estandar sobre la media. por otro lado, para el calculo con las funciones predefinidas se usa numpy.mean para la media, numpy.std para la desviacion estandar y el coeficiente de variacion se obtiene al dividir dichos valores.Todos estos resultados se muestran en la consola arrojando lo sieguiente. 
![image](https://github.com/user-attachments/assets/87271da6-1d82-4e2a-a14b-1a9e8ee67bc2)



*Resultados en consola.*




Luego de esto, Se utiliza el método de estimación de densidad por núcleo (KDE, Kernel Density Estimation) para obtener una representación suave de la distribución de la señal, se define un objeto KDE con gaussian_kde(señal), donde gaussian_kde de scipy.stats estima la densidad de la señal, asi mismo, se genera un conjunto de valores x_vals distribuidos uniformemente entre el mínimo y máximo de la señal utilizando np.linspace, finalmnete, se evalúa la función de densidad en estos puntos usando kde(x_vals), obteniendo pdf_vals, que representa la densidad estimada, asi como se muestra en la imagen.
![image](https://github.com/user-attachments/assets/c3d67944-5abc-40ed-b4c6-3703c2d543c3)


*Estimacion funcion de probabilidad usando KDE.*








Gracias a ello se obtiene el siguiente resultado:
![image](https://github.com/user-attachments/assets/f9865f43-2e7d-4b22-8a44-de0f841e7220)


*Histograma y Funcion de Probabilidad.* 








Como se evidencia en el grafico, el histograma (color rosado) representa la frecuencia con la que se muestran ciertos valores de voltaje en la señal, obteniendo que los valores estan centrados alrededor de los 0 mV o valores muy cercanos, demostrando una forma aproximadamente simetrica, de ese mismo modo, la funcion de probabilidad(linea morada) muestra que se lleva una forma de distribucion muy similar a la distribucion normal o gaussiana, se diece que es muy parecida puesto que se ve que no es completamnete simetrica para ser normal y que ademas en la partes inferiores al lado derecho esta tomando mas valores antes de llegar al 0, pero en este caso se puede tomar como gaussiana. 

Gracias a lo anterior es valido continuar con el analisis de la señal, ahora se da un enfoque en la evaluacion de la relacion señal ruido (SNR), para esto la señal es contaminada con tres tipos de ruido diferentes cada uno aplicado en dos niveles de amplitud diferentes, lo anterior permite ver como o que tanto afecta cada ruido a la calidad de la señal.

## SNR (Relación Señal Ruido)

Es una medida de cuantificación para evaluar una señal deseada comparando el ruido presentado (interferencia no deseada que degrada la calidad de la información) , es decir medir cuanto de lo que se desea ver esta presente en relación con lo que no. Entre mas alto sea el valor de SNR indican una señal más clara y con menos ruido. 

En este caso para la señal requerida, en la señal EMG el SNR es un parámetro que determina la calidad de esta y su utilidad para un analisis adecuado biomecánico y clínico. Un SNR alto indica una señal clara con poca interferenciay un SNR bajo sugiere que el ruido afecta los datos señalados.

Para calcular el SNR debe compararse la intensidad de la señal con el ruido de fondo, la formula para hallar este valor que se presenta en (dB) es la siguiente:
![image](https://github.com/user-attachments/assets/46d4cdff-f816-4780-b637-de251b41f5a1)
 
 *Formula para calcular SNR (Relación Señal Ruido)*
 
Esta técnica de medición tiene una aplicación muy importante ya sea en el uso de señales de internet, de sonido y de igual manera identificar el ruido para tomar decisiones respecto a esa señal. Se clasifican en tres tipos de ruido:

#### Ruido Gaussiano:
sigue una distribución normal con una media y una desviación estandar, los valores cercanos se relacionan con la media y los extremos no son frecuentes.

#### Ruido de impulso: 
Son valores aletorios en su mayoria grandes y en algunas muestras de la señal, se simulan picos de ruido de gran amplitud. 

#### Ruido tipo artefacto:
Se debe a movimientos o interferencias electricas pueden ser de baja frecuencia en este caso una señal seno.

## Ruidos en la señal aplicada
Se agregan estos tres tipos de ruidos a la señal EMG con diferentes amplitudes cada uno, es decir por cada ruido una onda grande y una mas pequeña. 

### Primer ruido
En el primer caso se agrega el ruido gaussiano y con cada amplitud se obtienen valores de SNR:
![image](https://github.com/user-attachments/assets/3ef0a4f7-c747-4257-ae5a-d149658f392e)

*Ruido Gaussiano con Amplitud Grande y Pequeña*

SNR(Amplitud Grande de 8mV): 0.94dB que indica que la potencia del ruido y la señal EMG son similares por lo que no se logra distinguir la señal esto justifica el valor bajo de SNR

SNR(Amplitud Pequeña de 2mV): 6.94dB este valor indica que la potencia del ruido es menor por lo cual la señal se logra identificar pero con una pequeña distorsión

### Segundo ruido
En el segundo caso se hace uso de ruido de impulso de igual manera con una amplitud grande y otra mas pequeña y se calcula el SNR para analizar como actua respecto a la señal EMG, se obtiene lo siguiente:
![image](https://github.com/user-attachments/assets/3da5cb5a-958b-4607-975a-7992a6dda307)

*Ruido de Impulso Amplitud Grande y Pequeña*

SNR(Amplitud Grande de 2mV): 

SNR(Amplitud Pequeña de 0.3mV):


