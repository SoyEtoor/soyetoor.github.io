# soyetoor.github.io

## Task and Feature Breakdown

Este documento captura los EPICs, features y tareas extraídas del EPIC Control. Cada tarea incluye descripción, criterios de aceptación, dependencias, prioridad y etiquetas, como referencia para crear issues en GitHub.

### EPIC: Control Plane / Superadmin

#### Feature: Onboarding e impersonación (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Crear entidad Empresa | Modelo para guardar nombre, correo_admin, plan_id, estado y empresa_id de cada compañía. | Nombre único por empresa, empresa_id generado automáticamente, estado activo o inactivo, timestamps para auditoría. | – | Alta | backend, saas |
| API crear empresa e invitación | Endpoint de superadmin para crear una empresa y enviar invitación al administrador. | Solo disponible para superadmin, genera token único, envía correo electrónico, registra log. | Autenticación, EmailService | Alta | backend, security, audit |
| Onboarding admin empresa | Flujo de registro iniciado a partir de la invitación. | Token válido, contraseña segura, datos guardados y log de creación. | API invitación | Alta | frontend, auth |
| Impersonation mode | Permitir al superadmin ingresar como un administrador de empresa. | Indicador visible de modo de suplantación, auditoría activa, restricciones de superadmin aplicadas. | Auth, Logs | Alta | backend, security |
| Listar empresas | Pantalla/tablero que muestra empresas con filtros. | Paginación, filtro por estado, acceso a detalle para editar. | Entidad Empresa | Media | frontend, backend |
| Cambiar admin de empresa | Reasignar el usuario administrador de una empresa. | Notificación al nuevo admin, registro en log de auditoría, solo superadmin puede ejecutarlo. | Usuario | Media | backend, audit |

#### Feature: Auditoría global (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Implementar logs | Crear tabla Auditoria con campos usuario, empresa, acción, entidad y fecha. | Registro de las acciones de create/update/delete; la información no debe ser editable. | Todas las entidades | Alta | backend, audit |
| API consulta logs | Endpoint para consultar logs filtrados por empresa, usuario y fecha. | Permite filtrar por usuario, empresa y rango de fechas; incluye paginación. | Logs | Media | backend |
| UI logs | Interfaz para visualizar y filtrar logs. | Búsqueda por fecha, usuario y acción; listado paginado. | API logs | Media | frontend |

### EPIC: Empresa (Tenant)

#### Feature: Configuración empresa (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad ConfiguracionEmpresa | Modelo con campos moneda, margen, maxStops y varios flags de configuración. | Existe solo una configuración por empresa; valores por defecto definidos. | Empresa | Alta | backend |
| API actualizar configuración | Endpoint que permite editar la configuración por el administrador. | Validaciones de campos y reglas (RLS) que aseguren que solo la empresa propietaria puede modificarla. | ConfiguracionEmpresa | Alta | backend, security |
| UI configuración | Formulario para editar la configuración de la empresa. | Dropdown para selección de moneda, switches para activar/desactivar flags. | API configuración | Media | frontend |

#### Feature: Stripe y suscripciones (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad PlanSuscripcion | Modelo con nombre, precio y lista de features. | Asociada a la empresa correspondiente. | Empresa | Alta | backend |
| Crear cliente Stripe | Registrar a la empresa en Stripe al darse de alta. | Guardar customer_id; manejar errores y registrar log. | Stripe | Alta | backend, integration |
| Crear suscripción | Asignar el plan de suscripción en Stripe. | Mantener sincronizado el estado entre el sistema y Stripe; registrar logs. | Stripe | Alta | backend |
| Webhooks Stripe | Procesar los eventos que envía Stripe (p. ej. invoice.paid, subscription.updated). | Validar firma, actualizar estado de la suscripción y registrar log. | Stripe | Alta | backend, security |
| UI suscripciones | Pantalla que muestra el plan actual y permite cambiar o cancelar la suscripción. | Ver el plan activo, opción para cambiar/cancelar y reflejar estado de Stripe. | Stripe API | Media | frontend |

