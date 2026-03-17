# Content Detection & Classification Rules

## When to Use This Reference

Load this reference when processing ANY document — especially documents from non-technical clients, stakeholders, or users who don't write in Agile format. These documents are often ambiguous, full of assumptions, and mix different levels of abstraction in the same paragraph.

## Document-Level Classification

First, classify the ENTIRE document:

| Signal in the document | Classification | Create |
|----------------------|----------------|--------|
| Multiple major areas/themes, product vision, roadmap | **Full PRD** | Epics → Features → Stories → Tasks |
| One major theme with sub-capabilities | **Epic description** | 1 Epic → Features → Stories → Tasks |
| One capability with detailed requirements | **Feature spec** | 1 Feature → Stories → Tasks |
| One specific behavior/need | **Single requirement** | 1 Story → Tasks |
| Error description, something broken | **Bug report** | 1 Bug |
| Action items, decisions, follow-ups | **Meeting notes** | Mixed: Stories + Tasks + Bugs |
| Vague ideas, "wouldn't it be nice if..." | **Ambiguous** | STOP → clarify first |

## Item-Level Detection (Inside the Document)

Within a document, detect what TYPE each paragraph/section/bullet is:

### Epic Signals

The text describes a **large initiative, theme, or product area** that will take multiple sprints:

| Pattern | Example from non-technical client |
|---------|----------------------------------|
| "Módulo de..." / "Sistema de..." | "Necesitamos un módulo de reportes completo" |
| "Todo lo relacionado con..." | "Todo lo relacionado con pagos y facturación" |
| A section title covering a broad area | "Gestión de Usuarios" |
| Multiple features grouped under one theme | "Para el tema de seguridad, necesitamos login, roles, auditoría..." |
| References to a product area, not a specific action | "El área de analytics" |
| Timeline: months, quarters | "Para Q3 queremos tener listo el marketplace" |

**Red flag:** If you can't build it in one sprint, it's probably an Epic, not a Feature.

### Feature Signals

The text describes a **specific capability** that delivers value but may need multiple stories:

| Pattern | Example from non-technical client |
|---------|----------------------------------|
| "[Verb] con/para [specific capability]" | "Registro de usuarios con verificación de email" |
| A concrete workflow with multiple steps | "El proceso de checkout: carrito → pago → confirmación → email" |
| Something that can be demoed in a sprint review | "Poder filtrar productos por precio y categoría" |
| A grouping of related behaviors | "Las notificaciones: email, push, y en la app" |
| References to a specific screen/page | "La página de perfil del usuario" |

**Red flag:** If it has sub-parts that each deliver value, it's a Feature containing Stories.

### User Story Signals

The text describes a **single behavior** from the user's perspective:

| Pattern | Example from non-technical client |
|---------|----------------------------------|
| "El usuario puede/debe/quiere..." | "El usuario debe poder cambiar su contraseña" |
| "Cuando [acción], [resultado]" | "Cuando busco un producto, quiero ver los resultados rápido" |
| "Necesito poder..." | "Necesito poder exportar los datos a Excel" |
| A single action with a clear outcome | "Enviar email de confirmación después de comprar" |
| "¿Se puede...?" / "Sería bueno que..." | "¿Se puede agregar un botón de favoritos?" |
| Something you can test with one scenario | "Ver mis últimas 10 transacciones" |

**Red flag:** If it needs more than 5 acceptance criteria, split into multiple stories.

### Task Signals

The text describes **technical work** that a developer would do:

| Pattern | Example |
|---------|---------|
| "Crear/Configurar/Implementar/Migrar..." | "Crear la tabla en la base de datos" |
| Infrastructure/DevOps work | "Configurar el pipeline de CI/CD" |
| Technical debt / refactoring | "Refactorizar el módulo de autenticación" |
| Mentions specific technologies | "Instalar Redis para cache" |
| No direct user-facing value | "Actualizar las dependencias de npm" |

**Note:** Tasks should always be children of a Story. If a task appears standalone, create a parent Story first.

### Bug Signals

The text describes **something broken** or behaving incorrectly:

| Pattern | Example from non-technical client |
|---------|----------------------------------|
| "No funciona..." / "No sirve..." | "No funciona el login desde el celular" |
| "Error cuando..." / "Falla al..." | "Sale error cuando intento subir una foto grande" |
| "Antes funcionaba y ahora no" | "El reporte de ventas ya no carga" |
| "Debería [X] pero hace [Y]" | "Debería mostrar el precio con IVA pero muestra sin IVA" |
| Screenshots showing errors | [Adjunto con error 500] |
| "Se cae" / "Se congela" / "Tarda mucho" | "La app se congela cuando abro el dashboard" |

### Ambiguity Signals (STOP AND ASK)

The text is too vague to classify — **do not guess**, ask:

