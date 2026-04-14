# Mi primer proyecto con FastAPI 🐍

Hola! Soy Hugo y estoy aprendiendo Python y desarrollo de APIs. Este es uno de mis primeros proyectos "de verdad" — antes solo hacía scripts sueltos y cositas básicas, pero me propuse construir algo con más estructura.

Me metí a aprender FastAPI porque leí que es moderno, rápido y tiene buena documentación. La verdad que al principio fue bastante confuso, sobre todo la parte de bases de datos y la autenticación, pero de a poco le fui agarrando la mano.

---

## ¿Qué hace este proyecto?

Es una API REST que funciona como el backend de una especie de red social sencilla. Por ahora permite:

- **Registrar usuarios** y que puedan **iniciar sesión** con un token JWT
- **Crear posts** que incluyen una imagen o video, que se sube a la nube con ImageKit
- **Guardar todo** en una base de datos con SQLAlchemy

Todavía le falta bastante, pero ya funciona lo básico y eso es lo importante 😅

---

## Tecnologías que usé

| Tecnología | Por qué la usé |
|---|---|
| **FastAPI** | El framework principal. Me gustó que genera documentación automática |
| **SQLAlchemy** | Para manejar la base de datos desde Python sin escribir SQL puro |
| **fastapi-users** | Una librería que simplifica un montón el sistema de login/registro |
| **ImageKit** | Para subir imágenes y videos a la nube |
| **SQLite** | Base de datos sencilla para desarrollo local, no necesitás instalar nada extra |
| **Pydantic** | Para validar los datos que llegan a la API (la usa FastAPI por debajo) |
| **uvicorn** | El servidor que corre la aplicación |
| **uv** | Manejador de entornos y dependencias, lo descubrí hace poco y es muy rápido |

---

## Estructura del proyecto

```
FastApiTutorial/
├── main.py           # Acá arranca todo, levanta el servidor
├── pyproject.toml    # Dependencias del proyecto
└── app/
    ├── app.py        # Las rutas y la lógica principal
    ├── db.py         # Los modelos de la base de datos (User, Post)
    ├── users.py      # Todo lo de autenticación y tokens JWT
    ├── schemas.py    # Los "moldes" para validar datos con Pydantic
    └── images.py     # La configuración para subir archivos a ImageKit
```

---

## Cómo correrlo

Necesitás Python 3.12 o superior.

### 1. Clonar el repo

```bash
git clone https://github.com/MartinOlazabal/Fast-API-project.git
cd Fast-API-project
```

### 2. Instalar dependencias

Con `uv` (lo que yo uso, lo recomiendo):

```bash
uv sync
```

Con pip clásico:

```bash
python -m venv .venv
.venv\Scripts\activate     # Windows
source .venv/bin/activate  # Mac/Linux
pip install -e .
```

### 3. Configurar variables de entorno

Crear un archivo `.env` en la raíz con:

```
IMAGEKIT_PRIVATE_KEY=tu_clave_privada
IMAGEKIT_URL_ENDPOINT=https://ik.imagekit.io/tu_id
```

> ⚠️ El `.env` no se sube al repositorio porque tiene claves privadas. Lo aprendí de la peor manera jaja.

### 4. Correr la app

```bash
python main.py
```

Listo, la API levanta en `http://localhost:8000`

### 5. Probar los endpoints

FastAPI tiene una interfaz web para probar la API sin necesidad de instalar nada extra:

- **Swagger UI** → http://localhost:8000/docs
- **ReDoc** → http://localhost:8000/redoc

---

## Endpoints disponibles

| Método | Ruta | Descripción | ¿Requiere login? |
|---|---|---|---|
| `POST` | `/auth/register` | Registrar un usuario nuevo | No |
| `POST` | `/auth/jwt/login` | Iniciar sesión, devuelve el token | No |
| `POST` | `/posts/` | Crear un post con imagen/video | Sí |

---

## Cosas que aprendí haciendo esto

- Cómo funciona la autenticación con **JWT** (básicamente es un token firmado que tiene fecha de vencimiento)
- A usar **async/await** en Python, que al principio me rompió la cabeza pero tiene sentido
- A modelar tablas con **SQLAlchemy** y hacer relaciones entre ellas (un User tiene muchos Posts)
- Que **Pydantic** te salva la vida validando los datos antes de que lleguen a la base de datos
- A nunca jamás subir el `.env` a GitHub 💀

---

## Lo que falta / ideas para el futuro

- [ ] Endpoint para listar posts
- [ ] Poder editar y eliminar posts
- [ ] Relacionar posts con el usuario que los creó en las respuestas
- [ ] Paginación
- [ ] Escribir tests (todavía no aprendí bien cómo)
- [ ] Deploy en algún servidor real

---

## Recursos que me ayudaron

- [Documentación oficial de FastAPI](https://fastapi.tiangolo.com/)
- [Documentación de fastapi-users](https://fastapi-users.github.io/fastapi-users/)
- [SQLAlchemy docs](https://docs.sqlalchemy.org/)
- Mucho Stack Overflow y algunos videos de YouTube que no recuerdo cuáles eran jaja

---

*Cualquier sugerencia o corrección es bienvenida, todavía estoy aprendiendo* 🙏
