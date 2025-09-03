---
title: "Laboratorios de la plataforma de INE"
date: 2025-09-03 14:52:00 -6GMT
categories: [Ciberseguridad, Pentesting, Certificaciones]
tags: [ejpt, ine, pentesting, laboratorio]

description: "¿Son suficientes los laboratorios de INE para prepararte para la eJPT?"

toc: true

image:
  path: /assets/img/2025-09-03/ine.png
  alt: INE

comments: true
---

## Los laboratorios de la plataforma INE
No se si lo sabias, pero en la plataforma de INE, cuando pagas el Bundle de $249 USD, tienes ademas de la certificación, acceso al curso **"Penetration Testing Studen"**, y no solo eso, también tenemos acceso a todos los cursos de aprendizaje de toda la platafomra de INE, y con ello, a sus laboratorios.

![img-description](/assets/img/2025-09-03/laboratorio_ine.png)
_¿Cómo identifico un laboratorio en INE? Fácil, con un ícono de un "frasco de laboratorio"._

He estado jugando (playing around) con estos laboratorios y la verdad es que estan cumpliendo mis expectativas, es por esta razón, que quiero mostrarles la resolución del primer laboratorio.

Vamos a darle!

## Primer laboratorio INE: Windows Recon: Nmap Host Discovery

En la sección de "Assessment Methodologies: Footprinting & Scanning", vamos a ir a la lección "Host Discovery", aquí encontraremos en el ultimo apartado de la lista el laboratorio "Windows Recon: Nmap Host Discovery", vamos a darle click y se nos mostrara la siguiente pantalla:

![img-description](/assets/img/2025-09-03/windows_recon_nmap_host_discovery.png)
_Windows Recon: Nmap Host Discovery_

Desde aquí tenemos que leer nuestra tarea dandole click en "Tasks", es decir nuestro objetivo, en donde **OJO**, también nos esta indicando nuestro __target__, que es `demo.ine.local`.

![img-description](/assets/img/2025-09-03/guacamole_tasks.png)
_Guacamole_

Ya que tenemos nuestro objetivo claro, a nuestro lado derecho, si es la primera vez que vamos abrir un laboratorio, debemos elegir 2 cosas:

1. "Select region closest to you": este es una region que debemos elegir como la más cercana, esto para tener una mejor latencia de conexión entre nuestra maquina/servicio de internet y el servidor donde nos conectará el laboratorio.
Si estamos en latinoamerica, yo recomiendo que elijas ya sea "US-EAST" o "US-WEST".
2. Keyboard layout: Esta seleccion es importante y te pudiera evitar algunos dolores de cabeza. Esta confguración es basicamente ¿Qué configuración de teclado tienes en tu maquina? No se si sabian pero incluso en latinoamerica tenemos configuraciones de teclado diferentes, así que elijan bien si no los caracteres o las letras les saldran movidos. En mi caso estoy acostumbrado a usar "Spanish Latin American" o incluso "US English".

Ahora si, vamos a darle a "Start Lab".
Aqui si debemos esperar un momento en lo que se levanta la maquina en linea.
Una vez que veamos la opcion de "Open Lab"...

![img-description](/assets/img/2025-09-03/open_lab.png)
_Open Lab_

... se nos abrirá una pestaña con la maquina virtual, una plataforma que ellos le llaman `Guacamole`:

![img-description](/assets/img/2025-09-03/guacamole.png)
_Guacamole_

... que básicamente es un maquina de Kali Linux en linea.

### Nuestro objetivo: Descubrir host disponibles y sus puertos abiertos y sus servicios usando Nmap

Una buena practica que me he hecho desde que he iniciado con el `Pentesting` ha sido identificar si es posible hacer ping a nuestro objetivo, y esta ves no sera la excepción.

#### Ping a nuestro objetivo

Vamos hacerle un ping a nuestro `target`, que en nuestro caso es `demo.ine.local`.
Para esto abrimos una terminal (podemos usar la tecla de `Windows` de nuestro tecleado y buscar `terminal` y dar enter), posteriormente ejecutamos el siguiente comando:

```bash
# ping -c 1 demo.ine.local
```

Vamos a ver que resultado nos da:

![img-description](/assets/img/2025-09-03/ping_target_ine_local.png)
_ping a nuestro target_

__Imporrante__: por aquí hubo una confusión de mi parte, era `demo.ine.local` en lugar de `target.ine.local`... aun que no iba a contestar de todas maneras XD... continuamos...

Bien, como vemos no nos responde, pero esto no quiere decir que la maquina este **inaccesible, desconecatada o apagada**, mas bien solo nos indica que el protocolo `icmp` esta impidiendo resolver el ping.

Para nuestro caso, no importa, vamos a continuar.

#### Adentrandonos con la herramienta Nmap

Vamos a ejecutar un escaneo de puertos sobre nuestro target, y como sabemos que el ping no esta accesible, vamos agregarle el parametro `-Pn` para que no intente mandar una traza `icmp`, ademas, como yo quiero identificar puertos abiertos y sus servicios agregaré los parametros `--open` y `-sSCV`:

```bash
# nmap -Pn --open -sSCV demo.ine.local
```

Ejecutamos y esperamos un poco...

![img-description](/assets/img/2025-09-03/nmap_port_scanning.png)
_Escaneo de Nmap con puertos abiertos y ejecucion de scripts para obtener servicios y versiones_

Bien, ya tenemos un resultado donde podemos observar que tenemos los puertos 80 (servicio HttpFileServer httpd 2.3), 135, 139, 445, 3389, 49154, 49155.. sus servicios y sus versiones.

Para este punto, el laboratorio ya debió haber identificado que nosotros ejecutamos correctamente el comando de Nmap y hemos descuberto tanto el descubrimiento de puertos abiertos, ademas sus servicios y la versión de dicho servicio.

¿Como es que nos damos cuenta que si hemos cumplido con el reto del laboratorio?
Fácil, en la pestaña, usualmente de donde se abrio nuestro `Guacamole` es donde podemos refrescar la pagina y veremos un `Finished` en verde en seguida del `ACTIVITY STATUS`, tal que se muestre de la siguinete manera:

![img-description](/assets/img/2025-09-03/activity_status_finished.png)
_Activity Status = Finished_

## ¿Tenemos guias en los laboratorios?

Si, tenemos 2 opcines, una junto a las opciones de "Overview" y "Tasks" que es nuestra opcion `Solutions`:

![img-description](/assets/img/2025-09-03/solutions.png)
_Solucion escrita_

... y ademas una opción adicional, la cual ya es un video que la podemos encontrar en la poret posterior al boton de "Stop Lab" y "Open Lab":

![img-description](/assets/img/2025-09-03/reveal_solution.png)
_Video de solución_

## Conclusiones

Desde mi punto de vista, los laboratorios de INE son un gran aporte a los cursos en video, ya que, primero que nada, son muy largos en el curso "Penetration Testing Student" y segundo, por que intentar rendir un examen práctico de forma solamente teórica, pudiera llegar a ser frustrante, tedioso, entre muchas otras cosas.

En fin, para mi es una gran ayuda para poder entrenar nuestros conocimientos.

Espero que te haya gustado este aporte, por mi parte es todo y espero que sigas estudiando para que puedas convertirte muy pronto en un Jr. Penetration Tester con esta certificación.

Saludos y hasta la proxima.