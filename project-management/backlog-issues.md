# Backlog jerárquico listo para crear issues

- Épicas: **13**
- Features: **51**
- Tasks: **181**

## Dependencias clave
- E01 → E02/E10
- E02/E03 → E04/E05
- E04/E05 → E09/E10
- E07/E08 → lanzamiento comercial multiempresa
- E11/E12/E13 → salida controlada a producción

## Orden de carga por lotes
1. Lote 1: Épicas + Features MVP
2. Lote 2: Tasks MVP críticas
3. Lote 3: Premium y optimizaciones

## Épicas, Features y Tasks

### [EPIC] E01 - Descubrimiento, alcance y arquitectura base
Labels: `type:epic`

- [FEATURE] F001 - Definir alcance funcional MVP vs Premium  _(parent: E01)_
  - [TASK] T001 - Documentar módulos MVP (tarificación, rutas, viajes, clientes, operadores)  _(parent: F001)_
  - [TASK] T002 - Documentar módulos Premium (tracking, GPS, flota, puntos interés)  _(parent: F001)_
  - [TASK] T003 - Definir matriz de exclusiones y supuestos del MVP  _(parent: F001)_
  - [TASK] T004 - Revisión de diferencias funcionales entre roles y planes  _(parent: F001)_
- [FEATURE] F002 - Diseñar arquitectura Clean Architecture para monolito modular  _(parent: E01)_
  - [TASK] T005 - Definir capas (domain, application, infrastructure, interfaces)  _(parent: F002)_
  - [TASK] T006 - Establecer convenciones de boundaries y dependencias  _(parent: F002)_
  - [TASK] T007 - Diagramar flujogramas de entrada/salida por módulo  _(parent: F002)_
  - [TASK] T008 - Definir guía de desacoplamiento por dominio  _(parent: F002)_
- [FEATURE] F003 - Definir modelo de datos inicial en PostgreSQL  _(parent: E01)_
  - [TASK] T009 - Diseñar entidades core con empresa_id multi-tenant  _(parent: F003)_
  - [TASK] T010 - Diseñar relaciones y claves externas  _(parent: F003)_
  - [TASK] T011 - Definir estrategia de migraciones versionadas  _(parent: F003)_
  - [TASK] T012 - Validar normalización y performance  _(parent: F003)_
- [FEATURE] F004 - Definir estrategia de ambientes (dev/staging/prod)  _(parent: E01)_
  - [TASK] T013 - Documentar variables de entorno por ambiente  _(parent: F004)_
  - [TASK] T014 - Separar archivos de configuración  _(parent: F004)_
  - [TASK] T015 - Definir procedimientos de migración por ambiente  _(parent: F004)_
  - [TASK] T016 - Establecer controles de acceso por ambiente  _(parent: F004)_

### [EPIC] E02 - Multi-tenant, identidad y seguridad
Labels: `type:epic`

- [FEATURE] F005 - Implementar esquema multiempresa por empresa_id  _(parent: E02)_
  - [TASK] T017 - Incorporar empresa_id en tablas transaccionales  _(parent: F005)_
  - [TASK] T018 - Agregar empresa_id a índices y constraints  _(parent: F005)_
  - [TASK] T019 - Definir migración y data legacy  _(parent: F005)_
  - [TASK] T020 - Documentar ejemplos de query multi-tenant  _(parent: F005)_
- [FEATURE] F006 - Habilitar Row-Level Security (RLS) en PostgreSQL  _(parent: E02)_
  - [TASK] T021 - Crear políticas RLS por tabla multi-tenant  _(parent: F006)_
  - [TASK] T022 - Implementar contexto de tenant en conexión DB  _(parent: F006)_
  - [TASK] T023 - Establecer tests de aislamiento de datos  _(parent: F006)_
  - [TASK] T024 - Revisar bypass y riesgos de backdoors  _(parent: F006)_
