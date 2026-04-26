# AGENTS.md — Guía para agentes de IA

Este fichero describe el proyecto, su estructura, las convenciones de desarrollo y las instrucciones que deben seguir
los agentes de IA (GitHub Copilot, etc.) al trabajar en este repositorio.

## Descripción del proyecto

Aplicación que facilita a los profesores organizar la resolución de preguntas durante una clase permitiendo que los
alumnos pidan su turno y sean atendidos de uno en uno.

## Estructura del repositorio

Este repositorio raíz es intencionalmente casi vacío: solo contiene el `README.md` y este `AGENTS.md`. **Todo el
contenido está ignorado a propósito** mediante `.gitignore`.

El trabajo real se encuentra en subdirectorios, cada uno de los cuales es un **repositorio Git independiente**. Esta es
una decisión de diseño del proyecto.

Cada subdirectorio puede contener además su propio fichero AGENTS.md con instrucciones para agentes, que todos los
agentes deberán leer y seguir. Las instrucciones de un subdirectorio tienen **precedencia** sobre las de este AGENTS.md
en caso de conflicto.

### Sub-repositorios

| Directorio  | Descripción                                           | Stack principal                          |
|-------------|-------------------------------------------------------|------------------------------------------|
| `backend/`  | Firebase Cloud Functions (API)                        | Node.js 22, Firestore, Hashids           |
| `web/`      | Sitio web estático (página principal + privacidad)    | Jekyll, Firebase Hosting                 |
| `android/`  | Apps alumno y profesor para Android                   | Kotlin, Jetpack Compose, Material 3      |
| `ios/`      | Apps alumno y profesor para iOS                       | Swift, SwiftUI, MVVM                     |
| `vue/`      | Apps web alumno y profesor (futuras versiones web)    | Vue 3, TypeScript, Vite, Pinia           |
| `shared/`   | Recursos gráficos y diagramas compartidos             | Solo assets, sin código ejecutable       |
| `private/`  | Credenciales, certificados y material sensible        | ⚠️ Solo lectura — ver advertencia abajo  |

### Infraestructura común

- **Firebase** es la plataforma de backend para todas las apps: Auth, Firestore, App Check, Cloud Functions y Hosting.
- **Proyecto Firebase de producción:** `turnoclase-eu` (región `europe-west1`).
- Los entornos locales de `backend/` y `web/` están dockerizados; usar `make` para las tareas habituales.

## Instrucciones para agentes

- **No crear commits en este repositorio raíz** salvo para modificar `README.md` o `AGENTS.md`.
- Para trabajar en el código, entrar en el subdirectorio correspondiente y operar sobre su repositorio Git propio.
- **Leer siempre el AGENTS.md del subdirectorio** antes de empezar a trabajar en él.
- **No leer ni exponer el contenido** de ningún fichero del repositorio `private/` (credenciales, certificados,
  keystores, etc.). Tratar todos sus ficheros como de solo lectura y usarlos exclusivamente por su ruta.

## Convenciones de commits

> **Regla fundamental**: cada funcionalidad completada o corrección de bug debe tener su propio commit independiente. No
> agrupar cambios no relacionados en un mismo commit.

### Cuándo hacer commit

- Al completar una funcionalidad nueva (aunque sea parcial pero funcional).
- Al corregir un bug concreto.
- Al añadir o actualizar documentación relevante.
- **No** hacer commit de código roto o que no compila.

### Formato del mensaje de commit

Usar [Conventional Commits](https://www.conventionalcommits.org/):

```
<tipo>(<scope>): <descripción breve en imperativo>
```

- **El mensaje debe escribirse en español.**
- Ejemplos de tipos: `feat`, `fix`, `docs`, `refactor`, `chore`.

### Trailer obligatorio

Todo commit creado por un agente de IA debe incluir el trailer con su información de co-autoría al final del mensaje.
