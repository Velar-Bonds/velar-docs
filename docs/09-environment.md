# Variables de entorno

Referencia completa de configuración para **Velar** (API + Web).  
Los secretos **nunca** van al frontend ni a GitHub — solo `.env.example` y Vercel/Railway dashboards.

---

## Resumen rápido

| Dónde | Archivo | Despliegue |
|-------|---------|------------|
| API | `apps/api/.env` | Vercel `velar-api` / Railway |
| Web | `apps/web/.env.local` | Vercel `velar-web` |
| Scripts | leen `apps/api/.env` | local / CI |

Sincronizar API → Vercel: `node scripts/sync-vercel-api-env.mjs velar-api production`

---

## API (`apps/api`)

### Supabase (obligatorio)

| Variable | Descripción |
|----------|-------------|
| `SUPABASE_URL` | URL del proyecto Supabase |
| `SUPABASE_SERVICE_ROLE_KEY` | Service role — **solo backend**. Bypass RLS |

### Servidor HTTP

| Variable | Default | Descripción |
|----------|---------|-------------|
| `PORT` | `3001` | Puerto local |
| `WEB_URL` | `http://localhost:3000` | Origen del front (CORS fallback) |
| `CORS_ORIGINS` | — | Orígenes permitidos separados por coma (prod) |
| `THROTTLE_TTL` | `60000` | Ventana rate-limit (ms) |
| `THROTTLE_LIMIT` | `100` | Requests por ventana por IP |

### Stellar — red y Horizon

| Variable | Default (testnet) | Descripción |
|----------|-------------------|-------------|
| `STELLAR_NETWORK` | `testnet` | `testnet` \| `mainnet` |
| `STELLAR_HORIZON_URL` | `https://horizon-testnet.stellar.org` | Horizon Classic |
| `SOROBAN_RPC_URL` | `https://soroban-testnet.stellar.org` | RPC Soroban |
| `STELLAR_ENABLE_FRIENDBOT` | `true` | Fondear cuentas nuevas en testnet |
| `STELLAR_USDC_CRC_RATE` | `530` | Tasa CRC→USDC para DvP wallet |

### Stellar — custodia (obligatorio en prod)

| Variable | Descripción |
|----------|-------------|
| `STELLAR_WALLETS_JSON` | JSON inline con llaves custodiales (`platform`, `escrow`, perfiles). En local: generado por `npm run provision:wallets` → `.stellar-wallets.json` |

### Soroban (opcional)

| Variable | Descripción |
|----------|-------------|
| `SOROBAN_VELAR_BOND_WASM_HASH` | Hash WASM desplegado del contrato `VelarBond` |
| `SOROBAN_TSE_ADDRESS` | Cuenta Stellar del TSE para firmar despliegues Soroban |

### Trustless Work (escrow)

| Variable | Default | Descripción |
|----------|---------|-------------|
| `TRUSTLESS_WORK_API_URL` | `https://dev.api.trustlesswork.com` | Testnet; mainnet: `https://api.trustlesswork.com` |
| `TRUSTLESS_WORK_API_KEY` | — | API key de Trustless Work |
| `TRUSTLESS_WORK_PLATFORM_ADDRESS` | — | Cuenta platform en TW (`npm run provision:wallets`) |

---

## Web (`apps/web`)

Todas las variables públicas llevan prefijo `NEXT_PUBLIC_`.

| Variable | Default | Descripción |
|----------|---------|-------------|
| `NEXT_PUBLIC_SUPABASE_URL` | — | Misma URL que Supabase |
| `NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY` | — | Anon / publishable key (segura en browser) |
| `NEXT_PUBLIC_API_URL` | `http://localhost:3001/api` | Base URL REST |
| `NEXT_PUBLIC_STELLAR_NETWORK` | testnet | `testnet` \| `mainnet` (Freighter PUBLIC) |
| `NEXT_PUBLIC_STELLAR_HORIZON_URL` | auto | Override Horizon front read-only |
| `NEXT_PUBLIC_DEMO_MODE` | `0` | `1` = selector multi-país en pitch |
| `NEXT_PUBLIC_SOCIAL_AUTH` | `0` | `1` = botones OAuth (si Supabase los tiene) |
| `NEXT_PUBLIC_SELF_CUSTODY` | `0` | `1` = vendedor firma transfer con Freighter |
| `PORT` | `3000` | Puerto dev Next.js |

---

## Scripts (`apps/api/scripts`)

Usados por `npm run demo:flow`, `seed`, etc.

| Variable | Descripción |
|----------|-------------|
| `API_URL` | Override URL API (default `http://localhost:3001/api`) |
| `SUPABASE_PUBLISHABLE_KEY` | Anon key para scripts cliente |
| `DEMO_PASSWORD` | Password cuentas demo (default `Velar12345!`) |

---

## Vercel — producción referencia

### `velar-web`

```
NEXT_PUBLIC_SUPABASE_URL
NEXT_PUBLIC_SUPABASE_PUBLISHABLE_KEY
NEXT_PUBLIC_API_URL=https://velar-api.vercel.app/api
NEXT_PUBLIC_STELLAR_NETWORK=testnet
```

### `velar-api`

Ver `scripts/sync-vercel-api-env.mjs` para lista completa sincronizada desde local.

---

## Checklist mainnet

1. `STELLAR_NETWORK=mainnet` + Horizon/RPC mainnet en API  
2. `NEXT_PUBLIC_STELLAR_NETWORK=mainnet` en web  
3. Freighter en red **PUBLIC**  
4. `STELLAR_WALLETS_JSON` con cuentas mainnet fondeadas (sin Friendbot)  
5. USDC real + trustlines  
6. `TRUSTLESS_WORK_API_URL=https://api.trustlesswork.com`
