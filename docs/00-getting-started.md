# Empezar

Esta guía levanta VELAR en tu máquina en pocos pasos. El código está en
[Velar-Bonds/Velar](https://github.com/Velar-Bonds/Velar).

## Requisitos

- Node.js 20+
- npm 10+
- (Opcional, para el contrato) Rust stable + target `wasm32-unknown-unknown`

## Pasos

```bash
git clone https://github.com/Velar-Bonds/Velar.git
cd Velar
npm install

# Variables de entorno
cp apps/web/.env.example apps/web/.env.local   # completá las claves
cp apps/api/.env.example apps/api/.env          # completá las claves

# Levantar API (puerto 3001) y Web (puerto 3000)
npm run dev
```

- Web: http://localhost:3000
- API: http://localhost:3001/api
- Verificación pública (sin login): http://localhost:3000/verificar

## Datos de demo

Desde `apps/api`, `npm run seed` carga partidos, bonos y usuarios de ejemplo.