- [FEATURE] F007 - Autenticación y autorización basada en roles  _(parent: E02)_
  - [TASK] T025 - Implementar login JWT y refresh tokens  _(parent: F007)_
  - [TASK] T026 - Definir estructura RBAC (superadmin, admin empresa, operador, analista)  _(parent: F007)_
  - [TASK] T027 - Socializar roles y permisos en documentación  _(parent: F007)_
  - [TASK] T028 - Seguridad en endpoints administrativos  _(parent: F007)_
- [FEATURE] F008 - Hardening de seguridad y cumplimiento mínimo  _(parent: E02)_
  - [TASK] T029 - Configurar rate limiting (IP/empresa/rol)  _(parent: F008)_
  - [TASK] T030 - Configurar CORS y headers seguros (Helmet)  _(parent: F008)_
  - [TASK] T031 - Definir política de contraseñas y rotación  _(parent: F008)_
  - [TASK] T032 - Añadir validación y sanitización de payloads  _(parent: F008)_
  - [TASK] T033 - Implementar hashing/cifrado fuerte de passwords y datos sensibles  _(parent: F008)_
  - [TASK] T034 - Revisión contra OWASP Top 10  _(parent: F008)_

### [EPIC] E03 - Catálogos de negocio y operación logística
Labels: `type:epic`

- [FEATURE] F009 - Gestión de clientes por empresa  _(parent: E03)_
  - [TASK] T035 - Crear CRUD de clientes con validaciones fiscales  _(parent: F009)_
  - [TASK] T036 - Agregar importación masiva CSV de clientes  _(parent: F009)_
  - [TASK] T037 - Implementar búsqueda y filtros por estatus  _(parent: F009)_
- [FEATURE] F010 - Gestión de operadores (choferes)  _(parent: E03)_
  - [TASK] T038 - Crear CRUD de operadores  _(parent: F010)_
  - [TASK] T039 - Validar vencimiento de licencias/certificados médicos  _(parent: F010)_
  - [TASK] T040 - Alertar expiraciones próximas  _(parent: F010)_
- [FEATURE] F011 - Gestión de bases logísticas y patios  _(parent: E03)_
  - [TASK] T041 - Crear CRUD de bases con georreferencia  _(parent: F011)_
  - [TASK] T042 - Evitar duplicados geográficos por empresa  _(parent: F011)_
  - [TASK] T043 - Asociar bases a rutas y zonas operativas  _(parent: F011)_
- [FEATURE] F012 - Gestión de unidades y parámetros de rendimiento  _(parent: E03)_
  - [TASK] T044 - Crear catálogo de unidades y tipos de carga  _(parent: F012)_
  - [TASK] T045 - Configurar rendimiento de combustible por unidad  _(parent: F012)_
  - [TASK] T046 - Registrar fichas técnicas y documentos de unidad  _(parent: F012)_
  - [TASK] T047 - Implementar soft delete transversal  _(parent: F012)_

### [EPIC] E04 - Motor de rutas y tarificación (INEGI + costos)
Labels: `type:epic`

- [FEATURE] F013 - Ingesta y normalización de datos oficiales INEGI  _(parent: E04)_
  - [TASK] T048 - Definir pipeline de carga de datasets INEGI  _(parent: F013)_
  - [TASK] T049 - Crear proceso de actualización periódica de datos  _(parent: F013)_
  - [TASK] T050 - Normalizar datos para queries de ruteo  _(parent: F013)_
- [FEATURE] F014 - Cálculo de rutas óptimas (cuota y libres)  _(parent: E04)_
  - [TASK] T051 - Implementar algoritmo de enrutamiento base  _(parent: F014)_
  - [TASK] T052 - Incluir opción comparativa cuota vs libre  _(parent: F014)_
  - [TASK] T053 - Agregar fallback cuando falte tramo oficial  _(parent: F014)_
  - [TASK] T054 - Testear precisión vs rutas reales  _(parent: F014)_
- [FEATURE] F015 - Cálculo de peajes y costos carreteros  _(parent: E04)_
  - [TASK] T055 - Modelar peajes por tramo y tipo de vehículo  _(parent: F015)_
  - [TASK] T056 - Implementar cálculo agregado por viaje  _(parent: F015)_
  - [TASK] T057 - Guardar históricos de peaje (Post-MVP)  _(parent: F015)_
