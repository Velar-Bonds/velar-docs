# Arquitectura

Monorepo (npm workspaces):

| Paquete | Tecnología | Rol |
|---|---|---|
| `apps/api` | NestJS | API REST, lógica de negocio, auditoría, escrow |
| `apps/web` | Next.js 16 | Frontend (landing, paneles TSE/Partido, verificación pública) |
| `packages/types` | TypeScript | Tipos compartidos `@velar/types` |
| `contracts/velar-bond` | Soroban (Rust) | Contrato del bono on-chain |
| `supabase/migrations` | SQL | Esquema Postgres + RLS |

## Flujo de datos

`Web (Next.js)` → `API (NestJS)` → `Supabase (Postgres)` y `Stellar (Horizon / Soroban RPC)`.

El estado de negocio vive en Postgres; la **verdad on-chain** vive en Stellar. La capa
de auditoría (`audit_events`) reconcilia ambos.
