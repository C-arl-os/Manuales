# Manual de Administración de Sistemas Linux — LabEx

> Manual de referencia construido a partir del curso **"Conviértete en un Administrador de Sistemas Junior"** de LabEx.
> Simula los primeros días de un ingeniero junior: navegación del sistema, gestión de usuarios y protección de recursos.

---

## Tabla de Contenidos

- [Sobre este curso](#sobre-este-curso)
- [Cómo usar este manual](#cómo-usar-este-manual)
- [Labs](#labs)
  - [Lab 01 — Reconocimiento de Terreno](#lab-01--reconocimiento-de-terreno)
  - [Lab 02 — Arquitecto Digital](#lab-02--arquitecto-digital)
- [Referencia Rápida](#referencia-rápida)
- [Glosario](#glosario)

---

## Sobre este curso

**Nivel:** Principiante
**Enfoque:** Administración de sistemas Linux en escenarios del mundo real
**Prerequisito recomendado:** Fundamentos de Linux (comandos básicos de terminal, navegación, permisos)

### Qué cubre este curso

Al completar este curso serás capaz de:

- Navegar y gestionar sistemas de archivos complejos
- Administrar cuentas de usuario y grupos
- Controlar permisos y proteger recursos del sistema
- Realizar tareas típicas del día a día de un sysadmin junior

### Diferencia con el manual anterior

El manual de Linux (`02-Inicio-Linux`) cubre comandos individuales desde cero.
Este manual aplica esos conocimientos en **escenarios de administración reales**, donde varios comandos se combinan para resolver un problema concreto.

---

## Cómo usar este manual

Cada lab en este manual sigue la misma estructura:

- **Escenario** — el contexto profesional que simula el lab
- **Comandos nuevos** — lo que aparece por primera vez, con explicación y ejemplos
- **Flujo del lab** — cómo se conectan los pasos del lab entre sí
- **Errores comunes** — lo que puede salir mal y cómo leerlo
- **Ejercicio** — práctica independiente en KillerCoda o cualquier Linux

---

## Labs

---

### Lab 01 — Reconocimiento de Terreno

**Escenario:** Es tu primer día en LabEx Corporation. Antes de tocar cualquier cosa del servidor del Proyecto Phoenix, necesitas hacer un reconocimiento completo: saber quién eres en el sistema, qué versión de SO corre, cuánto tiempo lleva encendido y qué procesos están activos.

> En administración de sistemas, nunca modificas un servidor sin antes inspeccionarlo. Este paso se llama **reconocimiento de terreno** o *system reconnaissance*.

---

#### `uname` — Información del sistema operativo y kernel

**Sintaxis:**
```
uname [opciones]
uname -a    # toda la información disponible
```

**Qué hace:** Muestra información sobre el kernel y el sistema operativo.

**Ejemplo:**
```bash
$ uname -a
Linux 69c743b5a829da522a3fa421 5.4.0-162-generic #179-Ubuntu SMP Mon Aug 14 08:51:31 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
```

**Cómo leer la salida de `uname -a`:**

```
Linux  69c743b5a829da522a3fa421  5.4.0-162-generic  #179-Ubuntu SMP ...  x86_64  GNU/Linux
  │           │                        │                      │              │        │
  │           │                        │                      │              │        └─ sistema operativo
  │           │                        │                      │              └─ arquitectura del procesador
  │           │                        │                      └─ versión de compilación del kernel
  │           │                        └─ versión del kernel
  │           └─ nombre del host (hostname)
  └─ nombre del kernel
```

| Flag | Muestra |
|------|---------|
| `-s` | solo el nombre del kernel (`Linux`) |
| `-n` | hostname de la máquina |
| `-r` | versión del kernel (`5.4.0-162-generic`) |
| `-m` | arquitectura (`x86_64`) |
| `-a` | todo lo anterior junto |

> **¿Para qué sirve en producción?** Para confirmar que el servidor tiene el kernel y la arquitectura que espera el software que vas a instalar. Una aplicación de 64 bits no corre en un kernel de 32 bits.

---

#### `uptime` — Tiempo activo del servidor y carga del sistema

**Sintaxis:**
```
uptime
```

**Ejemplo:**
```bash
$ uptime
 11:05:45 up 522 days, 21:59,  0 users,  load average: 0.18, 0.17, 0.25
```

**Cómo leer la salida:**

```
11:05:45  up 522 days, 21:59,  0 users,  load average: 0.18, 0.17, 0.25
    │         │                   │                     │     │     │
    │         │                   │                     │     │     └─ promedio últimos 15 min
    │         │                   │                     │     └─ promedio últimos 5 min
    │         │                   │                     └─ promedio último 1 min
    │         │                   └─ usuarios conectados ahora
    │         └─ tiempo encendido: 522 días y 21 horas
    └─ hora actual del sistema
```

**Load average (carga promedio):**

Es la cantidad promedio de procesos que están esperando CPU. La referencia es el número de núcleos del procesador:

| Load average | Interpretación (en CPU de 1 núcleo) |
|-------------|--------------------------------------|
| `0.0 – 1.0` | Normal, el sistema tiene capacidad libre |
| `~1.0` | El CPU está al límite, sin margen |
| `> 1.0` | Hay procesos en cola esperando CPU — el sistema está sobrecargado |

> Un servidor que lleva **522 días encendido** sin reinicios es normal en Linux de producción. En Windows sería impensable. Esta estabilidad es una de las razones por las que Linux domina en servidores.

---

#### `who` — Ver quién está conectado al sistema

**Sintaxis:**
```
who
```

**Qué hace:** Lista los usuarios que tienen sesiones activas en este momento.

**Ejemplo (con usuarios conectados):**
```bash
$ who
labex    pts/0    2026-03-27 11:00 (192.168.1.10)
admin    pts/1    2026-03-27 10:45 (192.168.1.15)
```

**Columnas:**
- `labex` → nombre de usuario
- `pts/0` → terminal virtual donde está conectado
- fecha y hora → cuándo inició sesión
- `(IP)` → desde qué dirección se conectó

Si el servidor del lab no muestra usuarios es porque es un entorno de contenedor aislado.

> **En producción:** `who` es el primer comando para saber si hay otros admins trabajando antes de hacer cambios en el servidor.

---

#### `top` — Monitor de procesos en tiempo real

**Sintaxis:**
```
top
```

**Qué hace:** Abre una vista interactiva y en tiempo real de los procesos activos, uso de CPU, memoria y carga del sistema. Se actualiza cada 3 segundos.

**Salida del lab:**
```
top - 11:03:28 up 522 days, 21:56,  0 users,  load average: 0.13, 0.20, 0.28
MiB Mem :  15728.3 total,   7407.4 free,   3399.1 used,   4921.8 buff/cache
MiB Swap:      0.0 total,      0.0 free,      0.0 used.  11952.7 avail Mem

    PID USER      PR  NI    VIRT    RES    SHR S  %CPU  %MEM     TIME+ COMMAND
    222 labex     20   0   12540   3976   3140 S   0.0   0.0   0:00.03 tmux: server
    553 labex     20   0    7364   3604   3012 R   0.0   0.0   0:00.03 top
```

**Desglose del encabezado:**

```
MiB Mem: 15728.3 total,  7407.4 free,  3399.1 used,  4921.8 buff/cache
              │               │              │               │
              │               │              │               └─ usada por caché del SO (recuperable)
              │               │              └─ usada por procesos activos
              │               └─ disponible sin tocar caché
              └─ RAM total del sistema
```

**Desglose de las columnas de procesos:**

| Columna | Significado |
|---------|-------------|
| `PID` | Process ID — número único del proceso |
| `USER` | Usuario que lanzó el proceso |
| `PR` | Prioridad del proceso (menor = más prioritario) |
| `NI` | Nice value — ajuste manual de prioridad |
| `VIRT` | Memoria virtual total reservada por el proceso |
| `RES` | Memoria física real usada (la que importa) |
| `SHR` | Memoria compartida con otros procesos |
| `S` | Estado: `S`=durmiendo, `R`=ejecutando, `Z`=zombie |
| `%CPU` | Porcentaje de CPU usado en este momento |
| `%MEM` | Porcentaje de RAM usada |
| `TIME+` | Tiempo total de CPU consumido desde que inició |
| `COMMAND` | Nombre del programa |

**Teclas útiles dentro de `top`:**

| Tecla | Acción |
|-------|--------|
| `q` | Salir de top |
| `k` | Matar un proceso (pide el PID) |
| `M` | Ordenar por uso de memoria |
| `P` | Ordenar por uso de CPU |
| `1` | Mostrar cada núcleo de CPU por separado |
| `h` | Ayuda |

---

#### `>` y `>>` — Redirigir salida hacia un archivo

Ya los viste en el manual de Linux. Aquí se usan en un contexto profesional: **generar un reporte del sistema**.

| Operador | Comportamiento |
|----------|----------------|
| `>` | Crea el archivo (o sobreescribe si ya existe) |
| `>>` | Agrega al final del archivo sin borrar lo que hay |

**Flujo del lab — construir el reporte paso a paso:**

```bash
$ whoami > system_report.txt        # crea el archivo con el usuario
$ uname -a >> system_report.txt     # agrega info del SO
$ uptime >> system_report.txt       # agrega carga del sistema

$ cat system_report.txt
labex
Linux 69c743b5a829da522a3fa421 5.4.0-162-generic #179-Ubuntu SMP Mon Aug 14 08:51:31 UTC 2023 x86_64 x86_64 x86_64 GNU/Linux
 11:05:45 up 522 days, 21:59,  0 users,  load average: 0.18, 0.17, 0.25
```

> **Patrón profesional:** Usar `>` para el primer dato (crea el archivo limpio) y `>>` para todos los siguientes (acumula sin borrar). Si usas `>>` desde el inicio y el archivo ya existía de una corrida anterior, el reporte tendrá datos duplicados.

---

### Ejercicio — Lab 01

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux.

**Escenario:** Eres el nuevo sysadmin de una empresa. Tu primer tarea es generar un reporte de estado del servidor antes de la reunión del lunes.

**Tareas:**

1. Confirma con qué usuario estás trabajando.
2. Muestra la información completa del sistema operativo e identifica: nombre del kernel, versión, hostname y arquitectura.
3. Verifica cuánto tiempo lleva activo el servidor. ¿El load average es normal?
4. Comprueba si hay otros usuarios conectados al servidor ahora mismo.
5. Abre `top`, identifica qué proceso consume más RAM (ordena con `M`), luego sal con `q`.
6. Genera un archivo `reporte_lunes.txt` que contenga en este orden:
   - Tu nombre de usuario
   - Info del SO (`uname -a`)
   - Tiempo activo (`uptime`)
7. Verifica el contenido del reporte con `cat`.
8. Agrega una segunda ejecución de `uptime` al mismo archivo con `>>`. ¿Qué diferencia notas entre las dos líneas?

**Resultado esperado de `cat reporte_lunes.txt`:**
```
root
Linux hostname 5.x.x-generic ... x86_64 GNU/Linux
 HH:MM:SS up X days, HH:MM, N users, load average: X.XX, X.XX, X.XX
 HH:MM:SS up X days, HH:MM, N users, load average: X.XX, X.XX, X.XX
```

<details>
<summary>Ver solución</summary>

```bash
whoami
uname -a
uptime
who
top       # presiona M para ordenar por memoria, luego q para salir

whoami > reporte_lunes.txt
uname -a >> reporte_lunes.txt
uptime >> reporte_lunes.txt
cat reporte_lunes.txt
uptime >> reporte_lunes.txt   # segunda línea de uptime
cat reporte_lunes.txt         # ahora tiene 4 líneas
```

</details>

---

---

### Lab 02 — Arquitecto Digital

**Escenario:** Tu segundo día en LabEx Corporation. Necesitas explorar la estructura del Proyecto Phoenix para entender cómo está organizado, y luego hacer rotación de logs: comprimir los archivos de log antiguos en un archivo y eliminar los originales para liberar espacio.

> **Rotación de logs** es una tarea rutinaria de sysadmin: los logs acumulan espacio en disco. La práctica estándar es comprimir los antiguos y conservar solo los recientes activos.

---

#### `ls -RF` — Listar todo el árbol de directorios

**Sintaxis:**
```
ls -RF [directorio]
```

**Qué hace:** Combina dos flags:
- `-R` → recursivo: entra en todos los subdirectorios
- `-F` → añade un sufijo para indicar el tipo: `/` para directorios, `*` para ejecutables, `@` para enlaces simbólicos

**Ejemplo del lab:**
```bash
$ ls -RF
.:
config/  docs/  src/

./config:
config.json  config.json.bak

./docs:
README.md  shared_docs/

./docs/shared_docs:
api_spec.doc  team_guidelines.txt

./src:
main_app.py
```

**Cómo leerlo:**
- Cada bloque empieza con `./ruta:` — eso es el directorio que se está listando
- Los elementos con `/` al final son subdirectorios
- Los archivos sin sufijo son archivos normales

**Comparación de variantes:**
```bash
$ ls          # solo el directorio actual, sin detalles
$ ls -R       # recursivo, sin indicador de tipo
$ ls -RF      # recursivo + indicador de tipo (el más útil para mapear estructura)
$ ls -lR      # recursivo + detalles (permisos, tamaño, fecha)
```

> En producción usarás `ls -RF` o `tree` (si está instalado) para mapear rápidamente un proyecto desconocido antes de trabajar en él.

---

#### `tar` — Comprimir y empaquetar archivos

**Sintaxis:**
```
tar -czf nombre.tar.gz archivo1 archivo2 ...    # crear archivo comprimido
tar -xzf nombre.tar.gz                          # extraer archivo comprimido
tar -tzf nombre.tar.gz                          # listar contenido sin extraer
```

**Qué hace:** `tar` empaqueta uno o más archivos en uno solo. Con `-z` también los comprime usando gzip.

**Desglose de los flags:**

| Flag | Nombre | Qué hace |
|------|--------|----------|
| `-c` | create | crea un nuevo archivo tar |
| `-x` | extract | extrae el contenido |
| `-t` | list | lista el contenido sin extraer |
| `-z` | gzip | comprime/descomprime con gzip |
| `-f` | file | el siguiente argumento es el nombre del archivo |
| `-v` | verbose | muestra los archivos mientras los procesa |

> **Regla de memoria:** `-czf` = **C**rear + g**Z**ip + **F**ilename. Los flags siempre van en ese orden cuando creas un archivo.

**Flujo del lab — rotación de logs:**

**Primer intento (solo un archivo):**
```bash
$ tar -czf old_logs.tar.gz app_2023-01-15.log
$ ls
app_2023-01-15.log  app_2024-05-01.log  db_2023-02-20.log  old_logs.tar.gz
```

Se creó el `.tar.gz` pero faltó incluir `db_2023-02-20.log`. Se borró y se rehízo:

```bash
$ rm -rf old_logs.tar.gz     # borra el intento anterior
```

**Segundo intento (múltiples archivos):**
```bash
$ tar -czf old_logs.tar.gz app_2023-01-15.log db_2023-02-20.log
$ ls
app_2023-01-15.log  app_2024-05-01.log  db_2023-02-20.log  old_logs.tar.gz
```

Ahora el `.tar.gz` contiene ambos logs antiguos. Se verificó visualmente con `ls` antes de borrar los originales.

**Eliminar los originales (paso final de la rotación):**
```bash
$ rm -rf app_2023-01-15.log db_2023-02-20.log
$ ls
app_2024-05-01.log  old_logs.tar.gz
```

**Resultado:** el directorio quedó limpio — solo el log activo y el archivo histórico comprimido.

**Verificar el contenido de un tar sin extraer:**
```bash
$ tar -tzf old_logs.tar.gz
app_2023-01-15.log
db_2023-02-20.log
```

> **Buena práctica:** Siempre verifica con `tar -tzf` que el archivo contiene lo que esperas **antes** de borrar los originales. Borrar primero y verificar después es un error de sysadmin que puede costar caro.

**Extensiones de archivo comunes con tar:**

| Extensión | Qué es |
|-----------|--------|
| `.tar` | Solo empaquetado, sin compresión |
| `.tar.gz` o `.tgz` | Empaquetado + compresión gzip |
| `.tar.bz2` | Empaquetado + compresión bzip2 (más lento, más compacto) |
| `.tar.xz` | Empaquetado + compresión xz (la más compacta) |

---

### Ejercicio — Lab 02

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux.

**Escenario:** Entras a un servidor nuevo y necesitas primero mapear su estructura, luego archivar los logs del año pasado.

**Preparación:**
```bash
mkdir -p ~/lab02/{proyecto/{src,docs,config},logs}
touch ~/lab02/proyecto/src/app.py
touch ~/lab02/proyecto/docs/manual.md
touch ~/lab02/proyecto/config/settings.json
touch ~/lab02/logs/error_2024-01-10.log
touch ~/lab02/logs/access_2024-02-15.log
touch ~/lab02/logs/error_2025-03-01.log
cd ~/lab02
```

**Tareas:**

1. Mapea toda la estructura del directorio `lab02` con un solo comando (recursivo + tipo).
2. Lista solo el contenido de `proyecto/docs/` usando su ruta relativa.
3. Lista el contenido de `logs/` usando la ruta absoluta (`~/lab02/logs/`).
4. Entra al directorio `logs/`.
5. Comprime los dos logs de 2024 en un archivo llamado `logs_2024.tar.gz`.
6. Verifica el contenido del tar **sin extraerlo**.
7. Solo si el contenido es correcto, elimina los dos archivos originales de 2024.
8. Verifica el estado final del directorio.

**Estado final esperado en `logs/`:**
```
error_2025-03-01.log
logs_2024.tar.gz
```

<details>
<summary>Ver solución</summary>

```bash
ls -RF ~/lab02
ls proyecto/docs/
ls ~/lab02/logs/
cd ~/lab02/logs
tar -czf logs_2024.tar.gz error_2024-01-10.log access_2024-02-15.log
tar -tzf logs_2024.tar.gz     # verificar ANTES de borrar
rm error_2024-01-10.log access_2024-02-15.log
ls
```

</details>

---

## Referencia Rápida

| Comando | Descripción breve | Lab |
|---------|------------------|-----|
| `whoami` | Muestra el usuario actual | 01 |
| `uname -a` | Info completa del SO y kernel | 01 |
| `uptime` | Tiempo activo y carga del sistema | 01 |
| `who` | Lista usuarios con sesión activa | 01 |
| `top` | Monitor interactivo de procesos y recursos | 01 |
| `cmd > archivo` | Redirige salida a archivo (sobreescribe) | 01 |
| `cmd >> archivo` | Agrega salida al final de un archivo | 01 |
| `ls -RF` | Lista árbol completo con indicador de tipo | 02 |
| `tar -czf arch.tar.gz archivos` | Empaqueta y comprime archivos | 02 |
| `tar -tzf arch.tar.gz` | Lista contenido del tar sin extraer | 02 |
| `tar -xzf arch.tar.gz` | Extrae un archivo tar comprimido | 02 |

---

## Glosario

| Término | Definición |
|---------|-----------|
| **Sysadmin** | Administrador de sistemas — gestiona servidores, usuarios y recursos |
| **Root** | Superusuario con acceso total al sistema Linux |
| **Proceso** | Programa en ejecución — tiene un PID (Process ID) único |
| **Daemon** | Proceso que corre en segundo plano como servicio del sistema |
| **Servicio** | Programa que se inicia con el sistema y corre continuamente (ej. `sshd`, `nginx`) |
| **Log** | Registro de eventos del sistema — generalmente en `/var/log/` |
| **`/etc`** | Directorio de configuración del sistema |
| **`/var`** | Directorio de datos variables: logs, bases de datos, colas de correo |
| **`/proc`** | Sistema de archivos virtual con información en tiempo real del kernel |
| **Kernel** | Núcleo del SO — gestiona hardware, memoria y procesos |
| **PID** | Process ID — número único que identifica a un proceso en ejecución |
| **Load average** | Promedio de procesos esperando CPU — valores altos indican sobrecarga |
| **RAM buff/cache** | Memoria usada por el SO como caché — la libera si un proceso la necesita |
| **`pts/N`** | Terminal virtual (pseudo-terminal) — cada sesión SSH o terminal abre una |
| **Reconocimiento** | Primer paso del sysadmin: inspeccionar el sistema antes de modificarlo |
| **`tar`** | Tape Archive — herramienta para empaquetar y comprimir archivos |
| **`.tar.gz`** | Archivo empaquetado con tar y comprimido con gzip |
| **Rotación de logs** | Práctica de archivar logs antiguos y borrar originales para liberar disco |
| **`-czf`** | Flags de tar: Create + gZip + Filename (para crear un comprimido) |
| **`-tzf`** | Flags de tar: lisT + gZip + Filename (para ver contenido sin extraer) |

---

_Última actualización: 2026-03-26_
