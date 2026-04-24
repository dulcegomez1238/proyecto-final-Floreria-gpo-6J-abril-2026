¡Hola! Es un proyecto ambicioso y bien estructurado. Vamos a configurar la arquitectura **.agents** para tu florería, asegurándonos de que cada "habilidad" (diseño, código, scraping) tenga su lugar mientras levantamos el CRUD de empleados en Flutter.

Sigue esta secuencia lógica para preparar tu entorno y generar el código base.

---

## 1. Estructura de la Habilidad Agente Global: `.agents`

Primero, definimos la jerarquía de carpetas para que tu agente tenga contexto de sus herramientas.

```text
proyectofloreria/
├── .agents/
│   ├── SKILL.md            # Definición de capacidades del agente
│   ├── scripts/            # Automatizaciones (bash/python)
│   ├── ejemplos/           # Snippets de código de referencia
│   └── resources/          # Activos, iconos y documentación
├── lib/                    # Código fuente Flutter
├── assets/                 # Recursos de la florería
└── pubspec.yaml
```

### SKILL.md (Resumen)
> **Agente:** Florería Global
> **Skills:** > - **Diseño:** UI/UX minimalista para venta de flores.
> - **Código:** Arquitectura limpia en Dart/Flutter.
> - **Scraping:** Obtención de precios de competidores (automatización).

---

## 2. Prerrequisitos y Verificación de Entorno

Antes de tocar el código, aseguremos que el motor está encendido. Ejecuta estos comandos en tu terminal (VS Code o Antigravity):

### Verificación de Herramientas
```bash
# 1. Verificar Flutter
flutter --version

# 2. Instalar FlutterFire CLI (si no lo tienes)
dart pub global activate flutterfire_cli

# 3. Login en Firebase
firebase login

# 4. Configurar el proyecto en la carpeta raíz
flutterfire configure
```

> **Nota:** Al ejecutar `flutterfire configure`, selecciona tu proyecto de Firebase creado previamente y elige la plataforma **Android**. Esto generará automáticamente el archivo `firebase_options.dart`.

---

## 3. Configuración del Proyecto (`pubspec.yaml`)

Asegúrate de tener estas dependencias para que Firestore funcione:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: ^2.x.x
  cloud_firestore: ^4.x.x
  cupertino_icons: ^1.0.2
```

---

## 4. Implementación del CRUD de Empleados

Vamos a crear una estructura funcional. Genera los siguientes archivos en `lib/`:

### A. Modelo de Datos (`lib/models/empleado_model.dart`)
```dart
class Empleado {
  String id;
  String nombre;
  String puesto;

  Empleado({required this.id, required this.nombre, required this.puesto});

  Map<String, dynamic> toMap() => {'nombre': nombre, 'puesto': puesto};

  factory Empleado.fromSnapshot(String id, Map<String, dynamic> data) {
    return Empleado(id: id, nombre: data['nombre'], puesto: data['puesto']);
  }
}
```

### B. Lógica Firestore (`lib/services/firebase_service.dart`)
```dart
import 'cloud_firestore/cloud_firestore.dart';

FirebaseFirestore db = FirebaseFirestore.instance;

Future<List> getEmpleados() async {
  List empleados = [];
  QuerySnapshot querySnapshot = await db.collection('empleados').get();
  for (var doc in querySnapshot.docs) {
    empleados.add({
      "id": doc.id,
      "nombre": doc.data()['nombre'],
      "puesto": doc.data()['puesto'],
    });
  }
  return empleados;
}

Future<void> addEmpleado(String nombre, String puesto) async {
  await db.collection('empleados').add({"nombre": nombre, "puesto": puesto});
}

Future<void> updateEmpleado(String id, String nuevoNombre) async {
  await db.collection('empleados').doc(id).set({"nombre": nuevoNombre, "puesto": "Florista"});
}

Future<void> deleteEmpleado(String id) async {
  await db.collection('empleados').doc(id).delete();
}
```

### C. Interfaz de Usuario UI (`lib/pages/home_page.dart`)

```dart
import 'package:flutter/material.dart';
import '../services/firebase_service.dart';

class HomePage extends StatefulWidget {
  @override
  _HomePageState createState() => _HomePageState();
}

class _HomePageState extends State<HomePage> {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
      app_builder: AppBar(title: const Text('Personal de Florería')),
      body: FutureBuilder(
        future: getEmpleados(),
        builder: (context, snapshot) {
          if (snapshot.hasData) {
            return ListView.builder(
              itemCount: snapshot.data?.length,
              itemBuilder: (context, index) {
                return ListTile(
                  title: Text(snapshot.data?[index]['nombre']),
                  subtitle: Text(snapshot.data?[index]['puesto']),
                  trailing: IconButton(
                    icon: Icon(Icons.delete, color: Colors.red),
                    onPressed: () async {
                      await deleteEmpleado(snapshot.data?[index]['id']);
                      setState(() {});
                    },
                  ),
                );
              },
            );
          } else {
            return const Center(child: CircularProgressIndicator());
          }
        },
      ),
      floatingActionButton: FloatingActionButton(
        onPressed: () async {
          await addEmpleado("Nuevo Empleado", "Florista Junior");
          setState(() {});
        },
        child: const Icon(Icons.add),
      ),
    );
  }
}
```

---

## 5. Pruebas de Verificación
1. **Conectividad:** Ejecuta `flutter run`. Si la app abre y muestra el indicador de carga, la conexión con Firebase es correcta.
2. **Escritura:** Presiona el botón `+`. Deberías ver un nuevo registro en tu **Firebase Console > Firestore Database**.
3. **Lectura:** Al reiniciar o refrescar la pantalla, el nombre "Nuevo Empleado" debe aparecer en la lista.

¿Deseas que profundicemos ahora en el **Skill de Scraping** para capturar precios de flores o prefieres pulir la UI del catálogo?
