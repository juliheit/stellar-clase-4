# Hello Tiburona Contract 🦈

# Tarea Clase 4

📋 Resumen del Proyecto
---
Este repositorio documenta la implementación completa de la **Tarea Clase 4**, mostrando el proceso de desarrollo con dos versiones diferentes de Soroban CLI debido a problemas de compatibilidad.

### Estructura del repositorio

```text
stellar-clase-4/
├── v20.0.0/    # Primera implementación (limitada)
└── v23.1.4/    # Implementación completa con WSL
```

🎯 Versiones Implementadas
---

| Versión | Soroban CLI | Soroban SDK | Entorno | Estado | Detalles |
| :--- | :---: | :---: | :---: | :---: | :--- |
| **Versión 1** | `v20.0.0` | `20.5.0` | Windows 10 | ✅ Compila, ⚠️ Limitaciones | [Issue reportado: #18](https://github.com/tu-usuario/tu-repo/issues/18) |
| **Versión 2** | `v23.1.4` | `23.0.3` | WSL2 (Ubuntu en Windows 10) | ✅ Completo, tests pasando | **Recomendada para desarrollo** |

🚀 El Proceso Completo
---

### Fase 1: Primera implementación (`v20.0.0`)
**Problemas encontrados:**
* ❌ `soroban contract init` no disponible.
* ❌ Versión más reciente no instalaba en Windows 10.
* ❌ Tests incompatibles por dependencias `stellar-xdr`.
* ❌ Falta de funcionalidades modernas.

**Logros:**
* ✅ Código funcional y compilable.
* ✅ Todos los conceptos implementados correctamente.
* ✅ Generación de WASM exitosa.
* ✅ Documentación del problema ([Issue #18](https://github.com/tu-usuario/tu-repo/issues/18)).

Ver detalles: [`v20.0.0/README.md`](./v20.0.0/README.md)

### Fase 2: Migración a WSL y `v23.1.4`
**Decisión:** Instalar WSL para tener un entorno Linux completo y acceder a la última versión de Soroban CLI.

**Proceso de instalación:**
1. Instalación de `WSL2` en Windows 10.
2. Configuración de Ubuntu.
3. Instalación de Rust `1.90.0` en WSL.
4. Instalación de Soroban CLI `v23.1.4`.

**Resultado:** ✅ Entorno profesional de desarrollo funcionando.

### Fase 3: Implementación completa (`v23.1.4`)
**Logros:**
* ✅ Todas las funciones implementadas según especificación.
* ✅ **6/6 tests pasando (100%)**.
* ✅ Contrato compilado y optimizado.
* ✅ Tamaño final: **3.7KB** (optimizado, reducción del 35% respecto al no optimizado).

![Running tests OK](./Running%20tests%20ok.png)

Ver detalles: [`v23.1.4/README.md`](./v23.1.4/README.md)

📊 Comparación de Versiones
---

| Aspecto | `v20.0.0` | `v23.1.4` |
| :--- | :---: | :---: |
| **Entorno** | Windows 10 | WSL2 (Ubuntu) |
| **Instalación** | Manual limitada | Completa desde `rustup.rs` |
| **`soroban init`** | ❌ No disponible | ✅ Disponible |
| **Tests** | ❌ No ejecutables | ✅ 6/6 pasando |
| **Optimización** | ❌ No disponible | ✅ `soroban contract optimize` |
| **Validaciones** | Internas del SDK | ✅ Manuales implementadas |
| **Compilación** | ✅ Exitosa | ✅ Exitosa |
| **Tamaño WASM** | 2.5KB | 3.7KB (optimizado) |

🛠️ Funcionalidades Implementadas
---
Ambas versiones implementan el contrato completo con:

#### Funciones principales:
* `initialize(admin)` - Inicializa el contrato con administrador.
* `hello(usuario, nombre)` - Registra saludos con validaciones.
* `get_contador()` - Consulta el contador total de saludos.
* `get_ultimo_saludo(usuario)` - Consulta último saludo de un usuario.
* `reset_contador(caller)` - Resetea contador (**solo admin**).

#### Conceptos aplicados:
* ✅ Manejo de errores con `Result<T, Error>`.
* ✅ `Storage` organizado con `DataKey` enum.
* ✅ `Instance storage` (datos del contrato).
* ✅ `Persistent storage` (datos de usuarios).
* ✅ Gestión de TTL (`Time To Live`).
* ✅ Control de acceso basado en roles.
* ✅ Validación de inputs.

🔄 Diferencias Técnicas por Versión
---

### Cambios en la API de Tests (`v20` → `v23`)
En Soroban `v23`, los errores se manejan con `Result` en lugar de causar `panic`, por lo que se usan métodos `try_*` para capturar errores.

| Versión | Código de Test |
| :--- | :--- |
| **v20.0.0 (Original)** | ```rust\n#[test]\n#[should_panic(expected = "NombreVacio")]\nfn test_nombre_vacio() {\n    client.hello(&usuario, &vacio);  // Esperaba panic\n}``` |
| **v23.1.4 (Actual)** | ```rust\n#[test]\nfn test_nombre_vacio() {\n    let resultado = client.try_hello(&usuario, &vacio);\n    assert_eq!(resultado, Err(Ok(Error::NombreVacio)));\n}``` |

### Cambios en registro de contratos
| Versión | Código de Registro |
| :--- | :--- |
| **v20.0.0** | ```rust\nlet contract_id = env.register_contract(None, HelloContract);``` |
| **v23.1.4** | ```rust\nlet contract_id = env.register(HelloContract, ());``` |

### Cambios en generación de `Address`
En `v23` es necesario importar el trait `testutils::Address` explícitamente.

| Versión | Código de Generación de Address |
| :--- | :--- |
| **v20.0.0** | ```rust\nlet admin = Address::generate(&env);``` |
| **v23.1.4** | ```rust\nuse soroban_sdk::testutils::Address as _;\nlet admin = Address::generate(&env);``` |

📚 Aprendizajes 
---

### Técnicos:
* **WSL como solución:** Linux proporciona mejor compatibilidad para herramientas blockchain.
* **Versiones:** Soroban evolucionan rápidamente.
* **Adaptabilidad:** Capacidad de migrar entre versiones manteniendo funcionalidad.
* **Testing en Rust:** Diferencias entre manejo de errores con `panic` vs `Result`.
* **Optimización WebAssembly:** Importancia de reducir tamaño para blockchain (`soroban contract optimize`).

### Metodológicos:
* **Documentación del proceso:** Reportar *issues* ayuda a la comunidad.
* **Perseverancia:** Superar obstáculos técnicos paso a paso.
* **Investigación:** Buscar soluciones cuando las herramientas fallan.
* **Backup de versiones:** Mantener implementaciones funcionales como referencia.

### Personales:
* Perseverancia y adaptación. Superar la incompatibilidad inicial de las versiones fue una prueba de persistencia 😅.
* La importancia de documentar los problemas, no solamente es una cuestión técnica y de aprendizaje sino que hace a la cmomunidad, se construye en conjunto.
* Los principios fundamentales (`storage`, errores, validaciones) son independientes de la versión.


🔗 Referencias
---
* [Documentación oficial de Soroban](https://soroban.stellar.org/docs/)
* [Issue #18 - Problema con v20.0.0](https://github.com/tu-usuario/tu-repo/issues/18)
* [Tarea original](https://link-a-la-tarea-original)
* [Instalación de WSL](https://docs.microsoft.com/es-es/windows/wsl/install)

✅ Estado Final
---
* ✅ `v20.0.0`: Implementación funcional con limitaciones documentadas.
* ✅ `v23.1.4`: Implementación completa con todos los tests pasando.
* ✅ Documentación: Completa y útil para la comunidad.
* ✅ Aprendizaje: Conceptos fundamentales de Soroban dominados.

---

🎧 Código Futura 🦈- Stellar Blockchain

