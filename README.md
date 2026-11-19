# Peak & Eat (ITESO) — Prototipo Visual Clicable

Prototipo móvil hiperlocal para apartar comida en cafeterías del campus y negocios vecinos al ITESO (Guadalajara) y recogerla sin filas mediante código QR. Incluye los roles **Alumno** y **Comercio aliado**.

---

## Cómo abrirlo

1. Descomprime la carpeta `peak-and-eat/` (no requiere servidor, Node.js ni conexión a internet).
2. Haz **doble clic en `index.html`** (recomendado: **Google Chrome** o **Microsoft Edge**).
3. En escritorio se muestra dentro de un marco de teléfono centrado de `390 px` con un panel lateral **🛠️ Herramientas de demo** (tema claro/oscuro, Modo test y accesos directos). En celular ocupa el 100 % de la pantalla y oculta el panel lateral.

---

## Credenciales y tarjetas de demostración

| Rol | Correo | Contraseña | Pantalla destino |
| --- | --- | --- | --- |
| **Alumno** (Arantxa Morales) | `arantxa.morales@iteso.mx` | `demo1234` | `explorar.html` |
| **Comercio** (Guich Iteso) | `guich@iteso.mx` | `demo1234` | `comercio-pedidos.html` |

- Cualquier otra contraseña en `login.html` dispara el error de credenciales (y bloqueo simulado de 30 s tras 5 fallos).
- **Tarjetas ficticias de prueba** (en `checkout.html` y `monedero.html`):
  - Aprobada: `4242 4242 4242 4242` (vigencia `08/29`, CVV `123`).
  - Rechazada: `4000 0000 0000 0002` (conserva el carrito y el saldo).

---

## Convenciones de datos de demostración

- **Fecha y hora ficticia:** Miércoles **18 de noviembre de 2026, ~12:30 h**.
  - Los atajos de horario `10:00` y `11:30` aparecen deshabilitados (*Pasada*).
  - **D' Eli, comida corrida** aparece como *Cerrado hoy* y **La Cocina de la Esquina** como *Pausado 15 min*.
  - En métricas de Hoy de Guich Iteso, las ventas por hora llegan hasta `12:00` (parcial hasta `12:30 h`) con pico en `11:00–12:00` (`$780`).
- **Alumna:** Arantxa Morales (`Ingeniería`, preferencia *Sin cacahuate*), **`220 pts`** (Nivel *Explorador*, `120/150` en este nivel), **racha de 2 semanas**.
- **Convención de saldo (`$159` vs `$140`):**
  - El chip del monedero muestra **`$159`** en toda la app (cuadre exacto de los 9 movimientos del monedero).
  - **Excepción en `checkout.html`:** muestra el saldo previo de **`$140`** (instante anterior a la recarga de `+$300` de las 12:14 h) para demostrar el flujo completo de saldo insuficiente (`$183 − $140 = faltan $43`) → recarga `$300` (`$440`) → pago de `PE-4821` (`$183`).
