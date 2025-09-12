# skeleton-ia

## Descripción
Este proyecto es una plantilla para levantar un entorno de desarrollo completo usando Docker Compose. Incluye los siguientes servicios:

- **PostgreSQL con pgvector**: Base de datos relacional con soporte para almacenamiento y búsqueda de vectores, ideal para aplicaciones de IA y búsquedas semánticas. Se inicializa con el script `init-evolution.sql` (crea la base de datos `evolution`) y el script `init-pgvector.sql` (habilita la extensión vectorial).
- **pgAdmin**: Herramienta web para administrar la base de datos PostgreSQL, accesible desde el puerto 8081 en localhost.
- **Redis**: Almacenamiento en memoria para caché y persistencia de datos.
- **Evolution API**: API oficial de Evolution, expuesta en el puerto 8080 solo en localhost, configurada mediante variables de entorno y con persistencia de instancias.

Todos los servicios se comunican a través de una red interna definida en Docker Compose, y los datos relevantes se almacenan en volúmenes persistentes.

## Requisitos
- Docker
- Docker Compose

## Cómo ejecutar

1. Clona este repositorio:
   ```powershell
   git clone https://github.com/bl0pez/skeleton-ia.git
   cd skeleton-ia
   ```

2. Crea un archivo `.env` con las variables necesarias para PostgreSQL, pgAdmin y Evolution API. Ejemplo:
   ```env
   POSTGRES_USER=usuario
   POSTGRES_PASSWORD=contraseña
   POSTGRES_DB=evolution
   PGADMIN_DEFAULT_EMAIL=admin@ejemplo.com
   PGADMIN_DEFAULT_PASSWORD=adminpass
   # Variables adicionales para evolution-api
   ```

3. Inicia los servicios con Docker Compose:
   ```powershell
   docker-compose up -d
   ```

4. La base de datos `evolution` y la extensión vectorial (pgvector) se crean automáticamente al iniciar el contenedor de PostgreSQL gracias a los scripts `init-evolution.sql` y `init-pgvector.sql`.

5. Accede a pgAdmin en [http://localhost:8081](http://localhost:8081) y a la Evolution API en [http://localhost:8080](http://localhost:8080) (solo desde localhost).

6. Para detener los servicios:
   ```powershell
   docker-compose down
   ```

## Estructura
- `docker-compose.yml`: Configuración de los servicios Docker (PostgreSQL con pgvector, pgAdmin, Redis, Evolution API).
- `init-evolution.sql`: Script de inicialización que crea la base de datos `evolution`.
- `init-pgvector.sql`: Script que habilita la extensión vectorial pgvector en PostgreSQL.
- `.env`: Variables de entorno necesarias para los servicios.
## Uso de pgvector

Una vez levantado el entorno, puedes crear tablas con columnas vectoriales en PostgreSQL usando:

```sql
CREATE TABLE items (
   id serial PRIMARY KEY,
   embedding vector(1536)
);
```

Consulta la documentación oficial de [pgvector](https://github.com/pgvector/pgvector) para más ejemplos y casos de uso.

## Licencia
Este proyecto está bajo la Licencia MIT. Consulta el archivo `LICENSE` para más detalles.
