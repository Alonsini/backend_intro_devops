# backend_intro_devops

API REST de gestión de tareas construida con **Node.js + Express**.
Forma parte de la asignatura **Introducción a Herramientas DevOps (ISY1101)**.

---

## Stack

- Node.js 20 (imagen base `node:20-alpine`)
- Express 4
- Persistencia en archivo JSON montado por volumen Docker

---

## Estructura

```
backend_intro_devops/
├── src/
│   └── server.js        ← API REST (rutas, lógica, persistencia)
├── Dockerfile
├── .dockerignore
├── package.json
└── .env.example
```

---

## Variables de entorno

| Variable | Valor por defecto | Descripción |
|---|---|---|
| `PORT` | `3000` | Puerto en que escucha la API |
| `MENSAJE_BIENVENIDA` | `API de Tareas` | Mensaje del endpoint raíz `GET /` |

Copia `.env.example` como `.env` antes de correr en local:

```bash
cp .env.example .env
```

---

## Endpoints

| Método | Ruta | Descripción |
|---|---|---|
| GET | `/` | Mensaje de bienvenida |
| GET | `/health` | Healthcheck (uptime) |
| GET | `/api/tareas` | Listar todas las tareas |
| GET | `/api/tareas/:id` | Obtener una tarea por ID |
| POST | `/api/tareas` | Crear tarea `{ "titulo": "..." }` |
| PATCH | `/api/tareas/:id` | Actualizar `completada` o `titulo` |
| DELETE | `/api/tareas/:id` | Eliminar una tarea |

---

## Cómo correr en local

### Sin Docker

```bash
npm install
npm start
# API disponible en http://localhost:3000
```

### Con Docker

```bash
# Construir imagen
docker build -t tareas-backend:1.0 .

# Correr contenedor con volumen para persistencia
docker run -d \
  --name tareas-backend \
  -p 3000:3000 \
  -v datos-tareas:/data \
  --env-file .env \
  tareas-backend:1.0
```

Verifica que responde:

```bash
curl http://localhost:3000/api/tareas
```

---

## Uso en las experiencias del curso

Este repositorio es el código base que se usa en las actividades prácticas.

| Experiencia | Qué se trabaja |
|---|---|
| Experiencia 2 – Docker en local | Build de imagen, `docker run`, volúmenes, redes, Docker Compose |
| Experiencia 3 – ECR + EC2 | Push a Amazon ECR, despliegue en instancia EC2 |

Repositorio de ejercicios: [repo_ejercicios](https://github.com/Umbingelelo/frontend_intro_devops)

---

## Repositorio del frontend

[https://github.com/Umbingelelo/frontend_intro_devops](https://github.com/Umbingelelo/frontend_intro_devops)
