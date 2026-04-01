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
  - [Lab 03 — Detective de Sistemas](#lab-03--detective-de-sistemas)
  - [Lab 04 — Guardián de la Fortaleza](#lab-04--guardián-de-la-fortaleza)
  - [Lab 05 — Guardián de las Llaves](#lab-05--guardián-de-las-llaves)
  - [Lab 06 — Gestión de Procesos](#lab-06--gestión-de-procesos)
  - [Lab 07 — El Portal Caído](#lab-07--el-portal-caído)
  - [Lab 08 — Mantenimiento del Sistema](#lab-08--mantenimiento-del-sistema)
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

---

### Lab 03 — Detective de Sistemas

**Escenario:** El Proyecto Phoenix está fallando en producción. Sarah Chen te pide que investigues los logs de error, compares las configuraciones de staging vs producción y encuentres archivos faltantes entre servidores. Tu trabajo es documentar todos los hallazgos.

> Este lab introduce el flujo de trabajo de **troubleshooting sistemático**: leer logs → filtrar errores → comparar configuraciones → documentar diferencias. Es la base del trabajo diario de un sysadmin.

---

#### `grep` — Filtrar líneas que coinciden con un patrón

**Sintaxis:**
```
grep "patrón" archivo
grep -i "patrón" archivo      # ignora mayúsculas/minúsculas
grep -n "patrón" archivo      # muestra número de línea
grep -r "patrón" directorio   # busca en todos los archivos recursivamente
grep -v "patrón" archivo      # muestra las líneas que NO coinciden
```

**Qué hace:** Busca líneas en un archivo que contengan el patrón indicado. Indispensable para analizar logs.

**Ejemplo — extraer solo los errores de un log:**
```bash
$ cat ~/project/error_report.txt
[2023-10-26 10:00:03] ERROR: Failed to process payment transaction #12345.
[2023-10-26 10:00:05] ERROR: NullPointerException at com.innovatech.Billing.process(Billing.java:101).
worker_processes 4;

$ grep "ERROR" ~/project/error_report.txt
[2023-10-26 10:00:03] ERROR: Failed to process payment transaction #12345.
[2023-10-26 10:00:05] ERROR: NullPointerException at com.innovatech.Billing.process(Billing.java:101).
```

`grep` filtró solo las líneas que contienen `"ERROR"`, descartando `worker_processes 4;`.

**Combinaciones frecuentes en logs:**
```bash
$ grep "ERROR" app.log              # solo errores
$ grep "ERROR\|WARN" app.log        # errores y advertencias
$ grep -i "error" app.log           # error, ERROR, Error...
$ grep -n "ERROR" app.log           # con número de línea
$ grep -c "ERROR" app.log           # cuántas líneas tienen ERROR (solo el conteo)
$ grep -v "INFO" app.log            # todo excepto las líneas INFO
```

> **En producción:** Los logs de aplicaciones tienen miles de líneas. `grep` te permite ir directo al problema en segundos sin leer todo el archivo.

---

#### `dmesg` — Mensajes del kernel y hardware

**Sintaxis:**
```
dmesg
dmesg | grep "patrón"    # filtrar mensajes específicos
dmesg | tail -20         # ver los últimos 20 mensajes
```

**Qué hace:** Muestra el buffer de mensajes del kernel — todo lo que el sistema operativo registró desde el arranque: detección de hardware, errores de dispositivos, eventos del sistema.

**Ejemplo de salida:**
```
[    0.000000] Linux version 5.4.0-162-generic
[    1.234567] ACPI: IRQ0 used by override.
[  522.891234] apparmor: AppArmor initialized
[ 1523.445678] comm="apparmor_parser"
```

**Cómo leer la salida:**
- `[segundos.microsegundos]` → tiempo desde el arranque del sistema
- El mensaje describe el evento del kernel

**Filtrar errores de hardware:**
```bash
$ dmesg | grep -i "error"
$ dmesg | grep -i "fail"
$ dmesg | grep -i "disk\|sda\|nvme"    # problemas de disco
```

> **Cuándo usarlo:** Cuando un servidor tiene comportamiento extraño (lentitud, procesos que mueren) y no hay errores en los logs de aplicación. Los problemas de hardware o kernel aparecen aquí.

---

#### `diff` en contexto profesional — Comparar configuraciones entre entornos

Ya conoces `diff` del manual de Linux. Aquí se usa para una tarea crítica de sysadmin: **detectar diferencias entre configuraciones de staging y producción**.

**El problema típico:**
> "La app funciona en staging pero falla en producción" → casi siempre hay una diferencia de configuración.

**Comparar dos archivos de configuración:**
```bash
$ diff ~/project/config/staging/app.conf ~/project/config/production/app.conf
1,5c1,5
< # Staging Configuration
< database.url=jdbc:mysql://staging-db:3306/nexus
< api.key=staging_key_abc123
< feature.flag.new_dashboard=true
< timeout.ms=3000
---
> # Production Configuration
> database.url=jdbc:mysql://prod-db:3306/nexus
> api.key=prod_key_xyz789
> feature.flag.new_dashboard=false
> timeout.ms=5000
```

**Interpretación de los hallazgos:**
- `database.url` → apunta a diferentes servidores de base de datos ✓ (esperado)
- `api.key` → claves distintas ✓ (esperado por seguridad)
- `feature.flag.new_dashboard=true` en staging vs `false` en producción → una feature nueva **no está activada en producción** — posible causa del fallo
- `timeout.ms=3000` vs `5000` → producción tiene mayor tolerancia de timeout

> Saber interpretar `diff` te permite identificar la causa raíz de un bug de entorno en segundos.

---

#### Guardar la salida de `diff` en un archivo

**Patrón:**
```
diff archivo1 archivo2 > reporte.txt
```

En lugar de mostrar las diferencias en pantalla, las guarda en un archivo para documentar y compartir.

```bash
$ diff ~/project/config/staging/app.conf ~/project/config/production/app.conf > ~/project/config_diff.txt
$ cat ~/project/config_diff.txt
1,5c1,5
< # Staging Configuration
...
```

> **En producción:** Generar reportes con `diff > archivo.txt` es la forma estándar de documentar hallazgos antes de reportarlos al equipo o abrir un ticket.

---

#### `diff` vs `diff -r` — Comparar directorios (revisitado)

En el Lab 03 del manual de Linux ya viste `diff -r`. Aquí se muestra la diferencia entre usarlo **sin** y **con** `-r` sobre directorios:

**Sin `-r` (no recursivo):**
```bash
$ diff server1_files server2_files > missing_files.txt
$ cat missing_files.txt
Only in server1_files: asset2.js
```

Solo detecta archivos en el nivel superior del directorio.

**Con `-r` (recursivo):**
```bash
$ diff -r server1_files server2_files > missing_files.txt
$ cat missing_files.txt
Only in server1_files: asset2.js
```

En este caso el resultado fue el mismo porque los directorios solo tenían un nivel. Pero si hubiera subdirectorios, `-r` los habría revisado también.

> **Regla:** En servidores de producción, siempre usa `diff -r` para comparar directorios. Sin `-r`, podrías perderte archivos faltantes en subdirectorios.

---

#### El flujo completo de troubleshooting

Este lab introduce el patrón que usarás en producción:

```
1. cat log.txt              → leer el log completo para entender el contexto
2. grep "ERROR" log.txt     → filtrar solo lo relevante
3. dmesg | grep "fail"      → revisar si hay problemas de hardware/kernel
4. diff staging prod        → comparar configuraciones entre entornos
5. diff -r servidor1 servidor2 → encontrar archivos faltantes
6. diff ... > reporte.txt   → documentar hallazgos para el equipo
```

---

### Ejercicio — Lab 03

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux.

**Escenario:** Recibes un reporte de que la app de pagos falla en producción. Debes investigar los logs y comparar las configuraciones.

**Preparación:**
```bash
mkdir -p ~/lab03/{logs,config/{staging,prod},servidores/{web1,web2}}

cat > ~/lab03/logs/app.log << 'EOF'
[2024-01-15 08:00:01] INFO: Server started on port 8080
[2024-01-15 08:01:22] INFO: User login: admin
[2024-01-15 08:02:45] ERROR: Database connection timeout
[2024-01-15 08:02:46] ERROR: Failed to process order #9981
[2024-01-15 08:03:10] WARN: Retry attempt 1 of 3
[2024-01-15 08:03:15] ERROR: Max retries exceeded, order failed
[2024-01-15 08:04:00] INFO: Health check OK
EOF

cat > ~/lab03/config/staging/app.conf << 'EOF'
db.host=staging-db
db.port=5432
debug=true
max_connections=10
timeout=3000
EOF

cat > ~/lab03/config/prod/app.conf << 'EOF'
db.host=prod-db
db.port=5432
debug=false
max_connections=50
timeout=3000
EOF

touch ~/lab03/servidores/web1/index.html ~/lab03/servidores/web1/styles.css ~/lab03/servidores/web1/deploy.sh
touch ~/lab03/servidores/web2/index.html ~/lab03/servidores/web2/styles.css
```

**Tareas:**

1. Lee el archivo de log completo con `cat`.
2. Filtra solo las líneas de `ERROR` del log.
3. Cuenta cuántas líneas de ERROR hay (usa `-c`).
4. Muestra todas las líneas que **no** sean `INFO`.
5. Compara las configuraciones de staging y producción. ¿Qué diferencias encuentras? ¿Alguna podría causar el fallo?
6. Guarda esa comparación en `~/lab03/config_diff.txt`.
7. Compara los directorios `web1` y `web2` para encontrar qué archivo falta en web2.
8. Guarda ese resultado en `~/lab03/archivos_faltantes.txt`.
9. Verifica ambos reportes con `cat`.

<details>
<summary>Ver solución</summary>

```bash
cat ~/lab03/logs/app.log
grep "ERROR" ~/lab03/logs/app.log
grep -c "ERROR" ~/lab03/logs/app.log
grep -v "INFO" ~/lab03/logs/app.log
diff ~/lab03/config/staging/app.conf ~/lab03/config/prod/app.conf
diff ~/lab03/config/staging/app.conf ~/lab03/config/prod/app.conf > ~/lab03/config_diff.txt
diff -r ~/lab03/servidores/web1 ~/lab03/servidores/web2
diff -r ~/lab03/servidores/web1 ~/lab03/servidores/web2 > ~/lab03/archivos_faltantes.txt
cat ~/lab03/config_diff.txt
cat ~/lab03/archivos_faltantes.txt
```

</details>

---

---

### Lab 04 — Guardián de la Fortaleza

**Escenario:** El CTO de TechNova te encarga asegurar el directorio del Proyecto Phoenix. Necesitas aplicar permisos precisos: proteger archivos sensibles, dar acceso controlado al equipo de desarrollo, y configurar el directorio `src` para que cualquier archivo creado dentro herede automáticamente el grupo del equipo.

> Este lab introduce los **bits de permiso especiales** de Linux — un nivel más allá de `rwx` estándar. El más importante para trabajo en equipo es el **setgid**.

---

#### Por qué `chmod` falló sin `sudo`

```bash
$ chmod -R 730 phoenix_project
chmod: changing permissions of 'phoenix_project': Operation not permitted
```

`chmod` solo puede cambiare los permisos de archivos que **te pertenecen**. El directorio `phoenix_project` pertenece a `dev_lead`, no a `labex`. Por eso se necesita `sudo`.

```bash
$ sudo chmod 730 phoenix_project    # ahora sí funciona
```

> **Regla:** Sin `sudo`, solo puedes modificar permisos de lo que tú creaste. Con `sudo`, actúas como root y puedes modificar cualquier cosa.

---

#### Repaso de permisos numéricos aplicados al lab

**Intento con `730`:**
```
7  3  0
│  │  └─ otros: --- (sin acceso)
│  └─ grupo: -wx (puede escribir y ejecutar, pero no leer) ← raro, casi nunca se usa
└─ dueño: rwx (acceso total)
```

`730` es inusual porque da al grupo escritura sin lectura. Se corrigió a `750`:

**Corrección con `750`:**
```
7  5  0
│  │  └─ otros: --- (sin acceso, correcto para datos privados)
│  └─ grupo: r-x (puede leer y entrar al directorio)
└─ dueño: rwx (acceso total)
```

```bash
$ sudo chmod 750 phoenix_project
$ ls -l
drwxr-x--- 4 dev_lead developers 53 Mar 29 12:44 phoenix_project
```

`750` es el permiso estándar para **directorios de proyecto privado de equipo**: el dueño tiene control total, el grupo puede trabajar, nadie más entra.

---

#### Los bits especiales de permisos

Además de `rwx`, Linux tiene tres bits especiales que se colocan **delante** del número de tres dígitos:

| Bit | Valor | Nombre | Se activa con |
|-----|-------|--------|---------------|
| setuid | 4 | Set User ID | `u+s` o `4xxx` |
| **setgid** | **2** | **Set Group ID** | **`g+s` o `2xxx`** |
| sticky | 1 | Sticky bit | `+t` o `1xxx` |

En este lab se usó el **setgid**.

---

#### `chmod g+s` / `chmod 2xxx` — El bit setgid

**¿Qué hace el setgid en un directorio?**

Normalmente, cuando un usuario crea un archivo, el archivo hereda el **grupo principal del usuario**. Con setgid activado en un directorio, todos los archivos nuevos creados dentro heredan el **grupo del directorio**, no el del usuario.

**Sin setgid:**
```
usuario labex (grupo principal: labex) crea archivo en src/
→ archivo queda con grupo: labex
```

**Con setgid en src/:**
```
usuario labex (grupo principal: labex) crea archivo en src/
→ archivo queda con grupo: developers  ← hereda el grupo del directorio
```

**Cómo se aplica:**

Con notación simbólica:
```bash
$ sudo chmod g+s phoenix_project/src
```

Con notación numérica (el `2` delante es el setgid):
```bash
$ sudo chmod 2770 phoenix_project/src
# 2 = setgid
# 7 = rwx para el dueño
# 7 = rwx para el grupo
# 0 = --- para otros
```

**Cómo reconocer el setgid en `ls -l`:**

```bash
$ ls -ld phoenix_project/src
drwxrws--- 2 dev_lead developers 6 Mar 29 12:40 phoenix_project/src
#      ^
#      └─ 's' minúscula en posición de ejecución del grupo = setgid activo + grupo tiene ejecución
```

| Lo que ves | Significado |
|-----------|-------------|
| `s` minúscula | setgid activo, el grupo **tiene** permiso de ejecución (`x`) |
| `S` mayúscula | setgid activo, el grupo **no tiene** permiso de ejecución (raro, casi siempre es un error) |

**Verificar que funciona — el archivo nuevo hereda el grupo:**
```bash
$ touch phoenix_project/src/test.txt
$ ls -l phoenix_project/src/test.txt
-rw-rw-r-- 1 labex developers 0 Mar 29 12:58 phoenix_project/src/test.txt
#                   ^^^^^^^^^^
#                   └─ grupo 'developers', no 'labex' — setgid funcionó
```

---

#### Por qué setgid es esencial en trabajo colaborativo

Sin setgid, en un directorio compartido por equipo:
- Ana crea `feature.py` → grupo: `ana` → Carlos no puede editarlo
- Carlos crea `utils.py` → grupo: `carlos` → Ana no puede editarlo
- El trabajo en equipo se fragmenta

Con setgid en el directorio:
- Ana crea `feature.py` → grupo: `developers` → Carlos puede editarlo
- Carlos crea `utils.py` → grupo: `developers` → Ana puede editarlo
- El equipo colabora sin fricción

> **Setgid en `src/` es el estándar** para directorios de código compartido en equipos Linux. Lo verás en casi todo servidor de desarrollo con múltiples usuarios.

---

#### Resumen de permisos aplicados al Proyecto Phoenix

| Archivo/Directorio | Permisos | Significado |
|-------------------|----------|-------------|
| `phoenix_project/` | `750` (`drwxr-x---`) | Dueño: control total. Grupo: leer+entrar. Otros: sin acceso |
| `phoenix_project/src/` | `2770` (`drwxrws---`) | Igual que arriba + setgid: nuevos archivos heredan grupo |
| `project_keys.txt` | `600` (`-rw-------`) | Solo el dueño puede leer/escribir. Nadie más ve nada |

---

### Ejercicio — Lab 04

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux con `sudo`.

**Escenario:** Configuras un servidor para el equipo de diseño. Hay un directorio compartido donde todos deben poder crear y editar archivos, y un directorio privado con credenciales que solo el líder puede ver.

**Preparación:**
```bash
sudo groupadd designers
sudo useradd -m -G designers alice
sudo useradd -m -G designers bob
mkdir -p ~/lab04/{compartido,privado}
touch ~/lab04/privado/api_credentials.txt
sudo chown -R alice:designers ~/lab04
```

**Tareas:**

1. Lista `~/lab04` con permisos detallados para ver el estado inicial.
2. Aplica `750` al directorio `lab04/` (dueño todo, grupo lee/entra, otros nada).
3. Aplica `700` a `privado/` (solo alice puede entrar).
4. Aplica `600` a `privado/api_credentials.txt` (solo alice lee/escribe).
5. Aplica `2770` a `compartido/` (equipo colabora + setgid).
6. Verifica con `ls -ld compartido/` — busca la `s` en la posición del grupo.
7. Cambia a alice con `su - alice`, entra a `compartido/` y crea `diseño.txt`.
8. Verifica con `ls -l compartido/diseño.txt` — ¿el grupo es `designers`?
9. Sal con `exit`.

**Resultado esperado:**
```
drwxrws--- alice designers compartido/   ← 's' indica setgid
-rw-rw---- alice designers diseño.txt    ← heredó el grupo automáticamente
drwx------ alice designers privado/
-rw------- alice designers api_credentials.txt
```

<details>
<summary>Ver solución</summary>

```bash
ls -la ~/lab04
sudo chmod 750 ~/lab04
sudo chmod 700 ~/lab04/privado
sudo chmod 600 ~/lab04/privado/api_credentials.txt
sudo chmod 2770 ~/lab04/compartido
ls -ld ~/lab04/compartido    # busca la 's'

su - alice
cd ~/lab04/compartido        # rutas variarán según tu sistema
touch diseño.txt
ls -l diseño.txt             # grupo debe ser 'designers'
exit
```

</details>

---

---

### Lab 05 — Guardián de las Llaves

**Escenario:** Última semana. El Proyecto Phoenix entra a su fase final. Necesitas incorporar a una desarrolladora senior nueva (`b.smith`), darle acceso al equipo, y bloquear la cuenta de un empleado que se va (`j.doe`) sin eliminar sus archivos, que el equipo legal necesita para una auditoría.

---

#### Convenciones de nombres de usuario

En entornos corporativos los usuarios no se llaman `labex` ni `bob`. El formato estándar es `inicial.apellido` o `nombre.apellido`:

```
b.smith   → Brenda Smith
j.doe     → John Doe
a.garcia  → Ana García
```

Linux acepta el punto `.` en nombres de usuario. No cambia nada técnico, solo sigue la convención de la empresa.

---

#### `useradd -m` — Crear usuario con directorio home

Ya lo conoces. Aquí el detalle importante es verificar que el home se creó:

```bash
$ sudo useradd -m b.smith
$ ls -la /home/
drwxr-x--- 2 b.smith b.smith 57 Mar 29  /home/b.smith
```

Cuando Linux crea el home con `-m`, lo llena automáticamente con archivos de configuración base:

```bash
$ sudo ls -la /home/b.smith/
.bash_logout
.bashrc
.profile
```

Estos archivos configuran el entorno del usuario cuando inicia sesión (variables de entorno, alias, mensaje de bienvenida, etc.).

---

#### `grep` con anclas `^` — Buscar exactamente al inicio de línea

**Sintaxis:**
```
grep "^patron" archivo
```

El símbolo `^` significa "inicio de línea". Úsalo cuando quieres encontrar una línea que **empieza** con ese texto, no que lo contiene en cualquier parte.

**Por qué importa en `/etc/passwd` y `/etc/shadow`:**

Sin ancla, `grep "j.doe"` también encontraría líneas como:
```
ajdoelen:x:1005:...
backupj.doe:x:1006:...
```

Con ancla `^`:
```bash
$ grep "^j.doe:" /etc/shadow
j.doe:!:20334:0:99999:7:::
```

Solo devuelve la línea que empieza exactamente con `j.doe:`.

> El `:` después del nombre también es importante. Sin él, `^j` encontraría tanto `j.doe` como `j.smith`.

---

#### `passwd` — Administrar contraseñas (revisitado)

Ya viste `passwd` en el manual de Linux. El punto clave aquí:

```bash
$ passwd b.smith
passwd: You may not view or modify password information for b.smith.

$ sudo passwd b.smith
New password:
Retype new password:
passwd: password updated successfully
```

`passwd` sin `sudo` solo funciona para cambiar **tu propia contraseña**. Para cambiar la de otro usuario, siempre se necesita `sudo`.

---

#### `usermod -aG` — Agregar al grupo sin romper membresías

Ya lo viste en el Lab 05 del manual de Linux. Aquí el recordatorio en contexto corporativo:

```bash
$ sudo usermod -aG developers b.smith
$ groups b.smith
b.smith : b.smith developers
```

**La diferencia crítica:**

```bash
$ sudo usermod -G developers b.smith    # PELIGROSO: reemplaza TODOS los grupos
$ sudo usermod -aG developers b.smith   # CORRECTO: agrega sin tocar los demás
```

Si `b.smith` ya era miembro de `sudo` o `docker` y usas `-G` sin `-a`, pierde esos grupos al instante. En producción esto puede dejar a un usuario sin acceso a herramientas críticas.

---

#### `usermod -L` — Bloquear una cuenta

**Sintaxis:**
```
sudo usermod -L usuario
sudo passwd -l usuario    # alternativa equivalente
```

Ambos hacen lo mismo: ponen un `!` al inicio del hash en `/etc/shadow`.

```bash
$ sudo usermod -L j.doe
```

**Verificar que la cuenta está bloqueada:**
```bash
$ sudo grep "^j.doe:" /etc/shadow
j.doe:!$y$j9T$...:20334:0:99999:7:::
       ^
       └─ el '!' indica cuenta bloqueada
```

**Lo que hace el `!` internamente:**
- El hash original sigue ahí, intacto, después del `!`
- Linux detecta el `!` al inicio y rechaza cualquier intento de autenticación
- Si se desbloquea con `usermod -U` o `passwd -u`, el `!` se quita y la contraseña vuelve a funcionar

> Bloquear en lugar de eliminar es la práctica correcta cuando hay auditorías pendientes. Los archivos, logs y permisos del usuario se conservan para revisión legal o forense.

---

#### Errores frecuentes en este lab

**Crear usuario sin `-m` y darse cuenta después:**

Opciones:

```bash
# Opción 1: eliminar y recrear correctamente
sudo userdel b.smith
sudo useradd -m b.smith

# Opción 2: crear el home manualmente (más avanzado)
sudo mkdir /home/b.smith
sudo chown b.smith:b.smith /home/b.smith
sudo chmod 750 /home/b.smith
```

**`grep` sin ancla devuelve resultados inesperados:**

```bash
sudo grep "j.doe" /etc/shadow
# podría devolver: ajdoe_backup, old_j.doe, etc.

sudo grep "^j.doe:" /etc/shadow
# exacto: solo la cuenta j.doe
```

**`usermod -G` sin `-a` (el error más peligroso de este lab):**

Si ejecutas `usermod -G developers b.smith` sin la `-a`, b.smith queda solo en `developers` y pierde todos sus demás grupos. Para corregir hay que agregarlos uno a uno de nuevo.

---

### Ejercicio — Lab 05

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux con `sudo`.

**Escenario:** Primer día como sysadmin en una empresa nueva. Debes incorporar a dos desarrolladores, darles acceso al grupo del proyecto, y bloquear la cuenta de alguien que ya no trabaja ahí.

**Preparación:**
```bash
sudo groupadd dev_team
sudo useradd -m j.williams
sudo passwd j.williams    # establece contraseña: password123
sudo usermod -aG dev_team j.williams
```

**Tareas:**

1. Crea el usuario `m.torres` con directorio home.
2. Verifica que aparece en `/etc/passwd` buscando exactamente `^m.torres:`.
3. Verifica que su home fue creado en `/home/`.
4. Establece una contraseña para `m.torres` (necesitas `sudo`).
5. Agrégalo al grupo `dev_team` sin eliminar sus grupos actuales.
6. Verifica sus grupos con `groups m.torres`.
7. Confirma con `id m.torres` que aparece el GID de `dev_team`.
8. Bloquea la cuenta de `j.williams` (se fue de la empresa).
9. Verifica en `/etc/shadow` que el `!` aparece al inicio del hash de `j.williams`.
10. Confirma que `m.torres` sigue activo (sin `!` en su hash).

<details>
<summary>Ver solución</summary>

```bash
sudo useradd -m m.torres
sudo grep "^m.torres:" /etc/passwd
ls -la /home/ | grep m.torres
sudo passwd m.torres
sudo usermod -aG dev_team m.torres
groups m.torres
id m.torres
sudo usermod -L j.williams
sudo grep "^j.williams:" /etc/shadow
sudo grep "^m.torres:" /etc/shadow
```

</details>

---

---

### Lab 06 — Gestión de Procesos

**Escenario:** El servidor del Proyecto Phoenix está lento. El load average en `top` muestra 1.14 con una CPU al 100% consumida por `resource_hog.sh`. Necesitas identificar el proceso, terminarlo, y luego lanzar una tarea legítima en segundo plano que siga corriendo aunque cierres la sesión.

---

#### `ps` — Listar procesos en ejecución

**Sintaxis:**
```
ps              # procesos de tu terminal actual
ps -x           # todos tus procesos, con o sin terminal
ps -u           # tus procesos con %CPU y %MEM
ps aux          # TODOS los procesos del sistema (el más usado)
ps -p PID -o columnas   # info específica de un PID
```

**`ps` básico — solo tu terminal:**
```bash
$ ps
    PID TTY          TIME CMD
    338 pts/2    00:00:00 script
    407 pts/3    00:00:00 ps
```

Muestra solo los procesos conectados a tu terminal actual. Útil para ver qué corre en esta sesión.

---

**`ps -x` — todos tus procesos:**
```bash
$ ps -x
    PID TTY      STAT   TIME COMMAND
     24 ?        Ss     0:00 /usr/bin/perl /usr/bin/vncserver ...
    201 ?        R      1:42 /bin/bash /home/labex/project/resource_hog.sh
    202 ?        S      0:00 /bin/bash /home/labex/project/critical_service.sh
```

La `?` en TTY significa que el proceso no está conectado a ninguna terminal — corre en segundo plano.

**La columna STAT — estado del proceso:**

| Estado | Significado |
|--------|-------------|
| `R` | Running — ejecutando activamente en CPU |
| `S` | Sleeping — dormido, esperando algo |
| `D` | Uninterruptible sleep — esperando I/O de disco |
| `Z` | Zombie — terminó pero el padre no lo recogió |
| `T` | Stopped — pausado con Ctrl+Z |
| `s` | Session leader — líder de una sesión de procesos |
| `l` | Multi-threaded |
| `+` | En el grupo de procesos del foreground |
| `N` | Baja prioridad (nice) |

---

**`ps -u` — procesos con uso de recursos:**
```bash
$ ps -u
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
labex        232  0.6  0.0   7632  6068 pts/1    Ss   11:16   0:00 -zsh
labex        338  0.0  0.0   2800  1124 pts/2    R+   11:16   0:00 script
```

Agrega las columnas `%CPU`, `%MEM`, `VSZ` (memoria virtual) y `RSS` (memoria física real usada).

---

**`ps aux` — todos los procesos del sistema:**
```bash
$ ps aux
USER         PID %CPU %MEM    VSZ   RSS TTY      STAT START   TIME COMMAND
root           1  0.0  0.0  11204  3828 ?        Ss   11:00   0:00 init.sh
labex        201  100  0.0   4356  1524 ?        R    11:16   4:29 resource_hog.sh
labex        202  0.0  0.0   4200  1100 ?        S    11:16   0:00 critical_service.sh
```

`aux` combina:
- `a` → procesos de todos los usuarios
- `u` → formato con usuario y recursos
- `x` → incluye procesos sin terminal

> `ps aux` es el comando más usado en producción para ver el estado completo del sistema en un momento dado.

---

**`ps -p PID -o` — información específica de un proceso:**
```bash
$ ps -p 201 -o pid,ppid,cmd
    PID    PPID CMD
    201       1 /bin/bash /home/labex/project/resource_hog.sh
```

`-o` permite elegir exactamente qué columnas mostrar. Aquí:
- `pid` → ID del proceso
- `ppid` → ID del proceso padre (quién lo lanzó)
- `cmd` → comando completo con ruta

---

#### `pgrep` — Encontrar PID por nombre

**Sintaxis:**
```
pgrep nombre_proceso
pgrep -f "patrón en línea completa"
```

**Qué hace:** Busca procesos por nombre y devuelve solo el PID. Más directo que `ps aux | grep`.

```bash
$ pgrep resource_hog.sh
201
```

**Con `-f` — busca en la línea de comando completa:**
```bash
$ pgrep -f "resource_hog"
201
```

Útil cuando el nombre del proceso es un script largo o cuando el nombre exacto no coincide con lo que muestra `ps`.

**Error del lab — nombre incorrecto:**
```bash
$ pgrep critical_services.sh
           ← sin salida: el proceso se llama critical_service.sh (sin 's')
```

Si `pgrep` no devuelve nada, el proceso no existe o el nombre está mal escrito. Verifica con `ps aux | grep nombre`.

---

#### `pkill` — Terminar procesos por nombre

**Sintaxis:**
```
pkill nombre_proceso
pkill -9 nombre_proceso    # forzado, sin posibilidad de limpieza
pkill -f "patrón"          # por línea de comando completa
```

**Qué hace:** Envía una señal de terminación a todos los procesos que coincidan con el nombre.

```bash
$ pkill resource_hog.sh
```

El proceso desaparece. `top` mostrará que el CPU vuelve a niveles normales.

**Señales principales:**

| Señal | Número | Comportamiento |
|-------|--------|----------------|
| `SIGTERM` | 15 | Pide al proceso que termine limpiamente (por defecto) |
| `SIGKILL` | 9 | Mata el proceso inmediatamente, sin limpieza |
| `SIGHUP` | 1 | Recarga la configuración (en daemons) |

> Usar siempre `SIGTERM` primero. Si el proceso no responde, entonces `SIGKILL` con `-9`. Matar con `-9` directamente puede dejar archivos a medias o corromper datos.

**Diferencia entre `pkill` y `kill`:**

| Comando | Forma de identificar el proceso |
|---------|--------------------------------|
| `kill PID` | Por número de proceso |
| `pkill nombre` | Por nombre (afecta a todos los que coincidan) |

---

#### `nohup` y `&` — Ejecutar en segundo plano

**Sintaxis:**
```
comando &                              # segundo plano, muere si cierras sesión
nohup comando &                        # segundo plano + sobrevive al cierre de sesión
nohup comando > salida.log 2>&1 &      # mismo + guarda toda la salida en archivo
```

**El problema sin `nohup`:**
Cuando cierras una sesión SSH o terminal, Linux envía la señal `SIGHUP` a todos sus procesos hijo. Eso los mata. Si lanzaste un proceso largo con solo `&`, muere al cerrar sesión.

**`nohup` ignora esa señal**, permitiendo que el proceso siga corriendo.

**El operador `&` — lanzar en background:**
```bash
$ ./data_processor.sh &
[1] 796
```

El `[1]` es el número de job, `796` es el PID. El proceso corre en paralelo y el prompt vuelve inmediatamente.

**La combinación completa del lab:**
```bash
$ nohup ./data_processor.sh > processor.log 2>&1 &
[1] 796
```

Desglose:
```
nohup                   → ignora SIGHUP (sobrevive al cierre de sesión)
./data_processor.sh     → el script a ejecutar
> processor.log         → redirige stdout (salida normal) al archivo
2>&1                    → redirige stderr (errores) al mismo lugar que stdout
&                       → lanza en segundo plano
```

**Verificar que terminó y leer su salida:**
```bash
$ cat processor.log
nohup: ignoring input
Starting data processing at Mon Mar 30 11:27:38 CST 2026
Data processing complete at Mon Mar 30 11:27:43 CST 2026
```

La línea `nohup: ignoring input` es normal — indica que nohup cortó la entrada estándar del proceso.

**Verificar si el proceso sigue corriendo:**
```bash
$ ps aux | grep data_processor
labex  823  0.0  0.0  grep data_processor    ← solo el grep, el proceso ya terminó
```

Si aparece solo la línea del `grep`, el proceso ya terminó. Si hay otra línea con el script, aún está corriendo.

---

#### `top` para identificar el proceso culpable

Ya conoces `top` del Lab 01. En este lab se usa activamente para diagnosticar:

```
%Cpu(s): 42.0 us,  1.3 sy,  56.6 id
    201 labex  20  0  4356  1524  1364 R  100.0  0.0  4:29.65 resource_hog.sh
```

- `42.0 us` → 42% de CPU usada por procesos de usuario (anormal si debería estar libre)
- El proceso PID 201 está al `100.0` %CPU con estado `R` (running)
- `4:29.65` en TIME+ → lleva más de 4 minutos consumiendo CPU continuo

Flujo de diagnóstico:
1. `top` → identifica que hay un proceso al 100% CPU
2. `pgrep nombre` → confirma el PID
3. `ps -p PID -o pid,ppid,cmd` → verifica qué es exactamente y quién lo lanzó
4. `pkill nombre` → lo termina
5. `top` de nuevo → confirma que el CPU bajó

---

#### Errores frecuentes en este lab

**`pgrep` sin resultado no significa error del comando:**
El proceso puede que no exista, ya terminó, o el nombre tiene un typo. Verificar siempre con `ps aux | grep nombre` antes de concluir que no existe.

**Usar `pkill` con nombre genérico:**
```bash
pkill bash    # mata TODOS los procesos bash del usuario, incluyendo tu propia sesión
```
Antes de `pkill`, confirmar con `pgrep` exactamente qué procesos coinciden.

**`ps aux | grep proceso` siempre incluye el grep en los resultados:**
```bash
$ ps aux | grep resource_hog
labex  658  0.0  grep resource_hog    ← esta línea es el grep mismo, no el proceso
```
Si solo ves la línea del `grep`, el proceso no está corriendo.

**`nohup` sin `2>&1` pierde los errores:**
Si el script falla, los errores van a `nohup.out` (archivo por defecto) en lugar del log que especificaste. Siempre agregar `2>&1` para capturar todo en un solo lugar.

---

### Ejercicio — Lab 06

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux.

**Preparación:**
```bash
# Crea un proceso que consuma CPU (se detiene solo en 60 segundos)
cat > /tmp/cpu_hog.sh << 'EOF'
#!/bin/bash
end=$((SECONDS+60))
while [ $SECONDS -lt $end ]; do :; done
echo "cpu_hog terminó"
EOF
chmod +x /tmp/cpu_hog.sh

# Crea una tarea larga
cat > /tmp/tarea_larga.sh << 'EOF'
#!/bin/bash
echo "Iniciando tarea $(date)"
sleep 10
echo "Tarea completada $(date)"
EOF
chmod +x /tmp/tarea_larga.sh

# Lanza el cpu_hog en segundo plano
/tmp/cpu_hog.sh &
```

**Tareas:**

1. Usa `ps aux` para encontrar el proceso `cpu_hog.sh` y anota su PID.
2. Usa `pgrep` para obtener el PID directamente por nombre.
3. Usa `ps -p PID -o pid,ppid,%cpu,cmd` para ver su info detallada.
4. Abre `top`, verifica que aparece consumiendo CPU (ordena con `P`), luego sal con `q`.
5. Termina el proceso con `pkill`.
6. Confirma con `pgrep` que ya no existe.
7. Lanza `tarea_larga.sh` en segundo plano con `nohup`, redirigiendo toda la salida a `/tmp/tarea.log`.
8. Verifica con `ps aux | grep tarea_larga` que está corriendo.
9. Espera que termine (`sleep 12`) y lee el resultado con `cat /tmp/tarea.log`.

<details>
<summary>Ver solución</summary>

```bash
ps aux | grep cpu_hog
pgrep cpu_hog.sh
ps -p $(pgrep cpu_hog.sh) -o pid,ppid,%cpu,cmd
top     # presiona P para ordenar por CPU, luego q
pkill cpu_hog.sh
pgrep cpu_hog.sh    # sin salida = terminado

nohup /tmp/tarea_larga.sh > /tmp/tarea.log 2>&1 &
ps aux | grep tarea_larga
sleep 12
cat /tmp/tarea.log
```

</details>

---

### Lab 07 — El Portal Caído

**Escenario:** El portal interno de la empresa dejó de responder. Los usuarios no pueden acceder y tu manager te asigna la tarea urgente. Nadie sabe si es un problema de red, de firewall o del servicio mismo. Tienes que diagnosticar paso a paso: primero las interfaces, luego la conectividad, después los puertos abiertos, y finalmente las reglas del firewall.

> Este es el flujo de diagnóstico de red que todo sysadmin junior ejecuta cuando llega el ticket "el servicio no responde". En la mayoría de los casos, la causa está en uno de estos cuatro niveles.

---

#### `ip addr` — Ver las interfaces de red y sus direcciones IP

**Sintaxis:**
```
ip addr
ip addr show
ip addr show eth0    # solo una interfaz específica
```

**Qué hace:** Muestra todas las interfaces de red del sistema con sus direcciones IP, máscaras de subred, direcciones MAC y estado (UP/DOWN).

**Ejemplo del lab:**
```
ip addr
```
```
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 ...
    inet 127.0.0.1/8 scope host lo
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 ...
    inet 172.16.50.197/24 ... scope global dynamic eth0
3: docker0: <NO-CARRIER,...,UP> mtu 1500 ...
    inet 172.17.0.1/16 ... scope global docker0
```

**Cómo leer la salida:**

| Campo | Qué significa |
|-------|--------------|
| `lo` | Loopback — interfaz virtual interna, siempre `127.0.0.1` |
| `eth0` | Interfaz Ethernet principal — la que conecta al mundo exterior |
| `docker0` | Interfaz virtual de Docker — crea su propia red interna |
| `UP` / `DOWN` | Estado de la interfaz. Si `eth0` está `DOWN`, no hay red |
| `inet 172.16.50.197/24` | Dirección IPv4 y máscara de subred (`/24` = 255.255.255.0) |
| `NO-CARRIER` | Cable no conectado o interfaz sin tráfico real |

> `ip addr` es la versión moderna de `ifconfig`. En sistemas nuevos, `ip` es la herramienta oficial del kernel — más detallada y siempre disponible.

---

#### `ifconfig` — Vista clásica de interfaces de red

**Sintaxis:**
```
ifconfig               # todas las interfaces activas
ifconfig eth0          # solo una interfaz
```

**Qué hace:** Muestra la configuración de las interfaces de red. Herramienta clásica (del paquete `net-tools`), equivalente a `ip addr` pero con formato diferente.

**Ejemplo del lab:**
```
ifconfig
```
```
eth0: flags=4163<UP,BROADCAST,RUNNING,MULTICAST>  mtu 1500
      inet 172.16.50.197  netmask 255.255.255.0  broadcast 172.16.50.255
      RX packets 20952  bytes 28650863 (28.6 MB)
      TX packets 3122   bytes 2169499 (2.1 MB)

lo:   flags=73<UP,LOOPBACK,RUNNING>  mtu 65536
      inet 127.0.0.1  netmask 255.0.0.0
```

**Diferencia práctica con `ip addr`:**

| `ip addr` | `ifconfig` |
|-----------|-----------|
| Moderno, del kernel | Clásico, del paquete `net-tools` |
| Disponible en todo Linux reciente | Puede no estar instalado por defecto |
| Muestra más detalles de IPv6 y enrutamiento | Formato más legible para lectura rápida |
| `inet 172.x.x.x/24` | `inet 172.x.x.x  netmask 255.255.255.0` |

> Ambos muestran la misma información esencial. En producción, `ip` es el estándar actual.

---

#### `ping` — Probar conectividad con otro host

**Sintaxis:**
```
ping destino
ping -c N destino    # envía exactamente N paquetes y termina
```

**Qué hace:** Envía paquetes ICMP al destino y espera respuesta. Sirve para verificar que hay conexión a un host y medir la latencia (tiempo de ida y vuelta).

**Ejemplo del lab:**
```
ping -c 3 8.8.8.8
```
```
PING 8.8.8.8 (8.8.8.8) 56(84) bytes of data.
64 bytes from 8.8.8.8: icmp_seq=1 ttl=118 time=1.47 ms
64 bytes from 8.8.8.8: icmp_seq=2 ttl=118 time=1.46 ms
64 bytes from 8.8.8.8: icmp_seq=3 ttl=118 time=1.44 ms

--- 8.8.8.8 ping statistics ---
3 packets transmitted, 3 received, 0% packet loss, time 2003ms
rtt min/avg/max/mdev = 1.438/1.455/1.467/0.012 ms
```

**Cómo leer la estadística final:**

| Campo | Qué indica |
|-------|-----------|
| `3 packets transmitted, 3 received` | No hay pérdida — hay conexión estable |
| `0% packet loss` | Ningún paquete se perdió en tránsito |
| `time=1.47 ms` | Latencia: 1.47 milisegundos — excelente |
| `rtt min/avg/max/mdev` | Tiempos mínimo, promedio, máximo y desviación |

> Sin `-c`, `ping` corre indefinidamente. En un diagnóstico, `-c 3` o `-c 4` es suficiente para confirmar conectividad. Para detener un ping sin `-c`, usa `Ctrl+C`.

> `8.8.8.8` es el servidor DNS público de Google — se usa frecuentemente en pruebas porque casi siempre responde ping desde cualquier red con acceso a internet.

---

#### `ss` — Inspeccionar puertos y conexiones de red

**Sintaxis:**
```
ss              # conexiones activas (resumen)
ss -t           # solo conexiones TCP establecidas
ss -l           # solo puertos en escucha (listening)
ss -n           # sin resolver nombres, muestra números
ss -p           # muestra el proceso dueño de cada socket
ss -tlnp        # combinado: TCP + listening + numérico + proceso
```

**Qué hace:** Muestra el estado de los sockets de red del sistema: qué puertos están escuchando, qué conexiones están activas y qué proceso es responsable de cada uno. Es el reemplazo moderno de `netstat`.

**Ejemplo del lab — conexiones TCP activas:**
```
ss -t
```
```
State    Recv-Q  Send-Q  Local Address:Port       Peer Address:Port
ESTAB    0       0       172.16.50.197:ssh         47.251.15.187:51614
ESTAB    0       0       172.16.50.197:3002        172.16.50.251:53496
```

**Ejemplo del lab — puertos en escucha con proceso:**
```
ss -tlnp
```
```
State   Recv-Q  Send-Q  Local Address:Port  Peer Address:Port  Process
LISTEN  0       5             0.0.0.0:8000        0.0.0.0:*    ("python3",pid=3262)
LISTEN  0       128           0.0.0.0:22          0.0.0.0:*
LISTEN  0       511           0.0.0.0:3000        0.0.0.0:*    ("node",pid=2089)
LISTEN  0       128           0.0.0.0:3002        0.0.0.0:*    ("ttyd",pid=897)
```

**Flags de `ss` explicados:**

| Flag | Nombre | Qué hace |
|------|--------|---------|
| `-t` | TCP | Solo muestra sockets TCP |
| `-l` | Listening | Solo muestra puertos en escucha |
| `-n` | Numeric | No resuelve nombres: muestra `22` en vez de `ssh`, IPs en vez de hostnames |
| `-p` | Process | Muestra qué proceso tiene abierto ese socket |
| `-u` | UDP | Solo muestra sockets UDP |

**Combinación más útil para diagnóstico:**
```
ss -tlnp
```
> Esto responde la pregunta crítica: **¿qué procesos están escuchando en qué puertos?** Si el portal debería estar en el puerto 8000 y no aparece aquí, el servicio no está corriendo.

**Filtrar un puerto específico:**
```
ss -tlnp | grep 8000
```
```
LISTEN  0  5  0.0.0.0:8000  0.0.0.0:*  users:(("python3",pid=3262,fd=3))
```

> Aquí descubrimos que el portal estaba escuchando en el puerto 8000, pero estaba bloqueado por el firewall. El servicio correría — el problema era `ufw`.

---

#### `ufw` — Firewall de Ubuntu/Debian (Uncomplicated Firewall)

**Sintaxis:**
```
sudo ufw status           # ver estado y reglas actuales
sudo ufw enable           # activar el firewall
sudo ufw disable          # desactivar el firewall
sudo ufw allow PUERTO     # permitir tráfico en ese puerto
sudo ufw deny PUERTO      # bloquear tráfico en ese puerto
sudo ufw status numbered  # ver reglas con número para poder borrarlas
sudo ufw delete N         # eliminar regla número N
```

**Qué hace:** Administra las reglas del firewall del sistema. Determina qué conexiones entrantes o salientes se permiten o bloquean. Un firewall mal configurado puede dejar servicios inaccesibles aunque estén corriendo correctamente.

**Flujo del lab — diagnóstico y corrección del firewall:**
```bash
# El portal estaba escuchando en 8000 pero era inaccesible
# Primero bloqueamos el puerto incorrecto que estaba sin protección
sudo ufw deny 8000

# Aseguramos que SSH siga accesible antes de activar el firewall
sudo ufw allow ssh

# Activamos el firewall
sudo ufw enable
```
```
Rules updated
Rules updated (v6)
Firewall is active and enabled on system startup
```

> En el lab, el problema era que el firewall no estaba activo (`ufw` desactivado), por lo que cualquier puerto quedaba expuesto. Al activarlo con las reglas correctas, el portal quedó protegido y accesible solo donde correspondía.

**Reglas comunes de referencia:**

| Comando | Efecto |
|---------|--------|
| `sudo ufw allow ssh` | Permite SSH (puerto 22) — siempre hacer esto **antes** de `enable` |
| `sudo ufw allow 80` | Permite tráfico HTTP |
| `sudo ufw allow 443` | Permite tráfico HTTPS |
| `sudo ufw deny 8000` | Bloquea el puerto 8000 |
| `sudo ufw status` | Muestra si el firewall está activo y qué reglas tiene |

> **Regla de oro:** Antes de ejecutar `sudo ufw enable`, siempre agrega `sudo ufw allow ssh`. Si activas el firewall sin esa regla y estás conectado por SSH, pierdes el acceso inmediatamente.

---

#### Flujo de diagnóstico de red

Cuando recibes el ticket "el servicio no responde", este es el orden de investigación:

```
1. ip addr              → ¿Las interfaces están UP? ¿Tenemos IP?
        ↓
2. ping -c 3 8.8.8.8   → ¿Hay conectividad hacia afuera?
        ↓
3. ss -tlnp             → ¿El servicio está escuchando en su puerto?
        ↓
4. ss -tlnp | grep PUERTO  → ¿Qué proceso ocupa ese puerto?
        ↓
5. sudo ufw status      → ¿El firewall permite o bloquea ese puerto?
```

Si el servicio aparece en `ss -tlnp` pero no responde externamente, el problema casi siempre está en el firewall. Si no aparece, el servicio no está corriendo.

---

#### Errores frecuentes — Lab 07

**`sudo ufw enable` sin permitir SSH antes**

Si activas `ufw` sin agregar la regla `allow ssh`, el firewall bloquea inmediatamente todas las conexiones SSH entrantes. Si estás en una sesión remota, pierdes el acceso en ese instante. La única recuperación es acceso físico a la máquina o consola de emergencia (como la consola de EC2 en AWS o acceso VNC).

**Interpretar `NO-CARRIER` como error de configuración**

`NO-CARRIER` en `ip addr` significa que la interfaz está activa en el SO pero no hay señal física (cable desconectado o interfaz virtual sin tráfico). Para `docker0` es completamente normal cuando no hay contenedores corriendo — no es un problema.

**Confundir `ss -l` con `ss -t`**

`ss -l` muestra los puertos que están *esperando conexiones* (modo servidor). `ss -t` muestra las conexiones *ya establecidas* (modo cliente activo). Para diagnóstico de servicios, siempre empieza con `ss -tlnp` — combina ambos enfoques con información del proceso responsable.

**Usar `ping` sin `-c` en un script**

Sin `-c N`, `ping` corre infinitamente. En un script de diagnóstico automatizado, un `ping` sin límite bloquea todo lo que sigue. Siempre especifica `-c 3` o `-c 4` cuando usas ping en scripts o en diagnósticos con pasos subsiguientes.

---

#### Ejercicio — Lab 07

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux con acceso sudo.

**Preparación:**

Ejecuta esto para simular el entorno del lab:
```bash
# Instala herramientas necesarias
sudo apt-get update -q && sudo apt-get install -y net-tools ufw python3

# Lanza un servidor simple en el puerto 8080
python3 -m http.server 8080 &
SERVER_PID=$!
echo "Servidor iniciado con PID $SERVER_PID en puerto 8080"
```

**Tareas:**

1. Usa `ip addr` para identificar tus interfaces de red. Anota la dirección IP de la interfaz principal (no `lo`).
2. Usa `ifconfig` y compara la salida con `ip addr` — ¿muestran la misma IP?
3. Usa `ping -c 3 8.8.8.8` para verificar conectividad externa. ¿Cuál fue el tiempo promedio (`avg`)?
4. Usa `ss -tlnp` para ver todos los puertos en escucha. ¿En qué puerto está corriendo `python3`?
5. Filtra con `ss -tlnp | grep 8080` para confirmar que es el puerto correcto.
6. Verifica el estado del firewall con `sudo ufw status`.
7. Agrega la regla para permitir SSH: `sudo ufw allow ssh`.
8. Activa el firewall con `sudo ufw enable`.
9. Verifica con `sudo ufw status` que las reglas están activas.
10. Termina el servidor: `kill $SERVER_PID` o `pkill -f "http.server"`.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1 y 2
ip addr
ifconfig

# Paso 3
ping -c 3 8.8.8.8

# Paso 4 y 5
ss -tlnp
ss -tlnp | grep 8080

# Paso 6
sudo ufw status

# Paso 7, 8 y 9
sudo ufw allow ssh
sudo ufw enable
sudo ufw status

# Paso 10
kill $SERVER_PID
# o si ya no tienes la variable:
pkill -f "http.server"
```

</details>

---

### Lab 08 — Mantenimiento del Sistema

**Escenario:** El servidor del equipo lleva semanas sin mantenimiento. Se han acumulado paquetes obsoletos que ningún servicio usa, hay software que ya no se necesita y las listas de repositorios están desactualizadas. Tu tarea: limpiar el sistema sin romper nada, verificar el estado del software instalado y mantener todo ordenado.

> Un sysadmin no solo instala cosas — también tiene la responsabilidad de mantener el sistema limpio. Los paquetes huérfanos ocupan disco, pueden tener vulnerabilidades sin parche y complican los diagnósticos futuros.

---

#### `apt` — Gestor de paquetes de Ubuntu/Debian

**Sintaxis:**
```
apt [opciones] comando
apt install paquete     # instalar
apt remove paquete      # desinstalar (conserva configuración)
apt purge paquete       # desinstalar + eliminar archivos de configuración
apt update              # actualizar listas de paquetes (no instala nada)
apt upgrade             # instalar actualizaciones disponibles
apt autoremove          # eliminar paquetes huérfanos no necesarios
apt search término      # buscar paquetes por nombre o descripción
apt show paquete        # ver detalles de un paquete
apt list --installed    # listar paquetes instalados
```

**Qué hace:** `apt` es el gestor de paquetes interactivo de sistemas basados en Debian (Ubuntu, Linux Mint, etc.). Permite instalar, actualizar y eliminar software del sistema, siempre descargando desde repositorios oficiales verificados.

**Ejemplo del lab — ver ayuda:**
```
apt
```
```
apt 2.4.12 (amd64)
Usage: apt [options] command

Most used commands:
  list         - list packages based on package names
  search       - search in package descriptions
  show         - show package details
  install      - install packages
  remove       - remove packages
  autoremove   - Remove automatically all unused packages
  update       - update list of available packages
  upgrade      - upgrade the system
```

> Ejecutar `apt` sin argumentos muestra los subcomandos disponibles — útil para recordar la sintaxis sin buscar en el manual.

**Diferencia entre los comandos de eliminación:**

| Comando | Qué elimina |
|---------|------------|
| `apt remove paquete` | Elimina el programa pero conserva archivos de configuración |
| `apt purge paquete` | Elimina el programa Y sus archivos de configuración |
| `apt autoremove` | Elimina paquetes instalados como dependencias que ya nadie usa |

> La regla de producción: usa `remove` cuando no estás seguro de volver a instalar, y `purge` cuando quieres limpiar completamente para reinstalar desde cero.

---

#### `sudo apt update` — Actualizar la lista de paquetes disponibles

**Sintaxis:**
```
sudo apt update
```

**Qué hace:** Descarga la lista actualizada de paquetes desde los repositorios configurados. No instala ni actualiza nada — solo sincroniza la base de datos local con lo que hay disponible.

**Ejemplo del lab:**
```
sudo apt update
```
```
Hit:1 http://mirrors.cloud.aliyuncs.com/ubuntu jammy InRelease
Hit:2 http://mirrors.cloud.aliyuncs.com/ubuntu jammy-updates InRelease
Hit:3 http://mirrors.cloud.aliyuncs.com/ubuntu jammy-backports InRelease
Hit:4 http://mirrors.cloud.aliyuncs.com/ubuntu jammy-security InRelease
Reading package lists... Done
344 packages can be upgraded. Run 'apt list --upgradable' to see them.
```

**Cómo leer la salida:**

| Indicador | Significado |
|-----------|------------|
| `Hit:N` | El repositorio no cambió desde la última vez — no descarga nada |
| `Get:N` | Hay nueva lista disponible — la descarga |
| `Ign:N` | El repositorio fue ignorado (puede ser irrelevante o redundante) |
| `Err:N` | Error al conectar con el repositorio — revisar red o URL |
| `N packages can be upgraded` | Cuántos paquetes tienen actualizaciones disponibles |

> `apt update` siempre debe ejecutarse antes de `apt install` o `apt upgrade`. Sin actualizar primero, instalarías versiones antiguas de la lista cacheada.

---

#### `sudo apt autoremove` — Limpiar paquetes huérfanos

**Sintaxis:**
```
sudo apt autoremove
```

**Qué hace:** Identifica y elimina paquetes que fueron instalados automáticamente como dependencias de otro paquete, pero que ya no son necesarios porque ese paquete principal fue desinstalado.

**Ejemplo del lab:**
```
sudo apt autoremove
```
```
The following packages will be REMOVED:
  gir1.2-libxfce4util-1.0 gir1.2-xfconf-0 gsfonts-x11 libdbus-glib-1-2
  libgdk-pixbuf-xlib-2.0-0 libjpeg-turbo-progs miscfiles xscreensaver-data
0 upgraded, 0 newly installed, 8 to remove and 344 not upgraded.
After this operation, 5,641 kB disk space will be freed.
Do you want to continue? [Y/n] y
```

**Qué pasó aquí:** Al eliminar un paquete principal (en este caso `figlet`), quedaron 8 dependencias que nadie más usa. `autoremove` las detectó y liberó 5.6 MB de disco.

> Antes de confirmar con `y`, lee la lista de paquetes que se van a eliminar. Si reconoces alguno que usas directamente, escribe `n` e investiga. Un paquete puede ser dependencia de otro que aún necesitas.

**Cuándo ejecutar `autoremove`:**
- Después de `apt remove` o `apt purge`
- Al final de una sesión de limpieza del sistema
- Periódicamente en servidores que llevan tiempo sin mantenimiento

---

#### `dpkg -s` — Verificar si un paquete está instalado

**Sintaxis:**
```
dpkg -s nombre_paquete
```

**Qué hace:** Consulta la base de datos local de paquetes instalados y muestra el estado detallado de un paquete específico. No requiere conexión a internet — trabaja con lo que ya está instalado.

**Ejemplo del lab:**
```
dpkg -s neofetch
```
```
Package: neofetch
Status: install ok installed
Priority: optional
Section: utils
Installed-Size: 351
Maintainer: Ubuntu Developers
Architecture: all
Version: 7.1.0-3
Description: Shows Linux System Information with Distribution Logo
```

**Campos más útiles:**

| Campo | Qué indica |
|-------|-----------|
| `Status: install ok installed` | El paquete está correctamente instalado |
| `Status: deinstall ok config-files` | Fue desinstalado pero quedan archivos de configuración |
| `Version` | Versión exacta instalada |
| `Installed-Size` | Espacio que ocupa en disco (en KB) |
| `Description` | Qué hace el paquete |

**Cuándo usar `dpkg -s` vs `apt show`:**

| Comando | Consulta | Requiere red |
|---------|---------|-------------|
| `dpkg -s paquete` | Estado de instalación actual | No — usa base de datos local |
| `apt show paquete` | Info del paquete en el repositorio | No (usa caché), sí para info nueva |
| `which comando` | Si un ejecutable está disponible en PATH | No |

> Para confirmar rápidamente si algo está instalado: `dpkg -s nombre 2>/dev/null | grep Status`. Si devuelve `install ok installed`, está. Si no devuelve nada, no está instalado.

---

#### `sudo apt remove` — Desinstalar un paquete

**Sintaxis:**
```
sudo apt remove nombre_paquete
```

**Qué hace:** Elimina el software del sistema pero conserva sus archivos de configuración en `/etc/`. Si reinstalaras el paquete, recuperaría tu configuración anterior.

**Ejemplo del lab:**
```
sudo apt remove figlet
```
```
The following packages will be REMOVED:
  figlet
After this operation, 615 kB disk space will be freed.
Do you want to continue? [Y/n] y
```

> `apt remove` muestra qué va a eliminar y cuánto espacio liberará antes de pedir confirmación. Siempre lee la lista — si aparecen paquetes inesperados, es porque son dependencias exclusivas del paquete que estás eliminando.

---

#### Flujo de mantenimiento de paquetes

Para mantener un sistema limpio de forma segura:

```
1. sudo apt update             → Sincronizar listas de repositorios
        ↓
2. dpkg -s paquete             → Verificar qué está instalado antes de actuar
        ↓
3. sudo apt remove paquete     → Eliminar software no necesario
        ↓
4. sudo apt autoremove         → Limpiar dependencias huérfanas
        ↓
5. sudo apt upgrade            → (Opcional) Instalar actualizaciones pendientes
```

> Este orden importa: actualizar primero, luego limpiar, luego parchear. Hacerlo al revés puede instalar actualizaciones de paquetes que vas a borrar de todas formas.

---

#### Errores frecuentes — Lab 08

**`apt install` sin `apt update` primero**

La lista de paquetes local puede estar desactualizada. Podrías instalar una versión antigua o recibir el error `Unable to locate package` aunque el paquete exista. Siempre `sudo apt update` antes de instalar algo nuevo.

**`apt remove` cuando se quería `apt purge`**

Si desinstalaras y reinstalaras un servicio (por ejemplo `nginx`), con `remove` la reinstalación recuperaría la configuración anterior — incluyendo posibles configuraciones incorrectas que causaron el problema original. Usa `purge` para empezar desde cero.

**Confirmar `autoremove` sin leer la lista**

Si un paquete fue instalado manualmente pero `apt` lo marcó como dependencia automática, `autoremove` intentará borrarlo. Antes de confirmar con `y`, lee los nombres — si algo parece importante, cancela con `n` y márcalo como manual: `sudo apt-mark manual nombre_paquete`.

**Mezclar `apt` y `dpkg` directamente para instalar `.deb`**

Instalar un `.deb` con `sudo dpkg -i paquete.deb` no resuelve dependencias automáticamente. Si falta alguna dependencia, el paquete queda en estado roto. La solución: después de `dpkg -i`, ejecuta `sudo apt install -f` para que `apt` resuelva las dependencias faltantes.

---

#### Ejercicio — Lab 08

**Entorno:** KillerCoda (Ubuntu) o cualquier Debian/Ubuntu con acceso sudo.

**Tareas:**

1. Ejecuta `sudo apt update` y anota cuántos paquetes pueden actualizarse.
2. Instala el paquete `cowsay`: `sudo apt install cowsay`.
3. Verifica que quedó instalado con `dpkg -s cowsay` — ¿cuál es la versión?
4. Usa `apt show cowsay` y compara la información con `dpkg -s cowsay`.
5. Desinstala `cowsay` con `sudo apt remove cowsay`.
6. Verifica con `dpkg -s cowsay` — ¿qué dice el campo `Status` ahora?
7. Ejecuta `sudo apt autoremove` y observa si queda alguna dependencia huérfana.
8. Instala `cowsay` de nuevo con `sudo apt install cowsay`.
9. Ahora desinstálalo con `sudo apt purge cowsay`.
10. Ejecuta `dpkg -s cowsay` de nuevo — ¿hay diferencia respecto al paso 6?

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
sudo apt update

# Paso 2
sudo apt install cowsay

# Paso 3
dpkg -s cowsay

# Paso 4
apt show cowsay

# Paso 5
sudo apt remove cowsay

# Paso 6 — Status cambia a: "deinstall ok config-files"
dpkg -s cowsay

# Paso 7
sudo apt autoremove

# Paso 8
sudo apt install cowsay

# Paso 9
sudo apt purge cowsay

# Paso 10 — dpkg -s puede no encontrar el paquete o mostrar "unknown ok not-installed"
dpkg -s cowsay
```

> La diferencia clave entre el paso 6 y el 10: `remove` deja el estado `config-files`, `purge` elimina completamente toda traza del paquete.

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
| `grep "patrón" archivo` | Filtra líneas que contienen el patrón | 03 |
| `grep -i` | Búsqueda sin distinguir mayúsculas/minúsculas | 03 |
| `grep -n` | Muestra número de línea de cada coincidencia | 03 |
| `grep -c` | Cuenta cuántas líneas coinciden | 03 |
| `grep -v` | Muestra líneas que NO coinciden | 03 |
| `grep -r "patrón" dir` | Busca en todos los archivos de un directorio | 03 |
| `dmesg` | Mensajes del kernel desde el arranque | 03 |
| `dmesg \| grep "error"` | Filtra mensajes del kernel con errores | 03 |
| `diff f1 f2 > reporte.txt` | Guarda diferencias en un archivo | 03 |
| `sudo chmod 750 dir` | Permisos privados de equipo (rwxr-x---) | 04 |
| `sudo chmod g+s dir` | Activa setgid en un directorio (simbólico) | 04 |
| `sudo chmod 2770 dir` | Setgid + rwx para dueño y grupo (numérico) | 04 |
| `sudo useradd -m usuario` | Crea usuario con home directory | 05 |
| `sudo passwd usuario` | Establece contraseña de otro usuario | 05 |
| `sudo usermod -aG grupo usuario` | Agrega a grupo sin eliminar membresías | 05 |
| `sudo usermod -L usuario` | Bloquea la cuenta de un usuario | 05 |
| `sudo usermod -U usuario` | Desbloquea la cuenta de un usuario | 05 |
| `grep "^usuario:" archivo` | Busca línea que empieza exactamente con ese texto | 05 |
| `ps` | Procesos de la terminal actual | 06 |
| `ps -x` | Todos tus procesos (con y sin terminal) | 06 |
| `ps -u` | Tus procesos con %CPU y %MEM | 06 |
| `ps aux` | Todos los procesos del sistema con recursos | 06 |
| `ps -p PID -o cols` | Info específica de un proceso por PID | 06 |
| `pgrep nombre` | Devuelve el PID de procesos que coinciden | 06 |
| `pgrep -f "patrón"` | Busca en la línea de comando completa | 06 |
| `pkill nombre` | Termina procesos por nombre (SIGTERM) | 06 |
| `pkill -9 nombre` | Fuerza la terminación (SIGKILL) | 06 |
| `nohup cmd > log 2>&1 &` | Lanza en background, sobrevive al cierre de sesión | 06 |
| `ip addr` | Muestra todas las interfaces de red y sus IPs | 07 |
| `ip addr show eth0` | Muestra solo una interfaz específica | 07 |
| `ifconfig` | Vista clásica de interfaces de red (net-tools) | 07 |
| `ping -c N destino` | Envía N paquetes ICMP para probar conectividad | 07 |
| `ss -t` | Conexiones TCP actualmente establecidas | 07 |
| `ss -tlnp` | Puertos TCP en escucha con proceso responsable | 07 |
| `ss -tlnp \| grep PUERTO` | Filtra qué proceso ocupa un puerto específico | 07 |
| `sudo ufw status` | Muestra si el firewall está activo y sus reglas | 07 |
| `sudo ufw allow ssh` | Permite SSH (siempre antes de `enable`) | 07 |
| `sudo ufw allow PUERTO` | Abre un puerto en el firewall | 07 |
| `sudo ufw deny PUERTO` | Bloquea un puerto en el firewall | 07 |
| `sudo ufw enable` | Activa el firewall | 07 |
| `sudo apt update` | Sincroniza listas de paquetes con los repositorios | 08 |
| `sudo apt install paquete` | Instala un paquete y sus dependencias | 08 |
| `sudo apt remove paquete` | Desinstala un paquete (conserva configuración) | 08 |
| `sudo apt purge paquete` | Desinstala paquete y elimina su configuración | 08 |
| `sudo apt autoremove` | Elimina dependencias huérfanas ya no necesarias | 08 |
| `apt show paquete` | Muestra info del paquete desde el repositorio | 08 |
| `dpkg -s paquete` | Verifica si un paquete está instalado y su versión | 08 |
| `apt list --installed` | Lista todos los paquetes instalados en el sistema | 08 |

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
| **`grep`** | Global Regular Expression Print — filtra líneas por patrón de texto |
| **`dmesg`** | Diagnostic Messages — buffer de mensajes del kernel |
| **Troubleshooting** | Proceso sistemático para identificar y resolver fallos en un sistema |
| **Staging** | Entorno de prueba que replica producción — donde se prueba antes de desplegar |
| **Producción** | Entorno real donde corre la aplicación para los usuarios finales |
| **`\|` (pipe)** | Operador que pasa la salida de un comando como entrada al siguiente |
| **Setgid** | Set Group ID — bit especial que hace que nuevos archivos hereden el grupo del directorio |
| **`s` minúscula** | En `ls -l`: setgid (o setuid) activo y el permiso de ejecución también está activo |
| **`S` mayúscula** | En `ls -l`: setgid activo pero sin permiso de ejecución — casi siempre un error |
| **Bits especiales** | Permisos adicionales de Linux: setuid(4), setgid(2), sticky(1) |
| **`2xxx`** | Notación numérica con setgid — el `2` va delante de los 3 dígitos normales |
| **Ancla `^`** | En grep: obliga a que el patrón coincida desde el inicio de la línea |
| **Cuenta bloqueada** | Usuario con `!` al inicio del hash en `/etc/shadow` — no puede autenticarse |
| **`-aG`** | Append + Groups: agrega grupo sin reemplazar los existentes |
| **`ps aux`** | Muestra todos los procesos del sistema con usuario, CPU y memoria |
| **PID** | Process ID — número único de identificación de un proceso |
| **PPID** | Parent Process ID — PID del proceso que lanzó este proceso |
| **`SIGTERM`** | Señal 15 — pide al proceso que termine limpiamente |
| **`SIGKILL`** | Señal 9 — mata el proceso inmediatamente sin limpieza posible |
| **`SIGHUP`** | Señal 1 — enviada al cerrar sesión; termina los procesos hijo |
| **`nohup`** | No Hangup — hace que un proceso ignore la señal SIGHUP |
| **`&`** | Operador que lanza un proceso en segundo plano (background) |
| **`2>&1`** | Redirige stderr al mismo destino que stdout |
| **Zombie** | Proceso que terminó pero su padre no liberó su entrada en la tabla de procesos |
| **Interfaz de red** | Punto de conexión entre el sistema y una red — física (`eth0`) o virtual (`lo`, `docker0`) |
| **`lo` (loopback)** | Interfaz virtual interna: `127.0.0.1` — el sistema habla consigo mismo |
| **`eth0`** | Primera interfaz Ethernet — la conexión principal a la red |
| **`NO-CARRIER`** | Interfaz activa en el SO pero sin señal física — normal en `docker0` sin contenedores |
| **`ip addr`** | Herramienta moderna del kernel para ver y gestionar interfaces de red |
| **`ifconfig`** | Herramienta clásica (net-tools) para ver interfaces — equivalente legacy de `ip addr` |
| **ICMP** | Protocolo que usa `ping` para probar conectividad — no es TCP ni UDP |
| **Latencia** | Tiempo de ida y vuelta de un paquete de red — se mide en milisegundos (ms) |
| **`ss`** | Socket Statistics — reemplazo moderno de `netstat` para ver puertos y conexiones |
| **Socket** | Punto de comunicación de red — combinación de IP + puerto + protocolo |
| **Puerto** | Número (0-65535) que identifica un servicio en un host — ej. 22=SSH, 80=HTTP |
| **LISTEN** | Estado de un socket esperando conexiones entrantes |
| **ESTAB** | Estado ESTABLISHED — conexión TCP activa y establecida |
| **Firewall** | Sistema que filtra tráfico de red según reglas — permite o bloquea puertos e IPs |
| **`ufw`** | Uncomplicated Firewall — capa simplificada sobre `iptables` para gestionar el firewall |
| **`/24`** | Notación CIDR de máscara de subred — equivale a `255.255.255.0`, red de 254 hosts |
| **`apt`** | Advanced Package Tool — gestor de paquetes interactivo de Debian/Ubuntu |
| **`dpkg`** | Debian Package Manager — herramienta de bajo nivel que instala `.deb` directamente |
| **Repositorio** | Servidor donde se almacenan y distribuyen paquetes de software verificados |
| **Paquete** | Unidad de software distribuible: contiene el programa, dependencias y metadatos |
| **Dependencia** | Paquete que otro paquete necesita para funcionar correctamente |
| **Paquete huérfano** | Dependencia instalada automáticamente cuyo paquete principal ya fue eliminado |
| **`apt update`** | Descarga listas actualizadas de paquetes — no instala nada, solo sincroniza |
| **`apt upgrade`** | Instala las actualizaciones disponibles de los paquetes instalados |
| **`apt remove`** | Elimina el software pero conserva archivos de configuración en `/etc/` |
| **`apt purge`** | Elimina el software Y sus archivos de configuración — limpieza completa |
| **`apt autoremove`** | Limpia paquetes instalados como dependencias que ya ningún paquete requiere |
| **`Hit:` en apt update** | El repositorio no cambió desde la última sincronización |
| **`Get:` en apt update** | Hay nueva información disponible — la descarga |
| **`Status: install ok installed`** | Estado de dpkg que confirma que el paquete está correctamente instalado |

---

## Errores Humanos Frecuentes

Esta sección recopila los errores más comunes al administrar sistemas Linux. No son errores de sintaxis — son decisiones que parecen correctas pero tienen consecuencias graves.

---

### Permisos y propiedad

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `chmod -G grupo user` | Elimina **todos** los grupos del usuario, solo queda el nuevo | `chmod -aG grupo user` |
| `chmod 777 directorio` | Cualquier usuario del sistema puede leer, escribir y ejecutar | Usar `755` o `750` según el caso |
| `chmod -R 777 /` | Destruye los permisos de todo el sistema operativo | Nunca usar `-R` en rutas raíz |
| `chown -R root /home/user` | El usuario pierde acceso a su propio home | Especificar siempre la ruta completa y verificar antes |

---

### Archivos y directorios

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `rm -rf /directorio /` | El espacio entre la ruta y `/` borra el sistema de archivos raíz | Verificar el comando antes de ejecutar con `echo rm -rf ...` |
| `cmd > archivo` cuando se quería `>>` | Sobreescribe y borra todo el contenido anterior | Usar `>>` para acumular, `>` solo cuando quieres empezar limpio |
| `tar -xzf archivo.tar.gz` sin verificar destino | Extrae archivos sobre el directorio actual, puede sobrescribir archivos existentes | Extraer en un directorio temporal primero: `tar -xzf archivo.tar.gz -C /tmp/prueba/` |
| Borrar originales antes de verificar el tar | Si el tar estaba incompleto o corrupto, los datos se pierden | Siempre `tar -tzf archivo.tar.gz` antes de `rm` |

---

### Usuarios y autenticación

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `useradd user` sin `-m` | El usuario existe pero no tiene home — no puede guardar archivos ni configs | `useradd -m user` o crear el home manualmente después |
| `usermod -G grupo user` sin `-a` | El usuario pierde todos sus grupos anteriores | Siempre `usermod -aG grupo user` |
| `userdel user` sin `-r` cuando se quería limpiar todo | El home queda huérfano ocupando espacio | `userdel -r user` para eliminar usuario y home juntos |
| `su -usuario` (sin espacio) | Error: `invalid option` — el `-` se interpreta como flag | `su - usuario` con espacio entre el guión y el nombre |
| `passwd user` sin `sudo` | Solo cambia tu propia contraseña, falla silenciosamente o da error | `sudo passwd user` para cambiar la de otro usuario |

---

### grep y búsquedas

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `grep "user" /etc/passwd` | Puede devolver líneas de otros usuarios que contienen "user" en cualquier campo | `grep "^user:" /etc/passwd` para buscar exactamente ese usuario |
| `grep "ERROR" log.txt` con mayúsculas fijas | Se pierden errores escritos como `error` o `Error` | `grep -i "error" log.txt` para búsqueda sin distinción de caso |
| `diff archivo1 archivo2` con el orden invertido | Los símbolos `<` y `>` quedan al revés, confunde la interpretación | Convención: siempre `diff original modificado` o `diff staging produccion` |

---

### Comandos con `sudo`

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| Ejecutar `sudo` sin entender el comando | Puede modificar archivos del sistema sin posibilidad de revertir | Siempre prueba el comando sin `sudo` primero para ver qué haría |
| `sudo !!` sin revisar el historial | Ejecuta como root el último comando, que puede no ser lo que esperas | Revisar con `history` antes de usar `!!` |

---

### Gestión de paquetes

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `apt install` sin `apt update` primero | Se instala una versión desactualizada o se recibe `Unable to locate package` | Siempre `sudo apt update` antes de instalar algo nuevo |
| `apt remove` cuando se quería `purge` | Quedan archivos de configuración — la reinstalación hereda la config rota | `sudo apt purge paquete` para eliminar programa y configuración completamente |
| Confirmar `autoremove` sin leer la lista | Se elimina un paquete que necesitas — puede romper servicios | Leer la lista antes de `y`; si algo parece importante, cancelar con `n` |
| `dpkg -i paquete.deb` sin resolver dependencias | El paquete queda en estado roto (`dependency problems`) | Después de `dpkg -i`, ejecutar `sudo apt install -f` para resolver dependencias |
| `apt upgrade` en producción sin probar antes | Las actualizaciones pueden cambiar comportamiento de servicios críticos | Primero en staging; en producción, actualizar paquete a paquete con `apt install paquete=versión` |

---

### Red y firewall

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `sudo ufw enable` sin agregar `allow ssh` antes | El firewall bloquea la sesión SSH activa — pierdes acceso remoto inmediatamente | Siempre `sudo ufw allow ssh` antes de `sudo ufw enable` |
| `ping` sin `-c N` en un script | El ping corre indefinidamente bloqueando los pasos siguientes | `ping -c 3 destino` para limitar a 3 paquetes |
| `ss -l` cuando se quería ver conexiones activas | Solo muestra puertos en espera, no conexiones ya establecidas | `ss -t` para conexiones activas, `ss -tlnp` para diagnóstico completo |
| Confundir puerto en escucha con servicio accesible | Un puerto puede estar en LISTEN pero bloqueado por firewall | Verificar con `ss -tlnp` Y con `sudo ufw status` — ambos deben alinearse |

---

_Última actualización: 2026-03-28_
