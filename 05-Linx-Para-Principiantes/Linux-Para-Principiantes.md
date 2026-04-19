# Linux para Principiantes — LabEx

> Manual de referencia construido a partir de dos cursos de LabEx:
> **"Linux para Principiantes"** y **"Practicar Comandos de Linux"**.
> Diseñado para llevarte desde cero hasta un uso fluido del sistema operativo más usado en servidores del mundo.

---

## Tabla de Contenidos

- [Sobre este manual](#sobre-este-manual)
- [Cómo usar este manual](#cómo-usar-este-manual)
- [Labs](#labs)
  - [Lab 01 — Tu Primera Terminal](#lab-01--tu-primera-terminal)
  - [Lab 02 — Navegar y Gestionar Archivos](#lab-02--navegar-y-gestionar-archivos)
  - [Lab 03 — Cómo Pedir Ayuda en Linux](#lab-03--cómo-pedir-ayuda-en-linux)
  - [Lab 04 — Desafío de Operaciones de Archivos](#lab-04--desafío-de-operaciones-de-archivos)
  - [Lab 05 — Usuarios, Grupos y Permisos](#lab-05--usuarios-grupos-y-permisos)
  - [Lab 06 — Crear Usuarios con Configuración Precisa](#lab-06--crear-usuarios-con-configuración-precisa)
  - [Lab 07 — El Sistema de Archivos y Búsqueda](#lab-07--el-sistema-de-archivos-y-búsqueda)
  - [Lab 08 — Variables de Entorno](#lab-08--variables-de-entorno)
  - [Lab 09 — Desafío: Variable de Entorno Permanente](#lab-09--desafío-variable-de-entorno-permanente)
  - [Lab 10 — Empaquetar y Comprimir Archivos](#lab-10--empaquetar-y-comprimir-archivos)
  - [Lab 11 — Desafío: Respaldo de Logs del Sistema](#lab-11--desafío-respaldo-de-logs-del-sistema)
  - [Lab 12 — Discos, Particiones y Sistemas de Archivos](#lab-12--discos-particiones-y-sistemas-de-archivos)
  - [Lab 13 — Tuberías, Operadores Condicionales y Procesamiento de Texto](#lab-13--tuberías-operadores-condicionales-y-procesamiento-de-texto)
  - [Lab 14 — Desafío: Procesar Datos de Sensores](#lab-14--desafío-procesar-datos-de-sensores)
  - [Lab 15 — tr, col, join y paste: Transformar y Combinar Texto](#lab-15--tr-col-join-y-paste-transformar-y-combinar-texto)
  - [Lab 16 — Desafío: Analizar el PATH con tr](#lab-16--desafío-analizar-el-path-con-tr)
- [Referencia Rápida](#referencia-rápida)
- [Errores Humanos Frecuentes](#errores-humanos-frecuentes)
- [Glosario](#glosario)

---

## Sobre este manual

**Nivel:** Principiante absoluto — no se requiere experiencia previa con Linux.
**Enfoque:** Construir confianza y fluidez con la terminal de Linux a través de práctica real.

### Qué cubre este manual

Este manual combina dos cursos complementarios de LabEx:

**Curso 1 — Linux para Principiantes**
Exploración sistemática y completa de Linux: navegación, usuarios, permisos, procesamiento de texto, variables de entorno, gestión de software y técnicas avanzadas de tubería.

**Curso 2 — Practicar Comandos de Linux**
Práctica intensiva de los comandos más usados en el trabajo diario: gestión de archivos y directorios, búsqueda, procesamiento de texto, uso de disco y medición de rendimiento.

### Temas que se cubren

| Área | Comandos |
|------|---------|
| Navegación y archivos | `ls`, `cd`, `pwd`, `mkdir`, `rm`, `mv`, `cp` |
| Visualización de texto | `cat`, `nl`, `more`, `less`, `head`, `tail` |
| Búsqueda | `find`, `which`, `whereis`, `xargs` |
| Procesamiento de texto | `grep`, `cut`, `paste`, `tr`, `sort`, `uniq`, `wc` |
| Comparación | `diff`, `patch`, `join`, `comm` |
| Usuarios y permisos | `useradd`, `chmod`, `chown`, `groups` |
| Variables de entorno | `echo`, `export`, `env`, `PATH` |
| Software | `apt`, `dpkg` |
| Disco y sistema | `df`, `du`, `mount` |
| Flujos y tuberías | `|`, `>`, `>>`, `2>&1`, `tee` |
| Expresiones regulares | `grep -E`, `sed` |

### Diferencia con los manuales anteriores

| Manual | Enfoque |
|--------|---------|
| `02-Inicio-Linux` | Primeros comandos — familiarizarse con la terminal |
| `03-Adminsitrar-Sistemas-Linux` | Escenarios de sysadmin — resolver problemas reales |
| `05-Linux-Para-Principiantes` (este) | Profundidad en cada comando — entender el "por qué" y dominar las variantes |

---

## Cómo usar este manual

Cada lab sigue la misma estructura:

- **Escenario** — el contexto que motiva el lab
- **Comandos nuevos** — explicación, sintaxis y ejemplos reales
- **Flujo del lab** — cómo se conectan los pasos entre sí
- **Errores frecuentes** — qué puede salir mal y cómo leerlo
- **Ejercicio** — práctica independiente en KillerCoda o cualquier Linux

---

## Labs

---

### Lab 01 — Tu Primera Terminal

**Escenario:** Acabas de abrir una terminal de Linux por primera vez. La pantalla está en blanco y hay un cursor parpadeando. No pasa nada hasta que tú escribas algo. Este lab es tu primer contacto con esa conversación: le escribes al sistema, él responde.

> La terminal no es un lugar peligroso — es simplemente una forma de hablar con el sistema operativo usando texto en lugar de clics. Todo lo que ves en una interfaz gráfica (reloj, calculadora, explorador de archivos) tiene su equivalente en comandos de terminal.

---

#### `echo` — Imprimir texto en la terminal

**Sintaxis:**
```
echo "texto"
echo texto        # las comillas son opcionales si no hay espacios
echo "texto $VARIABLE"   # expande variables dentro de comillas dobles
```

**Qué hace:** Imprime el texto que le des directamente en la terminal. Es el equivalente de `print()` o `console.log()` — el primer comando que usa cualquier persona cuando aprende a programar o a usar una terminal.

**Ejemplo del lab:**
```
echo "Hello LabEx"
```
```
Hello LabEx
```

**Usos reales de `echo`:**
- Imprimir mensajes en scripts: `echo "Proceso iniciado"`
- Ver el valor de una variable: `echo $HOME`
- Crear archivos rápidamente: `echo "contenido" > archivo.txt`
- Verificar que una variable existe: `echo $PATH`

> `echo` es uno de esos comandos que parece trivial al principio pero que usarás cientos de veces en scripts reales. Cada vez que un script imprime un mensaje de progreso, hay un `echo` detrás.

---

#### `date` — Consultar la fecha y hora del sistema

**Sintaxis:**
```
date                        # fecha y hora completa del sistema
date +"%Y-%m-%d"            # solo la fecha en formato año-mes-día
date +"%H:%M:%S"            # solo la hora en formato hora:minuto:segundo
date +"%d/%m/%Y %H:%M"      # formato personalizado
```

**Qué hace:** Muestra la fecha y hora actual del sistema. Sin argumentos, imprime todo en el formato por defecto. Con el prefijo `+` puedes controlar exactamente qué muestra y en qué formato.

**Ejemplo del lab:**
```
date
```
```
Fri Apr  3 09:29:06 AM CST 2026
```

**Cómo leer la salida:**

| Parte | Valor del ejemplo | Significado |
|-------|------------------|------------|
| `Fri` | Viernes | Día de la semana (abreviado en inglés) |
| `Apr  3` | 3 de abril | Mes y día |
| `09:29:06 AM` | 9:29:06 AM | Hora del sistema |
| `CST` | Central Standard Time | Zona horaria |
| `2026` | 2026 | Año |

**Formatos útiles con `date`:**

| Comando | Salida ejemplo | Uso típico |
|---------|---------------|-----------|
| `date +"%Y-%m-%d"` | `2026-04-03` | Nombres de archivos de respaldo |
| `date +"%d/%m/%Y"` | `03/04/2026` | Formato latinoamericano |
| `date +"%s"` | `1743681946` | Segundos desde epoch (Unix timestamp) |
| `date +"%A"` | `Friday` | Día completo en inglés |

> En el Lab 09 del manual de administración usamos `date +\%Y-\%m-\%d` dentro de cron para generar nombres únicos de respaldo. `date` no es solo informativo — es una herramienta de construcción en scripts.

---

#### `cal` — Ver el calendario del sistema

**Sintaxis:**
```
cal                  # mes actual
cal AÑO              # todos los meses del año indicado
cal MES AÑO          # un mes específico de un año específico
```

**Qué hace:** Muestra un calendario en la terminal. Sin argumentos muestra el mes actual con el día de hoy resaltado. Con un año, muestra los 12 meses completos.

**Ejemplo del lab:**
```
cal
```
```
     April 2026
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
...
```

```
cal 2025        # muestra el calendario completo de 2025
cal 2026        # muestra el calendario completo de 2026
```

**Variantes útiles:**

| Comando | Resultado |
|---------|----------|
| `cal` | Mes actual — el día de hoy aparece resaltado |
| `cal 2026` | Los 12 meses de 2026 |
| `cal 4 2026` | Solo abril de 2026 |
| `cal -3` | El mes anterior, el actual y el siguiente |

> El día actual siempre aparece en negrita o resaltado cuando usas `cal` sin argumentos. Es una forma rápida de ubicarte en la semana sin buscar el teléfono.

---

#### `expr` — Calculadora de la terminal

**Sintaxis:**
```
expr número operador número
```

**Qué hace:** Evalúa expresiones aritméticas simples y muestra el resultado. Opera con números enteros — no maneja decimales.

**Ejemplo del lab:**
```
expr 5 + 3
```
```
8
```

```
expr 2025 - 2024
```
```
1
```

```
expr 24 * 7
```
```
168
```

```
expr 60 / 5
```
```
12
```

**Operadores disponibles:**

| Operador | Operación | Ejemplo | Resultado |
|----------|----------|---------|----------|
| `+` | Suma | `expr 10 + 5` | `15` |
| `-` | Resta | `expr 10 - 5` | `5` |
| `\*` | Multiplicación | `expr 10 \* 5` | `50` |
| `/` | División entera | `expr 10 / 3` | `3` |
| `%` | Módulo (resto) | `expr 10 % 3` | `1` |

> El `*` necesita escaparse como `\*` en la mayoría de shells. Sin el `\`, el shell lo interpreta como un comodín de archivos (glob) y falla. En el lab lo escribiste directamente porque LabEx usa una configuración específica, pero en otros sistemas siempre usa `\*`.

**`expr` vs otras formas de calcular en Bash:**

```bash
expr 5 + 3          # forma clásica — funciona en cualquier shell POSIX
echo $((5 + 3))     # forma moderna de Bash — más rápida y soporta decimales
bc <<< "5 + 3"      # calculadora completa — soporta decimales y funciones
```

> En scripts modernos se prefiere `$((...))` sobre `expr` porque es más rápido y no requiere espacios obligatorios. Pero `expr` aparece mucho en scripts legacy y en exámenes de certificación, así que vale la pena conocerlo.

---

#### `figlet` — Arte ASCII en la terminal

**Sintaxis:**
```
figlet "texto"
figlet -f fuente "texto"     # usar una tipografía diferente
figlet -c "texto"            # centrar el texto
figlet -w N "texto"          # limitar el ancho a N caracteres
```

**Qué hace:** Convierte texto normal en arte ASCII usando diferentes "tipografías" de caracteres. No viene instalado por defecto en todos los sistemas — en Ubuntu se instala con `sudo apt install figlet`.

**Ejemplo del lab:**
```
figlet "LabEx"
```
```
 _          _     _____
| |    __ _| |__ | ____|_  __
| |   / _` | '_ \|  _| \ \/ /
| |__| (_| | |_) | |___ >  <
|_____\__,_|_.__/|_____/_/\_\
```

```
figlet -f slant "I Love Linux"
```
```
    ____   __                       __    _
   /  _/  / /   ____ _   _____     / /   (_)___  __  ___  __
   / /   / /   / __ \ | / / _ \   / /   / / __ \/ / / / |/_/
 _/ /   / /___/ /_/ / |/ /  __/  / /___/ / / / / /_/ />  <
/___/  /_____/\____/|___/\___/  /_____/_/_/ /_/\__,_/_/|_|
```

**Tipografías disponibles:**
```bash
figlet -f slant "texto"       # tipografía inclinada
figlet -f banner "texto"      # letras grandes y anchas
figlet -f big "texto"         # letras grandes
figlet -f mini "texto"        # letras pequeñas
```

Para ver todas las tipografías instaladas:
```bash
ls /usr/share/figlet/
```

> `figlet` se usa en scripts para marcar el inicio de procesos largos, en mensajes de bienvenida de servidores (`/etc/motd`) y en separadores visuales de logs. Un banner `figlet "BACKUP INICIADO"` al comienzo de un script de respaldo hace que el log sea mucho más legible de un vistazo.

---

#### `clear` — Limpiar la terminal

**Sintaxis:**
```
clear
```

**Qué hace:** Limpia la pantalla de la terminal, dejando solo el prompt al inicio. No borra el historial de comandos ni cierra ningún proceso — solo mueve la vista hacia arriba, como si hicieras scroll.

> Atajo de teclado equivalente: `Ctrl + L`. Funciona en casi todos los sistemas y es más rápido que escribir `clear`.

**Cuándo usar `clear`:**
- Cuando la terminal está llena de salida y quieres trabajar en un espacio limpio
- Antes de ejecutar un comando cuya salida quieres ver sin ruido visual alrededor
- Por higiene visual — un workspace limpio reduce errores de lectura

---

#### Flujo del lab

Este primer lab no tiene un flujo de resolución de problema — su objetivo es familiarizarte con el ritmo básico de la terminal:

```
Escribes un comando → presionas Enter → el sistema responde → vuelves al prompt
```

Cada comando que usaste sigue exactamente ese ciclo. El prompt (`$`) es la señal de que el sistema está listo para tu siguiente instrucción.

**Lo que aprendiste en este lab:**

| Comando | Para qué sirve en la práctica |
|---------|------------------------------|
| `echo` | Base de todos los mensajes en scripts |
| `date` | Generar nombres de archivos con fecha, registrar eventos |
| `cal` | Verificar días rápidamente sin salir de la terminal |
| `expr` | Cálculos simples en scripts |
| `figlet` | Banners visuales en scripts y logs |
| `clear` | Mantener el workspace limpio |

---

#### Errores frecuentes — Lab 01

**`expr 24 * 7` devuelve un error o lista de archivos**

Sin escapar el `*`, el shell lo expande como comodín y lista los archivos del directorio actual en lugar de multiplicar. La forma correcta es `expr 24 \* 7`. En LabEx no ocurre porque el entorno lo maneja, pero en otros sistemas sí.

**`echo` con comillas dobles expande variables sin querer**

`echo "El usuario es $USER"` imprimirá el nombre real del usuario porque `$USER` se expande dentro de `"..."`. Si quieres imprimir el texto literal `$USER`, usa comillas simples: `echo 'El usuario es $USER'`.

**`figlet` no está instalado**

Si ves `command not found: figlet`, el paquete no está instalado. En Ubuntu/Debian: `sudo apt install figlet`. En Fedora/RHEL: `sudo dnf install figlet`.

**`date` muestra la hora incorrecta**

La hora que muestra `date` es la del servidor o máquina virtual, no necesariamente tu hora local. En entornos de cloud como LabEx, el servidor puede estar en una zona horaria diferente a la tuya.

---

#### Ejercicio — Lab 01

**Entorno:** KillerCoda (Ubuntu) o cualquier terminal Linux.

**Tareas:**

1. Imprime tu nombre completo con `echo`.
2. Muestra la fecha actual en formato `DD/MM/YYYY` usando `date` con formato personalizado.
3. Muestra el calendario del mes en que naciste (ej: `cal 3 1999`).
4. Calcula cuántos días tiene un año: usa `expr` para multiplicar las semanas por los días.
5. Si `figlet` está instalado, genera arte ASCII con tu nombre. Si no, instálalo primero.
6. Limpia la terminal con `clear` y luego usa `echo` para imprimir `"Terminal lista"`.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
echo "Tu Nombre Completo"

# Paso 2
date +"%d/%m/%Y"

# Paso 3 (ejemplo: marzo de 1999)
cal 3 1999

# Paso 4
expr 52 \* 7

# Paso 5
sudo apt install figlet   # si no está instalado
figlet "Tu Nombre"

# Paso 6
clear
echo "Terminal lista"
```

</details>

---

### Lab 02 — Navegar y Gestionar Archivos

**Escenario:** Ya sabes hablar con la terminal. Ahora el siguiente paso es moverte por el sistema de archivos como si fuera tu propio escritorio: saber dónde estás, ir a donde necesitas, crear carpetas y archivos, y manipularlos. También aprenderás a pedir ayuda directamente al sistema cuando no recuerdes cómo funciona un comando.

> El sistema de archivos de Linux es un árbol que parte desde la raíz `/`. Todo lo que existe en el sistema — programas, configuraciones, documentos, dispositivos — es un nodo de ese árbol. Navegar ese árbol es la habilidad más fundamental de Linux.

---

#### El trío de navegación: `pwd`, `cd`, `ls`

Estos tres comandos son los que más vas a usar en cualquier sesión de terminal. Se usan juntos de manera natural: `pwd` para saber dónde estás, `cd` para moverte, y `ls` para ver qué hay.

---

#### `pwd` — Saber en qué directorio estás

**Sintaxis:**
```
pwd
```

**Qué hace:** Imprime la ruta absoluta del directorio actual. `pwd` significa *Print Working Directory* — el "directorio de trabajo" es el lugar del sistema de archivos donde se ejecutan tus comandos en este momento.

**Ejemplo del lab:**
```
pwd
```
```
/home/labex/project
```

```
cd ~
pwd
```
```
/home/labex
```

> `pwd` es tu brújula. Cuando te pierdas o no recuerdes dónde estás, `pwd` te lo dice al instante. Es especialmente útil después de varios `cd` encadenados o cuando trabajas con rutas largas.

---

#### `cd` — Cambiar de directorio

**Sintaxis:**
```
cd ruta            # ir a una ruta específica
cd ~               # ir al home del usuario actual
cd ..              # subir un nivel (directorio padre)
cd -               # volver al directorio anterior
cd                 # sin argumentos: ir al home (igual que cd ~)
```

**Qué hace:** Cambia el directorio de trabajo actual. Después de `cd`, todos los comandos relativos operan desde la nueva ubicación.

**Ejemplos del lab:**
```bash
cd ~               # va a /home/labex
cd project         # entra a /home/labex/project (ruta relativa)
```

**Atajos de `cd` que debes memorizar:**

| Comando | A dónde va |
|---------|-----------|
| `cd ~` | Tu directorio home (`/home/tu_usuario`) |
| `cd ..` | Un nivel arriba |
| `cd ../..` | Dos niveles arriba |
| `cd -` | Al directorio donde estabas antes — como el botón "atrás" |
| `cd /` | La raíz del sistema |
| `cd /var/log` | Ruta absoluta — funciona desde cualquier lugar |

**Ruta relativa vs ruta absoluta:**

```bash
# Ruta absoluta — empieza con /
cd /home/labex/project      # funciona desde cualquier lugar del sistema

# Ruta relativa — empieza desde donde estás ahora
cd project                  # solo funciona si "project" existe en el dir actual
cd ../project               # sube un nivel y entra a "project"
```

> `cd -` es uno de los atajos más subestimados. Si estabas en `/etc/nginx/` y fuiste a `/var/log/` para revisar un log, `cd -` te regresa a `/etc/nginx/` sin tener que escribirlo de nuevo.

---

#### `ls` — Listar el contenido de un directorio

**Sintaxis:**
```
ls                  # archivos del directorio actual
ls ruta             # archivos de otra ruta sin moverse
ls -l               # formato largo con permisos, tamaño y fecha
ls -a               # incluye archivos ocultos (los que empiezan con .)
ls -lh              # formato largo con tamaños legibles (KB, MB, GB)
ls -lt              # ordenado por fecha de modificación (más reciente primero)
ls -R               # lista recursiva incluyendo subdirectorios
```

**Ejemplo del lab:**
```bash
ls *.txt            # solo archivos con extensión .txt
ls ..               # contenido del directorio padre sin moverse
```
```
file2.txt  hello.txt   note_2.txt  note_4.txt
file3.txt  note_1.txt  note_3.txt  note_5.txt
```

```
ls ..
```
```
hello_copy.txt  linux_practice
```

**Pedir ayuda directamente a `ls`:**
```
ls --help
```

Esto imprime la página de ayuda completa del comando con todas sus opciones. En el lab la viste — es larga porque `ls` tiene docenas de flags. Lo importante es que **todos los comandos de Linux aceptan `--help`**.

---

#### `mkdir` — Crear directorios

**Sintaxis:**
```
mkdir nombre                    # crea un directorio
mkdir -p ruta/anidada/completa  # crea toda la estructura aunque no exista
mkdir dir1 dir2 dir3            # crea varios directorios a la vez
```

**Qué hace:** Crea uno o más directorios en el sistema de archivos.

**Ejemplo del lab:**
```bash
mkdir linux_practice
cd linux_practice
```

**El flag `-p` es el más importante:**
```bash
mkdir proyectos/web/frontend   # falla si "proyectos/" o "web/" no existen
mkdir -p proyectos/web/frontend  # crea toda la cadena sin importar si existe
```

> `-p` también significa que no da error si el directorio ya existe. Por eso `mkdir -p` es la forma estándar en scripts — nunca falla por directorios que ya están ahí.

---

#### `touch` — Crear archivos vacíos (y más)

**Sintaxis:**
```
touch archivo.txt               # crea un archivo vacío
touch a.txt b.txt c.txt         # crea varios archivos a la vez
touch nota_{1..5}.txt           # crea 5 archivos con expansión de llaves
```

**Qué hace:** Si el archivo no existe, lo crea vacío. Si ya existe, actualiza su fecha de última modificación sin cambiar el contenido.

**Ejemplos del lab:**
```bash
touch hello.txt                 # crea un archivo vacío
touch file1.txt file2.txt file3.txt   # tres archivos de una vez
touch note_{1..5}.txt           # crea note_1.txt hasta note_5.txt
```

**La expansión de llaves `{1..5}` — generar secuencias**

Esta es una característica del shell (no de `touch` en sí). Antes de ejecutar el comando, el shell expande `{1..5}` en `1 2 3 4 5`, generando el nombre completo de cada archivo:

```bash
touch note_{1..5}.txt
# el shell lo convierte en:
touch note_1.txt note_2.txt note_3.txt note_4.txt note_5.txt
```

**Más usos de la expansión de llaves:**
```bash
touch reporte_{enero,febrero,marzo}.txt   # nombres específicos
mkdir -p proyecto/{src,test,docs}          # estructura de proyecto de una vez
echo {a..z}                               # letras de a a z
echo {01..12}                             # números con ceros: 01 02 ... 12
```

> La expansión de llaves es una de las características más poderosas del shell para evitar repetición. En vez de crear 12 directorios uno a uno, `mkdir -p mes_{01..12}` los crea todos en un comando.

---

#### Comodines (wildcards) — Seleccionar múltiples archivos

Los comodines son patrones que el shell expande antes de ejecutar el comando. No los procesa el comando en sí — los expande el shell y le pasa la lista resultante.

**Comodines principales:**

| Patrón | Qué selecciona | Ejemplo |
|--------|---------------|---------|
| `*` | Cualquier cantidad de caracteres | `ls *.txt` → todos los .txt |
| `?` | Exactamente un carácter | `ls fil?.txt` → file1.txt, file2.txt |
| `[abc]` | Uno de los caracteres entre corchetes | `ls [fh]*.txt` → file.txt, hello.txt |
| `[1-5]` | Un carácter en el rango | `ls note_[1-3].txt` → note_1 a note_3 |

**Ejemplos del lab:**
```bash
ls *.txt        # todos los archivos que terminan en .txt
ls note*        # todos los que empiezan con "note"
```
```
note_1.txt  note_2.txt  note_3.txt  note_4.txt  note_5.txt
```

> Los comodines no son exclusivos de `ls`. Funcionan con cualquier comando: `rm *.log`, `cp nota_* respaldo/`, `cat report_*.txt`. El shell siempre los expande antes de pasarlos al comando.

---

#### `cp` — Copiar archivos y directorios

**Sintaxis:**
```
cp origen destino           # copia un archivo
cp origen directorio/       # copia dentro de un directorio
cp -r directorio/ destino/  # copia un directorio completo (recursivo)
cp -p origen destino        # preserva permisos y fechas originales
```

**Ejemplo del lab:**
```bash
cp hello.txt hello_copy.txt    # crea una copia en el mismo directorio
mv hello_copy.txt ..           # mueve la copia al directorio padre
```

> `cp` sin `-r` falla con directorios — da el error `omitting directory`. Siempre usa `cp -r` cuando copies carpetas.

---

#### `mv` — Mover o renombrar

**Sintaxis:**
```
mv origen destino_archivo    # renombra el archivo
mv origen directorio/        # mueve el archivo a ese directorio
mv dir1/ dir2/               # mueve o renombra directorios
```

**Qué hace:** Mueve un archivo o directorio a otra ubicación. Si el destino es un nombre de archivo en el mismo directorio, lo renombra. Si el destino es un directorio existente, lo mueve dentro.

**Ejemplo del lab:**
```bash
mv hello_copy.txt ..     # mueve hello_copy.txt al directorio padre
```

**`mv` como herramienta de renombrado:**
```bash
mv informe_final.txt informe_v2.txt    # renombra el archivo
mv carpeta_vieja/ carpeta_nueva/        # renombra el directorio
```

> `mv` no tiene papelera — si mueves un archivo encima de otro que ya existe, el segundo se sobreescribe sin aviso. Usa `mv -i` para que pida confirmación antes de sobreescribir.

---

#### `rm` — Eliminar archivos

**Sintaxis:**
```
rm archivo              # elimina un archivo
rm -r directorio/       # elimina un directorio y todo su contenido
rm -i archivo           # pide confirmación antes de borrar
rm -f archivo           # fuerza la eliminación sin confirmación
```

**Ejemplo del lab:**
```bash
rm file1.txt            # elimina file1.txt permanentemente
```

> **`rm` no tiene papelera.** No hay forma de recuperar lo borrado desde la terminal a menos que tengas un respaldo. Siempre verifica con `ls` antes de `rm`, especialmente con comodines. `rm *.txt` es muy diferente a `rm * .txt` (con espacio — ese espacio borra todo).

---

#### Cómo pedir ayuda al sistema: `--help` y `man`

Uno de los superpoderes de Linux es que trae su propia documentación integrada. No necesitas buscar en internet — el manual está en el sistema.

**`--help` — ayuda rápida**
```
ls --help
cp --help
rm --help
```

Casi todos los comandos de Linux aceptan `--help`. Muestra un resumen de las opciones disponibles directamente en la terminal. Es lo primero que debes intentar cuando no recuerdas una flag.

**`man` — el manual completo**
```
man ls
man cp
man mkdir
```

`man` abre la página del manual completa del comando. Es más detallada que `--help` e incluye ejemplos, advertencias y notas técnicas.

**Cómo navegar dentro de `man`:**

| Tecla | Acción |
|-------|--------|
| `Espacio` o `f` | Avanzar una página |
| `b` | Retroceder una página |
| `/término` | Buscar un término dentro del manual |
| `n` | Ir a la siguiente coincidencia de búsqueda |
| `q` | Salir del manual |

**Ejemplo del lab:**
```bash
man ls    # abre el manual completo de ls
man cp    # abre el manual completo de cp
```

> La diferencia entre un principiante y alguien avanzado no es memorizar todos los flags — es saber dónde buscarlos. `man comando` siempre tiene la respuesta correcta y actualizada para la versión instalada en tu sistema.

---

#### `tail -f /dev/null` — ¿Qué fue eso?

En el lab ejecutaste `tail -f /dev/null` y tuviste que cancelarlo con `Ctrl+C`. Aunque no era el foco del lab, vale la pena entenderlo:

- `tail -f archivo` sigue un archivo en tiempo real — muestra nuevas líneas conforme se agregan (muy útil para monitorear logs)
- `/dev/null` es un dispositivo especial que siempre está vacío y nunca recibe datos
- Combinados: `tail -f /dev/null` espera indefinidamente sin hacer nada — es un truco para mantener un proceso vivo o simplemente bloquear la terminal hasta `Ctrl+C`

> `Ctrl+C` es la forma de interrumpir cualquier proceso que esté corriendo en la terminal. Es la tecla de emergencia más importante de Linux.

---

#### Errores frecuentes — Lab 02

**`cd proyecto` cuando estás en el directorio equivocado**

`cd` usa rutas relativas — busca `proyecto` dentro del directorio actual. Si no estás en el directorio correcto, fallará con `No such file or directory`. Usa `pwd` para saber dónde estás y `ls` para confirmar que el directorio existe antes de entrar.

**`rm *.txt` borra más de lo esperado**

Si hay archivos `.txt` que no querías borrar, ya es tarde. Antes de `rm` con comodines, ejecuta primero `ls *.txt` para ver exactamente qué va a seleccionar el patrón. Solo si la lista es lo que esperas, ejecutas el `rm`.

**`cp hello.txt ..` en vez de `mv hello.txt ..`**

`cp` copia (el original queda), `mv` mueve (el original desaparece). Son operaciones distintas. Si querías mover y usaste `cp`, tienes un duplicado — elimina el original con `rm`.

**`mkdir ruta/anidada` sin `-p`**

Sin `-p`, `mkdir` solo crea el último nivel — y falla si los niveles intermedios no existen. Siempre usa `mkdir -p` cuando crees estructuras de más de un nivel.

---

#### Ejercicio — Lab 02

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Tareas:**

1. Usa `pwd` para confirmar en qué directorio estás.
2. Crea la siguiente estructura de directorios con un solo comando usando `-p`:
   `~/practica/notas/personales/` y `~/practica/notas/trabajo/`
3. Entra a `~/practica/notas/` y crea 5 archivos llamados `semana_{1..5}.txt`.
4. Usa un comodín para listar solo los archivos que empiecen con `semana_`.
5. Copia `semana_1.txt` a la carpeta `personales/` con el nombre `semana_1_copia.txt`.
6. Mueve `semana_5.txt` a la carpeta `trabajo/`.
7. Elimina `semana_2.txt`.
8. Verifica el resultado con `ls -lR ~/practica/`.
9. Consulta el manual de `rm` con `man rm` y busca la flag `-i`. ¿Para qué sirve?

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
pwd

# Paso 2
mkdir -p ~/practica/notas/personales ~/practica/notas/trabajo

# Paso 3
cd ~/practica/notas
touch semana_{1..5}.txt

# Paso 4
ls semana_*

# Paso 5
cp semana_1.txt personales/semana_1_copia.txt

# Paso 6
mv semana_5.txt trabajo/

# Paso 7
rm semana_2.txt

# Paso 8
ls -lR ~/practica/

# Paso 9
man rm
# dentro del manual: /\-i y presiona Enter para buscar
# -i  prompt before every removal
```

</details>

---

### Lab 03 — Cómo Pedir Ayuda en Linux

**Escenario:** Encuentras un comando que nunca has visto, o recuerdas que existe algo para hacer cierta tarea pero no recuerdas cómo se llama. En Linux no tienes que buscar en internet cada vez — el propio sistema trae toda la documentación integrada. Este lab te enseña a leer esa documentación eficientemente.

> Saber usar el sistema de ayuda de Linux es más valioso que memorizar comandos. Los comandos son cientos; la habilidad de encontrar lo que necesitas cuando lo necesitas dura para siempre.

---

#### `type` — Saber qué tipo de comando es

**Sintaxis:**
```
type comando
type -a comando    # muestra todas las ubicaciones donde existe
```

**Qué hace:** Revela la naturaleza de un comando. En Linux, no todos los "comandos" son iguales — algunos están integrados en el shell (built-ins), otros son programas externos en el disco.

**Ejemplo:**
```bash
type cd
```
```
cd is a shell builtin
```

```bash
type ls
```
```
ls is /usr/bin/ls
```

```bash
type echo
```
```
echo is a shell builtin
```

```bash
type python3
```
```
python3 is /usr/bin/python3
```

**Los tres tipos de comandos en Linux:**

| Tipo | Qué es | Ejemplo | Cómo lo reconoce `type` |
|------|--------|---------|------------------------|
| Built-in | Integrado en el shell — no existe como archivo | `cd`, `echo`, `pwd` | `is a shell builtin` |
| Externo | Programa en el disco, ejecutable | `ls`, `grep`, `python3` | `is /ruta/al/programa` |
| Alias | Nombre alternativo definido por el usuario o el sistema | `ll` (alias de `ls -l`) | `is aliased to 'ls -l'` |

**¿Por qué importa saber si es built-in o externo?**

- Los built-ins **no tienen una página `man` propia** — su documentación está en la sección de `man bash`
- Los externos **sí tienen `man`** porque son programas independientes
- Un built-in es **más rápido** que un externo — no hay que leer un archivo del disco

```bash
# Esto no da resultado (cd es built-in):
man cd         # puede redirigir a "man builtins" o no encontrar nada

# Esto sí funciona (ls es externo):
man ls         # página completa
```

> `type` es el comando que debes ejecutar primero cuando te preguntas "¿por qué este comando se comporta raro?" o "¿por qué `man` no encuentra nada?". La respuesta casi siempre está en si es built-in o externo.

---

#### `--help` — Ayuda rápida integrada en el comando

**Sintaxis:**
```
comando --help
comando -h        # en algunos comandos, versión corta de --help
```

**Qué hace:** Le pide al propio comando que imprima un resumen de sus opciones. Es más rápido que abrir `man` cuando solo necesitas recordar el nombre de una flag específica.

**Cuándo usar `--help` vs `man`:**

| Situación | Usa |
|-----------|-----|
| Necesitas recordar una flag rápidamente | `--help` |
| Quieres entender el comando a fondo | `man` |
| El comando es nuevo para ti | `man` |
| Estás en medio de una tarea y no quieres perder el contexto | `--help` |

**Ejemplo:**
```bash
ls --help | grep "\-h"
```
Esto filtra la ayuda de `ls` para encontrar la línea que describe `-h`, sin leer toda la página.

> La combinación `comando --help | grep "lo que busco"` es muy útil cuando la ayuda es larga y sabes aproximadamente qué flag buscas.

---

#### `man` — El manual completo

**Sintaxis:**
```
man comando              # abre el manual del comando
man N comando            # abre la sección N del manual
man -k palabra           # busca páginas relacionadas con esa palabra
```

**Qué hace:** Abre la página del manual del comando indicado. El manual de Linux (`man pages`) es una de las documentaciones técnicas más completas que existen. Fue diseñado para ser la referencia definitiva de cada comando, llamada de sistema y archivo de configuración.

**Estructura de una página `man`:**

Cada página `man` tiene secciones predecibles:

| Sección | Contenido |
|---------|----------|
| `NAME` | Nombre del comando y descripción en una línea |
| `SYNOPSIS` | Sintaxis completa con todos sus argumentos |
| `DESCRIPTION` | Explicación detallada de qué hace |
| `OPTIONS` | Lista de todas las flags con su descripción |
| `EXAMPLES` | Casos de uso (no siempre presente) |
| `SEE ALSO` | Comandos relacionados que podrían interesarte |
| `BUGS` | Comportamientos conocidos o limitaciones |

**Cómo navegar dentro de `man`:**

| Tecla | Acción |
|-------|--------|
| `Espacio` o `f` | Avanzar una página completa |
| `b` | Retroceder una página completa |
| `j` / `k` | Bajar / subir una línea |
| `/término` | Buscar un término hacia adelante |
| `?término` | Buscar un término hacia atrás |
| `n` | Ir a la siguiente coincidencia de búsqueda |
| `N` | Ir a la coincidencia anterior |
| `g` | Ir al inicio del manual |
| `G` | Ir al final del manual |
| `q` | Salir |

**Las 9 secciones del manual de Linux:**

`man` organiza la documentación en secciones numeradas. La sección determina de qué habla la página:

| Sección | Contiene |
|---------|---------|
| 1 | Comandos de usuario (los que usas en terminal) |
| 2 | Llamadas al sistema (del kernel) |
| 3 | Funciones de biblioteca (C, Python, etc.) |
| 4 | Archivos especiales (`/dev/null`, etc.) |
| 5 | Formatos de archivos (`/etc/passwd`, `crontab`, etc.) |
| 6 | Juegos |
| 7 | Miscelánea (convenciones, protocolos) |
| 8 | Comandos de administración del sistema (`root`) |

```bash
man ls          # sección 1 por defecto: comandos de usuario
man 5 crontab   # sección 5: formato del archivo crontab
man 8 useradd   # sección 8: comando de administración
```

> Cuando buscas documentación de un archivo de configuración como `/etc/passwd`, la documentación está en la sección 5: `man 5 passwd`. Sin el `5`, obtendrías la documentación del comando `passwd` (sección 1).

---

#### `apropos` — Buscar comandos por lo que hacen

**Sintaxis:**
```
apropos palabra_clave
apropos "frase con espacios"
```

**Qué hace:** Busca en los títulos y descripciones de todas las páginas `man` instaladas. Si no recuerdas el nombre de un comando pero sabes para qué sirve, `apropos` te da las opciones.

**Ejemplo:**
```bash
apropos compress
```
```
bzip2 (1)           - a block-sorting file compressor
gzip (1)            - compress or expand files
tar (1)             - an archiving utility
zip (1)             - package and compress (archive) files
zcat (1)            - compress or expand files
```

```bash
apropos "disk usage"
```
```
df (1)              - report file system disk space usage
du (1)              - estimate file space usage
```

```bash
apropos network
```
```
ifconfig (8)        - configure a network interface
ip (8)              - show / manipulate routing, network devices...
ping (8)            - send ICMP ECHO_REQUEST to network hosts
ss (8)              - another utility to investigate sockets
```

**`apropos` vs `man -k`:**

Son equivalentes — `apropos palabra` hace exactamente lo mismo que `man -k palabra`:

```bash
apropos compress     # equivalente a:
man -k compress      # misma búsqueda
```

> `apropos` es especialmente útil cuando estás estudiando un tema nuevo. `apropos backup` te muestra todos los comandos relacionados con respaldos. `apropos user` te muestra todo lo relacionado con gestión de usuarios.

**Si `apropos` no devuelve resultados:**

```bash
sudo mandb    # reconstruye la base de datos de man pages
```

En sistemas recién instalados o cuando se instala software nuevo, la base de datos de `apropos` puede estar desactualizada. `mandb` la reconstruye.

---

#### Flujo de diagnóstico — "¿Cómo uso este comando?"

Cuando encuentras un comando desconocido o no recuerdas cómo se usa, sigue este orden:

```
1. type comando
   → ¿Es built-in, externo o alias?
           ↓
2. comando --help
   → Resumen rápido de opciones
   → ¿Es suficiente para lo que necesitas?
       ├── SÍ → ejecuta el comando
       └── NO → continúa
           ↓
3. man comando
   → Documentación completa
   → Busca con /término lo que necesitas
           ↓
4. Si no recuerdas el nombre del comando:
   apropos "lo que quieres hacer"
   → Lista de candidatos con su descripción
```

---

#### Errores frecuentes — Lab 03

**`man cd` no encuentra nada o abre "builtins"**

`cd` es un built-in del shell, no un programa externo. No tiene su propia página `man`. La documentación de los built-ins de Bash está en `man bash` — es larga pero completa. Para ir directo: `man bash` y luego búsqueda con `/^SHELL BUILTIN COMMANDS`.

**`apropos` devuelve "nothing appropriate"**

La base de datos de `man` está desactualizada. Solución: `sudo mandb` para reconstruirla. Esto ocurre frecuentemente en sistemas recién instalados o después de instalar paquetes nuevos.

**`man 5 crontab` vs `man crontab` — confusión de secciones**

`man crontab` (sin número) abre la sección 1 — el comando `crontab`. `man 5 crontab` abre la sección 5 — el **formato del archivo** crontab. Son documentaciones completamente distintas. Si la página no contiene lo que buscas, prueba con otra sección.

**Buscar dentro de `man` con mayúsculas**

La búsqueda con `/término` dentro de `man` distingue mayúsculas y minúsculas por defecto. `/Copy` no encuentra `copy`. Para buscar sin distinción, agrega `-i` al invocar man: `man -P 'less -i' comando` — o simplemente busca en minúsculas.

---

#### Ejercicio — Lab 03

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Tareas:**

1. Usa `type` para investigar estos comandos y anota si cada uno es built-in, externo o alias:
   `echo`, `ls`, `grep`, `pwd`, `cat`, `alias`
2. Usa `ls --help | grep "\-t"` para encontrar qué hace la flag `-t` de `ls` sin abrir el manual completo.
3. Abre `man grep` y navega a la sección `EXAMPLES` usando `/EXAMPLES`. ¿Qué hace el ejemplo con `-i`?
4. Usa `apropos` para encontrar comandos relacionados con "process". ¿Cuántos aparecen?
5. Usa `man -k "file size"` y encuentra qué comando reporta el uso de espacio en disco.
6. Usa `man 5 passwd` y `man 1 passwd` — ¿qué documentan respectivamente?

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
type echo      # shell builtin
type ls        # /usr/bin/ls (externo)
type grep      # /usr/bin/grep (externo)
type pwd       # shell builtin
type cat       # /usr/bin/cat (externo)
type alias     # shell builtin

# Paso 2
ls --help | grep "\-t"
# -t: sort by time, newest first

# Paso 3
man grep
# dentro de man: escribes /EXAMPLES y presionas Enter
# navega hasta el ejemplo con -i (case insensitive)
# presiona q para salir

# Paso 4
apropos process

# Paso 5
man -k "file size"
# verás du (1) - estimate file space usage

# Paso 6
man 5 passwd   # formato del archivo /etc/passwd
man 1 passwd   # el comando passwd para cambiar contraseñas
```

</details>

---

### Lab 04 — Desafío de Operaciones de Archivos

**Escenario:** Este lab es diferente a los anteriores — no es una guía paso a paso, sino un **desafío**: se te entrega una estructura de directorios con archivos y debes reorganizarlos usando solo `rm`, `cp` y `mv`. El objetivo final es que `challenge1/` contenga `challenge2.txt` y `challenge3.txt`, y que `challenge1.txt` haya sido eliminado.

> En los labs anteriores aprendiste los comandos. Este lab simula cómo los usarás en la práctica real: frente a un sistema que no configuraste tú, con rutas que no conoces de memoria, resolviendo sobre la marcha.

---

#### El punto de partida

```
labex:project/ $ ls
challenge1  challenge2  challenge3

labex:project/ $ ls challenge1/
challenge1.txt

labex:project/ $ ls challenge2/
challenge2.txt

labex:project/ $ ls challenge3/
challenge3.txt
```

Estructura inicial:
```
project/
├── challenge1/
│   └── challenge1.txt   ← hay que eliminar este
├── challenge2/
│   └── challenge2.txt   ← hay que copiar este a challenge1/
└── challenge3/
    └── challenge3.txt   ← hay que mover este a challenge1/
```

Estructura final esperada:
```
project/
├── challenge1/
│   ├── challenge2.txt   ✓
│   └── challenge3.txt   ✓
├── challenge2/
│   └── challenge2.txt   (la copia, el original queda)
└── challenge3/
    (challenge3.txt ya no está aquí — fue movido)
```

---

#### Paso 1 — Eliminar `challenge1.txt`

```bash
cd challenge1
ls
```
```
challenge1.txt
```

```bash
rm challenge1.txt
ls
```
```
(vacío — el archivo ya no existe)
```

```bash
cd ..
```

> `rm` elimina el archivo permanentemente. El `ls` posterior confirma que el directorio está vacío — buen hábito de verificación.

---

#### Paso 2 — Copiar `challenge2.txt` a `challenge1/`

Aquí ocurrieron los errores más instructivos del lab:

**Intento 1 — ruta absoluta incorrecta:**
```bash
cp /challenge2/challenge2.txt /home/challenge1/
```
```
cp: cannot stat '/challenge2/challenge2.txt': No such file or directory
```

**¿Por qué falló?** La ruta `/challenge2/` empieza con `/`, lo que significa que busca `challenge2` en la **raíz del sistema** — no en el directorio actual. La carpeta `challenge2/` está en `/home/labex/project/challenge2/`, no en `/challenge2/`.

**Intento 2 — destino inexistente:**
```bash
cp challenge2/challenge2.txt /home/challenge1/
```
```
cp: cannot create regular file '/home/challenge1/': Not a directory
```

**¿Por qué falló?** Esta vez el origen sí estaba bien (ruta relativa correcta), pero el destino `/home/challenge1/` no existe como directorio. `cp` no puede crear directorios que no existen.

**Intento 3 — ambas rutas relativas correctas:**
```bash
cp challenge2/challenge2.txt challenge1/
```
```
(sin error = éxito)
```

**¿Por qué funcionó?** Origen: `challenge2/challenge2.txt` — relativo al directorio actual (`project/`) ✓. Destino: `challenge1/` — el directorio ya existe ✓. `cp` copia el archivo dentro del directorio destino conservando el nombre.

---

#### Paso 3 — Mover `challenge3.txt` a `challenge1/`

```bash
mv challenge3/challenge3.txt challenge1/
```
```
(sin error = éxito)
```

```bash
ls challenge1/
```
```
challenge2.txt  challenge3.txt
```

`mv` tomó el archivo de `challenge3/` y lo dejó en `challenge1/`. A diferencia de `cp`, el original ya no existe en `challenge3/`.

---

#### El mapa mental de rutas — el error más común de este lab

El error más importante del lab fue confundir rutas absolutas y relativas. Este mapa ayuda a entenderlo:

```
/ (raíz del sistema)
└── home/
    └── labex/
        └── project/        ← aquí estás (pwd = /home/labex/project)
            ├── challenge1/
            ├── challenge2/
            └── challenge3/
```

| Lo que escribiste | Dónde busca Linux |
|------------------|------------------|
| `/challenge2/` | En la raíz: `/challenge2/` — no existe |
| `/home/challenge1/` | En `/home/challenge1/` — no existe |
| `challenge2/` | En el dir actual: `/home/labex/project/challenge2/` ✓ |
| `challenge1/` | En el dir actual: `/home/labex/project/challenge1/` ✓ |

**Regla práctica:**
- Si la ruta empieza con `/` → es **absoluta** — busca desde la raíz del sistema
- Si la ruta NO empieza con `/` → es **relativa** — busca desde donde estás ahora

Antes de ejecutar cualquier `cp` o `mv`, ejecuta `ls` con la ruta para confirmar que existe:
```bash
ls challenge2/challenge2.txt    # confirma que el origen existe
ls challenge1/                   # confirma que el destino existe
```

---

#### El typo del lab — `ks` en vez de `ls`

```bash
ks
```
```
zsh: command not found: ks
```

Un error de dedo clásico. El shell es literal — `ks` no es ningún comando y lo dice claramente. No hay que entrar en pánico; simplemente repites el comando correcto. Linux nunca asume lo que quisiste decir.

> Cuando veas `command not found`, lo primero que hay que hacer es releer lo que escribiste. El 90% de las veces es un typo. El otro 10% es que el programa no está instalado.

---

#### Errores frecuentes — Lab 04

**Confundir ruta absoluta con relativa al copiar**

El error `/challenge2/` en vez de `challenge2/` es el más común al empezar. Si el path empieza con `/`, Linux lo busca desde la raíz — que raramente es donde están tus archivos de trabajo. Cuando trabajes en `/home/usuario/proyecto/`, usa siempre rutas relativas para archivos dentro del proyecto.

**`cp` con destino que no existe**

`cp archivo.txt /ruta/que/no/existe/` falla. `cp` no crea directorios — solo copia dentro de directorios que ya existen. Si necesitas crear el destino primero: `mkdir -p destino/ && cp archivo.txt destino/`.

**`mv` cuando querías `cp`**

`mv` elimina el original. Si moviste un archivo y necesitas que el original permanezca donde estaba, tendrás que copiarlo de vuelta. Cuando no estés seguro, usa `cp` primero y borra el original manualmente después de verificar.

**No verificar con `ls` antes de `rm`**

Antes de cualquier `rm`, especialmente con comodines, siempre hacer `ls` primero para ver exactamente qué se va a borrar. `rm challenge1.txt` es seguro porque es un archivo concreto; `rm challenge*` podría borrar más de lo esperado.

---

#### Ejercicio — Lab 04

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Preparación:**
```bash
mkdir -p ~/reto/{entrada,procesado,archivo}
touch ~/reto/entrada/datos_{1..3}.csv
touch ~/reto/entrada/temporal.tmp
```

**Estructura inicial:**
```
reto/
├── entrada/
│   ├── datos_1.csv
│   ├── datos_2.csv
│   ├── datos_3.csv
│   └── temporal.tmp
├── procesado/    (vacío)
└── archivo/      (vacío)
```

**Tareas:**

1. Elimina `temporal.tmp` — no se necesita.
2. Copia `datos_1.csv` a `procesado/` conservando el original en `entrada/`.
3. Mueve `datos_2.csv` y `datos_3.csv` a `archivo/`.
4. Verifica el resultado con `ls -R ~/reto/`.

**Estado final esperado:**
```
reto/
├── entrada/
│   └── datos_1.csv        (original)
├── procesado/
│   └── datos_1.csv        (copia)
└── archivo/
    ├── datos_2.csv
    └── datos_3.csv
```

<details>
<summary>Ver solución</summary>

```bash
cd ~/reto/entrada

# Paso 1
rm temporal.tmp

# Paso 2 (desde ~/reto/)
cd ..
cp entrada/datos_1.csv procesado/

# Paso 3
mv entrada/datos_2.csv archivo/
mv entrada/datos_3.csv archivo/

# Paso 4
ls -R ~/reto/
```

</details>

---

### Lab 05 — Usuarios, Grupos y Permisos

**Escenario:** El sistema Linux que administras lo comparten varias personas. Necesitas crear un nuevo usuario llamado `jack`, organizarlo en un grupo de trabajo, darle acceso `sudo` y asignarle la propiedad de un archivo con los permisos correctos.

> En Linux, **todo tiene un dueño**. Cada archivo pertenece a un usuario y a un grupo. Los permisos determinan qué puede hacer cada quién con ese archivo. Entender este modelo es fundamental — es lo que separa un sistema seguro de uno vulnerable.

---

#### El modelo de usuarios y grupos en Linux

Antes de ver los comandos, es importante entender cómo piensa Linux sobre identidad y acceso:

```
Cada archivo tiene:
  ├── Un usuario dueño   (owner)
  ├── Un grupo dueño     (group)
  └── Permisos para:
        ├── el dueño     (u = user)
        ├── el grupo     (g = group)
        └── todos los demás (o = others)
```

Cada usuario pertenece a:
- Un **grupo primario** — creado automáticamente con el mismo nombre que el usuario
- Cero o más **grupos secundarios** — se agregan manualmente para dar acceso adicional

---

#### `whoami` — Confirmar tu identidad actual

```bash
whoami
```
```
labex
```

**Qué hace:** Imprime el nombre del usuario con el que estás operando en este momento. Es útil cuando cambias de usuario con `su` o cuando trabajas con `sudo` y quieres confirmar con quién estás actuando realmente.

---

#### `id` — Ver información completa de un usuario

**Sintaxis:**
```
id                   # info del usuario actual
id nombre_usuario    # info de otro usuario
```

**Qué hace:** Muestra el UID (User ID), GID (Group ID primario) y todos los grupos a los que pertenece el usuario.

**Ejemplo del lab:**
```bash
id jack
```
```
uid=1000(jack) gid=1000(jack) groups=1000(jack)
```

```bash
id labex
```
```
uid=5000(labex) gid=5000(labex) groups=5000(labex),27(sudo),121(ssl-cert),5002(public)
```

**Cómo leer la salida:**

| Campo | Ejemplo | Significado |
|-------|---------|------------|
| `uid=1000(jack)` | 1000 | Número único de identificación del usuario |
| `gid=1000(jack)` | 1000 | Grupo primario del usuario |
| `groups=...` | `5000(labex),27(sudo)` | Todos los grupos a los que pertenece |

**Lo que revela `id labex` sobre los privilegios:**
- `27(sudo)` — `labex` puede ejecutar comandos como root con `sudo`
- `5002(public)` — pertenece al grupo `public`, que probablemente da acceso a recursos compartidos

> `id` es la forma más rápida de saber exactamente qué privilegios tiene un usuario. Si alguien dice "no tengo acceso a X", `id` te dice si está en el grupo correcto para tenerlo.

---

#### `sudo adduser` — Crear un usuario nuevo (forma interactiva)

**Sintaxis:**
```
sudo adduser nombre_usuario
```

**Qué hace:** Crea un nuevo usuario de forma interactiva. A diferencia de `useradd` (que es más bajo nivel y no configura casi nada solo), `adduser` guía con preguntas: solicita contraseña, nombre completo, y otros datos opcionales. También crea automáticamente el directorio home.

**Ejemplo del lab:**
```bash
sudo adduser jack
```
```
Adding user `jack' ...
Adding new group `jack' (1000) ...
Adding new user `jack' (1000) with group `jack' ...
Creating home directory `/home/jack' ...
New password:
Retype new password:
passwd: password updated successfully
Enter the new value, or press ENTER for the default
    Full Name []:
    Room Number []:
...
Is the information correct? [Y/n] y
```

**Lo que hace `adduser` automáticamente:**
1. Asigna un UID disponible
2. Crea un grupo primario con el mismo nombre y GID
3. Crea el directorio home en `/home/nombre`
4. Copia los archivos base de `/etc/skel/` al home nuevo
5. Solicita contraseña en el momento

**`adduser` vs `useradd`:**

| | `adduser` | `useradd` |
|--|-----------|-----------|
| Interactividad | Hace preguntas | Solo acepta flags |
| Home | Lo crea automáticamente | Necesita `-m` explícito |
| Contraseña | La pide en el momento | Hay que ejecutar `passwd` después |
| Disponibilidad | Debian/Ubuntu | Universal (todas las distros) |
| Uso recomendado | Cuando creas usuarios manualmente | Cuando creas usuarios en scripts |

---

#### `/etc/group` — El archivo que registra todos los grupos

**Sintaxis:**
```
cat /etc/group
cat /etc/group | sort              # ordenado alfabéticamente
cat /etc/group | grep "usuario"    # filtrar grupos de un usuario
```

**Qué hace:** Muestra el archivo de texto donde Linux almacena la definición de todos los grupos del sistema. Cada línea es un grupo.

**Formato de cada línea:**
```
nombre_grupo:contraseña:GID:lista_de_miembros
```

**Ejemplo:**
```
sudo:x:27:labex
developers:x:1001:jack
jack:x:1000:
```

| Campo | Ejemplo | Significado |
|-------|---------|------------|
| `sudo` | nombre del grupo | Identificador del grupo |
| `x` | contraseña | Siempre `x` — las contraseñas de grupo están en `/etc/gshadow` |
| `27` | GID | Número único del grupo |
| `labex` | miembros | Usuarios que pertenecen a este grupo como secundario |

**Del lab — filtrar los grupos de `labex`:**
```bash
cat /etc/group | grep -E "labex"
```
```
sudo:x:27:labex
ssl-cert:x:121:labex
labex:x:5000:
public:x:5002:labex
```

Esto muestra que `labex` aparece como miembro en `sudo`, `ssl-cert` y `public`, y que tiene su propio grupo primario `labex` con GID 5000.

> El flag `-E` en `grep` activa las **expresiones regulares extendidas** — permite patrones más complejos con `|`, `+`, `?`. Para búsquedas simples como esta, `grep "labex"` sin `-E` funciona igual, pero `-E` es buena práctica cuando el patrón puede crecer.

---

#### `sudo groupadd` — Crear un grupo nuevo

**Sintaxis:**
```
sudo groupadd nombre_grupo
```

**Qué hace:** Crea un nuevo grupo en el sistema. El grupo queda registrado en `/etc/group` con el siguiente GID disponible.

**Ejemplo del lab:**
```bash
sudo groupadd developers
```
```
(sin salida = éxito)
```

Verificar que se creó:
```bash
cat /etc/group | grep developers
```
```
developers:x:1001:
```

---

#### `sudo usermod -aG` — Agregar un usuario a un grupo

**Sintaxis:**
```
sudo usermod -aG grupo usuario
sudo usermod -aG grupo1,grupo2 usuario    # varios grupos a la vez
```

**Qué hace:** Modifica la configuración del usuario para agregarlo a un grupo adicional. El flag `-a` (append) es crítico — sin él, `-G` reemplaza todos los grupos secundarios del usuario por los que especifiques.

**Ejemplo del lab:**
```bash
sudo usermod -aG developers jack
groups jack
```
```
jack : jack developers
```

```bash
sudo usermod -aG sudo jack
groups jack
```
```
jack : jack sudo developers
```

**La diferencia entre `-aG` y `-G`:**

```bash
# SEGURO — agrega "developers" sin tocar los demás grupos
sudo usermod -aG developers jack

# PELIGROSO — jack pierde TODOS sus grupos anteriores, solo queda "developers"
sudo usermod -G developers jack
```

> Agregar a un usuario al grupo `sudo` le da capacidad de ejecutar cualquier comando como root con `sudo`. Es el equivalente Linux de "hacer administrador" a alguien. Hazlo solo con usuarios de confianza.

---

#### `groups` — Ver los grupos de un usuario

**Sintaxis:**
```
groups                   # grupos del usuario actual
groups nombre_usuario    # grupos de otro usuario
```

**Ejemplo del lab:**
```bash
groups jack
```
```
jack : jack sudo developers
```

El formato es: `usuario : grupo_primario grupos_secundarios...`

---

#### `ls -l` — Leer los permisos de archivos

**Ejemplo del lab:**
```bash
ls -l /home
```
```
drwxr-x--- 2 jack  jack    57 Apr  9 10:35 jack
drwxr-x--- 1 labex labex 4096 Apr  9 10:42 labex
```

```bash
ls -l /home/labex/testfile
```
```
-rw-rw-r-- 1 labex labex 0 Apr  9 10:43 /home/labex/testfile
```

**Cómo leer la columna de permisos:**

```
-rw-rw-r--
│└──┘└──┘└──┘
│  u   g   o
│
└── tipo: - archivo, d directorio, l enlace simbólico
```

| Posición | Caracteres | Para quién | Significado |
|----------|-----------|-----------|------------|
| 1 | `-` o `d` o `l` | — | Tipo de entrada |
| 2-4 | `rw-` | Usuario dueño (u) | r=leer, w=escribir, x=ejecutar |
| 5-7 | `rw-` | Grupo dueño (g) | r=leer, w=escribir, x=ejecutar |
| 8-10 | `r--` | Todos los demás (o) | r=leer, w=escribir, x=ejecutar |

**Ejemplos comunes:**

| Permisos | Numérico | Quién puede qué |
|----------|---------|----------------|
| `rwxr-xr-x` | 755 | Dueño: todo. Grupo y otros: leer y ejecutar |
| `rw-r--r--` | 644 | Dueño: leer y escribir. Grupo y otros: solo leer |
| `rwxr-x---` | 750 | Dueño: todo. Grupo: leer y ejecutar. Otros: nada |
| `rw-rw-r--` | 664 | Dueño y grupo: leer y escribir. Otros: solo leer |

---

#### `sudo chown` — Cambiar el dueño de un archivo

**Sintaxis:**
```
sudo chown usuario archivo
sudo chown usuario:grupo archivo      # cambia usuario y grupo a la vez
sudo chown :grupo archivo             # cambia solo el grupo
sudo chown -R usuario:grupo carpeta/  # recursivo
```

**Ejemplo del lab:**
```bash
ls -l /home/labex/testfile
```
```
-rw-rw-r-- 1 labex labex 0 Apr  9 10:43 /home/labex/testfile
```

```bash
sudo chown jack:jack /home/labex/testfile
ls -l /home/labex/testfile
```
```
-rw-rw-r-- 1 jack jack 0 Apr  9 10:43 /home/labex/testfile
```

El archivo ahora pertenece a `jack` tanto como usuario como grupo. `labex` ya no es el dueño — si quisiera modificar el archivo ahora, no podría (a menos que tenga sudo o pertenezca al grupo `jack`).

---

#### `sudo chmod` — Cambiar los permisos de un archivo

**Sintaxis:**
```
sudo chmod 750 archivo        # notación numérica
sudo chmod u+x archivo        # notación simbólica: agrega ejecutar al dueño
sudo chmod go-w archivo       # quita escritura a grupo y otros
sudo chmod -R 755 directorio/ # recursivo
```

**Cómo calcular el número de permisos:**

Cada permiso tiene un valor:

| Permiso | Valor |
|---------|-------|
| `r` (leer) | 4 |
| `w` (escribir) | 2 |
| `x` (ejecutar) | 1 |
| `-` (ninguno) | 0 |

Se suman para cada grupo (usuario, grupo, otros):

```
750:
  7 = 4+2+1 = rwx   (dueño: todo)
  5 = 4+0+1 = r-x   (grupo: leer y ejecutar)
  0 = 0+0+0 = ---   (otros: nada)
```

**Ejemplo del lab:**
```bash
sudo chmod 750 /home/labex/testfile
ls -l /home/labex/testfile
```
```
-rwxr-x--- 1 jack jack 0 Apr  9 10:43 /home/labex/testfile
```

> Nota que el archivo era de tamaño 0 (vacío) pero ahora tiene `x` (ejecutar). `chmod` no verifica si tiene sentido para el tipo de archivo — simplemente aplica lo que le pides.

**Tabla de permisos más usados:**

| Número | Simbólico | Uso típico |
|--------|----------|-----------|
| `644` | `rw-r--r--` | Archivos de texto, documentos |
| `755` | `rwxr-xr-x` | Programas, scripts ejecutables públicos |
| `750` | `rwxr-x---` | Scripts de equipo (grupo puede ejecutar, otros no) |
| `700` | `rwx------` | Scripts privados, claves privadas |
| `664` | `rw-rw-r--` | Archivos compartidos de equipo |
| `600` | `rw-------` | Archivos muy sensibles (ej. `~/.ssh/id_rsa`) |

---

#### Flujo completo del lab

```
1. whoami / id labex           → Confirmar identidad y grupos actuales
        ↓
2. sudo adduser jack           → Crear usuario con home y contraseña
        ↓
3. id jack                     → Verificar UID, GID y grupos del nuevo usuario
        ↓
4. sudo groupadd developers    → Crear grupo de trabajo
        ↓
5. sudo usermod -aG developers jack  → Agregar jack al grupo
   sudo usermod -aG sudo jack        → Dar privilegios sudo a jack
        ↓
6. groups jack                 → Verificar que los grupos quedaron bien
        ↓
7. touch testfile              → Crear archivo de prueba
   sudo chown jack:jack testfile → Transferir propiedad a jack
   sudo chmod 750 testfile     → Establecer permisos adecuados
        ↓
8. ls -l testfile              → Confirmar dueño y permisos finales
```

---

#### Errores frecuentes — Lab 05

**`usermod -G grupo usuario` sin `-a`**

Sin el flag `-a`, el usuario pierde todos sus grupos secundarios anteriores. `sudo usermod -G developers jack` deja a jack solo en `developers` — perdería `sudo` si ya lo tenía. Siempre `usermod -aG`.

**`chown usuario archivo` sin `sudo`**

Solo root puede cambiar el dueño de un archivo. Sin `sudo`, recibirás `Operation not permitted`. Esto es por diseño de seguridad — si cualquier usuario pudiera cambiar dueños, podría apropiarse de archivos ajenos.

**`chmod 777` como solución rápida**

`777` significa que cualquier usuario del sistema puede leer, modificar y ejecutar el archivo. Nunca es la respuesta correcta en un entorno real — siempre existe un permiso más restrictivo que cumple el mismo objetivo.

**Confundir `adduser` (interactivo) con `useradd` (programático)**

En scripts, `adduser` puede colgar esperando respuesta interactiva. En scripts, usa `useradd -m -s /bin/bash usuario` y `echo "usuario:contraseña" | chpasswd` para automatizar.

---

#### Ejercicio — Lab 05

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux con sudo.

**Tareas:**

1. Crea un usuario llamado `alice` con `sudo adduser alice`.
2. Crea un grupo llamado `equipo`.
3. Agrega a `alice` al grupo `equipo` usando `usermod -aG`.
4. Verifica con `groups alice` que quedó en el grupo correcto.
5. Crea el archivo `~/proyecto.sh` con `touch`.
6. Cambia el dueño del archivo a `alice:equipo`.
7. Establece permisos `750` en el archivo.
8. Usa `ls -l` para confirmar que el archivo tiene los permisos y dueño correctos.
9. Usa `id alice` para ver toda la información del usuario que creaste.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
sudo adduser alice

# Paso 2
sudo groupadd equipo

# Paso 3
sudo usermod -aG equipo alice

# Paso 4
groups alice

# Paso 5
touch ~/proyecto.sh

# Paso 6
sudo chown alice:equipo ~/proyecto.sh

# Paso 7
sudo chmod 750 ~/proyecto.sh

# Paso 8
ls -l ~/proyecto.sh
# -rwxr-x--- 1 alice equipo 0 ... proyecto.sh

# Paso 9
id alice
```

</details>

---

### Lab 06 — Crear Usuarios con Configuración Precisa

**Escenario:** Necesitas incorporar a dos desarrolladores: `jack` del equipo de desarrollo y `bob` del equipo de testing. Cada uno debe tener su propio directorio home, pertenecer al grupo primario de su equipo, y compartir acceso al grupo común `labex`. Todo sin interacción manual — la configuración debe especificarse de una vez en el comando.

> El Lab 05 usó `adduser`, que hace preguntas y configura cosas por defecto. Este lab usa `useradd` con flags específicos — el enfoque de un administrador que sabe exactamente qué quiere y no necesita que el sistema le pregunte.

---

#### `useradd` con flags — Crear usuarios sin interacción

**Sintaxis:**
```
sudo useradd [opciones] nombre_usuario
```

**Qué hace:** Crea un usuario en el sistema con la configuración que especifiques mediante flags. A diferencia de `adduser`, no hace preguntas — todo se define en el comando. Esto lo hace ideal para scripts y automatización.

**Flags usadas en el lab:**

| Flag | Nombre | Qué configura |
|------|--------|--------------|
| `-m` | `--create-home` | Crea el directorio home si no existe |
| `-d /ruta` | `--home-dir` | Especifica la ruta del directorio home |
| `-g grupo` | `--gid` | Establece el **grupo primario** del usuario |
| `-G grupo1,grupo2` | `--groups` | Establece los **grupos secundarios** |

---

#### Crear los grupos primarios primero

```bash
sudo groupadd dev
sudo groupadd test
```

Los grupos deben existir antes de asignarlos como grupo primario con `-g`. Si intentas usar `-g dev` y el grupo `dev` no existe, `useradd` fallará con error.

---

#### Crear `jack` — desarrollador

```bash
sudo useradd -m -d /home/jack -g dev -G labex jack
```

Desglosado:

| Parte | Efecto |
|-------|--------|
| `-m` | Crea `/home/jack/` si no existe |
| `-d /home/jack` | El home de jack es exactamente `/home/jack` |
| `-g dev` | Grupo **primario**: `dev` — es el grupo que aparecerá en los archivos que crea |
| `-G labex` | Grupo **secundario**: `labex` — acceso adicional a recursos de ese grupo |
| `jack` | Nombre del usuario |

**Verificar:**
```bash
id jack
```
```
uid=5001(jack) gid=5003(dev) groups=5003(dev),5000(labex)
```

La salida confirma exactamente lo que pedimos:
- `gid=5003(dev)` → grupo primario es `dev`
- `groups=5003(dev),5000(labex)` → pertenece a `dev` y a `labex`

---

#### Crear `bob` — tester

```bash
sudo useradd -m -d /home/bob -g test -G labex bob
```

Mismo patrón, diferente equipo:

```bash
id bob
```
```
uid=5002(bob) gid=5004(test) groups=5004(test),5000(labex)
```

- `gid=5004(test)` → grupo primario es `test`
- `groups=5004(test),5000(labex)` → pertenece a `test` y a `labex`

---

#### `-g` vs `-G` — la distinción más importante de este lab

Esta diferencia causa confusión constantemente porque las flags se parecen:

| Flag | Mayúscula/Minúscula | Qué hace | ¿Cuántos grupos acepta? |
|------|--------------------|---------|-----------------------|
| `-g` | minúscula | Grupo **primario** — uno solo | Exactamente uno |
| `-G` | MAYÚSCULA | Grupos **secundarios** | Uno o varios separados por coma |

```bash
# Un solo grupo primario:
sudo useradd -g dev jack

# Varios grupos secundarios:
sudo useradd -G labex,docker,git jack

# Ambos combinados:
sudo useradd -g dev -G labex,docker jack
```

**¿Qué hace el grupo primario en la práctica?**

Cuando `jack` crea un archivo, ese archivo hereda el grupo primario de `jack`:
```bash
# Jack crea un archivo
touch /tmp/codigo.py
ls -l /tmp/codigo.py
# -rw-rw-r-- 1 jack dev 0 ... codigo.py
#                    ^^^
#              grupo primario "dev"
```

El grupo primario es el que "firma" los archivos que crea el usuario. Los grupos secundarios son para acceder a recursos de otros — directorios, dispositivos, servicios.

---

#### `useradd` completo — flags más usadas

Además de las del lab, estas son las flags más frecuentes:

| Flag | Qué hace | Ejemplo |
|------|---------|---------|
| `-m` | Crear home | `useradd -m usuario` |
| `-d /ruta` | Ruta del home | `useradd -d /srv/usuario usuario` |
| `-g grupo` | Grupo primario | `useradd -g developers usuario` |
| `-G grupos` | Grupos secundarios | `useradd -G sudo,docker usuario` |
| `-s /bin/bash` | Shell por defecto | `useradd -s /bin/bash usuario` |
| `-c "Nombre Apellido"` | Comentario/nombre real | `useradd -c "Jack Smith" jack` |
| `-e YYYY-MM-DD` | Fecha de expiración | `useradd -e 2026-12-31 usuario` |

**Comando completo típico en producción:**
```bash
sudo useradd -m -d /home/jack -g dev -G labex,sudo -s /bin/bash -c "Jack Smith" jack
sudo passwd jack    # asignar contraseña por separado
```

> `useradd` no asigna contraseña — hay que hacerlo con `passwd` después. Sin contraseña, la cuenta existe pero el usuario no puede iniciar sesión con ella.

---

#### Comparativa final: `adduser` vs `useradd`

| Característica | `adduser` | `useradd -m -d ... -g ... -G ...` |
|---------------|-----------|----------------------------------|
| Interacción | Pide datos en pantalla | Todo por flags en el comando |
| Contraseña | La pide en el momento | Hay que ejecutar `passwd` después |
| Home | Lo crea automáticamente | Necesita `-m` explícito |
| Shell | Configura bash por defecto | Puede quedar en `/bin/sh` sin `-s` |
| Ideal para | Uso manual, un usuario a la vez | Scripts, automatización, configuración precisa |
| Disponibilidad | Solo Debian/Ubuntu | Todas las distribuciones Linux |

---

#### Errores frecuentes — Lab 06

**`useradd -g grupo` cuando el grupo no existe todavía**

Si el grupo no fue creado previamente con `groupadd`, `useradd` falla con `invalid group name`. El orden correcto es siempre: primero `groupadd`, luego `useradd`.

**Confundir `-g` (minúscula) con `-G` (mayúscula)**

`-g dev` establece `dev` como grupo primario. `-G dev` lo agrega como grupo secundario. Usar `-G` cuando quieres el grupo primario resulta en que el usuario queda con un grupo primario diferente al que esperabas.

**`useradd` sin `-m` — home que no existe**

Si omites `-m`, el usuario existe en el sistema pero no tiene directorio home. Al iniciar sesión, el shell puede arrancar en `/` o dar un warning. Siempre usa `-m` a menos que el home ya exista o no sea necesario.

**No ejecutar `passwd` después de `useradd`**

Con `useradd`, la cuenta queda bloqueada hasta que se asigne una contraseña. El usuario no podrá iniciar sesión hasta que ejecutes `sudo passwd nombre_usuario`.

---

#### Ejercicio — Lab 06

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux con sudo.

**Tareas:**

Crea la siguiente estructura de usuarios y grupos usando solo `groupadd` y `useradd` con flags (sin `adduser`):

| Usuario | Home | Grupo primario | Grupos secundarios |
|---------|------|---------------|-------------------|
| `ana` | `/home/ana` | `backend` | `labex` |
| `luis` | `/home/luis` | `frontend` | `labex` |

1. Crea los grupos `backend` y `frontend` con `groupadd`.
2. Crea los usuarios `ana` y `luis` con `useradd` usando `-m`, `-d`, `-g` y `-G`.
3. Verifica con `id ana` e `id luis` que los grupos son los correctos.
4. Asigna contraseñas a ambos usuarios con `sudo passwd`.
5. Usa `cat /etc/group | grep -E "backend|frontend|labex"` para ver los grupos resultantes.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
sudo groupadd backend
sudo groupadd frontend

# Paso 2
sudo useradd -m -d /home/ana -g backend -G labex ana
sudo useradd -m -d /home/luis -g frontend -G labex luis

# Paso 3
id ana
id luis

# Paso 4
sudo passwd ana
sudo passwd luis

# Paso 5
cat /etc/group | grep -E "backend|frontend|labex"
```

</details>

---

### Lab 07 — El Sistema de Archivos y Búsqueda

**Escenario:** Para trabajar con Linux con confianza necesitas dos cosas: entender el mapa del territorio (la estructura de directorios del sistema) y saber buscar cuando no encuentras algo. Este lab cubre ambas: exploras la raíz del sistema, practicas todas las variantes de navegación, aprendes a crear archivos multilínea, y dominas `find` para localizar cualquier cosa en el sistema.

> El sistema de archivos de Linux no es un disco caótico — es una estructura definida por un estándar llamado FHS (Filesystem Hierarchy Standard). Cada directorio tiene un propósito específico y saber qué hay en cada uno te da contexto para entender cómo funciona el sistema.

---

#### La raíz del sistema — `ls -l /`

```bash
cd /
ls -l
```

La salida del lab reveló el mapa completo del sistema. Cada directorio de la raíz tiene una función específica:

| Directorio | Propósito |
|-----------|----------|
| `/bin → usr/bin` | Comandos esenciales de usuario — `ls`, `cp`, `cat`, etc. (enlace simbólico) |
| `/boot` | Archivos del gestor de arranque y kernel |
| `/dev` | Dispositivos del sistema — discos, terminales, `/dev/null` |
| `/etc` | Configuración del sistema — `passwd`, `group`, `crontab`, `nginx.conf` |
| `/home` | Directorios personales de los usuarios |
| `/lib → usr/lib` | Bibliotecas compartidas que usan los programas |
| `/media` | Punto de montaje para dispositivos extraíbles (USB, CD) |
| `/mnt` | Punto de montaje manual para sistemas de archivos temporales |
| `/opt` | Software adicional instalado opcionalmente |
| `/proc` | Sistema de archivos virtual — información en tiempo real del kernel y procesos |
| `/root` | Home del superusuario (root) — separado de `/home` |
| `/run` | Datos de procesos en ejecución — se limpia al reiniciar |
| `/sbin → usr/sbin` | Comandos de administración del sistema (para root) |
| `/srv` | Datos de servicios del servidor — HTTP, FTP, etc. |
| `/sys` | Sistema de archivos virtual — información del hardware y kernel |
| `/tmp` | Archivos temporales — se borran al reiniciar (permisos `rwxrwxrwt`) |
| `/usr` | Programas, librerías y datos de los usuarios |
| `/var` | Datos variables — logs, bases de datos, colas de correo |

**Cosas notables de la salida del lab:**

```
lrwxrwxrwx 1 root root 7 Jun 27  2024 bin -> usr/bin
```
La `l` al inicio indica **enlace simbólico** — `/bin` no es un directorio real, apunta a `/usr/bin`. En Linux moderno, `/bin`, `/lib`, `/sbin` son todos enlaces a sus equivalentes en `/usr/`.

```
drwxrwxrwt 1 root root 119 Apr  9 11:30 tmp
```
La `t` al final de `rwxrwxrwt` es el **sticky bit** — en `/tmp` cualquiera puede crear archivos, pero nadie puede borrar los de otro usuario.

```
drwxrwxrwx 1 root public 49 Jul 18  2024 opt
```
`/opt` tiene grupo `public` y permisos `777` en este entorno LabEx — todos los usuarios pueden escribir ahí.

---

#### Navegación avanzada — repaso con contexto real

El lab practicó todas las formas de `cd` juntas:

```bash
# Ruta relativa desde home
mkdir -p ~/project/practice/subdirectory
cd ~/project/practice/subdirectory
pwd    # /home/labex/project/practice/subdirectory

# Subir un nivel (relativa)
cd ..
pwd    # /home/labex/project/practice

# Ruta absoluta completa
cd /home/labex/project/practice/subdirectory
pwd    # /home/labex/project/practice/subdirectory

# Ir al home
cd ~
pwd    # /home/labex

# Volver al directorio anterior (como el botón atrás)
cd -   # vuelve a /home/labex/project/practice/subdirectory

# cd sin argumentos = cd ~
cd
pwd    # /home/labex
```

> `cd -` es el atajo más subestimado. Cuando saltas entre dos directorios distantes (ej. `/etc/nginx/` y `/var/log/nginx/`), `cd -` alterna entre ambos sin tener que escribir las rutas largas cada vez.

---

#### `tree` — Ver la estructura en árbol

**Sintaxis:**
```
tree                     # árbol del directorio actual
tree ruta/               # árbol de una ruta específica
tree -L N                # limitar la profundidad a N niveles
tree -a                  # incluir archivos ocultos
tree -d                  # solo directorios (sin archivos)
```

**Qué hace:** Muestra la estructura de directorios y archivos de forma visual en árbol. Mucho más legible que `ls -R` para entender jerarquías.

**Ejemplo del lab:**
```bash
mkdir -p nested/structure/example
tree nested
```
```
nested
└── structure
    └── example

2 directories, 0 files
```

```bash
cp -r nested dir1/
tree dir1
```
```
dir1
├── file1.txt
└── nested
    └── structure
        └── example

3 directories, 1 file
```

> `tree` no siempre viene instalado. Si no está: `sudo apt install tree`. Es uno de los primeros paquetes que se instalan en un servidor nuevo — facilita enormemente auditar estructuras de directorios.

---

#### Here-document — Crear archivos multilínea desde la terminal

**Sintaxis:**
```bash
cat << EOF > archivo.txt
línea 1
línea 2
línea 3
EOF
```

**Qué hace:** El operador `<<` le dice a `cat` que lea su entrada hasta encontrar la palabra indicada (`EOF` en este caso). Todo lo que escribas entre `<< EOF` y la línea `EOF` se convierte en el contenido del archivo.

**Ejemplo del lab:**
```bash
cat << EOF > multiline.txt
Line 1: Hello, Linux
Line 2: This is a multiline file.
Line 3: Created using a here-document.
EOF
```

```bash
cat multiline.txt
```
```
Line 1: Hello, Linux
Line 2: This is a multiline file.
Line 3: Created using a here-document.
```

**Comparativa de formas de crear contenido en archivos:**

| Método | Cuándo usarlo |
|--------|--------------|
| `echo "texto" > archivo` | Una sola línea, sobreescribe |
| `echo "texto" >> archivo` | Una sola línea, agrega al final |
| `cat << EOF > archivo` | Varias líneas de una vez |
| `nano archivo` | Edición interactiva con interfaz visual |

**`EOF` no es especial — es solo la palabra de cierre:**
```bash
cat << FIN > nota.txt
Esta es mi nota.
FIN
# También funciona con STOP, DONE, o cualquier palabra
```

> El here-document es muy útil en scripts cuando necesitas crear archivos de configuración con múltiples líneas. En vez de `echo` repetido o un editor interactivo, defines todo el contenido de una vez.

---

#### `nl` — Numerar las líneas de un archivo

**Sintaxis:**
```
nl archivo
nl -b a archivo    # numera también las líneas vacías
nl -n rz archivo   # números con ceros a la izquierda (001, 002...)
```

**Qué hace:** Muestra el contenido de un archivo añadiendo el número de línea al principio de cada una.

**Ejemplo del lab:**
```bash
nl multiline.txt
```
```
     1	Line 1: Hello, Linux
     2	Line 2: This is a multiline file.
     3	Line 3: Created using a here-document.
```

**`nl` vs `cat -n`:**

```bash
nl multiline.txt       # no numera líneas vacías por defecto
cat -n multiline.txt   # numera todas las líneas incluyendo vacías
```

> `nl` es útil para revisar logs o archivos de configuración cuando necesitas referenciar líneas específicas. "El error está en la línea 47" es mucho más fácil de localizar con `nl` que contando manualmente.

---

#### `head` y `tail` — Ver partes específicas de un archivo

**Sintaxis:**
```
head -n N archivo      # primeras N líneas
tail -n N archivo      # últimas N líneas
tail -f archivo        # modo seguimiento en tiempo real
```

**Ejemplo del lab:**
```bash
head -n 2 multiline.txt
```
```
Line 1: Hello, Linux
Line 2: This is a multiline file.
```

```bash
tail -n 1 multiline.txt
```
```
Line 3: Created using a here-document.
```

**Cuándo usar cada uno:**

| Comando | Caso de uso típico |
|---------|------------------|
| `head -n 20 archivo` | Ver el encabezado de un CSV o log |
| `tail -n 50 /var/log/syslog` | Ver los últimos 50 eventos del log |
| `tail -f /var/log/nginx/access.log` | Monitorear un log en tiempo real |

---

#### `find` — Buscar archivos en el sistema

**Sintaxis:**
```
find ruta [criterios]
```

**Qué hace:** Recorre el sistema de archivos desde la ruta indicada y devuelve todos los archivos que cumplan los criterios. Es la herramienta de búsqueda más poderosa de Linux — puede buscar por nombre, tipo, tamaño, fecha, permisos y más.

**Criterios más usados:**

| Criterio | Ejemplo | Qué busca |
|----------|---------|----------|
| `-name "patrón"` | `-name "*.txt"` | Archivos cuyo nombre coincida |
| `-iname "patrón"` | `-iname "readme*"` | Igual pero sin distinción de mayúsculas |
| `-type f` | `-type f` | Solo archivos regulares |
| `-type d` | `-type d` | Solo directorios |
| `-size +N` | `-size +1M` | Archivos de más de N tamaño |
| `-size -N` | `-size -100k` | Archivos de menos de N tamaño |
| `-mtime -N` | `-mtime -1` | Modificados en los últimos N días |
| `-mtime +N` | `-mtime +30` | Modificados hace más de N días |
| `-user nombre` | `-user jack` | Archivos cuyo dueño es ese usuario |

**Ejemplo 1 — buscar por extensión en el directorio actual:**
```bash
find . -name "*.txt"
```
```
./dir1/file1.txt
./dir2/file2_copy.txt
./dir3/renamed_file.txt
./file2.txt
./multiline.txt
./test.txt
```

**Ejemplo 2 — buscar en todo el sistema (requiere sudo):**
```bash
sudo find / -name "passwd"
```
```
/etc/pam.d/passwd
/etc/passwd
/home/labex/.vnc/passwd
/usr/bin/passwd
find: '/proc/24/map_files': Permission denied
find: '/proc/36/map_files': Permission denied
...
```

Los mensajes `Permission denied` en `/proc/` son normales — incluso con `sudo`, algunos subdirectorios de `/proc/` tienen restricciones especiales del kernel. Los resultados útiles (`/etc/passwd`, `/usr/bin/passwd`) sí aparecen.

**Suprimir los mensajes de error:**
```bash
sudo find / -name "passwd" 2>/dev/null
```
```
/etc/pam.d/passwd
/etc/passwd
/home/labex/.vnc/passwd
/usr/bin/passwd
```

`2>/dev/null` redirige los mensajes de error (`stderr`) a la papelera — la búsqueda funciona igual pero la salida es limpia.

**Ejemplo 3 — buscar por tamaño:**
```bash
find ~ -size +1M
```
Busca archivos de más de 1 MB en tu home. Útil para encontrar archivos que ocupan mucho espacio.

**Ejemplo 4 — buscar archivos modificados recientemente:**
```bash
find ~ -mtime -1
```
Archivos modificados en las últimas 24 horas — útil para auditar qué cambió.

---

#### `which` — Encontrar la ubicación de un ejecutable

**Sintaxis:**
```
which comando
which -a comando    # muestra todas las ubicaciones si hay varias
```

**Qué hace:** Busca en los directorios del `PATH` del sistema y devuelve la ruta completa del ejecutable que se usaría al escribir ese comando.

**Ejemplo del lab:**
```bash
which python
```
```
/usr/bin/python
```

```bash
which python3
```
```
/usr/bin/python3
```

**Cuándo usar `which`:**
- Para saber qué versión de un programa se ejecuta: `which python` vs `which python3`
- Para confirmar que un programa está instalado y en el PATH
- Para detectar si hay dos versiones de un programa instaladas

**`which` vs `type` vs `find`:**

| Comando | Busca | Resultado |
|---------|-------|----------|
| `which python3` | En el PATH del sistema | `/usr/bin/python3` |
| `type python3` | Igual + aliases y built-ins | `python3 is /usr/bin/python3` |
| `find / -name "python3"` | En todo el sistema de archivos | Todas las copias, incluyendo fuera del PATH |

> `which` es la forma rápida de responder "¿qué programa corre cuando escribo este comando?". Si escribes `python` y no sabes si es Python 2 o Python 3, `which python` + `python --version` te da la respuesta definitiva.

---

#### `nano` — Editor de texto en la terminal

**Sintaxis:**
```
nano archivo          # abrir o crear un archivo para editar
```

**Qué hace:** Abre un editor de texto simple directamente en la terminal. A diferencia de `vim` o `emacs`, `nano` muestra los atajos disponibles en la parte inferior — ideal para principiantes.

**Controles básicos de `nano`:**

| Atajo | Acción |
|-------|--------|
| `Ctrl + O` | Guardar (O = "Write Out") |
| `Enter` | Confirmar el nombre del archivo al guardar |
| `Ctrl + X` | Salir |
| `Ctrl + K` | Cortar la línea actual |
| `Ctrl + U` | Pegar |
| `Ctrl + W` | Buscar texto |
| `Ctrl + G` | Mostrar ayuda |

> `nano` siempre muestra los atajos en la barra inferior — el `^` representa `Ctrl`. Si ves `^O Write Out`, significa `Ctrl+O` para guardar.

---

#### Errores frecuentes — Lab 07

**`find / -name "archivo"` sin `sudo` da miles de "Permission denied"**

Sin `sudo`, `find` no puede acceder a directorios restringidos (como `/root/`, `/proc/PID/`). El resultado se mezcla con errores. Solución: `sudo find / -name "archivo" 2>/dev/null` para buscar con privilegios y suprimir los errores de permisos.

**`cat << EOF` — la línea `EOF` debe estar sola al inicio**

Si la línea de cierre tiene espacios antes (`  EOF` con espacios) o después (`EOF  ` con espacios), el here-document no cierra y el terminal queda esperando. El `EOF` de cierre debe estar al inicio de la línea, solo, sin espacios alrededor.

**`tree` no está instalado**

`tree` no viene en todas las distribuciones. Si ves `command not found: tree`, instálalo con `sudo apt install tree`.

**`find . -name *.txt` sin comillas**

Sin comillas, el shell expande `*.txt` antes de pasárselo a `find` — si hay archivos `.txt` en el directorio actual, `find` recibe solo esos nombres en vez del patrón. Siempre: `find . -name "*.txt"` con comillas para que el patrón llegue intacto a `find`.

---

#### Ejercicio — Lab 07

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Preparación:**
```bash
mkdir -p ~/lab7/{documentos,imagenes,scripts}
echo "Reporte mensual" > ~/lab7/documentos/reporte.txt
echo "Datos crudos" > ~/lab7/documentos/datos.csv
echo "#!/bin/bash" > ~/lab7/scripts/deploy.sh
touch ~/lab7/imagenes/foto.png
```

**Tareas:**

1. Usa `tree ~/lab7/` para ver la estructura completa.
2. Crea un archivo multilínea `~/lab7/notas.txt` con 3 líneas usando here-document.
3. Usa `nl` para ver el contenido de `notas.txt` con números de línea.
4. Usa `head -n 1` y `tail -n 1` para ver solo la primera y última línea.
5. Usa `find ~/lab7 -name "*.txt"` para listar todos los archivos de texto.
6. Usa `find ~/lab7 -type d` para listar solo los directorios.
7. Usa `which bash` para encontrar dónde está el intérprete bash.
8. Usa `find ~/lab7 -mtime -1` para ver qué archivos modificaste hoy.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
tree ~/lab7/

# Paso 2
cat << EOF > ~/lab7/notas.txt
Nota 1: Completar el reporte
Nota 2: Revisar los datos
Nota 3: Desplegar la app
EOF

# Paso 3
nl ~/lab7/notas.txt

# Paso 4
head -n 1 ~/lab7/notas.txt
tail -n 1 ~/lab7/notas.txt

# Paso 5
find ~/lab7 -name "*.txt"

# Paso 6
find ~/lab7 -type d

# Paso 7
which bash

# Paso 8
find ~/lab7 -mtime -1
```

</details>

---

### Lab 08 — Variables de Entorno

**Escenario:** Quieres entender cómo Linux "recuerda" configuraciones entre comandos y sesiones. Creas tu propia variable, descubres que un script hijo no puede verla, usas `export` para solucionarlo, extiendes el `PATH` para ejecutar tus scripts desde cualquier lugar, y finalmente guardas todo en `.zshrc` para que persista para siempre.

> Una variable de entorno es información que el sistema pasa automáticamente a cada programa que lanzas. Cuando tu terminal sabe que eres el usuario `labex`, que tu home está en `/home/labex` y que el idioma es inglés — todo eso son variables de entorno trabajando.

---

#### Variables de shell — el nivel más básico

**Sintaxis:**
```bash
NOMBRE="valor"         # definir (sin espacios alrededor del =)
echo $NOMBRE           # leer el valor
echo "${NOMBRE}"       # forma recomendada — más segura
```

**Qué hace:** Crea un nombre que almacena un valor dentro de la sesión de shell actual. La variable existe mientras esa terminal esté abierta y solo es accesible desde ese mismo proceso de shell.

**Ejemplo del lab:**
```bash
my_var="Hello, Linux"
echo $my_var
```
```
Hello, Linux
```

```bash
echo "The value of my_var is: $my_var"
```
```
The value of my_var is: Hello, Linux
```

> El signo `$` es lo que le dice al shell "no tomes esto como texto literal, busca el valor de esa variable". Sin `$`, `echo my_var` imprime literalmente `my_var`.

---

#### `env` — Ver todas las variables de entorno activas

**Sintaxis:**
```bash
env                    # lista todas las variables de entorno
env | grep PATRON      # filtrar por nombre
```

**Qué hace:** Imprime todas las variables de entorno que el shell actual tiene definidas. Son las variables que se heredan automáticamente por cualquier proceso hijo.

**Variables importantes que reveló `env` en el lab:**

| Variable | Valor del lab | Qué significa |
|----------|-------------|--------------|
| `HOME` | `/home/labex` | Directorio home del usuario |
| `USER` | `labex` | Nombre del usuario actual |
| `SHELL` | `/usr/bin/zsh` | El shell que se está usando |
| `PWD` | `/home/labex/project` | Directorio de trabajo actual |
| `PATH` | `/usr/bin:/bin:...` | Directorios donde buscar ejecutables |
| `LANG` | `en_US.UTF-8` | Idioma y codificación del sistema |
| `TERM` | `xterm-256color` | Tipo de terminal (afecta colores y atajos) |
| `JAVA_HOME` | `/usr/lib/jvm/java-11-...` | Dónde está instalado Java |
| `GOROOT` | `/usr/local/go` | Dónde está instalado Go |

> La salida de `env` en LabEx revela todo el stack tecnológico del entorno: Java, Go, Node.js, Maven, Yarn — cada uno configurado con sus propias variables de entorno.

---

#### La diferencia clave: variable de shell vs variable de entorno

El lab demostró este concepto de forma directa con un script:

```bash
# 1. Variable de shell (sin export)
my_var="Hello, Linux"

# 2. Variable de entorno (con export)
export MY_ENV_VAR="This is an environment variable"

# 3. Script que intenta acceder a ambas
cat << 'EOF' > test_vars.sh
echo "Shell variable: $my_var"
echo "Environment variable: $MY_ENV_VAR"
EOF

chmod +x test_vars.sh
./test_vars.sh
```
```
Shell variable:
Environment variable: This is an environment variable
```

**¿Qué pasó?** Al ejecutar `./test_vars.sh`, el shell lanza un **proceso hijo** (una nueva instancia de shell) para correr el script. Ese proceso hijo hereda las variables de entorno (`export`) pero no tiene acceso a las variables de shell del proceso padre.

**Los tres niveles de permanencia:**

| Tipo | Cómo se crea | Acceso proceso hijo | Persiste al cerrar |
|------|-------------|--------------------|--------------------|
| Variable de shell | `mi_var="valor"` | No | No |
| Variable de entorno | `export MI_VAR="valor"` | Sí | No |
| Variable permanente | En `~/.zshrc` o `~/.bashrc` | Sí | Sí — sobrevive al reinicio |

---

#### `export` — Convertir una variable en variable de entorno

**Sintaxis:**
```bash
export NOMBRE="valor"         # definir y exportar en un paso
export NOMBRE                 # exportar una variable ya definida
```

**Qué hace:** Marca la variable para que sea heredada por todos los procesos hijos que se lancen desde este shell. Sin `export`, la variable es privada del shell actual.

**Ejemplo del lab:**
```bash
export MY_ENV_VAR="This is an environment variable"
env | grep MY_ENV_VAR
```
```
MY_ENV_VAR=This is an environment variable
```

---

#### `echo $PATH` — Entender el PATH

`PATH` es la variable de entorno más importante del sistema. Contiene una lista de directorios separados por `:` donde el shell busca los ejecutables cuando escribes un comando.

```bash
echo $PATH
```
```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:...:/home/labex/my_scripts
```

**Cómo funciona en la práctica:**

Cuando escribes `ls`, el shell no sabe dónde está `ls`. Lo busca en cada directorio del `PATH` de izquierda a derecha hasta encontrarlo. En este caso, lo encuentra en `/usr/bin/ls`.

Si escribes un comando que no está en ningún directorio del PATH:
```
command not found: mi_script
```

La solución es agregar el directorio al PATH.

---

#### Extender el PATH con un directorio propio

**El problema que resuelve:** Tienes scripts en `~/my_scripts/` y quieres ejecutarlos desde cualquier directorio sin escribir la ruta completa.

```bash
mkdir ~/my_scripts
export PATH="$PATH:$HOME/my_scripts"
```

**Desglosado:**
- `$PATH` — el valor actual del PATH (todos los directorios existentes)
- `:` — el separador de directorios en PATH
- `$HOME/my_scripts` — agrega tu carpeta al final

**El resultado:**
```bash
cat << 'EOF' > ~/my_scripts/hello.sh
echo "Hello from my custom script!"
EOF
chmod +x ~/my_scripts/hello.sh

# Ahora funciona desde cualquier directorio:
hello.sh
```
```
Hello from my custom script!
```

```bash
cd /tmp
hello.sh
```
```
Hello from my custom script!
```

> Agregar al final del PATH (`$PATH:nuevo`) significa que tus scripts tienen menor prioridad que los del sistema. Agregar al inicio (`nuevo:$PATH`) les da mayor prioridad — pero puede causar problemas si tu script tiene el mismo nombre que un comando del sistema.

---

#### `<< 'EOF'` vs `<< EOF` — detalle importante del lab

El lab usó comillas simples alrededor de `EOF`:

```bash
cat << 'EOF' > test_vars.sh
echo "Shell variable: $my_var"
echo "Environment variable: $MY_ENV_VAR"
EOF
```

**¿Por qué las comillas simples?**

| Sintaxis | Comportamiento dentro del heredoc |
|----------|----------------------------------|
| `<< EOF` | El shell expande `$variables` antes de escribir |
| `<< 'EOF'` | El contenido se trata como texto literal — `$variables` no se expande |

```bash
# Con << EOF: $my_var se expande al escribir el archivo
cat << EOF > script.sh
echo "$my_var"        # el archivo quedaría: echo "Hello, Linux"
EOF

# Con << 'EOF': $my_var queda como texto literal
cat << 'EOF' > script.sh
echo "$my_var"        # el archivo quedaría: echo "$my_var"
EOF
```

Para crear scripts, siempre usa `<< 'EOF'` — quieres que las variables se expandan cuando el script corra, no cuando se crea el archivo.

---

#### Hacer variables permanentes con `.zshrc` / `.bashrc`

Las variables creadas con `export` desaparecen al cerrar la terminal. Para que persistan, hay que agregarlas al archivo de configuración del shell.

```bash
nano ~/.zshrc
```

Al final del archivo, agrega:
```bash
export MY_ENV_VAR="This is an environment variable"
export PATH="$PATH:$HOME/my_scripts"
```

**Aplicar los cambios sin cerrar la terminal:**
```bash
source ~/.zshrc
```

`source` ejecuta el archivo en el **contexto del shell actual** — a diferencia de `./archivo.sh` que lanza un proceso hijo, `source` aplica los cambios directamente a la sesión actual.

**¿Qué archivo usar?**

| Archivo | Shell | Cuándo se ejecuta |
|---------|-------|------------------|
| `~/.bashrc` | Bash | Al abrir una terminal interactiva |
| `~/.zshrc` | Zsh | Al abrir una terminal interactiva |
| `~/.bash_profile` | Bash | Al iniciar sesión (login shell) |
| `~/.profile` | Cualquiera | Al iniciar sesión (genérico) |

> En el lab el shell era `zsh` (el `SHELL=/usr/bin/zsh` que viste en `env`). Por eso se usó `~/.zshrc`. En Ubuntu sin personalizar, el shell por defecto es `bash` y el archivo sería `~/.bashrc`.

---

#### Variables de entorno integradas del sistema

Linux define automáticamente estas variables para todos los usuarios:

```bash
echo $HOME    # /home/labex
echo $USER    # labex
echo $SHELL   # /usr/bin/zsh
echo $PWD     # /tmp (directorio actual)
echo $TERM    # xterm-256color
```

**Variables integradas más útiles:**

| Variable | Qué contiene | Uso típico |
|----------|-------------|-----------|
| `$HOME` | Home del usuario | `cd $HOME`, rutas en scripts |
| `$USER` | Nombre del usuario | Logs, mensajes personalizados |
| `$SHELL` | Shell activo | Detectar qué shell usar en scripts |
| `$PWD` | Directorio actual | Equivalente a `$(pwd)` en scripts |
| `$PATH` | Directorios de ejecutables | Extender con nuevos directorios |
| `$TERM` | Tipo de terminal | Afecta colores y capacidades |
| `$LANG` | Idioma y codificación | Afecta ordenamiento y fechas |
| `$EDITOR` | Editor de texto preferido | Git, crontab usan este para abrir archivos |
| `$OLDPWD` | Directorio anterior | Lo que usa `cd -` internamente |

---

#### `unset` — Eliminar una variable

**Sintaxis:**
```bash
unset NOMBRE_VARIABLE
unset -v NOMBRE_VARIABLE    # explícitamente una variable (no función)
unset -f nombre_funcion      # eliminar una función
```

**Qué hace:** Elimina completamente la variable del entorno. Después de `unset`, la variable deja de existir — accederla devuelve cadena vacía.

**Ejemplo del lab:**
```bash
echo $MY_ENV_VAR
```
```
This is an environment variable
```

```bash
unset MY_ENV_VAR
echo $MY_ENV_VAR
```
```
(línea vacía — la variable ya no existe)
```

> `unset` solo afecta la sesión actual. Si la variable está definida en `~/.zshrc`, reaparecerá la próxima vez que abras una terminal. Para eliminarla permanentemente, también hay que borrarla del archivo de configuración.

---

#### Flujo completo del lab

```
1. my_var="valor"                → Variable de shell (privada, solo esta sesión)
        ↓
2. export MY_VAR="valor"         → Variable de entorno (heredada por procesos hijos)
        ↓
3. env | grep MY_VAR             → Verificar que existe en el entorno
        ↓
4. export PATH="$PATH:$HOME/dir" → Extender el PATH con tu directorio
        ↓
5. nano ~/.zshrc                 → Agregar las variables para hacerlas permanentes
        ↓
6. source ~/.zshrc               → Aplicar cambios sin reiniciar la terminal
        ↓
7. unset MY_VAR                  → Eliminar una variable de la sesión actual
```

---

#### Errores frecuentes — Lab 08

**`MI_VAR = "valor"` con espacios alrededor del `=`**

Bash interpreta `MI_VAR = "valor"` como "ejecuta el comando `MI_VAR` con el argumento `=` y el argumento `valor`" — que no existe. El `=` en la asignación de variables no puede tener espacios. Siempre: `MI_VAR="valor"`.

**`export PATH="nuevo_dir"` sin incluir `$PATH`**

Si escribes `export PATH="/mi/dir"` sin `$PATH:` al inicio, reemplazas el PATH completo por ese único directorio. Los comandos como `ls`, `grep`, `cat` dejan de funcionar porque sus directorios ya no están en el PATH. La forma correcta es siempre `export PATH="$PATH:/mi/dir"`.

**Modificar `.bashrc` cuando el shell es `zsh` (o viceversa)**

Los cambios en `~/.bashrc` no tienen efecto si el shell activo es `zsh`. Verifica primero con `echo $SHELL` para saber qué archivo editar.

**`source` vs `./archivo.sh` para aplicar configuración**

`./archivo.sh` lanza un proceso hijo — los cambios de variables ocurren en ese hijo y desaparecen cuando termina. `source archivo.sh` ejecuta el archivo en el shell actual — los cambios quedan. Para aplicar `.zshrc` o `.bashrc`, siempre usa `source`.

**`unset` sin efecto al reabrir la terminal**

`unset MY_VAR` elimina la variable de la sesión actual, pero si está en `~/.zshrc`, la próxima terminal la cargará de nuevo. Para que sea permanente, también hay que borrarla del archivo con `nano ~/.zshrc`.

---

#### Ejercicio — Lab 08

**Entorno:** KillerCoda (Ubuntu/Zsh) o cualquier Linux.

**Tareas:**

1. Crea una variable de shell `proyecto="mi_app"` y verifícala con `echo`.
2. Exporta `export VERSION="1.0.0"`.
3. Crea el script `test_scope.sh` usando here-document con `<< 'EOF'` que imprima ambas variables. Ejecuta el script y observa cuál aparece vacía.
4. Usa `env | grep VERSION` para confirmar que `VERSION` está en el entorno.
5. Crea el directorio `~/mis_scripts` y agrega un script `saludo.sh` que imprima tu nombre.
6. Extiende el PATH: `export PATH="$PATH:$HOME/mis_scripts"`.
7. Ejecuta `saludo.sh` desde `/tmp` para confirmar que el PATH funciona.
8. Agrega `export VERSION="1.0.0"` y la línea del PATH a tu `~/.bashrc` o `~/.zshrc`.
9. Aplica los cambios con `source`.
10. Usa `unset VERSION` y verifica que la variable desapareció.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
proyecto="mi_app"
echo $proyecto

# Paso 2
export VERSION="1.0.0"

# Paso 3
cat << 'EOF' > test_scope.sh
echo "Variable de shell: $proyecto"
echo "Variable de entorno: $VERSION"
EOF
chmod +x test_scope.sh
./test_scope.sh
# "proyecto" aparece vacía — no fue exportada

# Paso 4
env | grep VERSION

# Paso 5
mkdir ~/mis_scripts
cat << 'EOF' > ~/mis_scripts/saludo.sh
echo "Hola, soy Tu_Nombre!"
EOF
chmod +x ~/mis_scripts/saludo.sh

# Paso 6
export PATH="$PATH:$HOME/mis_scripts"

# Paso 7
cd /tmp
saludo.sh

# Paso 8 (editar el archivo correspondiente)
echo 'export VERSION="1.0.0"' >> ~/.bashrc
echo 'export PATH="$PATH:$HOME/mis_scripts"' >> ~/.bashrc

# Paso 9
source ~/.bashrc

# Paso 10
unset VERSION
echo $VERSION   # vacío
```

</details>

---

### Lab 09 — Desafío: Variable de Entorno Permanente

**Escenario:** Como administrador de sistemas junior, necesitas establecer un entorno de desarrollo consistente. La tarea: crear la variable `PROJECT_DIR` que apunte a `/home/labex/project`, hacerla permanente en `~/.zshrc`, y verificar que funciona correctamente en cualquier sesión.

> Este desafío parece simple pero concentra exactamente los tres pasos que más confunden al principiante: dónde escribir la variable, cómo aplicarla sin reiniciar, y cómo verificar que realmente persiste.

---

#### Por qué es un desafío real

El desafío tiene tres requisitos concretos que deben cumplirse todos juntos:

| Requisito | Comandos involucrados |
|-----------|----------------------|
| Crear la variable en la sesión actual | `export PROJECT_DIR=...` |
| Hacerla permanente en `.zshrc` | `nano ~/.zshrc` o `echo ... >> ~/.zshrc` |
| Verificar que funciona | `echo $PROJECT_DIR` después de `source` |

El error más común: hacer solo uno o dos de los tres pasos. Solo `export` no es permanente. Solo editar `.zshrc` sin `source` no la activa en la sesión actual. Solo `echo` sin haberla exportado muestra vacío.

---

#### Solución paso a paso

**Paso 1 — Ir al directorio correcto**
```bash
cd /home/labex
```

**Paso 2 — Exportar la variable en la sesión actual**
```bash
export PROJECT_DIR=/home/labex/project
```

Esto crea la variable de inmediato en la sesión actual. Si cierras la terminal ahora, desaparece. Por eso necesitas el siguiente paso.

**Paso 3 — Agregarla al archivo de configuración permanente**

Opción A — con `echo >>` (más rápido, sin abrir editor):
```bash
echo 'export PROJECT_DIR=/home/labex/project' >> ~/.zshrc
```

Opción B — con `nano` (más visual):
```bash
nano ~/.zshrc
```
Al final del archivo agrega:
```bash
export PROJECT_DIR=/home/labex/project
```
Guarda con `Ctrl+O`, confirma con `Enter`, sal con `Ctrl+X`.

**Paso 4 — Aplicar los cambios sin cerrar la terminal**
```bash
source ~/.zshrc
```

**Paso 5 — Verificar que funciona**
```bash
echo $PROJECT_DIR
```
```
/home/labex/project
```

**Verificación adicional — confirmar que está en el entorno:**
```bash
env | grep PROJECT_DIR
```
```
PROJECT_DIR=/home/labex/project
```

**Verificación de persistencia — confirmar que está en `.zshrc`:**
```bash
grep PROJECT_DIR ~/.zshrc
```
```
export PROJECT_DIR=/home/labex/project
```

---

#### Por qué falló la primera vez — análisis

Los puntos donde típicamente se traba este desafío:

**Traba 1 — Solo hacer `export` sin editar `.zshrc`**

`export PROJECT_DIR=/home/labex/project` funciona en la sesión actual, pero al cerrar la terminal y volver a abrirla, la variable ya no existe. El desafío pide que sea **permanente**.

**Traba 2 — Editar `.zshrc` pero olvidar `source`**

Editar el archivo no aplica los cambios automáticamente. El archivo `.zshrc` solo se lee cuando se abre una nueva terminal. Para aplicarlo en la sesión actual sin reiniciar: `source ~/.zshrc`.

**Traba 3 — Usar comillas dobles en el `echo >>` incorrecto**

```bash
# MAL — las variables se expanden antes de escribir
echo "export PROJECT_DIR=$HOME/project" >> ~/.zshrc
# Resultado en .zshrc: export PROJECT_DIR=/home/labex/project ← puede funcionar
# pero si $HOME no está definido en ese momento, queda vacío

# BIEN — texto literal, sin expansión
echo 'export PROJECT_DIR=/home/labex/project' >> ~/.zshrc
```

Con comillas simples el texto se escribe exactamente como está — más seguro y predecible.

**Traba 4 — El shell es Bash pero se edita `.zshrc`**

Si el shell activo es Bash (`echo $SHELL` muestra `/bin/bash`), editar `.zshrc` no tiene efecto. El archivo correcto sería `~/.bashrc`. Siempre verificar el shell antes de editar el archivo de configuración.

---

#### La solución completa en un bloque

Para un administrador que necesita hacer esto rápido y bien:

```bash
# 1. Agregar al archivo de configuración permanente
echo 'export PROJECT_DIR=/home/labex/project' >> ~/.zshrc

# 2. Aplicar en la sesión actual
source ~/.zshrc

# 3. Verificar
echo $PROJECT_DIR
env | grep PROJECT_DIR
grep PROJECT_DIR ~/.zshrc
```

Los tres comandos de verificación responden tres preguntas distintas:
- `echo $PROJECT_DIR` → ¿está activa en esta sesión?
- `env | grep PROJECT_DIR` → ¿está en el entorno del proceso actual?
- `grep PROJECT_DIR ~/.zshrc` → ¿quedó guardada para la próxima sesión?

---

#### Ejercicio — Lab 09

**Entorno:** KillerCoda (Ubuntu/Zsh) o cualquier Linux.

Replica el desafío completo con una variable diferente:

1. Crea la variable permanente `LOG_DIR=/var/log` en tu shell.
2. Agrégala a tu archivo de configuración (`~/.bashrc` o `~/.zshrc` según tu shell).
3. Aplícala con `source`.
4. Verifica con los tres comandos: `echo`, `env | grep`, `grep ~/.bashrc`.
5. Abre una nueva terminal y verifica que la variable sigue disponible.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1 y 2 — agregar al archivo y exportar en la sesión actual
echo 'export LOG_DIR=/var/log' >> ~/.bashrc
export LOG_DIR=/var/log

# Paso 3
source ~/.bashrc

# Paso 4 — verificación triple
echo $LOG_DIR
env | grep LOG_DIR
grep LOG_DIR ~/.bashrc

# Paso 5 — abrir nueva terminal y verificar
echo $LOG_DIR    # debe mostrar /var/log
```

</details>

---

### Lab 10 — Empaquetar y Comprimir Archivos

**Escenario:** Necesitas enviar un directorio completo a un servidor remoto. El directorio tiene decenas de archivos y subdirectorios. Si los copias uno a uno es lento y propenso a errores. La solución: empaquetar todo en un solo archivo y opcionalmente comprimirlo para que ocupe menos espacio.

> En Linux, **empaquetar** y **comprimir** son dos operaciones distintas que se hacen con herramientas distintas. Entender esa diferencia es la clave de este lab — y es lo que confunde a la mayoría al principio.

---

#### La distinción fundamental: empaquetar ≠ comprimir

| Operación | Qué hace | Herramienta | Resultado |
|-----------|---------|-------------|----------|
| **Empaquetar** | Une múltiples archivos en uno solo | `tar` | Un archivo más grande que los originales |
| **Comprimir** | Reduce el tamaño de un archivo | `gzip`, `bzip2`, `xz` | Un archivo más pequeño |
| **Empaquetar + comprimir** | Las dos cosas juntas | `tar + gzip` | Un archivo comprimido |

**Analogía:** Empaquetar es meter ropa en una maleta — todo junto pero sin apretar. Comprimir es usar una bolsa de vacío para reducir el volumen. Se puede hacer una sin la otra, pero juntas son más útiles.

**¿Por qué usar los dos pasos en vez de solo comprimir?**

`gzip` solo comprime **un archivo a la vez**. No puede comprimir un directorio con subdirectorios. Por eso primero usas `tar` para unir todo en un archivo, y luego `gzip` para reducir ese archivo. O directamente `tar -z` que hace los dos pasos en un solo comando.

---

#### Estructura de prueba del lab

```bash
mkdir -p test_dir/{subdir1,subdir2}
echo "This is file 1" > test_dir/file1.txt
echo "This is file 2" > test_dir/file2.txt
echo "This is in subdir1" > test_dir/subdir1/subfile1.txt
echo "This is in subdir2" > test_dir/subdir2/subfile2.txt
```

```bash
tree test_dir
```
```
test_dir
├── file1.txt
├── file2.txt
├── subdir1
│   └── subfile1.txt
└── subdir2
    └── subfile2.txt
```

---

#### `tar` — La herramienta de empaquetado de Linux

`tar` viene de *Tape Archive* — originalmente se usaba para grabar archivos en cintas magnéticas. Hoy se usa para empaquetar cualquier conjunto de archivos en uno solo, conservando toda la estructura de directorios, permisos y metadatos.

**Las flags de `tar` — la clave para no confundirse:**

| Flag | Nombre | Qué hace |
|------|--------|---------|
| `-c` | **C**reate | **Crear** un archivo nuevo |
| `-x` | e**X**tract | **Extraer** el contenido |
| `-t` | lis**T** | **Listar** el contenido sin extraer |
| `-v` | **V**erbose | Mostrar progreso (qué archivo procesa) |
| `-f` | **F**ile | El siguiente argumento es el nombre del archivo |
| `-z` | g**Z**ip | Comprimir/descomprimir con gzip |
| `-C` | **C**hange dir | Cambiar al directorio indicado antes de operar |

> El truco para memorizar: `c`rear, e`x`traer, lis`t`ar — son las tres operaciones principales. Todo lo demás son modificadores de cómo se hace.

---

#### Paso 1 — `tar -cvf`: crear archivo tar (sin compresión)

```bash
tar -cvf test_archive.tar test_dir
```

| Parte | Qué hace |
|-------|---------|
| `-c` | Crear un archivo nuevo |
| `-v` | Verbose — muestra cada archivo mientras lo agrega |
| `-f test_archive.tar` | El archivo resultante se llamará `test_archive.tar` |
| `test_dir` | El directorio que se va a empaquetar |

**Salida:**
```
test_dir/
test_dir/subdir1/
test_dir/subdir1/subfile1.txt
test_dir/subdir2/
test_dir/subdir2/subfile2.txt
test_dir/file1.txt
test_dir/file2.txt
```

Cada línea confirma que ese archivo o directorio fue incluido en el tar. Un `.tar` sin compresión es más grande que los originales porque incluye metadatos de cada archivo.

---

#### Paso 2 — `tar -tvf`: listar sin extraer

```bash
tar -tvf test_archive.tar
```
```
drwxrwxr-x labex/labex    0 2026-04-13 11:53 test_dir/
-rw-rw-r-- labex/labex   19 2026-04-13 11:54 test_dir/subdir1/subfile1.txt
-rw-rw-r-- labex/labex   15 2026-04-13 11:53 test_dir/file1.txt
...
```

`-t` (list) muestra el inventario completo con permisos, dueño, tamaño y fecha de cada entrada. Es la forma de verificar que el tar está íntegro **antes de borrar los originales**.

---

#### Paso 3 — `tar -xvf -C`: extraer en un directorio específico

```bash
mkdir extracted_tar
tar -xvf test_archive.tar -C extracted_tar
```

| Parte | Qué hace |
|-------|---------|
| `-x` | Extraer el contenido |
| `-v` | Mostrar cada archivo al extraerlo |
| `-f test_archive.tar` | El archivo a extraer |
| `-C extracted_tar` | Extraer dentro del directorio `extracted_tar` |

> Sin `-C`, el tar se extrae en el directorio actual — puede sobreescribir archivos existentes. Siempre usa `-C directorio/` para controlar dónde van los archivos.

---

#### Paso 4 — `gzip`: comprimir por separado

```bash
gzip test_archive.tar
```

`gzip` toma el archivo, lo comprime y **reemplaza el original** por la versión comprimida con extensión `.gz`. No pide confirmación — el archivo `.tar` desaparece y aparece `.tar.gz`.

```bash
ls -lh test_archive.tar.gz
```
```
-rw-rw-r-- 1 labex labex 301 Apr 13 11:57 test_archive.tar.gz
```

---

#### La comparación de tamaños del lab

El lab midió los tamaños para entender qué pasa con cada operación:

```bash
# Contenido real de los archivos
find test_dir -type f -exec ls -l {} \; | awk '{total += $5} END {print total " bytes"}'
```
```
68 bytes      ← el contenido de texto puro
```

```bash
# El tar sin comprimir
ls -lh test_archive_compare.tar
```
```
10K           ← ¡más grande que los originales!
```

```bash
# El tar comprimido con gzip
ls -lh test_archive.tar.gz
```
```
301 bytes     ← mucho más pequeño
```

```bash
# Espacio en disco del directorio
du -sh test_dir
```
```
16K           ← espacio que ocupa en disco (incluye bloques del filesystem)
```

**Por qué el tar sin comprimir ocupa 10K si el contenido son 68 bytes:**

Los sistemas de archivos trabajan con **bloques de disco** — la unidad mínima de almacenamiento. En Linux el bloque típico es de 4KB. Un archivo de 15 bytes ocupa 4KB completos en disco. Además, `tar` añade cabeceras de 512 bytes por cada archivo para guardar metadatos (permisos, fechas, dueño). Con archivos pequeños, los metadatos pueden pesar más que el contenido.

| Archivo | Tamaño |
|---------|--------|
| Contenido real | 68 bytes |
| Directorio en disco | 16 KB (bloques del filesystem) |
| `.tar` (empaquetado) | 10 KB (cabeceras + contenido) |
| `.tar.gz` (comprimido) | 301 bytes |

> La compresión es más efectiva cuanto más grande y más repetitivo es el contenido. En archivos de texto pequeños como estos, el ratio es impresionante. En archivos de video o imágenes ya comprimidos, `gzip` apenas reduce el tamaño.

---

#### Paso 5 — `tar -czvf`: empaquetar y comprimir en un solo paso

En la práctica, casi nunca se hace `tar` y `gzip` por separado. `tar` tiene la flag `-z` que llama a `gzip` automáticamente:

```bash
tar -czvf test_combined.tar.gz test_dir
```

| Flag combinada | Qué hace |
|---------------|---------|
| `-c` | Crear |
| `-z` | Comprimir con gzip mientras empaqueta |
| `-v` | Verbose |
| `-f test_combined.tar.gz` | Nombre del archivo resultante |
| `test_dir` | Lo que se empaqueta |

**Listar el contenido del `.tar.gz`:**
```bash
tar -tzvf test_combined.tar.gz
```
`-t` + `-z` para listar un archivo comprimido con gzip.

**Extraer el `.tar.gz`:**
```bash
mkdir extracted
tar -xzvf test_combined.tar.gz -C extracted
```

---

#### Paso 6 — `zip` y `unzip`: formato multiplataforma

`zip` es un formato de compresión y empaquetado en un solo paso, con mejor compatibilidad multiplataforma — especialmente para compartir archivos con usuarios de Windows y macOS.

**Crear un zip:**
```bash
zip -r test_archive.zip test_dir
```

| Parte | Qué hace |
|-------|---------|
| `-r` | **R**ecursivo — incluye subdirectorios |
| `test_archive.zip` | Nombre del archivo resultante |
| `test_dir` | Directorio a comprimir |

**Salida:**
```
adding: test_dir/ (stored 0%)
adding: test_dir/subdir1/subfile1.txt (deflated 5%)
adding: test_dir/file1.txt (stored 0%)
```

`stored 0%` significa que ese archivo es tan pequeño que la compresión no ayuda — se guarda sin comprimir. `deflated 5%` significa que se comprimió un 5%.

**Extraer un zip:**
```bash
unzip -d unzipped_files test_archive.zip
```

| Parte | Qué hace |
|-------|---------|
| `-d unzipped_files` | Extraer en el directorio `unzipped_files` |
| `test_archive.zip` | El archivo a extraer |

---

#### Cuándo usar cada formato

| Formato | Comando | Cuándo usarlo |
|---------|---------|--------------|
| `.tar` | `tar -cvf` | Agrupar sin comprimir — para transferencias rápidas donde el tamaño no importa |
| `.tar.gz` | `tar -czvf` | El estándar de Linux — compresión buena, velocidad razonable |
| `.tar.bz2` | `tar -cjvf` | Mejor compresión que gzip, más lento — para archivos muy grandes |
| `.tar.xz` | `tar -cJvf` | La mejor compresión, el más lento — distribuciones de software |
| `.zip` | `zip -r` | Compartir con Windows/macOS — máxima compatibilidad |

> En Linux se usa casi siempre `.tar.gz`. En entornos donde el destino puede ser Windows, `.zip`. Para distribuciones de software muy grandes, `.tar.xz`.

---

#### Mapa mental de flags de `tar`

Para no perderse con las flags, este mapa ayuda a visualizarlas:

```
tar  [acción]  [modificadores]  [archivo_resultado]  [fuente]
      -c          -v                -f archivo.tar      directorio/
      -x          -z (gzip)
      -t          -j (bzip2)
                  -J (xz)
                  -C destino/
```

**Receta para las 6 operaciones más comunes:**

```bash
# 1. Empaquetar (sin comprimir)
tar -cvf archivo.tar directorio/

# 2. Empaquetar y comprimir (gzip)
tar -czvf archivo.tar.gz directorio/

# 3. Ver contenido de un tar
tar -tvf archivo.tar

# 4. Ver contenido de un tar.gz
tar -tzvf archivo.tar.gz

# 5. Extraer un tar
tar -xvf archivo.tar -C destino/

# 6. Extraer un tar.gz
tar -xzvf archivo.tar.gz -C destino/
```

---

#### `du -sh` — Medir el espacio en disco

```bash
du -sh test_dir
```
```
16K   test_dir
```

| Flag | Qué hace |
|------|---------|
| `-s` | Summary — muestra el total del directorio, no archivo por archivo |
| `-h` | Human-readable — muestra KB, MB, GB en vez de bloques |

> `du` (disk usage) mide el espacio **real en disco** — que puede ser muy distinto del tamaño del contenido. Un archivo de 1 byte ocupa 4KB en disco si el bloque es de 4KB.

---

#### Errores frecuentes — Lab 10

**`gzip directorio/` en vez de comprimirlo con tar primero**

`gzip` solo opera sobre archivos individuales — no puede comprimir directorios directamente. El error: `gzip: directorio/: Is a directory`. Solución: primero `tar -cvf archivo.tar directorio/` y luego `gzip archivo.tar`, o directamente `tar -czvf archivo.tar.gz directorio/`.

**`tar -xvf archivo.tar` sin `-C` — extrae en el directorio actual**

Si el tar contiene una carpeta `project/` y lo extraes sin `-C`, aparece una carpeta `project/` en tu directorio actual que puede sobreescribir trabajo existente. Siempre especifica el destino con `-C directorio/`.

**`zip archivo.zip directorio/` sin `-r`**

Sin `-r`, `zip` solo agrega el directorio vacío — no su contenido. Siempre `zip -r` para incluir subdirectorios y archivos.

**`tar -xzvf` en un `.tar` sin comprimir**

Si el archivo no está comprimido con gzip, usar `-z` da error o extrae incorrectamente. Para un `.tar` normal, omite la `z`: `tar -xvf archivo.tar`. Para un `.tar.gz`, sí usa `z`: `tar -xzvf archivo.tar.gz`.

**Borrar los originales antes de verificar el tar**

El flujo correcto es: crear tar → verificar con `-t` → borrar originales. Si borras antes de verificar y el tar estaba incompleto o corrupto, los datos se pierden.

---

#### Ejercicio — Lab 10

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Preparación:**
```bash
mkdir -p ~/practica-compress/{documentos,imagenes,scripts}
echo "Reporte Q1" > ~/practica-compress/documentos/q1.txt
echo "Reporte Q2" > ~/practica-compress/documentos/q2.txt
echo "#!/bin/bash" > ~/practica-compress/scripts/deploy.sh
touch ~/practica-compress/imagenes/logo.png
```

**Tareas:**

1. Empaqueta `practica-compress/` en `backup.tar` sin comprimir.
2. Lista el contenido del tar con `-t` para verificar que todos los archivos están.
3. Comprime `backup.tar` con `gzip` y observa el cambio de nombre.
4. Crea desde cero un `backup_v2.tar.gz` usando el flag `-z` en un solo comando.
5. Extrae `backup_v2.tar.gz` en un directorio llamado `restaurado/`.
6. Crea un `backup.zip` del mismo directorio con `zip -r`.
7. Extrae el zip en `desde_zip/` con `unzip -d`.
8. Usa `du -sh` para comparar el tamaño de `practica-compress/` con los archivos generados.

<details>
<summary>Ver solución</summary>

```bash
cd ~

# Paso 1
tar -cvf backup.tar practica-compress/

# Paso 2
tar -tvf backup.tar

# Paso 3
gzip backup.tar
ls -lh backup.tar.gz

# Paso 4
tar -czvf backup_v2.tar.gz practica-compress/

# Paso 5
mkdir restaurado
tar -xzvf backup_v2.tar.gz -C restaurado/

# Paso 6
zip -r backup.zip practica-compress/

# Paso 7
unzip -d desde_zip backup.zip

# Paso 8
du -sh practica-compress/
du -sh backup.tar.gz backup_v2.tar.gz backup.zip
```

</details>

---

### Lab 11 — Desafío: Respaldo de Logs del Sistema

**Escenario:** TechCorp necesita respaldos diarios de los logs del servidor para cumplimiento normativo. Cada respaldo debe tener en el nombre la fecha en que fue creado para poder identificarlo sin abrirlo. El reto es hacer todo en un solo comando.

> Este desafío conecta tres habilidades de labs anteriores en un comando de producción real: `tar` (Lab 10), `date` con formato (Lab 01/08), y sustitución de comandos con `$()` (Lab 08). Cuando estas tres piezas se combinan, el resultado es una línea que pueden usar administradores reales todos los días.

---

#### El concepto clave: sustitución de comandos `$()`

Antes de ver el comando completo, hay que entender `$()`:

```bash
$(comando)
```

**Qué hace:** Ejecuta el comando que está dentro de los paréntesis y reemplaza `$()` con su resultado — en el mismo momento en que se construye el comando exterior.

**Ejemplos sencillos:**
```bash
echo "Hoy es $(date)"
# Resultado: Hoy es Mon Apr 14 12:00:00 CST 2026

echo "El usuario es $(whoami)"
# Resultado: El usuario es labex

mkdir backup_$(date +%Y-%m-%d)
# Crea el directorio: backup_2026-04-14
```

> `$()` es la forma moderna de lo que antes se hacía con backticks `` `comando` ``. Son equivalentes, pero `$()` es más legible y permite anidamiento.

---

#### El comando completo del lab — desglosado

```bash
sudo tar -czvf /home/labex/project/$(date +%Y-%m-%d).tar.gz /var/log
```

Desglosado pieza por pieza:

| Parte | Qué hace |
|-------|---------|
| `sudo` | Se necesita para leer archivos de `/var/log` que pertenecen a root |
| `tar` | La herramienta de empaquetado |
| `-c` | Crear un archivo nuevo |
| `-z` | Comprimir con gzip |
| `-v` | Verbose — muestra cada archivo que agrega |
| `-f` | El siguiente argumento es el nombre del archivo de salida |
| `/home/labex/project/` | El directorio donde se guardará el respaldo |
| `$(date +%Y-%m-%d)` | Se evalúa como la fecha actual: `2026-04-14` |
| `.tar.gz` | Extensión del archivo resultante |
| `/var/log` | El directorio de logs del sistema que se respalda |

**El nombre del archivo resultante:**
```
/home/labex/project/2026-04-14.tar.gz
```

Cada día que ejecutes el comando, `$(date +%Y-%m-%d)` genera una fecha diferente — nunca sobreescribirás el respaldo anterior.

---

#### El mensaje "Removing leading `/` from member names"

```
tar: Removing leading `/' from member names
```

Este mensaje aparece siempre que pasas una **ruta absoluta** a `tar`. Es una advertencia informativa, no un error — el respaldo se crea correctamente.

**Por qué existe esta advertencia:**

Cuando `tar` guarda `/var/log/nginx/access.log` con la barra inicial, al extraerlo intentaría colocarlo exactamente en `/var/log/nginx/access.log` — sobreescribiendo el archivo del sistema. Para protegerte, `tar` elimina el `/` inicial y guarda la ruta como `var/log/nginx/access.log`. Al extraer, el archivo queda relativo al directorio actual.

```bash
# Lo que guarda tar internamente (sin la / inicial):
var/log/alternatives.log
var/log/apt/history.log
var/log/nginx/access.log
```

**Si quisieras suprimir el mensaje** (en scripts automáticos donde no quieres ruido):
```bash
sudo tar -czvf /home/labex/project/$(date +%Y-%m-%d).tar.gz /var/log 2>/dev/null
```

---

#### Lo que contiene `/var/log`

La salida del lab reveló qué hay en el directorio de logs:

| Log | Qué registra |
|-----|-------------|
| `/var/log/apt/history.log` | Instalaciones y actualizaciones de paquetes |
| `/var/log/dpkg.log` | Operaciones de dpkg (instalador de .deb) |
| `/var/log/bootstrap.log` | Log del proceso de arranque del sistema |
| `/var/log/btmp` | Intentos fallidos de inicio de sesión |
| `/var/log/wtmp` | Historial de inicios y cierres de sesión |
| `/var/log/faillog` | Fallos de autenticación por usuario |
| `/var/log/nginx/access.log` | Peticiones HTTP recibidas por Nginx |
| `/var/log/nginx/error.log` | Errores del servidor web Nginx |
| `/var/log/apache2/` | Logs del servidor web Apache |
| `/var/log/supervisor/` | Logs del gestor de procesos supervisor |

> Guardar los logs con fecha permite reconstruir qué ocurrió en el sistema en una fecha específica. Si el martes ocurre un incidente de seguridad, abres el respaldo del lunes para ver el estado previo.

---

#### Verificar el respaldo

```bash
ls /home/labex/project/
```
```
2026-04-14.tar.gz
```

**Verificaciones adicionales recomendadas:**

```bash
# Ver que el archivo existe y su tamaño
ls -lh /home/labex/project/2026-04-14.tar.gz

# Listar el contenido sin extraer (primeras 20 líneas)
tar -tzvf /home/labex/project/2026-04-14.tar.gz | head -20

# Contar cuántos archivos tiene el respaldo
tar -tzvf /home/labex/project/2026-04-14.tar.gz | wc -l
```

---

#### Convertirlo en tarea automática diaria

El siguiente paso natural es automatizarlo con cron (visto en el Lab 09 del manual de Administración de Sistemas):

```bash
crontab -e
```

Agregar esta línea para ejecutarlo todos los días a las 2 AM:
```
0 2 * * * sudo tar -czvf /home/labex/project/$(date +\%Y-\%m-\%d).tar.gz /var/log 2>/dev/null
```

> Recuerda que dentro de `crontab`, los `%` deben escaparse como `\%` — de lo contrario cron los interpreta como separadores de línea.

---

#### Errores frecuentes — Lab 11

**`tar: /var/log: Cannot open: Permission denied`**

`/var/log` pertenece a root — sin `sudo`, `tar` no puede leer muchos de sus archivos. Siempre usa `sudo` cuando respaldes directorios del sistema.

**El archivo de respaldo queda dentro del directorio que se está respaldando**

Si guardas el respaldo dentro de `/var/log/`:
```bash
sudo tar -czvf /var/log/$(date +%Y-%m-%d).tar.gz /var/log
```
El tar intentará incluirse a sí mismo mientras se está creando. `tar` lo detecta e imprime un warning, pero el resultado puede ser inconsistente. Siempre guarda el respaldo **fuera** del directorio que estás respaldando.

**`$(date +%Y-%m-%d)` no expande la fecha en el nombre del archivo**

Si usaste comillas simples: `'$(date +%Y-%m-%d).tar.gz'`, la sustitución no ocurre. Las comillas simples bloquean toda expansión. Usa comillas dobles o sin comillas cuando quieras que `$()` se evalúe.

---

#### Ejercicio — Lab 11

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux con sudo.

**Tareas:**

1. Crea el directorio `~/respaldos/` donde se guardarán los respaldos.
2. Usa un solo comando para crear un respaldo comprimido de `/etc/` con el nombre `etc_YYYY-MM-DD.tar.gz` dentro de `~/respaldos/`.
3. Verifica con `ls -lh ~/respaldos/` que el archivo fue creado.
4. Lista las primeras 10 entradas del respaldo con `tar -tzvf ... | head -10`.
5. Usa `tar -tzvf ... | wc -l` para saber cuántos archivos tiene el respaldo.
6. (Opcional) Agrega este comando a tu crontab para que se ejecute todos los días a las 3 AM.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
mkdir -p ~/respaldos

# Paso 2
sudo tar -czvf ~/respaldos/etc_$(date +%Y-%m-%d).tar.gz /etc 2>/dev/null

# Paso 3
ls -lh ~/respaldos/

# Paso 4
tar -tzvf ~/respaldos/etc_$(date +%Y-%m-%d).tar.gz | head -10

# Paso 5
tar -tzvf ~/respaldos/etc_$(date +%Y-%m-%d).tar.gz | wc -l

# Paso 6 — crontab
# crontab -e
# Agregar:
# 0 3 * * * sudo tar -czvf ~/respaldos/etc_$(date +\%Y-\%m-\%d).tar.gz /etc 2>/dev/null
```

</details>

---

### Lab 12 — Discos, Particiones y Sistemas de Archivos

**Escenario:** El servidor de producción tiene un disco casi lleno. El equipo necesita saber qué directorio está consumiendo más espacio, agregar un disco nuevo, formatearlo con el sistema de archivos correcto y montarlo para poder usarlo. Este es el flujo completo que se repite en cualquier empresa que administra servidores Linux.

> Este lab toca una de las habilidades más críticas de la administración de sistemas: entender dónde está el espacio en disco, cómo están organizados los discos, y cómo preparar almacenamiento nuevo para usarlo. Sin esto, no puedes resolver "el servidor no arranca", "el directorio /var está lleno" o "necesitamos más espacio para los logs".

---

#### Los tres conceptos que hay que entender antes de empezar

Antes de ver los comandos, hay que construir el modelo mental correcto. La confusión con discos en Linux viene casi siempre de no tener claro estos tres conceptos.

---

**Concepto 1 — Sistema de archivos (Filesystem)**

Un disco recién sacado de la caja es como una hoja en blanco: no tiene estructura, no tiene carpetas, no sabe nada de archivos. Antes de poder guardar información en él, hay que **formatearlo** con un sistema de archivos.

El sistema de archivos es el lenguaje que usa el disco para organizar información. Define:
- Cómo se dividen los bloques en el disco
- Dónde se guarda el nombre de cada archivo
- Quién es el dueño
- Cuándo fue modificado
- A qué bloque físico del disco pertenece cada pedazo del archivo

Piénsalo como el índice de un libro: sin el índice, las páginas existen pero no sabes dónde está nada.

**La evolución: ext2 → ext3 → ext4**

En Linux, la familia de sistemas de archivos más usada históricamente es la familia `ext`. Entender su evolución explica por qué hoy se usa `ext4` y no los anteriores.

| Sistema | Año | Novedad principal | Problema que resuelve | Limitación que dejó |
|---------|-----|------------------|-----------------------|---------------------|
| **ext2** | 1993 | Sistema de archivos moderno para Linux | El primero estable para Linux | Sin journaling — si el sistema se apaga de golpe, los datos pueden corromperse |
| **ext3** | 2001 | **Journaling** | Un corte de luz ya no corrompe el sistema — el disco sabe volver a un estado consistente | Archivos máximo 2 TB, más lento que ext2 en algunas operaciones |
| **ext4** | 2008 | **Extents** + escalabilidad | Archivos hasta 16 TB, filesystem hasta 1 Exabyte, mucho más rápido que ext3 | Es el estándar actual — sin limitaciones relevantes para uso normal |

**¿Qué es el journaling y por qué fue tan importante?**

Imagina que estás escribiendo un archivo de 50 MB. A mitad de escritura, se va la luz. Sin journaling (ext2): el archivo queda a medias, el sistema de archivos no sabe si los bloques fueron asignados o no, y al arrancar necesitas ejecutar `fsck` (file system check) — que puede tardar minutos o horas en discos grandes, y a veces no puede recuperar nada.

Con journaling (ext3 en adelante): antes de escribir cualquier cambio real, el sistema escribe en una pequeña área especial llamada **journal** (bitácora) exactamente qué va a hacer. Si se va la luz, al reiniciar, el sistema lee el journal y dice: "ah, estaba en medio de esta operación, la deshago o la completo". El disco vuelve a un estado consistente en segundos, sin perder datos de otros archivos.

**¿Qué son los extents en ext4?**

En ext3, un archivo se describía bloque a bloque: "el archivo está en el bloque 100, 101, 102, 103...". Para un archivo de 1 GB eso significa miles de entradas en la tabla. Con los **extents** de ext4, en cambio, se puede decir: "el archivo está en los bloques del 100 al 350.000, contiguos" — una sola entrada. Esto hace que la lectura y escritura de archivos grandes sea dramáticamente más rápida.

**¿Por qué ext4 en campo laboral y no XFS o btrfs?**

| Sistema | Cuándo se usa en campo real |
|---------|---------------------------|
| **ext4** | El estándar para servidores Ubuntu/Debian — amplio soporte de herramientas, maduro, predecible |
| **XFS** | Estándar en Red Hat Enterprise Linux (RHEL) y CentOS — excelente para archivos muy grandes y alta concurrencia |
| **btrfs** | Sistemas modernos (openSUSE, Fedora) — tiene snapshots integrados, pero más complejo de administrar |
| **NTFS** | Windows — Linux puede leerlo pero no está optimizado para él |
| **FAT32/exFAT** | Memorias USB y tarjetas SD — máxima compatibilidad entre sistemas operativos |

En la práctica: si eres sysadmin en un entorno Ubuntu/Debian, usarás ext4 para casi todo. En Red Hat/CentOS, usarás XFS. Para discos externos, exFAT.

---

**Concepto 2 — Montaje (Mounting)**

En Windows, cada disco aparece automáticamente como una letra: `C:`, `D:`, `E:`. En Linux no existe eso. En Linux, **todo es parte de un único árbol de directorios** que empieza en `/`. Para que el contenido de un disco sea accesible, hay que decirle al sistema: "el contenido de este disco aparece aquí, en este directorio".

Ese directorio donde "aterriza" el disco se llama **punto de montaje**. El proceso de conectar el disco a ese directorio se llama **montar**.

```
Sin montar:           Después de montar /dev/sdb1 en /mnt/datos:
/                     /
├── home/             ├── home/
├── etc/              ├── etc/
└── mnt/              └── mnt/
    └── datos/  ←—        └── datos/     ← aquí aparece el contenido del disco
                               ├── proyecto/
                               └── backups/
```

En el campo real, los puntos de montaje más comunes son:
- `/mnt/` — montajes temporales (un disco que conectas para copiar algo)
- `/media/` — discos externos (USB, DVD) — algunos sistemas los montan aquí automáticamente
- `/data/` o `/opt/` — en servidores, particiones dedicadas para datos o software
- `/var/` — a veces en su propia partición para que si los logs llenan el disco, no afecten el sistema

---

**Concepto 3 — Particiones**

Un disco físico se puede dividir en secciones independientes llamadas **particiones**. Cada partición se comporta como si fuera un disco separado: tiene su propio sistema de archivos, su propio espacio, y se monta en un punto diferente.

Razones para particionar un disco en campo real:
- **Separar `/` de `/home`**: si `/home` se llena de archivos de usuario, el sistema sigue funcionando porque `/` tiene su propio espacio
- **Separar `/var/log`**: los logs nunca pueden llenar el disco del sistema operativo
- **Sistemas de archivos diferentes**: la partición del SO en ext4, una partición de datos en XFS
- **Swap**: partición especial sin sistema de archivos, usada como memoria virtual cuando la RAM se llena
- **Recuperación**: si el SO falla, los datos en otras particiones siguen intactos

En el lab, el comando `fdisk -l` muestra la tabla de particiones del sistema:

```
/dev/nvme0n1p1 *     2048 83886046 83883999  40G 83 Linux
```

Esto significa: disco `/dev/nvme0n1`, partición número 1, marcada como booteable (`*`), 40 GB, tipo Linux. El `p1` al final del nombre es la convención para discos NVMe — en discos SATA tradicionales sería `/dev/sda1`.

---

#### `df` — Ver el uso del disco por sistema de archivos

**Sintaxis:**
```bash
df               # muestra todos los filesystems montados en bloques de 1K
df -h            # human-readable — muestra GB, MB en vez de bloques
df -h /ruta      # solo el filesystem donde vive esa ruta
df -T            # también muestra el tipo de sistema de archivos (ext4, tmpfs, etc.)
```

**Qué hace:** Muestra cuánto espacio tiene cada filesystem montado, cuánto está usado, cuánto libre y en qué porcentaje. `df` responde la pregunta "¿cuánto espacio libre hay?".

**Ejemplo del lab:**
```bash
df -h
```
```
Filesystem      Size  Used Avail Use% Mounted on
overlay          20G  126M   20G   1% /
tmpfs            64M     0   64M   0% /dev
tmpfs           7.7G     0  7.7G   0% /sys/fs/cgroup
shm              64M     0   64M   0% /dev/shm
/dev/nvme1n1    100G   19G   82G  19% /etc/hosts
```

**Qué significa cada columna:**

| Columna | Qué muestra |
|---------|------------|
| `Filesystem` | El dispositivo o tipo de sistema de archivos |
| `Size` | El tamaño total del filesystem |
| `Used` | Espacio ocupado |
| `Avail` | Espacio disponible para uso |
| `Use%` | Porcentaje de uso — la columna que más miras como sysadmin |
| `Mounted on` | El directorio donde está montado |

**Tipos de filesystem que aparecen en el lab y qué son:**

| Filesystem | Tipo | Para qué existe |
|-----------|------|----------------|
| `overlay` | Overlay FS | Lo que usa Docker/contenedores — capas de filesystem apiladas |
| `tmpfs` | RAM filesystem | Vive en memoria RAM — `/dev/shm` es memoria compartida, muy rápido pero volátil |
| `/sys/fs/cgroup` | cgroup FS | Control de grupos de procesos (límites de CPU/RAM para contenedores) |
| `/dev/nvme1n1` | Disco real NVMe | El disco físico de la máquina — el que tiene los datos reales |

> `overlay` aparece porque el lab de LabEx corre en un contenedor Docker. En un servidor real verías directamente `/dev/sda1` o `/dev/nvme0n1p1` montado en `/`.

**En campo real, los umbrales que importan:**

Un sysadmin configura alertas en estos niveles:
- **70%** — empezar a monitorear
- **80%** — planificar limpieza o ampliación
- **90%** — acción inmediata requerida
- **95%+** — el sistema puede comenzar a fallar: logs no se escriben, aplicaciones no guardan datos, bases de datos pueden corromperse

**Diferencia entre `df` sin flags (bloques de 1K) y `df -h`:**

El `df` sin flags devuelve los valores en bloques de 1024 bytes. Para humanos es prácticamente ilegible:
```
/dev/nvme1n1   104806400 18921756  85884644  19%  /etc/hosts
```
Con `-h` se convierte en:
```
/dev/nvme1n1    100G   19G   82G  19%  /etc/hosts
```
Siempre usa `-h` cuando estás inspeccionando manualmente. Solo usa sin `-h` cuando el resultado se procesa con otro comando (porque los números exactos son más fáciles de comparar programáticamente).

---

#### `du` — Medir cuánto espacio ocupa un directorio

**Sintaxis:**
```bash
du -sh directorio/          # tamaño total del directorio (resumen)
du -h --max-depth=1 ~       # tamaños de primer nivel, sin entrar recursivamente
du -sh ~/*                  # tamaño de cada cosa dentro del home
du -h ~ | sort -rh | head   # los 10 más grandes en el home
```

**Qué hace:** Mide el espacio real en disco que ocupa cada directorio y sus subdirectorios. `du` responde la pregunta "¿qué directorio está comiendo el espacio?". `df` te dice que el disco está lleno; `du` te dice quién es el culpable.

**Ejemplo del lab — investigación completa:**

```bash
# Paso 1: ¿Cuánto pesa el home entero?
du -sh ~
```
```
2.1G    /home/labex
```

```bash
# Paso 2: ¿Qué hay en el primer nivel?
du -h --max-depth=1 ~
```
```
32K     /home/labex/.codeblocks
148K    /home/labex/.config
9.3M    /home/labex/.oh-my-zsh
844M    /home/labex/.cache
900M    /home/labex/.local
18M     /home/labex/.npm
333M    /home/labex/golang
2.1G    /home/labex
```

```bash
# Paso 3: ¿Quiénes son los 10 más grandes?
du -h ~ | sort -rh | head -n 10
```
```
2.1G    /home/labex
900M    /home/labex/.local
844M    /home/labex/.cache
763M    /home/labex/.cache/puppeteer/chrome/linux-113.0.5672.63/chrome-linux64
763M    /home/labex/.cache/puppeteer/chrome/linux-113.0.5672.63
763M    /home/labex/.cache/puppeteer/chrome
763M    /home/labex/.cache/puppeteer
601M    /home/labex/.local/share
579M    /home/labex/.local/share/code-server/extensions
579M    /home/labex/.local/share/code-server
```

**Cómo leer esta investigación:**

El home pesa 2.1G. `.local` tiene 900M y `.cache` tiene 844M — juntos son prácticamente todo el espacio. Dentro de `.cache`, hay una copia de Chrome (763M) guardada por Puppeteer (herramienta de automatización de navegadores). En `.local` hay extensiones de code-server (579M). Esto es exactamente lo que harías en producción cuando un servidor tiene el disco lleno: desciender nivel por nivel hasta encontrar el directorio culpable.

**Análisis del pipeline `du -h ~ | sort -rh | head -n 10`:**

```
du -h ~          → genera una línea por cada directorio con su tamaño
     |
sort -rh         → -r: orden inverso (mayor primero), -h: entiende K/M/G como humano
     |
head -n 10       → toma solo las primeras 10 líneas
```

> `sort -h` es el detalle crítico aquí. Sin `-h`, `sort` ordena alfabéticamente y `9M` quedaría después de `844M` porque `9` > `8` en orden de texto. Con `-h`, entiende que `844M` es mayor que `9M`.

**`du -sh ~/*` vs `du -h --max-depth=1 ~`:**

```bash
du -sh ~/*          # solo archivos/dirs visibles (no empieza con .)
du -h --max-depth=1 ~   # incluye archivos ocultos (los que empiezan con .)
```

En el lab, `du -sh ~/*` mostró solo 3 entradas (Code, Desktop, golang) porque los archivos que más pesan (`~/.cache`, `~/.local`) son ocultos. Con `--max-depth=1` sí aparecen. En un servidor real, siempre usa `--max-depth=1` para no perderte nada.

---

#### `dd` — Crear un disco virtual

**Sintaxis:**
```bash
dd if=FUENTE of=DESTINO bs=TAMAÑO count=NUMERO
```

**Qué hace:** `dd` (disk dump / data duplicator) copia datos bloque a bloque entre dispositivos o archivos. En este lab se usa para crear un archivo que simula un disco físico.

**El comando del lab:**
```bash
dd if=/dev/zero of=virtual.img bs=1M count=256
```

| Parte | Qué hace |
|-------|---------|
| `if=/dev/zero` | Input file: `/dev/zero` es un dispositivo especial que produce ceros infinitamente |
| `of=virtual.img` | Output file: el archivo donde se guardan esos ceros — el "disco virtual" |
| `bs=1M` | Block size: escribe bloques de 1 megabyte a la vez |
| `count=256` | Cuántos bloques escribir: 256 × 1M = 256 MB en total |

**Qué es `/dev/zero`:** Es un dispositivo especial de Linux que, cuando lo lees, produce ceros indefinidamente. Junto con `/dev/null` (descarta todo) y `/dev/random` (genera datos aleatorios), son los tres "dispositivos vacíos" más usados. Escribir ceros es la forma de crear un archivo con un tamaño definido y contenido conocido.

**Resultado:**
```
256+0 records in
256+0 records out
268435456 bytes (268 MB) copied
```
```bash
ls -lh virtual.img
```
```
-rw-rw-r-- 1 labex labex 256M Apr 14 11:03 virtual.img
```

Se creó un archivo de 256 MB. Ese archivo es la representación de un disco — no tiene sistema de archivos todavía, es solo espacio vacío.

**Usos reales de `dd` en campo laboral:**
- Crear imágenes de respaldo de discos completos: `dd if=/dev/sda of=backup.img`
- Crear tarjetas USB arrancables: `dd if=ubuntu.iso of=/dev/sdb bs=4M`
- Crear archivos de swap: `dd if=/dev/zero of=/swapfile bs=1G count=2`
- Probar velocidad de escritura de disco: `dd if=/dev/zero of=test bs=1M count=1000`

> **Advertencia:** `dd` opera a nivel de bloques crudos, sin protecciones. `dd if=/dev/zero of=/dev/sda` borra completamente el disco `/dev/sda` sin preguntar nada. Es una de las pocas herramientas de Linux que puede destruir datos de forma irreversible con un solo comando mal escrito.

---

#### `mkfs.ext4` — Formatear el disco virtual

**Sintaxis:**
```bash
sudo mkfs.ext4 archivo_o_dispositivo
sudo mkfs.ext4 /dev/sdb1            # formatear una partición real
sudo mkfs.ext4 virtual.img          # formatear un archivo como si fuera un disco
sudo mkfs -t ext4 /dev/sdb1         # variante equivalente
```

**Qué hace:** Crea un sistema de archivos ext4 en el dispositivo o archivo indicado. Después de este comando, el "disco" ya tiene estructura: sabe dónde guardar archivos, tiene un directorio raíz, tiene espacio para metadatos.

**Ejemplo del lab:**
```bash
sudo mkfs.ext4 virtual.img
```
```
mke2fs 1.46.5 (30-Dec-2021)
Discarding device blocks: done
Creating filesystem with 65536 4k blocks and 65536 inodes
Filesystem UUID: 74e7ebed-ee16-49ba-8901-cd702012329d
Superblock backups stored on blocks:
    32768

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
```

**Qué significa esta salida — línea por línea:**

| Línea | Significado |
|-------|------------|
| `Creating filesystem with 65536 4k blocks and 65536 inodes` | 65536 bloques de 4KB = 256MB. El número de inodes determina cuántos archivos puede contener (uno por archivo) |
| `Filesystem UUID: 74e7ebed-...` | Identificador único universal del filesystem — se usa para montaje confiable en lugar de nombres de dispositivo |
| `Superblock backups stored on blocks: 32768` | El superbloque contiene la info crítica del filesystem. Se hace copia de seguridad en otros bloques por si el primero se corrompe |
| `Writing inode tables: done` | Crea la tabla de inodes — la estructura que guarda los metadatos de cada archivo |
| `Creating journal (4096 blocks): done` | Crea el journal de ext4 — la bitácora que garantiza consistencia ante cortes de luz |
| `Writing superblocks and filesystem accounting information: done` | Guarda la info del filesystem (tamaño, inodes libres, bloques libres) |

**¿Qué es un inode?**

Un inode es la ficha técnica de un archivo. Cada archivo tiene exactamente un inode que contiene:
- El dueño (UID, GID)
- Los permisos
- Fechas (creación, modificación, acceso)
- El tamaño
- Los bloques del disco donde está el contenido

Lo que el inode **no** guarda es el nombre del archivo — el nombre vive en el directorio. Por eso en Linux puedes tener dos nombres para el mismo archivo (hard links): dos entradas en el directorio apuntan al mismo inode.

Cuando un disco reporta "no space left" pero `df` muestra espacio libre, el problema puede ser que se agotaron los inodes — hay espacio físico pero no hay más fichas para crear archivos nuevos. Puedes verificarlo con `df -i`.

---

#### `mount` — Montar un filesystem

**Sintaxis:**
```bash
sudo mount dispositivo punto_de_montaje
sudo mount -o loop archivo.img punto_de_montaje   # montar un archivo como disco
sudo mount -t ext4 /dev/sdb1 /mnt/datos           # especificar el tipo de filesystem
mount                                              # listar todo lo que está montado
mount | grep patron                                # filtrar montajes
```

**Qué hace:** Conecta un filesystem a un punto del árbol de directorios. Después de montar, el contenido del disco aparece como si fuera una carpeta normal.

**El flag `-o loop` — qué es un loop device:**

Los loop devices (`/dev/loop0`, `/dev/loop1`, etc.) son dispositivos virtuales que hacen que un **archivo** se comporte como si fuera un **disco físico**. Cuando el kernel ve `/dev/loop0`, lo trata exactamente igual que si fuera un disco real — pero internamente sabe que los datos están en un archivo.

`-o loop` le dice a `mount` que primero cree un loop device para el archivo, y luego monte ese loop device.

```bash
sudo mkdir /mnt/virtualdisk
sudo mount -o loop virtual.img /mnt/virtualdisk
```

**Verificar que quedó montado:**
```bash
mount | grep virtualdisk
```
```
/home/labex/project/virtual.img on /mnt/virtualdisk type ext4 (rw,relatime)
```

**Qué significa esta línea:**

| Parte | Qué dice |
|-------|---------|
| `/home/labex/project/virtual.img` | El origen — en este caso un archivo |
| `on /mnt/virtualdisk` | El punto de montaje — donde aparece el contenido |
| `type ext4` | El sistema de archivos que se detectó |
| `(rw,relatime)` | Opciones: rw = lectura y escritura; relatime = la fecha de acceso se actualiza solo si es anterior a la de modificación (optimización de rendimiento) |

**Usar el disco montado:**
```bash
sudo touch /mnt/virtualdisk/testfile
ls /mnt/virtualdisk
```
```
lost+found  testfile
```

`lost+found` es un directorio especial que crea `mkfs.ext4`. Sirve de repositorio para archivos que el sistema de recuperación (`fsck`) encuentra al reparar el filesystem — archivos cuyos inodes existen pero cuyo nombre se perdió por una corrupción.

**Montaje automático al arrancar — `/etc/fstab`:**

En producción, los discos se montan automáticamente al arrancar usando el archivo `/etc/fstab`. Un ejemplo de entrada:
```
/dev/sdb1    /mnt/datos    ext4    defaults    0    2
UUID=74e7ebed-ee16-49ba-8901-cd702012329d    /mnt/datos    ext4    defaults    0    2
```

Se recomienda usar el UUID (que viste en la salida de `mkfs.ext4`) en vez del nombre del dispositivo — porque si agregas otro disco, el nombre puede cambiar de `/dev/sdb` a `/dev/sdc`, pero el UUID siempre identifica el mismo disco.

---

#### `umount` — Desmontar un filesystem

**Sintaxis:**
```bash
sudo umount /mnt/punto_de_montaje    # desmontar por punto de montaje
sudo umount /dev/dispositivo         # desmontar por dispositivo
```

**Qué hace:** Desconecta el filesystem del árbol de directorios. Después de desmontar, el punto de montaje queda vacío (vuelve a ser una carpeta vacía).

**Ejemplo del lab:**
```bash
sudo umount /mnt/virtualdisk
```

**¿Por qué hay que desmontar antes de desconectar un disco?**

Cuando escribes datos, el kernel no los escribe inmediatamente al disco — los guarda en un buffer en memoria para optimizar rendimiento y los vacía (flush) periódicamente. Si desconectas el disco sin desmontar, puede haber datos en el buffer que todavía no llegaron al disco físico — esos datos se pierden y el filesystem queda en estado inconsistente.

`umount` espera a que todos los buffers se vacíen antes de completarse. Es equivalente al "expulsar dispositivo" de Windows o macOS.

**Error frecuente — "device is busy":**
```
umount: /mnt/virtualdisk: target is busy
```
Esto ocurre cuando hay un proceso que tiene un archivo abierto en ese directorio, o cuando tu propio shell está dentro del punto de montaje (`cd /mnt/virtualdisk` y luego intentas desmontarlo). Soluciones:
```bash
# Ver qué proceso está usando el disco
lsof /mnt/virtualdisk
# O salir del directorio primero
cd ~
sudo umount /mnt/virtualdisk
```

---

#### `fdisk -l` — Ver la tabla de particiones

**Sintaxis:**
```bash
sudo fdisk -l                  # lista todos los discos y sus particiones
sudo fdisk -l /dev/sda         # solo el disco indicado
sudo fdisk -l virtual.img      # también funciona con archivos de imagen
```

**Qué hace:** Muestra información detallada de todos los discos detectados: tamaño, modelo, sectores, y la tabla de particiones de cada uno.

**Ejemplo del lab — salida completa:**
```bash
sudo fdisk -l
```
```
Disk /dev/loop4: 200 MiB, 209715200 bytes, 409600 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/nvme1n1: 100 GiB, 107374182400 bytes, 209715200 sectors
Disk model: Alibaba Cloud Elastic Block Storage
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes


Disk /dev/nvme0n1: 40 GiB, 42949672960 bytes, 83886080 sectors
Disk model: Alibaba Cloud Elastic Block Storage
Units: sectors of 1 * 512 = 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disklabel type: dos
Disk identifier: 0xfcadb325

Device         Boot Start      End  Sectors Size Id Type
/dev/nvme0n1p1 *     2048 83886046 83883999  40G 83 Linux
```

**Qué hay en este sistema:**

| Disco | Tamaño | Qué es |
|-------|--------|--------|
| `/dev/loop4` | 200 MiB | Un loop device — hay un archivo de imagen montado como disco |
| `/dev/nvme1n1` | 100 GiB | Disco NVMe real — en LabEx es el almacenamiento del contenedor |
| `/dev/nvme0n1` | 40 GiB | El disco del sistema operativo — tiene la partición de arranque |

**Desglosando la tabla de particiones:**
```
Device         Boot Start      End  Sectors Size Id Type
/dev/nvme0n1p1 *     2048 83886046 83883999  40G 83 Linux
```

| Columna | Valor | Qué significa |
|---------|-------|--------------|
| `Device` | `/dev/nvme0n1p1` | Nombre del dispositivo — disco `nvme0n1`, partición `p1` |
| `Boot` | `*` | Esta partición es booteable — el gestor de arranque (GRUB) la busca aquí |
| `Start` | `2048` | El primer sector de la partición (los primeros 2048 sectores están reservados para el MBR) |
| `End` | `83886046` | El último sector |
| `Sectors` | `83883999` | Total de sectores en la partición |
| `Size` | `40G` | Tamaño total |
| `Id` | `83` | Tipo de partición en hexadecimal — 83 significa Linux (ext2/3/4) |
| `Type` | `Linux` | Descripción del tipo |

**Convenciones de nombres de dispositivos en Linux:**

| Nombre | Tipo de disco |
|--------|--------------|
| `/dev/sda`, `/dev/sdb` | Disco SATA o SAS — el más común en servidores tradicionales |
| `/dev/nvme0n1`, `/dev/nvme1n1` | Disco NVMe — los SSD modernos de alta velocidad |
| `/dev/vda`, `/dev/vdb` | Disco virtual — en máquinas virtuales (KVM, VirtualBox) |
| `/dev/loop0`, `/dev/loop1` | Loop device — un archivo montado como disco |

Y las particiones añaden un número al final: `/dev/sda1`, `/dev/sda2`, `/dev/nvme0n1p1`, `/dev/nvme0n1p2`.

**Ver información de un archivo de imagen:**
```bash
sudo fdisk -l virtual.img
```
```
Disk virtual.img: 256 MiB, 268435456 bytes, 524288 sectors
Units: sectors of 1 * 512 = 512 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
```

El archivo `virtual.img` aparece como si fuera un disco de 256 MiB. No tiene tabla de particiones porque lo formateamos directamente con ext4 sin particionarlo (fue directo al sistema de archivos).

---

#### Flujo completo del lab

```
1. df -h                      → Ver qué filesystems están montados y cuánto espacio libre hay
        ↓
2. du -sh ~                   → ¿Cuánto pesa el home completo?
   du -h --max-depth=1 ~      → ¿Qué hay en el primer nivel?
   du -h ~ | sort -rh | head  → ¿Cuáles son los 10 más grandes?
        ↓
3. dd if=/dev/zero of=virtual.img bs=1M count=256
                              → Crear un archivo de 256MB que simulará un disco
        ↓
4. sudo mkfs.ext4 virtual.img → Formatear el "disco" con ext4 (crea estructura de archivos)
        ↓
5. sudo mkdir /mnt/virtualdisk
   sudo mount -o loop virtual.img /mnt/virtualdisk
                              → Crear punto de montaje y montar el disco virtual
        ↓
6. mount | grep virtualdisk   → Verificar que el montaje fue exitoso
   sudo touch /mnt/virtualdisk/testfile
   ls /mnt/virtualdisk        → Confirmar que podemos escribir en él
        ↓
7. sudo umount /mnt/virtualdisk
                              → Desmontar limpiamente (vacía los buffers antes de soltar)
        ↓
8. sudo fdisk -l              → Ver todos los discos del sistema y sus particiones
   sudo fdisk -l virtual.img  → Ver la imagen como si fuera un disco
```

---

#### Errores frecuentes — Lab 12

**`df: /dev/vdb: No such file or directory`**

El lab de LabEx menciona `/dev/vdb` (un disco virtual adicional) pero en este entorno de contenedor ese disco no existe. `df` sin argumentos o con una ruta válida siempre funciona. El error es del entorno del lab, no de tu comando.

**`mkfs.ext4` sin `sudo` — Permission denied**

Formatear un disco requiere privilegios de root. Sin `sudo`, el comando falla con `mke2fs: No such file or directory while trying to determine filesystem size`. Siempre usa `sudo mkfs.ext4`.

**Montar sin crear el punto de montaje primero**

```
mount: /mnt/virtualdisk: mount point does not exist
```
`mount` no crea el directorio destino — debes crearlo con `mkdir` antes. El directorio puede estar en cualquier parte, pero por convención los montajes temporales van en `/mnt/`.

**`target is busy` al intentar desmontar**

Tu terminal está dentro del directorio que quieres desmontar. Ejecuta `cd ~` primero para salir, y luego `sudo umount /mnt/virtualdisk`. También puede ser otro proceso — usa `lsof /mnt/virtualdisk` para identificarlo.

**`du -h ~` vs `du -sh ~` — la diferencia crítica**

`du -h ~` lista **todos** los subdirectorios recursivamente con su tamaño — puede producir miles de líneas en un home poblado. `du -sh ~` produce solo **una línea** con el total. Para investigar, usa `--max-depth=1` para controlar cuántos niveles bajas.

**Creer que `df` muestra dónde está el espacio usado**

`df` dice que el disco está lleno, pero no dice quién lo llenó. Para eso es `du`. En campo real: primero `df -h` para identificar qué filesystem está lleno, luego `du -h --max-depth=1 /punto_de_montaje | sort -rh | head -20` para descender y encontrar el culpable.

---

#### Ejercicio — Lab 12

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux con sudo.

**Tareas:**

1. Usa `df -h` para ver todos los filesystems montados. Identifica cuál tiene el mayor porcentaje de uso.
2. Usa `du -sh /var` para ver cuánto pesa el directorio `/var`. Luego baja un nivel con `du -h --max-depth=1 /var | sort -rh | head -10`.
3. Crea un disco virtual de 128 MB llamado `disco_prueba.img` usando `dd` con bloques de 1M.
4. Formatea el disco virtual con `mkfs.ext4`.
5. Crea el directorio `/mnt/prueba` y monta el disco virtual ahí.
6. Verifica el montaje con `mount | grep prueba` y con `df -h /mnt/prueba`.
7. Crea tres archivos dentro del disco montado: `archivo1.txt`, `archivo2.txt`, `archivo3.txt`.
8. Desmonta el disco con `umount`.
9. Vuelve a montar el disco y verifica que los tres archivos siguen ahí (los datos persisten en el archivo `.img`).
10. Usa `fdisk -l disco_prueba.img` para ver la información del disco virtual.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
df -h

# Paso 2
sudo du -sh /var
sudo du -h --max-depth=1 /var | sort -rh | head -10

# Paso 3
dd if=/dev/zero of=disco_prueba.img bs=1M count=128

# Paso 4
sudo mkfs.ext4 disco_prueba.img

# Paso 5
sudo mkdir /mnt/prueba
sudo mount -o loop disco_prueba.img /mnt/prueba

# Paso 6
mount | grep prueba
df -h /mnt/prueba

# Paso 7
sudo touch /mnt/prueba/archivo1.txt /mnt/prueba/archivo2.txt /mnt/prueba/archivo3.txt
ls /mnt/prueba

# Paso 8
sudo umount /mnt/prueba

# Paso 9
sudo mount -o loop disco_prueba.img /mnt/prueba
ls /mnt/prueba
# Los archivos siguen ahí — viven en disco_prueba.img, no en la RAM

# Paso 10
sudo fdisk -l disco_prueba.img
```

</details>

---

### Lab 13 — Tuberías, Operadores Condicionales y Procesamiento de Texto

**Escenario:** El equipo de operaciones necesita analizar archivos de configuración del sistema: ¿cuántos directorios tiene `/etc`? ¿Cuántos usuarios usan cada shell? ¿Cuántas líneas de su configuración contienen la variable `PATH`? No existe ningún comando que responda estas preguntas directamente — la respuesta está en combinar herramientas simples con tuberías y operadores lógicos.

> Este lab enseña la filosofía central de Unix: **cada herramienta hace una cosa, pero al combinarlas formas un procesador de datos arbitrariamente poderoso**. Un sysadmin que domina tuberías puede responder en segundos preguntas que tomarían horas programar desde cero.

---

#### Los operadores que conectan comandos: `&&`, `||`, y `|`

Antes de ver los comandos de texto, hay que entender cómo Linux encadena comandos. Hay tres operadores, y tienen lógicas completamente diferentes.

---

**`&&` — AND lógico: "si el primero funciona, ejecuta el segundo"**

```bash
comando1 && comando2
```

El shell ejecuta `comando1`. Si termina con éxito (código de salida 0), ejecuta `comando2`. Si falla (código distinto de 0), el segundo nunca se ejecuta.

**Ejemplos del lab:**
```bash
date && ls ~
```
```
Thu Apr 16 11:00:35 AM CST 2026
Code  Desktop  golang  project
```

`date` siempre tiene éxito → `ls ~` se ejecuta. El resultado es ambos comandos en secuencia.

```bash
sudo apt-get update && sudo apt-get install -y cowsay
```

Este es el patrón más común con `&&` en campo real: primero actualiza la lista de paquetes; si eso funciona, instala. Si `apt-get update` falla (sin internet, repositorio caído), la instalación no se intenta — evita instalar desde una lista desactualizada.

**En campo real, `&&` se usa para:**
- Compilar y ejecutar solo si la compilación fue exitosa: `make && ./programa`
- Respaldar antes de modificar: `cp config.conf config.conf.bak && nano config.conf`
- Verificar antes de borrar: `ls archivos_viejos/ && rm -r archivos_viejos/`
- Encadenar pasos de un proceso que dependen del anterior: `git add . && git commit -m "mensaje" && git push`

---

**`||` — OR lógico: "si el primero falla, ejecuta el segundo"**

```bash
comando1 || comando2
```

El shell ejecuta `comando1`. Si tiene éxito, `comando2` no se ejecuta. Si falla, entonces sí ejecuta `comando2`. Es el "plan B".

**Ejemplo del lab:**
```bash
which cowsay && cowsay "Hello, LabEx" || echo "cowsay is not installed"
```

Este comando hace tres cosas en cadena:
1. `which cowsay` — busca si `cowsay` está instalado
2. Si lo encontró (`&&`), ejecuta `cowsay "Hello, LabEx"`
3. Si `which cowsay` falló (`||`), imprime el mensaje alternativo

**Primera ejecución** (antes de instalar cowsay):
```
cowsay not found
cowsay is not installed
```

**Después de instalar cowsay:**
```
/usr/games/cowsay
 ______________
< Hello, LabEx >
 --------------
        \   ^__^
         \  (oo)\_______
            (__)\       )\/\
                ||----w |
                ||     ||
```

`which cowsay` devuelve la ruta y tiene éxito → `cowsay` se ejecuta → el `||` no se activa.

**En campo real, `||` se usa para:**
- Valores por defecto: `echo $VAR || echo "VAR no está definida"`
- Crear directorio si no existe: `mkdir /tmp/datos 2>/dev/null || true`
- Mensajes de error legibles en scripts: `comando_importante || { echo "Error crítico"; exit 1; }`

**La tabla completa de cómo interactúan `&&` y `||`:**

| `comando1` resulta en | `comando1 && comando2` | `comando1 \|\| comando2` |
|----------------------|----------------------|------------------------|
| Éxito (código 0) | Ejecuta `comando2` | No ejecuta `comando2` |
| Fallo (código ≠ 0) | No ejecuta `comando2` | Ejecuta `comando2` |

> **Código de salida (exit code):** Cada programa en Linux, al terminar, devuelve un número al shell. `0` significa éxito. Cualquier otro número significa que algo salió mal (1 = error genérico, 2 = uso incorrecto, 127 = comando no encontrado...). `&&` y `||` toman decisiones basándose en ese número. Puedes ver el código del último comando con `echo $?`.

---

**`|` — Pipe: "la salida de uno es la entrada del siguiente"**

```bash
comando1 | comando2 | comando3
```

La tubería conecta la **salida estándar** (stdout) de un comando con la **entrada estándar** (stdin) del siguiente. Los tres comandos se ejecutan en paralelo — no es "uno termina y pasa datos al otro", sino que todos corren al mismo tiempo y los datos fluyen conforme se producen.

**Ejemplo del lab:**
```bash
ls -l /etc | grep '^d' | wc -l
```
```
103
```

Desglose paso a paso:

```
ls -l /etc           → lista todo lo que hay en /etc con detalles
      |
grep '^d'            → filtra solo las líneas que empiezan con 'd' (directorios)
      |
wc -l                → cuenta cuántas líneas quedaron
```

Resultado: hay 103 directorios en `/etc`. Ningún comando individual puede decirte eso — es la combinación.

**La diferencia fundamental entre `|`, `&&` y `||`:**

| Operador | Conecta | Cuándo activa el segundo |
|----------|---------|------------------------|
| `\|` | stdout → stdin | Siempre — sin importar si el primero falla |
| `&&` | comandos | Solo si el primero tiene éxito |
| `\|\|` | comandos | Solo si el primero falla |

---

#### `cut` — Extraer campos de texto estructurado

**Sintaxis:**
```bash
cut -d DELIMITADOR -f CAMPOS archivo
cut -d: -f1 /etc/passwd          # solo el primer campo (nombre de usuario)
cut -d: -f1,6 /etc/passwd        # campos 1 y 6 (nombre y directorio home)
cut -d: -f3-5 /etc/passwd        # campos del 3 al 5
cut -c 1-10 archivo              # caracteres del 1 al 10 de cada línea
```

**Qué hace:** Extrae columnas específicas de texto estructurado. Piénsalo como seleccionar columnas de una tabla de Excel, pero para texto plano. Ideal para archivos con un separador consistente (`:`, `,`, `\t`).

**Ejemplo del lab:**
```bash
cut -d: -f1,6 /etc/passwd | head -n 5
```
```
root:/root
daemon:/usr/sbin
bin:/bin
sys:/dev
sync:/bin
```

**El archivo `/etc/passwd` — estructura:**

Cada línea de `/etc/passwd` tiene 7 campos separados por `:`:
```
nombre:contraseña:UID:GID:comentario:home:shell
root   :x        :0  :0  :root      :/root:/bin/bash
```

| Campo | Número | Contenido |
|-------|--------|---------|
| `root` | 1 | Nombre del usuario |
| `x` | 2 | Contraseña (siempre `x` — la real está en `/etc/shadow`) |
| `0` | 3 | UID (User ID) |
| `0` | 4 | GID (Group ID) |
| `root` | 5 | Comentario o nombre completo |
| `/root` | 6 | Directorio home |
| `/bin/bash` | 7 | Shell por defecto |

Con `cut -d: -f1,6` extraemos solo el nombre y el home — ignoramos los otros 5 campos.

**En campo real, `cut` se usa para:**
- Extraer IPs de logs: `cut -d' ' -f1 access.log`
- Obtener nombres de procesos: `ps aux | cut -c 66-` (a partir del carácter 66)
- Procesar CSV: `cut -d, -f2 datos.csv`
- Extraer el primer campo de rutas: `echo $PATH | cut -d: -f1`

---

#### `grep` — Buscar patrones en texto

**Sintaxis:**
```bash
grep "patron" archivo            # busca líneas que contienen el patrón
grep "patron" archivo | wc -l   # contar cuántas líneas coinciden
grep "^d" archivo               # líneas que empiezan con 'd'
grep -v "patron" archivo        # líneas que NO contienen el patrón
grep -i "patron" archivo        # sin distinguir mayúsculas/minúsculas
grep -E "patron1|patron2"       # varios patrones (OR)
```

**Qué hace:** Filtra líneas de texto que coinciden con un patrón. La entrada puede ser un archivo o la salida de otro comando via tubería. Es el filtro más usado en Linux.

**Ejemplos del lab:**

```bash
grep "PATH" ~/.zshrc | wc -l
```
```
14
```
De las líneas de `~/.zshrc`, 14 contienen la palabra "PATH".

```bash
grep "PATH" ~/.zshrc && grep "HOME" ~/.zshrc
```
```
# If you come from bash you might have to change your $PATH.
# export PATH=$HOME/bin:/usr/local/bin:$PATH
export PATH=$PATH:/home/labex/.local/bin
...
# export PATH=$HOME/bin:/usr/local/bin:$PATH
export JAVA_HOME=/usr/lib/jvm/java-11-openjdk-amd64
export JRE_HOME=$JAVA_HOME
```

Aquí `&&` no está filtrando — está ejecutando ambos greps en secuencia (el primero tiene éxito porque encuentra resultados, entonces ejecuta el segundo).

```bash
grep "bin" /etc/passwd | sort | head -n 5
```
```
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
avahi:x:109:114:Avahi mDNS daemon,,,:/run/avahi-daemon:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
colord:x:111:118:colord colour management daemon,,,:/var/lib/colord:/usr/sbin/nologin
```

Primero filtra líneas que contienen "bin", luego las ordena alfabéticamente, luego toma las primeras 5.

**Los patrones especiales de `grep` (expresiones regulares básicas):**

| Patrón | Qué busca | Ejemplo |
|--------|----------|---------|
| `^texto` | Líneas que **empiezan** con "texto" | `grep '^d'` → líneas que empiezan con d |
| `texto$` | Líneas que **terminan** con "texto" | `grep 'bash$'` → líneas que terminan en bash |
| `.` | Cualquier carácter | `grep 'a.b'` → aXb, a1b, a b... |
| `*` | Cero o más del carácter anterior | `grep 'ab*c'` → ac, abc, abbc... |
| `\|` | OR (con `-E`) | `grep -E 'bash\|zsh'` → líneas con bash O zsh |

> `grep '^d'` en el lab filtra los directorios de `ls -l /etc` porque `ls -l` muestra `drwxr-xr-x` para directorios — la `d` es siempre el primer carácter.

---

#### `wc` — Contar líneas, palabras y caracteres

**Sintaxis:**
```bash
wc archivo              # muestra líneas, palabras y caracteres
wc -l archivo           # solo líneas
wc -w archivo           # solo palabras
wc -c archivo           # solo caracteres (bytes)
comando | wc -l         # contar la salida de otro comando
```

**Qué hace:** Word Count — cuenta líneas, palabras o caracteres de un archivo o de la entrada que llega por tubería.

**Ejemplos del lab:**

```bash
ls -l /etc | grep '^d' | wc -l
```
```
103
```
Cuenta cuántos directorios hay en `/etc`.

```bash
grep "PATH" ~/.zshrc | wc -l
```
```
14
```
Cuenta cuántas líneas de `~/.zshrc` mencionan "PATH".

```bash
wc -l /etc/passwd
```
```
35 /etc/passwd
```
El sistema tiene 35 usuarios (una línea por usuario en `/etc/passwd`).

```bash
head -n 10 /etc/passwd | wc -w
```
```
10
```

Esto parece raro: `head` sacó 10 líneas, pero `wc -w` dice 10 palabras — ¿una sola palabra por línea? Sí, porque `wc` define "palabra" como texto separado por espacios. Las líneas de `/etc/passwd` usan `:` como separador, no espacios — así que cada línea completa `root:x:0:0:root:/root:/bin/bash` cuenta como **una sola palabra** (no hay espacios). 10 líneas × 1 palabra = 10.

**`wc -l` vs `wc -w` — cuándo usar cada uno:**

| Flag | Cuándo usarlo |
|------|--------------|
| `-l` | Contar resultados (usuarios, archivos, líneas de log...) |
| `-w` | Contar palabras en texto con espacios (párrafos, comentarios...) |
| `-c` | Medir tamaño de un archivo o salida en bytes |

---

#### `sort` — Ordenar líneas de texto

**Sintaxis:**
```bash
sort archivo                    # orden alfabético ascendente
sort -r archivo                 # orden inverso
sort -n archivo                 # orden numérico (no alfabético)
sort -t: -k3 -n archivo         # ordenar por el campo 3, delimitado por ':', numéricamente
sort -rh archivo                # numérico en unidades humanas (K/M/G), reverso
```

**Qué hace:** Ordena las líneas de un archivo o de una tubería. Sin flags, ordena alfabéticamente. Con flags, puede ordenar por campos específicos o por valor numérico.

**Ejemplo del lab:**
```bash
sort -t: -k3 -n /etc/passwd | head -n 5
```
```
root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
```

Esto ordena el archivo de usuarios por UID (el tercer campo) de menor a mayor. El resultado muestra que `root` tiene UID 0, `daemon` tiene 1, `bin` tiene 2...

**Desglose de los flags:**

| Flag | Qué hace en este contexto |
|------|--------------------------|
| `-t:` | El separador de campos es `:` (igual que en `cut`) |
| `-k3` | Ordena por el campo número 3 (el UID) |
| `-n` | Orden numérico — sin esto, `10` vendría antes de `2` porque `1` < `2` en texto |

**Por qué `-n` importa tanto:**

Sin `-n` (orden alfabético):
```
10
2
35
9
```

Con `-n` (orden numérico):
```
2
9
10
35
```

El ejemplo ya lo viste en el Lab 12: `sort -rh` para ordenar tamaños de disco con `du`. Sin `-h`, `9M` quedaría después de `844M` porque el carácter `9` > `8`.

---

#### `uniq` — Eliminar o contar líneas duplicadas

**Sintaxis:**
```bash
uniq archivo                    # elimina líneas consecutivas duplicadas
sort archivo | uniq             # el patrón completo: ordenar primero, luego deduplicar
sort archivo | uniq -c          # contar cuántas veces aparece cada línea
sort archivo | uniq -d          # mostrar solo las que tienen duplicados
sort archivo | uniq -u          # mostrar solo las que son únicas (sin duplicados)
```

**Qué hace:** Elimina líneas **consecutivas** repetidas. La limitación clave es "consecutivas" — por eso casi siempre se usa después de `sort`.

**Ejemplos del lab:**

```bash
cut -d: -f7 /etc/passwd | sort | uniq
```
```
/bin/bash
/bin/false
/bin/sh
/bin/sync
/usr/bin/zsh
/usr/sbin/nologin
```

Extrae el campo 7 (shell por defecto) de todos los usuarios, los ordena y elimina duplicados. Resultado: los shells únicos que existen en el sistema.

```bash
cut -d: -f7 /etc/passwd | sort | uniq -c
```
```
      1 /bin/bash
      1 /bin/false
      1 /bin/sh
      1 /bin/sync
      1 /usr/bin/zsh
     30 /usr/sbin/nologin
```

El mismo pipeline pero con `-c` (count). Ahora ves cuántos usuarios usan cada shell. Resultado revelador: 30 de los 35 usuarios del sistema usan `/usr/sbin/nologin` — son cuentas de servicio que no pueden iniciar sesión interactivamente. Solo hay 1 usuario real con shell interactivo (`/bin/bash`, que es root).

**Por qué `sort` antes de `uniq` es obligatorio:**

`uniq` solo elimina duplicados **adyacentes**. Si el archivo es:
```
bash
nologin
bash
nologin
```
`uniq` sin `sort` devolvería las 4 líneas (ninguna está adyacente a su duplicado). Con `sort` primero:
```
bash
bash
nologin
nologin
```
Ahora `uniq` puede eliminar: `bash`, `nologin`.

---

#### Técnica avanzada: pipe hacia un bloque `{ }`

**Ejemplo del lab:**
```bash
grep "sh" /etc/passwd | wc -l | {
  read count
  [ $count -gt 5 ] && grep "sh" /etc/passwd || echo "Found $count lines, not enough to display."
}
```
```
Found 4 lines, not enough to display.
```

Este patrón canaliza la salida de `wc -l` (un número) hacia un bloque de código `{ }`:

1. `grep "sh" /etc/passwd | wc -l` → produce `4` (hay 4 líneas que contienen "sh")
2. `read count` → la variable `count` toma el valor `4` que llegó por tubería
3. `[ $count -gt 5 ]` → ¿es 4 mayor que 5? No
4. Como la condición falla (`&&` no activa el segundo), el `||` sí activa el `echo`
5. Resultado: imprime el mensaje con el conteo

Esto demuestra que puedes pipe-ar hacia lógica completa, no solo comandos simples.

> Este patrón es el precursor de los scripts: cuando la lógica se vuelve más compleja, el siguiente paso natural es moverla a un archivo `.sh`.

---

#### Flujo completo del lab

```
1. date && ls ~                         → Ejecutar dos comandos en secuencia (ambos siempre tienen éxito)
        ↓
2. which cowsay && cowsay "..." || echo "no instalado"
                                        → Verificar si existe → usarlo → o alternativa
        ↓
3. sudo apt-get update && sudo apt-get install -y cowsay
                                        → Patrón clásico: actualizar y luego instalar
        ↓
4. ls -l /etc | grep '^d' | wc -l      → Contar directorios en /etc (pipeline de 3 comandos)
        ↓
5. cut -d: -f1,6 /etc/passwd           → Extraer nombre y home de cada usuario
        ↓
6. grep "PATH" ~/.zshrc | wc -l        → Contar líneas de config que mencionan PATH
        ↓
7. grep "bin" /etc/passwd | sort | head → Filtrar, ordenar y tomar los primeros
        ↓
8. wc -l /etc/passwd                   → Contar usuarios del sistema
        ↓
9. sort -t: -k3 -n /etc/passwd | head  → Ordenar usuarios por UID
        ↓
10. cut -d: -f7 /etc/passwd | sort | uniq -c
                                        → Contar cuántos usuarios usan cada shell
```

---

#### Errores frecuentes — Lab 13

**`&&` en lugar de `|` — comandos que no se conectan**

```bash
ls -l /etc && grep '^d'    # ERROR conceptual
ls -l /etc | grep '^d'     # CORRECTO
```
`&&` ejecuta `grep '^d'` como comando independiente (sin entrada), que queda esperando texto del teclado. `|` conecta la salida de `ls` como entrada de `grep`.

**`uniq` sin `sort` — duplicados que no se eliminan**

Si los duplicados no están juntos en el archivo, `uniq` no los detecta. Siempre el patrón es `sort | uniq`, no solo `uniq`.

**`cut` con el delimitador equivocado**

`cut -d: -f1 archivo.csv` en un CSV separado por comas no funciona — el delimitador es `,`. La flag `-d` acepta exactamente un carácter. Para CSV: `cut -d, -f1`.

**`wc -l` cuenta una línea más si el archivo no termina en newline**

Algunos archivos generados por programas no tienen salto de línea al final. `wc -l` cuenta saltos de línea, no líneas — así que un archivo con `N` líneas pero sin `\n` final reporta `N-1`. Para contar líneas reales: `grep -c '' archivo`.

**`grep "patron"` sin comillas en patrones con espacios o caracteres especiales**

```bash
grep path=/home /etc/passwd        # si "path=/home" tiene caracteres especiales, falla
grep "path=/home" /etc/passwd      # CORRECTO — comillas protegen el patrón
```

**`sort -n` con texto no numérico**

`sort -n` en un campo de texto produce resultados impredecibles. Solo usa `-n` cuando el campo es efectivamente un número (UID, contador, tamaño...).

---

#### Ejercicio — Lab 13

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Preparación:**
```bash
# Crea un archivo de datos de prueba
cat << 'EOF' > ~/ventas.csv
producto,cantidad,precio
manzana,5,1.50
naranja,3,2.00
manzana,8,1.50
pera,2,3.00
naranja,6,2.00
banana,10,0.80
pera,1,3.00
manzana,3,1.50
EOF
```

**Tareas:**

1. Usa `wc -l ~/ventas.csv` para saber cuántas líneas tiene el archivo (incluyendo el encabezado).
2. Extrae solo la columna de productos con `cut -d, -f1 ~/ventas.csv`.
3. Pipe ese resultado a `sort | uniq -c | sort -rn` para saber cuántas veces aparece cada producto.
4. Cuenta cuántos directorios hay en `/tmp` con `ls -l /tmp | grep '^d' | wc -l`.
5. Lista los shells únicos del sistema con `cut -d: -f7 /etc/passwd | sort | uniq`.
6. Verifica si el comando `tree` está instalado con `which tree && tree /tmp --max-depth 1 || echo "tree no está instalado"`.
7. Usa `wc -l /etc/passwd && wc -l /etc/group` para contar usuarios y grupos del sistema.
8. Encadena: extrae el campo de home de `/etc/passwd`, ordénalos y muestra los 5 primeros: `cut -d: -f6 /etc/passwd | sort | head -5`.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
wc -l ~/ventas.csv

# Paso 2
cut -d, -f1 ~/ventas.csv

# Paso 3
cut -d, -f1 ~/ventas.csv | sort | uniq -c | sort -rn

# Paso 4
ls -l /tmp | grep '^d' | wc -l

# Paso 5
cut -d: -f7 /etc/passwd | sort | uniq

# Paso 6
which tree && tree /tmp --max-depth 1 || echo "tree no está instalado"

# Paso 7
wc -l /etc/passwd && wc -l /etc/group

# Paso 8
cut -d: -f6 /etc/passwd | sort | head -5
```

</details>

---

### Lab 14 — Desafío: Procesar Datos de Sensores

**Escenario:** El sistema de sensores de una nave espacial está capturando detecciones de naves enemigas en un archivo de texto crudo (`sensor_data.txt`). El problema: el archivo tiene ruido — hay otros tipos de eventos mezclados, y hay detecciones duplicadas registradas dos veces con el mismo timestamp y sector. El objetivo es extraer solo las detecciones de naves enemigas, ordenarlas cronológicamente y eliminar los duplicados exactos — todo en un solo comando y guardar el resultado limpio en otro archivo.

> Este desafío combina tres herramientas del Lab 13 en una sola línea de producción: `grep` para filtrar, `sort` para ordenar, `uniq` para deduplicar. La parte que confunde es `-k1,1` en `sort` — y tiene una lógica que vale la pena entender bien porque es una de las flags más comunes en procesamiento de datos reales.

---

#### El comando completo — autopsia

```bash
grep "Detected enemy vessel" /home/labex/project/sensor_data.txt | sort -k1,1 | uniq > /home/labex/project/processed_sensor_data.txt
```

Desglosado pieza por pieza:

| Pieza | Qué hace |
|-------|---------|
| `grep "Detected enemy vessel"` | Filtra solo las líneas que contienen esa frase exacta |
| `/home/labex/project/sensor_data.txt` | El archivo de entrada con todos los eventos crudos |
| `\|` | Pipe — la salida de grep se convierte en entrada de sort |
| `sort -k1,1` | Ordena las líneas usando solo el primer campo como clave |
| `\|` | Pipe — la salida de sort se convierte en entrada de uniq |
| `uniq` | Elimina líneas consecutivas idénticas (los duplicados exactos) |
| `>` | Redirige la salida a un archivo (crea o sobreescribe) |
| `/home/labex/project/processed_sensor_data.txt` | El archivo de salida con los datos limpios |

---

#### La parte que confunde: `sort -k1,1`

Este es el núcleo del desafío. Para entenderlo bien hay que entender cómo `sort` define los "campos".

**Cómo `sort` divide una línea en campos:**

Por defecto, `sort` usa espacios en blanco como separador de campos. Cada palabra separada por espacios es un campo numerado desde 1.

Una línea del archivo:
```
0001h - Detected enemy vessel at sector O4
```

Los campos son:
```
Campo 1: 0001h
Campo 2: -
Campo 3: Detected
Campo 4: enemy
Campo 5: vessel
Campo 6: at
Campo 7: sector
Campo 8: O4
```

**Qué hace `-k` en sort:**

`-k` define la **clave de ordenamiento** — qué parte de la línea se usa para comparar y ordenar. Su sintaxis es:

```
-k INICIO,FIN
```

| Forma | Qué significa | Comportamiento |
|-------|--------------|---------------|
| `sort -k1` | "Empieza en el campo 1 y sigue hasta el **final de la línea**" | Usa todo desde el campo 1 hasta el final como clave |
| `sort -k1,1` | "Empieza en el campo 1 y **termina en el campo 1**" | Usa solo el campo 1 como clave — nada más |
| `sort -k3,5` | "Empieza en el campo 3 y termina en el campo 5" | Usa los campos 3, 4 y 5 como clave |

**¿Por qué importa la diferencia entre `-k1` y `-k1,1`?**

Imagina dos líneas con el mismo timestamp:
```
0002h - Detected enemy vessel at sector F8
0002h - Detected enemy vessel at sector Y5
```

Con `sort -k1` (sin límite de campo):
- La clave de ordenamiento es "todo desde el campo 1 hasta el final": `0002h - Detected enemy vessel at sector F8`
- Compara toda la línea como clave — funciona, pero puede producir un orden diferente al esperado

Con `sort -k1,1`:
- La clave de ordenamiento es exactamente el campo 1: `0002h`
- Cuando dos líneas tienen el mismo campo 1, el orden entre ellas no se determina por la clave — quedan en el orden en que llegaron (orden estable)

**En este lab, `-k1,1` es la elección correcta porque:**
- Solo quieres ordenar por el timestamp (`0001h`, `0002h`...)
- Cuando dos detecciones tienen el mismo timestamp (como `0002h` con sectores F8 y Y5), no quieres que el sector cambie el ordenamiento — ambas están en el mismo momento y deben aparecer juntas para que `uniq` pueda hacer su trabajo
- Si usaras `sort -k1` o `sort` sin flag, ordenaría por toda la línea y podrías separar detecciones del mismo timestamp por la posición del sector en el alfabeto

**Ejemplo visual:**

Con `sort` (sin -k, ordena toda la línea):
```
0002h - Detected enemy vessel at sector F8    ← F antes de Y
0002h - Detected enemy vessel at sector Y5
```

Con `sort -k1,1` (solo por timestamp):
```
0002h - Detected enemy vessel at sector F8    ← también F antes de Y, pero por razón diferente
0002h - Detected enemy vessel at sector Y5
```

En este caso el resultado es el mismo — pero si hubiera una línea como `0001h - Detected enemy vessel at sector Z1`, con `sort` completo podría terminar antes de `0002h - Detected enemy vessel at sector A1` aunque sea un timestamp menor, porque `Z` > `A`. Con `-k1,1` solo compara los timestamps y el orden cronológico es siempre correcto.

**Casos donde `-k` cambia todo:**

```bash
# Archivo de ejemplo: nombre y edad
Alice 30
Bob 25
Carol 30

sort -k2,2n    # Ordena por campo 2 (edad) numéricamente
```
```
Bob 25
Alice 30
Carol 30
```

Sin `-k`, ordenaría: `Alice 30` → `Bob 25` → `Carol 30` (alfabético por nombre).

---

#### Por qué el orden de los tres comandos importa

El pipeline es `grep | sort | uniq`. ¿Por qué ese orden y no otro?

**¿Por qué `grep` va primero?**

`grep` reduce el volumen de datos al principio. Si `sensor_data.txt` tiene 10.000 líneas y solo 500 son detecciones de naves enemigas, `sort` y `uniq` solo trabajan con esas 500 líneas en vez de con las 10.000. Filtrar antes de procesar es siempre más eficiente.

Si pusieras `sort` primero:
```bash
sort -k1,1 sensor_data.txt | grep "Detected enemy vessel" | uniq
```
Funcionaría, pero `sort` haría trabajo extra ordenando las 10.000 líneas antes de que `grep` las reduzca.

**¿Por qué `sort` va antes de `uniq`?**

`uniq` solo elimina duplicados **consecutivos**. Si el archivo contiene:
```
0001h - Detected enemy vessel at sector O4   ← primera aparición
0005h - Detected enemy vessel at sector D1
0001h - Detected enemy vessel at sector O4   ← duplicado, pero NO es consecutivo
```

`uniq` sin `sort` dejaría las tres líneas — no detecta que la primera y tercera son iguales porque no están juntas.

Con `sort -k1,1` primero:
```
0001h - Detected enemy vessel at sector O4
0001h - Detected enemy vessel at sector O4   ← ahora sí están juntas
0005h - Detected enemy vessel at sector D1
```

Ahora `uniq` elimina el duplicado perfectamente.

**El orden correcto siempre es: filtrar → ordenar → deduplicar.**

---

#### La redirección `>` — guardar en archivo

```bash
... | uniq > /home/labex/project/processed_sensor_data.txt
```

`>` redirige la salida estándar a un archivo. Si el archivo no existe, lo crea. Si ya existe, lo **sobreescribe completamente** — el contenido anterior se pierde.

| Operador | Comportamiento | Cuándo usar |
|----------|---------------|------------|
| `>` | Crea el archivo o sobreescribe si existe | Cuando quieres un resultado limpio cada vez |
| `>>` | Agrega al final del archivo si existe; lo crea si no | Cuando quieres acumular resultados (logs, respaldos) |

En este lab se usa `>` porque cada vez que procesas los sensores quieres un archivo limpio con el resultado actual, no una acumulación de ejecuciones anteriores.

**Verificar el resultado:**
```bash
cat processed_sensor_data.txt
```

Muestra el contenido del archivo resultante — las detecciones filtradas, ordenadas y deduplicadas.

---

#### Errores que probablemente ocurrieron

**`sort -k1` sin `,1`**

```bash
grep "Detected enemy vessel" sensor_data.txt | sort -k1 | uniq > resultado.txt
```

Esto funciona casi igual para este archivo específico — pero no es semánticamente correcto. `sort -k1` ordena desde el campo 1 hasta el final de la línea, lo que puede dar resultados inesperados cuando los timestamps son iguales. La forma precisa es siempre `-k1,1`.

**`uniq` antes de `sort`**

```bash
grep "Detected enemy vessel" sensor_data.txt | uniq | sort -k1,1 > resultado.txt
```

Los duplicados no están juntos en el archivo original (el sensor registra eventos en orden de llegada, no agrupados). `uniq` no elimina nada porque los duplicados no son consecutivos. Después de `sort`, los duplicados llegan ordenados y ya no pueden ser eliminados — `sort` solo los pone juntos, `uniq` necesita operar después.

**`>>` en vez de `>`**

```bash
grep "Detected enemy vessel" sensor_data.txt | sort -k1,1 | uniq >> resultado.txt
```

Cada vez que ejecutas el comando, agrega el resultado al archivo. Si lo ejecutas tres veces, el archivo tiene tres copias de los datos. Para un archivo procesado que debe estar limpio, siempre `>`.

**`grep` sin comillas en el patrón**

```bash
grep Detected enemy vessel sensor_data.txt
```

Sin comillas, `grep` interpreta `Detected` como el patrón y `enemy`, `vessel`, `sensor_data.txt` como archivos a buscar — que no existen. El patrón con espacios siempre va entre comillas dobles.

**Rutas relativas cuando se está en el directorio incorrecto**

```bash
grep "Detected enemy vessel" sensor_data.txt | sort -k1,1 | uniq > processed_sensor_data.txt
```

Si estás en `/home/labex/project/` esto funciona. Pero si estás en `/home/labex/` o en cualquier otro directorio, `sensor_data.txt` no se encuentra. El lab usa rutas absolutas (`/home/labex/project/...`) para garantizar que funcione sin importar dónde esté el shell.

---

#### Flujo completo visualizado

```
sensor_data.txt (datos crudos, todos los eventos)
        ↓
grep "Detected enemy vessel"
        → filtra: solo líneas con detecciones de naves enemigas
        → descarta: alarmas, lecturas de temperatura, otros eventos
        ↓
sort -k1,1
        → ordena cronológicamente por el timestamp (campo 1: 0001h, 0002h...)
        → si dos detecciones tienen el mismo timestamp, las deja juntas
        → los duplicados exactos ahora son líneas consecutivas
        ↓
uniq
        → elimina las líneas consecutivas idénticas
        → mantiene una sola copia de cada detección única
        ↓
> processed_sensor_data.txt (resultado limpio)
```

---

#### La clave mental para recordar `-k INICIO,FIN`

> "Empieza a comparar en el campo INICIO y **para** en el campo FIN."
>
> `-k1,1` = "empieza en campo 1, para en campo 1" → usa solo el campo 1.
> `-k1` = "empieza en campo 1, no pares" → usa el campo 1 y todo lo que le sigue.
>
> Si solo quieres un campo exacto, siempre escribe el mismo número dos veces: `-k3,3`, `-k2,2`, `-k7,7`.

---

#### Ejercicio — Lab 14

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Preparación:**
```bash
cat << 'EOF' > ~/sistema_eventos.log
1001 ERROR disco lleno en /var
1002 INFO backup completado
1001 ERROR disco lleno en /var
1003 WARNING temperatura alta en CPU
1004 INFO usuario root inició sesión
1003 WARNING temperatura alta en CPU
1002 INFO backup completado
1005 ERROR conexión rechazada en puerto 22
1003 WARNING temperatura alta en CPU
1006 INFO usuario labex inició sesión
EOF
```

**Tareas:**

1. Usa `grep "ERROR" ~/sistema_eventos.log` para ver solo los errores.
2. Conecta con `| sort -k1,1` para ordenarlos por código de evento.
3. Agrega `| uniq` para eliminar duplicados.
4. Redirige el resultado a `~/errores_unicos.log` con `>`.
5. Usa `cat ~/errores_unicos.log` para verificar el resultado.
6. **Desafío extra:** Cuenta cuántos eventos únicos de WARNING hay con `grep "WARNING" ~/sistema_eventos.log | sort -k1,1 | uniq | wc -l`.

<details>
<summary>Ver solución</summary>

```bash
# Pasos 1-4 en un solo comando
grep "ERROR" ~/sistema_eventos.log | sort -k1,1 | uniq > ~/errores_unicos.log

# Paso 5
cat ~/errores_unicos.log

# Paso 6
grep "WARNING" ~/sistema_eventos.log | sort -k1,1 | uniq | wc -l
```

**Resultado esperado de errores_unicos.log:**
```
1001 ERROR disco lleno en /var
1005 ERROR conexión rechazada en puerto 22
```
Dos errores únicos — `1001` apareció dos veces en el original, `uniq` lo redujo a uno.

</details>

---

### Lab 15 — tr, col, join y paste: Transformar y Combinar Texto

**Escenario:** Los datos de texto rara vez llegan en el formato exacto que necesitas. A veces hay que cambiar mayúsculas, limpiar caracteres no deseados, convertir tabulaciones a espacios, cruzar datos de dos archivos por un campo común, o pegar columnas de archivos distintos lado a lado. Este lab enseña cuatro herramientas de transformación que hacen exactamente eso — cada una resuelve un problema diferente, y juntas cubren la mayor parte del trabajo de transformación de texto del día a día.

---

#### `tr` — Traducir, eliminar o comprimir caracteres

**Sintaxis:**
```bash
echo "texto" | tr SET1 SET2       # reemplaza caracteres de SET1 por los de SET2
echo "texto" | tr -d SET1         # elimina todos los caracteres de SET1
echo "texto" | tr -s SET1         # comprime repeticiones consecutivas de SET1
```

**Qué hace:** `tr` (translate) transforma el texto carácter por carácter. No trabaja con palabras ni líneas — trabaja con caracteres individuales. Siempre recibe texto por tubería (no acepta archivos como argumento directamente).

> Piénsalo como una tabla de sustitución: "cada vez que veas el carácter A, cámbialo por el carácter X". La tabla se define con los dos conjuntos que le das.

---

**`tr SET1 SET2` — Mapeo de caracteres uno a uno**

Cada carácter en SET1 se reemplaza por el carácter en la misma posición de SET2.

**Ejemplo del lab:**
```bash
echo 'hello world' | tr 'ol' 'OL'
```
```
heLLO wOrLd
```

La tabla de mapeo es:
```
o → O
l → L
```

Cada `o` minúscula en la entrada se convierte en `O` mayúscula, y cada `l` se convierte en `L`. Las demás letras no cambian. Nota que hay dos `l` seguidas en "hello" — cada una se mapea individualmente, por eso el resultado tiene dos `L`.

**Ejemplo más simple:**
```bash
echo 'abc' | tr 'abc' 'xyz'
# a→x, b→y, c→z
```
```
xyz
```

**La regla del mapeo:** SET1 y SET2 deben tener el mismo número de caracteres. Si SET2 es más corto, el último carácter de SET2 se usa para todos los caracteres restantes de SET1.

---

**`tr '[:lower:]' '[:upper:]'` — Clases de caracteres**

```bash
echo 'hello labex' | tr '[:lower:]' '[:upper:]'
```
```
HELLO LABEX
```

En lugar de listar cada letra del alfabeto (`tr 'abcdefghijklmnopqrstuvwxyz' 'ABCDEFGHIJKLMNOPQRSTUVWXYZ'`), `tr` tiene clases predefinidas:

| Clase | Qué representa |
|-------|---------------|
| `[:lower:]` | Todas las letras minúsculas (a-z) |
| `[:upper:]` | Todas las letras mayúsculas (A-Z) |
| `[:digit:]` | Todos los dígitos (0-9) |
| `[:alpha:]` | Todas las letras (a-z y A-Z) |
| `[:alnum:]` | Letras y dígitos |
| `[:space:]` | Espacios, tabulaciones, saltos de línea |
| `[:punct:]` | Signos de puntuación |

`tr '[:lower:]' '[:upper:]'` es la forma correcta de convertir todo a mayúsculas — funciona incluso con letras acentuadas en algunos sistemas, mientras que `tr 'a-z' 'A-Z'` puede fallar con caracteres no ASCII.

**En campo real:** Normalizar nombres antes de comparar, convertir cabeceras de CSV, preparar datos para herramientas que son sensibles a mayúsculas.

---

**`tr -d SET` — Eliminar caracteres**

```bash
echo "hello labex" | tr -d 'olh'
```
```
e abex
```

`-d` (delete) elimina cada carácter del conjunto sin reemplazarlo por nada. De "hello labex": `h` eliminado, `e` queda, `l` eliminado, `l` eliminado, `o` eliminado, ` ` queda, `l` eliminado, `a` queda, `b` queda, `e` queda, `x` queda.

Resultado: `e abex` (con el espacio en su lugar).

**Usos reales de `tr -d`:**
```bash
# Eliminar saltos de línea (unir todo en una línea)
cat archivo.txt | tr -d '\n'

# Eliminar tabulaciones
cat archivo.txt | tr -d '\t'

# Eliminar dígitos de un texto
echo "abc123def456" | tr -d '[:digit:]'
# abc def

# Eliminar caracteres de retorno de carro Windows (\r) de archivos convertidos
cat archivo_windows.txt | tr -d '\r' > archivo_linux.txt
```

Este último caso es muy común en equipos mixtos Windows/Linux: los archivos de texto de Windows terminan las líneas con `\r\n` (retorno de carro + nueva línea), pero Linux espera solo `\n`. Archivos con `\r` extra causan problemas en scripts.

---

**`tr -s SET` — Comprimir (squeeze) caracteres repetidos**

```bash
echo 'hello' | tr -s 'l'
```
```
helo
```

`-s` (squeeze) reemplaza una secuencia de caracteres idénticos **consecutivos** por uno solo. "hello" tiene dos `l` seguidas → se comprimen a una sola.

```bash
echo 'ballon' | tr -s 'o'
```
```
ballon
```

"ballon" tiene solo una `o` → no hay nada que comprimir → la salida es idéntica a la entrada. `tr -s` no cambia nada si el carácter ya aparece solo.

**Uso real de `-s`:**
```bash
# Comprimir espacios múltiples a uno solo
echo "esto    tiene   muchos    espacios" | tr -s ' '
# esto tiene muchos espacios

# Limpiar líneas vacías múltiples de un archivo
cat archivo.txt | tr -s '\n'
```

---

#### `cat -A` y `col -x` — Ver y limpiar caracteres invisibles

**`cat -A` — Mostrar todos los caracteres, incluyendo invisibles**

```bash
cat -A /etc/protocols | head -n 10
```
```
# Internet (IP) protocols$
#$
ip^I0^IIP^I^I# internet protocol$
```

`cat -A` agrega marcas a los caracteres no visibles:

| Símbolo que muestra | Carácter real | Qué es |
|--------------------|---------------|--------|
| `$` al final | `\n` | Fin de línea (newline) — aparece al final de **cada** línea |
| `^I` | `\t` | Tabulación horizontal (Tab) |
| `^M` | `\r` | Retorno de carro (carriage return) — señal de que el archivo es de Windows |
| `^@` | `\0` | Byte nulo |

En la salida del lab, `ip^I0^IIP^I^I# internet protocol` significa: la palabra `ip`, luego un Tab (`^I`), luego `0`, luego un Tab, luego `IP`, luego dos Tabs, luego el comentario.

**Por qué esto importa en campo real:**

Cuando un script falla con comportamiento extraño, `cat -A` revela caracteres ocultos que causan el problema. Los más comunes:
- `^M` al final de líneas → archivo fue editado en Windows y tiene `\r\n` en vez de `\n`
- `^I` donde no debería haber → el archivo usa tabs donde el script espera espacios (o viceversa)
- `$` en una posición inesperada → puede indicar un salto de línea embebido en medio de un campo

---

**`col -x` — Convertir tabulaciones a espacios**

```bash
cat /etc/protocols | col -x | cat -A | head -n 10
```
```
ip      0       IP              # internet protocol$
```

Comparado con la versión sin `col -x`:
```
ip^I0^IIP^I^I# internet protocol$
```

`col -x` reemplaza cada tabulación (`^I`) por los espacios necesarios para llegar a la siguiente columna de 8 en 8. El resultado es texto con espacios en vez de tabs — visualmente similar pero sin el carácter de tabulación.

**Pipeline en este ejemplo:**

```
cat /etc/protocols          → lee el archivo con tabulaciones
      |
col -x                      → convierte cada \t a espacios equivalentes
      |
cat -A                      → muestra el resultado para verificar que no hay ^I
      |
head -n 10                  → toma solo las primeras 10 líneas
```

**Cuándo usar `col -x`:**
- Preparar texto con tabs para herramientas que no los entienden
- Convertir salida de columnas (como `column -t` o `ps aux`) antes de procesarla con `cut` (que usa espacios, no tabs, por defecto)
- Limpiar archivos de documentación que mezclan tabs y espacios

---

#### `join` — Cruzar datos de dos archivos por un campo común

**Sintaxis:**
```bash
join archivo1 archivo2                 # join por el campo 1 de ambos archivos
join -1 N -2 M archivo1 archivo2       # join por el campo N de archivo1 y campo M de archivo2
join -a 1 archivo1 archivo2            # incluir también las líneas sin coincidencia de archivo1
```

**Qué hace:** `join` es la versión de terminal del `JOIN` de SQL. Une líneas de dos archivos cuando tienen el mismo valor en un campo determinado. Produce una línea combinada por cada coincidencia.

**Regla crítica: ambos archivos deben estar ordenados por el campo que se usa como clave de join**, de lo contrario el resultado es incorrecto o vacío.

**Preparación del lab:**
```bash
echo -e "1 apple\n2 banana\n3 cherry" > fruits.txt
echo -e "1 red\n2 yellow\n3 red" > colors.txt
```

Esto crea:
```
fruits.txt          colors.txt
1 apple             1 red
2 banana            2 yellow
3 cherry            3 red
```

**Ejemplo básico:**
```bash
join fruits.txt colors.txt
```
```
1 apple red
2 banana yellow
3 cherry red
```

`join` usó el campo 1 (el número) como clave:
- Línea con `1`: `apple` de fruits + `red` de colors → `1 apple red`
- Línea con `2`: `banana` + `yellow` → `2 banana yellow`
- Línea con `3`: `cherry` + `red` → `3 cherry red`

El campo clave aparece una sola vez en el resultado.

---

**`join -1 2 -2 2` — Join por el campo 2 de ambos archivos**

```bash
join -1 2 -2 2 <(sort -k2 fruits.txt) <(sort -k2 colors.txt)
```
```
(salida vacía)
```

Este comando intentó unir ambos archivos por su campo 2:
- Campo 2 de `fruits.txt`: `apple`, `banana`, `cherry`
- Campo 2 de `colors.txt`: `red`, `yellow`, `red`

No hay ningún valor en común entre esos dos conjuntos (`apple` ≠ `red`, `banana` ≠ `yellow`...) → cero coincidencias → salida vacía. El comando es sintácticamente correcto, pero los datos no tienen valores que coincidan en esa columna.

**Qué hace cada parte de `-1 2 -2 2`:**

| Parte | Qué dice |
|-------|---------|
| `-1 2` | "Usa el campo 2 del **primer** archivo como clave" |
| `-2 2` | "Usa el campo 2 del **segundo** archivo como clave" |

**La sintaxis `<()` — sustitución de proceso:**

```bash
<(sort -k2 fruits.txt)
```

Esto es **sustitución de proceso** (process substitution). `<()` ejecuta el comando dentro de los paréntesis y le pasa su salida como si fuera un archivo temporal. `join` necesita archivos como argumentos, no tuberías — `<()` resuelve eso.

Equivale a:
```bash
# Forma larga
sort -k2 fruits.txt > /tmp/fruits_sorted.txt
sort -k2 colors.txt > /tmp/colors_sorted.txt
join -1 2 -2 2 /tmp/fruits_sorted.txt /tmp/colors_sorted.txt
rm /tmp/fruits_sorted.txt /tmp/colors_sorted.txt
```

`<()` hace todo eso en una sola línea sin archivos temporales.

**En campo real, `join` se usa para:**
- Cruzar un archivo de usuarios con un archivo de permisos (por username)
- Combinar reportes de ventas con catálogo de productos (por ID de producto)
- Unir logs de dos sistemas diferentes por timestamp
- El equivalente de `INNER JOIN` en SQL pero en la línea de comandos

---

#### `paste` — Pegar archivos lado a lado por columnas

**Sintaxis:**
```bash
paste archivo1 archivo2 archivo3       # une columnas con Tab como separador
paste -d ':' archivo1 archivo2         # usa ':' como separador en vez de Tab
paste -s archivo1 archivo2            # modo serial: cada archivo se convierte en una línea
```

**Qué hace:** `paste` une archivos horizontalmente — toma la primera línea de cada archivo y las pone en una sola línea separadas por el delimitador. Es como `join` pero sin necesidad de campo común: une por posición (línea 1 con línea 1, línea 2 con línea 2...).

**Preparación del lab:**
```bash
echo -e "apple\nbanana\ncherry" > fruits.txt
echo -e "red\nyellow\nred" > colors.txt
echo -e "sweet\nsweet\nsweet" > tastes.txt
```

Los tres archivos:
```
fruits.txt    colors.txt    tastes.txt
apple         red           sweet
banana        yellow        sweet
cherry        red           sweet
```

---

**`paste` básico — Tab como separador:**
```bash
paste fruits.txt colors.txt tastes.txt
```
```
apple	red	sweet
banana	yellow	sweet
cherry	red	sweet
```

La línea 1 de cada archivo se combina: `apple` + `red` + `sweet`. La línea 2: `banana` + `yellow` + `sweet`. El separador entre columnas es una tabulación (invisible pero está ahí).

---

**`paste -d ':'` — Separador personalizado:**
```bash
paste -d ':' fruits.txt colors.txt tastes.txt
```
```
apple:red:sweet
banana:yellow:sweet
cherry:red:sweet
```

El `:` reemplaza el Tab como separador. Esto produce directamente texto con formato de campos separados por `:` — útil para generar CSV (con `-d ','`) o formatos como `/etc/passwd`.

---

**`paste -s` — Modo serial (cada archivo en una sola línea):**
```bash
paste -s fruits.txt colors.txt tastes.txt
```
```
apple	banana	cherry
red	yellow	red
sweet	sweet	sweet
```

Con `-s`, en lugar de combinar los archivos columna a columna, toma **cada archivo** y pone todas sus líneas en una sola línea separadas por Tab. Útil cuando necesitas convertir una lista vertical en una lista horizontal.

**Diferencia visual entre `paste` normal y `paste -s`:**

```
Sin -s (une líneas correspondientes de cada archivo):
archivo1_línea1  archivo2_línea1  archivo3_línea1
archivo1_línea2  archivo2_línea2  archivo3_línea2

Con -s (serializa cada archivo):
archivo1_línea1  archivo1_línea2  archivo1_línea3
archivo2_línea1  archivo2_línea2  archivo2_línea3
```

---

**`join` vs `paste` — cuándo usar cada uno:**

| Situación | Herramienta | Por qué |
|-----------|------------|---------|
| Los archivos tienen un campo ID en común | `join` | Une por coincidencia de valor, no por posición |
| Los archivos tienen el mismo número de líneas y el orden es la clave | `paste` | Une por posición, sin necesidad de campo común |
| Necesitas algo como SQL JOIN | `join` | Diseñado exactamente para eso |
| Necesitas construir columnas de forma horizontal | `paste` | Diseñado para eso |
| Los archivos pueden tener líneas que no coinciden | `join -a` | `join` con salida de líneas sin coincidencia |

---

#### `echo -e` — Saltos de línea y escapes en `echo`

El lab usa `echo -e "1 apple\n2 banana\n3 cherry"` para crear archivos de varias líneas en un comando.

```bash
echo -e "1 apple\n2 banana\n3 cherry" > fruits.txt
```

`-e` activa la interpretación de secuencias de escape:

| Secuencia | Carácter | Cuándo usarla |
|-----------|---------|--------------|
| `\n` | Salto de línea | Crear archivos multilínea en una sola línea |
| `\t` | Tabulación | Crear texto con columnas alineadas |
| `\r` | Retorno de carro | Raramente — solo al simular formato Windows |
| `\\` | Backslash literal | Cuando necesitas escribir un backslash |

**Sin `-e`:** `echo "\n"` imprime literalmente `\n` — dos caracteres, backslash y n.
**Con `-e`:** `echo -e "\n"` imprime un salto de línea real — una línea vacía.

---

#### El error del lab: `ehco` en vez de `echo`

```bash
ehco -e "red\nyellow\nred" > colors.txt
```
```
zsh: command not found: ehco
```

Un typo clásico. El shell busca el comando `ehco` y no lo encuentra. La consecuencia importante: la redirección `> colors.txt` **no se ejecutó** porque el comando falló. `colors.txt` mantiene su contenido anterior (o no se crea si no existía). Siempre verifica con `cat` después de crear archivos por redirección.

---

#### Flujo completo del lab

```
1. echo 'hello labex' | tr -d 'olh'
   → Eliminar caracteres específicos del texto

2. echo 'hello' | tr -s 'l'
   → Comprimir caracteres repetidos consecutivos

3. echo 'hello labex' | tr '[:lower:]' '[:upper:]'
   → Convertir todo a mayúsculas con clase de caracteres

4. echo 'hello world' | tr 'ol' 'OL'
   → Mapeo de caracteres individuales

5. cat -A /etc/protocols | head
   → Ver los caracteres ocultos (tabs como ^I, fines de línea como $)

6. cat /etc/protocols | col -x | cat -A | head
   → Convertir tabs a espacios y verificar que ^I desapareció

7. echo -e "..." > fruits.txt / colors.txt
   join fruits.txt colors.txt
   → Crear archivos y unirlos por el campo 1 común (el número)

8. join -1 2 -2 2 <(sort -k2 fruits.txt) <(sort -k2 colors.txt)
   → Intentar join por campo 2 — resultado vacío porque no hay valores comunes

9. paste fruits.txt colors.txt tastes.txt
   → Unir tres archivos columna a columna (por posición)

10. paste -d ':' ...
    → Mismo resultado pero con ':' como separador

11. paste -s ...
    → Cada archivo se serializa en una sola línea horizontal
```

---

#### Errores frecuentes — Lab 15

**`tr` con archivos en vez de tuberías**

```bash
tr 'ol' 'OL' archivo.txt    # no funciona como se espera
```

`tr` no acepta archivos como argumento. Siempre necesita su entrada por tubería o redirección:
```bash
cat archivo.txt | tr 'ol' 'OL'
tr 'ol' 'OL' < archivo.txt    # alternativa con redirección de entrada
```

**`tr -s` cuando el carácter no se repite**

Como vimos con `echo 'ballon' | tr -s 'o'` → la salida es `ballon` sin cambios. `tr -s` solo actúa cuando hay dos o más caracteres **consecutivos** iguales. Si solo hay uno, pasa sin cambio. No es un error — es el comportamiento correcto.

**`join` sin ordenar los archivos primero**

`join` requiere que ambos archivos estén ordenados por el campo de join. Sin ordenar:
```bash
join archivo_desordenado.txt otro_archivo.txt
```
Puede producir resultados incorrectos o incompletos silenciosamente. Siempre usa `sort` antes o `<(sort -kN ...)` como en el lab.

**`join` vs `paste` — confundir cuándo usar cada uno**

Si los archivos tienen el mismo número de líneas y ya están alineados por posición, usa `paste`. Si necesitas cruzar por un valor común (como un ID), usa `join`. Usar `paste` cuando debías usar `join` produce líneas mezcladas incorrectamente si los archivos tienen diferentes órdenes.

**`paste -d` con más de un carácter**

`paste -d ':,'` usa los delimitadores en rotación — primero `:`, luego `,`, luego `:`, etc. No concatena los dos caracteres como separador único. Para un separador de dos caracteres como `--`, no hay forma directa con `paste` — habría que postprocesar con `sed`.

---

#### Ejercicio — Lab 15

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux.

**Preparación:**
```bash
echo -e "101 Ana\n102 Bob\n103 Carlos" > empleados.txt
echo -e "101 Ventas\n102 IT\n103 HR" > departamentos.txt
echo -e "101 5000\n102 6000\n103 4500" > salarios.txt
```

**Tareas:**

1. Convierte todos los nombres a mayúsculas: `cat empleados.txt | tr '[:lower:]' '[:upper:]'`
2. Elimina los números de `empleados.txt` con `tr -d '[:digit:]'` y observa el resultado.
3. Usa `cat -A empleados.txt` para verificar si hay caracteres ocultos.
4. Haz join de `empleados.txt` con `departamentos.txt` para ver nombre y departamento de cada uno.
5. Haz join de ese resultado con `salarios.txt` — nota: `join` solo une dos archivos a la vez, así que necesitas dos join consecutivos.
6. Usa `paste -d ',' empleados.txt departamentos.txt salarios.txt` para crear un CSV.
7. Usa `paste -s empleados.txt` para ver todos los empleados en una sola línea.
8. Genera una versión "limpia" de cualquier archivo de sistema con tabs usando `col -x`.

<details>
<summary>Ver solución</summary>

```bash
# Paso 1
cat empleados.txt | tr '[:lower:]' '[:upper:]'

# Paso 2
cat empleados.txt | tr -d '[:digit:]'

# Paso 3
cat -A empleados.txt

# Paso 4
join empleados.txt departamentos.txt

# Paso 5 — dos join encadenados con <()
join empleados.txt departamentos.txt > /tmp/emp_dep.txt
join /tmp/emp_dep.txt salarios.txt
# O en una línea con sustitución de proceso:
join <(join empleados.txt departamentos.txt) salarios.txt

# Paso 6
paste -d ',' empleados.txt departamentos.txt salarios.txt

# Paso 7
paste -s empleados.txt

# Paso 8
col -x < /etc/protocols | head -20
```

</details>

---

### Lab 16 — Desafío: Analizar el PATH con tr

**Escenario:** El desafío pide un script que muestre el PATH completo, luego liste cada directorio en una línea separada, y finalmente cuente cuántos directorios hay en total. El PATH en Linux se almacena como una cadena donde los directorios están separados por `:` — hay que transformar esa cadena con `tr` para hacerla legible y procesable.

---

#### El script completo — autopsia línea por línea

```bash
#!/bin/bash

# Display the full PATH
echo "Full PATH:"
echo "$PATH"

# List each directory in PATH on a separate line
echo
echo "Directories in PATH:"
echo "$PATH" | tr ':' '\n'

# Count the total number of directories in PATH
echo
echo "Total directories in PATH: $(echo "$PATH" | tr ':' '\n' | wc -l)"
```

---

#### Primera pregunta: ¿por qué `"$PATH"` y no `$PATH` o `'$PATH'`?

Esta es una de las diferencias más importantes del shell, y se repite en todo script real. Hay tres formas de escribirlo y las tres se comportan diferente:

**Opción 1: sin comillas — `$PATH`**

```bash
echo $PATH
```

El shell primero expande `$PATH` a su valor (por ejemplo `/usr/bin:/bin:/home/labex/.local/bin`), y luego divide ese valor por espacios. Como el PATH raramente tiene espacios, en la práctica funciona igual. Pero si alguna vez un directorio en el PATH tiene un espacio en su nombre (como `/home/mi usuario/scripts`), el shell lo partiría en dos palabras y el resultado sería incorrecto. No se recomienda para scripts.

**Opción 2: comillas simples — `'$PATH'`**

```bash
echo '$PATH'
```
```
$PATH
```

Las comillas simples desactivan **toda** expansión. El shell ve el `$` como un carácter literal, no como inicio de variable. Imprime exactamente `$PATH` — la cadena de texto, no el valor de la variable. Esto es lo que no querías.

**Opción 3: comillas dobles — `"$PATH"` ← la correcta**

```bash
echo "$PATH"
```
```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/...
```

Las comillas dobles permiten la expansión de variables (el `$` sigue funcionando) pero protegen contra la división por espacios. El valor completo de `$PATH` se trata como **un solo argumento** aunque contenga espacios. Esta es siempre la forma correcta en scripts.

**La regla de oro para scripts:**

| Cuando quieres | Usa |
|---------------|-----|
| El valor de la variable, protegido de división por espacios | `"$VARIABLE"` |
| El texto literal `$VARIABLE` sin expandir | `'$VARIABLE'` |
| El valor expandido sin protección (scripts simples, línea de comandos) | `$VARIABLE` |

> Siempre usa `"$VARIABLE"` en scripts. Nunca uses comillas simples cuando necesitas el valor de una variable. El 90% de los bugs silenciosos en scripts de shell vienen de olvidar las comillas dobles.

---

#### Segunda pregunta: ¿por qué `$()` y no simplemente `()`?

```bash
echo "Total directories in PATH: $(echo "$PATH" | tr ':' '\n' | wc -l)"
```

La confusión es natural: si `$VARIABLE` accede a una variable, ¿qué hace `$()`?

**`()` sin el `$` — crea un subshell**

```bash
(echo "hola")
```

Esto ejecuta `echo "hola"` en un **subshell** — un proceso hijo aislado. La salida aparece en pantalla (porque el subshell hereda el stdout), pero el resultado no se puede insertar en otro comando. Es útil para agrupar comandos o aislar cambios de directorio, pero no para capturar la salida.

**`$()` con el `$` — sustitución de comando**

```bash
echo "Hoy es $(date)"
```
```
Hoy es Thu Apr 16 11:00:35 CST 2026
```

El `$` delante de `()` le dice al shell: "ejecuta esto y **sustituye** `$()` por el resultado". El shell ejecuta el comando adentro, captura su stdout, y pone ese texto en el lugar donde estaba `$()`.

**Visualización de cómo el shell procesa la línea:**

```
ANTES de ejecutar:
echo "Total directories in PATH: $(echo "$PATH" | tr ':' '\n' | wc -l)"
                                   ↑ el shell ve esto

PASO 1 — ejecuta lo que está dentro de $():
echo "$PATH" | tr ':' '\n' | wc -l
→ produce el número 14 (o el que sea)

PASO 2 — sustituye $() por ese resultado:
echo "Total directories in PATH: 14"

PASO 3 — ejecuta el echo con la línea ya completa:
Total directories in PATH: 14
```

Sin el `$`, el shell no sabría que tiene que capturar y sustituir — solo vería paréntesis que agrupan comandos.

**La diferencia en la práctica:**

```bash
# Con $() — captura el resultado y lo inserta
echo "Son $(wc -l < /etc/passwd) usuarios"
# → Son 35 usuarios

# Sin $() — ejecuta el subshell pero no inserta nada
echo "Son (wc -l < /etc/passwd) usuarios"
# → Son (wc -l < /etc/passwd) usuarios   ← texto literal
```

---

#### Desglose del pipeline clave: `echo "$PATH" | tr ':' '\n'`

El PATH tiene este formato:
```
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin:/home/labex/.local/bin
```

Todo en una línea, separado por `:`. `tr ':' '\n'` transforma cada `:` en un salto de línea real (`\n`):

```
/usr/local/sbin
/usr/local/bin
/usr/sbin
/usr/bin
/sbin
/bin
/home/labex/.local/bin
```

Cada directorio queda en su propia línea — exactamente lo que querías mostrar.

**¿Por qué `\n` y no literalmente una nueva línea?**

`tr` acepta secuencias de escape como `\n` (nueva línea), `\t` (tabulación), `\\` (backslash literal). No puedes poner un salto de línea real dentro de las comillas de `tr` — las secuencias de escape son la forma de referirse a esos caracteres invisibles.

---

#### Desglose de la línea del contador

```bash
echo "Total directories in PATH: $(echo "$PATH" | tr ':' '\n' | wc -l)"
```

Paso a paso dentro del `$()`:

```
echo "$PATH"           → imprime el PATH como cadena: /usr/bin:/bin:/usr/local/bin:...
      |
tr ':' '\n'            → convierte cada ':' en salto de línea
                         resultado: una línea por directorio
      |
wc -l                  → cuenta cuántas líneas hay
                         resultado: el número (ejemplo: 14)
```

Ese número `14` reemplaza al `$()` en el `echo` exterior, produciendo:
```
Total directories in PATH: 14
```

---

#### Por qué `echo` sin argumento produce una línea vacía

```bash
echo
echo "Directories in PATH:"
```

`echo` sin argumentos imprime exactamente una línea vacía. Es la forma idiomática de añadir una línea en blanco para separar secciones de la salida de un script — más claro que `echo ""` o `printf '\n'`.

---

#### Flujo completo del script

```
1. echo "Full PATH:"
   echo "$PATH"
   → Muestra el PATH completo en una sola línea

2. echo
   echo "Directories in PATH:"
   echo "$PATH" | tr ':' '\n'
   → Convierte ':' en saltos de línea y muestra un directorio por línea

3. echo
   echo "Total directories in PATH: $(echo "$PATH" | tr ':' '\n' | wc -l)"
   → El $() captura la cuenta y la inserta en el mensaje
```

---

#### Errores frecuentes — Lab 16

**Usar comillas simples alrededor de `$PATH`**

```bash
echo '$PATH'    # imprime literalmente: $PATH
echo "$PATH"    # imprime el valor real del PATH
```

Las comillas simples bloquean toda expansión de variables. Si el script imprime `$PATH` como texto en vez del valor, es este error.

**Olvidar el `$` antes de `()`**

```bash
echo "Total: (echo $PATH | tr ':' '\n' | wc -l)"
# Imprime: Total: (echo /usr/bin:... | tr ':' '\n' | wc -l)
# El shell no ejecutó nada — imprimió todo como texto
```

Sin el `$`, el shell no reconoce `()` como sustitución de comando.

**`tr ':' '\n'` con comillas simples alrededor de `\n`**

```bash
echo $PATH | tr ':' '\n'    # correcto — \n se interpreta como nueva línea
echo $PATH | tr ':' '\''n'  # error tipográfico — intención incorrecta
```

Dentro de las comillas dobles o simples en `tr`, `\n` siempre se interpreta como salto de línea. No necesitas hacer nada especial.

**`wc -l` cuenta una línea de más si el PATH termina en `:`**

Si el PATH termina en `:` (ej: `/usr/bin:/bin:`), `tr` convierte ese `:` final en un `\n` extra, produciendo una línea vacía al final. `wc -l` la cuenta. En la práctica, los PATHs no terminan en `:`, pero es un edge case a conocer en scripts de producción.

---

#### Ejercicio — Lab 16

**Entorno:** KillerCoda (Ubuntu) o cualquier Linux con bash.

**Tareas:**

1. Crea el script `analizar_path.sh`:
```bash
#!/bin/bash
echo "Full PATH:"
echo "$PATH"
echo
echo "Directories in PATH:"
echo "$PATH" | tr ':' '\n'
echo
echo "Total directories in PATH: $(echo "$PATH" | tr ':' '\n' | wc -l)"
```

2. Dale permisos de ejecución: `chmod +x analizar_path.sh`
3. Ejecútalo: `./analizar_path.sh`
4. Agrega una sección extra al script que muestre solo los directorios que **existen realmente** usando `while read dir; do [ -d "$dir" ] && echo "$dir"; done`:
```bash
echo
echo "Directorios que existen:"
echo "$PATH" | tr ':' '\n' | while read dir; do
  [ -d "$dir" ] && echo "$dir"
done
```
5. Guarda el listado de directorios en un archivo: `echo "$PATH" | tr ':' '\n' > mis_directorios_path.txt`
6. Usa `wc -l mis_directorios_path.txt` para confirmar el conteo.

<details>
<summary>Ver solución completa</summary>

```bash
# Crear el script
cat << 'EOF' > analizar_path.sh
#!/bin/bash

echo "Full PATH:"
echo "$PATH"

echo
echo "Directories in PATH:"
echo "$PATH" | tr ':' '\n'

echo
echo "Total directories in PATH: $(echo "$PATH" | tr ':' '\n' | wc -l)"

echo
echo "Directorios que existen:"
echo "$PATH" | tr ':' '\n' | while read dir; do
  [ -d "$dir" ] && echo "$dir"
done
EOF

# Dar permisos y ejecutar
chmod +x analizar_path.sh
./analizar_path.sh

# Guardar el listado
echo "$PATH" | tr ':' '\n' > mis_directorios_path.txt
wc -l mis_directorios_path.txt
```

</details>

---

## Referencia Rápida

| Comando | Descripción breve | Lab |
|---------|------------------|-----|
| `echo "texto"` | Imprime texto en la terminal | 01 |
| `echo $VARIABLE` | Muestra el valor de una variable | 01 |
| `date` | Fecha y hora completa del sistema | 01 |
| `date +"%Y-%m-%d"` | Fecha en formato personalizado | 01 |
| `cal` | Calendario del mes actual | 01 |
| `cal AÑO` | Calendario completo del año indicado | 01 |
| `cal MES AÑO` | Calendario de un mes específico | 01 |
| `expr N op N` | Calcula una operación aritmética | 01 |
| `figlet "texto"` | Convierte texto en arte ASCII | 01 |
| `figlet -f fuente "texto"` | Arte ASCII con tipografía específica | 01 |
| `clear` | Limpia la pantalla de la terminal | 01 |
| `pwd` | Muestra el directorio de trabajo actual | 02 |
| `cd ruta` | Cambia al directorio indicado | 02 |
| `cd ~` | Va al home del usuario | 02 |
| `cd ..` | Sube un nivel al directorio padre | 02 |
| `cd -` | Vuelve al directorio anterior | 02 |
| `ls` | Lista archivos del directorio actual | 02 |
| `ls -lh` | Lista con permisos y tamaños legibles | 02 |
| `ls *.ext` | Lista solo los archivos que coinciden con el patrón | 02 |
| `ls ruta` | Lista el contenido de otra ruta sin moverse | 02 |
| `mkdir nombre` | Crea un directorio | 02 |
| `mkdir -p ruta/anidada` | Crea toda la estructura de directorios | 02 |
| `touch archivo.txt` | Crea un archivo vacío | 02 |
| `touch a_{1..5}.txt` | Crea 5 archivos con expansión de llaves | 02 |
| `cp origen destino` | Copia un archivo | 02 |
| `cp -r dir/ destino/` | Copia un directorio completo | 02 |
| `mv origen destino` | Mueve o renombra un archivo | 02 |
| `rm archivo` | Elimina un archivo permanentemente | 02 |
| `rm -r directorio/` | Elimina un directorio y todo su contenido | 02 |
| `comando --help` | Muestra la ayuda rápida del comando | 02 |
| `man comando` | Abre el manual completo del comando | 02 |
| `type comando` | Revela si el comando es built-in, externo o alias | 03 |
| `type -a comando` | Muestra todas las ubicaciones del comando | 03 |
| `comando --help \| grep "flag"` | Filtra la ayuda para encontrar una opción específica | 03 |
| `man N comando` | Abre una sección específica del manual | 03 |
| `man 5 passwd` | Manual del formato del archivo /etc/passwd (sección 5) | 03 |
| `man -k palabra` | Busca páginas de manual por palabra clave | 03 |
| `apropos palabra` | Busca comandos por lo que hacen (igual que man -k) | 03 |
| `sudo mandb` | Reconstruye la base de datos del sistema de man | 03 |
| `whoami` | Muestra el usuario actual con el que estás operando | 05 |
| `id usuario` | Muestra UID, GID y todos los grupos del usuario | 05 |
| `sudo adduser nombre` | Crea un usuario de forma interactiva con home y contraseña | 05 |
| `cat /etc/group` | Muestra todos los grupos del sistema | 05 |
| `cat /etc/group \| grep usuario` | Filtra los grupos en los que aparece un usuario | 05 |
| `sudo groupadd grupo` | Crea un nuevo grupo en el sistema | 05 |
| `sudo usermod -aG grupo usuario` | Agrega un usuario a un grupo sin quitar los anteriores | 05 |
| `groups usuario` | Lista los grupos a los que pertenece un usuario | 05 |
| `sudo chown usuario:grupo archivo` | Cambia el dueño y grupo de un archivo | 05 |
| `sudo chmod 750 archivo` | Establece permisos en notación numérica | 05 |
| `ls -l` | Lista archivos con permisos, dueño, grupo y tamaño | 05 |
| `sudo groupadd grupo` | Crea un grupo (debe existir antes de usarlo en useradd) | 06 |
| `sudo useradd -m -d /home/u -g GP -G GS usuario` | Crea usuario con home, grupo primario y secundarios | 06 |
| `sudo useradd -s /bin/bash usuario` | Crea usuario especificando el shell por defecto | 06 |
| `sudo useradd -c "Nombre" usuario` | Crea usuario con nombre completo en el comentario | 06 |
| `sudo passwd usuario` | Asigna o cambia la contraseña de un usuario | 06 |
| `ls -l /` | Lista el contenido de la raíz con permisos y tipos | 07 |
| `tree ruta/` | Muestra la estructura de directorios en forma de árbol | 07 |
| `tree -L N ruta/` | Árbol limitado a N niveles de profundidad | 07 |
| `cat << EOF > archivo` | Crea un archivo multilínea con here-document | 07 |
| `nl archivo` | Muestra el archivo con números de línea | 07 |
| `head -n N archivo` | Muestra las primeras N líneas del archivo | 07 |
| `tail -n N archivo` | Muestra las últimas N líneas del archivo | 07 |
| `nano archivo` | Abre el editor de texto interactivo nano | 07 |
| `find ruta -name "*.ext"` | Busca archivos por nombre o patrón | 07 |
| `find ruta -type d` | Busca solo directorios | 07 |
| `find ruta -size +1M` | Busca archivos mayores a 1 MB | 07 |
| `find ruta -mtime -1` | Busca archivos modificados en las últimas 24 horas | 07 |
| `sudo find / -name "f" 2>/dev/null` | Busca en todo el sistema suprimiendo errores de permisos | 07 |
| `which comando` | Muestra la ruta completa del ejecutable que se usaría | 07 |
| `VAR="valor"` | Crea una variable de shell (solo sesión, no heredada) | 08 |
| `echo $VAR` | Muestra el valor de una variable | 08 |
| `env` | Lista todas las variables de entorno activas | 08 |
| `env \| grep PATRON` | Filtra variables de entorno por nombre | 08 |
| `export VAR="valor"` | Crea variable de entorno heredada por procesos hijos | 08 |
| `export PATH="$PATH:/nueva/ruta"` | Agrega un directorio al PATH sin sobreescribirlo | 08 |
| `echo $PATH` | Muestra los directorios donde el shell busca ejecutables | 08 |
| `source ~/.zshrc` | Aplica cambios del archivo de config sin reiniciar la terminal | 08 |
| `unset VAR` | Elimina una variable del entorno de la sesión actual | 08 |
| `echo $HOME` | Muestra el directorio home del usuario actual | 08 |
| `echo $USER` | Muestra el nombre del usuario actual | 08 |
| `echo $SHELL` | Muestra el shell que se está usando | 08 |
| `tar -cvf arch.tar dir/` | Empaquetar un directorio (sin compresión) | 10 |
| `tar -tvf arch.tar` | Listar contenido del tar sin extraer | 10 |
| `tar -xvf arch.tar -C destino/` | Extraer tar en un directorio específico | 10 |
| `tar -czvf arch.tar.gz dir/` | Empaquetar y comprimir con gzip en un paso | 10 |
| `tar -tzvf arch.tar.gz` | Listar contenido de un tar.gz | 10 |
| `tar -xzvf arch.tar.gz -C destino/` | Extraer un tar.gz en un directorio | 10 |
| `gzip archivo` | Comprimir un archivo (reemplaza el original con .gz) | 10 |
| `gunzip archivo.gz` | Descomprimir un archivo .gz | 10 |
| `zip -r arch.zip directorio/` | Crear archivo zip recursivo (multiplataforma) | 10 |
| `unzip -d destino/ arch.zip` | Extraer zip en un directorio específico | 10 |
| `du -sh directorio/` | Muestra el espacio en disco del directorio | 10 |
| `df -h` | Muestra el uso de disco de todos los filesystems montados | 12 |
| `df -h /ruta` | Muestra el filesystem donde vive esa ruta específica | 12 |
| `df -T` | Muestra el tipo de filesystem (ext4, tmpfs, overlay...) | 12 |
| `df -i` | Muestra el uso de inodes (útil cuando hay "no space" con espacio libre) | 12 |
| `du -h --max-depth=1 ~` | Tamaños de directorios de primer nivel incluyendo ocultos | 12 |
| `du -h dir \| sort -rh \| head -n 10` | Los 10 directorios más grandes ordenados de mayor a menor | 12 |
| `dd if=/dev/zero of=archivo.img bs=1M count=N` | Crea un archivo de N megabytes lleno de ceros | 12 |
| `sudo mkfs.ext4 dispositivo` | Formatea un disco o archivo con el sistema de archivos ext4 | 12 |
| `sudo mkdir /mnt/punto` | Crea el directorio que servirá como punto de montaje | 12 |
| `sudo mount -o loop archivo.img /mnt/punto` | Monta un archivo de imagen como si fuera un disco físico | 12 |
| `sudo mount /dev/sdb1 /mnt/datos` | Monta una partición real en un punto de montaje | 12 |
| `mount \| grep patron` | Filtra la lista de filesystems montados | 12 |
| `sudo umount /mnt/punto` | Desmonta un filesystem vaciando los buffers antes de soltar | 12 |
| `sudo fdisk -l` | Lista todos los discos del sistema y sus tablas de particiones | 12 |
| `sudo fdisk -l archivo.img` | Muestra la información de un archivo de imagen de disco | 12 |
| `lsof /mnt/punto` | Lista los procesos que tienen archivos abiertos en ese punto de montaje | 12 |
| `cmd1 && cmd2` | Ejecuta cmd2 solo si cmd1 tiene éxito (código de salida 0) | 13 |
| `cmd1 \|\| cmd2` | Ejecuta cmd2 solo si cmd1 falla (código de salida ≠ 0) | 13 |
| `cmd1 \| cmd2` | Conecta la salida de cmd1 con la entrada de cmd2 | 13 |
| `echo $?` | Muestra el código de salida del último comando ejecutado | 13 |
| `cut -d: -f1 archivo` | Extrae el primer campo de un archivo con delimitador ':' | 13 |
| `cut -d: -f1,6 archivo` | Extrae los campos 1 y 6 separados por ':' | 13 |
| `cut -d, -f2 archivo` | Extrae el segundo campo de un CSV separado por comas | 13 |
| `grep "patron" archivo` | Filtra líneas que contienen el patrón | 13 |
| `grep '^d' archivo` | Filtra líneas que empiezan con 'd' | 13 |
| `grep -v "patron" archivo` | Filtra líneas que NO contienen el patrón | 13 |
| `grep -i "patron" archivo` | Búsqueda sin distinguir mayúsculas/minúsculas | 13 |
| `grep -E "p1\|p2" archivo` | Busca líneas que contienen p1 o p2 (OR) | 13 |
| `wc -l archivo` | Cuenta el número de líneas | 13 |
| `wc -w archivo` | Cuenta el número de palabras (separadas por espacios) | 13 |
| `wc -c archivo` | Cuenta el número de bytes | 13 |
| `sort archivo` | Ordena líneas alfabéticamente | 13 |
| `sort -n archivo` | Ordena numéricamente | 13 |
| `sort -r archivo` | Ordena en orden inverso | 13 |
| `sort -t: -k3 -n archivo` | Ordena por el campo 3 (delimitado por ':') numéricamente | 13 |
| `sort \| uniq` | Elimina líneas duplicadas (sort primero es obligatorio) | 13 |
| `sort \| uniq -c` | Cuenta cuántas veces aparece cada línea | 13 |
| `sort \| uniq -d` | Muestra solo las líneas que tienen al menos un duplicado | 13 |
| `sort \| uniq -u` | Muestra solo las líneas completamente únicas | 13 |
| `sort -k1,1` | Ordena usando solo el campo 1 como clave (inicio,fin del campo) | 14 |
| `sort -k2,2n` | Ordena numéricamente por el campo 2 exactamente | 14 |
| `grep "patron" archivo \| sort -k1,1 \| uniq > resultado` | Pipeline completo: filtrar → ordenar → deduplicar → guardar | 14 |
| `echo "texto" \| tr 'ab' 'AB'` | Reemplaza 'a'→'A' y 'b'→'B' (mapeo carácter por carácter) | 15 |
| `echo "texto" \| tr '[:lower:]' '[:upper:]'` | Convierte todo a mayúsculas usando clases de caracteres | 15 |
| `echo "texto" \| tr -d 'aeiou'` | Elimina todos los caracteres del conjunto indicado | 15 |
| `echo "texto" \| tr -d '\r'` | Elimina retornos de carro Windows de un archivo | 15 |
| `echo "texto" \| tr -s ' '` | Comprime múltiples espacios consecutivos a uno solo | 15 |
| `cat -A archivo` | Muestra todos los caracteres incluyendo ocultos: tabs como ^I, fin de línea como $ | 15 |
| `cat archivo \| col -x` | Convierte tabulaciones a espacios equivalentes | 15 |
| `join archivo1 archivo2` | Une líneas de dos archivos por el campo 1 (como SQL JOIN) | 15 |
| `join -1 N -2 M archivo1 archivo2` | Une por el campo N del archivo1 y campo M del archivo2 | 15 |
| `join -a 1 archivo1 archivo2` | Incluye también las líneas de archivo1 sin coincidencia | 15 |
| `paste archivo1 archivo2` | Combina archivos columna a columna separados por Tab | 15 |
| `paste -d ',' archivo1 archivo2` | Combina columnas usando ',' como separador (genera CSV) | 15 |
| `paste -s archivo` | Serializa el archivo: todas sus líneas en una sola línea horizontal | 15 |
| `echo -e "línea1\nlínea2"` | Crea texto con saltos de línea reales (escape habilitado) | 15 |
| `<(comando)` | Sustitución de proceso: pasa la salida del comando como si fuera un archivo | 15 |

---

## Errores Humanos Frecuentes

Esta sección recopila los errores más comunes al usar Linux como principiante. No son errores de sintaxis — son patrones de confusión que aparecen una y otra vez.

---

### Navegación y archivos

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `rm archivo` creyendo que va a la papelera | El archivo se borra para siempre — Linux no tiene papelera en terminal | Verificar con `ls` antes; usar `rm -i` para que pida confirmación |
| `mv archivo/` con barra al final | Si el destino no existe como directorio, falla con error | `mv archivo destino` sin barra al final a menos que sea un directorio existente |
| `cp origen destino` sin `-r` para directorios | `cp` sin `-r` no copia directorios — da error silencioso | `cp -r directorio/ destino/` para copiar directorios |

---

### Permisos y usuarios

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `chmod 777` como solución rápida | Cualquier usuario del sistema puede leer, modificar y ejecutar el archivo | Usar el permiso mínimo necesario — `644` para archivos, `755` para directorios públicos |
| Olvidar `sudo` al instalar software | Falla con `Permission denied` | `sudo apt install paquete` |

---

### Tuberías y redirección

| Error | Consecuencia | Forma correcta |
|-------|-------------|----------------|
| `>` cuando se quería `>>` | Sobreescribe el archivo completo — se pierde el contenido anterior | `>>` para acumular, `>` solo cuando quieres empezar limpio |
| Olvidar `2>&1` al redirigir errores | Los mensajes de error siguen apareciendo en pantalla aunque redirijas stdout | `comando > archivo.log 2>&1` para capturar todo |

---

## Glosario

| Término | Definición |
|---------|-----------|
| **Terminal** | Interfaz de texto para dar comandos al sistema operativo |
| **Shell** | Intérprete que lee los comandos que escribes y los ejecuta — el más común es Bash |
| **Bash** | Bourne Again Shell — el shell por defecto en la mayoría de distribuciones Linux |
| **Comando** | Instrucción que le das al sistema — puede ser un programa (`ls`) o una función del shell (`cd`) |
| **Flag / Opción** | Modificador de un comando — cambia su comportamiento. Ej: `ls -l` (la `-l` es una flag) |
| **Argumento** | Dato que le pasas al comando para que trabaje con él. Ej: `rm archivo.txt` |
| **Ruta absoluta** | Ruta que empieza desde la raíz `/` — siempre funciona sin importar dónde estés |
| **Ruta relativa** | Ruta desde el directorio actual — depende de dónde estés en el sistema |
| **`~`** | Atajo para el directorio home del usuario actual (`/home/usuario`) |
| **`.`** | El directorio actual |
| **`..`** | El directorio padre (un nivel arriba) |
| **`/`** | La raíz del sistema de archivos — el punto de partida de toda ruta absoluta |
| **Pipe `\|`** | Operador que conecta comandos: la salida del primero se convierte en la entrada del segundo |
| **Stdin** | Entrada estándar — de dónde lee datos un programa (normalmente el teclado) |
| **Stdout** | Salida estándar — a dónde escribe resultados un programa (normalmente la pantalla) |
| **Stderr** | Salida de error — canal separado para mensajes de error |
| **Proceso** | Programa en ejecución — tiene un PID único |
| **Root** | Superusuario con acceso total al sistema |
| **`sudo`** | Ejecuta un comando con privilegios de root |
| **Permiso** | Control de acceso a archivos — lectura (r), escritura (w), ejecución (x) |
| **Distribución** | Versión empaquetada de Linux — Ubuntu, Debian, Fedora, etc. |
| **Kernel** | Núcleo del SO — gestiona hardware, memoria y procesos |
| **`/etc`** | Directorio de configuración del sistema |
| **`/var/log`** | Directorio donde se guardan los logs del sistema |
| **`/home`** | Directorio que contiene los homes de todos los usuarios |
| **`/tmp`** | Directorio para archivos temporales — se limpia al reiniciar |
| **`echo`** | Comando que imprime texto en la terminal — base de todos los mensajes en scripts |
| **`date`** | Muestra la fecha y hora del sistema — también genera cadenas formateadas para scripts |
| **`cal`** | Muestra un calendario en la terminal — con el día actual resaltado |
| **`expr`** | Evalúa expresiones aritméticas enteras directamente en la terminal |
| **`figlet`** | Genera arte ASCII a partir de texto — usado en banners de scripts y mensajes de bienvenida |
| **`clear`** | Limpia la pantalla de la terminal sin borrar el historial de comandos |
| **`Ctrl + L`** | Atajo de teclado equivalente a `clear` |
| **Prompt** | El símbolo `$` que indica que la terminal está lista para recibir un nuevo comando |
| **Arte ASCII** | Representación de texto o imágenes usando solo caracteres de texto |
| **Unix timestamp** | Número de segundos transcurridos desde el 1 de enero de 1970 — base del tiempo en sistemas Unix |
| **Epoch** | El momento de referencia del tiempo Unix: `1970-01-01 00:00:00 UTC` |
| **`/etc/motd`** | Message Of The Day — texto que se muestra al iniciar sesión en un servidor |
| **`pwd`** | Print Working Directory — muestra la ruta absoluta del directorio actual |
| **Directorio de trabajo** | El directorio desde donde se ejecutan tus comandos en este momento |
| **`cd`** | Change Directory — cambia el directorio de trabajo |
| **`ls`** | List — lista el contenido de un directorio |
| **`mkdir`** | Make Directory — crea uno o más directorios |
| **`touch`** | Crea un archivo vacío o actualiza la fecha de modificación de uno existente |
| **`cp`** | Copy — copia archivos o directorios |
| **`mv`** | Move — mueve o renombra archivos y directorios |
| **`rm`** | Remove — elimina archivos o directorios (sin papelera) |
| **Comodín (wildcard)** | Patrón que el shell expande antes de ejecutar el comando — `*`, `?`, `[]` |
| **`*`** | Comodín que representa cualquier cantidad de caracteres |
| **`?`** | Comodín que representa exactamente un carácter |
| **Expansión de llaves** | Sintaxis `{1..5}` o `{a,b,c}` que el shell expande en una lista antes de ejecutar |
| **`man`** | Manual — muestra la documentación completa de un comando |
| **`--help`** | Flag que muestra la ayuda rápida de un comando |
| **`/dev/null`** | Dispositivo especial que descarta todo lo que se escribe en él — siempre vacío |
| **`Ctrl+C`** | Atajo para interrumpir (cancelar) el proceso que se está ejecutando |
| **`tail -f`** | Sigue un archivo en tiempo real mostrando nuevas líneas conforme aparecen |
| **`type`** | Revela la naturaleza de un comando: built-in, externo o alias |
| **Built-in** | Comando integrado en el shell — no existe como archivo en el disco |
| **Comando externo** | Programa independiente en el disco — generalmente en `/usr/bin/` o `/bin/` |
| **Alias** | Nombre alternativo para un comando, usualmente definido en `~/.bashrc` |
| **`man`** | Manual de Linux — documentación técnica completa de comandos, archivos y llamadas al sistema |
| **`man pages`** | Las páginas del manual de Linux — escritas en formato específico para el comando `man` |
| **Sección de `man`** | Número del 1 al 9 que clasifica el tipo de documentación (1=comandos, 5=archivos, 8=admin) |
| **`apropos`** | Busca en los títulos y descripciones de todas las páginas man instaladas |
| **`mandb`** | Base de datos de páginas man — se reconstruye con `sudo mandb` |
| **SYNOPSIS en man** | Sección que muestra la sintaxis completa del comando con todos sus argumentos posibles |
| **SEE ALSO en man** | Sección que lista comandos relacionados — útil para descubrir herramientas similares |
| **UID** | User ID — número único que identifica a un usuario en el sistema |
| **GID** | Group ID — número único que identifica a un grupo en el sistema |
| **Grupo primario** | Grupo creado automáticamente con el mismo nombre del usuario — aparece en los archivos que crea |
| **Grupo secundario** | Grupo adicional al que se agrega un usuario para darle acceso a recursos compartidos |
| **`/etc/group`** | Archivo que almacena la definición de todos los grupos del sistema |
| **`/etc/skel`** | Directorio con los archivos base que se copian al home de cada usuario nuevo |
| **`adduser`** | Comando interactivo de Debian/Ubuntu para crear usuarios — más amigable que `useradd` |
| **`useradd`** | Comando universal (bajo nivel) para crear usuarios — ideal para scripts |
| **`groupadd`** | Crea un nuevo grupo en el sistema |
| **`usermod`** | Modifica la configuración de un usuario existente |
| **`-aG`** | Flags de usermod: Append + Groups — agrega grupos sin eliminar los existentes |
| **`chown`** | Change Owner — cambia el usuario y/o grupo dueño de un archivo |
| **`chmod`** | Change Mode — cambia los permisos de acceso de un archivo o directorio |
| **Permisos rwx** | r=leer(4), w=escribir(2), x=ejecutar(1) — se suman para formar el número de permisos |
| **Notación numérica** | Forma de expresar permisos con 3 dígitos: ej. `750` = `rwxr-x---` |
| **Dueño (owner)** | El usuario propietario del archivo — controla quién puede cambiarlo |
| **`sudo`** | Permite ejecutar comandos con privilegios de root — solo usuarios del grupo `sudo` pueden usarlo |
| **`useradd`** | Herramienta de bajo nivel para crear usuarios — universal en todas las distros, ideal para scripts |
| **`-m` en useradd** | Flag que crea el directorio home del usuario si no existe |
| **`-d` en useradd** | Flag que especifica la ruta exacta del directorio home |
| **`-g` (minúscula)** | Establece el grupo **primario** del usuario — uno solo, el que firman los archivos que crea |
| **`-G` (mayúscula)** | Establece los grupos **secundarios** — pueden ser varios, separados por coma |
| **`-s` en useradd** | Especifica el shell por defecto del usuario (ej. `/bin/bash`) |
| **Grupo primario** | El grupo que hereda cada archivo nuevo creado por el usuario |
| **Grupo secundario** | Grupos adicionales para dar acceso a recursos — no afecta la propiedad de archivos nuevos |
| **FHS** | Filesystem Hierarchy Standard — estándar que define la estructura de directorios de Linux |
| **Enlace simbólico** | Acceso directo a otro archivo o directorio — la `l` al inicio en `ls -l`, ej. `bin -> usr/bin` |
| **Sticky bit** | Permiso especial (`t` al final) en `/tmp` — cualquiera puede crear archivos pero no borrar los ajenos |
| **`/proc`** | Sistema de archivos virtual — no existe en disco, el kernel lo genera en tiempo real con info de procesos |
| **`/etc`** | Directorio de configuración del sistema — todo lo que configura cómo funciona Linux |
| **`/var/log`** | Donde viven los logs del sistema — nginx, syslog, auth, etc. |
| **`tree`** | Muestra la jerarquía de directorios en forma visual de árbol |
| **Here-document** | Sintaxis `<< EOF ... EOF` para escribir texto multilínea directamente en la terminal |
| **`EOF`** | End Of File — la palabra que cierra un here-document (puede ser cualquier palabra) |
| **`nl`** | Number Lines — muestra el contenido de un archivo con números de línea |
| **`find`** | Herramienta de búsqueda que recorre el sistema de archivos aplicando criterios |
| **`-name "*.txt"`** | Criterio de find: busca por nombre usando comodines |
| **`-mtime -N`** | Criterio de find: archivos modificados en los últimos N días |
| **`-size +NM`** | Criterio de find: archivos de más de N megabytes |
| **`which`** | Localiza el ejecutable que se invocaría al escribir un comando |
| **`nano`** | Editor de texto de terminal — muestra los atajos en la barra inferior |
| **`2>/dev/null`** | Redirige stderr (mensajes de error) a la papelera — limpia la salida |
| **Variable de shell** | Variable local al proceso de shell actual — no se hereda por procesos hijos |
| **Variable de entorno** | Variable marcada con `export` — se hereda automáticamente por todos los procesos hijos |
| **`export`** | Marca una variable para que sea heredada por procesos hijos |
| **`PATH`** | Variable de entorno con los directorios donde el shell busca ejecutables |
| **Proceso hijo** | Proceso lanzado por otro proceso (el padre) — hereda las variables de entorno del padre |
| **`source`** | Ejecuta un archivo en el contexto del shell actual — aplica cambios de configuración sin reiniciar |
| **`~/.bashrc`** | Archivo de configuración de Bash — se ejecuta al abrir cada terminal interactiva |
| **`~/.zshrc`** | Archivo de configuración de Zsh — equivalente al `.bashrc` para el shell Zsh |
| **`unset`** | Elimina una variable del entorno de la sesión actual |
| **`env`** | Muestra todas las variables de entorno del proceso actual |
| **`$HOME`** | Variable integrada con el directorio home del usuario |
| **`$USER`** | Variable integrada con el nombre del usuario actual |
| **`$SHELL`** | Variable integrada con la ruta del shell activo |
| **`$OLDPWD`** | Directorio anterior — es lo que usa `cd -` internamente |
| **`<< 'EOF'`** | Here-document con expansión desactivada — las variables no se expanden al escribir el archivo |
| **`<< EOF`** | Here-document normal — las variables se expanden mientras se escribe el archivo |
| **Empaquetar** | Unir múltiples archivos en uno solo sin reducir tamaño — lo hace `tar` |
| **Comprimir** | Reducir el tamaño de un archivo mediante algoritmos — lo hacen `gzip`, `bzip2`, `xz` |
| **`tar`** | Tape Archive — herramienta de empaquetado que conserva estructura, permisos y metadatos |
| **`.tar`** | Archivo empaquetado sin compresión — puede ser más grande que los originales |
| **`.tar.gz`** | Archivo empaquetado con `tar` y comprimido con `gzip` — el formato más común en Linux |
| **`.tar.bz2`** | Empaquetado con tar y comprimido con bzip2 — mejor compresión, más lento que gzip |
| **`.tar.xz`** | Empaquetado con tar y comprimido con xz — la mejor compresión, el más lento |
| **`gzip`** | GNU Zip — compresor de archivos individuales, muy usado en Linux |
| **`zip`** | Formato de compresión y empaquetado con mejor compatibilidad en Windows y macOS |
| **`-z` en tar** | Flag que activa la compresión gzip — equivale a hacer tar y gzip en un solo paso |
| **`-C` en tar** | Cambia al directorio indicado antes de operar — controla dónde se extraen los archivos |
| **Bloque de disco** | Unidad mínima de almacenamiento — un archivo pequeño puede ocupar 4KB aunque tenga solo 1 byte |
| **`du`** | Disk Usage — mide el espacio real que ocupa en disco un archivo o directorio |
| **`stored 0%`** | En zip: el archivo se guarda sin comprimir porque es demasiado pequeño para beneficiarse |
| **`deflated N%`** | En zip: el archivo se comprimió un N% respecto a su tamaño original |
| **`df`** | Disk Free — muestra el espacio usado y libre en cada filesystem montado |
| **`du`** | Disk Usage — mide cuánto espacio en disco ocupa un directorio y su contenido |
| **Filesystem** | La estructura que organiza los datos en un disco — define cómo se guardan y recuperan archivos |
| **ext2** | Second Extended Filesystem (1993) — el primer filesystem estable de Linux, sin journaling |
| **ext3** | Third Extended Filesystem (2001) — añade journaling a ext2, evita corrupción ante cortes de luz |
| **ext4** | Fourth Extended Filesystem (2008) — el estándar actual en Linux, soporta archivos hasta 16TB, usa extents |
| **Journaling** | Técnica de los filesystems modernos: escribe en una bitácora qué va a hacer antes de hacerlo, garantizando consistencia ante fallos |
| **Journal** | La bitácora interna del filesystem donde se registran las operaciones antes de ejecutarlas |
| **Extent** | Rango contiguo de bloques descrito con un solo registro — en ext4 reemplaza la lista bloque-a-bloque de ext3 |
| **Inode** | Ficha técnica de un archivo: guarda dueño, permisos, fechas y bloques del disco, pero NO el nombre |
| **Superbloque** | Estructura crítica del filesystem que contiene su estado global: tamaño, inodes libres, bloques libres |
| **`lost+found`** | Directorio especial en ext4 donde `fsck` deposita archivos rescatados cuyo nombre se perdió por corrupción |
| **`fsck`** | File System Check — herramienta de reparación de filesystems, equivalente al "chkdsk" de Windows |
| **Montaje** | El proceso de conectar un filesystem a un punto del árbol de directorios para hacerlo accesible |
| **Punto de montaje** | El directorio donde "aterriza" el contenido de un disco al montarlo |
| **`/mnt`** | Convención para montajes temporales — es el lugar habitual para montar discos manualmente |
| **`/media`** | Convención para dispositivos externos (USB, DVD) — muchos sistemas montan aquí automáticamente |
| **`/etc/fstab`** | Archivo de configuración que define qué filesystems se montan automáticamente al arrancar |
| **UUID** | Universally Unique Identifier — identificador único del filesystem, más confiable que el nombre del dispositivo |
| **`dd`** | Disk Dump — copia datos bloque a bloque entre dispositivos o archivos, sin ninguna capa de abstracción |
| **`/dev/zero`** | Dispositivo especial que produce ceros indefinidamente — usado para crear archivos de tamaño fijo |
| **Loop device** | Dispositivo virtual (`/dev/loop0`) que hace que un archivo se comporte como un disco físico |
| **`-o loop`** | Opción de `mount` que crea automáticamente un loop device para montar un archivo de imagen |
| **`mkfs.ext4`** | Make Filesystem — formatea un dispositivo o archivo con el sistema de archivos ext4 |
| **Partición** | División lógica de un disco físico — cada partición tiene su propio filesystem y se monta independientemente |
| **Tabla de particiones** | Estructura al inicio del disco que define cuántas particiones hay y sus posiciones |
| **`fdisk`** | Herramienta para ver y modificar tablas de particiones en discos de estilo MBR |
| **MBR** | Master Boot Record — esquema de particionado clásico, soporta hasta 4 particiones primarias y discos de hasta 2TB |
| **GPT** | GUID Partition Table — esquema moderno que reemplaza a MBR, soporta más particiones y discos mayores a 2TB |
| **`/dev/sda`** | Primer disco SATA/SAS del sistema — `b`, `c`... para discos adicionales |
| **`/dev/nvme0n1`** | Primer disco NVMe — los SSD modernos de alta velocidad conectados directamente a PCIe |
| **`/dev/vda`** | Disco virtual en máquinas virtuales (KVM, VirtualBox, cloud) |
| **Swap** | Partición o archivo usado como extensión de la RAM — el sistema mueve páginas de memoria aquí cuando la RAM se llena |
| **`lsof`** | List Open Files — lista todos los archivos que los procesos tienen abiertos actualmente |
| **Buffer de escritura** | Área en RAM donde el kernel acumula escrituras antes de enviarlas al disco — mejora rendimiento |
| **`sort -h`** | Flag de sort para ordenar correctamente valores con sufijos humanos (K, M, G) |
| **`sort -r`** | Flag de sort para ordenar en orden inverso (mayor a menor) |
| **`&&`** | Operador AND lógico — ejecuta el segundo comando solo si el primero tiene éxito (exit code 0) |
| **`\|\|`** | Operador OR lógico — ejecuta el segundo comando solo si el primero falla (exit code ≠ 0) |
| **`\|` (pipe)** | Tubería — conecta la salida estándar de un comando con la entrada estándar del siguiente |
| **Código de salida** | Número que devuelve cada programa al terminar — 0 = éxito, cualquier otro = algún tipo de error |
| **`$?`** | Variable especial que guarda el código de salida del último comando |
| **`cut`** | Extrae columnas específicas de texto estructurado usando un delimitador y número de campo |
| **`-d` en cut** | Define el delimitador (el carácter que separa campos) — por defecto es el tabulador |
| **`-f` en cut** | Especifica qué campos extraer (1-indexed) — puede ser uno (`-f1`), varios (`-f1,3`) o un rango (`-f2-5`) |
| **`grep`** | Global Regular Expression Print — filtra líneas que coinciden con un patrón |
| **`^` en grep** | Ancla de inicio — el patrón debe estar al comienzo de la línea |
| **`$` en grep** | Ancla de fin — el patrón debe estar al final de la línea |
| **`wc`** | Word Count — cuenta líneas (`-l`), palabras (`-w`) o bytes (`-c`) de texto |
| **`sort`** | Ordena líneas de texto — alfabético por defecto, numérico con `-n`, por campo con `-k` |
| **`-k` en sort** | Especifica el campo por el cual ordenar (equivalente a `-f` en cut) |
| **`uniq`** | Elimina o cuenta líneas consecutivas duplicadas — requiere `sort` previo para funcionar correctamente |
| **`uniq -c`** | Agrega un contador al inicio de cada línea indicando cuántas veces aparece |
| **`/etc/passwd`** | Archivo que contiene la definición de todos los usuarios del sistema — 7 campos separados por `:` |
| **`/etc/shadow`** | Archivo que contiene las contraseñas encriptadas — solo root puede leerlo |
| **`/usr/sbin/nologin`** | Shell especial que rechaza el inicio de sesión — usado en cuentas de servicio del sistema |
| **Expresión regular** | Patrón de texto con sintaxis especial para describir conjuntos de cadenas — base de `grep`, `sed`, `awk` |
| **Pipeline** | Cadena de comandos conectados por tuberías donde cada uno procesa la salida del anterior |
| **`cowsay`** | Herramienta de entretenimiento que muestra texto con una vaca ASCII — útil para demos y banners en scripts |
| **`tr`** | Translate — transforma texto carácter por carácter: reemplaza, elimina o comprime caracteres |
| **`tr SET1 SET2`** | Mapea cada carácter de SET1 al carácter en la misma posición de SET2 |
| **`tr -d`** | Delete — elimina todos los caracteres del conjunto dado sin reemplazarlos |
| **`tr -s`** | Squeeze — comprime secuencias consecutivas del mismo carácter a uno solo |
| **`[:lower:]`** | Clase de caracteres de tr: representa todas las letras minúsculas (a-z) |
| **`[:upper:]`** | Clase de caracteres de tr: representa todas las letras mayúsculas (A-Z) |
| **`[:digit:]`** | Clase de caracteres de tr: representa todos los dígitos del 0 al 9 |
| **`[:space:]`** | Clase de caracteres de tr: espacios, tabs, y saltos de línea |
| **`cat -A`** | Muestra todos los caracteres incluyendo ocultos — `^I` para tabs, `$` para fin de línea, `^M` para `\r` de Windows |
| **`^I` en cat -A** | Representación visual de una tabulación (`\t`) |
| **`^M` en cat -A** | Representación visual del retorno de carro (`\r`) — señal de que el archivo tiene formato Windows |
| **`col -x`** | Convierte tabulaciones a los espacios equivalentes para alinear columnas |
| **`join`** | Une líneas de dos archivos cuando comparten el mismo valor en un campo — equivale al INNER JOIN de SQL |
| **`-1 N` en join** | Usa el campo N del primer archivo como clave de unión |
| **`-2 M` en join** | Usa el campo M del segundo archivo como clave de unión |
| **`-a` en join** | También incluye las líneas sin coincidencia (como LEFT JOIN en SQL) |
| **`paste`** | Combina archivos horizontalmente: une la línea N de cada archivo en una sola línea |
| **`paste -d`** | Define el delimitador entre columnas (por defecto es Tab) |
| **`paste -s`** | Modo serial — serializa cada archivo: convierte sus líneas verticales en una línea horizontal |
| **`echo -e`** | Habilita la interpretación de secuencias de escape como `\n` (nueva línea) y `\t` (tab) |
| **`\n` en echo -e** | Inserta un salto de línea real en la salida |
| **`\t` en echo -e** | Inserta una tabulación real en la salida |
| **`\r`** | Retorno de carro — en Windows, las líneas terminan en `\r\n`; en Linux, solo en `\n` |
| **`<(comando)`** | Sustitución de proceso — ejecuta el comando y pasa su salida como si fuera un archivo temporal |
| **Sustitución de proceso** | Técnica del shell para usar la salida de un comando donde se espera un archivo (`<()`) |
| **`-k INICIO,FIN` en sort** | Define la clave de ordenamiento: compara desde el campo INICIO hasta el campo FIN — si INICIO=FIN, usa exactamente ese campo |
| **`-k1,1`** | Ordena usando solo el primer campo (campo 1 a campo 1) — el patrón más común para ordenar por un identificador |
| **`-k1`** | Ordena desde el campo 1 hasta el final de la línea — más amplio que `-k1,1`, puede dar orden inesperado |
| **Campo en sort** | Segmento de texto separado por espacios (por defecto) o por el delimitador de `-t` — numerado desde 1 |
| **`sort -t`** | Define el delimitador de campos para sort, igual que `-d` en cut — ej. `sort -t: -k3,3n` ordena `/etc/passwd` por UID |
| **Clave de ordenamiento** | El fragmento de cada línea que `sort` compara para decidir el orden — definido por `-k` |
| **Deduplicar** | Eliminar entradas duplicadas de un conjunto de datos — en Linux se hace con `sort | uniq` |
| **Duplicados consecutivos** | Líneas idénticas que están una seguida de la otra — lo único que `uniq` puede eliminar |
