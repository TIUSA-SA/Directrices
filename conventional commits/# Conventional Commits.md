# Conventional Commits

**Conventional Commits** es una especificación para añadir significado a la historia de cambios (commits) en un proyecto. Aporta una estructura estandarizada a los mensajes de commit, lo que facilita la automatización de tareas como generación de changelogs, versiones semánticas y revisión de cambios.

---

## Beneficios

- Facilita la lectura y comprensión de los cambios.
- Permite automatizar changelogs y versionado semántico (semver).
- Mejora la trazabilidad y organización del código.
- Favorece la colaboración en equipo con reglas claras de escritura.

---

## Estructura de un Commit Convencional

```bash
<tipo>[opcional alcance]: <mensaje breve>

[opcional descripción larga]
[opcional footer para issues o breaking changes]
```

### Ejemplo básico:
```bash
feat(auth): agregar validación de tokens JWT
```

### Ejemplo con descripción:
```bash
fix(api): corregir error de autenticación con tokens expirados

El error ocurría cuando el token expirado no se removía del storage.
Se añadió un interceptor para validar y limpiar tokens inválidos.
```

### Ejemplo con referencias:
```bash
feat(login): permitir autenticación con redes sociales

BREAKING CHANGE: se eliminó el flujo de login anterior basado en cookies.

Closes #123
```

---

## Tipos de Commits Comunes

| Tipo     | Descripción                                      |
|----------|--------------------------------------------------|
| `feat`   | Se añade una nueva funcionalidad.                |
| `fix`    | Corrección de errores.                           |
| `docs`   | Cambios en la documentación.                     |
| `style`  | Formato del código (espacios, comas, etc.).      |
| `refactor` | Cambios que no corrigen errores ni agregan funcionalidades. |
| `test`   | Añadir o modificar pruebas.                      |
| `chore`  | Cambios en herramientas, tareas o mantenimiento. |
| `perf`   | Mejora del rendimiento.                          |
| `build`  | Cambios relacionados con el sistema de build.    |
| `ci`     | Cambios en la configuración de integración continua. |

---

## Uso de Alcance (Scope)

El **alcance** es opcional, pero ayuda a indicar qué parte del sistema se ve afectada:
```bash
feat(auth): agregar método de recuperación de contraseña
fix(ui): corregir scroll en lista de usuarios
```

---

## Convenciones Adicionales

- Usar infinitivo y minúsculas en el mensaje breve.
- No terminar la línea del título con punto.
- Incluir `BREAKING CHANGE:` cuando se introduzcan cambios incompatibles.
- Relacionar issues con `Closes #<número>` o `Refs #<número>` en el footer.

---

## Herramientas Complementarias

- [commitlint](https://commitlint.js.org/): Valida que los commits cumplan con la convención.
- [standard-version](https://github.com/conventional-changelog/standard-version): Genera versiones semánticas y changelogs automáticamente.
- Integración con GitHub Actions o CI/CD para rechazar commits mal formateados.

---

## Conclusión

Adoptar Conventional Commits en el equipo de desarrollo permite una mejor comunicación, automatización de procesos y una gestión más clara del historial del proyecto. Su implementación es sencilla y escalable para equipos pequeños y grandes por igual.

