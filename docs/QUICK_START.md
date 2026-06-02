# 🚀 Guía de Inicio Rápido - IntelliJ IDEA

## Abrir el Proyecto en IntelliJ

### Paso 1: Clonar el Repositorio

```bash
git clone https://github.com/jdsarnedo/nomina-calculator.git
cd nomina-calculator
```

### Paso 2: Abrir en IntelliJ

1. **Opción A:** Desde línea de comandos
   ```bash
   idea .
   ```

2. **Opción B:** Desde IntelliJ
   - File → Open
   - Selecciona la carpeta `nomina-calculator`
   - Click en "Open"

### Paso 3: Esperar a que Gradle/Maven indexe

IntelliJ tardará 1-2 minutos descargando dependencias.

## Ejecutar Backend

### Opción 1: Con Docker Compose (⭐ Recomendado)

```bash
# En la carpeta raíz del proyecto
docker-compose up -d

# El backend estará en http://localhost:8080
```

**Verificar que está corriendo:**
```bash
docker-compose ps
```

### Opción 2: Desde IntelliJ (Sin Docker)

**Requisitos previos:**
- Java 17+ instalado
- MongoDB corriendo localmente

**Pasos:**

1. **Abre Terminal en IntelliJ**
   - View → Tool Windows → Terminal

2. **Ejecuta Maven:**
   ```bash
   cd backend
   mvn clean install
   mvn spring-boot:run
   ```

3. **Deberías ver:**
   ```
   Started NominaCalculatorBackendApplication
   Tomcat started on port(s): 8080
   ```

**Verificar:**
- Abre http://localhost:8080/api
- Deberías ver un error 404 (que es normal, es la raíz)

## Ejecutar Frontend

### Opción 1: Con Docker Compose

```bash
# Ya está incluido en docker-compose up -d
# Accede a http://localhost
```

### Opción 2: Desde IntelliJ (Desarrollo)

**Requisitos previos:**
- Node.js 18+ instalado
- npm o yarn

**Pasos:**

1. **Abre otra terminal en IntelliJ**

2. **Instala dependencias:**
   ```bash
   cd frontend
   npm install
   ```

3. **Ejecuta el servidor de desarrollo:**
   ```bash
   ng serve
   ```

4. **Deberías ver:**
   ```
   ✔ Compiled successfully.
   ✔ Built successfully.
   Application bundle generated successfully.
   ```

5. **Accede a:**
   - http://localhost:4200

## Estructura del Proyecto en IntelliJ

```
nomina-calculator/
├── backend/
│   ├── src/
│   │   ├── main/
│   │   │   ├── java/
│   │   │   │   └── com/nomina/
│   │   │   │       ├── entity/          👈 Modelos
│   │   │   │       ├── controller/      👈 API endpoints
│   │   │   │       ├── service/         👈 Lógica de negocio
│   │   │   │       ├── repository/      👈 Acceso a datos
│   │   │   │       ├── config/          👈 Configuración
│   │   │   │       └── security/        👈 JWT y seguridad
│   │   │   └── resources/
│   │   │       └── application.yml      👈 Configuración
│   │   └── test/
│   ├── pom.xml                          👈 Dependencias Maven
│   ├── Dockerfile                       👈 Containerización
│   └── docker-compose.yml (en raíz)
│
├── frontend/
│   ├── src/
│   │   ├── app/
│   │   │   ├── components/             👈 Pantallas
│   │   │   │   ├── login/
│   │   │   │   ├── dashboard/
│   │   │   │   ├── horario/
│   │   │   │   └── nomina/
│   │   │   ├── services/               👈 Llamadas a API
│   │   │   │   ├── auth.service.ts
│   │   │   │   ├── horario.service.ts
│   │   │   │   ├── libranza.service.ts
│   │   │   │   └── nomina.service.ts
│   │   │   ├── guards/                 👈 Protección de rutas
│   │   │   │   └── auth.guard.ts
│   │   │   ├── interceptors/           👈 Middleware HTTP
│   │   │   │   └── auth.interceptor.ts
│   │   │   ├── app.module.ts
│   │   │   ├── app-routing.module.ts
│   │   │   └── app.component.ts
│   │   ├── index.html
│   │   ├── main.ts
│   │   └── styles.css
│   ├── package.json                    👈 Dependencias npm
│   ├── angular.json
│   ├── Dockerfile
│   └── nginx.conf
│
├── docs/
│   ├── DOCKER_GUIDE.md                 📖 Guía de Docker
│   ├── ARCHITECTURE.md                 🏗️ Arquitectura
│   ├── USER_GUIDE.md                   👤 Guía de uso
│   └── QUICK_START.md                  🚀 Este archivo
│
├── README.md                           📋 General
├── docker-compose.yml                  🐳 Compose
└── .gitignore
```

## Debugging en IntelliJ

### Backend (Spring Boot)

#### Debug Mode
1. Click en el icono "debug" al lado de main: `NominaCalculatorBackendApplication`
2. O: Run → Debug...
3. Usa breakpoints (click en número de línea)

#### Logs
- View → Tool Windows → Services
- Haz clic en Backend
- Tab "Console" muestra logs en tiempo real

### Frontend (Angular)

#### DevTools del Navegador
1. Con `ng serve` corriendo, abre http://localhost:4200
2. F12 para abrir DevTools
3. Tab "Sources" para debugging
4. Tab "Console" para logs

#### Breakpoints
1. En DevTools → Sources
2. Abre archivo de TypeScript
3. Click en número de línea
4. Vuelve a ejecutar el código

