¡Bienvenido al manual de apuntes en Git! Esta plantilla te ayuda a capturar definiciones, flujos, comandos, errores y decisiones importantes mientras estudias.

# 📘 Manual personal de Git

## 📌 Información general
- **Uso ideal:** Sigue el flujo de la plantilla (conceptos → comandos → práctica) para que cada sesión tenga estructura.
- **Nivel actual:** Marca tu punto de partida antes de empezar; puedes usar una tabla rápida debajo si quieres comparar sesiones.
- **Cierre:** Antes de cerrar la sesión, revisa la bitácora para saber qué practicarás la próxima vez.

## 🧭 Índice
- [📘 Manual personal de Git](#-manual-personal-de-git)
  - [📌 Información general](#-información-general)
  - [🧭 Índice](#-índice)
    - [📝 Formato Markdown útil](#-formato-markdown-útil)
  - [1️⃣ Propósito y objetivos](#1️⃣-propósito-y-objetivos)
  - [2️⃣ Conceptos clave](#2️⃣-conceptos-clave)
  - [3️⃣ Flujo de trabajo sugerido](#3️⃣-flujo-de-trabajo-sugerido)
    - [Checklist rápida](#checklist-rápida)
  - [4️⃣ Comandos y tablas](#4️⃣-comandos-y-tablas)
    - [4.1 Comandos esenciales](#41-comandos-esenciales)
    - [4.2 Tablas útiles](#42-tablas-útiles)
      - [Tabla de errores frecuentes](#tabla-de-errores-frecuentes)
      - [Tabla de comandos extra para repasar](#tabla-de-comandos-extra-para-repasar)
    - [¿Que es Git?](#que-es-git)
  - [Comandos Terminal](#comandos-terminal)
      - [ls](#ls)
  - [📋 Comando `ls` – Variantes más comunes](#-comando-ls--variantes-más-comunes)
      - [pwd](#pwd)
      - [`MKFILE`](#mkfile)
  - [Configuración de GIT](#configuración-de-git)
      - [Git config](#git-config)
      - [Comando touch](#comando-touch)
    - [Git Init](#git-init)
  - [Rama en GIT](#rama-en-git)
    - [`git branch -m main`](#git-branch--m-main)
  - [Git ADD y COMMMIT](#git-add-y-commmit)

### 📝 Formato Markdown útil
- Usa tablas para comparar comandos, errores o conceptos semejantes.
- Prefiere listas cortas con verbos y enfócate en la acción tomada.
- Resalta hallazgos importantes con iconos (`✅`, `⚠️`, `❌`).
- Divide secciones largas con subtítulos (`###`) para mantener claridad.

## 1️⃣ Propósito y objetivos
- **Meta de aprendizaje:** ¿Qué deseas dominar con Git ahora? (ej. ramas, rebases, colaborar)
- **Nivel actual:** Anota qué sabes hoy y qué necesitas reforzar.
- **Preguntas guía:** Lista breve de dudas que deben resolverse (ej. “¿Cuándo usar `git pull --rebase`?”).

## 2️⃣ Conceptos clave
| Concepto | Definición | Analogía visual | Notas rápidas |
| --- | --- | --- | --- |
| Repositorio | Contenedor de commits y ramas | Biblioteca con versiones | Local vs remota |
| Commit | Foto del código | Guardar un punto de control | Mensajes cortos, verbo en infinitivo |
| Rama | Línea paralela | Camino de proyecto paralelo | `main`, `feature/*` |
| Merge | Fusionar | Encontrar punto de encuentro | Evita conflictos repetidos |
| Rebase | Reescribir historial | Moverte a la cima del tren | Ideal antes de `push` |

Incluye aquí otros términos como staging area, HEAD, stash, tag, upstream, etc.

## 3️⃣ Flujo de trabajo sugerido
1. **Preparación:** Revisa el estado actual con `git status` y asegúrate de trabajar en la rama adecuada.
2. **Desarrollo:** Usa `git add` selectivo y `git diff` para validar cambios antes del commit.
3. **Commit:** Escribe mensajes con verbo y contexto (`Fix button layout`).
4. **Sincronización:** Actualiza tu rama (`git pull --rebase`) antes de compartir.
5. **Revisión:** Usa `git log --oneline` y `git diff origin/main` para verificar el contexto.

### Checklist rápida
- [ ] Estado limpio antes de comenzar
- [ ] Cambios revisados con `git diff`
- [ ] Mensaje de commit claro
- [ ] Push exitoso y sin conflictos
- [ ] Notas agregadas en esta plantilla (si hubo hallazgos)

## 4️⃣ Comandos y tablas
### 4.1 Comandos esenciales
| Acción | Comando | Propósito | Recordatorio |
| --- | --- | --- | --- |
| Inicializar repo | `git init` | Crear seguimiento | Útil para proyectos nuevos |
| Estado | `git status -sb` | Ver rápido estado | Cambios staged/unstaged |
| Añadir | `git add <file>` | Stage selectivo | Usa `-p` para fragmentos |
| Commit | `git commit -m "mensaje"` | Guardar checkpoint | Mensaje claro y presente |
| Ver historial | `git log --oneline --graph` | Visualizar cambios | Añade `--decorate` |
| Fusionar | `git merge feature` | Junta ramas | Resuelve conflictos en el momento |
| Rebasing | `git rebase main` | Actualiza rama | Ideal antes de push |
| Push | `git push origin <rama>` | Compartir cambios | Requiere permisos |
| Pull | `git pull --rebase` | Traer cambios limpios | Evita merges innecesarios |

### 4.2 Tablas útiles
#### Tabla de errores frecuentes
| Error | Descripción | Pasos para recuperar |
| --- | --- | --- |
| Conflicto | `Merge failed` | Ver archivos (`git status`), editar, `git add`, `git commit` |
| HEAD detached | Aparece al checkout de un SHA | Crear rama (`git switch -c backup`) |
| Push rechazado | Historia divergente | `git pull --rebase origin main`, resolver y volver a enviar |

#### Tabla de comandos extra para repasar
| Nivel | Comando | Cómo usarlo |
| --- | --- | --- |
| Avanzado | `git reflog` | Recupera commits perdidos |
| Exploración | `git show HEAD~2` | Ver detalles anteriores |
| Limpieza | `git branch -d feature` | Borrar ramas fusionadas |

### ¿Que es Git?
Git es de codígo abierto, github es una paltaforma donde se aloja 
codigo, es una herramienta de control de versiones.

Nos permite llevar el historial de cambios, como una linea de tiempo
poder consultar desde que se comenzo el proyecto hasta que finalice.

Inicialmente, git aparecio 7 de abril del 2005 es una tecnologia que sigue evolucionando.

crado por Linus Torvalds quien ademas creo el Kernel de linux.

***git -h***
te ayudare a ver los comandos mas importantes en dado caso se te olvide uno.

## Comandos Terminal

#### ls
Sirve para mostrar los archivos y carpetas que hay dentro de un directorio por defecto muestra:
- Carpetas
- Archivos
## 📋 Comando `ls` – Variantes más comunes

| Comando | Descripción | Ejemplo de uso |
|-------|------------|---------------|
| `ls` | Lista archivos y carpetas del directorio actual | `ls` |
| `ls -l` | Lista detallada (permisos, tamaño, fecha, propietario) | `ls -l` |
| `ls -a` | Muestra archivos ocultos (`.` y `..`) | `ls -a` |
| `ls -la` | Lista detallada + archivos ocultos | `ls -la` |
| `ls -h` | Muestra tamaños legibles (KB, MB) | `ls -lh` |
| `ls -lh` | Detallado con tamaños legibles | `ls -lh` |
| `ls -R` | Lista recursivamente subcarpetas | `ls -R` |
| `ls -t` | Ordena por fecha de modificación | `ls -lt` |
| `ls -S` | Ordena por tamaño | `ls -lS` |
| `ls -r` | Orden inverso | `ls -lr` |
| `ls -1` | Un archivo por línea | `ls -1` |
| `ls --color=auto` | Colorea la salida por tipo de archivo | `ls --color=auto` |
| `ls nombre_carpeta` | Lista el contenido de una carpeta específica | `ls Documentos` |
| `ls *.txt` | Lista solo archivos `.txt` | `ls *.txt` |
| `ls */` | Lista solo carpetas | `ls */` |

como mover entre los directorios `cd` mas tabulador.

o tambien puede usar cd Desktop ejemplo.

***Ejemplo de Navegación***
```BASH
sanci@Sancir MINGW64 ~
$ cd OneDrive/

sanci@Sancir MINGW64 ~/OneDrive
$ ls
'Almacén personal.lnk'*   Document.docx                       Pictures/
'Datos adjuntos'/         Documentos/                         desktop.ini
 Desktop/                 Escritorio/
'Document 1.docx'        'HT #12 - TRANSPORTES 1S2025.docx'

sanci@Sancir MINGW64 ~/OneDrive
$ cd Escritorio/

sanci@Sancir MINGW64 ~/OneDrive/Escritorio
$

```
Si quieres regresar atras debes usar: **`cd ..`**

#### pwd
Sirve para saber en la ruta en que te encuentras y significa Print Working Directory (imprimir directorio de trabajo).

1️⃣ pwd -L (ruta lógica) ✅ por defecto
pwd -L


Muestra la ruta siguiendo enlaces simbólicos

Es el comportamiento normal de pwd

2️⃣ pwd -P (ruta física)
pwd -P


Muestra la ruta real del sistema, sin enlaces simbólicos

Útil si trabajas con enlaces (symlinks)


#### `MKFILE`
mkdir significa Make Directory (crear directorio).
Sirve para crear carpetas desde la terminal.

**EJEMPLO**
```BASH
mkdir "proyecto"

```
**Crear varias carpetas a la vez**
`mkdir docs src test`
Crea tres carpetas:
- docs
- src
- test

**Variante más importante: -p**

mkdir -p → crear carpetas padre si no existen

mkdir -p proyectos/web/frontend


✔ Crea toda la ruta completa aunque no exista nada.

💡 Es la opción más usada en la práctica.

| Comando | Descripción | Ejemplo |
|-------|------------|---------|
| `mkdir nombre` | Crea una carpeta | `mkdir proyecto` |
| `mkdir dir1 dir2` | Crea varias carpetas | `mkdir docs src` |
| `mkdir -p ruta` | Crea carpetas padre si no existen | `mkdir -p a/b/c` |
| `mkdir -m permisos` | Crea carpeta con permisos | `mkdir -m 755 privada` |
| `mkdir -v nombre` | Muestra mensaje al crear | `mkdir -v logs` |
| `mkdir -pv ruta` | Crea ruta completa y muestra proceso | `mkdir -pv app/api` |

## Configuración de GIT

#### Git config
establcere git a nivel global a la hora de trabajar
Sirve para configurar Git a nivel de usuario, es decir:

- La configuración se aplica a todos los repositorios de tu computadora
- No depende de un proyecto específico

| Comando | Qué hace |
|------|---------|
| `git config --global user.name "Nombre"` | Configura el nombre de usuario |
| `git config --global user.email "correo"` | Configura el correo |
| `git config --global --list` | Muestra configuración global |
| `git config --global core.editor "code --wait"` | Define editor por defecto |
| `git config --global color.ui auto` | Activa colores |
| `git config --global alias.st status` | Crea alias |

#### Comando touch
| Comando | Descripción | Ejemplo |
|------|------------|---------|
| `touch archivo` | Crea archivo vacío | `touch notas.txt` |
| `touch a b c` | Crea varios archivos | `touch a.txt b.txt` |
| `touch -c archivo` | No crea archivo nuevo | `touch -c test.txt` |
| `touch -t fecha archivo` | Define fecha manual | `touch -t 202601201200 log.txt` |
| `touch -a archivo` | Cambia fecha de acceso | `touch -a archivo.txt` |
| `touch -m archivo` | Cambia fecha de modificación | `touch -m archivo.txt` |


### Git Init
`git init` inicializa un repositorio Git en una carpeta.

Convierte una carpeta normal en un repositorio controlado por Git.
Git:

Crea una carpeta oculta llamada .git

Empieza a rastrear versiones

Deja la carpeta lista para:
- commits
- ramas
- historial
- No sube nada a internet, todo es loca
  
***¿Qué contiene .git? (idea general)***
- HEAD → rama actual
- objects/ → historial real
- refs/ → ramas
- config → configuración del repo
- No se debe borrar ni editar a mano.

## Rama en GIT
Una rama en Git es un puntero móvil a un commit específico que permite desarrollar funcionalidades de forma aislada sin afectar la línea principal de desarrollo (rama main o master). Las ramas son fundamentales para:
- Trabajar en paralelo con otros desarrolladores
- Desarrollar características sin alterar el código estable
- Experimentar sin riesgo
- Gestionar diferentes versiones del proyecto
![RAMAS](/GIT/Imagenes/Diagrama%20Ramas.png)

### `git branch -m main`
Este comando renombra la rama actual y le pone el nombre main.
Normalmente se usa para cambiar la rama por defecto de master a main.

## Git ADD y COMMMIT

#
