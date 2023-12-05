# Robotica_2023-2_EPSON

## Integrantes

- Wilfer Armando Fiquitiva Mendez.
- Johan Leonardo Castellanos Ruiz.
- Juan Pablo Cardenas Higuera.

## Desarrollo de la practica.
Inicialmente se asistió a una capacitación virtual donde se tuvo un acercamiento al software de programación de EPSON del robot escara en donde vimos cómo se debían hacer movimientos en modo JOG, definición de puntos para trayectorias, rutina HOME, y una simulación de Pick and Place.

En el siguiente video teneos la simulacion de los comandos de JOG en las cuales se puede simular el robot scara Epson T6

[joging - Practica Epson.webm](https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/981f6d5b-bfbd-4eaf-8301-aa0806d20364)


El siguiente codigo muestra los diferentes paletizados usados en la practica:




Posterior a ello con las indicaciones previas en la capacitación hicimos la instalación del software y se hizo una simulación de una rutina de pick and place en una matriz de movimiento de elementos incluyendo la rutina de home..

Los puntos programados para las rutinas en el codigo se pueden observar en la siguiente tabla
![Tabla Epson Puntos](https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/05aa9391-5d84-4662-bd54-f4eff518329e)

Rutinas de paletizado:

```prg
Global Integer Out_11, Out_12
Integer i, j

Function main
	Pallet 1, Origen, Ejey, Ejex, 2, 3
	Pallet Outside, 2, Origen, Ejey, Ejex, 2, 3
	
	Motor On
	Power High
	Accel 50, 50
	Speed 75
	Out_11 = 515
	Out_12 = 516
	
Do
	If MemSw(512) Then
		Call paletizado_z
	EndIf
	If MemSw(513) Then
		Call paletizado_s
	EndIf
	If MemSw(514) Then
		Call paletizado_externo
	EndIf
Loop

		
Fend

Function paletizado_externo
	#define estado_paletizado_ex 517
	MemOn estado_paletizado_ex
	For i = 1 To 3
		For j = 1 To 4
			Jump Pallet(2, i, j)
		Next
	Next
	MemOff estado_paletizado_ex
Fend

Function paletizado_s
	MemOn Out_11
	For i = 1 To 2
		Jump Pallet(1, i)
	Next
	Jump Pallet(1, 4)
	Jump Pallet(1, 3)
	For i = 5 To 6
		Jump Pallet(1, i)
	Next
	MemOff Out_11
	Fend
Function paletizado_z
	MemOn Out_12
	For i = 1 To 6
		Jump Pallet(1, i)
	Next
	MemOff Out_12
	Fend
```
Simulacion de rutina Paletizado en z:

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/acba3911-4bf4-4ad7-8ba1-560536b4f4c4

Simulacion de rutina Paletizado en s:

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/a0dee71e-e997-4af2-8959-341ac57e0686

Simulacion de rutina Paletizado Externo:

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/71040a26-b28c-4155-961f-aaaef3424813

Una vez se tuvo lista la practica simulada en el software de EPSON se programó la visita a las instalaciones de Control de movimiento en donde el objetivo fue tener un acercamiento real con el robot y poder interactuar con él, haciendo puesta a punto del robot, definiendo su espacio de trabajo y parametrizando las condiciones de operación de acuerdo al espacio, soporte y estabilidad donde se encontraba el robot.

Una vez realizada la parametrización puesto a punto se hizo una verificación simulada en el software y se envió el código de la rutina al robot para ser ejecutada como se muestra en los videos.

Practica paletizado en z a velocidad baja

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/af89b3ed-429f-4cb4-8b00-07debbfa292d

Practica paletizado en z a velocidad alta

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/f9cb6041-a632-4d3d-addb-f5ec08a2bd30

Practica paletizado en s a velocidad baja

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/b044a31c-905f-4617-911e-ae5535b8a3a3

Practica paletizado en s a velocidad alta

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/a07ae375-b61b-46e6-b7c4-625664dfd1d3

Practica paletizado en externo a velocidad baja

[Practica ext1 - Practica Epson.webm](https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/b16476c2-c43d-44db-862d-e7e8323b0a87)

Practica paletizado en externo a velocidad alta

https://github.com/jcardenash99/Robotica_2023-2_EPSON/assets/61796945/4702b4b0-6b9c-45e4-bc62-edd79afcbdc5

Como pudimos observar el robot Epson se puede programar en diferentes tipos de rutinas de desplazamiento para pick an place, el paletizado es una rutina en la que el robot toma un producto y lo ubica en una paleta la cual es una plataforma de varias posiciones organizadas sobre su superficie usada para el almacenaje de productos.

En la practica pudimos observar 2 velocidades, en la realidad tenemos un conjunto de porcentajes de velocidad maxima, como se puede observar en la practica tenemos una velocidad baja la cual corresponde alrededor del 20%-30% de la velocidad, mientras que la velocidad alta corresponde al 60%-80% de la velocidad maxima, en este caso en particular no se pudo usar la maxima velocidad dado a que el robot no poseia un soporte lo suficiente mente firme, como se podia apreciar en la practica a la velocidad alta el la base tembalaba con los movimientos del robot.