| Pattern | What to ask |
|---------|------------|
| "Algo para..." / "Algo como..." | "¿Puedes describir qué haría el usuario exactamente?" |
| "Mejorar [X]" (sin especificar cómo) | "¿Qué significa 'mejorar'? ¿Más rápido? ¿Más fácil de usar? ¿Más datos?" |
| "Que sea mejor" / "Que sea más bonito" | "¿Puedes dar un ejemplo de cómo se vería 'mejor'? ¿Hay algún referente?" |
| "Algo parecido a [competitor]" | "¿Qué funcionalidad específica de [competitor] quieres replicar?" |
| "Automatizar [proceso vago]" | "¿Cuáles son los pasos manuales que se hacen hoy?" |
| Conditional / uncertain language | "'Tal vez necesitemos...' / 'Quizás...' / 'No estoy seguro si...'" → Marcar como [SUPUESTO] |
| Contradictions | "En la sección 2 dice X pero en la sección 5 dice Y — ¿cuál es correcto?" |
| Scope unclear | "¿Esto es para todos los usuarios o solo para admins?" |
| Missing acceptance criteria | "¿Cómo sabemos que esto está 'terminado'? ¿Qué debe pasar exactamente?" |

## Non-Technical Client Language Translation

Common phrases from non-technical stakeholders and what they actually mean:

| Client says | Actually means | Create as |
|------------|---------------|-----------|
| "Quiero una app" | Un producto completo con múltiples módulos | Multiple Epics |
| "Necesito un dashboard" | Una página con gráficos y métricas | 1 Feature → varias Stories |
| "Que se pueda compartir" | Funcionalidad de sharing (email, link, social) | 1 Feature |
| "Que sea rápido" | Requisito no funcional de performance | AC en cada Story: "carga en < 2s" |
| "Que sea seguro" | Auth + authorization + encryption + audit | 1 Epic (Seguridad) |
| "Que se vea bien en el celular" | Diseño responsivo | AC en cada Story: "funciona en mobile 375px+" |
| "Integración con [X]" | API integration con servicio externo | 1 Feature → Stories por cada endpoint |
| "Como lo tiene [competidor]" | Replicar funcionalidad específica | Investigar qué hace el competidor → Features/Stories |
| "Que notifique" | Sistema de notificaciones (email/push/in-app) | 1 Feature → 1 Story por canal |
| "Un reporte de..." | Vista con datos filtrados/agrupados + posible export | 1 Feature (filtros + vista + export) |
| "Que sea automático" | Background job o trigger-based workflow | 1 Feature → Stories: trigger, proceso, notificación, retry |
| "Control de acceso" | RBAC (roles + permisos + vistas filtradas por rol) | 1 Epic si es complejo, 1 Feature si es simple |

## Decomposition Rules

### When to split an Epic into Features:
- Has 3+ distinct capabilities that can be delivered independently
- Spans more than 2-3 sprints
- Different team members would work on different parts

### When to split a Feature into Stories:
- Has multiple user-facing behaviors
- Can be released incrementally (Story 1 adds value even without Story 2)
- Different acceptance criteria groups (happy path, error handling, edge cases = separate stories)

### When to split a Story:
- More than 5 acceptance criteria → split by scenario
- More than 8 story points → split by path (happy path vs error handling)
- Multiple user roles involved → 1 story per role
- Uses SPIDR method:
  - **S**pike: Need research first? Create a spike story
  - **P**aths: Split by happy path, error path, edge cases
  - **I**nterface: Split by platform (web, mobile, API)
  - **D**ata: Split by data source or data type
  - **R**ules: Split by business rule

### When NOT to split:
- The story is already 1-3 points
- Splitting would create stories that don't deliver value alone
- The "stories" would be tasks (implementation steps, not user behaviors)

## Assumption Handling

When the document has implicit assumptions or gaps:

1. **Identify** every assumption you're making
2. **Mark clearly** with `[SUPUESTO]` prefix in the description:
   ```
   [SUPUESTO] Se asume que el usuario ya está autenticado al acceder a esta página.
   [SUPUESTO] Se asume que el formato de exportación es CSV. Confirmar con el cliente.
   [SUPUESTO] El documento no especifica qué pasa si el pago falla. Se asume redirect a página de error.
   ```
3. **Group assumptions** at the end of the plan before presenting to user:
   ```
   ## Supuestos a confirmar (X items)
   - [ ] El rol principal es "inversor" (no se especificó)
   - [ ] Los reportes se generan diariamente (no se especificó frecuencia)
   - [ ] El presupuesto permite API de pago externa (Stripe/PayPal)
   ```
4. **Let the user decide**: confirm, reject, or defer each assumption
5. **Tag** all items created with assumptions: tag `tiene-supuestos` for easy filtering

## Mixed Documents

Some documents mix everything — features, bugs, ideas, technical debt. Process them in this order:

1. **First pass:** Read the entire document, mark each section/paragraph with its type
2. **Group:** Organize by type (Epics → Features → Stories → Bugs → Ambiguous)
3. **Present the classification** to the user before creating anything:
   ```
   He analizado el documento y clasifico el contenido así:

   📦 Epics (2):
     1. Sistema de reportes
     2. Módulo de notificaciones

   🔧 Features (5):
     1. Dashboard de métricas (bajo Epic 1)
     2. Exportación a Excel (bajo Epic 1)
     ...

   📝 User Stories (8):
     1. Ver resumen de ventas del mes (bajo Feature 1)
     ...

   🐛 Bugs (3):
     1. Login falla en Safari
     ...

   ❓ Necesitan clarificación (4):
     1. "Que sea más intuitivo" — ¿qué significa exactamente?
     ...

   ¿Está correcta esta clasificación? ¿Quieres ajustar algo?
   ```
4. **Wait for approval** of the classification before creating items
