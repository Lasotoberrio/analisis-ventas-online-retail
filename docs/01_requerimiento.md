# Documento de requerimiento: Análisis comercial de la tienda en línea

**Versión:** 1.0 · **Autor:** Leonardo Soto, Analista de Datos · **Solicitante:** Laura Restrepo, Gerente Comercial

## 1. Contexto y objetivo

La Gerencia Comercial necesita entender el desempeño del negocio entre diciembre de 2009 y diciembre de 2011 para presentarlo en la junta directiva, en 6 semanas. Las ventas parecen haber crecido, pero no se sabe si el crecimiento viene de captar más clientes o de que los clientes actuales compren más. También preocupan el nivel de cancelaciones y la posible pérdida de clientes.

**Objetivo:** construir un tablero mensual y un informe ejecutivo que muestren qué impulsa las ventas (clientes, productos y países), cuánto se pierde por cancelaciones y qué tan bien se retiene a los clientes, para apoyar las decisiones comerciales de la junta.

## 2. Stakeholders

| Rol | Persona | Qué necesita |
|---|---|---|
| Solicitante y usuaria principal | Laura Restrepo, Gerente Comercial | Respuestas claras para la junta y un tablero para revisar cada mes |
| Audiencia final | Junta directiva | Conclusiones y recomendaciones, sin detalle técnico |
| Proveedor de datos | Área de Sistemas | Acceso a la tabla de transacciones y resolución de dudas sobre los datos |
| Responsable del análisis | Leonardo Soto, Analista de Datos | Requerimiento claro, datos confiables, validación de definiciones |

## 3. Preguntas de negocio

| # | Pregunta de negocio | Pregunta de datos |
|---|---|---|
| 1 | ¿Crecieron las ventas? | ¿Cuánto variaron las ventas netas mensuales entre ene-nov de 2010 y ene-nov de 2011? |
| 2 | ¿El crecimiento viene de más clientes o de que cada cliente compre más? | ¿Cómo evolucionaron mes a mes los clientes activos (nuevos y recurrentes), las facturas por cliente y el ticket promedio? |
| 3 | ¿Qué productos mueven el negocio? | ¿Qué productos generan más ventas netas y qué % de los productos concentra el 80% de las ventas? |
| 4 | ¿Qué países mueven el negocio? | ¿Cómo se distribuyen las ventas netas y los clientes por país? ¿Cuánto pesa el Reino Unido frente al resto? |
| 5 | ¿Tenemos muchas cancelaciones? | ¿Qué % del valor vendido se cancela cada mes, y en qué productos, países y clientes se concentra? |
| 6 | ¿Quiénes son nuestros mejores clientes? | ¿Cómo se segmentan los clientes según qué tan reciente fue su última compra, con qué frecuencia compran y cuánto gastan? ¿Qué % de las ventas aporta cada segmento? |
| 7 | ¿Estamos perdiendo clientes? | De los clientes que compraron por primera vez en cada mes, ¿qué % volvió a comprar en los 3 meses siguientes? ¿Mejora o empeora en el tiempo? |

## 4. KPIs

