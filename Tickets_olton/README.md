# Tickets_olton
#  Sistema de Gestión de Tickets (Tickets Olton)

Este proyecto consta de dos partes principales:
1. **Backend (Django)**: Un servidor web que gestiona los tickets, perfiles de usuario, autenticación mediante tokens de sesión y almacenamiento de archivos/imágenes.
2. **Aplicación Móvil (Android)**: Una app nativa desarrollada en Java que se conecta al backend para crear, visualizar, editar y eliminar tickets, incluyendo captura de fotos con la cámara y selección desde galería.

---

##  1. Backend (Django)

El backend utiliza Django como framework web y SQLite como base de datos por defecto.

### Requisitos Previos
* **Python 3.8 o superior** instalado en el sistema.
* **Gestor de paquetes pip**.

### Pasos para la Configuración y Ejecución

1. **Clonar o acceder al directorio del proyecto** y entrar en la carpeta del backend:
   ```bash
   cd proyecto
   ```

2. **Crear un Entorno Virtual de Python**:
   ```bash
   python -m venv venv
   ```

3. **Activar el Entorno Virtual**:
   * **En Windows (PowerShell)**:
     ```powershell
     .\venv\Scripts\Activate.ps1
     ```
   * **En Windows (CMD)**:
     ```cmd
     .\venv\Scripts\activate.bat
     ```
   * **En macOS/Linux**:
     ```bash
     source venv/bin/activate
     ```

4. **Instalar dependencias necesarias**:
   ```bash
   pip install django bcrypt pillow
   ```
   *(Nota: `pillow` es requerido por Django para el manejo y validación de campos de archivos de imagen, y `bcrypt` se utiliza para la encriptación segura de contraseñas)*.

5. **Realizar migraciones de la Base de Datos**:
   ```bash
   python manage.py makemigrations
   ```
   ```bash
   python manage.py migrate
   ```

6. **Crear un Administrador (Opcional - para panel de Django)**:
   ```bash
   python manage.py createsuperuser
   ```

7. **Ejecutar el Servidor**:
   ```bash
   python manage.py runserver 0.0.0.0:8000
   ```
   *El backend estará disponible en `http://localhost:8000/` para la versión web y expuesto en tu red local.*

---

##  2. Aplicación Móvil (Android)

La aplicación de Android está configurada para comunicarse de manera local y en red con el servidor Django.

### Requisitos Previos
* **Android Studio** (Koala o versión moderna).
* Un emulador Android o un dispositivo físico configurado con Depuración USB activa.

### Pasos para la Configuración y Ejecución

1. **Abrir el proyecto en Android Studio**:
   * Selecciona **File > Open** y elige el directorio `tickets_android`.
   * Deja que Gradle sincronice las dependencias del proyecto de forma automática.

2. **Configurar la URL de Conexión**:
   * Abre el archivo: `tickets_android/app/src/main/java/com/example/tickets_android/Conexiones.java`.
   * Configura la constante `BASE_URL`:
     * **Si usas Emulador Android**: Déjalo como está (`http://10.0.2.2:8000`), ya que `10.0.2.2` es el alias que usa el emulador para referenciar al `localhost` de tu ordenador.
     * **Si usas un Dispositivo Físico**: Cambia el valor por la dirección IP de tu ordenador en la red local (ejemplo: `http://192.168.1.50:8000`). Asegúrate de que el móvil y el ordenador estén conectados a la misma red Wi-Fi.

3. **Ejecutar la App**:
   * Conecta tu dispositivo o inicia el emulador.
   * Presiona el botón de **Run (Flecha verde)** en Android Studio.

---

##  Tecnologías y Características Destacadas
* **Autenticación Basada en Tokens**: Cada usuario registrado tiene un token de sesión dinámico e individual almacenado en la base de datos y administrado en Android mediante `SharedPreferences`.
* **Subida y Compresión de Archivos**: Al adjuntar una imagen de ticket (cámara o galería), la aplicación comprime la foto automáticamente a JPEG con calidad 80 antes de enviarla mediante peticiones `multipart/form-data` con Volley, evitando desbordamientos de memoria (OutOfMemory) y acelerando la subida.
* **Diseño Premium y Responsive**: Layouts mejorados mediante contenedores con soporte para scroll, evitando solapamiento de botones o campos en pantallas de cualquier resolución.
* **Panel de Control Django**: Puedes acceder a `http://localhost:8000/admin/` desde el navegador para administrar usuarios, empresas y tickets creados de forma visual.
