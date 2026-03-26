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

## Referencia Rápida

| Comando | Descripción breve | Lab |
|---------|------------------|-----|
| `echo "texto"` | Imprime texto en pantalla | 01 |
| `whoami` | Muestra el usuario actual | 01 |
| `id` | Muestra uid, gid y grupos del usuario | 01 |
| `id -un` | Muestra solo el nombre del usuario | 01 |

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

---

_Última actualización: 2026-03-25_
