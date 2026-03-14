# Data Model

Descripción del modelo normalizado para la aplicación TMDB.

## Entidades principales

- Movie
  - id (integer)
  - title (string)
  - release_date (date)
  - ...
- Genre
  - id (integer)
  - name (string)

## Reglas de transformación

1. Convertir fechas a formato ISO 8601.
2. Normalizar nombres de campos camelCase a snake_case.
3. Filtrar valores nulos.

<!-- Añadir más detalles según sea necesario -->