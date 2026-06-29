# Modelo de roles

VELAR tiene tres perspectivas sobre el mismo registro:

- **TSE** — emite bonos, audita el sistema completo, valida transferencias.
- **Partido** — tenedor de bonos; los recibe, los publica al marketplace y reporta.
- **Ciudadano / Usuario** — verifica quién financia qué, sin pedir permiso ni cuenta.

El control de acceso se aplica con un `RolesGuard` global (`@Roles(...)`) en la API y
guards por shell en el frontend.
