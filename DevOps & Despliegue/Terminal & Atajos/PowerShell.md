# PowerShell (Windows)

PowerShell es una shell de línea de comandos y lenguaje de scripting orientado a objetos, usado para administración de sistemas Windows.

## 1. Comandos básicos

### 1.1. Navegación y Sistema de Archivos

```powershell
Get-Location         # Ver carpeta actual
Set-Location C:\     # Cambiar de directorio
Get-ChildItem        # Listar archivos y carpetas (alias: ls)
New-Item archivo.txt # Crear archivo
Remove-Item archivo.txt # Eliminar archivo
Copy-Item fuente destino # Copiar archivo o carpeta
Move-Item fuente destino # Mover archivo o carpeta
Get-Content archivo.txt                # Leer archivo
Set-Content archivo.txt "Hola"         # Escribir (sobrescribe)
Add-Content archivo.txt "Otra línea"   # Agregar línea
Rename-Item archivo.txt nuevo.txt      # Renombrar archivo
Compress-Archive carpeta salida.zip    # Comprimir
Expand-Archive salida.zip carpeta/     # Descomprimir
```

### 1.2. Gestión del Sistema

```powershell
Get-Process           # Ver procesos
Stop-Process -Name notepad  # Terminar proceso
Get-Counter '\Processor(_Total)\% Processor Time'  # Uso general de CPU
Get-Counter '\Process(chrome)\% Processor Time'    # Uso de CPU de un proceso
Get-Service           # Ver servicios
Start-Service nombre  # Iniciar servicio
Stop-Service nombre   # Detener servicio
Restart-Computer      # Reiniciar PC
```

### 1.3. Scripts y Automatización

```powershell
# Guardar en archivo.ps1 y ejecutarlo:
.\archivo.ps1
```

### 1.4. Información del Sistema

```powershell
Get-ComputerInfo      # Información general
Get-EventLog -LogName System -Newest 10  # Últimos 10 logs
Get-CimInstance Win32_OperatingSystem        # Sistema operativo
Get-CimInstance Win32_ComputerSystem         # RAM, nombre de equipo, etc.
Get-CimInstance Win32_Processor              # CPU
Get-CimInstance Win32_LogicalDisk            # Discos
Get-PhysicalDisk                             # Info física de discos
Get-Volume                                   # Volúmenes montados
```

### 1.5. Redes

```powershell
Get-NetIPAddress                     # Ver IPs
Test-Connection google.com           # Hacer ping
Resolve-DnsName google.com           # Resolver DNS
Get-NetAdapter                      # Info de adaptadores
Get-NetRoute                        # Tabla de rutas
```

### 1.6. Usuarios y Grupos (Administración local)

```powershell
Get-LocalUser                         # Ver usuarios
Get-LocalGroup                        # Ver grupos
New-LocalUser -Name "usuario" -Password (Read-Host -AsSecureString)  # Crear usuario
Add-LocalGroupMember -Group "Administrators" -Member "usuario"       # Agregar a grupo
```

### 1.7. Historial y Aliases

```powershell
Get-History        # Ver historial
Invoke-History 5   # Ejecutar comando 5 del historial
Get-Alias          # Ver alias disponibles
```

### 1.8. Seguridad

```powershell
Get-ExecutionPolicy               # Ver política actual (p. ej. Restricted, RemoteSigned)
Set-ExecutionPolicy RemoteSigned  # Cambiar (requiere admin)
```

### 1.9. Módulos y Ayuda

```powershell
Get-Module -ListAvailable        # Ver módulos instalados
Import-Module nombre             # Importar un módulo
Update-Help                      # Actualizar ayuda de PowerShell
Get-Help Get-Process             # Ver ayuda de un comando
```

### 1.10. Tips Avanzados

```powershell
# Filtrar y seleccionar columnas
Get-Process | Where-Object { $_.CPU -gt 100 } | Select-Object Name, CPU

# Exportar resultados a CSV o JSON
Get-Process | Export-Csv procesos.csv -NoTypeInformation
Get-Process | ConvertTo-Json | Out-File procesos.json        # Ver ayuda de un comando
```
