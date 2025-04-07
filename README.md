# Gestor de Tareas

## Descripción

**Gestor de Tareas** es una aplicación backend diseñada para gestionar las tareas de los usuarios de forma eficiente y segura. Los usuarios pueden registrarse, iniciar sesión y administrar sus tareas (crear, leer, actualizar y eliminar) a través de una API RESTful. El sistema está implementado en Node.js y utiliza PostgreSQL como base de datos para el almacenamiento persistente de los datos.

## Características

- **Registro y Login de Usuarios**: Los usuarios pueden registrarse y autenticarse mediante un sistema basado en JWT.
- **Gestión de Tareas**: Los usuarios pueden crear, listar, buscar, actualizar y eliminar tareas.
- **Autenticación con JWT**: El sistema asegura que solo los usuarios autenticados puedan acceder y gestionar sus tareas.

## Tecnologías Utilizadas

- **Node.js**: Framework de JavaScript para construir la API RESTful.
- **Express**: Framework web para Node.js que facilita la creación de la API.
- **PostgreSQL**: Sistema de gestión de bases de datos relacional para almacenar los datos.
- **Sequelize**: ORM que facilita la interacción con la base de datos y asegura la protección contra inyecciones SQL.
- **JWT (JSON Web Tokens)**: Utilizado para la autenticación de usuarios y la protección de rutas.
- **bcrypt.js**: Para la encriptación de contraseñas de los usuarios.

## Endpoints de la API

### 1. Autenticación

#### Registrar usuario
- **Método**: `POST`
- **URL**: `/api/auth/register`
- **Cuerpo (JSON)**:
    ```json
    {
        "nombre": "Juan",
        "email": "juan@mail.com",
        "password": "123456"
    }
    ```
- **Descripción**: Permite registrar un nuevo usuario.

#### Login de usuario
- **Método**: `POST`
- **URL**: `/api/auth/login`
- **Cuerpo (JSON)**:
    ```json
    {
        "email": "juan@mail.com",
        "password": "123456"
    }
    ```
- **Descripción**: Permite iniciar sesión con un usuario registrado. Devuelve un token JWT para autenticar futuras solicitudes.

#### Obtener usuario autenticado
- **Método**: `GET`
- **URL**: `/api/auth/me`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Descripción**: Obtiene la información del usuario autenticado.

### 2. Gestión de Tareas

#### Crear tarea
- **Método**: `POST`
- **URL**: `/api/tasks`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Cuerpo (JSON)**:
    ```json
    {
        "titulo": "Organizar reunión de equipo",
        "descripcion": "Planificar la reunión de equipo para discutir el avance del proyecto.",
        "fechaLimite": "2025-04-15"
    }
    ```
- **Descripción**: Permite crear una nueva tarea.

#### Listar todas las tareas
- **Método**: `GET`
- **URL**: `/api/tasks`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Descripción**: Lista todas las tareas asociadas al usuario autenticado.

#### Buscar tareas por estado o palabra clave
- **Método**: `GET`
- **URL**: `/api/tasks?status=pendiente`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Descripción**: Filtra las tareas por estado (por ejemplo, "pendiente").

- **Método**: `GET`
- **URL**: `/api/tasks?search=reunión`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Descripción**: Filtra las tareas por palabra clave en el título o descripción.

#### Filtrar tareas por fechas
- **Método**: `GET`
- **URL**: `/api/tasks?startDate=2025-04-01&endDate=2025-04-30`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Descripción**: Filtra las tareas dentro de un rango de fechas.

#### Obtener una tarea específica
- **Método**: `GET`
- **URL**: `/api/tasks/1`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Descripción**: Obtiene los detalles de una tarea específica.

#### Actualizar tarea
- **Método**: `PUT`
- **URL**: `/api/tasks/1`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Cuerpo (JSON)**:
    ```json
    {
        "titulo": "Organizar reunión de equipo para planificar el proyecto",
        "estado": "en progreso"
    }
    ```
- **Descripción**: Permite actualizar los detalles de una tarea existente.

#### Eliminar tarea
- **Método**: `DELETE`
- **URL**: `/api/tasks/1`
- **Headers**:
    ```
    Authorization: Bearer <tu_token_jwt>
    ```
- **Descripción**: Elimina una tarea si está marcada como completada.

## Configuración y Uso

1. **Instalar dependencias**: Para instalar todas las dependencias del proyecto, ejecutar el siguiente comando en la raíz del proyecto:
    ```bash
    npm install
    ```

2. **Configuración de la base de datos**: Asegúrate de tener PostgreSQL instalado y crea una base de datos para este proyecto. Luego, configura los parámetros de conexión en el archivo de configuración de Sequelize.

3. **Migraciones**: Ejecuta las migraciones de Sequelize para crear las tablas necesarias en la base de datos:
    ```bash
    npx sequelize-cli db:migrate
    ```

4. **Ejecutar el servidor**: Inicia el servidor localmente con:
    ```bash
    npm start
    ```

   El servidor escuchará en el puerto **4000**.

## Contribuciones

Las contribuciones son bienvenidas. Si deseas contribuir al proyecto, por favor sigue estos pasos:

1. Haz un fork del repositorio.
2. Crea una nueva rama para tu característica (`git checkout -b feature/mi-nueva-caracteristica`).
3. Realiza tus cambios y realiza un commit (`git commit -am 'Añadir nueva característica'`).
4. Empuja tu rama (`git push origin feature/mi-nueva-caracteristica`).
5. Crea un Pull Request.

## Licencia

Este proyecto está licenciado bajo la [Licencia Pública General GNU v3.0](https://www.gnu.org/licenses/gpl-3.0.html).
