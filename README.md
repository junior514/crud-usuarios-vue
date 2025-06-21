CRUD de Usuarios - Vue.js
Una aplicación web moderna desarrollada con Vue.js 3 para la gestión completa de usuarios, implementando operaciones CRUD (Crear, Leer, Actualizar, Eliminar) con una interfaz intuitiva y responsive.
🚀 Características

Listado de usuarios con tabla responsive y datos en tiempo real
Agregar usuarios mediante formularios modales con validación
Editar usuarios existentes con datos precargados
Eliminar usuarios con confirmación de seguridad
Validación de formularios en tiempo real
Loading states para mejor experiencia de usuario
Diseño responsive compatible con dispositivos móviles
Interfaz moderna con Bootstrap 5 y gradientes personalizados

🛠️ Tecnologías Utilizadas

Vue.js 3 - Framework principal con Composition API
Bootstrap 5 - Framework CSS para diseño responsive
Vite - Build tool y servidor de desarrollo
JSONPlaceholder API - API REST para datos de usuarios
HTML5 - Markup semántico
CSS3 - Estilos personalizados y animaciones

📁 Estructura del Proyecto
crud-usuarios-vue/
├── src/
│   ├── components/
│   │   ├── DeleteModal.vue      # Modal de confirmación de eliminación
│   │   ├── LoadingSpinner.vue   # Componente de carga
│   │   ├── UserModal.vue        # Modal para agregar/editar usuarios
│   │   └── UserTable.vue        # Tabla de usuarios
│   ├── App.vue                  # Componente principal
│   └── main.js                  # Punto de entrada de la aplicación
├── package.json
├── vite.config.js
└── README.md
🔧 Instalación y Configuración
Prerrequisitos

Node.js (versión 16 o superior)
npm o yarn

Pasos de instalación

Clonar el repositorio
bashgit clone <url-del-repositorio>
cd crud-usuarios-vue

Instalar dependencias
bashnpm install

Ejecutar en modo desarrollo
bashnpm run dev

Acceder a la aplicación
http://localhost:3000


📋 Funcionalidades Detalladas
Gestión de Usuarios
Listar Usuarios

Carga inicial desde JSONPlaceholder API
Tabla responsive con información completa
Estados de carga visual
Contador de usuarios en tiempo real

Agregar Usuario

Formulario modal con validación
Campos requeridos: nombre, usuario, email, teléfono
Validación de formato de email
Generación automática de ID secuencial

Editar Usuario

Formulario precargado con datos existentes
Actualización en tiempo real del array local
Validaciones consistentes con el formulario de creación

Eliminar Usuario

Modal de confirmación antes de eliminar
Eliminación del array local
Feedback visual inmediato

Validaciones Implementadas

Campos obligatorios: Todos los campos son requeridos
Formato de email: Validación con expresión regular
Feedback visual: Indicadores de error en tiempo real
Estado del formulario: Botón de guardar habilitado solo con datos válidos

🎨 Diseño y UX
Características Visuales

Gradientes modernos en header y botones
Cards con sombras para mejor jerarquía visual
Modales centrados para formularios y confirmaciones
Estados hover en elementos interactivos
Iconografía consistente con Bootstrap Icons

Responsive Design

Formularios adaptables a diferentes tamaños de pantalla
Tabla responsive con scroll horizontal en móviles
Botones y espaciados optimizados para touch

🔄 API Integration
La aplicación consume la API pública de JSONPlaceholder:
javascriptGET https://jsonplaceholder.typicode.com/users
Nota: Las operaciones de creación, edición y eliminación se realizan únicamente en el estado local de la aplicación, manteniendo la persistencia durante la sesión.
📱 Componentes
App.vue
Componente principal que maneja:

Estado global de usuarios
Coordinación entre componentes
Lógica de negocio principal

UserTable.vue

Renderizado de tabla de usuarios
Eventos de edición y eliminación
Diseño responsive

UserModal.vue

Formulario modal reutilizable
Validaciones en tiempo real
Manejo de estados de edición/creación

DeleteModal.vue

Confirmación de eliminación
Información del usuario a eliminar
Acciones de confirmación/cancelación

LoadingSpinner.vue

Indicador de carga personalizado
Animación suave
Estado centralizado

🚀 Scripts Disponibles
bash# Servidor de desarrollo
npm run dev

# Build para producción
npm run build

# Preview del build
npm run preview
🔮 Mejoras Futuras

 Implementación de paginación
 Filtros y búsqueda avanzada
 Persistencia de datos con localStorage
 Integración con API real para operaciones CRUD
 Testing unitario con Jest
 Implementación de rutas con Vue Router
 Estado global con Pinia/Vuex

🤝 Contribución
Las contribuciones son bienvenidas. Para cambios importantes:

Fork el proyecto
Crea una rama para tu feature (git checkout -b feature/AmazingFeature)
Commit tus cambios (git commit -m 'Add: Amazing Feature')
Push a la rama (git push origin feature/AmazingFeature)
Abre un Pull Request
