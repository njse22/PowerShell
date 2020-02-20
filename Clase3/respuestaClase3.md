# PowerShell
-------------

Ejercicios clase 3: 

**1.** Cree dos archivos de texto similares (con una o dos líneas diferentes).
   Compárelos empleando ``diff``.

**Respuesta:**

```powershell

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

**2.** Qué ocurre si se ejecuta:
   ```powershell
   get-service | export-csv servicios.csv | out-file
   ```
 Por qué?

**Respuesta:**

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

porque el parametro `` out-file `` esta esperando que le sea especificado un archivo 

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


**3.** Cómo haría para crear un archivo delimitado por puntos y comas (;)?
   PISTA: Se emplea ``export-csv``, pero con un parámetro adicional.

**Respuesta:**

se utiliza el siguiente comando: 

```powershell
	get-service | export-csv servicios2.csv -Delimiter ";"
```

**4.** ``Export-cliXML`` y ``Export-CSV`` modifican el sistema, porque pueden crear
   y sobreescribir archivos. Existe algún parámetro que evite la
   sobreescritura de un archivo existente? Existe algún parámetro que
   permita que el comando pregunte antes de sobresscribir un archivo?

**5.** Windows emplea configuraciones regionales, lo que incluye el separador de
   listas. En Windows en inglés, el separador de listas es la coma (,).
   Cómo se le dice a ``Export-CSV`` que emplee el separador del sistema en lugar
   de la coma?

**Respuesta:**
```powershell
Get-Process |Export-Csv servicios4.csv -Delimiter ((Get-Culture).TextInfo.ListSeparator)

cat .\servicios4.csv

#TYPE System.Diagnostics.Process
"Name";"SI";"Handles";"VM";"WS";"PM";"NPM";"Path";"Company";"CPU";"FileVersion";"ProductVersion";"Descript
ion";"Product";"__NounName";"BasePriority";"ExitCode";"HasExited";"ExitTime";"Handle";"SafeHandle";"Handle
Count";"Id";"MachineName";"MainWindowHandle";"MainWindowTitle";"MainModule";"MaxWorkingSet";"MinWorkingSet
";"Modules";"NonpagedSystemMemorySize";"NonpagedSystemMemorySize64";"PagedMemorySize";"PagedMemorySize64";
"PagedSystemMemorySize";"PagedSystemMemorySize64";"PeakPagedMemorySize";"PeakPagedMemorySize64";"PeakWorki
ngSet";"PeakWorkingSet64";"PeakVirtualMemorySize";"PeakVirtualMemorySize64";"PriorityBoostEnabled";"Priori
tyClass";"PrivateMemorySize";"PrivateMemorySize64";"PrivilegedProcessorTime";"ProcessName";"ProcessorAffin
ity";"Responding";"SessionId";"StartInfo";"StartTime";"SynchronizingObject";"Threads";"TotalProcessorTime"
;"UserProcessorTime";"VirtualMemorySize";"VirtualMemorySize64";"EnableRaisingEvents";"StandardInput";"Stan
dardOutput";"StandardError";"WorkingSet";"WorkingSet64";"Site";"Container"
```

**6.** Identifique un cmdlet que permita generar un número aleatorio.

**Respuesta:**
el comando random genera un número aleatorio 

```powershell
	random
	433184730
	random
	1019773911
```


**7.** Identifique un cmdlet que despliegue la fecha y hora actuales.

**Respuesta:**

```powershell
	date
	sábado, 15 de febrero de 2020 1:57:54 p. m.
```

**8.** Qué tipo de objeto produce el cmdlet de la pregunta 7?

**Respuesta:**
el objeto producido por el comando de la pregunta 7 en un ``DateTime``

```powershell 	
date | gm


   TypeName: System.DateTime

Name                 MemberType     Definition                                                           
----                 ----------     ----------                                                           
Add                  Method         datetime Add(timespan value)                                         
AddDays              Method         datetime AddDays(double value)              
```


**9.** Usando el cmdlet de la pregunta 7 y ``select-object``, despliegue solamente
   el día de la semana, así:

```console
   DayOfWeek
   ---------
    Thursday
