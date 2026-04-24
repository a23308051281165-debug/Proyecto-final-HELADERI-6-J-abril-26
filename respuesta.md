Para implementar tu arquitectura de agentes **`.agents`** y configurar el proyecto de la Heladería, seguiremos una estructura modular.

### 1. Estructura del Directorio (`proyectoproductos`)

Crea la carpeta raíz `proyectoproductos` y dentro ejecuta la estructura:

```text
proyectoproductos/
├── .agents/
│   ├── SKILL.md
│   ├── scripts/
│   ├── ejemplos/
│   └── resources/
├── lib/
│   ├── models/producto.dart
│   ├── services/firestore_service.dart
│   ├── ui/
│   │   ├── home_screen.dart
│   │   └── crud_screen.dart
│   └── main.dart
└── pubspec.yaml
```

---

### 2. Configuración de Prerrequisitos

Si no tienes `firebase_cli`, ejecútalo en tu terminal:
1. **Firebase CLI:** `npm install -g firebase-tools`
2. **Login:** `firebase login`
3. **FlutterFire CLI:** `dart pub global activate flutterfire_cli`
4. **Configurar proyecto:** En la raíz del proyecto, ejecuta:
   `flutterfire configure` (selecciona tu proyecto de Firebase creado en la consola).

---

### 3. Archivo `.agents/SKILL.md`

```markdown
# Skill: HeladeriaManager
Habilidad para gestionar el ciclo de vida de productos (CRUD) en Firestore.
- Agente Diseño: Define UI/UX de pantallas.
- Agente Código: Implementa lógica en Dart/Flutter.
- Agente Scraping: Extrae datos de sabores si es necesario.
```

---

### 4. Dependencias (`pubspec.yaml`)

Agrega esto a tu `pubspec.yaml`:

```yaml
dependencies:
  flutter:
    sdk: flutter
  firebase_core: latest
  cloud_firestore: latest
```

---

### 5. Código del Proyecto

#### `lib/models/producto.dart`
```dart
class Producto {
  String id;
  String nombre;
  double precio;

  Producto({required this.id, required this.nombre, required this.precio});

  Map<String, dynamic> toMap() => {'nombre': nombre, 'precio': precio};
}
```

#### `lib/services/firestore_service.dart`
```dart
import 'package:cloud_firestore/cloud_firestore.dart';
import '../models/producto.dart';

class FirestoreService {
  final FirebaseFirestore _db = FirebaseFirestore.instance;

  Future<void> addProducto(Producto p) => _db.collection('productos').add(p.toMap());
  Stream<QuerySnapshot> getProductos() => _db.collection('productos').snapshots();
  Future<void> deleteProducto(String id) => _db.collection('productos').doc(id).delete();
}
```

#### `lib/ui/home_screen.dart`
```dart
import 'package:flutter/material.dart';
import '../services/firestore_service.dart';

class HomeScreen extends StatelessWidget {
  final FirestoreService _service = FirestoreService();

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("Heladería App")),
      body: StreamBuilder(
        stream: _service.getProductos(),
        builder: (context, snapshot) {
          if (!snapshot.hasData) return CircularProgressIndicator();
          return ListView.builder(
            itemCount: snapshot.data!.docs.length,
            itemBuilder: (context, i) => ListTile(
              title: Text(snapshot.data!.docs[i]['nombre']),
              trailing: IconButton(
                icon: Icon(Icons.delete),
                onPressed: () => _service.deleteProducto(snapshot.data!.docs[i].id),
              ),
            ),
          );
        },
      ),
    );
  }
}
```

#### `lib/main.dart`
```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'ui/home_screen.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(MaterialApp(home: HomeScreen()));
}
```

---

### 6. Verificación de Funcionalidad
1. **Terminal:** Ejecuta `flutter doctor` para validar que VS Code y Android SDK están listos.
2. **Conectividad:** Verifica que el archivo `firebase_options.dart` (generado por `flutterfire configure`) esté en `lib/`.
3. **Ejecución:** `flutter run`.

¿Deseas que profundice en la lógica de alguno de los agentes específicos para ampliar la automatización de este CRUD?