## Configuración de Dependencias

### Backend - Agregar dependencia Maven

**Opción 1:** Editar pom.xml
```xml
<dependency>
    <groupId>org.example</groupId>
    <artifactId>my-library</artifactId>
    <version>1.0</version>
</dependency>
```

Luego: Maven → Reimport All Maven Projects

**Opción 2:** Maven Helper Plugin
- Click derecho en pom.xml
- Maven → Add Dependency
- Busca y agrega

### Frontend - Agregar dependencia npm

```bash
cd frontend
npm install nombre-del-paquete

# O para desarrollo:
npm install --save-dev nombre-del-paquete
```

Reconstruye la aplicación para que coja los cambios.

## Cambios Comunes y Dónde Editarlos

### Cambiar Puerto del Backend

**Archivo:** `backend/src/main/resources/application.yml`
```yaml
server:
  port: 9000  # Cambiar aquí
```

### Cambiar URL de MongoDB

**Archivo:** `backend/src/main/resources/application.yml`
```yaml
spring:
  data:
    mongodb:
      uri: mongodb://usuario:pass@localhost:27017/nomina_db
```

### Cambiar URL de API en Frontend

**Archivo:** `frontend/src/app/services/*.service.ts`
```typescript
private apiUrl = '/api';  // O cambiar a http://localhost:8080/api
```

### Agregar Nueva Ruta en Frontend

**Archivo:** `frontend/src/app/app-routing.module.ts`
```typescript
const routes: Routes = [
  { path: 'nueva-ruta', component: NuevoComponent, canActivate: [AuthGuard] }
];
```

### Agregar Nuevo Endpoint en Backend

**Archivo:** `backend/src/main/java/com/nomina/controller/MiController.java`
```java
@PostMapping("/mi-endpoint")
public ResponseEntity<MiRespuesta> miMetodo() {
    // Tu código aquí
    return ResponseEntity.ok(respuesta);
}
```

## Hot Reload / Auto Refresh

### Backend
```bash
# Instala spring-boot-devtools (ya está en pom.xml)
# Los cambios se aplican automáticamente al guardar
```

### Frontend
```bash
# ng serve ya tiene hot reload
# Cualquier cambio en archivos se refleja automáticamente
```

## Compilar para Producción

### Backend
```bash
cd backend
mvn clean package
# Genera: target/nomina-calculator-backend-1.0.0.jar
```

### Frontend
```bash
cd frontend
ng build --configuration production
# Genera: dist/nomina-calculator-frontend/
```

## Base de Datos - Acceso directo

### Opción 1: Desde IntelliJ

1. View → Tool Windows → Database
2. Click en "+" → Data Source → MongoDB
3. Configura:
   - Host: localhost
   - Port: 27017
   - User: admin
   - Password: admin123
   - Database: nomina_db

### Opción 2: Línea de Comandos

```bash
# Acceder a MongoDB desde contenedor
docker-compose exec mongodb mongosh -u admin -p admin123

# Ver bases de datos
show databases

# Usar la BD
use nomina_db

# Ver colecciones
show collections

# Ver documentos
db.users.find()
db.horarios.find()
db.nominas.find()
```

## Problema Común: "Port Already in Use"

```bash
# Windows
netstat -ano | findstr :8080
taskkill /PID <PID> /F

# Mac/Linux
lsof -i :8080
kill -9 <PID>

# O cambia el puerto en application.yml
```

## Workflow Recomendado

### Día 1: Setup
```bash
git clone https://github.com/jdsarnedo/nomina-calculator.git
cd nomina-calculator
docker-compose up -d
# Leer docs/DOCKER_GUIDE.md
```

### Día 2-3: Entendimiento
```bash
# Leo documentación
open docs/ARCHITECTURE.md
open docs/USER_GUIDE.md

# Exploro BD
docker-compose exec mongodb mongosh -u admin -p admin123
```

### Día 4+: Desarrollo
```bash
# Terminal 1: Backend
cd backend
mvn spring-boot:run

# Terminal 2: Frontend
cd frontend
ng serve

# Terminal 3: MongoDB
docker run -d -p 27017:27017 mongo:7.0

# Edita código en IntelliJ
# Los cambios se aplican automáticamente
```

## Recursos Útiles en IntelliJ

### Shortcuts Útiles
| Shortcut | Acción |
|----------|--------|
| Ctrl+Space | Autocompletar |
| Ctrl+Shift+F10 | Ejecutar configuración actual |
| Ctrl+F9 | Rebuild proyecto |
| Ctrl+/ | Comentar línea |
| Ctrl+D | Duplicar línea |
| Ctrl+H | Buscar y reemplazar |
| F2 | Ir a siguiente error |

### Plugins Recomendados
- Lombok (reduce boilerplate Java)
- MongoDB Browser
- RESTClient
- Angular Language Service

## Terminal Integrada en IntelliJ

```bash
# Abre: View → Tool Windows → Terminal

# Útil para:
npm install
mvn clean install
docker-compose ps
git status
```

## Commit y Push desde IntelliJ

1. Git → Commit (Ctrl+K)
2. Escribe mensaje
3. Commit and Push
4. O: Git → Push (Ctrl+Shift+K)

---

**¡Listo!** Ya puedes trabajar con el proyecto en IntelliJ. 

¿Preguntas? Consulta `docs/DOCKER_GUIDE.md` o `docs/ARCHITECTURE.md`
