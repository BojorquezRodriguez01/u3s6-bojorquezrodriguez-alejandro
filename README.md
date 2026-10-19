# 🚀 APLICAWEB - Semana 6: Autenticación, Sesiones y Aislamiento de Datos

**Estudiante:** Alejandro Bojórquez Rodríguez  
**Proyecto:** Sistema CRUD de Servicios con Django y MySQL en Aiven  
**Despliegue:** [https://u3s6-bojorquezrodriguez-alejandro.onrender.com](https://u3s6-bojorquezrodriguez-alejandro.onrender.com)

---

## 📋 Descripción de la Práctica

En esta sexta semana de la materia **APLICAWEB**, se implementó un sistema completo de autenticación de usuarios, gestión de sesiones seguras e integración de lógica de aislamiento de datos (*multitenancy* básico) sobre el CRUD desarrollado anteriormente. 

Cada usuario registrado interactúa exclusivamente con sus propios datos, garantizando la privacidad y seguridad a nivel de base de datos y vistas.

---

## 🛠️ Tecnologías Utilizadas

* **Framework:** Django 5.x (Python 3.14)
* **Base de Datos:** MySQL hospedado en **Aiven** (con conexión cifrada SSL)
* **Estilos:** HTML5 + Tailwind CSS (vía Play CDN)
* **Autenticación:** `django.contrib.auth` (`UserCreationForm`, `AuthenticationForm`, `@login_required`)
* **Servidor de Producción / Hosting:** Render (Gunicorn + WhiteNoise)

---

## ✨ Características Principales

1. **Gestión de Cuentas de Usuario:**
   * **Registro (`/registro/`):** Creación de nuevos usuarios con validación de contraseñas seguras y hashing PBKDF2 directo en la base de datos.
   * **Inicio de Sesión (`/login/`):** Autenticación mediante cookies de sesión.
   * **Cierre de Sesión (`/logout/`):** Invalidación de la sesión activa del usuario.

2. **Aislamiento de Datos por Usuario:**
   * **Filtrado en Listado:** La consulta en la base de datos se realiza con `.filter(propietario=request.user)`, permitiendo que cada usuario vea únicamente los servicios que creó.
   * **Asignación Automática:** Al crear un servicio (`/servicios/nuevo/`), el propietario se asigna automáticamente usando `request.user`.

3. **Seguridad y Control de Acceso:**
   * **Protección de Vistas:** Decoradores `@login_required` para impedir el acceso directo por URL a usuarios no autenticados.
   * **Candado en Edición y Borrado:** Verificación en vistas de actualización y eliminación mediante `get_object_or_404(Servicio, pk=pk, propietario=request.user)`, devolviendo un error **404 Not Found** si un usuario intenta alterar o eliminar el registro de otro usuario.

4. **Interfaz
