# TMDB API Endpoints

## 1) Endpoints principales de TMDB (para app estilo Netflix)

| Endpoint | Descripción | Parámetros clave | Uso
|---|---|---|---|
| `GET /movie/popular` | Películas populares | `page`, `language`, `region` | Home sección "Populares"
| `GET /movie/top_rated` | Películas mejor valoradas | `page`, `language` | Home sección "Top"
| `GET /movie/upcoming` | Próximos estrenos | `page`, `language`, `region` | Home "Próximos" 
| `GET /tv/popular` | Series populares | `page`, `language`, `region` | Home sección series 
| `GET /tv/top_rated` | Series top | `page`, `language` | Home top series 
| `GET /tv/on_the_air` | Series al aire | `page`, `language`, `region` | Home

## 2) Detalles y datos extendidos

| Endpoint | Descripción | Parámetros | Uso
|---|---|---|---|
| `GET /movie/{movie_id}` | Detalle película | `language`, `append_to_response` | Pantalla detalle
| `GET /tv/{tv_id}` | Detalle serie | `language`, `append_to_response` | Pantalla detalle
| `GET /movie/{movie_id}/videos` | Trailers + clips | `language` | Trailers en detalle
| `GET /tv/{tv_id}/videos` | Trailers serie | `language` | Trailers en detalle
| `GET /movie/{movie_id}/credits` | Reparto equipo | `language` | Cast en detalle
| `GET /tv/{tv_id}/credits` | Reparto equipo | `language` | Cast en detalle
| `GET /movie/{movie_id}/recommendations` | Recomendadas | `language`, `page` | Sugerencias
| `GET /tv/{tv_id}/recommendations` | Recomendadas series | `language`, `page` | Sugerencias
| `GET /movie/{movie_id}/similar` | Similares | `language`, `page` | Sugerencias
| `GET /tv/{tv_id}/similar` | Similares series | `language`, `page` | Sugerencias

## 3) Búsqueda y descubrimiento

| Endpoint | Descripción | Parámetros clave | Uso
|---|---|---|---|
| `GET /search/movie` | Buscar películas | `query`, `page`, `include_adult`, `language` | Barra de búsqueda
| `GET /search/tv` | Buscar series | `query`, `page`, `language` | Barra de búsqueda
| `GET /search/multi` | Buscar en todo | `query`, `page`, `language` | Búsqueda universal
| `GET /discover/movie` | Descubrimiento películas | `page`, `with_genres`, `sort_by`, `primary_release_year`, `vote_average.gte` | Filtros avanzados
| `GET /discover/tv` | Descubrimiento series | `page`, `with_genres`, `sort_by`, `first_air_date_year`, `vote_average.gte` | Filtros avanzados
| `GET /genre/movie/list` | Lista de géneros películas | `language` | Filtros UI
| `GET /genre/tv/list` | Lista de géneros series | `language` | Filtros UI
| `GET /trending/{media_type}/{time_window}` | Tendencias | `media_type=all/movie/tv`, `time_window=day/week` | Sección "Tendencias"

## 4) Reglas y buenas prácticas para consumo (Node + React + Dotenv)

- Nunca exponer `TMDB_API_KEY` en cliente React. Usar backend proxy.
- Usar variables de entorno:
  - `TMDB_API_KEY`
  - `TMDB_BASE_URL=https://api.themoviedb.org/3`
  - `TMDB_IMAGE_BASE_URL=https://image.tmdb.org/t/p/`
  - `TMDB_LANGUAGE=es-ES` (o `en-US`)
  - `VITE_API_URL=http://localhost:4000/api` (frontend)
- Backend debe cachear respuestas (memory/Redis) y manejar rate limit.
- Implementar paginación y filtros en cada listado (`page`, `with_genres`, `sort_by`, `year`, `vote_average.gte`).
- Definir DTO con campos comunes: `id`, `title/name`, `media_type`, `overview`, `poster_path`, `backdrop_path`, `vote_average`, `release_date/first_air_date`.

## 5) UI requerimientos mínimos

- Listados con skeleton loading y estados de carga.
- Carrusel horizontal con scroll.
- Dropdown modernos para filtros: género, año, clasificación, tipo (movie/tv).
- Modo claro/oscuro.
- Pagina de detalle con hero, sinopsis, videos, reparto, recomendados.

## 6) Ejemplo de request básico (Node backend)

```http
GET https://api.themoviedb.org/3/movie/popular?api_key=YOUR_KEY&language=es-ES&page=1
```

> Nota: el backend debe agregar la key y retornar JSON limpio al frontend.
