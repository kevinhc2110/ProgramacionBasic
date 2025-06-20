# WSL (Linux en Windows)

WSL permite ejecutar una distribución Linux directamente sobre Windows sin necesidad de una máquina virtual.

## 1. Comandos básicos

### 1.1. Comandos Iniciales

```bash
wsl                  # Iniciar WSL
wsl --list           # Ver distribuciones instaladas
wsl --install        # Instalar WSL
```

### 1.2. Navegación y Archivos

```bash
pwd                  # Ver directorio actual
cd /ruta             # Cambiar de directorio
ls -l                # Listar archivos
cp archivo destino   # Copiar archivos
mv archivo destino   # Mover archivos
rm archivo           # Eliminar archivos
mkdir nueva_carpeta  # Crear carpeta
touch archivo.txt    # Crear archivo vacío
cat archivo.txt          # Mostrar contenido
head archivo.txt         # Primeras líneas
tail archivo.txt         # Últimas líneas
tail -f archivo.log      # Ver archivo en tiempo real
nano archivo.txt         # Editar archivo
tar -czvf archivo.tar.gz carpeta/   # Comprimir carpeta
tar -xzvf archivo.tar.gz            # Extraer
zip archivo.zip archivo.txt         # Comprimir ZIP
unzip archivo.zip                   # Extraer ZIP
ls -l > listado.txt       # Redirigir salida a archivo
cat archivo.txt | grep "Error" > errores.txt
```

### 1.3. Búsqueda

```bash
find . -name "*.txt"          # Buscar archivos
grep "texto" archivo.txt      # Buscar dentro de archivos
```

### 1.4. Procesos y Sistema

```bash
ps aux                 # Ver procesos
top                    # Monitor de procesos
kill PID               # Matar proceso
df -h                  # Ver espacio en disco
free -h                # Ver memoria RAM usada
uname -a                 # Información del kernel
hostname                 # Nombre del equipo
uptime                   # Tiempo encendido
whoami                   # Usuario actual
lscpu                    # Info del procesador
lsblk                    # Info de discos
htop                     # Monitor de sistema (más completo que top)
ps aux | grep nombre     # Buscar proceso
kill -9 PID              # Forzar cierre de proceso
watch -n 1 df -h         # Ver espacio disco cada segundo
```

### 1.5. Paquetes

```bash
sudo apt update              # Actualizar índices
sudo apt upgrade             # Actualizar sistema
sudo apt install nombre      # Instalar paquetes
```

### 1.6. Permisos & Propiedades

```bash
chmod +x script.sh       # Hacer ejecutable
chmod 755 archivo        # Asignar permisos
chown usuario:grupo archivo # Cambiar propietario
ls -lh                   # Ver permisos legibles
```

### 1.7. Red

```bash
ip a                     # Ver interfaces de red
ping google.com          # Hacer ping
curl ifconfig.me         # Obtener IP pública
netstat -tuln            # Ver puertos escuchando
ss -tunap                # Ver sockets abiertos
```

### 1.8. Scripting Básico

```bash
# Guardar como script.sh y hacer ejecutable con chmod +x script.sh
#!/bin/bash
echo "Hola desde WSL"
```

### 1.9. Interacción con Windows desde WSL

```bash
explorer.exe .             # Abrir carpeta actual en el explorador de Windows
notepad.exe archivo.txt    # Abrir archivo en el Bloc de notas
powershell.exe Get-Date    # Ejecutar comando PowerShell
```

### 1.10. Herramientas útiles para instalar

```bash
sudo apt install htop curl git vim net-tools unzip zip tree
```