| KPI | Definición | Fórmula | Granularidad | Reglas | Para qué sirve |
|---|---|---|---|---|---|
| Ventas netas (£) | Dinero facturado menos lo cancelado | Σ (cantidad × precio) de facturas normales − Σ (cantidad × precio) de facturas canceladas | Mensual, por país y producto | Facturas que empiezan con "C" = cancelación. Se excluyen códigos que no son productos (portes, ajustes manuales), a confirmar en la fase de calidad | Medir el tamaño real del negocio |
| Clientes activos | Clientes distintos con al menos una compra en el mes, separados en nuevos y recurrentes | Conteo de Customer ID distintos con facturas no canceladas en el mes | Mensual, por país | Nuevo = primera compra en ese mes. Registros sin Customer ID no cuentan como cliente | Saber si el crecimiento viene de captar clientes |
| Ticket promedio (£) | Valor promedio de una factura | Ventas netas ÷ número de facturas no canceladas | Mensual | Solo facturas con cliente identificado | Saber si cada compra es más grande |
| Frecuencia de compra | Facturas promedio por cliente activo | Facturas no canceladas ÷ clientes activos | Mensual | Igual que el ticket promedio | Saber si los clientes compran más veces |
| Tasa de cancelación (%) | Porcentaje del valor vendido que se cancela | Valor cancelado ÷ ventas brutas × 100 | Mensual, por país, producto y cliente | Se mide en valor (£), no en número de facturas | Dimensionar el problema de las cancelaciones |
| Retención a 90 días (%) | De los clientes nuevos de un mes, cuántos vuelven a comprar en los 90 días siguientes | Clientes nuevos del mes que recompran en 90 días ÷ clientes nuevos del mes × 100 | Mensual, por mes de primera compra (cohorte) | No se calcula para los últimos 3 meses, que no tienen 90 días de seguimiento | Saber si estamos perdiendo clientes |
| Unidades por factura | Cantidad promedio de unidades que lleva una compra | Σ Quantity de facturas no canceladas ÷ número de facturas no canceladas | Mensual, por país | Se excluyen las facturas que empiezan con "C" y los códigos que no son productos. Se revisarán cantidades atípicas (compras muy grandes) en la fase de calidad | Distinguir compras al por mayor de compras al detalle y detectar si el tamaño de las compras cambia en el tiempo |

## 5. Alcance

**Incluye:**
- Transacciones de diciembre de 2009 a diciembre de 2011, todos los países.
- Los KPIs definidos y las 7 preguntas de negocio.
- Tablero mensual en Power BI y una versión publicada en Tableau.
- Informe ejecutivo para la junta.

**No incluye:**
- Rentabilidad o margen (no hay datos de costos).
- Análisis de marketing o canales de adquisición (no hay datos).
- Pronósticos de ventas futuras (posible fase 2).
- Inventario o logística.

## 6. Supuestos

1. Customer ID identifica de forma única a cada cliente.
2. Los precios están en libras esterlinas y son el valor final cobrado.
3. Las facturas que empiezan con "C" son cancelaciones de compras registradas en la misma tabla.
4. Los registros sin Customer ID son ventas válidas: cuentan en las ventas totales, pero no en las métricas de clientes.
5. El último mes podría estar incompleto; se validará en la fase de calidad de datos.
6. Un cliente que no compra en 90 días se considera "en riesgo" (umbral por confirmar con la Gerencia Comercial).

## 7. Preguntas para la Gerencia Comercial

1. Para la junta, ¿"ventas" debe ser neta de cancelaciones o bruta? Se propone neta.
2. ¿Las cancelaciones incluyen devoluciones de producto, o son solo pedidos anulados antes del envío?
3. ¿Existe una meta o presupuesto de ventas para comparar los resultados?
4. ¿Se pueden diferenciar clientes mayoristas de minoristas? No hay una columna para eso. ¿Existe otra fuente?
5. ¿A partir de cuántos días sin comprar se considera perdido a un cliente? Se proponen 90.
6. Además de la Gerencia Comercial, ¿quién más usará el tablero?
7. ¿Qué decisiones se espera que tome la junta con esta información?
8. ¿Hubo cambios importantes en el negocio entre 2009 y 2011 (campañas, cambios de precios, apertura de nuevos países o nuevas líneas de productos) que debamos tener en cuenta al interpretar las tendencias?

## 8. Entregables y cronograma

| Semana | Entregable |
|---|---|
| 1 | Documento de requerimiento aprobado + entorno de trabajo listo |
| 2 | Base de datos cargada + informe de calidad de datos |
| 3-4 | Análisis en SQL de las 7 preguntas |
| 5 | Tablero en Power BI (revisión con la Gerencia) + versión en Tableau |
| 6 | Informe ejecutivo para la junta + ajustes finales |
