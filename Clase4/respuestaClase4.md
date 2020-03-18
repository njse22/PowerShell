#Ejercicios Clase 4 
-------------------

**1.** Mostrar una tabla de procesos que incluya �nicamente los nombres de los
   procesos, sus IDs, y si est�n respondiendo a Windows (la propiedad
   ``Responding`` muestra eso). Haga que la tabla tome el m�nimo de espacio
   horizontal, pero no permita que la informaci�n se trunque.

**Respuesta:**

```powershell
 Get-Process | ft Name,Id,Responding -Wrap
```


**2.**  Muestre una tabla de procesos que incluya los nombres de los procesos y sus
   IDs. Tambi�n incluya columnas para uso de memoria virtual y f�sica;
   exprese dichos valores en megabytes (MB).

**Respuesta:**

```powershell
Get-Process | ft Name,Id,@{n='VM(MB)';e={$_.VM / 1MB}},@{n='PM(MB)';e={$_.PM / 1MB}}
```

**3.**  Emplee ``Get-EventLog`` para mostrar una lista de los logs de eventos
   disponibles (revise la ayuda para encontrar el par�metro que le permitir�
   obtener dicha informaci�n). Formatee la salida como una tabla que incluya
   el nombre de despliegue del log y el per�odo de retenci�n. Los encabezados
   de columna deben ser NombreLog y Per-Retencion.

**Respuesta:**

```powershell
Get-EventLog -List | ft @{n='NombreLog';e={$_.Log}},@{n='Per-Retencion';e={$_.minimumRetentionDays}}
```

**4.** Muestre una lista de servicios, de tal manera que aparezcan agrupados los
   servicios que est�n iniciados y los que est�n detenidos. Los que est�n
   iniciados deben aparecer primero.

**Respuesta:**

```powershell
Get-Service | sort Status -Descending | ft -GroupBy status
```

**5.** Mostrar una lista a cuatro columnas de todos los directorios que est�n en
   el ra�z de la unidad ``C:``

**Respuesta:**

```powershell
ls -Path C:\ | fw name -col 4
```

**6.** Cree una lista formateada de todos los archivos ``.exe`` del directorio
   ``C:\Windows``. Debe mostrarse el nombre, la informaci�n de versi�n, y el
   tama�o del archivo. La propiedad de tama�o se llama ``length`` en Powershell,
   pero para mayor claridad, la columna se debe llamar **Tama�o** en su listado.

**Respuesta:**

```powershell
 ls -Path C:\Windows\ | where -Filter {$_.Name -like "*.exe"}| fl Name,VersionInfo,@{n='Tama�o';e={$_.'length'}}
```

**7.** Importe el m�dulo ``NetAdapter`` (empleando el comando ``Import-Module
   NetAdapter``).
   Empleando el cmdlet ``Get-NetAdapter``, muestre una lista de adaptadores no
   virtuales (adaptadores cuya propiedad Virtual sea falsa. El valor l�gico
   falso es representado por Powershell como ``$False``).

**Respuesta:**

```powershell
 Import-Module NetAdapter
 Get-NetAdapter | fl | where -Filter {$_.Virtual -eq $false}
```

**8.** Importe el m�dulo ``DnsClient``. Empleando el cmdlet ``Get-DnsClientCache``,
   muestre una lista de los registros ``A`` y ``AAAA`` que est�n en el cach�.
   Sugerencia: Si el cach� est� vac�o, visite algunos sitios web para poblarlo.

**Respuesta:**

```powershell
Get-DnsClientCache | fl | where -Filter {$_.Type -eq 1 -or $_.Type -eq 28} 
```

**9.**  Genere una lista de todos los archivos ``.exe`` del directorio
   ``C:\Windows\System32`` que tengan m�s de 5 MB.

**Respuesta:**

```powershell
ls -Path C:\Windows\System32 | fl | where -Filter {$_.Name -like "*.exe"} | where -Filter {$_.Length -ge 5MB}
```

**10.** Muestre una lista de parches que sean actualizaciones de seguridad.

**Respuesta:**

```powershell
 Get-HotFix -Description "Security*" | fl 
```

**11.**  Muestre una lista de parches que hayan sido instalados por el
    usuario ``Administrador``, que sean actualizaciones. Si no tiene ninguno,
    busque parches instalados por el usuario ``System``. Note que algunos parches
    no tienen valor en el campo ``Installed By``.

**Respuesta:**

```powershell
 Get-HotFix | where -Filter {$_.InstalledBy -like "*SYS*"} | fl 
```

**12.** Genere una lista de todos los procesos que est�n corriendo con el nombre
    **Conhost** o **Svchost**.

**Respuesta:**

```powershell
 Get-Process | where -Filter {$_.name -like "Conhost" -or $_.name -like "Svchost" } 
```
