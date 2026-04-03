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
