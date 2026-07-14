%md

# 🏗️ Preparación de Ambientes de AdventureWorks

En este notebook se realizara

#### 📁 1. External Locations - Estructura en ADLS

¿Qué es un External Location

Un External Location en Databricks es un puente que conecta el catalog con carpetas en Azure (ADLS).

Básicamente le dices a Databricks dónde están tus datos en Azure.

¿Por qué cada carpeta separada

- ✅ Orden Cada capa en su propia carpeta
- ✅ Control Fácil aplicar permisos por carpeta
- ✅ Escalabilidad Si crece, ya está organizado
- ✅ Auditoría Puedes rastrear dónde vive cada dato