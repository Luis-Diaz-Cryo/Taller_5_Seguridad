# 🔐 Taller 5 — Evaluación de Seguridad con STRIDE

**EdukIT · Plataforma de Educación Virtual**  
Arquitectura Empresarial — Universidad de La Sabana

---

## 🎯 Descripción

Análisis de riesgos de seguridad aplicando el marco **STRIDE** sobre cuatro flujos críticos de EdukIT, una plataforma de educación online para estudiantes en América Latina. El sistema gestiona acceso a cursos, publicación de contenido educativo, procesamiento de pagos y almacenamiento de datos personales y académicos.

---

## 📁 Estructura del Repositorio

```
taller-05-seguridad-stride/
├── README.md                          ← Este archivo
├── clase/
│   ├── tabla-stride-clase.xlsx        ← Análisis STRIDE: Flujo de Autenticación
│   └── notas.md                       ← Metodología y observaciones de clase
└── entrega/
    ├── tabla-stride-cliente.xlsx      ← Análisis STRIDE completo (4 flujos)
    ├── informe.md                     ← Informe técnico de seguridad
    └── referencias.md                 ← Buenas prácticas y normativas citadas
```

---

## 🔎 Flujos Analizados

| Flujo | Descripción | Amenazas |
|-------|-------------|----------|
| **F1** | Autenticación y Acceso a Cursos | 4 |
| **F2** | Publicación de Contenido por Docentes | 3 |
| **F3** | Procesamiento de Pagos | 3 |
| **F4** | Datos Personales y Académicos | 4 |
| **Total** | | **14** |

---

## 🚨 Resumen de Hallazgos

| Nivel | Cantidad | Acción requerida |
|-------|----------|-----------------|
| 🔴 CRÍTICO | 7 | Mitigación inmediata (sprint actual) |
| 🟠 ALTO | 6 | Mitigación en 30 días |
| 🟡 MEDIO | 1 | Planificar en 90 días |

**Principales riesgos identificados:**
- Ausencia de MFA en login de estudiantes y docentes
- Tokens JWT vulnerables a manipulación de payload
- SQL Injection en módulo de búsqueda de usuarios
- Monto de pagos manipulable desde el cliente
- Panel de administración accesible sin validación de rol en servidor

---

## 🛡️ Marco STRIDE

| Letra | Categoría | Propiedad vulnerada |
|-------|-----------|---------------------|
| **S** | Spoofing | Autenticación |
| **T** | Tampering | Integridad |
| **R** | Repudiation | No repudio |
| **I** | Information Disclosure | Confidencialidad |
| **D** | Denial of Service | Disponibilidad |
| **E** | Elevation of Privilege | Autorización |

---

## 📋 Referencias Principales

- OWASP Top 10 2021 — https://owasp.org/Top10/
- NIST Cybersecurity Framework 2.0 — https://www.nist.gov/cyberframework
- Ley 1581 de 2012 — Protección de Datos Personales (Colombia)
- ISO/IEC 27001:2022
- PCI-DSS v4.0

---

## ✅ Licencia

Este taller hace parte del curso de Arquitectura Empresarial — Universidad de La Sabana.  
Uso académico bajo licencia **MIT**.
