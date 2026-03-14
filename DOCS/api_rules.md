# Reglas para consumir TMDB (Node + dotenv + React + Tailwind + shadcn)

## 1) Variables de entorno (dotnet)

Backend (`.env`):
- `TMDB_API_KEY=tu_api_key_tmdb`
- `TMDB_BASE_URL=https://api.themoviedb.org/3`
- `TMDB_IMAGE_BASE_URL=https://image.tmdb.org/t/p/`
- `TMDB_LANGUAGE=es-ES`
- `PORT=4000`

Frontend (`.env` o `.env.local`):
- `VITE_API_URL=http://localhost:4000/api`

> No exponer `TMDB_API_KEY` en el frontend.

## 2) Endpoints proxy comunes en backend

- `/api/movies/popular?page=1`
- `/api/movies/top-rated?page=1`
- `/api/movies/upcoming?page=1`
- `/api/tv/popular?page=1`
- `/api/tv/top-rated?page=1`
- `/api/trending/:media_type/:time_window`
- `/api/search?q=...&type=movie|tv|multi&page=1`
- `/api/movie/:id`
- `/api/tv/:id`
- `/api/movie/:id/videos`
- `/api/tv/:id/videos`
- `/api/movie/:id/credits`
- `/api/tv/:id/credits`
- `/api/movie/:id/recommendations`
- `/api/tv/:id/recommendations`
- `/api/discover/movie?...` y `/api/discover/tv?...`

## 3) Reglas de paginación y filtros

- Siempre enviar `page` en listados grandes.
- Filtrar con parámetros:
  - `with_genres`
  - `sort_by` (`popularity.desc`, `vote_average.desc`, etc.)
  - `primary_release_year` / `first_air_date_year`
  - `vote_average.gte`
  - `language`
- Soportar `region` para estrenos localizados.
- Backend debe recibir query y mapear a TMDB.

## 4) UI y experiencia de usuario

- Componentes base (shadcn): `Button`, `Input`, `Dropdown`, `Card`, `Badge`, `Skeleton`, `Tabs`, `Dialog`.
- Home: Hero grande, secciones con carrusel horizontal.
- Filtros: dropdown modernos con `genre`, `year`, `rating`.
- Paginación: controls `Anterior / Siguiente`.
- Loading: skeleton cards con shimmer.
- Modo claro/oscuro dependiente de `prefers-color-scheme` o toggle.

## 5) Estructura de datos devueltos (front)

Cada item debe normalizarse a:
- `id`
- `media_type` (`movie`/`tv`)
- `title` (movie) / `name` (tv)
- `overview`
- `poster_path`
- `backdrop_path`
- `vote_average`
- `release_date` / `first_air_date`
- `genre_ids`

## 6) Caché y resiliencia

- Cachear respuestas de TMDB por 1-5 minutos (popular, top-rated, detalle). 
- Manejar errores HTTP (401, 429, 500) y mostrar mensaje útil.
- Retry/backoff en backend para llamadas externas.

## 7) Reglas de implementación de versión

- Prioriza MVP (Home, detalle, búsqueda, mi lista).
- Versión `0.x.y` para desarrollo; `1.0.0` para release con app completa.
- Fecha objetivo inicial para MVP: 2026-03-25.
