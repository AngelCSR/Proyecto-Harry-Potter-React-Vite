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


# Protección de la Documentación
La documentación esencial del proyecto, que se considera código fuente y artefactos críticos, se aloja en el repositorio principal y se adhiere a las siguientes prácticas para proteger su integridad y disponibilidad:

## 1. Uso de Ramas Protegidas (Protected Branches)
La rama principal del repositorio (ej., main o master) que contiene la documentación final y los archivos de código fuente estará protegida.

### Las protecciones incluyen:

Restricción de Pushes: Se prohíbe el push directo a la rama principal. Todos los cambios deben realizarse a través de Pull Requests (PRs).

Revisión Obligatoria de PRs: Se requiere al menos una revisión aprobada por un colaborador designado antes de que se pueda fusionar un PR.

Comprobaciones de Estado (Status Checks): Se deben pasar las pruebas automatizadas (si las hay) antes de la fusión.

## 2. Revisión de Pull Requests (PRs)
Todo cambio propuesto a la documentación o el código debe pasar por un proceso de revisión por pares.

El revisor es responsable de:

Verificar la corrección y claridad de la documentación.

Asegurar el cumplimiento de los estándares y guías de estilo del proyecto.

Comprobar que no se introduzcan credenciales o información sensible.

## 3. Auditoría de Historial
Se fomentan los mensajes de commit claros y descriptivos para facilitar la auditoría y el seguimiento de los cambios.

Se restringe la reescritura del historial (ej., uso de git push --force) en las ramas compartidas o principales.

## Garantía de Recuperación del Repositorio
La recuperación del repositorio ante una pérdida de datos, corrupción o un error grave (ej., eliminación accidental, fallo del proveedor de hosting Git) se garantiza mediante:

### 1.Copias de Seguridad (Backups)
Copias de Seguridad Externas Automáticas: Se realiza una copia de seguridad diaria y automatizada del repositorio completo (incluyendo el historial) en un servicio de almacenamiento externo y geográficamente separado del proveedor de hosting principal (ej., un mirror en otro servicio Git o almacenamiento en la nube).

#### Retención de Backups: Las copias de seguridad se retienen durante un mínimo de 30 días para permitir la restauración a un punto anterior en el tiempo.

#### Pruebas de Restauración: Se realizan pruebas periódicas trimestrales de restauración a partir de los backups para asegurar la viabilidad del proceso.

### 2. Redundancia de Proveedor 
El repositorio se mantiene replicado en al menos dos plataformas de hosting Git diferentes (ej., GitHub y GitLab, o GitHub y un servidor Git autoalojado). Esto proporciona redundancia en caso de interrupción del servicio del proveedor principal.

### 3. Mantenimiento del Historial Completo
Git, por diseño, distribuye el historial completo del repositorio a cada colaborador que lo clona. Si el repositorio central falla, cualquier colaborador con un clone reciente puede, teóricamente, restablecer el repositorio. Esto actúa como una línea de defensa inicial.