- [FEATURE] F016 - Estimación de combustible y costo operativo real  _(parent: E04)_
  - [TASK] T058 - Integrar rendimiento por unidad en cálculo  _(parent: F016)_
  - [TASK] T059 - Incorporar precio de combustible configurable  _(parent: F016)_
  - [TASK] T060 - Integrar consulta a API (INEGI/externa) de precios combustible (Premium)  _(parent: F016)_
  - [TASK] T061 - Guardar histórico de precios consultados (Premium)  _(parent: F016)_
- [FEATURE] F017 - Motor de cotización versionado y auditable  _(parent: E04)_
  - [TASK] T062 - Generar desglose detallado por componente de costo  _(parent: F017)_
  - [TASK] T063 - Guardar parámetros versión por cotización  _(parent: F017)_
  - [TASK] T064 - Auditar cambios en cotización vs precios históricos  _(parent: F017)_

### [EPIC] E05 - Viajes, trazabilidad y operación diaria
Labels: `type:epic`

- [FEATURE] F018 - Registro de viajes end-to-end  _(parent: E05)_
  - [TASK] T065 - Crear flujo alta/edición/cierre de viaje  _(parent: F018)_
  - [TASK] T066 - Relacionar viaje con cliente, operador y unidad  _(parent: F018)_
  - [TASK] T067 - Guardar costos y cotización seleccionada  _(parent: F018)_
  - [TASK] T068 - Registrar hitos operativos (salida/llegada/paradas)  _(parent: F018)_
- [FEATURE] F019 - Trazabilidad de eventos del viaje  _(parent: E05)_
  - [TASK] T069 - Implementar timeline de eventos con timestamps  _(parent: F019)_
  - [TASK] T070 - Auditar cambios de estado del viaje  _(parent: F019)_
  - [TASK] T071 - Permitir comentarios o anotaciones en eventos  _(parent: F019)_
- [FEATURE] F020 - Evidencias y documentos del viaje  _(parent: E05)_
  - [TASK] T072 - Permitir adjuntar documentos y comprobantes  _(parent: F020)_
  - [TASK] T073 - Validar y versionar archivos subidos  _(parent: F020)_
  - [TASK] T074 - Definir política de retención documental  _(parent: F020)_
- [FEATURE] F021 - Incidencias y excepciones operativas  _(parent: E05)_
  - [TASK] T075 - Crear catálogo de incidencias tipificadas  _(parent: F021)_
  - [TASK] T076 - Permitir apertura y cierre de incidencias ligadas a viaje  _(parent: F021)_
  - [TASK] T077 - Notificar a supervisores según gravedad  _(parent: F021)_

### [EPIC] E06 - Funcionalidades premium: tracking, GPS y flota
Labels: `type:epic`

- [FEATURE] F022 - Tracking de viajes en tiempo real  _(parent: E06)_
  - [TASK] T078 - Implementar canal de actualización en tiempo real (WebSocket/REST)  _(parent: F022)_
  - [TASK] T079 - Mostrar estado y ubicación actual del viaje  _(parent: F022)_
  - [TASK] T080 - Configurar permisos por plan funcional  _(parent: F022)_
- [FEATURE] F023 - Gestión de puntos GPS  _(parent: E06)_
  - [TASK] T081 - Modelar almacenamiento eficiente por viaje  _(parent: F023)_
  - [TASK] T082 - Definir reglas de muestreo y compresión  _(parent: F023)_
  - [TASK] T083 - Highlight puntos críticos (paradas, excesos velocidad)  _(parent: F023)_
- [FEATURE] F024 - Mapa de trazas y replay de recorrido  _(parent: E06)_
  - [TASK] T084 - Visualización histórica de ruta recorrida  _(parent: F024)_
  - [TASK] T085 - Agregar replay por rango de tiempo  _(parent: F024)_
  - [TASK] T086 - Exportar trazas en formatos estándar  _(parent: F024)_
