# Análisis de ventas · Online Retail

Proyecto de análisis de datos de punta a punta: desde un requerimiento de negocio
hasta dashboards en Power BI y Tableau, usando datos reales de una tienda en línea.

## Contexto

Una tienda en línea del Reino Unido que vende artículos de regalo y decoración,
con muchos clientes mayoristas, necesita entender el desempeño de su negocio
entre diciembre de 2009 y diciembre de 2011 (más de 1 millón de transacciones).

## Preguntas de negocio

1. ¿Cuánto crecieron las ventas?
2. ¿El crecimiento viene de más clientes o de clientes que compran más?
3. ¿Qué productos y qué países mueven el negocio?
4. ¿Qué tan graves son las cancelaciones?
5. ¿Quiénes son los mejores clientes?
6. ¿Estamos perdiendo clientes?

El detalle está en el [documento de requerimiento](docs/01_requerimiento.md).

## Herramientas

- **PostgreSQL** · base de datos
- **SQL** · limpieza, transformación y análisis
- **DBeaver** · cliente SQL
- **Power BI** y **Tableau** · visualización
- **Git y GitHub** · control de versiones

## Estructura del repositorio

    ├── data/          # datos (no incluidos en el repositorio)
    │   ├── raw/       # datos originales
    │   └── processed/ # datos transformados
    ├── docs/          # documentación del proyecto
    ├── sql/           # scripts SQL
    ├── dashboards/    # Power BI y Tableau
    └── reports/       # informe final

## Estado del proyecto

- [x] Requerimiento de negocio
- [x] Configuración del entorno
- [ ] Carga de datos
- [ ] Calidad y limpieza de datos
- [ ] Análisis en SQL
- [ ] Modelo de datos
- [ ] Dashboard en Power BI
- [ ] Dashboard en Tableau
- [ ] Informe ejecutivo

## Datos

**Fuente:** [Online Retail II](https://archive.ics.uci.edu/dataset/502/online+retail+ii),
UCI Machine Learning Repository. Licencia CC BY 4.0.
Los datos no se incluyen en el repositorio; las instrucciones para obtenerlos se agregarán en la fase de carga.

## Autor

**Leonardo Soto** · [LinkedIn](https://www.linkedin.com/in/leonardo-soto-berrio/) · [GitHub](https://github.com/Lasotoberrio)