```

**Respuesta:**

la siguiente linea de comando da el resultado pedido 

```powershell
	date | Select-Object DayOfWeek

	DayOfWeek
	---------
 	Saturday
 ```


**10.** Identifique un cmdlet que muestre información acerca de parches (hotfixes)    instalados en el sistema.

**Respuesta:**

el comando ``Get-HotFix`` retorna los hotfixes instalados en el sistema

```powershell
Get-HotFix

Source        Description      HotFixID      InstalledBy          InstalledOn              
------        -----------      --------      -----------          -----------              
DESKTOP-O7... Update           KB4534131     NT AUTHORITY\SYSTEM  12/02/2020 12:00:00 a. m.
DESKTOP-O7... Update           KB4462930     NT AUTHORITY\SYSTEM  4/02/2020 12:00:00 a. m. 
DESKTOP-O7... Update           KB4465065     NT AUTHORITY\SYSTEM  4/02/2020 12:00:00 a. m. 
DESKTOP-O7... Update           KB4486153     NT AUTHORITY\SYSTEM  4/02/2020 12:00:00 a. m. 
DESKTOP-O7... Security Update  KB4516115     NT AUTHORITY\SYSTEM  4/02/2020 12:00:00 a. m. 
DESKTOP-O7... Security Update  KB4523204     NT AUTHORITY\SYSTEM  4/02/2020 12:00:00 a. m. 
DESKTOP-O7... Security Update  KB4524244     NT AUTHORITY\SYSTEM  12/02/2020 12:00:00 a. m.
DESKTOP-O7... Security Update  KB4537759     NT AUTHORITY\SYSTEM  12/02/2020 12:00:00 a. m.
DESKTOP-O7... Security Update  KB4532691     NT AUTHORITY\SYSTEM  12/02/2020 12:00:00 a. m.
```

**11.** Empleando el cmdlet de la pregunta 10, muestre una lista de parches
    instalados. Luego extienda la expresión para ordenar la lista por fecha
    de instalación, y muestre en pantalla únicamente la fecha de instalación,
    el usuario que instaló el parche, y el ID del parche. Recuerde examinar
    los nombres de las propiedades.

**Respuesta:**

```powershell

Get-HotFix | Select-Object InstalledOn,InstalledBy,HotFixID | Sort-Object -Property InstalledOn

InstalledOn               InstalledBy         HotFixID 
-----------               -----------         -------- 
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4462930
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4465065
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4486153
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4516115
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4523204
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4534131
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4524244
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4537759
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4532691
```

**12.** Complemente la solución a la pregunta 11, para que el sistema ordene los
    resultados por la descripción del parche, e incluya en el listado la
    descripción, el ID del parche, y la fecha de instalación.
    Escriba los resultados a un archivo HTML.

**Respuesta:**

```powershell
Get-HotFix | Select-Object -Property InstalledOn, InstalledBy, HotfixID | Sort-Object -Property InstalledOn

InstalledOn               InstalledBy         HotfixID 
-----------               -----------         -------- 
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4462930
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4465065
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4486153
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4516115
4/02/2020 12:00:00 a. m.  NT AUTHORITY\SYSTEM KB4523204
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4534131
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4524244
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4537759
12/02/2020 12:00:00 a. m. NT AUTHORITY\SYSTEM KB4532691
```

**13.** Muestre una lista de las 50 entradas más nuevas del log de eventos System.
    Ordene la lista de modo que las entradas más antiguas aparezcan primero;
    las entradas producidas al mismo tiempo deben ordenarse por número índice.
    Muestre el número índice, la hora y la fuente para cada entrada. Escriba
    esta información en un archivo de texto plano.

**Respuesta:**

```powershell
Get-EventLog -LogName System -Newest 50 | Select-Object -Property Index, TimeGenerated, Source | Sort-Object -Property TimeGenerated, Index > eventLog.txt

cat .\eventLog.txt