- [FEATURE] F025 - Gestión de flota premium  _(parent: E06)_
  - [TASK] T087 - Dashboard de utilización de unidades  _(parent: F025)_
  - [TASK] T088 - Alertas de mantenimiento preventivo  _(parent: F025)_
  - [TASK] T089 - Registrar historial de servicios  _(parent: F025)_
  - [TASK] T090 - Selección avanzada de unidad para cotizar viaje  _(parent: F025)_

### [EPIC] E07 - Superadministrador, onboarding e impersonation
Labels: `type:epic`

- [FEATURE] F026 - Onboarding de nuevas empresas  _(parent: E07)_
  - [TASK] T091 - Flujo de alta de empresa y datos iniciales  _(parent: F026)_
  - [TASK] T092 - Provisionar configuración inicial por tenant  _(parent: F026)_
  - [TASK] T093 - Enviar invitación y seguimiento de registro  _(parent: F026)_
  - [TASK] T094 - Validación de dominio correo vs nombre empresa  _(parent: F026)_
- [FEATURE] F027 - Panel de superadministrador global  _(parent: E07)_
  - [TASK] T095 - Vista consolidada de empresas activas/inactivas  _(parent: F027)_
  - [TASK] T096 - Filtros por plan, estado y actividad reciente  _(parent: F027)_
  - [TASK] T097 - Métricas rápidas de uso por tenant  _(parent: F027)_
  - [TASK] T098 - Cambios de plan y reactivación/suspensión  _(parent: F027)_
- [FEATURE] F028 - Impersonation mode seguro  _(parent: E07)_
  - [TASK] T099 - Implementar acceso temporal como usuario empresa  _(parent: F028)_
  - [TASK] T100 - Aviso visual de sesión impersonada  _(parent: F028)_
  - [TASK] T101 - Registrar historial y trazabilidad completa  _(parent: F028)_
  - [TASK] T102 - Limitar operaciones sensibles bajo impersonation  _(parent: F028)_
- [FEATURE] F029 - Auditoría global multiempresa  _(parent: E07)_
  - [TASK] T103 - Centralización eventos críticos seguridad y negocio  _(parent: F029)_
  - [TASK] T104 - Habilitar logs de cambios y acceso por empresa/actor  _(parent: F029)_
  - [TASK] T105 - Consulta avanzada filtrada por rango fechas/entidad  _(parent: F029)_
  - [TASK] T106 - Exportar registros en CSV/XML  _(parent: F029)_

### [EPIC] E08 - Planes, suscripciones y Stripe
Labels: `type:epic`

- [FEATURE] F030 - Modelo de planes y límites por funcionalidad  _(parent: E08)_
  - [TASK] T107 - Definir planes (Starter, Growth, Premium, Custom)  _(parent: F030)_
  - [TASK] T108 - Definir límites por módulo funcional y consumo  _(parent: F030)_
  - [TASK] T109 - Implementar middleware de chequeo de límites  _(parent: F030)_
  - [TASK] T110 - UI para upgrade/downgrade  _(parent: F030)_
- [FEATURE] F031 - Integración de checkout y suscripciones con Stripe  _(parent: E08)_
  - [TASK] T111 - Implementar alta de suscripción desde portal  _(parent: F031)_
  - [TASK] T112 - Soporte a prueba gratis / upgrade inmediato  _(parent: F031)_
  - [TASK] T113 - Gestionar cambios de plan prorrateados  _(parent: F031)_
  - [TASK] T114 - UI para gestión y actualización de método pago  _(parent: F031)_
- [FEATURE] F032 - Webhooks Stripe y sincronización de estado  _(parent: E08)_
  - [TASK] T115 - Crear endpoint seguro de webhooks Stripe  _(parent: F032)_
  - [TASK] T116 - Sincronizar automáticamente estado de suscripción  _(parent: F032)_
  - [TASK] T117 - Notificar pagos fallidos o renovaciones  _(parent: F032)_
- [FEATURE] F033 - Facturación, cancelaciones y reintentos  _(parent: E08)_
  - [TASK] T118 - Implementar flujo de cancelación controlado  _(parent: F033)_
  - [TASK] T119 - Gestionar reintentos de cobranza básica  _(parent: F033)_
  - [TASK] T120 - Visualización historial y facturas en UI  _(parent: F033)_

