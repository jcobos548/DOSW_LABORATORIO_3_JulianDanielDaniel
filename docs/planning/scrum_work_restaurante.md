# Desglose del Trabajo - Restaurante Wok (MVP)

## Épica
**EPIC-01: Gestión integral del ciclo de pedidos digitales en Wok**
* **Descripción:** Implementación del flujo completo de un pedido, desde la visualización de la carta en tiempo real por el cliente, la gestión de ítems, hasta la notificación y preparación organizada por lotes en el tablero de cocina.
* **Prioridad:** Alta. (Es el núcleo operativo que justifica la existencia del sistema).

---

## Feature 1: Consulta de Carta y Disponibilidad
**FEAT-01**
* **Descripción:** Capacidad del sistema para mostrar la oferta gastronómica actualizada, filtrando o bloqueando automáticamente ítems según el inventario de ingredientes en cocina.

### Historia de Usuario 1.1
**STORY-01: Consultar carta disponible**
* **Descripción:** Como cliente, quiero consultar los platos de la carta para conocer las opciones disponibles y armar mi orden.
* **Criterios de Aceptación:**
  * **Dado** que el cliente ingresa a la aplicación, **Cuando** selecciona ver la carta, **Entonces** el sistema muestra la lista de platos clasificados por categoría.
  * **Dado** que el cliente busca un plato, **Cuando** ingresa el nombre en el buscador, **Entonces** el sistema retorna los resultados coincidentes mostrando su estado actual (disponible/no disponible).
* **Prioridad:** Alta (Sin visualizar la carta, el ciclo del pedido no puede iniciar).
* **Puntos de Historia Estimados:** [Por definir en Parte 7]
* **Subtareas:**
  * **SUB-01:** Crear el esquema y la tabla de `Platos` en la base de datos con sus respectivos atributos.
  * **SUB-02:** Desarrollar el endpoint `GET /carta/platos` con soporte para filtros por categoría y nombre.
  * **SUB-03:** Construir la interfaz de usuario del menú y la tarjeta de producto (Product Card) en el frontend.

### Historia de Usuario 1.2
**STORY-02: Bloqueo de platos por ingredientes agotados**
* **Descripción:** Como administrador, quiero que el sistema marque automáticamente un plato como no disponible si alguno de sus ingredientes se agota, para evitar que los clientes ordenen algo que la cocina no puede preparar.
* **Criterios de Aceptación:**
  * **Dado** que el ingrediente "Salmón" llega a stock cero, **Cuando** el sistema actualiza el inventario, **Entonces** todos los platos que contienen "Salmón" cambian su estado a "No disponible" en la carta.
  * **Dado** que un plato está marcado como "No disponible", **Cuando** el cliente intenta seleccionarlo, **Entonces** el sistema deshabilita el botón de agregar e informa la causa.
* **Prioridad:** Alta (Regla de negocio principal que previene inconsistencias operativas).
* **Puntos de Historia Estimados:** [Por definir en Parte 7]
* **Subtareas:**
  * **SUB-04:** Crear la tabla relacional `plato_ingrediente` y la tabla `inventario`.
  * **SUB-05:** Implementar la lógica de verificación de stock (trigger o servicio) al actualizar el inventario.
  * **SUB-06:** Bloquear la interacción en el frontend para ítems con la propiedad `isAvailable: false`.

---

## Feature 2: Armado y Gestión del Pedido
**FEAT-02**
* **Descripción:** Capacidad transaccional que permite la recolección, modificación y confirmación de ítems por parte del cliente o mesero, conectando directamente con las reglas de preparación en cocina.

### Historia de Usuario 2.1
**STORY-03: Armar y modificar pedido**
* **Descripción:** Como cliente, quiero agregar, modificar o quitar platos de mi orden actual para ajustar mi consumo antes de confirmar el envío a cocina.
* **Criterios de Aceptación:**
  * **Dado** que tengo un pedido en estado RECIBIDO, **Cuando** agrego un nuevo plato, **Entonces** el ítem se suma a la lista y el precio total se recalcula automáticamente.
  * **Dado** que mi pedido ya pasó a estado EN PREPARACIÓN, **Cuando** intento eliminar un ítem, **Entonces** el sistema bloquea la acción y muestra un mensaje de error.
* **Prioridad:** Alta (Funcionalidad base del core transaccional).
* **Puntos de Historia Estimados:** [Por definir en Parte 7]
* **Subtareas:**
  * **SUB-07:** Desarrollar el endpoint `POST /pedidos/{id}/items` y `DELETE /pedidos/{id}/items`.
  * **SUB-08:** Implementar la lógica de negocio para congelar el precio del plato al momento de insertarlo en el pedido.
  * **SUB-09:** Crear el validador de estado (middleware) que rechace peticiones si el pedido es distinto a RECIBIDO.

### Historia de Usuario 2.2
**STORY-04: Gestión de lotes de preparación en barra (Sushi)**
* **Descripción:** Como cocinero de la barra de sushi, quiero recibir las comandas fraccionadas en tandas de máximo 6 rolls por vez para mantener la calidad y el ritmo operativo sin saturar el área de trabajo.
* **Criterios de Aceptación:**
  * **Dado** que un cliente ordena 8 rolls de sushi diferentes, **Cuando** el pedido entra al tablero de cocina, **Entonces** el sistema divide la visualización en dos comandas relacionadas (una de 6 y otra de 2).
  * **Dado** que un pedido tiene 4 rolls y 2 platos calientes (Wok), **Cuando** ingresa a cocina, **Entonces** el sistema envía los platos calientes a la estación Wok y los 4 rolls juntos a la barra de sushi.
* **Prioridad:** Media (Regla de negocio fundamental del concepto japonés, pero puede entrar posterior al flujo transaccional básico).
* **Puntos de Historia Estimados:** [Por definir en Parte 7]
* **Subtareas:**
  * **SUB-10:** Extender el modelo de datos de `Categoría` para identificar cuáles platos pertenecen a la "Barra de Sushi".
  * **SUB-11:** Desarrollar el algoritmo de partición que agrupe los ítems de sushi en arreglos de longitud máxima de 6 antes de renderizarlos en cocina.
  * **SUB-12:** Ajustar la interfaz del tablero de cocina para reflejar visualmente las tandas fraccionadas (ej. "Tanda 1 de 2").