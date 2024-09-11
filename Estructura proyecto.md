#Flutter #estructuraProyect

```c
lib
├───controllers
│   ├───login_controller.dart
│   ├───order_controller.dart
│   └───user_controller.dart
├───models
│   ├───user.dart
│   ├───order.dart
│   └───login.dart
├───pages
│   ├───login_page.dart
│   ├───order_page.dart
│   └───user_list_page.dart
├───services
│   ├───user_service.dart
│   ├───order_service.dart
│   └───auth_service.dart
└───utils
    ├───constants.dart
    └───helpers.dart

```


Para manejar las dependencias en un proyecto Flutter desde la terminal, sigues estos pasos básicos:

1. **Abrir la Terminal**:
    
    - Abre la terminal en tu entorno de desarrollo (ya sea la terminal integrada en tu editor o una terminal externa).
2. **Agregar Dependencias**:
    
    - Usa el comando `flutter pub add` para agregar nuevas dependencias. Este comando se encarga de modificar tu archivo `pubspec.yaml` y descargar los paquetes necesarios.
    
    Aquí están los comandos específicos para agregar las dependencias que mencionaste (`json_annotation`, `build_runner`, y `json_serializable`):

```c
flutter pub add json_annotation
flutter pub add build_runner --dev
flutter pub add json_serializable --dev
```

**Actualizar Dependencias**:

- Después de agregar las dependencias, puedes usar el comando `flutter pub get` para descargar las nuevas dependencias y actualizarlas en tu proyecto.
```c
flutter pub get
```


**Generar Código con `build_runner`**:

- Una vez que hayas agregado las dependencias necesarias, ejecuta el siguiente comando para generar el código automáticamente para la serialización JSON.
```c
flutter pub run build_runner build
```


### Configuración de `json_serializable`

Para que este modelo funcione correctamente, debes asegurarte de que el paquete `json_serializable` esté incluido en tu archivo `pubspec.yaml` y luego ejecutar el comando para generar los archivos necesarios.

**Archivo `pubspec.yaml`:**

```c
dependencies:
  flutter:
    sdk: flutter
  json_annotation: ^4.8.0

dev_dependencies:
  flutter_test:
    sdk: flutter
  build_runner: ^2.3.0
  json_serializable: ^6.4.0

```

