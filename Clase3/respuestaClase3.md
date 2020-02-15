# PowerShell

Ejercicios clase 4: 

1. Mostrar una tabla de procesos que incluya únicamente los nombres de los procesos, sus IDs, y si están respondiendo a Windows (la propiedad Responding muestra eso). Haga que la tabla tome el mínimo de espacio horizontal, pero no permita que la información se trunque.

## **Respuesta:**

```console

  New-Item -ItemType File texto1.txt
  New-Item -ItemType File texto2.txt
  notepad texto1.txt
  notepad texto2.txt

  cat .\texto1.txt
  Nicolas Salazar
  archivo creado
  archivo 1 el bueno 

  cat .\texto2.txt
  Nicolas Salazar
  archivo creado
  archivo 2 el malo

  diff -Ref (cat .\texto1.txt) -Diff (cat .\texto2.txt)

  InputObject         SideIndicator
  -----------         -------------
  archivo 2 el malo   =>           
  archivo 1 el bueno  <=           
```  

2. Qué ocurre si se ejecuta:
   ```powershell
   get-service | export-csv servicios.csv | out-file
   ```
 Por qué?

## **Respuesta:**

la salida del comando anterior es: 

```powershell
	out-file : No se puede procesar el argumento porque el valor del argumento "path" es NULL. 
	Cambie el valor del argumento "path" a un valor no nulo.
	En línea: 1 Carácter: 42
	+ get-service | export-csv servicios.csv | out-file
	+                                          ~~~~~~~~
    		+ CategoryInfo          : InvalidArgument: (:) [Out-File], PSArgumentNullException
    		+ FullyQualifiedErrorId : ArgumentNull,Microsoft.PowerShell.Commands.OutFileCommand

```

porque el parametro ```powershell out-file ``` esta esperando que le sea especificado un archivo 

si por ejemplo escribieramos el comando de la siguiente forma: 

```powershell 
	get-service | export-csv servicios.csv | out-file .\service2.csv
```
no saltaría el error en consola y se crearían los dos archivos ```servicios.csv``` y ```servicios.csv```
pero toda la información del comando ```get-service``` se escriviría en el archivo ```servicios.csv```
por lo cual el comando: 

```powershell 
	get-service | export-csv servicios.csv 
```

produciría el mismo resultado sin errores. 

