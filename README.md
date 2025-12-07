# InstaDAM - Red Social con Arquitectura Empresarial

**Descripción del proyecto**
InstaDAM es una aplicación móvil tipo Instagram desarrollada con Flutter y Firebase, que implementa una **arquitectura de base de datos empresarial completa** con normalización, historial de cambios (soft-delete mediante high_date/low_date), y estructura relacional avanzada, superando los requisitos mínimos del proyecto.

- Colecciones principales implementadas:
  1. "users" - Usuarios del sistema
  2. "user_addresses" - Direcciones de usuarios
  3. "countries", "provinces", "populations", "post_codes" - Sistema geográfico completo
  4. "user_logins" - Historial de conexiones
  5. "user_conditions" - Aceptación de términos legales
  6. "user_profiles_pictures" - Historial de fotos de perfil
  7. posts - Publicaciones principales
  8. post_pictures - Historial de imágenes del post
  9. post_likes - Sistema de likes con historial
  10. post_comments - Comentarios con respuestas anidadas
  11. user_followers - Sistema de seguimiento
  12. post_types - Tipos de publicación (opcional)

**Instalación**
- Dependencias Flutter
  dependencies:
  flutter:
      sdk: flutter
    firebase_core: ^2.24.2
    firebase_auth: ^4.13.0
    cloud_firestore: ^4.13.0
    firebase_storage: ^11.5.0
    cloud_functions: ^4.6.0  # Para triggers y lógica compleja
    image_picker: ^1.0.4
    shared_preferences: ^2.2.2
    provider: ^6.1.1
    intl: ^0.18.1  # Para fechas y formatos
    cached_network_image: ^3.3.0  # Para imágenes
    uuid: ^3.0.7  # Para generar IDs únicos

  - Crear proyecto en Firebase Console
      1. Añadir app Flutter (Android/iOS)
      2. Descargar archivos de configuración
      3. Habilitar:
        - Authentication (Email/Password)
        - Firestore Database (modo de prueba)
       -Storage
      4. Configurar reglas de seguridad (ver sección siguiente)

**Estructura del proyecto (REVISAR 100%)**
lib/
├── main.dart                          # Punto de entrada
├── config/
│   ├── firebase_config.dart           # Configuración Firebase
│   └── app_constants.dart             # Constantes globales
├── models/                            # Modelos de datos
│   ├── user/
│   │   ├── user_model.dart            # Modelo User
│   │   ├── user_address_model.dart    # Modelo UserAddress
│   │   ├── user_login_model.dart      # Modelo UserLogin
│   │   └── user_conditions_model.dart # Modelo UserConditions
│   ├── geographic/                    # Modelos geográficos
│   │   ├── country_model.dart
│   │   ├── province_model.dart
│   │   ├── population_model.dart
│   │   └── post_code_model.dart
│   ├── post/
│   │   ├── post_model.dart
│   │   ├── post_picture_model.dart
│   │   ├── post_like_model.dart
│   │   ├── post_comment_model.dart
│   │   └── post_type_model.dart
│   └── relationship/
│       └── user_follower_model.dart
├── services/                          # Servicios Firebase
│   ├── auth_service.dart              # Autenticación
│   ├── firestore_service.dart         # Operaciones Firestore
│   ├── storage_service.dart           # Almacenamiento de imágenes
│   ├── geographic_service.dart        # Servicio geográfico (países, etc.)
│   └── preferences_service.dart       # SharedPreferences
├── screens/                           # Pantallas
│   ├── auth/
│   │   ├── login_screen.dart
│   │   └── register_screen.dart
│   ├── main/
│   │   ├── feed_screen.dart
│   │   ├── post_detail_screen.dart
│   │   ├── create_post_screen.dart
│   │   ├── profile_screen.dart
│   │   └── settings_screen.dart
│   └── geographic/                    # Pantallas geográficas (opcionales)
│       ├── country_selection.dart
│       └── address_management.dart
├── widgets/                           # Widgets reutilizables
│   ├── post/
│   │   ├── post_card.dart
│   │   ├── like_button.dart
│   │   └── comment_section.dart
│   ├── user/
│   │   ├── user_avatar.dart
│   │   └── profile_header.dart
│   └── geographic/
│       ├── address_form.dart
│       └── location_picker.dart
├── utils/                             # Utilidades
│   ├── validators.dart                # Validación de formularios
│   ├── date_formatter.dart            # Formateo de fechas
│   ├── image_picker_helper.dart       # Helper para imágenes
│   └── firebase_helpers.dart          # Helpers para Firestore
└── providers/                         # State Management (Provider)
    ├── auth_provider.dart
    ├── post_provider.dart
    ├── user_provider.dart
    └── theme_provider.dart


/ 

lib/
├── main.dart
├── models/
│   ├── user.dart
│   ├── post.dart
│   ├── comment.dart
│   └── like.dart
├── screens/
│   ├── login_screen.dart
│   ├── feed_screen.dart
│   ├── create_post_screen.dart
│   ├── profile_screen.dart
│   └── settings_screen.dart
└── services/
    ├── auth_service.dart
    └── firestore_service.dart

**Funcionalidades implementadas**
- Login/Registro: Con opción "Recordar usuario" (SharedPreferences)
- Feed: Muestra posts con imagen, usuario, descripción, fecha, likes y comentarios
- Likes: Dar/quitar like, actualiza en tiempo real
- Crear posts: Seleccionar imagen y añadir descripción
- Comentarios: Añadir y ver comentarios por post
- Perfil: Ver perfil y posts propios
- Ajustes: Tema claro/oscuro, idioma, cerrar sesión

La app usa Firebase Auth, Firestore y Storage. Los datos del usuario se guardan en SharedPreferences.
