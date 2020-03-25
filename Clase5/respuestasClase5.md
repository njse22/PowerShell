## Clase 5

**1.** ¿Cuál clase puede emplearse para consultar la dirección IP de un adaptador
   de red? ¿Posee dicha clase algún método para liberar un préstamo de
   dirección (lease) DHCP?

**Respuesta:**

```powershell
 Get-WmiObject -Namespace root/CIMv2 -List | where -filter {$_.name -like "*adapter*"}
 get-cimInstance win32_networkadapterconfiguration | Select IP
```

el metodo para liberar un prestano de dirección DHCP es: 

```console
 ReleaseDHCPLease
```


**2.** Despliegue una lista de parches empleando WMI (Microsoft se refiere a los
   parches con el nombre **quick-fix engineering**). Es diferente el listado al
   que produce el cmdlet ``Get-Hotfix``?

**Respuesta:**
```powershell
 Get-WmiObject -Namespace root/CIMv2 -List | where -filter {$_.name -like "*fix*"}
 Get-WmiObject Win32_QuickFixEngineering |fl
```


**3.** Empleando WMI, muestre una lista de servicios, que incluya su status actual,
   su modalidad de inicio, y las cuentas que emplean para hacer login.

**Respuesta:**
```powershell
 Get-WmiObject -Namespace root/CIMv2 -List | where -filter {$_.name -like "*service*"} 
 Get-WmiObject win32_service | select Status,starMode, startname | fl 
```

**4.** Empleando cmdlets de CIM, liste todas las clases del namespace
   ``SecurityCenter2``, que tengan **product** como parte del nombre.

**Respuesta:**
```powershell
Get-CimClass -Namespace root/SecurityCenter2 | where -filter {$_.CimClassName -like "*product*"} | fl 
```

**5.** Empleando cmdlets de CIM, y los resultados del ejercicio anterior, muestre
   los nombres de las aplicaciones antispyware instaladas en el sistema.
   También puede consultar si hay productos antivirus instalados en el sistema.

**Respuesta:**

```powershell
Get-CimInstance -Namespace root/SecurityCenter2 -ClassName "AntiSpywareProduct" | select displayName 
Get-CimInstance -Namespace root/SecurityCenter2 -ClassName "AntiVirusProduct" | select displayName 
```
