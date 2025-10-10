# FASE 5 — Integración Sandbox

## Credenciales
- Configurar .env.local con MP_ACCESS_TOKEN y MP_PUBLIC_KEY (sandbox).
- APP_URL es la URL base (local: http://localhost:3000).

## Endpoints
- GET /api/products — lista productos con stock y lowStock.
- GET/POST/DELETE /api/cart — requiere auth (cookie auth_token=demo-token).
- POST /api/orders — crea pedido (pending), envía email de confirmación (mock).
- POST /api/mercadopago/create_preference — crea preferencia (Checkout Pro), usa external_reference=orderId.
- POST /api/mercadopago/pay — pago tokenizado (Cards) con token (sandbox).
- POST /api/mercadopago/webhook — confirma pago, marca order como paid, decrementa stock, envía email (mock).
- GET/POST /api/shipping — cálculo de envío por zonas; Microcentro gratis a consultar.
- GET/POST /api/pickup — slots de retiro en local, reservas con bloqueos.

## Flujo
1) Login (demo): POST /api/auth/login
2) Carrito: POST /api/cart
3) Order: POST /api/orders → obtiene orderId
4) MP: POST /api/mercadopago/create_preference → redirigir a init_point (sandbox)
5) Webhook: POST /api/mercadopago/webhook → actualiza estado → stock decrement → email
