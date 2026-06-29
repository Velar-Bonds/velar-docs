# Visión general

VELAR tokeniza y traza la propiedad de **bonos políticos** de Costa Rica sobre la
blockchain de **Stellar**. Cada etapa del ciclo de vida de un bono —emisión,
asignación, transferencia, validación— queda registrada on-chain de forma inmutable
y públicamente verificable.

## Problema

Los bonos políticos se negocian con poca trazabilidad: es difícil saber quién es el
dueño actual de un bono, a qué precio se transfirió y si el registro fue alterado.

## Solución

Un registro público e inmutable donde:

- Cada bono **es un token real** en Stellar (Classic Asset + contrato Soroban `VelarBond`).
- Las compraventas se coordinan vía **escrow on-chain** (Trustless Work).
- Cualquier ciudadano **verifica el historial** sin cuenta, en `/verificar`.