### EPIC: Autenticación y Usuarios

#### Feature: Auth y roles (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad Usuario | Tabla con email, password (hash), rol y empresa_id. | Email único por empresa; contraseña almacenada de forma segura (hash). | Empresa | Alta | backend, auth |
| Login | Mecanismo de autenticación basado en JWT. | Generación de token válido con expiración, validación en cada petición. | Usuario | Alta | backend, frontend |
| Invitar usuario | Envío de invitación por correo electrónico para crear usuario dentro de una empresa. | Generar token único con expiración, enviar correo con la invitación. | Email service | Alta | backend |
| CRUD usuarios | Endpoints para crear, listar, actualizar y desactivar usuarios. | Soporte a soft delete, registro de auditoría; el email no debe ser editable. | Usuario | Alta | backend |
| UI usuarios | Interfaz de gestión de usuarios. | Tabla con paginación, orden alfabético, acciones de editar/desactivar. | API usuarios | Media | frontend |

### EPIC: Operadores

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad Operador | Registro de operadores con datos personales y número/licencia de conductor. | RFC válido; fecha de vencimiento de la licencia obligatoria. | Empresa | Alta | backend |
| CRUD operadores | Endpoints para alta, baja y modificación de operadores. | Validaciones de campos; auditoría de cambios. | Operador | Alta | backend |
| UI operadores | Tabla que muestra operadores con un identificador corto. | Funcionalidad de búsqueda y paginación. | API operadores | Media | frontend |

### EPIC: Clientes y Bases

#### Feature: Clientes (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad Cliente | Modelo con campos RFC, razón social y contacto. | RFC único por empresa. | Empresa | Alta | backend |
| CRUD clientes | Endpoints para alta, baja y edición de clientes. | Evitar duplicados; registrar logs de auditoría. | Cliente | Alta | backend |
| UI clientes | Interfaz para visualizar y administrar clientes. | Tabla con búsqueda y paginación. | API clientes | Media | frontend |

#### Feature: Bases logísticas (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad Base | Registro con coordenadas y dirección detallada. | Latitud y longitud son obligatorios. | Cliente | Alta | backend |
| CRUD bases | Endpoints para gestionar bases logísticas. | Evitar duplicados de coordenadas; auditoría de cambios. | Base | Alta | backend |
| UI bases | Formulario con mapa para seleccionar ubicación. | Selección visual de la posición en el mapa (Leaflet). | Leaflet | Media | frontend |

### EPIC: Cotizador de rutas

#### Feature: Geocoding (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Servicio geocoding | Servicio interno que convierte texto de dirección a coordenadas. | Precisión básica aceptable; manejo de errores de la API externa. | API externa | Alta | backend |
| UI búsqueda | Componente UI con autocomplete para direcciones. | Sugerencias dinámicas mientras se escribe. | API geocoding | Alta | frontend |

#### Feature: Rutas INEGI (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Integrar API INEGI | Consumir la API de rutas de INEGI para obtener trayectos. | Al menos 3 rutas válidas por consulta. | INEGI | Alta | backend |
| Procesar rutas | Normalizar y enriquecer la información de las rutas. | Calcular distancia, tiempo y costos de peaje. | INEGI | Alta | backend |
| Calcular combustible | Calcular consumo de combustible en función de kilómetros y rendimiento. | Fórmula correcta km/lt según configuración de empresa. | Rutas | Alta | backend |
| UI mapa rutas | Visualizar las tres rutas sugeridas. | Mostrar rutas con colores distintos y permitir interacción sobre el mapa. | Leaflet | Media | frontend |

