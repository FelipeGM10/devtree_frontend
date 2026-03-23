# DevTree
La aplicación DevTree es un clon de Linktree, diseñada para centralizar todos los enlaces de redes sociales de un usuario en un solo perfil. Cuyos objetivos serán:

1. Concentrar Redes Sociales: Permite a los usuarios crear un perfil donde pueden subir una imagen, escribir una descripción y agregar enlaces a sus diferentes redes sociales.
2. Interacción y Registro de Usuarios: DevTree permite a cualquier usuario registrarse y gestionar su información. Cada usuario puede tener su propio "Dev Tree" donde organizan sus enlaces.
3. Validaciones de Usuario: La aplicación implementa validaciones para asegurarse de que los nombres de usuario (handles) sean únicos, evitando conflictos en la identificación de usuarios, similar a plataformas como Instagram o Twitter.
4. Interfaz Pública y Privada: Ofrece tanto una interfaz pública donde los enlaces pueden ser compartidos como una interfaz privada para que los usuarios puedan gestionar sus propios perfiles, habilitar o deshabilitar enlaces, y reorganizar la presentación de sus redes.
5. Gestión de Enlaces: Los usuarios pueden actualizar, eliminar o agregar enlaces, y se asegura que estos cambios se reflejen en tiempo real.

# DevTree Frontend

Frontend de DevTree, una aplicación para crear una página pública tipo link-in-bio donde cada usuario puede centralizar sus redes sociales y compartirlas desde una sola URL.

Este proyecto está construido con React, TypeScript y Vite, y consume una API para autenticación, gestión de perfil, carga de imagen y publicación del árbol de enlaces.

## Características

- Registro e inicio de sesión de usuarios.
- Búsqueda y validación de disponibilidad de `handle`.
- Panel privado para editar perfil, descripción e imagen.
- Configuración de enlaces sociales habilitados o deshabilitados.
- Reordenamiento de enlaces mediante drag and drop.
- Vista pública por `/:handle` para compartir el perfil.
- Manejo de estado remoto con React Query.
- Notificaciones visuales con Sonner.

## Stack tecnológico

- React 18
- TypeScript
- Vite
- Tailwind CSS
- React Router DOM
- TanStack React Query
- React Hook Form
- Axios
- DnD Kit
- Headless UI

## Requisitos

- Node.js 18 o superior
- npm 9 o superior
- API backend de DevTree disponible y accesible

## Variables de entorno

Crear un archivo `.env.local` en la raíz del frontend:

```bash
VITE_API_URL=http://localhost:4000
```

`VITE_API_URL` define la URL base de la API que este frontend consume.

## Instalación

```bash
npm install
```

## Ejecución en desarrollo

```bash
npm run dev
```

La aplicación quedará disponible en la URL local que indique Vite, normalmente `http://localhost:5173`.

## Scripts disponibles

```bash
npm run dev
npm run build
npm run preview
npm run lint
```

- `dev`: inicia el servidor de desarrollo.
- `build`: compila TypeScript y genera el build de producción.
- `preview`: levanta una vista previa local del build generado.
- `lint`: ejecuta ESLint sobre el proyecto.

## Flujo principal de la aplicación

### Público

- `/` muestra la landing principal.
- El formulario de búsqueda permite validar un `handle` antes del registro.
- `/:handle` renderiza la página pública del usuario con sus enlaces activos.

### Autenticación

- `/auth/register` crea una cuenta.
- `/auth/login` autentica al usuario y guarda el token en `localStorage` como `AUTH_TOKEN`.

### Panel privado

- `/admin` permite activar, desactivar, editar y reordenar enlaces sociales.
- `/admin/profile` permite editar `handle`, descripción e imagen de perfil.

## Integración con la API

El frontend espera una API compatible con estos endpoints:

- `POST /auth/register`
- `POST /auth/login`
- `GET /user`
- `PATCH /user`
- `POST /user/image`
- `POST /search`
- `GET /:handle`

Las peticiones autenticadas envían automáticamente el token Bearer desde `localStorage`.

## Estructura principal

```text
src/
  api/          # Funciones para consumir la API
  components/   # Componentes reutilizables de UI
  config/       # Configuración de Axios
  data/         # Datos estáticos, como redes sociales disponibles
  layouts/      # Layouts para autenticación y panel privado
  views/        # Pantallas principales
  router.tsx    # Definición de rutas
```

## Build de producción

```bash
npm run build
```

Los archivos listos para despliegue se generan en `dist/`.

El proyecto incluye `public/_redirects`, lo que facilita el soporte de rutas del lado del cliente en despliegues tipo Netlify.

## Notas

- Este frontend depende de que el backend esté operativo.
- Actualmente el proyecto incluye linting, pero no una suite de tests automatizados configurada en este paquete.
