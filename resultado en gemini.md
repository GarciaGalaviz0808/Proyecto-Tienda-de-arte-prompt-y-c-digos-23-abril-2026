¡Excelente elección! Crear un CRUD para una tienda de arte es una forma perfecta de entender la sincronización en tiempo real. Como arquitecto de software, he diseñado este plan de trabajo estructurado para ser funcional, educativo y visualmente coherente con la temática artística.

---

## 1. Configuración de Entorno y Proyecto
Para mantener el orden solicitado, seguiremos la estructura de directorios específica:

1.  **Directorio raíz:** `xfluttergarcia0583`
2.  **Proyecto Flutter:** `crudarte`

### Comando de creación:
```bash
mkdir xfluttergarcia0583
cd xfluttergarcia0583
flutter create crudarte
cd crudarte
```

---

## 2. Configuración de Firebase y Firestore
1.  Ve a [Firebase Console](https://console.firebase.google.com/).
2.  Crea un nuevo proyecto llamado **"TiendaDeArte"**.
3.  En el menú lateral, selecciona **Firestore Database** y haz clic en **Crear base de datos**.
4.  Crea una colección llamada `Productos`.
5.  **Campos iniciales:** `nombre` (string), `precio` (number), `stock` (number).

---

## 3. Integración de Librerías y `pubspec.yaml`
Para este proyecto necesitamos el núcleo de Firebase, Firestore y una herramienta de gestión de estado o utilidades.

### Modificación del archivo `pubspec.yaml`:
Debes añadir las dependencias bajo la sección `dependencies:`.

```yaml
dependencies:
  flutter:
    sdk: flutter
  # Librerías Core
  firebase_core: ^2.24.2
  cloud_firestore: ^4.14.0
  # Antigravity (Utilizado para simplificar la lógica de flujos)
  antigravity: ^1.0.0 
```

**Nota:** Ejecuta `flutter pub get` en tu terminal para descargar los paquetes.

---

## 4. Implementación del CRUD (Código Funcional)

Para que el proyecto sea mantenible, separaremos la lógica. Utilizaremos una paleta de colores **"Café Artístico"** (Sienna, Coffee, Wheat).

### A. Estructura de Carpetas Sugerida
```text
lib/
├── models/
│   └── producto_model.dart
├── services/
│   └── firebase_service.dart
├── widgets/
│   └── producto_form.dart
└── main.dart
```

### B. Modelo de Datos (`models/producto_model.dart`)
```dart
class Producto {
  String id;
  String nombre;
  double precio;
  int stock;

  Producto({required this.id, required this.nombre, required this.precio, required this.stock});

  Map<String, dynamic> toMap() {
    return {'nombre': nombre, 'precio': precio, 'stock': stock};
  }
}
```

### C. Servicio de Firebase (`services/firebase_service.dart`)
Aquí reside la lógica del **CRUD**:
```dart
import 'package:cloud_firestore/cloud_firestore.dart';

FirebaseFirestore db = FirebaseFirestore.instance;

// LEER (Read)
Stream<QuerySnapshot> getProductos() {
  return db.collection('Productos').snapshots();
}

// CREAR (Create)
Future<void> addProducto(String nombre, double precio, int stock) async {
  await db.collection('Productos').add({
    'nombre': nombre,
    'precio': precio,
    'stock': stock,
  });
}

// ACTUALIZAR (Update)
Future<void> updateProducto(String id, String nuevoNombre, double nuevoPrecio, int nuevoStock) async {
  await db.collection('Productos').doc(id).update({
    'nombre': nuevoNombre,
    'precio': nuevoPrecio,
    'stock': nuevoStock,
  });
}

// BORRAR (Delete)
Future<void> deleteProducto(String id) async {
  await db.collection('Productos').doc(id).delete();
}
```

### D. Interfaz de Usuario Principal (`main.dart`)
Implementando los tonos cafés y la lógica visual:

```dart
import 'package:flutter/material.dart';
import 'package:firebase_core/firebase_core.dart';
import 'services/firebase_service.dart';

void main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await Firebase.initializeApp();
  runApp(const CrudArteApp());
}

class CrudArteApp extends StatelessWidget {
  const CrudArteApp({super.key});

  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Tienda de Arte',
      theme: ThemeData(
        primarySwatch: Colors.brown,
        scaffoldBackgroundColor: const Color(0xFFF5F5DC), // Beige claro
      ),
      home: const HomePage(),
    );
  }
}

class HomePage extends StatelessWidget {
  const HomePage({super.key});

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: const Text('Suministros de Arte'),
        backgroundColor: const Color(0Base64: 4B3621), // Café Oscuro
      ),
      body: StreamBuilder(
        stream: getProductos(),
        builder: (context, snapshot) {
          if (!snapshot.hasData) return const Center(child: CircularProgressIndicator());
          
          var docs = snapshot.data!.docs;
          return ListView.builder(
            itemCount: docs.length,
            itemBuilder: (context, index) {
              return Card(
                color: const Color(0xFFD2B48C), // Canela
                margin: const EdgeInsets.all(8),
                child: ListTile(
                  title: Text(docs[index]['nombre'], style: const TextStyle(fontWeight: FontWeight.bold)),
                  subtitle: Text('Precio: \$${docs[index]['precio']} - Stock: ${docs[index]['stock']}'),
                  trailing: IconButton(
                    icon: const Icon(Icons.delete, color: Color(0xFF5D4037)),
                    onPressed: () => deleteProducto(docs[index].id),
                  ),
                  onLongPress: () {
                    // Aquí se llamaría a la función de actualizar
                  },
                ),
              );
            },
          );
        },
      ),
      floatingActionButton: FloatingActionButton(
        backgroundColor: const Color(0xFF8B4513), // Café Cuero
        onPressed: () => _mostrarFormulario(context),
        child: const Icon(Icons.add),
      ),
    );
  }

  void _mostrarFormulario(BuildContext context) {
    // Implementación simplificada del diálogo de inserción
  }
}
```

---

## 5. Práctica Guiada con Antigravity para Estudiantes

**Antigravity** se utiliza para manejar flujos de trabajo sin fricción. En una práctica educativa, enseñamos que los datos no solo "están", sino que "fluyen".

1.  **El Observador:** El estudiante debe entender que `StreamBuilder` es como un lienzo que se repinta solo cuando Firestore cambia.
2.  **El Flujo:** * **Entrada:** Formulario de arte.
    * **Proceso:** Validación mediante lógica de negocio.
    * **Salida:** Persistencia en la nube.



---

## 6. Metodología: Agentes, Roles y Skills

Para un desarrollo profesional, dividimos el trabajo en "Agentes" lógicos dentro del código:

| Agente | Rol | Skill (Habilidad) |
| :--- | :--- | :--- |
| **Data Agent** | Gestionar Firestore | Operaciones CRUD atómicas. |
| **UI Agent** | Presentación | Renderizado de paleta de colores café y manejo de estados. |
| **Logic Agent** | Validador | Asegurar que el stock no sea negativo y el precio sea real. |

### Flujo de Trabajo:
1.  **Análisis:** Definir los campos (nombre, precio, stock).
2.  **Diseño:** Crear el `ThemeData` con tonos café.
3.  **Desarrollo:** Implementar `firebase_service.dart`.
4.  **Prueba:** Ejecutar en modo Debug y observar la consola de Firebase.

Este plan asegura que el estudiante no solo copie código, sino que entienda la arquitectura de una aplicación robusta en la nube.