### [EPIC] E09 - Frontend React 18 + Leaflet
Labels: `type:epic`

- [FEATURE] F034 - Shell de aplicación y navegación principal  _(parent: E09)_
  - [TASK] T121 - Configurar estructura modular y rutas protegidas  _(parent: F034)_
  - [TASK] T122 - Implementar layout base con menú lateral y superior  _(parent: F034)_
  - [TASK] T123 - Adaptación responsive (mobile/desktop)  _(parent: F034)_
  - [TASK] T124 - Personalización de tema por empresa  _(parent: F034)_
- [FEATURE] F035 - Módulo de mapas con Leaflet  _(parent: E09)_
  - [TASK] T125 - Integrar Leaflet con proveedor de tiles personalizable  _(parent: F035)_
  - [TASK] T126 - Visualizar rutas (cuota/libre) y marcadores de origen/destino  _(parent: F035)_
  - [TASK] T127 - Soporte a iconos personalizados y layers  _(parent: F035)_
  - [TASK] T128 - Exportar vista del mapa como imagen  _(parent: F035)_
- [FEATURE] F036 - Pantallas de cotización y detalle de costos  _(parent: E09)_
  - [TASK] T129 - Formulario para datos de cotización  _(parent: F036)_
  - [TASK] T130 - Renderizado de desglose de costos por ruta  _(parent: F036)_
  - [TASK] T131 - Comparador 3 rutas vs criterios (tiempo, costo, distancia)  _(parent: F036)_
  - [TASK] T132 - Acciones “Seleccionar”, “Exportar” y feedback inmediato  _(parent: F036)_
- [FEATURE] F037 - Pantallas de viajes, tracking y operación  _(parent: E09)_
  - [TASK] T133 - Tablero de viajes activos/finalizados  _(parent: F037)_
  - [TASK] T134 - Vista de tracking en mapa e info complementaria  _(parent: F037)_
  - [TASK] T135 - Filtro por fechas, operador, cliente  _(parent: F037)_
  - [TASK] T136 - Acciones rápidas: cerrar viaje, exportar reporte  _(parent: F037)_

### [EPIC] E10 - Backend Node.js/Express por módulos
Labels: `type:epic`

- [FEATURE] F038 - Estructura de monolito modular en Express  _(parent: E10)_
  - [TASK] T137 - Crear módulos desacoplados por dominio  _(parent: F038)_
  - [TASK] T138 - Separar controladores, rutas, servicios y repositorios  _(parent: F038)_
  - [TASK] T139 - Pruebas de integración básica por módulo  _(parent: F038)_
  - [TASK] T140 - Contratos de entrada/salida, validador central  _(parent: F038)_
- [FEATURE] F039 - API de tarificación y rutas  _(parent: E10)_
  - [TASK] T141 - Endpoint de cálculo de ruta/costo  _(parent: F039)_
  - [TASK] T142 - Integrar con motor INEGI y FuelService  _(parent: F039)_
  - [TASK] T143 - Implementar validaciones y manejo de errores  _(parent: F039)_
  - [TASK] T144 - Versionado del endpoint y documentación  _(parent: F039)_
- [FEATURE] F040 - API de catálogos y operación de viajes  _(parent: E10)_
  - [TASK] T145 - CRUD multi-tenant para clientes, operadores, unidades, bases  _(parent: F040)_
  - [TASK] T146 - Añadir paginación, filtros y ordenamiento  _(parent: F040)_
  - [TASK] T147 - Soporte para soft delete y restauración  _(parent: F040)_
- [FEATURE] F041 - API de administración global y auditoría  _(parent: E10)_
  - [TASK] T148 - Endpoints exclusivos para superadmin/impersonation  _(parent: F041)_
  - [TASK] T149 - Endpoints de consulta/exportación de logs  _(parent: F041)_
  - [TASK] T150 - Gestión de triggers por evento crítico  _(parent: F041)_

### [EPIC] E11 - DevOps, CI/CD y contenerización
Labels: `type:epic`

