# soyetoor.github.io

## Campo de texto

<textarea rows="40" cols="140">
ChatsFuentesBacklog Completo — SaaS Multiempresa de Tarificación Logística
Epics: 13 — Features: 51 — Tasks: 112 — Total: 163

E01 — Descubrimiento, alcance y arquitectura base
F001 Definir alcance funcional MVP vs Premium

T001 Documentar módulos MVP (tarificación, rutas, viajes, clientes, operadores)
T002 Documentar módulos Premium (tracking, GPS, flota, puntos interés)
T003 Definir matriz de exclusiones y supuestos del MVP
T004 Revisión de diferencias funcionales entre roles y planes

F002 Diseñar arquitectura Clean Architecture para monolito modular

T005 Definir capas (domain, application, infrastructure, interfaces)
T006 Establecer convenciones de boundaries y dependencias
T007 Diagramar flujogramas de entrada/salida por módulo
T008 Definir guía de desacoplamiento por dominio

F003 Definir modelo de datos inicial en PostgreSQL

T009 Diseñar entidades core con empresa_id multi-tenant
T010 Diseñar relaciones y claves externas
T011 Definir estrategia de migraciones versionadas
T012 Validar normalización y performance

F004 Definir estrategia de ambientes (dev/staging/prod)

T013 Documentar variables de entorno por ambiente
T014 Separar archivos de configuración
T015 Definir procedimientos de migración por ambiente
T016 Establecer controles de acceso por ambiente

E02 — Multi-tenant, identidad y seguridad
F005 Implementar esquema multiempresa por empresa_id

T017 Incorporar empresa_id en tablas transaccionales
T018 Agregar empresa_id a índices y constraints
T019 Definir migración y data legacy
T020 Documentar ejemplos de query multi-tenant

F006 Habilitar Row-Level Security (RLS) en PostgreSQL

T021 Crear políticas RLS por tabla multi-tenant
T022 Implementar contexto de tenant en conexión DB
T023 Establecer tests de aislamiento de datos
T024 Revisar bypass y riesgos de backdoors

F007 Autenticación y autorización basada en roles

T025 Implementar login JWT y refresh tokens
T026 Definir estructura RBAC (superadmin, admin empresa, operador, analista)
T027 Socializar roles y permisos en documentación
T028 Seguridad en endpoints administrativos

F008 Hardening de seguridad y cumplimiento mínimo

T029 Configurar rate limiting (IP/empresa/rol)
T030 Configurar CORS y headers seguros (Helmet)
T031 Definir política de contraseñas y rotación
T032 Añadir validación y sanitización de payloads
T033 Implementar hashing/cifrado fuerte de passwords y datos sensibles
T034 Revisión contra OWASP Top 10

E03 — Catálogos de negocio y operación logística
F009 Gestión de clientes por empresa

T035 Crear CRUD de clientes con validaciones fiscales
T036 Agregar importación masiva CSV de clientes
T037 Implementar búsqueda y filtros por estatus

F010 Gestión de operadores (choferes)

T038 Crear CRUD de operadores
T039 Validar vencimiento de licencias/certificados médicos
T040 Alertar expiraciones próximas

F011 Gestión de bases logísticas y patios

T041 Crear CRUD de bases con georreferencia
T042 Evitar duplicados geográficos por empresa
T043 Asociar bases a rutas y zonas operativas

F012 Gestión de unidades y parámetros de rendimiento

T044 Crear catálogo de unidades y tipos de carga
T045 Configurar rendimiento de combustible por unidad
T046 Registrar fichas técnicas y documentos de unidad
T047 Implementar soft delete transversal

E04 — Motor de rutas y tarificación (INEGI + costos)
F013 Ingesta y normalización de datos oficiales INEGI

T048 Definir pipeline de carga de datasets INEGI
T049 Crear proceso de actualización periódica de datos
T050 Normalizar datos para queries de ruteo

F014 Cálculo de rutas óptimas (cuota y libres)

T051 Implementar algoritmo de enrutamiento base
T052 Incluir opción comparativa cuota vs libre
T053 Agregar fallback cuando falte tramo oficial
T054 Testear precisión vs rutas reales

F015 Cálculo de peajes y costos carreteros

T055 Modelar peajes por tramo y tipo de vehículo
T056 Implementar cálculo agregado por viaje
T057 Guardar históricos de peaje (Post-MVP)

F016 Estimación de combustible y costo operativo real

