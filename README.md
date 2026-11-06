# dsy1104-meta

Repositorio paraguas del taller de despliegue en AWS de **DSY1104 Full Stack 2**. Reúne el frontend y el backend como submódulos de Git, un `docker-compose` para levantar todo en local y el material de clase.

```
dsy1104-meta/
├── backend/        submódulo → dsy1104-backend  (Spring Boot, API REST)
├── frontend/       submódulo → dsy1104-frontend (React + Vite)
├── docker-compose.yml
├── docs/           guías del taller
└── presentacion/   diapositivas
```

## Clonar

```bash
git clone --recurse-submodules https://github.com/donkiwicl/dsy1104-meta.git
cd dsy1104-meta
```

Si ya clonaste sin submódulos: `git submodule update --init --recursive`.

## Levantar el entorno local

Requiere Docker con Compose.

```bash
docker compose up --build
```

| Servicio | URL |
| --- | --- |
| Frontend | http://localhost:3000 |
| API | http://localhost:8080/api/productos |
| Salud | http://localhost:8080/actuator/health |

El entorno replica la arquitectura de AWS: `db` equivale a RDS, `backend` a la instancia EC2 y `frontend` al bucket de S3. Las credenciales locales tienen valores por defecto; para cambiarlas copia `.env.example` a `.env`.

```bash
docker compose down        # detener
docker compose down -v     # detener y borrar los datos de MySQL
```

## Actualizar los submódulos

```bash
git submodule update --remote --merge
git add backend frontend && git commit -m "Actualiza submódulos"
```

Los cambios de código se hacen y se suben dentro de cada submódulo (`cd backend && git commit ... && git push`); después se registra el nuevo commit en este repositorio.
