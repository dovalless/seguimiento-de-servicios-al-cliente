# 📞 ZAKIDATA Empowordato - Seguimiento de Servicios de Atención al Cliente

<div align="center">

**Dashboard Interactivo para el Monitoreo y Análisis del Servicio de Atención al Cliente**

[![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)](https://powerbi.microsoft.com/)
[![Customer Service](https://img.shields.io/badge/Atención_al_Cliente-Expert-0078D4?style=for-the-badge)](https://powerbi.microsoft.com/)
[![Service Analytics](https://img.shields.io/badge/Análisis_de_Servicio-Dashboard-FF6B6B?style=for-the-badge)](https://powerbi.microsoft.com/)
[![Licencia](https://img.shields.io/badge/Licencia-MIT-yellow?style=for-the-badge)](LICENSE)

[🚀 Características](#-características) • [📊 Instalación](#-instalación) • [🏗️ Arquitectura](#️-arquitectura) • [🎨 Diseño](#-diseño-del-dashboard) • [📈 Métricas](#-métricas-analizadas) • [👨‍💻 Autor](#-autor)

</div>

---

## 📊 Descripción del Proyecto

**ZAKIDATA Empowordato - Seguimiento de Servicios** es un dashboard interactivo desarrollado en **Power BI** que permite monitorear y analizar el desempeño del servicio de atención al cliente. Este proyecto proporciona métricas clave sobre atenciones, tiempos de respuesta, satisfacción del cliente y distribución de casos por área y agente.

### 🎯 Objetivos del Proyecto
- **Monitorear el estado** de las atenciones al cliente en tiempo real.
- **Analizar la distribución** de casos por áreas específicas (Ventas, Interacciones, Reclamaciones, Cancelaciones).
- **Evaluar el desempeño** de los agentes según tiempo de atención.
- **Seguir la frecuencia** de llamadas por fecha para identificar patrones temporales.
- **Medir la satisfacción** del cliente y tiempos de espera.
- **Identificar áreas de mejora** en el servicio al cliente.

---

## 🚀 Características

### 📈 Métricas Principales
| Característica | Descripción | Estado |
|----------------|-------------|--------|
| **Estado de Atenciones** | Porcentaje de casos resueltos vs. pendientes | ✅ Implementado |
| **Distribución por Área** | Desglose de atenciones por tipo (Ventas, Interacciones, Reclamaciones, Cancelaciones) | ✅ Implementado |
| **Tiempo por Agente** | Ranking de agentes según tiempo de atención | ✅ Implementado |
| **Total por Área** | Gráfico de barras con volumen de atenciones por área | ✅ Implementado |
| **Frecuencia de Llamadas** | Serie temporal de llamadas por fecha | ✅ Implementado |
| **Métricas de Calidad** | Tiempo de espera, satisfacción y asistencias totales | ✅ Implementado |

### 🔍 Filtros e Interactividad
- **Filtro por rango de fechas** (01/03/2023 - 31/03/2023).
- **Segmentación por agente** para análisis individual.
- **Filtrado por tipo de atención** (Ventas, Interacciones, Reclamaciones, Cancelaciones).
- **Interactividad cruzada** entre gráficos para análisis detallado.
- **Tooltips informativos** con detalles específicos.

---

## 📊 Instalación

### **Requisitos Previos**
1. **Power BI Desktop** (versión más reciente recomendada)
   - Descargar desde: [Microsoft Power BI](https://powerbi.microsoft.com/desktop/)
2. **Fuente de datos** compatible (Excel, SQL Server, CRM, etc.) con datos de atención al cliente.
3. **Permisos de acceso** a los sistemas de registro de atención al cliente.

### **Pasos de Instalación**
```bash
# 1. Clonar o descargar el repositorio
git clone https://github.com/tu-usuario/zakidata-seguimiento-servicios.git
cd zakidata-seguimiento-servicios

# 2. Abrir el archivo .pbix con Power BI Desktop
# Archivo: ZAKIDATA_Seguimiento_Servicios.pbix

# 3. Configurar la conexión de datos
# - Ir a "Inicio" > "Transformar datos" > "Configuración de origen de datos"
# - Actualizar la conexión a tu fuente de datos

# 4. Actualizar los datos
# - Hacer clic en "Actualizar" en la pestaña "Inicio"

# 5. Explorar el dashboard interactivo
```

### **Estructura de Datos Requerida**
El dashboard espera datos con la siguiente estructura mínima:
- `ID_Atencion`
- `Fecha`
- `Agente`
- `Area` (Ventas, Interacciones, Reclamaciones, Cancelaciones)
- `Tiempo_Atencion` (en minutos)
- `Estado` (Resuelto, Pendiente, En proceso)
- `Tiempo_Espera` (en minutos)
- `Satisfaccion` (puntuación 1-5)
- `Tipo_Llamada`

---

## 🏗️ Arquitectura

### **Flujo de Datos**
```
Sistemas de Atención (CRM, Call Center) → Extracción de Datos → Power BI Query Editor → Modelo de Datos → Visualizaciones → Dashboard Interactivo
```

### **Modelo de Datos**
```
Tabla Principal: Atenciones_Cliente
├── Relación con: Dim_Agentes
├── Relación con: Dim_Fechas
├── Relación con: Dim_Areas
└── Relación con: Dim_Tipos_Atencion
```

### **Estructura del Proyecto**
```
ZAKIDATA_Seguimiento_Servicios/
├── data/                            # Archivos de datos de ejemplo
│   ├── atenciones_clientes.csv      # Datos principales
│   ├── agentes.csv                  # Información de agentes
│   └── areas.csv                    # Catálogo de áreas
├── docs/                            # Documentación
│   ├── manual_usuario.pdf           # Guía de uso
│   └── especificaciones_tecnicas.md
├── images/                          # Capturas y recursos
│   ├── dashboard_preview.png
│   └── diagrama_flujo.png
├── ZAKIDATA_Seguimiento_Servicios.pbix     # Archivo principal Power BI
└── README.md                        # Este archivo
```

### **Medidas DAX Principales**
```DAX
// Total de atenciones
Total_Atenciones = COUNTROWS(Atenciones_Cliente)

// Porcentaje de casos resueltos
Porcentaje_Resueltos = 
DIVIDE(
    CALCULATE(COUNTROWS(Atenciones_Cliente), Atenciones_Cliente[Estado] = "Resuelto"),
    [Total_Atenciones]
)

// Tiempo promedio de atención por agente
Tiempo_Promedio_Atencion = 
AVERAGEX(
    VALUES(Atenciones_Cliente[Agente]),
    CALCULATE(AVERAGE(Atenciones_Cliente[Tiempo_Atencion]))
)

// Satisfacción promedio
Satisfaccion_Promedio = AVERAGE(Atenciones_Cliente[Satisfaccion])
```

---

## 🎨 Diseño del Dashboard

### **Tema y Colores**
- **Esquema de colores corporativo** (azules, verdes y naranjas) que indica estados.
- **Tema claro** para máxima legibilidad de los datos.
- **Tipografía moderna** (Segoe UI) con jerarquías visuales claras.
- **Iconografía intuitiva** para una rápida identificación de métricas.

### **Layout y Organización**
El dashboard está organizado en 6 secciones principales:

1. **Encabezado y Filtros**: Período de análisis (01/03/2023 - 31/03/2023) y controles de filtrado.
2. **Métricas de Estado**: Tarjetas con porcentaje de casos resueltos vs. pendientes.
3. **Distribución por Área**: Tabla y gráficos de las atenciones por categoría.
4. **Desempeño por Agente**: Ranking de agentes según tiempo de atención.
5. **Análisis Temporal**: Gráfico de frecuencia de llamadas por fecha.
6. **Métricas de Calidad**: Tiempo de espera, satisfacción y volumen total.

### **Interactividad Avanzada**
- **Segmentación por fecha**: Control deslizante para seleccionar rangos específicos.
- **Filtros jerárquicos**: Selección por área → agente → tipo de atención.
- **Destacado cruzado**: Al seleccionar un área, se resaltan los agentes relacionados.
- **Drill-through**: Navegación desde métricas resumidas a detalles específicos.
- **Tooltips enriquecidos**: Información contextual al pasar el cursor sobre elementos.

---

## 📈 Métricas Analizadas

### **1. Estado de las Atenciones (Marzo 2023)**
- **Total de atenciones**: 1,009 casos.
- **Casos resueltos**: 74 (7.33%).
- **Casos pendientes/proceso**: 935 (92.67%).

### **2. Distribución por Área**
| Área | Cantidad | Porcentaje |
|------|----------|------------|
| **Ventas** | 411 | 40.73% |
| **Cancelaciones** | 208 | 20.61% |
| **Interacciones** | 199 | 19.72% |
| **Reclamaciones** | 191 | 18.94% |

### **3. Tiempo de Atención por Agente (Top 7)**
1. **Juan D.**: 171 minutos
2. **Leandro C.**: 153 minutos
3. **Paulo G.**: 149 minutos
4. **Marina Z.**: 148 minutos
5. **Gustavo M.**: 137 minutos
6. **Ana S.**: 136 minutos
7. **Marcelo F.**: 115 minutos

### **4. Total de Atenciones por Área (Detallado)**
- **Ventas**: 38 atenciones (máximo)
- **Interacciones**: 31 atenciones
- **Reclamaciones**: 29 atenciones
- Distribución descendente hasta 0 atenciones.

### **5. Frecuencia de Llamadas por Fecha**
- **Patrón cíclico**: Picos de hasta 40 llamadas en días específicos.
- **Tendencia**: Variabilidad diaria significativa.
- **Días con menor volumen**: Algunas fechas con 0-10 llamadas.

### **6. Métricas de Calidad del Servicio**
- **Asistencias totales**: 1,009 atenciones.
- **Satisfacción promedio**: 3.40/5 (escala 1-5).
- **Tiempo de espera promedio**: 67 minutos.

---

## 👨‍💻 Autor

<div align="center">

**Darwin Manuel Ovalles Cesar**

[![LinkedIn](https://img.shields.io/badge/LinkedIn-Perfil_Profesional-blue?style=flat&logo=linkedin)](https://www.linkedin.com/in/darwin-manuel-ovalles-cesar-dev/)
[![GitHub](https://img.shields.io/badge/GitHub-Repositorios-black?style=flat&logo=github)](https://github.com/dovalless)

💼 **Analista de Datos & Business Intelligence**  
🎓 **Especialista en Power BI y Analytics de Servicio al Cliente**  
📞 **Apasionado por la mejora de experiencias de atención al cliente**

*"Este dashboard de Power BI transforma datos crudos de atención al cliente en información accionable para mejorar la calidad del servicio. Cada métrica está diseñada para identificar oportunidades de optimización y medir el impacto de las mejoras implementadas."*

**#PowerBI #CustomerService #ServiceAnalytics #CallCenter #BusinessIntelligence**

</div>

---

## 📄 Licencia

Este proyecto está bajo la Licencia MIT. Consulta el archivo [LICENSE](LICENSE) para más detalles.

```
MIT License
Copyright (c) 2024 Darwin Manuel Ovalles Cesar
```

---

<div align="center">

### ⭐ Si este dashboard te ayuda a mejorar tu servicio al cliente, ¡dale una estrella en GitHub! ⭐

### 📞 Convierte datos de atención en experiencias excepcionales para tus clientes 📞

**Desarrollado con ❤️ y 📊 para optimizar la atención al cliente**

---
*Dashboard de seguimiento de servicios | Analytics de atención al cliente | Power BI*

</div>
