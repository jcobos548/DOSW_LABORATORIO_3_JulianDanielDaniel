# Scope — Wok System

## Sistema
**Wok System** es la plataforma web de *El Restaurante* para el concepto de comida asiática tipo wok. Permite al cliente consultar la carta y armar su pedido, al mesero y la cocina gestionar las órdenes, y a la administración controlar inventario, pagos y reportes.

## Problema a resolver
Hoy el restaurante opera sin sistema digital: sin carta que refleje disponibilidad en tiempo real, sin forma de que el cliente arme su pedido sin esperar al mesero, sin visibilidad del pedido entre salón y cocina, sin control de inventario, y sin reportes de venta.

## Diagrama de contexto (C4 — Nivel 1)

**Actores:** Cliente, Mesero, Cocinero, Gerente, Cajero, Recepcionista, Bartender, Personal de aseo.
**Sistemas externos:** Pasarela de Pagos, Facturación Electrónica, Sistema de Proveedores, Servicio de Notificaciones.
**Herramienta:** Miro — [tablero editable](https://miro.com/welcomeonboard/WEdadkNoUGVXZnowaE8xaWJnZDVqY09GSm9USFdVdDh6eEx2ZC9IcHk3U2JaUFd2aW1Sd2o5Y3k2eXNVREptcXJJNlRnb0c2TlNIa0w4U0lnenpFTWora1V4LzRCcVdzeHExVUlPYkdtVmNvRWtWcys0Ti9ub05nZ0phRVlaeHR3VHhHVHd5UWtSM1BidUtUYmxycDRnPT0hdjE=?share_link_id=524382764077)

![Diagrama de contexto](docs/images/DiagramaContexto.png)

## Alcance (MVP)
**Incluye:** carta con disponibilidad en tiempo real · armar y confirmar pedido · tablero de cocina por estados · administración de carta e inventario · cierre de cuenta y pago · reportes de venta.

**No incluye (fases futuras):** domicilios, reservas, fidelización, app móvil nativa.

## Reglas de negocio
Confirmada con el ejemplo documentado en `requirements.md` (RW-01 — Consultar carta y disponibilidad):
- Un plato no puede ordenarse si alguno de sus ingredientes está agotado; el sistema lo marca como no disponible automáticamente.

Propias del concepto Wok *(borrador — confirmar con el equipo antes de subir)*:
1. Un wok no puede llevar más de 6 ingredientes/toppings personalizables.
2. La estación de wok prepara máximo 4 órdenes simultáneas; la 5ª queda en cola.

