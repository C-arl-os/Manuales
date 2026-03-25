# Manual de Linux — LabEx Labs

> Manual de referencia personal construido a partir de los laboratorios de LabEx.
> Cada sección cubre los comandos usados en un lab, con explicación y ejemplos.

---

## Tabla de Contenidos

- [Cómo usar este manual](#cómo-usar-este-manual)
- [Conceptos Fundamentales](#conceptos-fundamentales)
- [Labs](#labs)
  - [Lab 01 — (pendiente)](#lab-01)
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

## Conceptos Fundamentales

> Esta sección se llena con conceptos que aplican a múltiples labs.

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

---

## Labs

---

### Lab 01

> _Título y contexto del lab se agregarán cuando me pases los comandos._

---

## Referencia Rápida

Tabla con los comandos más usados. Se llena automáticamente conforme avanzas.

| Comando | Descripción breve | Sección |
|---------|------------------|---------|
| —       | —                | —       |

---

## Glosario

| Término | Definición |
|---------|-----------|
| **Shell** | Intérprete de comandos (bash, zsh, etc.) |
| **Directorio** | Equivalente a una carpeta en Linux |
| **Ruta absoluta** | Ruta completa desde `/` (ej. `/home/user/docs`) |
| **Ruta relativa** | Ruta desde el directorio actual (ej. `./docs`) |
| **Flag / Opción** | Modificador de un comando (ej. `-l` en `ls -l`) |
| **Root** | Usuario administrador con todos los permisos (`#`) |
| **Permiso** | Control de quién puede leer/escribir/ejecutar un archivo |

---

_Última actualización: 2026-03-25_
