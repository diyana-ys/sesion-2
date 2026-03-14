# Política de Dependencias

- Se usa un gestor de dependencias (npm/poetry/...) según el stack.
- Actualizar dependencias siguiendo semver.
- Revisar changelog de cada paquete antes de hacer bump.

## Version Bump

- Los cambios mayores en dependencias deben revisarse en PR.
- Se recomienda fijar versiones con rangos (`^` o `~`) según estabilidad.

> Nota: Mantener actualizadas las dependencias para evitar vulnerabilidades.