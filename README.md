# Comunicación de Datos y Redes

**Alumnos:** Felipe Sánchez Arnés y Karla Jiménez Millar  
**Carrera:** Ingeniería Civil en Informática

## Juego Batalla Naval en C++

### 💬 Enunciado

Implemente el Juego Batalla Naval mediante el modelo Cliente/Servidor. Para ello, debe crear dos programas de los cuales uno funcionará como el Servidor de juegos (con peticiones concurrentes) y el otro será el Cliente que se conectará al servidor para jugar.

El juego consiste en los siguientes pasos:

Por parte del cliente:
- Conectar al servidor.
- Definir posiciones de embarcaciones (puede ser aleatoria) y enviarlas al servidor.
- Visualizar tableros.
- Esperar por la indicación del servidor respecto de quién comienza (selección al azar).
- Jugar:
  - Indicar coordenadas de disparo.
  - Esperar y visualizar el resultado.
  - Lo anterior se repite hasta que existe un ganador.

Por parte del servidor:
- Levantar servicio y esperar por conexiones (clientes).
- Por cada jugador conectado (cada hebra):
  - Definir posiciones de embarcaciones (aleatoria).
  - Seleccionar al azar quién comienza el juego.
  - Solicitar disparo o generar disparo al azar según corresponda el turno.
  - Verificar las jugadas.
  - Enviar resultados.
- Mostrar por la terminal información del estado de las conexiones (conexiones nuevas, cerradas), además de los resultados parciales de los juegos.

### ☝️ Consideraciones

- Se debe utilizar **C++ como lenguaje de programación** y su implementación de sockets.
- Orientado a objetos.
- Por juego se deben definir: 1 portaaviones (P), 2 buques (B), 2 submarinos (S) y 3 lanchas (L).
- Portaaviones 5 casillas, buque 4 casillas, submarino 3 casillas, lancha 1 casilla.
- Tamaño de los tableros debe ser 15x15 celdas.
- El servidor debe crear por cada jugador una ejecución independiente, la cual “controlará” el juego. El servidor debe permitir múltiples conexiones y atenderlas simultáneamente.
- El servidor debe levantar su servicio en un puerto TCP/IP que se le indicará al momento de ejecutar, por ejemplo:

```console
$ ./servidor 7777
```
*Donde:*  
*```7777``` indica el puerto donde recibirá conexiones.*

- El cliente debe permitir indicar al momento de ejecutarlo la dirección IP y el puerto del servidor al cual se conectará, por ejemplo:

```console
$ ./cliente 192.168.1.100 7777
```
*Donde:*  
*```192.168.1.100``` es la dirección IP del servidor y ```7777``` es el puerto al cual conectar en el servidor.*

- La manera en que el cliente indique su disparo queda a criterio del programador.
- **IMPORTANTE:** Es el servidor el que debe mantener la información de los tableros de los jugadores y enviar los resultados a cada cliente. El cliente debe mostrar la información que le envía el servidor.

### 💻 Salida por la terminal

#### Por el lado del servidor

```console
$ ./servidor 7777
Esperando conexiones ...

Juego nuevo[IP1:puerto1]
Juego nuevo[IP2:puerto2]
Juego [IP1:puerto1]: inicia disparos el cliente.
Juego nuevo[IP3:puerto3]
Juego [IP2:puerto2]: inicia disparos el servidor.
Juego [IP1:puerto1]: disparo cliente fallido.
Juego [IP3:puerto3]: inicia disparos el cliente.
Juego [IP1:puerto1]: disparo servidor toca portaavión.
...
Juego [IP3:puerto3]: disparo cliente hunde lancha.
Juego [IP2:puerto2]: gana cliente.
...
```

#### Por el lado de los jugadores

```console
$ ./cliente 192.168.1.100 7777

TABLERO MIS EMBARCACIONES

A | L
B |           S S S
C | L
D | P P P P P         S
E |             L S
F |               S
...
--------------------------
    1 2 3 4 5 6   ...   15

TABLERO DISPAROS

A |
B | X   L
C |         X
D |
E |   X P P
F |
...
--------------------------
    1 2 3 4 5 6   ...   15

DISPARAR [CLIENTE]: leer coordenadas, enviar al servidor y mostrar tableros.
o
DISPARAR [SERVIDOR]: esperar resultados y mostrar tableros.
```
