## 1. Requerimientos funcionales

| Código | Requerimiento |
|---|---|
| **RF-01** | Consultar la carta con el estado de disponibilidad de cada plato. |
| **RF-02** | Agregar, modificar y quitar ítems de un pedido mientras la cuenta esté abierta. |
| **RF-03** | Confirmar un pedido y enviarlo automáticamente al tablero de cocina. |
| **RF-04** | Cambiar el estado de un pedido desde cocina: RECIBIDO → EN PREPARACIÓN → LISTO → ENTREGADO. |
| **RF-05** | Cerrar la cuenta de una mesa y registrar el pago. |
| **RF-06** | Generar reportes de ventas por plato, fecha y mesero. |

## 2. Requerimientos no funcionales

### RNF-01 Seguridad
El sistema debe controlar el acceso según el rol del usuario.

### RNF-02 Rendimiento
El tablero de cocina debe reflejar un pedido nuevo en menos de 2 segundos.

### RNF-03 Disponibilidad
El sistema debe funcionar durante las 12 horas continuas del servicio.

### RNF-04 Usabilidad
Un cliente nuevo debe poder completar su primer pedido en máximo 4 pantallas.

### RNF-05 Auditabilidad
Cada cambio de estado de un pedido debe registrar el usuario y la hora.

### RNF-06 Integridad
El sistema debe evitar que una mesa tenga más de una cuenta abierta.

![Historia_Usuario](docs/uml/HU1.png)

![Historia_Usuario](docs/uml/HU2.png)

![Historia_Usuario](docs/uml/HU3.png)

## 3. Análisis crítico

**a. ¿Hay algún requerimiento que deba detallarse más?**

Sí. El requerimiento de cierre de cuenta y pago necesita más detalle porque involucra diferentes formas de pago y sistemas externos como la pasarela de pagos y facturación electrónica.

**b. ¿Existen requerimientos que se contradigan?**

No se identifican contradicciones directas. Sin embargo, se debe tener en cuenta que un pedido puede ser modificado mientras está en RECIBIDO, pero no después de pasar a EN PREPARACIÓN.

**c. ¿Cuáles serían los 2 más importantes para una primera iteración?**

RF-02, armar el pedido, y RF-04, gestionar el pedido en cocina. Son importantes porque permiten validar el flujo principal del restaurante desde que se realiza la orden hasta que cocina la prepara.

**d. ¿Hay alguno que no debería realizarse en el MVP?**

Los reportes de ventas podrían dejarse para una segunda etapa. El objetivo inicial es validar el ciclo completo de carta, pedido, cocina y pago antes de agregar funcionalidades adicionales.