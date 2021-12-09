# Tutorial-NGSPICE
Tutorial básico para aprender a usar NGSPICE
UNIVERSIDAD DE LAS FUERZAS ARMADAS ESPE

DEPARTAMENTO DE ELECTRICA Y ELECTRÓNICA
FUNDAMENTOS DE CIRCUITOS ELECTRICOS
               ![image](https://user-images.githubusercontent.com/95496629/144930417-976da442-2b34-4ba9-92e7-859596ccb269.png)


 


TEMA:
DISEÑO DE CIRCUITOS MIXTOS Y TOMA DE MEDICIONES EMPLEANDO NGSPICE

MARTÍN AUGUSTO CORONEL MOREIRA




TEMA: Tutorial básico para aprender a usar NGSPICE
1.	OBJETIVOS
1.1 Objetivo General
Entender el funcionamiento y descripción de un circuito electrónico mediante el uso de NGSPICE como un simulador de circuitos.

1.2 Objetivos Específicos
	Ser capaz de realizar la simulación digital de circuitos electrónicos analógicos, digitales y mixtos.
	Simular circuitos electrónicos analógicos compuestos por resistencias y fuentes de corrientes. 
	Describir los componentes, describir el circuito y luego elegir el tipo de simulación

2.	MARCO TEÓRICO

2.1 Qué es NGSPICE?

Ngspice (Next Generation Simulation Program with Integrated Circuits Emphasis ) es un programa para la simulación de circuitos electrónicos lineales y no lineales con propósito general.
Ngspice soporta una gran cantidad de elementos como resistencias, condensadores, bobinas, bobinas acopladas, fuentes de tensión y de corriente tanto independientes como independientes, líneas de transmisión con y sin pérdidas, interruptores controlados por tensión o por corriente, diodos, transistores BJT, JFETs, MESFETs y MOSFETs. 
El programa utiliza las mismas leyes de Kirchhoff que ya habrá estudiado en Teoria de Circuitos. Para cada punto de tiempo, ngspice tiene que crear una matriz y resolverla. Adicionalmente se usa el algoritmo de Newton-raphson para resolver ecuaciones no lineales que surgen de la descripción de los circuitos. (Zerberros, s.f.)

 ![image](https://user-images.githubusercontent.com/95496629/144930491-064b3d75-2451-4f1a-8fc8-9fad46dcc9d6.png)



2.2 Funcionamiento del programa

Resistencia:

 ![image](https://user-images.githubusercontent.com/95496629/144930524-ad8879da-88c7-40e5-be32-8304260ac77b.png)

El elemento debe empezar con R para que el programa pueda determinar que estamos hablando de una resistencia, después de eso se pone el nombre de la resistencia para poder diferenciarla de las otras, luego se pone el nodo en el que está junto con el otro nodo y finalmente el valor de la resistencia en ohmios. 

Fuente de voltaje:

 ![image](https://user-images.githubusercontent.com/95496629/144930538-7cf4d269-f197-4449-bb65-69216b79e833.png)

Las fuentes pueden haber de muchos tipos (corriente alterna, corriente directa, pulsos, escalones, etc), en esta introducción a ngspice solamente se entenderá el uso de corriente directa. Para poner una fuente de tensión es importante tener en cuenta cual es el nodo positivo y el negativo de la fuente y siempre se va a empezar con una V para saber que estamos hablando de voltaje y de igual manera luego va el nombre de la fuente, junto con el nombre del nodo positivo y del negativo, después se procede a poner el tipo de corriente que vamos a utilizar, como se dijo en este caso será una fuente de corriente directa (DC), y finalmente se deberá poner el valor de la fuente.

Fuente de corriente:

 ![image](https://user-images.githubusercontent.com/95496629/144930557-9d7c4312-fe27-42a1-8227-682584c0ce30.png)

Esta fuente se indica con la letra I acompañado del nombre de dicha corriente, se indica el nodo positivo y negativo, el tipo de corriente que deberá ser directa (DC) y al final el valor de la corriente. Con las fuentes de corriente hay que tomar en cuenta que la corriente pasa por el nodo positivo, luego entra a la fuente y sale por el nodo negativo.

Fuente de tensión controlada por corriente:

 ![image](https://user-images.githubusercontent.com/95496629/144930565-6d3c9985-4591-47ad-a81f-69b979437a8f.png)

En este tipo de fuente es importante entender en qué nodo esta conectado, que es una fuente dependiente, el valor de k y luego la corriente que la controla. Para poder medir el valor de una corriente en ngspice solamente se podrá hacer a través de fuentes de tensión de 0 voltios. La manera de describir esta fuente controlada es empezar con una H junto con el nombre que se desee poner, el nodo positivo y negativo, luego se coloca el nombre de la fuente por donde pasa la corriente que lo controla (ic) y al final se pone el valor de la ganancia.



Fuente de corriente controlada por tensión:

 ![image](https://user-images.githubusercontent.com/95496629/144930579-6ad32a58-aa55-4489-8be8-9013298d38d9.png)

En este caso la corriente va del nodo positivo al negativo, se inicia con la letra G con el nombre, la corriente Vc se encuentra entre el nodo de control positivo y el nodo de control negativo, para definir estos nodos en la fuente hay que decir a spice cual es cada nodo y nodo de control en los que vamos a medir esa tensión, finalmente se coloca el valor.

	2.3 Ejemplo del funcionamiento del programa
 ![image](https://user-images.githubusercontent.com/95496629/144930603-f7fed94f-b9dd-4fac-9ad1-58f877065a56.png)
![image](https://user-images.githubusercontent.com/95496629/144930627-5c471e31-03c8-4643-9289-fc6fdb055dcb.png)


 


	Código con explicación:
Primera línea (título del programa). - Circuito para aprender Spice
*<- asterisco para poner comentario. - *Resistencias
•	A continuación, se debe describir todas las resistencias 
R1 n1 n4 20 (quiere decir que la resistencia 1 está conectada entre el nodo n1-n4 y tiene un valor de 20 ohms)
R2 n1 n2 5
R3 n2 n5 5
R4 n2 n3 5
R5 n3 n6 15
R6 n1 n3io 10

*Fuentes independientes
V1 n4 0 DC 15 (quiere decir que el voltaje 1 está conectado entre el n4 y la tierra, primero es n4 porque es positivo y luego 0 porque es negativo, es una fuente de tensión constante y tiene un valor de 15 voltios)
V2 0 n6 DC 10
I1 n1 n3 DC 3

*Fuentes de medición de corrientes
Vio n3io n3 DC 0 (Debemos agregar la fuente de medición a la corriente Vio la cual tiene la particularidad de ser una fuente de tensión y además con una tensión igual a 0)

*Fuentes dependientes
H1 n5 0 Vio 4 (Esta fuente H1 está conectado entre n5 y 0, a su vez está controlada por la fuente io la cual es medida por la fuente Vio y tiene una ganancia de 4)

.end (Se finaliza el circuito del programa)


	Código en documento de texto
 ![image](https://user-images.githubusercontent.com/95496629/144930689-8f1f2791-099c-4733-bf4a-40b6478bf77c.png)

	Este código debe ser guardado en el programa de ngspice en dos pasos:
 
1. Se guarda como un archivo .cir
 ![image](https://user-images.githubusercontent.com/95496629/144930718-072b0330-78a1-4361-8ba6-7fd337eea5ca.png)

2. Se guarda el archivo dentro de la carpeta de ngspice


-	Código en NGSPICE
-	Antes que nada no olvidar descomprimir la carpeta de ngspice
 ![image](https://user-images.githubusercontent.com/95496629/144930752-ae49ed67-5b0f-4b45-9a80-14f6d9cfd3a2.png)
![image](https://user-images.githubusercontent.com/95496629/144930782-a6c549c1-f335-46a0-9ae5-abfd0380b7d9.png)

 
De esta manera se inicia el programa en el cual describe que es un simulador para circuitos, el creador del programa junto con los derechos, manual y la fecha de creación.

![image](https://user-images.githubusercontent.com/95496629/144930796-31b74d16-52e9-4c1c-bb74-2e309bfbde72.png)

 
Para abrir el circuito que hemos escrito en un documento de texto se debe ingresar la palabra “source” junto con el nombre del archivo. Luego de eso se desplegará el nombre del circuito.
![image](https://user-images.githubusercontent.com/95496629/144930818-c4c90049-661b-40fc-8f04-98a1c532f411.png)

 
Se procede a digitar la palabra “listing”, la cual su función será desplegar toda la definición del circuito. Como se observa en la imagen se puede ver que el código es el mismo que escribimos en el archivo de texto.
![image](https://user-images.githubusercontent.com/95496629/144930828-4dbd639a-e3a4-4d7e-b052-51e0f2d52f9b.png)

 
Luego se ingresa el comando “op”, que significa operation point, lo cual quiere decir que es el punto de operación que funciona cuando todo está constante mediante una fuente DC. Como se puede observar el programa ha analizado todo el circuito.
![image](https://user-images.githubusercontent.com/95496629/144930852-77a174a9-d521-4bfb-b9d7-b3a368ee6d90.png)

 
Finalmente, para poder ver todas las tensiones del circuito se debe poner el comando “print all”, lo que quiere decir imprimir todo, cuya función será dar todos los resultados del circuito, por ejemplo, el primero que dice h1#branch quiere decir la corriente que pasa por la fuente de tensión controlada, n1 es la tensión del nodo uno, n2 la tensión del nodo 2 y así sucesivamente; todas estas tensiones están medidas con respecto a tierra. Otros datos que me brinda el programa es la corriente por la fuente V1, V2 e Vio, si da negativo quiere decir que la corriente está saliendo.

	2.4 Resultados 
-	Código completo en NGSPICE
![image](https://user-images.githubusercontent.com/95496629/144930863-32a062c8-efc7-4b18-81df-4b4bb5cbb0c8.png)

 


3.	Conclusiones:

•	Este programa es muy útil ya que cuenta con múltiples herramientas que permiten realizar un circuito que permite hacer pruebas sin correr el riesgo de dañar algún circuito ya que este circuito trabaja correctamente en el simulador.

•	Ngspice permite tener un circuito que será fácil de armar en una tabla de prototipo y se puede tener la seguridad de que el circuito va a funcionar de manera correcta.

•	Con el simulador se puede hallar de manera fácil los errores y problemas que surgen a la hora de ensamblar los circuitos eléctricos, con algunas herramientas con la cuales el programa viene incluido. 

4.	Recomendaciones:

•	Se recomienda tener un previo conocimiento del funcionamiento del simulador para manejar el programa ya que podría llegar a generar retrasos en el diseño, se debe estudiar de manera completa todas las componentes, comandos y opciones que tiene el programa para poder realizar un trabajo de manera funcional y efectiva.

•	Es importante tener instalado algún editor de textos que permite trabajar con texto sin formato ya que este puede ser utilizado como un editor de código para programadores, se recomienda utilizar un editor como Notepad++, Atom, Sublime text, entre otros.

•	Es recomendable dibujar el circuito antes de comenzar a codificar, para poder entender desde donde parte la corriente y sigue su trayectoria, también se deberá describir todo el circuito dentro del grafico incluyendo nodos, resistencias con sus respectivos valores, tierra de referencia, voltajes, corrientes y todo lo que sea necesario escribir en el programa.


5. Video:
https://www.youtube.com/watch?v=14r8h_bEIyw


6.	Bibliografías y Referencias: 
Automática EIE. (2020, 2 mayo). Introducción a SPICE con ngspice [Vídeo], Departamento de Automática de la Escuela de Ingeniería Eléctrica, Universidad de Costa Rica. YouTube. https://www.youtube.com/watch?v=wx6ysVJEjqQ

Zerberros, Z. J. (s. f.). Introdución a NGSPICE. GitHub. Recuperado 1 de diciembre de 2021, de https://zerberros.github.io/blog/2017/11/17/introducion-a-ngspice.html








