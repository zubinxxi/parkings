# Reglas de Desarrollo - Proyecto Gestión de Estacionamientos para la AMP

Este documento establece las normas estrictas de comportamiento para la generación de código y asistencia técnica.

## 1. Idioma de Interacción
- **Obligatorio:** Todas las explicaciones, comentarios de código, documentación y respuestas deben ser exclusivamente en **Español**.
- Si se detecta un término técnico sin traducción clara, se usará el término en inglés seguido de una breve explicación en español.

## 2. Fidelidad a la Documentación Oficial
El modelo DEBE regirse estrictamente por los estándares y mejores prácticas de las siguientes fuentes oficiales, evitando patrones obsoletos:

- **Backend (FastAPI):** Referenciar siempre [https://fastapi.tiangolo.com/es/](https://fastapi.tiangolo.com/es/). Priorizar el uso de Pydantic v2 y tipado estático (Type Hints).
- **Frontend (Vue.js 3):** Referenciar [https://vuejs.org/guide/quick-start.html](https://vuejs.org/guide/quick-start.html). 
Utilizar **Composition API** y la sintaxis `<script setup>`. 
Utilizar **vue-multiselect** para todos los campos de selección (Única y Multiple) referenciar [https://vue-multiselect.js.org/](https://vue-multiselect.js.org/).

- **Diseño y UI (vue-pure-admin):** Seguir la estructura de componentes de Element Plus y la plantilla basada en [https://github.com/pure-admin/vue-pure-admin](https://github.com/pure-admin/vue-pure-admin). Usar el [proyecto精简 (thin)](https://github.com/pure-admin/pure-admin-thin) como base para el desarrollo real.

## 3. Restricciones Técnicas del Entorno
- Sistema Operativo: **Debian 13**.
- Firewall: **ufw** activo (asegurar que los endpoints propuestos consideren la apertura de puertos si es necesario).
- Base de Datos: Considerar la integración con **MariaDB** según el histórico del sistema.

## 4. Uso Obligatorio de Skills del Proyecto

El proyecto cuenta con skills especializadas en `.agents/skills/`. **ES OBLIGATORIO** cargar la skill correspondiente antes de realizar cualquier tarea que coincida con su ámbito:

| Skill | Cuándo usarla |
|-------|---------------|
| **brainstorming** | Antes de cualquier trabajo creativo: nuevas features, componentes, funcionalidades o cambios de comportamiento. Explora intención, requisitos y diseño antes de implementar. |
| **fastapi** | Siempre que se trabaje con APIs FastAPI, modelos Pydantic, o rutas del backend. |
| **vue-best-practices** | Siempre que se trabaje con componentes Vue, Vue Router, Pinia, Vite + Vue, o archivos `.vue`. |
| **api-design-principles** | Al diseñar nuevas APIs REST/GraphQL, revisar especificaciones o establecer estándares de diseño de APIs. |
| **error-handling-patterns** | Al implementar manejo de errores, diseñar APIs, o mejorar la confiabilidad de la aplicación. |
| **frontend-design** | Al crear componentes web, páginas, landing pages, dashboards, componentes React, o maquetación HTML/CSS. |
| **interface-design** | Al diseñar dashboards, paneles de administración, apps o herramientas interactivas (NO para landing pages o sitios de marketing). |
| **systematic-debugging** | **SIEMPRE** ante cualquier bug, fallo de tests o comportamiento inesperado, antes de proponer correcciones. |
| **sc-security-module** | **SIEMPRE** al inicio del desarrollo del proyecto y al trabajar con autenticación, autorización RBAC, roles, permisos, grupos, usuarios del módulo de seguridad, o cualquier operación relacionada con `sec_*` / `sc_log`. |

Regla: si la tarea coincide con el ámbito de una skill, se DEBE cargar dicha skill con la herramienta `skill` antes de comenzar a trabajar.

## 5. Directrices de Modificación de Código

Estas directrices aplican a toda modificación de código, independientemente de la skill o tecnología involucrada.

### 5.1 Precisión Quirúrgica
- **Fidelidad al Alcance:** Modifica única y exclusivamente las líneas o funciones solicitadas.
- **Prohibición de Refactorización Silenciosa:** No cambies nombres de variables, estructuras de bases de datos o lógica circundante para "limpiar" el código, a menos que se pida explícitamente.
- **Preservación de Estilo:** Mantén el patrón de diseño y las convenciones de nomenclatura detectadas en el código existente (ej. CamelCase o snake_case, no los mezcles).

### 5.2 Integridad del Sistema
- **Respeto a la Arquitectura:** Antes de sugerir un cambio, analiza cómo afecta a los componentes dependientes (especialmente en entornos multi-tenant o arquitecturas de microservicios).
- **Consistencia de Datos:** Al proponer cambios en consultas SQL o esquemas, asegura la compatibilidad con los tipos de datos y relaciones existentes.
- **Comentarios de Cambio:** Si una modificación requiere ajustar una configuración en otro archivo (ej. variable de entorno o ruta), notifícalo al final de la respuesta.

### 5.3 Verificación y Comunicación
- **Confirmación de Ambigüedad:** Si una instrucción puede interpretarse de forma que rompa la compatibilidad hacia atrás, solicita aclaración antes de proceder.
- **Bloques Contextuales:** Devuelve suficiente código para entender dónde va el cambio, pero evita reescribir archivos masivos si la modificación es puntual.
- **Explicaciones Técnicas:** Proporciona una explicación breve de qué se cambió y por qué es seguro para el resto del sistema, solo si la lógica es compleja.

### 5.4 Control de Regresiones
- Antes de generar la respuesta final, verifica mentalmente que el nuevo código no altera funciones auxiliares ni dependencias compartidas.
