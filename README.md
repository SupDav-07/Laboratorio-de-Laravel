# Laboratorio de Laravel: Login y Registro

📅 Fecha: [28/10/2026]

## 📄 Contenido del Repositorio

Este repositorio contiene un proyecto desarrollado con el framework Laravel, correspondiente a la unidad "Patrón MVC" del curso de Desarrollo Web. Incluye la instalación y configuración de Laravel, la conexión con una base de datos MySQL mediante migraciones, y un sistema de **autenticación** (registro de usuarios, inicio y cierre de sesión) generado con el paquete `laravel/ui` y Bootstrap.

## 🛠️ Tecnologías Utilizadas

- **Lenguaje:** PHP 8.3.28
- **Framework:** Laravel [versión: verificar con `php artisan --version`]
- **Autenticación y front-end:** `laravel/ui` con Bootstrap
- **Compilador de assets:** Vite (Node.js y npm)
- **Gestor de dependencias:** Composer
- **Servidor local:** WampServer 3.4.0 (Apache 2.4.65)
- **Base de datos:** MySQL / MariaDB (incluidas en WampServer)
- **Editor:** Visual Studio Code
- **Control de versiones:** Git / GitHub

## 🖥️ Capturas de Pantalla y Problemas

### Interfaz Principal

- **Creación del proyecto (`laravel new` / `composer create-project`):** se crea el proyecto `Proyecto2026` dentro de `C:\wamp64\www\`.
  <img width="2180" height="925" alt="Screenshot 2026-10-28 174823" src="https://github.com/user-attachments/assets/4193edeb-7b58-40fd-8b35-13af23249971" />


- **Configuración del `.env` y migraciones (`php artisan migrate`):** se configuran las credenciales de la base de datos y se ejecutan las migraciones para crear las tablas `users`, `cache` y `jobs`.
  <img width="921" height="561" alt="image" src="https://github.com/user-attachments/assets/575b8d75-3282-4ec2-9b46-01738c817ee3" />
  <img width="921" height="459" alt="image" src="https://github.com/user-attachments/assets/e360b440-02ef-4dd8-80c3-e27a81dc2122" />



- **Instalación del paquete de autenticación (`composer require laravel/ui` y `php artisan ui bootstrap --auth`):** se genera el scaffolding de Bootstrap junto con las vistas de login, registro y restablecimiento de contraseña.
  <img width="921" height="853" alt="image" src="https://github.com/user-attachments/assets/09b0bfba-3995-4737-bb03-4f1958634725" />

  <img width="921" height="671" alt="image" src="https://github.com/user-attachments/assets/b6e7d3f9-8507-466c-b811-83e4a456f604" />



- **Dependencias de Node y servidor de desarrollo (`npm install` y `composer run dev`):** se instalan las dependencias de front-end y se levantan juntos el servidor, la cola y Vite.
  <img width="717" height="173" alt="image" src="https://github.com/user-attachments/assets/142440b4-e27b-47cb-b4c9-a1887cda4822" />
  <img width="921" height="787" alt="image" src="https://github.com/user-attachments/assets/c50fc15e-c36a-4237-9e25-0cab6aa70ab7" />



- **Pantalla de registro (`/register`):** formulario para crear un usuario con nombre, correo y contraseña.
  <img width="921" height="347" alt="image" src="https://github.com/user-attachments/assets/36306458-04c1-43e7-8c12-cca8a7403aac" />


- **Pantalla de login (`/login`):** formulario de inicio de sesión con correo y contraseña.
  <img width="921" height="302" alt="image" src="https://github.com/user-attachments/assets/77f8aa62-b1c3-448c-bc7e-dfcb5461075d" />


- **Panel del usuario (`/home`):** vista protegida que se muestra solo después de iniciar sesión, con mensaje de bienvenida y botón de **cerrar sesión**.
  <img width="921" height="315" alt="image" src="https://github.com/user-attachments/assets/389dd976-b350-45d0-8260-1ded52d578ad" />

- **Usuario guardado en la base de datos (phpMyAdmin):** registro creado en la tabla `users`.
  <img width="3355" height="1285" alt="Screenshot 2026-10-30 091619" src="https://github.com/user-attachments/assets/75d772ea-2445-4afd-ba16-2ffc50f79ac6" />

### Problemas encontrados y soluciones

- **Versión de PHP incorrecta en la terminal:** la terminal usaba PHP 8.0.30 y Laravel 12 requiere PHP 8.2 o superior. Se solucionó cambiando la entrada de PHP en las variables de entorno (Path) a `C:\wamp64\bin\php\php8.3.28` y reiniciando la terminal.
- **Carpeta `vendor` inexistente:** los comandos de `php artisan` fallaban con el error `Failed opening required ... vendor/autoload.php`. Se solucionó ejecutando `composer install` (o creando un proyecto nuevo con la versión de PHP correcta).
- **Menú de usuario que no se desplegaba:** la opción **Logout** de la barra superior no se abría. Como solución, se agregó un botón de cierre de sesión directamente en `resources/views/home.blade.php`, usando un formulario con método `POST` y el token `@csrf`.

## 📁 Estructura de Carpetas o Directorios

```
Proyecto2026/
├── app/
│   ├── Http/
│   │   └── Controllers/
│   │       ├── Auth/               # Controladores de login, registro y contraseña (laravel/ui)
│   │       └── HomeController.php  # Controlador del panel del usuario
│   ├── Models/
│   │   └── User.php                # Modelo de usuario
│   └── Providers/
│       └── AppServiceProvider.php  # Configuración de longitud de cadena (Schema::defaultStringLength)
├── database/
│   └── migrations/                 # Migraciones: users, cache y jobs
├── resources/
│   ├── js/                         # JavaScript (Bootstrap)
│   ├── sass/                       # Estilos (Bootstrap)
│   └── views/
│       ├── auth/                   # Vistas de login, registro y recuperación de contraseña
│       ├── layouts/
│       │   └── app.blade.php       # Plantilla principal con la barra de navegación
│       └── home.blade.php          # Panel del usuario con botón de cerrar sesión
├── routes/
│   └── web.php                     # Rutas de la aplicación (incluye Auth::routes())
├── .env.example                    # Plantilla de variables de entorno
├── composer.json                   # Dependencias de PHP
├── package.json                    # Dependencias de Node.js
└── README.md                       # Documentación del proyecto
```

## ▶️ Instrucciones de Ejecución / Uso

1. Clonar el repositorio.
2. Copiar la carpeta del proyecto dentro de `C:\wamp64\www\` (o la carpeta `htdocs` de tu servidor local).
3. Iniciar WampServer y verificar que Apache y MySQL estén activos (ícono en verde). Verificar con `php -v` que la terminal use PHP 8.2 o superior.
4. Abrir una terminal dentro de la carpeta del proyecto e instalar las dependencias:
   ```bash
   composer install
   npm install
   ```
5. Crear el archivo de variables de entorno y generar la clave de la aplicación:
   ```bash
   copy .env.example .env
   php artisan key:generate
   ```
6. Editar el archivo `.env` con los datos de la base de datos:
   ```env
   DB_CONNECTION=mysql
   DB_HOST=127.0.0.1
   DB_PORT=3306
   DB_DATABASE=pruebaregistrolaravel
   DB_USERNAME=root
   DB_PASSWORD=
   ```
7. Limpiar la caché de configuración y ejecutar las migraciones:
   ```bash
   php artisan config:clear
   php artisan config:cache
   php artisan migrate
   ```
8. Levantar el servidor de desarrollo:
   ```bash
   composer run dev
   ```
9. Abrir el navegador y acceder a:
   - `http://127.0.0.1:8000` (página de bienvenida)
   - `http://127.0.0.1:8000/register` (registro de usuarios)
   - `http://127.0.0.1:8000/login` (inicio de sesión)
   - `http://127.0.0.1:8000/home` (panel del usuario, requiere sesión iniciada)

> **Nota:** el archivo `.env` y las carpetas `vendor` y `node_modules` no se suben al repositorio, por eso es necesario generarlos con los pasos anteriores.

## 👤 Autor y Contexto

- **Nombre:** René Gaitán
- **Cedula:** 20-53-8703
- **Institución:** Universidad Tecnológica de Panamá (UTP)
- **Curso:** Desarrollo Web
- **Docente:** Ing. Irina Fong
- **Fecha de Realización:** [28/10/2026]

## 🔗 Referencias

- Guía de Laboratorio: "Cómo crear un Login y Registro en Laravel" (Ing. Irina Fong, Patrón MVC)
- Documentación oficial de Laravel: https://laravel.com/docs/12.x
- Paquete `laravel/ui`: https://github.com/laravel/ui
