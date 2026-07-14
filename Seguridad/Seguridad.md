%md

### 🔐 Roles y Governance - AdventureWorks

¿Por qué necesitamos roles?

Con la premisa de mínimo acceso de datos, se establece que no todos necesitan tener los mismos permisos:


- **Data Engineers** necesitan crear y modificar tablas (trabajo técnico)
- **Data Analysts** solo necesitan leer datos finales (Gold) para hacer reportes
- **Data Governance** necesita monitorear y auditar (solo lectura)


##  Estructura de roles en Adventure Works

Existen 3 grupos con permisos diferentes:

---
 

| Grupo | Nomenclatura | ¿Qué hacen? | ¿Dónde acceden? | Permisos |
|-------|--------------|----------|-----------------|----------|
| **Data Engineers** | `advwks_DE` | Crean/modifican tablas | Todo: Bronze → Silver → Gold | CREATE, ALTER, DELETE, SELECT |
| **Data Analysts** | `advwks_DA` | Hacen reportes/análisis | Solo Golden (Gold) | SELECT (solo lectura) |
| **Data Governance** | `advwks_DG` | Monitorean y auditan | Todo el catálogo | SELECT (solo lectura) |

---

**¿Qué significa cada permiso?**

| Permiso |¿Qué permite? | ¿Quién lo tiene? |
|---------|-------------|-----------------|
| **CREATE** | Crear nuevas tablas | Data Engineers |
| **ALTER** | Modificar estructura de tablas | Data Engineers  |
| **DELETE** | Eliminar tablas/datos | Data Engineers |
| **SELECT** | Leer datos (consultas) | Todos  |
| **INSERT/UPDATE** | Insertar/actualizar datos | Data Engineers |

---

**Quién accede a dónde**

```
CATALOG: cat-advw-d
│
├── 🔴 BRONZE (ingesta)
│   ├── Data Engineers    → CREATE, ALTER, DELETE, SELECT ✅
│   ├── Data Analysts     → ❌ (Sin acceso)
│   └── Data Governance   → SELECT (solo lectura) ✅
│
├── 🟡 SILVER (transformaciones)
│   ├── Data Engineers    → CREATE, ALTER, DELETE, SELECT ✅
│   ├── Data Analysts     → ❌ (Sin acceso)
│   └── Data Governance   → SELECT (solo lectura) ✅
│
└── 🟢 GOLDEN (análisis)
    ├── Data Engineers    → CREATE, ALTER, DELETE, SELECT ✅
    ├── Data Analysts     → SELECT (lectura) ✅
    └── Data Governance   → SELECT (lectura) ✅
```

---
**¿Por qué está estructurado así?**

- 🛠️ **Data Engineer** (advwks_DE) → Admin
Necesitan acceso total para construir la arquitectura
Ingestión, transformaciones, mantenimiento
Responsables de la calidad técnica

- 📊 **Data Analyst** (advwks_DA) → Lectura en Gold
Solo necesitan datos finales listos para análisis
No tocan tablas crudas (no necesitan Bronze/Silver)
Protege la integridad de datos de ingesta

- 📜 **Data Governance** (advwks_DG) → Auditoría
Monitorea uso, cambios, accesos
Solo lectura en todo (no modifica nada)
Garantiza cumplimiento y trazabilidad

**Beneficios**

- ✅ Seguridad: Datos protegidos por roles
- ✅ Orden: Cada grupo sabe sus privilegios
- ✅ Auditoría: Se puede rastrear las actividades
- ✅ Escalabilidad: Si crece el equipo, se aplica el mismo patrón sobre un usuario en particular
- ✅ Compliance: Se garantiza el cumplemiento de regulaciones de acceso de datos
---

 ![image_1783472498726.png](./image_1783472498726.png "image_1783472498726.png")
