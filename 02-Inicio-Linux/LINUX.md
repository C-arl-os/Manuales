# Manual de Linux — LabEx Labs

> Manual de referencia personal construido a partir de los laboratorios de LabEx.
> Cada sección cubre los comandos usados en un lab, con explicación y ejemplos.

---

## Tabla de Contenidos

- [Cómo usar este manual](#cómo-usar-este-manual)
- [Cómo leer la salida de un comando](#cómo-leer-la-salida-de-un-comando)
- [Cómo aprender Linux desde cualquier entorno](#cómo-aprender-linux-desde-cualquier-entorno)
- [Conceptos Fundamentales](#conceptos-fundamentales)
- [Labs](#labs)
  - [Lab 01 — Primeros pasos en la terminal](#lab-01--primeros-pasos-en-la-terminal)
  - [Lab 02 — Operaciones con archivos y directorios](#lab-02--operaciones-con-archivos-y-directorios)
- [Referencia Rápida](#referencia-rápida)
- [Glosario](#glosario)

---

## Cómo usar este manual

Este manual se construye de forma progresiva conforme avanzas en los labs de LabEx.
Cada lab tiene su propia sección con:

- **Contexto** — qué problema resuelve el lab
- **Comandos** — cada comando con sintaxis, explicación y ejemplo real
- **Notas** — errores comunes, tips, o comportamientos a recordar

---

## Cómo leer la salida de un comando

Cuando ejecutas un comando en Linux, puede pasar una de tres cosas:

### 1. El comando imprime algo (salida estándar)

```
$ whoami
labex
```

La línea con `$` es lo que **tú escribes**. La línea de abajo es lo que **Linux responde**.
Si no hay respuesta, el comando funcionó en silencio (eso también es válido).

### 2. El comando da un error (salida de error)

```
$ Echo hola
bash: Echo: command not found
```

Los errores en Linux son descriptivos. Léelos completos:
- `command not found` → el comando no existe o está mal escrito (mayúsculas/minúsculas importan)
- `Permission denied` → no tienes permisos para esa acción
- `No such file or directory` → la ruta o archivo no existe

### 3. El comando no responde (cursor parpadeando)

Puede significar que está esperando más entrada. Presiona `Ctrl + C` para cancelarlo.

### Anatomía de una salida compleja

Algunos comandos devuelven varias columnas. Ejemplo de `id`:

```
uid=1000(labex) gid=1000(labex) groups=1000(labex),4(adm),27(sudo)
```

Léelo en partes:
- `uid=1000(labex)` → ID numérico del usuario y su nombre
- `gid=1000(labex)` → ID del grupo principal
- `groups=...` → todos los grupos a los que pertenece (separados por coma)

> **Regla de oro:** si no entiendes una salida, busca los patrones `clave=valor` o `clave: valor`.
> Linux habla en pares.

---

## Cómo aprender Linux desde cualquier entorno

Linux está en todas partes. Puedes practicar en:

| Entorno | Cómo acceder |
|---------|-------------|
| **LabEx** | Laboratorios online con terminal lista para usar |
| **WSL (Windows)** | `wsl` en la terminal de Windows — Linux dentro de Windows |
| **macOS Terminal** | Ya es Unix, la mayoría de comandos son iguales |
| **VirtualBox / VMware** | Instala Ubuntu o Debian en una máquina virtual |
| **Replit / Codespaces** | Terminal en el navegador, sin instalar nada |
| **Raspberry Pi** | Hardware real con Linux (Raspberry Pi OS) |

### Estrategia para aprender bien

1. **Escribe los comandos tú mismo** — no copies y pegues al principio. El error muscular enseña.
2. **Lee los errores** — son mensajes, no sentencias. Cada error dice exactamente qué falló.
3. **Usa `--help`** — casi todo comando acepta `comando --help` para ver opciones.
4. **Usa `man`** — el manual integrado: `man whoami`, `man id`, etc. Sal con `q`.
5. **Experimenta** — cambia un flag, observa qué cambia en la salida.
6. **Repite sin notas** — después de un lab, cierra el manual y repite los comandos de memoria.

---

## Conceptos Fundamentales

### El sistema de archivos de Linux

Linux organiza todo en una jerarquía de directorios que parte desde la raíz `/`.

```
/
├── home/       → directorios de usuarios
├── etc/        → configuración del sistema
├── bin/        → comandos básicos del sistema
├── var/        → logs, datos variables
└── tmp/        → archivos temporales
```

### La terminal

La terminal (shell) es la interfaz donde escribes comandos.
El prompt típico luce así:

```
usuario@maquina:~/directorio$
```

- `~` representa tu directorio home (`/home/usuario`)
- `$` indica usuario normal (si fuera `#` sería root)

### Reglas básicas de Linux que no se olvidan

- **Linux distingue mayúsculas de minúsculas** — `echo`, `Echo` y `ECHO` son tres cosas distintas. Solo `echo` es un comando válido.
- **Los espacios importan** — `echo"hola"` es un error; `echo "hola"` es correcto. Siempre un espacio entre el comando y sus argumentos.
- **Las comillas definen el texto exacto** — `echo "Hola mundo"` le dice a echo que repita exactamente esa cadena, incluyendo el espacio interior.

---

## Labs

---

### Lab 01 — Primeros pasos en la terminal

**Objetivo del lab:** Abrir la terminal y usar los comandos más básicos de identidad del sistema.

---

#### `echo` — Imprimir texto en pantalla

**Sintaxis:**
```
echo "texto"
```

**Qué hace:** Repite (imprime) exactamente el texto que le das.

**Ejemplos:**
```bash
$ echo "Hola mundo"
Hola mundo

$ echo "Mi nombre es labex"
Mi nombre es labex
```

**Errores comunes:**
```bash
$ Echo "hola"
bash: Echo: command not found   # ← mayúscula incorrecta

$ echo"hola"
bash: echohola: command not found  # ← falta el espacio
```

> **Regla:** `echo` siempre en minúsculas, siempre con espacio antes de las comillas.

---

#### `whoami` — Saber qué usuario eres

**Sintaxis:**
```
whoami
```

**Qué hace:** Imprime el nombre del usuario activo en la sesión actual.

**Ejemplo:**
```bash
$ whoami
labex
```

**Cuándo usarlo:** Cuando no recuerdas con qué usuario entraste, o quieres confirmar que cambiaste de usuario con `su`.

---

#### `id` — Ver identidad completa del usuario

**Sintaxis:**
```
id
id [opciones]
```

**Qué hace:** Muestra el ID numérico del usuario (`uid`), su grupo principal (`gid`) y todos sus grupos (`groups`).

**Ejemplo:**
```bash
$ id
uid=1000(labex) gid=1000(labex) groups=1000(labex),4(adm),27(sudo)
```

**Cómo leer la salida:**
- `uid=1000(labex)` → el usuario se llama `labex` y tiene el número 1000
- `gid=1000(labex)` → su grupo principal también es `labex`
- `groups=1000(labex),4(adm),27(sudo)` → pertenece además a los grupos `adm` y `sudo`

> El grupo `sudo` significa que este usuario **puede ejecutar comandos como administrador**.

---

#### `id -un` — Extraer solo el nombre de usuario

**Sintaxis:**
```
id -un
```

**Qué hace:** En lugar de mostrar toda la información de `id`, extrae únicamente el nombre del usuario actual.

**Ejemplo:**
```bash
$ id -un
labex
```

**Desglose de las opciones:**
- `-u` → muestra solo el `uid` (user ID)
- `-n` → en lugar del número, muestra el **nombre** correspondiente
- Juntos (`-un`) → nombre del usuario, sin números

**Comparación:**
```bash
$ id -u        # muestra el número
1000

$ id -un       # muestra el nombre
labex
```

> **Tip:** Puedes combinar flags de una letra en Linux. `-un` es lo mismo que `-u -n`.

---

### Ejercicio — Lab 01

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux.

**Escenario:** Eres nuevo en un servidor Linux y quieres confirmar quién eres y qué permisos tienes.

**Tareas:**

1. Imprime el mensaje `"Hola, soy nuevo en Linux"` en la terminal.
2. Descubre cómo se llama el usuario con el que estás conectado.
3. Muestra tu información completa de identidad (uid, gid y grupos).
4. Extrae solo tu nombre de usuario usando `id` con las opciones correctas.
5. Intenta escribir `Echo "prueba"` (con mayúscula) y observa el error. Luego corrígelo.

**Resultado esperado (los valores serán distintos según tu entorno):**
```
Hola, soy nuevo en Linux
root
uid=0(root) gid=0(root) groups=0(root)
root
```

**Pista:** Si en el paso 4 obtienes un número en lugar de un nombre, revisa qué flags usaste.

<details>
<summary>Ver solución</summary>

```bash
echo "Hola, soy nuevo en Linux"
whoami
id
id -un
```

</details>

---

---

### Lab 02 — Operaciones con archivos y directorios

**Objetivo del lab:** Navegar el sistema de archivos, crear, copiar, mover y eliminar archivos y directorios.

---

#### `pwd` — Saber en qué directorio estás

**Sintaxis:**
```
pwd
```

**Qué hace:** Imprime la ruta completa (absoluta) del directorio donde te encuentras ahora.

**Ejemplo:**
```bash
$ pwd
/home/labex/project
```

> Úsalo siempre que te pierdas. Es tu "¿dónde estoy?" de Linux.

---

#### `cd` — Cambiar de directorio

**Sintaxis:**
```
cd ruta
```

**Qué hace:** Te mueve a otro directorio. Acepta rutas relativas y absolutas.

**Formas de usarlo:**

```bash
$ cd project          # ruta relativa: entra a 'project' desde donde estás
$ cd ..               # sube un nivel (va al directorio padre)
$ cd ~                # va directo a tu home (/home/labex)
$ cd /home/labex/project   # ruta absoluta: va exactamente ahí, sin importar dónde estés
```

**Diferencia entre ruta relativa y absoluta:**
```bash
# Si estás en /home/labex:
$ cd project          # relativa: funciona porque 'project' existe aquí
$ cd /home/labex/project   # absoluta: siempre funciona desde cualquier lugar
```

> **`~`** es un atajo que Linux reemplaza automáticamente por `/home/tu_usuario`.
> `echo ~` lo comprueba: imprime la ruta completa de tu home.

```bash
$ echo ~
/home/labex
```

---

#### `ls` — Listar el contenido de un directorio

**Sintaxis:**
```
ls [opciones] [directorio]
```

**Qué hace:** Muestra los archivos y carpetas de un directorio.

**Sin opciones:**
```bash
$ ls
file1.txt  file2.txt  testdir
```

Solo muestra archivos visibles, sin detalles.

---

#### `ls -l` — Listado largo (con detalles)

```bash
$ ls -l
total 4
-rw-rw-r-- 1 labex labex  0 Mar 27 09:56 file1.txt
-rw-rw-r-- 1 labex labex 13 Mar 27 09:56 file2.txt
drwxrwxr-x 2 labex labex  6 Mar 27 09:57 testdir
```

**Cómo leer cada columna:**

```
-rw-rw-r--   1   labex   labex   13   Mar 27 09:56   file2.txt
│             │   │       │       │    │              │
│             │   │       │       │    │              └─ nombre del archivo
│             │   │       │       │    └─ fecha y hora de modificación
│             │   │       │       └─ tamaño en bytes
│             │   │       └─ grupo propietario
│             │   └─ usuario propietario
│             └─ número de enlaces duros
└─ tipo y permisos
```

**Desglose de permisos (`-rw-rw-r--`):**

```
-  rw-  rw-  r--
│   │    │    │
│   │    │    └─ otros usuarios: solo lectura (r)
│   │    └─ grupo: lectura y escritura (rw)
│   └─ propietario: lectura y escritura (rw)
└─ tipo: - = archivo, d = directorio
```

| Letra | Significado |
|-------|-------------|
| `r` | read — puede leer |
| `w` | write — puede escribir/modificar |
| `x` | execute — puede ejecutar (o entrar si es directorio) |
| `-` | sin ese permiso |

---

#### `ls -a` — Mostrar archivos ocultos

```bash
$ ls -a
.  ..  file1.txt  file2.txt  .hiddenfile  testdir
```

Los archivos que empiezan con `.` son **ocultos**. `ls` normal no los muestra.

- `.` → el directorio actual
- `..` → el directorio padre (un nivel arriba)
- `.hiddenfile` → archivo oculto real

---

#### `ls -la` — Detallado + ocultos (la combinación más usada)

```bash
$ ls -la
total 8
drwxr-xr-x 1 labex labex  74 Mar 27 09:57 .
drwxr-x--- 1 labex labex 248 Mar 27 09:58 ..
-rw-rw-r-- 1 labex labex   0 Mar 27 09:56 file1.txt
-rw-rw-r-- 1 labex labex  13 Mar 27 09:56 file2.txt
-rw-rw-r-- 1 labex labex  12 Mar 27 09:57 .hiddenfile
drwxrwxr-x 2 labex labex   6 Mar 27 09:57 testdir
```

> `-la` y `-al` son equivalentes. El orden de los flags no importa.

---

#### `ls -R` — Listar recursivamente

```bash
$ ls -R temp_dir
temp_dir:
temp_file.txt
```

Muestra el contenido de un directorio **y todos sus subdirectorios**. Útil para ver la estructura completa de una carpeta.

---

#### `touch` — Crear un archivo vacío

**Sintaxis:**
```
touch nombre_archivo
```

**Qué hace:** Crea un archivo vacío si no existe. Si ya existe, actualiza su fecha de modificación.

```bash
$ touch file1.txt
$ ls -l file1.txt
-rw-rw-r-- 1 labex labex 0 Mar 27 09:56 file1.txt
```

El tamaño `0` confirma que está vacío.

También puedes crear archivos dentro de otro directorio directamente:

```bash
$ touch temp_dir/temp_file.txt
```

---

#### `mkdir` — Crear un directorio

**Sintaxis:**
```
mkdir nombre_directorio
```

```bash
$ mkdir testdir
$ ls
file1.txt  file2.txt  testdir
```

---

#### `echo "texto" > archivo` — Crear archivo con contenido

**Sintaxis:**
```
echo "contenido" > nombre_archivo
```

**Qué hace:** El operador `>` redirige la salida de `echo` hacia un archivo, creándolo con ese contenido.

```bash
$ echo "Hello, linux" > file2.txt
$ echo "Hidden file" > .hiddenfile
```

> **Importante:** `>` **sobreescribe** el archivo si ya existe. Si quieres añadir sin borrar lo anterior, usa `>>`.

---

#### `cp` — Copiar archivos

**Sintaxis:**
```
cp origen destino
cp -r origen destino    # para directorios
```

**Copiar un archivo:**
```bash
$ cp file1.txt file1_copy.txt     # copia en el mismo directorio con otro nombre
$ cp file2.txt testdir/           # copia dentro de testdir (conserva el nombre)
```

**Copiar un directorio completo (requiere `-r`):**
```bash
$ cp -r testdir testdir_copy
```

La `-r` significa **recursivo**: copia el directorio y todo lo que contiene.

```bash
$ ls testdir
file2.txt
$ ls testdir_copy
file2.txt                         # el contenido también se copió
```

---

#### `mv` — Mover o renombrar

**Sintaxis:**
```
mv origen destino
```

**Qué hace dos cosas distintas según el destino:**

**1. Renombrar** (destino es un nombre nuevo en el mismo lugar):
```bash
$ mv file1.txt newname.txt        # file1.txt ya no existe, ahora es newname.txt
```

**2. Mover** (destino es un directorio existente):
```bash
$ mv newname.txt testdir/         # mueve el archivo dentro de testdir/
```

**3. Mover y renombrar al mismo tiempo:**
```bash
$ mv testdir/newname.txt ./original_file1.txt   # lo saca de testdir y le cambia el nombre
```

**4. Renombrar un directorio:**
```bash
$ mv testdir_copy new_testdir
```

**Errores que cometiste (y qué significan):**
```bash
$ mv rename.txt testdir/
mv: cannot stat 'rename.txt': No such file or directory
# ← el archivo origen no existe. Revisa el nombre.

$ mv newname.txt tetsdir/
mv: cannot move 'newname.txt' to 'tetsdir/': Not a directory
# ← 'tetsdir/' no existe (era un typo). mv no crea el destino automáticamente.
```

---

#### `rm` — Eliminar archivos

**Sintaxis:**
```
rm archivo
rm -i archivo     # con confirmación
rm -r directorio  # directorio y contenido
rm -rf directorio # forzado, sin preguntas
```

**Borrar un archivo normal:**
```bash
$ rm original_file1.txt
```

No hay papelera. El archivo desaparece permanentemente.

**Borrar con confirmación (`-i`):**
```bash
$ rm -i file2.txt
rm: remove regular file 'file2.txt'? y
```

Pregunta antes de borrar. Responde `y` para confirmar o `n` para cancelar. Útil cuando no estás seguro.

**Borrar un archivo oculto:**
```bash
$ rm .hiddenfile
```

Igual que cualquier archivo, solo que el nombre empieza con `.`.

**Error por typo:**
```bash
$ rm ,hiddenfile
rm: cannot remove ',hiddenfile': No such file or directory
# ← coma en lugar de punto. Los detalles importan.
```

**Borrar directorio y contenido (`-r`):**
```bash
$ rm -r testdir
```

Borra el directorio y **todo lo que tenga dentro**, de forma recursiva.

**Borrar forzado sin confirmación (`-rf`):**
```bash
$ rm -rf temp_dir
```

`-r` (recursivo) + `-f` (force, sin preguntar). El comando más peligroso del día a día.

> **Advertencia:** `rm -rf` no tiene vuelta atrás. Úsalo con cuidado y verifica el nombre antes de ejecutarlo.

---

#### `rmdir` — Eliminar directorio vacío

**Sintaxis:**
```
rmdir directorio
```

**Qué hace:** Elimina un directorio **solo si está completamente vacío**.

```bash
$ rmdir new_testdir
rmdir: failed to remove 'new_testdir': Directory not empty
# ← falló porque tenía archivos dentro

$ rm -r testdir      # la solución: usa rm -r si tiene contenido
```

> Úsalo cuando quieras asegurarte de no borrar nada por accidente. Si falla, es porque hay algo dentro y te obliga a verificar primero.

---

### Ejercicio — Lab 02

> Practica en [KillerCoda](https://killercoda.com/playgrounds/scenario/ubuntu) o cualquier terminal Linux.

**Escenario:** Vas a organizar los archivos de un proyecto desde cero usando solo la terminal.

**Tareas:**

1. Confirma en qué directorio estás y ve a tu home si no estás ahí.
2. Crea un directorio llamado `mi_proyecto` y entra en él.
3. Crea dos archivos vacíos: `notas.txt` y `tareas.txt`.
4. Crea el archivo `readme.txt` con el contenido `"Mi primer proyecto en Linux"`.
5. Crea un subdirectorio llamado `backup`.
6. Copia `readme.txt` dentro de `backup/`.
7. Renombra `notas.txt` a `notas_v1.txt`.
8. Lista el directorio actual con todos los detalles y verifica que todo esté como esperas.
9. Lista el contenido de `backup/` para confirmar la copia.
10. Elimina `tareas.txt` pidiendo confirmación antes de borrarlo.
11. Elimina el directorio `backup` con todo su contenido.
12. Verifica el estado final con `ls -la`.

**Estructura esperada al final:**
```
./mi_proyecto/
├── notas_v1.txt
└── readme.txt
```

**Errores a propósito (intenta estos y lee el mensaje):**
- Intenta `rmdir mi_proyecto` desde afuera antes de limpiar — observa el error.
- Intenta `mv notas_v1.txt carpeta_que_no_existe/` — observa el error.

<details>
<summary>Ver solución</summary>

```bash
pwd
cd ~
mkdir mi_proyecto
cd mi_proyecto
touch notas.txt tareas.txt
echo "Mi primer proyecto en Linux" > readme.txt
mkdir backup
cp readme.txt backup/
mv notas.txt notas_v1.txt
ls -l
ls backup/
rm -i tareas.txt
rm -r backup
ls -la
```

</details>

---

## Referencia Rápida

| Comando | Descripción breve | Lab |
|---------|------------------|-----|
| `echo "texto"` | Imprime texto en pantalla | 01 |
| `whoami` | Muestra el usuario actual | 01 |
| `id` | Muestra uid, gid y grupos del usuario | 01 |
| `id -un` | Muestra solo el nombre del usuario | 01 |
| `pwd` | Muestra el directorio actual | 02 |
| `cd ruta` | Cambia de directorio | 02 |
| `cd ..` | Sube un nivel en el árbol | 02 |
| `cd ~` | Va al directorio home | 02 |
| `ls` | Lista archivos del directorio actual | 02 |
| `ls -l` | Lista con detalles (permisos, tamaño, fecha) | 02 |
| `ls -a` | Lista incluyendo archivos ocultos | 02 |
| `ls -la` | Lista detallada incluyendo ocultos | 02 |
| `ls -R dir` | Lista recursivamente un directorio | 02 |
| `touch archivo` | Crea un archivo vacío | 02 |
| `mkdir dir` | Crea un directorio | 02 |
| `echo "texto" > archivo` | Crea archivo con contenido | 02 |
| `cp origen destino` | Copia un archivo | 02 |
| `cp -r origen destino` | Copia un directorio completo | 02 |
| `mv origen destino` | Mueve o renombra archivo/directorio | 02 |
| `rm archivo` | Elimina un archivo | 02 |
| `rm -i archivo` | Elimina pidiendo confirmación | 02 |
| `rm -r dir` | Elimina directorio y su contenido | 02 |
| `rm -rf dir` | Elimina sin confirmación (peligroso) | 02 |
| `rmdir dir` | Elimina directorio solo si está vacío | 02 |

---

## Glosario

| Término | Definición |
|---------|-----------|
| **Shell** | Intérprete de comandos (bash, zsh, etc.) |
| **Directorio** | Equivalente a una carpeta en Linux |
| **Ruta absoluta** | Ruta completa desde `/` (ej. `/home/user/docs`) |
| **Ruta relativa** | Ruta desde el directorio actual (ej. `./docs`) |
| **Flag / Opción** | Modificador de un comando (ej. `-u` en `id -u`) |
| **Root** | Usuario administrador con todos los permisos (prompt `#`) |
| **Permiso** | Control de quién puede leer/escribir/ejecutar un archivo |
| **uid** | User ID — número único que identifica a un usuario |
| **gid** | Group ID — número único que identifica a un grupo |
| **stdout** | Salida estándar — donde el comando imprime su resultado |
| **stderr** | Salida de error — donde el comando imprime sus errores |
| **Archivo oculto** | Archivo cuyo nombre empieza con `.` — solo visible con `ls -a` |
| **Redirección (`>`)** | Operador que envía la salida de un comando a un archivo |
| **Recursivo (`-r`)** | Opción que aplica la operación a un directorio y todo su contenido |

---

_Última actualización: 2026-03-26_
