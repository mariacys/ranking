[copilot-instructions.md](https://github.com/user-attachments/files/30049804/copilot-instructions.md)
# Contexto de la aplicación Ranking

## Descripción general
**Ranking** es una aplicación interna de consulta de datos de artículos de Inditex (Zara).  
Permite a los usuarios explorar y analizar el rendimiento de los artículos en tienda, ordenados según diferentes criterios.

---

## Pantalla principal

### Cabecera de la pantalla
- Logo **ZARA** y título **RANKING**
- Sección activa: **ROPA · SEÑORA · TOTAL**
- Filtros activos visibles: `VENTA UNIDADES HOY`, `TEMPORADA: I26, V26`, `HOY`, `TTFF Y .COM`
- Última actualización: `ACT. 15 JUL 13:04 H`

### Barra de herramientas global (parte superior derecha)

| Icono | Nombre | Función |
|---|---|---|
| 📄 PDF | **Exportar PDF** | Exporta el ranking visible a PDF. Al pulsar permite: (1) limitar el número de artículos a exportar, (2) agrupar los artículos de forma diferente al ranking actual (por comprador, familia o atributo) |
| 🚩 Bandera | **Alertas globales** | Permite resaltar indicadores de las fichas según condiciones definidas por el usuario |
| 📊 XLS | **Exportar Excel** | Descarga un fichero Excel con: **Hoja 1**: una fila por artículo y tantas columnas como indicadores tiene la ficha visible. **Hoja 2**: los filtros utilizados para ejecutar el ranking |
| ⚙️ Rueda dentada | **Configuraciones** | Guarda la consulta actual o recupera y ejecuta configuraciones anteriormente guardadas |
| ℹ️ Info | **Información** | (por documentar) |
| **NUEVA BÚSQUEDA** | **Nueva búsqueda** | Abre la sidebar para ejecutar un ranking totalmente nuevo |
| **MS** (avatar) | **Menú de usuario** | Cambiar idioma o cerrar sesión |

### Barra de controles de visualización

#### 📍 Localizador
- Posiciona el ranking en un artículo introduciendo su clave: `modelo / calidad / color`
- Si solo se indica `modelo / calidad`, navega entre los coincidentes con una flechita

#### 🔲 Cambio de vista
| Modo | Descripción |
|---|---|
| **Ficha** | Vista completa con foto, cabecera e indicadores |
| **Foto** | Solo foto y pequeño encabezado |
| **Mosaico** | Fotos muy pequeñas, máxima densidad de artículos |

#### MULTIPOSICIÓN
Muestra sobre la foto de cada ficha la posición del artículo en rankings por canal: tiendas físicas / .COM / marketplaces

#### MODELO · PLANO
- **MODELO**: foto con la prenda puesta en una modelo
- **PLANO**: foto de la prenda sola

---

### Zona de filtros rápidos
Barra que filtra los artículos visibles en pantalla sin relanzar la consulta.

#### Filtros siempre visibles
`COMPRADOR`, `FAMILIA`, `SUBFAMILIA`, `ATRIBUTO`, `2º ATRIBUTO`, `COLECCIÓN`, `PAQ/CONF`, `NEW`, `PROMO`, `MOV. CAMP`

#### Filtros contextuales
Aparecen solo bajo determinadas condiciones (ej. artículos en rebajas).

### Barra de resumen

#### Accionable de totales
Muestra: **nº artículos | UDS | Importe €**. Al expandir, si hay filtro rápido activo muestra el % que representa sobre el total del ranking sin filtros.

#### Accionable TOP
| Pestaña | Descripción |
|---|---|
| **TOP ARTÍCULOS** | Muestra solo los primeros X artículos (20, 40, 50, 100 o número personalizado) |
| **% PESO** | Muestra los artículos que acumulan un % sobre el indicador de ordenación |

---

## Fichas de artículo

### Parte fija

#### Foto
Imagen del artículo. Tipo controlado por selector MODELO · PLANO.

#### Cabecera
- Posición, referencia, temporada, nombre, familia/subfamilia/colección, precios
- **Clic** → detalle del artículo
- **Hover** → aparecen `...` → menú de navegación a otras apps:
  - **Análisis Históricos**
  - **Gestión Entregas**

#### Etiquetas de características
Sobre la foto. Solo en algunos artículos. Ej: `NEW 7D`, `CONT (93)`

### Parte variable — Indicadores
Lista personalizable de métricas (desde PERSONALIZAR RANKING):

| Indicador | Descripción |
|---|---|
| Venta Unidades | Unidades vendidas |
| Venta Importe | Importe en € |
| Nº Tiendas Con Venta | Tiendas con venta registrada |
| Expuesto | Unidades expuestas y % cobertura |
| Stock Tienda RFID | Stock en tienda por RFID |
| Nº Tiendas Con Stock | Tiendas con stock disponible |
| Bloqueos RFID | Nº bloqueos RFID |
| Stock Disp. Almacén Hoy | Stock en almacén (puede ser negativo) |

---

## Pantalla de detalle del artículo

### Layout — 3 columnas

**Izquierda**: miniaturas de artículos del ranking → clicar navega a su detalle  
**Centro**: galería de fotos del artículo actual  
**Derecha**:
1. Cabecera (referencia, nombre, origen, precios)
2. Chips de colores → clicar navega al artículo-color
3. Pestañas de desglose
4. Barra de herramientas del grid
5. Tabla de datos

### Pestañas de desglose
| Pestaña | Contenido |
|---|---|
| **MERCADOS** | Desglose por mercado/país y tienda |
| **CANAL DE VENTA** | Desglose por canal |
| **COLORES** | Desglose por color |
| **TALLAS** | Desglose por talla |
| **BLOQUEOS** | Bloqueos RFID |
| **ENTREGAS** | Próximas entradas de stock en almacén |

### Barra de herramientas del grid
| Icono | Función |
|---|---|
| 🚩 Bandera | Alertas: colorear celdas según condiciones |
| `<>` | Restablecer anchos de columna al defecto |
| ⚙️ | Mostrar/ocultar columnas |
| XLS | Exportar tabla a Excel |
| ⤢ | Maximizar tabla |

> El usuario puede redimensionar columnas manualmente arrastrando sus bordes.

### Columnas de la tabla
- **Días en tienda**
- **Venta Unidades**: HOY, DÍA -1, DÍA -2, 7D, -8 A -14D
- **Acum. Unidades**: ENVIADO, VENTA
- **Venta Imp €**: HOY, DÍA -1, DÍA -2, 7D, -8 A -14D
- **Nº Tiendas**: C/VENTA HOY, C/VENTA DÍA -1, C/STOCK HOY…

---

## Sidebar — "Nuevo Ranking"

| Campo | Ejemplo |
|---|---|
| Cadena | Zara |
| Secciones | Señora |
| Productos | Ropa |
| Tipo de Ranking | Total |
| Campaña | Temporada, I26, V26 |
| Canal de venta | Tienda física, Zara .COM |
| Fechas | Hoy |
| Ordenación | Venta Unidades Hoy |
| Mercados | (desplegable) |

- **BÚSQUEDA AVANZADA**: filtros más específicos
- **PERSONALIZAR RANKING**: elige indicadores visibles en las fichas
- **Buscador**: por Mo/Ca/Co o Descripción
- **LIMPIAR** / **APLICAR**

---

## Notas técnicas
- La clave de un artículo: **modelo / calidad / color**
- Un artículo-color: combinación de modelo + color, con sus propios datos
- Filtros rápidos: actúan sobre datos ya cargados, sin relanzar consulta
- Filtros contextuales: solo aparecen si las condiciones del ranking los hacen aplicables
- Configuraciones: consultas guardadas, gestionadas desde la rueda dentada global
- Excel exportado: siempre incluye segunda hoja con los filtros del ranking
- La navegación desde `...` pasa el contexto del artículo y filtros activos del ranking
- Stock Disp. Almacén Hoy puede ser negativo (sobreasignación o ajuste pendiente)
