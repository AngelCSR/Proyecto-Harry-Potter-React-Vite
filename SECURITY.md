# 🛡️ Política de Seguridad

La seguridad de nuestro proyecto es nuestra máxima prioridad. Agradecemos a la comunidad de desarrolladores e investigadores de seguridad por tomarse el tiempo de informar de posibles vulnerabilidades de forma responsable.

## Cómo Reportar una Vulnerabilidad (Divulgación Responsable)

Si encuentra una vulnerabilidad de seguridad en este repositorio, **NO** abra un Issue público ni un Pull Request.

Para proteger a la comunidad, la información debe ser revelada de forma privada.

1.  **Contacto Principal:** Por favor, envíe un correo electrónico detallado a [**tuncorreo@email.com**].

**Información que debe incluir:**
* Una descripción detallada de la vulnerabilidad.
* Pasos claros y concisos para reproducir el problema.
* La versión del proyecto afectada (por ejemplo, el *commit hash* o número de versión).

Nos comprometemos a acusar recibo de su informe en un plazo de **48 horas** y a trabajar en una corrección lo más rápido posible. Solicitamos que la vulnerabilidad se mantenga confidencial hasta que hayamos lanzado un parche oficial.

---

## Exclusión de Archivos y Seguridad (a través de `.gitignore`)

Para garantizar la integridad y la confidencialidad de nuestro código y evitar la exposición accidental de secretos, utilizamos un archivo `.gitignore`  que excluye los siguientes archivos del control de versiones:

### 1. Logs y Archivos de Depuración

Estos archivos se excluyen para mitigar la **fuga de datos sensibles** generados durante la ejecución de la aplicación.

| Patrones Excluidos | Razones de Seguridad y Práctica |
| :--- | :--- |
| **`logs`, `*.log`** | Los archivos de registro pueden capturar accidentalmente **claves API, tokens de sesión, direcciones IP** o rastros de datos privados si un error de *logging* está mal configurado. Su exclusión es una medida de seguridad crítica. |
| **`npm-debug.log*`, `yarn-debug.log*`, etc.** | Los *logs* de los gestores de paquetes son específicos del entorno de depuración del usuario y, al igual que los *logs* generales, pueden contener información de rutas locales o detalles de configuración que no deben ser públicos. |

---

### 2. Dependencias, Compilación y Caché

La exclusión de estos directorios asegura la uniformidad del entorno de desarrollo y reduce la superficie de ataque.

| Patrones Excluidos | Razones de Seguridad y Práctica |
| :--- | :--- |
| **`node_modules`** | **Integridad del Entorno.** Este directorio es voluminoso y sus archivos son dependientes de la arquitectura del sistema operativo. Subirlo puede introducir dependencias no uniformes o específicas del entorno. Excluirlo fuerza a los colaboradores a instalar dependencias limpias y consistentes según **`package.json`** y **`package-lock.json`**. |
| **`dist`, `dist-ssr`** | **Artefactos de Compilación.** Contienen el código de producción compilado o transpuesto (minificado y optimizado). Su exclusión garantiza que el repositorio solo contenga el código fuente auditable y legible. |
| **`.vite/`** | **Caché del Bundler.** Este es el directorio de caché interno de Vite. Excluirlo evita que los artefactos de compilación temporales se rastreen. |
| **`.eslintcache`** | **Caché de Herramientas.** Es el caché generado por ESLint. No solo es específico del usuario, sino que su rastreo ralentizaría Git sin aportar valor al código fuente. |

---

### 3. Configuración Local y Archivos de Editor

Esta sección protege directamente los secretos del proyecto y los metadatos privados del desarrollador.

| Patrones Excluidos | Razones de Seguridad y Práctica |
| :--- | :--- |
| **`*.local`** | **Protección de Secretos.** Este patrón (usado para archivos como `.env.local`) filtra todas las **variables de entorno sensibles** (p. ej., claves API, credenciales, URLs de servicios privados). Su exclusión es una medida de seguridad fundamental. |
| **`.vscode/`, `.idea`** | **Mitigación de Fuga de Metadatos.** Estos directorios contienen configuraciones de usuario del IDE (rutas de depuración, historial de búsqueda o *settings* específicos de la máquina). Su exclusión previene la publicación involuntaria de información que podría ser útil para la elaboración de ataques dirigidos. **Nota:** Se mantiene la excepción para `!.vscode/extensions.json` para estandarizar las herramientas de calidad y seguridad. |
| **`*.suo`, `*.sln`, `.DS_Store`, etc.** | **Metadatos del Sistema/IDE.** Son archivos generados por sistemas operativos (macOS) o IDEs como Visual Studio. No solo son irrelevantes, sino que evitan conflictos al compartir el código entre desarrolladores que usan diferentes herramientas. |
