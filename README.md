# 📚 Frontend CRUD de Libros

Aplicación web moderna para la gestión de libros (CRUD completo) desarrollada con Vue 3, Vite y desplegada en AWS S3.

## 🚀 Características

- ✨ **CRUD Completo**: Crear, Leer, Actualizar y Eliminar libros
- 🎨 **Interfaz Moderna**: Diseño responsive y amigable
- ⚡ **Vue 3 + Vite**: Desarrollo rápido con HMR (Hot Module Replacement)
- 📦 **Pinia**: Gestión de estado moderna para Vue
- 🛣️ **Vue Router**: Navegación SPA (Single Page Application)
- 🌐 **Axios**: Cliente HTTP para conexión con API REST
- ☁️ **AWS S3**: Infraestructura de despliegue con Terraform

## 🛠️ Tecnologías

- **Vue 3** (^3.5.18) - Framework JavaScript progresivo
- **Vite** (^7.0.6) - Build tool y dev server
- **Pinia** (^3.0.3) - State management
- **Vue Router** (^4.5.1) - Enrutamiento
- **Axios** (^1.11.0) - Cliente HTTP
- **Terraform** - Infraestructura como código (IaC)

## 📋 Prerequisitos

- Node.js (versión 18 o superior)
- npm o yarn
- Terraform (para despliegue en AWS)
- Cuenta de AWS (para despliegue)

## 🔧 Instalación

1. **Clonar el repositorio**
```bash
git clone <url-del-repositorio>
cd frontend-crud
```

2. **Instalar dependencias**
```bash
npm install
```

3. **Configurar variables de entorno**

Copia el archivo de ejemplo y configura tus variables:
```bash
cp .env.example .env
```

O crea manualmente un archivo `.env` en la raíz del proyecto con el siguiente contenido:
```env
# API Configuration
VITE_API_URL=http://localhost:8080/api

# Environment
NODE_ENV=development
```

**Nota:** Asegúrate de que la URL de tu API backend esté correctamente configurada en `VITE_API_URL`.

## 💻 Desarrollo

### Iniciar servidor de desarrollo
```bash
npm run dev
```
La aplicación estará disponible en `http://localhost:5173`

### Compilar para producción
```bash
npm run build
```

### Vista previa de build de producción
```bash
npm run preview
```

## 🌟 Estructura del Proyecto

```
frontend-crud/
├── public/              # Archivos estáticos
│   └── favicon.ico
├── src/
│   ├── assets/         # CSS y recursos
│   │   ├── base.css
│   │   ├── main.css
│   │   └── logo.svg
│   ├── components/     # Componentes reutilizables
│   │   ├── HelloWorld.vue
│   │   ├── TheWelcome.vue
│   │   ├── WelcomeItem.vue
│   │   └── icons/
│   ├── router/         # Configuración de rutas
│   │   └── index.js
│   ├── stores/         # Pinia stores
│   │   └── counter.js
│   ├── views/          # Vistas/Páginas
│   │   ├── AboutView.vue
│   │   ├── BooksView.vue
│   │   └── HomeView.vue
│   ├── App.vue         # Componente raíz
│   └── main.js         # Punto de entrada
├── terraform/          # Infraestructura AWS
│   └── main.tf
├── .env                # Variables de entorno (no versionado)
├── .env.example        # Plantilla de variables de entorno
├── .gitignore          # Archivos ignorados por Git
├── index.html
├── vite.config.js
└── package.json
```

## 📚 Componentes Principales

### BooksView.vue
Vista principal que implementa el CRUD de libros con:
- Formulario para crear/editar libros
- Tabla con listado de libros
- Operaciones CRUD (Create, Read, Update, Delete)
- Validación de formularios
- Diseño responsive

## 🚢 Despliegue en AWS S3

Este proyecto incluye configuración de Terraform para despliegue automático en AWS S3.

### 1. Configurar credenciales de AWS
```bash
cd terraform
```

### 2. Inicializar Terraform
```bash
terraform init
```

### 3. Planificar despliegue
```bash
terraform plan
```

### 4. Aplicar cambios
```bash
terraform apply
```

### 5. Desplegar con GitHub Pages (alternativa)
```bash
npm run deploy
```

## 🔌 API Backend

La aplicación requiere un backend con los siguientes endpoints:

- `GET /api/books` - Obtener todos los libros
- `POST /api/books` - Crear un libro
- `PUT /api/books/:id` - Actualizar un libro
- `DELETE /api/books/:id` - Eliminar un libro

### Modelo de Libro
```javascript
{
  id: Number,
  title: String,
  author: String,
  year: Number,
  price: Number,
  stock: Number,
  description: String
}
```

## 🎨 Configuración IDE Recomendada

- [VSCode](https://code.visualstudio.com/)
- [Volar](https://marketplace.visualstudio.com/items?itemName=Vue.volar) (desactivar Vetur)
- [Vue DevTools](https://devtools.vuejs.org/)

### Extensiones VSCode Recomendadas
- Vue - Official (Volar)
- ESLint
- Prettier

## 📝 Scripts Disponibles

```bash
npm run dev      # Inicia servidor de desarrollo
npm run build    # Compila para producción
npm run preview  # Vista previa de build
npm run deploy   # Despliega en GitHub Pages
```

## 🤝 Contribuir

1. Fork el proyecto
2. Crea una rama para tu feature (`git checkout -b feature/AmazingFeature`)
3. Commit tus cambios (`git commit -m 'Add some AmazingFeature'`)
4. Push a la rama (`git push origin feature/AmazingFeature`)
5. Abre un Pull Request

## 📄 Licencia

Este proyecto es privado y está bajo derechos reservados.

## 👤 Autor

**Henry Vega**

## 🐛 Reporte de Bugs

Si encuentras algún bug, por favor abre un issue en el repositorio.

## 📞 Soporte

Para soporte, contacta al equipo de desarrollo.

---

⭐ Si te gusta este proyecto, dale una estrella en GitHub!

