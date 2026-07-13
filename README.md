# NetFlow — De datos desordenados a un sistema que ordena, analiza y predice

Proyecto integrador de ciencia de datos aplicado a NetFlow, una empresa proveedora de servicios de internet. Incluye el diseño completo de la base de datos relacional y un modelo de machine learning para anticipar la baja de clientes.

---

## 1. El problema de negocio

NetFlow enfrentaba un problema común en empresas en crecimiento: la información estaba dispersa. No había forma de saber con certeza qué equipo tenía cada cliente, qué empleado realizó cada instalación, qué plan generaba más ingresos, o qué clientes estaban en riesgo de abandonar el servicio.

Sin datos organizados, las decisiones se tomaban a ciegas. El objetivo de este proyecto fue cambiar eso: estructurar la información, analizarla y usarla para anticipar comportamientos.

---

## 2. La base de datos

### Diseño relacional

Se diseñó una base de datos relacional que cubre las principales operaciones de NetFlow:

- **Clientes y empleados**: información personal y operativa.
- **Planes de internet**: velocidades disponibles y precios.
- **Servicios contratados**: qué plan tiene cada cliente.
- **Cablemodems y asignaciones**: control de inventario y entrega de equipos.
- **Movimientos de stock**: trazabilidad completa de entradas, salidas y bajas.

El diagrama entidad-relación completo está en [`/docs/DER_ProyectoNetFlow.png`](docs/DER_ProyectoNetFlow.png).

### Archivos SQL

| Archivo | Contenido |
|---|---|
| [`tablas_create.sql`](sql/tablas_create.sql) | Creación de todas las tablas con claves y restricciones |
| [`insertar_datos.sql`](sql/insertar_datos.sql) | Datos de ejemplo para poblar la base |
| [`vistas.sql`](sql/vistas.sql) | Vistas para consultas frecuentes (clientes-servicios, stock, asignaciones) |
| [`funciones.sql`](sql/funciones.sql) | Funciones: precio de plan, cantidad de servicios, disponibilidad de equipo |
| [`proc-almacenados.sql`](sql/proc-almacenados.sql) | Procedimientos: alta de servicio, asignación de equipo, movimientos de stock |
| [`triggers.sql`](sql/triggers.sql) | Triggers: validación y actualización automática de estados de equipos |
| [`netflow-backup.sql`](sql/netflow-backup.sql) | Backup completo de la base de datos |

---

## 3. El análisis predictivo

### Objetivo

Con la base de datos como punto de partida, el siguiente paso fue analizar el comportamiento de los clientes para anticipar quiénes tienen mayor riesgo de darse de baja.

### Proceso

El notebook [`/notebook/ProyectoNetFlow_Sanchez_Micaela.ipynb`](notebook/ProyectoNetFlow_Sanchez_Micaela.ipynb) cubre todo el flujo:

1. Carga y exploración de datos de clientes (estado, antigüedad, ubicación geográfica).
2. Limpieza y tratamiento de nulos con criterio de negocio.
3. Feature engineering: variables `antiguedad_dias` y `tiene_baja`.
4. Visualizaciones: distribución por estado, antigüedad, ciudades con más clientes.
5. Entrenamiento de un modelo de **Regresión Logística** con scikit-learn.
6. Evaluación con matriz de confusión y curva ROC.

### Resultados

- **81% de precisión general** del modelo.
- La **antigüedad del cliente** y su **ubicación geográfica** son los factores más relevantes para anticipar la baja.
- La base de clientes se concentra en un grupo reducido de ciudades clave.
- El modelo detectó un **desbalance de clases** (muchos más clientes activos que dados de baja), lo que limita la detección de bajas reales y abre el camino a mejoras concretas: incorporar motivos de baja, ajustar pesos de clase, o enriquecer el dataset.

### Herramientas

Python · Google Colab · Pandas · NumPy · Matplotlib · Seaborn · scikit-learn

---

## 4. Conclusión

Este proyecto recorre el ciclo completo de trabajo con datos en una empresa:

1. **Ordenar**: diseñar la estructura que permite registrar todo de forma confiable.
2. **Analizar**: explorar los datos para entender qué está pasando.
3. **Predecir**: construir un modelo que anticipe comportamientos futuros.

El resultado no es solo un conjunto de archivos técnicos, sino un sistema que transforma datos desordenados en información accionable: saber qué clientes retener, dónde concentrar esfuerzos comerciales y cómo mejorar la gestión interna.

---

## Estructura del repositorio

```
NetFlow_Analisis/
├── docs/
│   └── DER_ProyectoNetFlow.png      ← Diagrama entidad-relación
├── sql/
│   ├── tablas_create.sql
│   ├── insertar_datos.sql
│   ├── vistas.sql
│   ├── funciones.sql
│   ├── proc-almacenados.sql
│   ├── triggers.sql
│   └── netflow-backup.sql
├── notebook/
│   └── ProyectoNetFlow_Sanchez_Micaela.ipynb
└── tableau/                          ← Dashboard (próximamente)
```

---

*Proyecto integrador · Micaela Sanchez · Analista y Científica de Datos*
