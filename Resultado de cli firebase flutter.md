Para configurar Firebase CLI en un entorno de desarrollo profesional con Flutter, es fundamental asegurar que el ecosistema de **Node.js** sea estable. Aquí tienes la guía técnica detallada para preparar tu estación de trabajo en Windows.

---

## 1. Software necesario: Node.js y npm
Para gestionar herramientas como Firebase CLI de forma global, necesitamos el entorno de ejecución **Node.js**, el cual incluye automáticamente **npm** (Node Package Manager).

* **Software:** Instalador oficial de Node.js (.msi).
* **Versión recomendada:** **LTS** (Long Term Support) para garantizar estabilidad con los plugins de Flutter.

---

## 2. Procedimiento de Verificación e Instalación

### Cómo verificar si ya tienes Node.js y npm
Abre una terminal (PowerShell o CMD) y ejecuta:

```bash
node -v
npm -v
```
> **Nota:** Si la terminal devuelve un error de "comando no reconocido", procede con la instalación manual.

### Instalación paso a paso en Windows
1.  **Descarga:** Ve al sitio oficial [nodejs.org](https://nodejs.org/) y descarga el instalador **LTS**.
2.  **Ejecución:** Abre el archivo `.msi` descargado.
3.  **Configuración Clave:** Durante el asistente, asegúrate de que la opción **"Add to PATH"** esté seleccionada (esto permite ejecutar comandos desde cualquier carpeta).
4.  **Herramientas adicionales:** El instalador preguntará si deseas instalar "Tools for Native Modules". Es recomendable marcar la casilla para evitar errores futuros con herramientas de C++.
5.  **Reinicio:** Al finalizar, **debes cerrar y volver a abrir tu terminal** para que Windows reconozca los nuevos caminos del sistema.

---

## 3. Instalación de Firebase CLI (Global)
Una vez que `npm` esté listo, instalaremos las herramientas de Firebase para que estén disponibles en todo tu sistema (específicamente para que Flutter las use).

### Comando de instalación global:
```bash
npm install -g firebase-tools
```
* **`-g`**: Indica que la instalación es **global**, permitiendo usar el comando `firebase` en cualquier carpeta de tu proyecto Flutter.

---

## 4. Comandos Esenciales de Firebase

### Cómo acceder a Firebase con tu Cuenta de Google
Para vincular tu terminal con tu consola de Firebase, usa el comando de autenticación:

```bash
firebase login
```
1.  Se abrirá una ventana en tu navegador predeterminado.
2.  Selecciona tu cuenta de Google asociada al proyecto.
3.  Otorga los permisos necesarios.
4.  Al terminar, la terminal mostrará: `✔ Success! Logged in as correo@gmail.com`.

### Cómo usar firebase-tools en Flutter
Para que tu aplicación Flutter se comunique con Firebase, una vez logueado, debes inicializar el puente de configuración:

* **Listar proyectos:** `firebase projects:list` (Verifica que tienes acceso a tus proyectos).
* **Configurar FlutterFire CLI:** (Paso crítico para Flutter):
    ```bash
    dart pub global activate flutterfire_cli
    flutterfire configure
    ```
    Este último comando utiliza las `firebase-tools` para generar automáticamente el archivo `firebase_options.dart` en tu proyecto.

---

## 5. Resumen de Flujo de Trabajo



1.  **Instalar Node.js/npm** (Motor de herramientas).
2.  **npm install -g firebase-tools** (Instalar el "agente" de Firebase).
3.  **firebase login** (Identificarse ante Google).
4.  **flutterfire configure** (Vincular el código Dart con la consola de Firebase).

¿Tienes algún problema con las variables de entorno o prefieres que revisemos cómo configurar el archivo `firebase_options.dart` una vez instalado el CLI?
