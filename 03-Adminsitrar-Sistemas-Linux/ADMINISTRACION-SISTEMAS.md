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

_Última actualización: 2026-03-28_