#### Feature: Resultados (MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Calcular costo total | Sumar todos los costos asociados a la ruta (combustible, peajes, margen). | Cálculo incluye margen configurado de la empresa. | Rutas | Alta | backend |
| UI resultados | Presentar los resultados de cada ruta de forma comparativa. | Tarjetas comparativas con selección clara de la ruta. | API rutas | Alta | frontend |
| Registrar viaje | Persistir la ruta seleccionada como un viaje. | Guardar todos los datos relevantes y registrar auditoría. | Viaje | Alta | backend |
| Exportar | Exportar información del viaje en PDF, XML o XLSX. | Genera archivos válidos para descarga. | Librerías de exportación | Media | backend |

### EPIC: Viajes

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad Viaje | Definición del modelo de viaje que relaciona cliente, operador y ruta. | Claves foráneas válidas para cliente y operador. | Cliente, Operador | Alta | backend |
| Listar viajes | Endpoint e interfaz para ver historial de viajes. | Permitir filtros por fecha, cliente u operador. | Viaje | Alta | backend |
| UI viajes | Tabla de viajes en la interfaz. | Orden predeterminado por fecha; paginación. | API viajes | Media | frontend |

### EPIC: Seguridad y Multi-tenant

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Implementar RLS PostgreSQL | Configurar Row-Level Security para aislar datos por empresa. | Pruebas que demuestren el aislamiento correcto. | Base de datos | Alta | backend, security |
| Soft delete global | Añadir campo deleted_at para eliminación lógica. | No se elimina físicamente ningún registro. | Base de datos | Alta | backend |
| Validación empresa en endpoints | Middleware que restringe el acceso a recursos de otras empresas. | Asegura que el empresa_id del token corresponde a los datos solicitados. | Auth | Alta | backend |

### EPIC: Mapas

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Configurar Leaflet | Configurar librería Leaflet en el frontend. | El mapa se muestra correctamente y carga sin errores. | Frontend | Alta | frontend |
| Dibujar rutas | Dibujar polylines de rutas en el mapa. | Las rutas son visibles y se ajustan al mapa. | Rutas | Media | frontend |

### EPIC: Premium (Post-MVP)

#### Feature: Tracking (Post-MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Estados de viaje | Definir el flujo de estados del viaje (p. ej. pendiente, en curso, finalizado). | Transiciones válidas entre estados. | Viaje | Media | backend |
| Tracking en mapa | Mostrar la posición en tiempo real del vehículo. | Actualización dinámica de la posición. | GPS | Baja | frontend |

#### Feature: Puntos GPS (Post-MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad PuntoInteres | Modelo para puntos de interés (POIs). | Contiene tipos definidos de POI. | Empresa | Media | backend |
| CRUD POIs | Endpoints para gestionar puntos de interés. | Validaciones de entrada y logs. | PuntoInteres | Media | backend |
| Mostrar POIs | Visualizar POIs en el mapa Leaflet. | Filtrado por tipo y empresa. | Leaflet | Media | frontend |

#### Feature: Flota (Post-MVP)

| Task | Description | Acceptance criteria | Dependencies | Priority | Labels |
| --- | --- | --- | --- | --- | --- |
| Entidad Vehiculo | Modelo para datos de vehículos (placa, modelo, capacidad, etc.). | La placa es única por empresa. | Empresa | Media | backend |
| CRUD vehículos | Endpoints para gestionar vehículos. | Registro de auditoría y validación de datos. | Vehículo | Media | backend |
| Alertas mantenimiento | Lógica para detectar y notificar necesidad de mantenimiento. | Enviar notificaciones de mantenimiento a responsables. | Vehículo | Baja | backend |

## Cómo usar esta lista

Cada fila de las tablas representa un issue que puede crearse en GitHub. El título del issue debería ser el nombre de la tarea; la descripción del issue puede incluir la descripción, criterios de aceptación, dependencias, prioridad y etiquetas.

También se recomienda agrupar los issues mediante labels de GitHub, por ejemplo:

- `epic/control-plane`
- `feature/onboarding`
- `priority/alta`

Esto facilita el seguimiento del roadmap y el avance por fases.
