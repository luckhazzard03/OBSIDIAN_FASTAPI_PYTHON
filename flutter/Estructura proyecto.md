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

si hago con vysor para poner a correr mi codigo de flutter de vscode como lo haria?


Para usar Vysor para correr tu código de Flutter en un dispositivo Android, sigue estos pasos:

1. **Instala Vysor:**
    
    - **En tu PC:** Descarga e instala Vysor desde su [sitio web oficial](https://www.vysor.io/).
    - **En tu dispositivo Android:** No es necesario instalar nada en el dispositivo para usar Vysor, ya que Vysor funciona como una aplicación de escritorio que proyecta la pantalla del dispositivo en tu computadora.
2. **Configura el dispositivo Android:**
    
    - **Habilita la depuración USB:** Ve a `Ajustes` > `Acerca del teléfono` y toca `Número de compilación` siete veces para activar las `Opciones de desarrollador`. Luego, ve a `Opciones de desarrollador` y habilita `Depuración USB`.
    - **Conecta el dispositivo a tu computadora** usando un cable USB.
3. **Conecta el dispositivo con Vysor:**
    
    - Abre Vysor en tu PC.
    - Deberías ver una opción para conectar un dispositivo. Selecciona tu dispositivo Android de la lista que aparece.
4. **Configura Flutter en VSCode:**
    
    - Asegúrate de tener el SDK de Flutter instalado en tu máquina y que esté configurado correctamente.
    - Abre tu proyecto de Flutter en Visual Studio Code.
    - En VSCode, abre la terminal (puedes usar el atajo `Ctrl + ``) y ejecuta` flutter devices` para asegurarte de que tu dispositivo esté listado. Si no aparece, asegúrate de que el dispositivo esté correctamente conectado y que la depuración USB esté habilitada.
5. **Ejecuta tu aplicación Flutter:**
    
    - En la parte inferior derecha de VSCode, debería aparecer una lista de dispositivos. Selecciona tu dispositivo Android (debería aparecer como un dispositivo físico o algo similar).
    - Puedes iniciar tu aplicación Flutter desde la terminal ejecutando `flutter run` o usando el botón de ejecución en la interfaz de usuario de VSCode.
6. **Verifica la proyección en Vysor:**
    
    - La pantalla de tu dispositivo Android debería estar proyectada en tu PC a través de Vysor. Deberías poder ver y controlar el dispositivo desde la ventana de Vysor.

**Notas adicionales:**

- Asegúrate de que tanto Vysor como tu entorno de desarrollo estén actualizados para evitar problemas de compatibilidad.
- La conexión USB debe ser estable para evitar desconexiones mientras trabajas.

Siguiendo estos pasos, deberías poder correr tu código de Flutter y probarlo en tu dispositivo Android usando Vysor para la proyección de pantalla. ¡Buena suerte con tu desarrollo en Flutter!