- **Folios coherentes en todas las pantallas:**
  - `PE-4821` (Guich Iteso, `$183`, 18 nov 12:15, Preparando / Recibo `?pedido=4821`)
  - `PE-4822` (Guich Iteso, `$98`, 18 nov 12:25, Programado 14:30)
  - `PE-4790` (La Cocina de la Esquina, `$95`, 16 nov 14:20, Recogido / Recibo `?pedido=4790`)
  - `PE-4785` (Tacos de Canasta Jorgillo, `$65`, 14 nov 13:05, Recogido / Recibo `?pedido=4785`)
  - `PE-4810` (D' Eli, `$90`, 18 nov 10:05–10:12, Cancelado y reembolsado)
- **Almacenamiento local:** `sessionStorage` se utiliza únicamente para recordar el tema claro/oscuro (`pe_theme`) y el Modo test CMA (`pe_test_on`, `pe_test_t0`, `pe_test_ck`).

---

## Mapa de archivos

```text
peak-and-eat/
├── index.html                  # Bienvenida y onboarding (3 diapositivas)
├── registro.html               # Registro alumno + términos + bono bienvenida
├── login.html                  # Acceso alumno / comercio + recuperar contraseña
├── explorar.html               # Catálogo (9 platillos, 6 locales), filtros, platillo y carrito
├── locales.html                # Directorio de los 6 locales aliados del ITESO
├── pedidos.html                # Pedidos activos, programados e historial + QR + guardar combo
├── perfil.html                 # Cuenta, resumen monedero/puntos, accesos y alianza comercio
├── checkout.html               # Resumen PE-4821, programar hora, cupón, saldo $140 y recarga
├── monedero.html               # Saldo $159, 9 movimientos filtrables, cupones y recarga
├── pedido.html                 # Seguimiento PE-4821 (4 pasos), Voy en camino, QR y cancelar
├── pedido-programado.html      # Seguimiento PE-4822 (14:30), cambiar hora y cancelar sin costo
├── chat.html                   # Chat alumno ↔ Guich Iteso (PE-4821)
├── calificar.html              # Calificación (?pedido=4785 | 4821), etiquetas y propina
├── recibo.html                 # Ticket imprimible (?pedido=4790 | 4785 | 4821)
├── notificaciones.html         # Centro de avisos agrupado (Hoy / Antes)
├── progreso.html               # Nivel, 220 pts, racha 2 sem, retos, insignias, facultad y canje
├── favoritos.html              # Platillos favoritos y combos guardados
├── ayuda.html                  # Buscador y 6 preguntas frecuentes en acordeón
├── reportar.html               # Formulario de reporte de problema (SUP-205)
├── mis-reportes.html           # Tickets SUP-204 y SUP-203
├── ajustes.html                # Notificaciones, tema, Modo test, demo, restablecer y salir
├── comercio-pedidos.html       # Panel Guich Iteso (5 pestañas + simular entrante)
├── comercio-menu.html          # Disponibilidad, agotados (1 h / hoy), edición y pausa 15 min
├── comercio-metricas.html      # KPIs Hoy/7d/30d, gráficas por hora y 7 días, ranking y reseñas
├── comercio-local.html         # Perfil Guich Iteso, horario, pausa, demo y cerrar sesión
├── comercio-chat.html          # Chat vista comercio (PE-4821)
├── css/
│   └── style.css               # Sistema de diseño claro/oscuro, marco móvil y @media print
└── js/
    ├── app.js                  # Núcleo compartido (window.PE) + Fase 2 y Fase 3
    ├── pedidos.js              # Fase 4 (pedidos, seguimiento, chat, calificación, recibos)
    ├── cuenta.js               # Fase 5 (monedero, perfil, favoritos)
    ├── gamificacion.js         # Fase 5 (progreso, retos, insignias, canje)
    ├── soporte.js              # Fase 6 (notificaciones, ayuda, reportes, ajustes)
    └── comercio.js             # Fase 7 (pedidos, menú, métricas, local y chat comercio)
```

---

## Qué requeriría un backend real para dejar de ser simulado

1. **Autenticación y sesiones seguras:** registro con verificación de correo `@iteso.mx`, contraseñas con hash (`Argon2`/`bcrypt`), tokens JWT/cookies `HttpOnly`, recuperación real por correo y bloqueo por tasa en servidor.
2. **Base de datos transaccional:** tablas para usuarios, comercios, platillos/inventario en tiempo real, pedidos con máquina de estados en servidor, libro contable del monedero (evitando saldos negativos o dobles cobros) y tickets de soporte.
3. **Pasarela de pagos real:** integración PCI-DSS (Stripe, Conekta o Mercado Pago) con webhooks para recargas, cobros con tarjeta, propinas y reembolsos automáticos por cancelación o rechazo.
4. **Tiempo real y notificaciones push:** WebSockets o Server-Sent Events para sincronizar en vivo estados de pedido, marca *"Viene en camino"*, mensajes de chat y disponibilidad de agotados entre alumno y comercio, más Web Push / FCM.
5. **Validación segura de entregas QR:** códigos firmados de un solo uso con expiración, escaneo desde cámara en el panel del comercio y registro auditable de entrega.
6. **Operación, analítica y cumplimiento:** generación de comprobantes fiscales (CFDI) si aplica, protección de datos personales (LFPDPPP), panel multi-comercio con roles y permisos, y respaldo automático de métricas históricas.