T058 Integrar rendimiento por unidad en cálculo
T059 Incorporar precio de combustible configurable
T060 Integrar consulta a API (INEGI/externa) de precios combustible (Premium)
T061 Guardar histórico de precios consultados (Premium)

F017 Motor de cotización versionado y auditable

T062 Generar desglose detallado por componente de costo
T063 Guardar parámetros versión por cotización
T064 Auditar cambios en cotización vs precios históricos

E05 — Viajes, trazabilidad y operación diaria
F018 Registro de viajes end-to-end

T065 Crear flujo alta/edición/cierre de viaje
T066 Relacionar viaje con cliente, operador y unidad
T067 Guardar costos y cotización seleccionada
T068 Registrar hitos operativos (salida/llegada/paradas)

F019 Trazabilidad de eventos del viaje

T069 Implementar timeline de eventos con timestamps
T070 Auditar cambios de estado del viaje
T071 Permitir comentarios o anotaciones en eventos

F020 Evidencias y documentos del viaje

T072 Permitir adjuntar documentos y comprobantes
T073 Validar y versionar archivos subidos
T074 Definir política de retención documental

F021 Incidencias y excepciones operativas

T075 Crear catálogo de incidencias tipificadas
T076 Permitir apertura y cierre de incidencias ligadas a viaje
T077 Notificar a supervisores según gravedad

E06 — Funcionalidades premium: tracking, GPS y flota
F022 Tracking de viajes en tiempo real

T078 Implementar canal de actualización en tiempo real (WebSocket/REST)
T079 Mostrar estado y ubicación actual del viaje
T080 Configurar permisos por plan funcional

F023 Gestión de puntos GPS

T081 Modelar almacenamiento eficiente por viaje
T082 Definir reglas de muestreo y compresión
T083 Highlight puntos críticos (paradas, excesos velocidad)

F024 Mapa de trazas y replay de recorrido

T084 Visualización histórica de ruta recorrida
T085 Agregar replay por rango de tiempo
T086 Exportar trazas en formatos estándar

F025 Gestión de flota premium

T087 Dashboard de utilización de unidades
T088 Alertas de mantenimiento preventivo
T089 Registrar historial de servicios
T090 Selección avanzada de unidad para cotizar viaje

E07 — Superadministrador, onboarding e impersonation
F026 Onboarding de nuevas empresas

T091 Flujo de alta de empresa y datos iniciales
T092 Provisionar configuración inicial por tenant
T093 Enviar invitación y seguimiento de registro
T094 Validación de dominio correo vs nombre empresa

F027 Panel de superadministrador global

T095 Vista consolidada de empresas activas/inactivas
T096 Filtros por plan, estado y actividad reciente
T097 Métricas rápidas de uso por tenant
T098 Cambios de plan y reactivación/suspensión

F028 Impersonation mode seguro

T099 Implementar acceso temporal como usuario empresa
T100 Aviso visual de sesión impersonada
T101 Registrar historial y trazabilidad completa
T102 Limitar operaciones sensibles bajo impersonation

F029 Auditoría global multiempresa

T103 Centralización eventos críticos seguridad y negocio
T104 Habilitar logs de cambios y acceso por empresa/actor
T105 Consulta avanzada filtrada por rango fechas/entidad
T106 Exportar registros en CSV/XML

E08 — Planes, suscripciones y Stripe
F030 Modelo de planes y límites por funcionalidad

T107 Definir planes (Starter, Growth, Premium, Custom)
T108 Definir límites por módulo funcional y consumo
T109 Implementar middleware de chequeo de límites
T110 UI para upgrade/downgrade

F031 Integración de checkout y suscripciones con Stripe

T111 Implementar alta de suscripción desde portal
T112 Soporte a prueba gratis / upgrade inmediato
T113 Gestionar cambios de plan prorrateados
T114 UI para gestión y actualización de método pago

F032 Webhooks Stripe y sincronización de estado

T115 Crear endpoint seguro de webhooks Stripe
T116 Sincronizar automáticamente estado de suscripción
T117 Notificar pagos fallidos o renovaciones

F033 Facturación, cancelaciones y reintentos

T118 Implementar flujo de cancelación controlado
T119 Gestionar reintentos de cobranza básica
T120 Visualización historial y facturas en UI

E09 — Frontend React 18 + Leaflet
F034 Shell de aplicación y navegación principal

