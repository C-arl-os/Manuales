# Introducción a Git — LabEx

> Manual de referencia construido a partir del curso de Git en LabEx.
> Cubre desde los conceptos básicos de control de versiones hasta flujos de trabajo colaborativos.

---

## Tabla de Contenidos

- [Sobre este manual](#sobre-este-manual)
- [¿Qué es Git y por qué importa?](#qué-es-git-y-por-qué-importa)
- [Cómo usar este manual](#cómo-usar-este-manual)
- [Labs](#labs)
- [Referencia Rápida](#referencia-rápida)
- [Errores Humanos Frecuentes](#errores-humanos-frecuentes)
- [Glosario](#glosario)

---

## Sobre este manual

**Nivel:** Principiante
**Enfoque:** Control de versiones con Git, desde configuración inicial hasta colaboración en equipo
**Prerequisito recomendado:** Manejo básico de terminal (comandos de navegación y archivos)

### Qué cubre este manual

Al completar este manual serás capaz de:

- Entender qué es el control de versiones y por qué se usa
- Inicializar y configurar repositorios Git
- Registrar cambios con commits significativos
- Trabajar con ramas para desarrollo paralelo
- Colaborar con otros mediante repositorios remotos
- Resolver conflictos de fusión

---

## ¿Qué es Git y por qué importa?

**Git** es un sistema de control de versiones distribuido. Registra cada cambio que haces en tu código, quién lo hizo y cuándo.

### El problema que resuelve

Sin Git, el historial de un proyecto se ve así:
```
proyecto_final.zip
proyecto_final_v2.zip
proyecto_final_ESTE_SI.zip
proyecto_final_definitivo_ahora_si.zip
```

Con Git:
```
commit a3f2b1c  "Agrega validación de formulario"
commit 9e8d7c5  "Corrige bug en login"
commit 4b2a1f0  "Versión inicial"
```

Cada versión tiene nombre, descripción y autor. Puedes volver a cualquiera en cualquier momento.

### Los tres estados de Git

Todo archivo en un repositorio Git vive en uno de estos tres estados:

```
Working Directory    →    Staging Area    →    Repository
  (archivos           (archivos listos      (historial
   modificados)        para commit)          permanente)

    git add →              git commit →
```

| Estado | Qué significa |
|--------|--------------|
| **Working Directory** | Archivos en tu disco, con o sin cambios |
| **Staging Area** | Cambios marcados para incluir en el próximo commit |
| **Repository** | Historial permanente de commits |

### Git vs GitHub

| Git | GitHub |
|-----|--------|
| Programa que corre en tu computadora | Sitio web que almacena repositorios en la nube |
| Gestiona el historial local | Facilita la colaboración remota |
| Funciona sin internet | Requiere internet |
| Gratis y de código abierto | Servicio de Microsoft (gratuito con planes de pago) |

> Git es la herramienta. GitHub es uno de los servicios que la usa (también existen GitLab, Bitbucket, etc.).

---

## Cómo usar este manual

Cada lab sigue la misma estructura:

- **Escenario** — el contexto práctico del lab
- **Comandos nuevos** — explicación, sintaxis y ejemplos
- **Flujo del lab** — cómo se conectan los pasos
- **Errores frecuentes** — qué puede salir mal en este lab
- **Ejercicio** — práctica independiente en cualquier máquina con Git instalado

> Para practicar solo necesitas Git instalado. Puedes verificarlo con `git --version` en tu terminal.

---

## Labs

> Los labs se agregarán conforme avances en el curso.

---

## Referencia Rápida

| Comando | Descripción breve | Lab |
|---------|------------------|-----|
| —       | —                | —   |

---

## Errores Humanos Frecuentes

> Esta sección se irá llenando conforme avancen los labs.

---

## Glosario

| Término | Definición |
|---------|-----------|
| **Repositorio** | Carpeta de proyecto con todo su historial de cambios gestionado por Git |
| **Commit** | Instantánea permanente del estado del proyecto en un momento dado |
| **Staging area** | Zona intermedia donde se preparan los cambios antes de hacer commit |
| **Branch (rama)** | Línea de desarrollo paralela e independiente del proyecto |
| **Merge** | Fusión de dos ramas en una |
| **Remote** | Repositorio almacenado en un servidor (GitHub, GitLab, etc.) |
| **Clone** | Copia completa de un repositorio remoto en tu máquina local |
| **Push** | Enviar commits locales al repositorio remoto |
| **Pull** | Traer cambios del repositorio remoto a tu copia local |
| **HEAD** | Puntero que indica en qué commit o rama estás trabajando ahora |
| **Working tree** | Los archivos del proyecto tal como están en tu disco ahora mismo |
| **Index** | Otro nombre para el staging area |
| **Hash / SHA** | Identificador único de cada commit (ej. `a3f2b1c`) — generado automáticamente |

---

_Última actualización: 2026-03-28_