Index TimeGenerated            Source                               
----- -------------            ------                               
 1457 19/02/2020 4:47:06 p. m. Microsoft-Windows-Kernel-General     
 1458 19/02/2020 4:47:07 p. m. Microsoft-Windows-Kernel-General     
 1459 19/02/2020 4:47:07 p. m. Microsoft-Windows-Kernel-General     
 1460 19/02/2020 4:47:07 p. m. Microsoft-Windows-Dhcp-Client        
 1461 19/02/2020 4:47:07 p. m. Microsoft-Windows-Dhcp-Client        
 1462 19/02/2020 4:47:07 p. m. Microsoft-Windows-DHCPv6-Client      
 1463 19/02/2020 4:47:08 p. m. Microsoft-Windows-FilterManager      
 1464 19/02/2020 4:47:08 p. m. Microsoft-Windows-FilterManager      
 1465 19/02/2020 4:47:08 p. m. Microsoft-Windows-FilterManager      
 1466 19/02/2020 4:47:08 p. m. Microsoft-Windows-FilterManager      
 1467 19/02/2020 4:47:08 p. m. Microsoft-Windows-FilterManager      
 1468 19/02/2020 4:47:08 p. m. Microsoft-Windows-FilterManager      
 1469 19/02/2020 4:47:11 p. m. Service Control Manager              
 1470 19/02/2020 4:47:19 p. m. Microsoft-Windows-Kernel-General     
 1471 19/02/2020 4:47:49 p. m. Microsoft-Windows-Kernel-General     
 1472 19/02/2020 4:47:57 p. m. Microsoft-Windows-Winlogon           
 1474 19/02/2020 4:47:57 p. m. Microsoft-Windows-Kernel-General     
 1473 19/02/2020 4:47:58 p. m. Kerberos                             
 1475 19/02/2020 4:47:58 p. m. Microsoft-Windows-Kernel-General     
 1476 19/02/2020 4:48:06 p. m. DCOM                                 
 1477 19/02/2020 4:48:06 p. m. DCOM                                 
 1478 19/02/2020 4:48:30 p. m. Microsoft-Windows-Kernel-General     
 1479 19/02/2020 4:48:37 p. m. Microsoft-Windows-Kernel-General     
 1480 19/02/2020 4:48:40 p. m. Microsoft-Windows-Kernel-General     
 1481 19/02/2020 4:48:44 p. m. Microsoft-Windows-Kernel-General     
 1482 19/02/2020 4:48:51 p. m. Microsoft-Windows-Kernel-General     
 1483 19/02/2020 4:49:07 p. m. Microsoft-Windows-Kernel-General     
 1484 19/02/2020 4:49:54 p. m. Microsoft-Windows-Kernel-General     
 1485 19/02/2020 4:49:55 p. m. Microsoft-Windows-Kernel-General     
 1486 19/02/2020 4:50:30 p. m. DCOM                                 
 1487 19/02/2020 4:50:30 p. m. DCOM                                 
 1488 19/02/2020 4:50:30 p. m. DCOM                                 
 1489 19/02/2020 4:50:31 p. m. Microsoft-Windows-Kernel-General     
 1490 19/02/2020 4:50:41 p. m. Microsoft-Windows-Kernel-General     
 1491 19/02/2020 4:50:42 p. m. Microsoft-Windows-Kernel-General     
 1492 19/02/2020 4:50:42 p. m. Microsoft-Windows-Kernel-General     
 1493 19/02/2020 4:50:42 p. m. Microsoft-Windows-FilterManager      
 1494 19/02/2020 4:52:40 p. m. Service Control Manager              
 1495 19/02/2020 4:52:42 p. m. Microsoft-Windows-WindowsUpdateClient
 1496 19/02/2020 4:52:50 p. m. Microsoft-Windows-WindowsUpdateClient
 1497 19/02/2020 4:52:55 p. m. Microsoft-Windows-WindowsUpdateClient
 1498 19/02/2020 4:53:22 p. m. Microsoft-Windows-WindowsUpdateClient
 1499 19/02/2020 4:53:22 p. m. Microsoft-Windows-Kernel-General     
 1500 19/02/2020 4:53:38 p. m. Microsoft-Windows-Kernel-General     
 1501 19/02/2020 4:58:44 p. m. Microsoft-Windows-Kernel-General     
 1502 19/02/2020 4:59:19 p. m. Microsoft-Windows-Kernel-Power       
 1503 19/02/2020 4:59:42 p. m. Microsoft-Windows-Kernel-General     
 1504 19/02/2020 4:59:50 p. m. Microsoft-Windows-Kernel-General     
 1505 19/02/2020 4:59:52 p. m. Microsoft-Windows-WindowsUpdateClient
 1506 19/02/2020 5:00:02 p. m. Microsoft-Windows-WindowsUpdateClient
```
