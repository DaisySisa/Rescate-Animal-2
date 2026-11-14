# 🐾 Sistema de Gestión de Casos - Refugio Animal

Sistema integral diseñado para centralizar, organizar y dar seguimiento en tiempo real a los casos de rescate, atención veterinaria y procesos de adopción de animales en un refugio.

---

## 📋 Descripción del Problema y Alcance

Los refugios animales suelen gestionar reportes de rescate mediante canales dispersos, lo que dificulta el seguimiento clínico y la coordinación entre el personal. Este proyecto resuelve dicha problemática mediante una arquitectura modular que controla el ciclo de vida completo de cada animal desde su ingreso hasta su adopción.

### 👥 Actores del Sistema
* **Ciudadano / Reportante:** Registra alertas de animales en situación de riesgo o abandono.
* **Voluntario / Veterinario:** Recibe notificaciones de nuevos casos, actualiza diagnósticos médicos y gestiona el estado de recuperación.
* **Administrador del Refugio:** Supervisa la operatividad general, asigna personal a los casos y autoriza los procesos de adopción.

### ⚙️ Requerimientos Funcionales Principales
1. **Registro de Casos:** Creación de expedientes con ubicación, estado inicial y evidencia del rescate.
2. **Categorización por Especies:** Clasificación estructurada para **Perros**, **Gatos** y **Fauna Silvestre**, adaptando los protocolos de atención según la especie.
3. **Asignación de Personal:** Vinculación directa de veterinarios y voluntarios responsables por cada caso activo.
4. **Control de Estados:** Trazabilidad completa a través de las etapas: `Rescatado` ➔ `En Tratamiento` ➔ `En Adopción` ➔ `Adoptado`.

---

## 🏗️ Arquitectura y Patrones de Diseño

El sistema está estructurado bajo el patrón arquitectónico **MVC (Modelo-Vista-Controlador)** e implementa tres patrones de diseño clásicos de ingeniería de software para garantizar escalabilidad, bajo acoplamiento y mantenibilidad:

| Patrón de Diseño | Ubicación en el Código | Justificación Técnica y Función |
| :--- | :--- | :--- |
| **Singleton** | `src/config/DatabaseConnection.js` | Garantiza una única instancia centralizada de conexión hacia el motor de almacenamiento de expedientes, evitando duplicidad de registros y conflictos de concurrencia. |
| **Factory Method** | `src/factories/ExpedienteFactory.js` | Encapsula la lógica de instanciación polimórfica para crear expedientes especializados (Perro, Gato, Fauna Silvestre) con sus propios requisitos clínicos sin acoplar el código cliente. |
| **Observer** | `src/observers/NotificadorVoluntarios.js` | Implementa un mecanismo reactivo de suscripción que alerta automáticamente a los voluntarios y veterinarios disponibles cada vez que se registra un nuevo rescate o cambia un estado crítico. |

---

## 📂 Estructura del Proyecto

```text
Rescate-Animal-2/
├── docs/                  # Documentación técnica y diagramas UML (Casos de uso, Clases, Secuencia)
├── src/
│   ├── config/            # Configuración global e instancia única (Singleton)
│   ├── controllers/       # Lógica de control y flujo de peticiones (MVC)
│   ├── factories/         # Fábricas de creación de expedientes por especie (Factory Method)
│   ├── models/            # Entidades del dominio (Animal, Expediente, Usuario)
│   └── observers/         # Gestión de eventos y alertas automáticas (Observer)
└── README.md              # Documentación principal del repositorio