T121 Configurar estructura modular y rutas protegidas
T122 Implementar layout base con menú lateral y superior
T123 Adaptación responsive (mobile/desktop)
T124 Personalización de tema por empresa

F035 Módulo de mapas con Leaflet

T125 Integrar Leaflet con proveedor de tiles personalizable
T126 Visualizar rutas (cuota/libre) y marcadores de origen/destino
T127 Soporte a iconos personalizados y layers
T128 Exportar vista del mapa como imagen

F036 Pantallas de cotización y detalle de costos

T129 Formulario para datos de cotización
T130 Renderizado de desglose de costos por ruta
T131 Comparador 3 rutas vs criterios (tiempo, costo, distancia)
T132 Acciones “Seleccionar”, “Exportar” y feedback inmediato

F037 Pantallas de viajes, tracking y operación

T133 Tablero de viajes activos/finalizados
T134 Vista de tracking en mapa e info complementaria
T135 Filtro por fechas, operador, cliente
T136 Acciones rápidas: cerrar viaje, exportar reporte

E10 — Backend Node.js/Express por módulos
F038 Estructura de monolito modular en Express

T137 Crear módulos desacoplados por dominio
T138 Separar controladores, rutas, servicios y repositorios
T139 Pruebas de integración básica por módulo
T140 Contratos de entrada/salida, validador central

F039 API de tarificación y rutas

T141 Endpoint de cálculo de ruta/costo
T142 Integrar con motor INEGI y FuelService
T143 Implementar validaciones y manejo de errores
T144 Versionado del endpoint y documentación

F040 API de catálogos y operación de viajes

T145 CRUD multi-tenant para clientes, operadores, unidades, bases
T146 Añadir paginación, filtros y ordenamiento
T147 Soporte para soft delete y restauración

F041 API de administración global y auditoría

T148 Endpoints exclusivos para superadmin/impersonation
T149 Endpoints de consulta/exportación de logs
T150 Gestión de triggers por evento crítico

E11 — DevOps, CI/CD y contenerización
F042 Dockerización de servicios

T151 Crear Dockerfile para backend
T152 Crear Dockerfile para frontend
T153 Generar imágenes para entornos oficiales

F043 Orquestación local con Docker Compose

T154 Definir servicios: app(s), PostgreSQL, herramientas utilitarias
T155 Configurar volúmenes, redes y persistencia
T156 Script de inicialización para startup local

F044 Pipeline CI (lint, test, build)

T157 Configurar workflow de CI en GitHub Actions
T158 Ejecutar linters y tests unitarios automáticamente
T159 Publicar artefactos/builds según rama y entorno

F045 Pipeline CD a staging y producción

T160 Automatizar despliegue a entorno staging
T161 Automatizar despliegue a producción (aprobación manual)
T162 Pipeline rollback y monitoreo de rollback

E12 — Observabilidad, soporte y operación
F046 Logging estructurado y correlación

T163 Implementar trazas request-id por petición
T164 Estandarizar niveles de log por módulo
T165 Centralizar logs backend en servicio externo (opcional)

F047 Métricas y monitoreo básico

T166 Exponer endpoint /health y métricas básicas
T167 Configurar alertas por disponibilidad y errores críticos
T168 Documentar procedimientos de monitoreo

F048 Backups, recuperación y continuidad

T169 Definir política y periodicidad de backups PostgreSQL
T170 Probar restauración de backup en staging
T171 Automatizar backup y notificaciones de éxito/fallo

E13 — QA, datos de prueba y salida a producción
F049 Estrategia de testing por capas

T172 Pruebas unitarias por dominio crítico
T173 Pruebas integración API+DB
T174 Pruebas E2E de flujo cotización-viaje
T175 Scripts automatizados para regresión

F050 UAT multiempresa y checklist de release

T176 Ejecutar UAT con escenarios por tipo de cliente
T177 Crear checklist go-live técnico y operativo
T178 Cierre post-mortem de pruebas

F051 Plan de adopción, capacitación y handoff

T179 Crear guía de operación para admins de empresa
T180 Crear guía de superadmin y soporte L1/L2
T181 Definir plan de capacitación inicial post-lanzamiento

Resumen
Épicas: 13
Features: 51
Tasks: 112
Total Features+Tasks: 163

Dependencias clave
E01 → E02/E10
E02/E03 → E04/E05
E04/E05 → E09/E10
E07/E08 → lanzamiento comercial multiempresa
E11/E12/E13 → salida controlada a producción
</textarea>
