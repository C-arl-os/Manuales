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