- [FEATURE] F042 - Dockerización de servicios  _(parent: E11)_
  - [TASK] T151 - Crear Dockerfile para backend  _(parent: F042)_
  - [TASK] T152 - Crear Dockerfile para frontend  _(parent: F042)_
  - [TASK] T153 - Generar imágenes para entornos oficiales  _(parent: F042)_
- [FEATURE] F043 - Orquestación local con Docker Compose  _(parent: E11)_
  - [TASK] T154 - Definir servicios: app(s), PostgreSQL, herramientas utilitarias  _(parent: F043)_
  - [TASK] T155 - Configurar volúmenes, redes y persistencia  _(parent: F043)_
  - [TASK] T156 - Script de inicialización para startup local  _(parent: F043)_
- [FEATURE] F044 - Pipeline CI (lint, test, build)  _(parent: E11)_
  - [TASK] T157 - Configurar workflow de CI en GitHub Actions  _(parent: F044)_
  - [TASK] T158 - Ejecutar linters y tests unitarios automáticamente  _(parent: F044)_
  - [TASK] T159 - Publicar artefactos/builds según rama y entorno  _(parent: F044)_
- [FEATURE] F045 - Pipeline CD a staging y producción  _(parent: E11)_
  - [TASK] T160 - Automatizar despliegue a entorno staging  _(parent: F045)_
  - [TASK] T161 - Automatizar despliegue a producción (aprobación manual)  _(parent: F045)_
  - [TASK] T162 - Pipeline rollback y monitoreo de rollback  _(parent: F045)_

### [EPIC] E12 - Observabilidad, soporte y operación
Labels: `type:epic`

- [FEATURE] F046 - Logging estructurado y correlación  _(parent: E12)_
  - [TASK] T163 - Implementar trazas request-id por petición  _(parent: F046)_
  - [TASK] T164 - Estandarizar niveles de log por módulo  _(parent: F046)_
  - [TASK] T165 - Centralizar logs backend en servicio externo (opcional)  _(parent: F046)_
- [FEATURE] F047 - Métricas y monitoreo básico  _(parent: E12)_
  - [TASK] T166 - Exponer endpoint /health y métricas básicas  _(parent: F047)_
  - [TASK] T167 - Configurar alertas por disponibilidad y errores críticos  _(parent: F047)_
  - [TASK] T168 - Documentar procedimientos de monitoreo  _(parent: F047)_
- [FEATURE] F048 - Backups, recuperación y continuidad  _(parent: E12)_
  - [TASK] T169 - Definir política y periodicidad de backups PostgreSQL  _(parent: F048)_
  - [TASK] T170 - Probar restauración de backup en staging  _(parent: F048)_
  - [TASK] T171 - Automatizar backup y notificaciones de éxito/fallo  _(parent: F048)_

### [EPIC] E13 - QA, datos de prueba y salida a producción
Labels: `type:epic`

- [FEATURE] F049 - Estrategia de testing por capas  _(parent: E13)_
  - [TASK] T172 - Pruebas unitarias por dominio crítico  _(parent: F049)_
  - [TASK] T173 - Pruebas integración API+DB  _(parent: F049)_
  - [TASK] T174 - Pruebas E2E de flujo cotización-viaje  _(parent: F049)_
  - [TASK] T175 - Scripts automatizados para regresión  _(parent: F049)_
- [FEATURE] F050 - UAT multiempresa y checklist de release  _(parent: E13)_
  - [TASK] T176 - Ejecutar UAT con escenarios por tipo de cliente  _(parent: F050)_
  - [TASK] T177 - Crear checklist go-live técnico y operativo  _(parent: F050)_
  - [TASK] T178 - Cierre post-mortem de pruebas  _(parent: F050)_
- [FEATURE] F051 - Plan de adopción, capacitación y handoff  _(parent: E13)_
  - [TASK] T179 - Crear guía de operación para admins de empresa  _(parent: F051)_
  - [TASK] T180 - Crear guía de superadmin y soporte L1/L2  _(parent: F051)_
  - [TASK] T181 - Definir plan de capacitación inicial post-lanzamiento  _(parent: F051)_

