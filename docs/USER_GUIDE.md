# 📖 Guía de Uso - Nómina Calculator

## Índice

1. [Primeros Pasos](#primeros-pasos)
2. [Acceso al Sistema](#acceso-al-sistema)
3. [Roles y Permisos](#roles-y-permisos)
4. [Flujos Principales](#flujos-principales)
5. [Ejemplos Prácticos](#ejemplos-prácticos)
6. [FAQ](#faq)

## Primeros Pasos

### Requisitos

- Navegador moderno (Chrome, Firefox, Safari, Edge)
- Conexión a Internet
- Credenciales de acceso (ADMIN debe crear la primera vez)

### Acceder a la Aplicación

1. Abre http://localhost en tu navegador
2. Deberías ver la pantalla de login

## Acceso al Sistema

### Login

```
Usuario: admin
Contraseña: admin123
```

**Primera vez (crear usuarios):**

1. Accede como ADMIN
2. Los ADMINs pueden crear usuarios en base de datos
3. Comparte credenciales con usuarios

## Roles y Permisos

### ADMIN (Administrador)

**Puede:**
- ✅ Crear y editar horarios
- ✅ Crear abreviaturas de turnos
- ✅ Ver todas las nóminas
- ✅ Crear libranzas para trabajadores
- ✅ Gestionar usuarios (futura)

**No puede:**
- ❌ Ver datos privados de trabajadores

### USER (Trabajador/Empleado)

**Puede:**
- ✅ Ver sus libranzas
- ✅ Cargar horarios mensuales
- ✅ Calcular su nómina
- ✅ Descargar desprendible en PDF
- ✅ Ver historial de nóminas

**No puede:**
- ❌ Crear horarios
- ❌ Ver datos de otros trabajadores

## Flujos Principales

### Flujo 1: ADMIN - Parametrizar Horarios

**Objetivo:** Crear los tipos de horarios que existirán

**Pasos:**

1. Login como ADMIN
2. Menú → Horarios
3. Llenar el formulario:
   - **Abreviatura:** MT (Mañana Temprano)
   - **Descripción:** Mañana Temprano (5am - 1pm)
   - **Horas:** 8
   - **¿Tiene Recargo?** No
   - Click en "Crear Horario"

4. Repetir para otros horarios:

| Abreviatura | Descripción | Horas | Recargo | % |
|-------------|------------|-------|---------|-----|
| MT | Mañana Temprano | 8 | No | - |
| TA | Tarde | 8 | No | - |
| NO | Nocturno | 8 | Sí | 25% |
| FES | Festivo | 8 | Sí | 100% |
| DOM | Dominical | 8 | Sí | 50% |
| EXT | Extra | 4 | Sí | 50% |

**Resultado:** Tabla con horarios disponibles

### Flujo 2: ADMIN - Crear Libranza para Trabajador

**Objetivo:** Registrar un préstamo/libranza de un trabajador

**Pasos:**

1. Menú → (futuro) Gestionar Libranzas
2. Seleccionar trabajador
3. Llenar formulario:
   - **Concepto:** Préstamo de caja
   - **Monto Total:** $2,000,000
   - **Cuota Mensual:** $200,000
   - **Cuotas Restantes:** 10
   - Click en "Crear"

**Resultado:** La cuota se descontará automáticamente en nóminas

### Flujo 3: USER - Cargar Horarios Mensuales

**Objetivo:** Ingresar qué turno trabajó cada día del mes

**Pasos:**

1. Login como TRABAJADOR
2. Menú → (futuro) Cargar Horarios
3. Seleccionar Mes: JUNIO
4. Seleccionar Año: 2026
5. Para cada día:
   - Día 1: Seleccionar horario MT (Mañana Temprano)
   - Día 2: Seleccionar horario TA (Tarde)
   - Día 3: Seleccionar horario NO (Nocturno)
   - Etc.
6. Click en "Guardar"

**Resultado:** Horarios guardados para el mes

### Flujo 4: USER - Calcular Nómina

**Objetivo:** Obtener el desprendible de pago del mes

**Pasos:**

1. Menú → Nómina
2. Seleccionar Mes: JUNIO
3. Seleccionar Año: 2026
4. Click en "Calcular Nómina"
5. Sistema calcula automáticamente:
   - Salario mínimo: $1,300,000
   - Auxilio transporte: $163,540
   - Recargos nocturnos y dominicales
   - Descuentos (EPS, Pensión)
   - Descuentos por libranzas
   - **SALARIO LÍQUIDO**

**Ver resultado:**

```
DEVENGOS
├─ Salario Mínimo:        $1,300,000
├─ Auxilio Transporte:    $  163,540
└─ Recargos:              $  200,000
   Total Devengado:       $1,663,540

DESCUENTOS
├─ EPS (4%):              $   52,000
├─ Pensión (4%):          $   52,000
├─ Libranzas:             $  200,000
└─ Total Descuentos:      $  304,000

RESUMEN
└─ SALARIO LÍQUIDO:       $1,359,540
```

6. Click en "Descargar PDF" para tener el desprendible

## Ejemplos Prácticos

### Ejemplo 1: Nómina Básica (sin recargos)

**Horarios del mes:**
- 20 días: MT (Mañana Temprano)
- 10 días: TA (Tarde)
- Total: 30 días = 240 horas

**Cálculo:**
```
Salario mínimo (240h):     $1,300,000
Auxilio transporte:        $  163,540
Recargos:                  $        0
─────────────────────────────────────
Devengado:                 $1,463,540

EPS (4%):                  $   52,000
Pensión (4%):              $   52,000
─────────────────────────────────────
Descuentos:                $  104,000

SALARIO LÍQUIDO:           $1,359,540
```

### Ejemplo 2: Con Libranza

**Mismo mes + Libranza de $200,000 (cuota)**

```
Devengado:                 $1,463,540

EPS (4%):                  $   52,000
Pensión (4%):              $   52,000
Libranza (cuota):          $  200,000
─────────────────────────────────────
Descuentos:                $  304,000

SALARIO LÍQUIDO:           $1,159,540
```

### Ejemplo 3: Con Recargos (Nocturno y Dominical)

**Horarios del mes:**
- 15 días: MT (240h / 30 = 8h/día)
- 10 días: NO (Nocturno +25%)
- 5 días: DOM (Dominical +50%)

```
Salario base (240h):       $1,300,000
  Por hora: 1,300,000/240 = $5,416.67

Recargos:
  - Nocturno: 80h * 5,416.67 * 25% = $108,333
  - Dominical: 40h * 5,416.67 * 50% = $108,333
  Total Recargos:           $  216,666

Auxilio transporte:        $  163,540
─────────────────────────────────────
Devengado:                 $1,680,206

EPS (4%):                  $   52,000
Pensión (4%):              $   52,000
─────────────────────────────────────
Descuentos:                $  104,000

SALARIO LÍQUIDO:           $1,576,206
```

## FAQ

### P1: ¿Cómo creo mi primer usuario?

**R:** El primer usuario ADMIN se crea manualmente en la base de datos MongoDB:

```javascript
db.users.insertOne({
  "username": "admin",
  "password": "$2a$10$...", // BCrypt hash de "admin123"
  "email": "admin@nomina.local",
  "firstName": "Admin",
  "lastName": "Sistema",
  "role": "ADMIN",
  "active": true,
  "createdAt": new Date(),
  "updatedAt": new Date()
})
```

### P2: ¿Puedo editar una nómina ya calculada?

**R:** No. Las nóminas son de solo lectura después de calcularse. Si necesitas corregir:

1. Corrige los horarios en HorarioDia
2. Borra el documento de Nomina en la BD
3. Vuelve a calcular

### P3: ¿Qué pasa si no cargo los horarios de un día?

**R:** Se cuenta como día sin trabajar. No hay horas ni salario por ese día.

### P4: ¿Las libranzas se cargan automáticamente?

**R:** Sí. El sistema calcula automáticamente las nóminas activas (estado=ACTIVO) y descuenta la cuota mensual.

### P5: ¿Puedo descargar nóminas anteriores?

**R:** Sí. En la pantalla de Nómina:

1. Selecciona el mes anterior
2. Click en "Calcular"
3. Si existe, la muestra
4. Descargar PDF

### P6: ¿Se actualizan los recargos si cambio los horarios?

**R:** No. Debes recalcular la nómina. El sistema te muestra una versión nueva.

### P7: ¿Puedo tener múltiples turnos el mismo día?

**R:** En la versión actual, NO. Un día = un turno. Para versiones futuras se podría permitir jornadas partidas.

### P8: ¿Cómo sé si mi nómina está bien calculada?

**R:** El sistema realiza validaciones:
- Salario nunca es menor al mínimo
- Descuentos nunca son mayores al devengado
- Saldo de libranzas siempre positivo

### P9: ¿Puedo cambiar mi contraseña?

**R:** En la versión actual, NO. Contacta al ADMIN.

### P10: ¿Qué pasa si se cae MongoDB?

**R:** La aplicación mostrará errores de conexión. Reinicia:

```bash
docker-compose restart mongodb
```

## Troubleshooting

### Problema: No puedo ingresar

**Soluciones:**
1. Verifica usuario y contraseña
2. Limpia cache del navegador: Ctrl+F5
3. Verifica que MongoDB está corriendo: `docker ps`

### Problema: No veo los horarios que creé

**Soluciones:**
1. Recarga la página: F5
2. Verifica que eres ADMIN
3. Revisa los logs: `docker-compose logs backend`

### Problema: El cálculo de nómina es diferente a lo esperado

**Soluciones:**
1. Verifica los horarios cargados para el mes
2. Verifica las libranzas activas
3. Contacta al soporte técnico

### Problema: No puedo descargar el PDF

**Soluciones:**
1. Permite ventanas emergentes en el navegador
2. Verifica que tienes espacio en disco
3. Prueba con otro navegador

## Contacto y Soporte

Para reportar bugs o sugerencias:

📧 Email: jdsarnedo@gmail.com
🐛 GitHub Issues: https://github.com/jdsarnedo/nomina-calculator/issues

---

**Última actualización:** Junio 2026
