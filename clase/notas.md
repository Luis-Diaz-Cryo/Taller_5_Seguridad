# 📝 Notas de Clase — Taller 5: Evaluación de Seguridad con STRIDE

## Flujo Seleccionado

**Autenticación y Acceso a Cursos**

### Justificación de la selección

Se seleccionó este flujo porque:

1. **Es el punto de entrada universal** — todo usuario (estudiante, docente, admin) debe pasar por él antes de cualquier otra operación.
2. **Concentra las amenazas más críticas** — compromete simultáneamente confidencialidad (datos del usuario), integridad (acceso a cursos correctos) y disponibilidad (la plataforma depende de que el login funcione).
3. **Gestiona activos sensibles de alto valor** — credenciales, tokens de sesión, datos personales y control de acceso a contenido de pago.

---

## Diagrama del Flujo Analizado

```
[Estudiante]
    │
    ▼
[Formulario de Login]  ──── HTTPS ────►  [API de Autenticación]
                                                │
                             ┌──────────────────┤
                             ▼                  ▼
                     [Valida credenciales] [Genera JWT]
                             │
                             ▼
                    [Retorna Token JWT]
                             │
                             ▼
                    [Panel del Estudiante]
                             │
                    ┌────────┴────────┐
                    ▼                 ▼
           [Listado de Cursos]  [Perfil / Datos]
                    │
                    ▼
           [API de Contenido]
                    │
                    ▼
           [Recurso / Video / PDF]
```

---

## Metodología Aplicada

### Paso 1 — Identificación de componentes
Se listaron todos los activos involucrados en el flujo:
- Portal de Login (frontend)
- API de Autenticación (backend)
- Servicio de tokens JWT
- Sistema de logs de acceso
- Endpoint `/api/profile`
- Servidor de contenido (videos, PDFs)

### Paso 2 — Aplicación de STRIDE

Para cada componente se preguntó:

| Letra | Pregunta clave |
|-------|----------------|
| **S** | ¿Puede alguien fingir ser otro usuario o sistema? |
| **T** | ¿Pueden los datos ser alterados en tránsito o reposo? |
| **R** | ¿Puede alguien negar haber realizado una acción? |
| **I** | ¿Puede información sensible ser expuesta a quien no debe? |
| **D** | ¿Puede el servicio ser interrumpido o saturado? |
| **E** | ¿Puede alguien obtener más permisos de los que le corresponden? |

### Paso 3 — Evaluación de riesgo

**Matriz de riesgo usada:**

|                  | **Impacto Alto** | **Impacto Medio** | **Impacto Bajo** |
|------------------|-----------------|-------------------|-----------------|
| **Prob. Alta**   | 🔴 CRÍTICO       | 🟠 ALTO            | 🟡 MEDIO         |
| **Prob. Media**  | 🟠 ALTO          | 🟡 MEDIO           | 🟢 BAJO          |
| **Prob. Baja**   | 🟡 MEDIO         | 🟢 BAJO            | 🟢 BAJO          |

### Paso 4 — Estrategias de mitigación

Las mitigaciones se alinearon con:
- **OWASP Top 10 2021** (A01-A10)
- **NIST CSF** (Identify, Protect, Detect, Respond, Recover)
- **ISO/IEC 27001** controles de acceso y criptografía

---

## Hallazgos Clave del Flujo

| ID | Amenaza | Riesgo | Mitigación principal |
|----|---------|--------|---------------------|
| EC-01 | Credential-stuffing en login | 🔴 CRÍTICO | MFA + bloqueo progresivo |
| EC-02 | Manipulación de JWT | 🔴 CRÍTICO | RS256 + expiración corta |
| EC-03 | Repudio de descargas | 🟠 ALTO | Audit-logs firmados |
| EC-04 | Exposición en /api/profile | 🟠 ALTO | RBAC + filtrado de campos |
| EC-05 | Saturación del servidor | 🟠 ALTO | Rate limiting + DDoS |
| EC-06 | Escalada de rol estudiante→docente | 🔴 CRÍTICO | Validación server-side |

---

## Observaciones del Equipo

- La mayor concentración de riesgos **críticos** se da en la gestión de identidad y control de acceso.
- La ausencia de MFA es el control faltante con mayor impacto potencial.
- Los logs actuales no son suficientes para cumplir con requisitos de auditoría de la Ley 1581.
- Se recomienda priorizar la implementación de MFA y RS256 en el próximo sprint.
