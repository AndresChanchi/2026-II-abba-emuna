# Getting Started

Evidencia de que el equipo instaló el entorno y desplegó su primer contrato en testnet.
Guía que seguimos: [Getting Started de contratos](https://developers.stellar.org/docs/build/smart-contracts/getting-started).

| Dato | Valor |
|---|---|
| Lo hizo | Ana Gómez (Técnico) |
| Sistema operativo | macOS 27 |
| Fecha | 2026-10-27 |

## 1. Entorno

Salida de los comandos, copiada de la terminal como texto (no como captura).

```
$ rustc --version
rustc 1.96.0 (ac68faa20 2026-05-25) (Homebrew)

$ stellar --version
stellar 27.0.0 (5a7c5fe76530bf4248477ac812fc757146b98cc4)
stellar-xdr 27.0.0 (5262803470be965e42f80023d12fba12808c774a)
xdr (68fa1ac55692f68ad2a2ca549d0a283273554439)
```

## 2. hello_world en testnet

| Dato | Valor |
|---|---|
| Red | Testnet |
| Cuenta que desplegó | `ejemplo-ana` · `GBPJQ5YGROKKLNPLDLTJD4JYVRO2TYBI36JA7X5VUFKPAZ6A4CSZBZQ6` |
| Contract ID | `<C…>` |
| Enlace en stellar.expert | https://stellar.expert/explorer/testnet/contract/<Contract ID> |
| Hash del invoke de `hello` | `<64 caracteres hexadecimales>` |
| Resultado del invoke | `["Hello","Javeriana"]` |

## 3. Comandos que usamos

```bash
# Crear el proyecto y compilar
stellar contract init hello-jave
cd hello-jave
stellar contract build

# Cuenta de testnet con fondos de Friendbot
stellar keys generate ejemplo-ana --network testnet --fund

# Desplegar: devuelve el Contract ID (empieza por C)
stellar contract deploy \
  --wasm target/wasm32v1-none/release/hello_world.wasm \
  --source-account ejemplo-ana --network testnet --alias hello_world

# Invocar hello y enviar la transacción para obtener el hash
stellar contract invoke --id hello_world --source-account ejemplo-ana \
  --network testnet --send=yes -- hello --to Javeriana
```

> 💡 **¿Por qué `--send=yes`?** `hello` solo lee, no escribe nada. Sin esa opción la CLI simula la llamada, te muestra el resultado y **no** envía transacción, así que no hay hash que pegar.

## 4. Revisión antes del PR

- [ ] Las versiones están pegadas como texto, con el comando arriba de cada una.
- [ ] El Contract ID empieza por `C` y el enlace de stellar.expert abre el contrato.
- [ ] El hash tiene 64 caracteres y aparece en stellar.expert al buscarlo.
- [ ] No hay llaves secretas (`S…`) en ningún archivo.
