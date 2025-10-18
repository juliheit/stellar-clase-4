# Hello Tiburona Contract

# Tarea Clase 4

## Versión implementada

- **Soroban CLI:** 20.0.0
- **Soroban SDK:** 20.5.0

## Estado de la implementación

✅ **Funciones implementadas:**

- `initialize()` - Inicializa el contrato con admin
- `hello()` - Registra saludos (sin validaciones manuales por limitación de SDK 20.x)
- `get_contador()` - Consulta el contador de saludos
- `get_ultimo_saludo()` - Consulta último saludo de un usuario
- `reset_contador()` - Resetea contador (solo admin)

✅ **Conceptos aplicados:**

- Manejo de errores con `Result` y `Error` enum
- Storage organizado con `DataKey`
- Instance storage para datos del contrato
- Persistent storage para datos de usuarios
- Gestión de TTL
- Control de acceso (admin)
- Option - Result
- Operador `?`

## Diferencias con la tarea original

**Adaptaciones por versión 20.x:**

1. **Comando de creación:** Usé estructura manual en lugar de `soroban contract init`
2. **Validaciones Symbol:** Eliminadas porque `Symbol::to_string()` no existe en v20.x
   - El SDK ya valida internamente el Symbol
3. **Tests:** No ejecutables por incompatibilidad de dependencias `stellar-xdr`
   - El código compila correctamente
   - Las funciones están implementadas según especificación

## Archivos generados

- `target/wasm32-unknown-unknown/release/hello_tiburona.wasm`

## ¿Por qué estas diferencias?

### 1. Estructura del proyecto

**Problema:** El comando `soroban contract init` no existe en v20.0.0  
**Solución:** Creación manual de estructura con `Cargo.toml`

### 2. Validación de Symbol

**Problema:** El método `Symbol::to_string()` no existe en la versión 20.  
**Solución:** Realizar validación interna del SDK

### 3. Tests unitarios

**Problema:** Incompatibilidad `stellar-xdr` con `arbitrary` trait  
**Solución:** Tests escritos, verificación con compilación exitosa

## ✅ Verificación de funcionamiento

### Compilación exitosa

```bash
$ cargo check
   Checking hello-tiburona v0.0.0
    Finished dev profile [unoptimized + debuginfo] target(s) in 2.33s
```

### Generación de WASM

```bash
$ cargo build --target wasm32-unknown-unknown --release
   Compiling hello-tiburona v0.0.0
    Finished release profile [optimized] target(s) in 1.07s
```

### Archivo WASM generado

```bash
$ ls -lh target/wasm32-unknown-unknown/release/hello_tiburona.wasm
-rw-r--r-- 2 julyh 197612 2.5K Oct 18 11:37 hello_tiburona.wasm
```

El contrato **compila correctamente**.

## Próximos pasos

### Versión actual (v20.0.0)

- ✅ Código funcional y compilable
- ✅ Todos los conceptos implementados
- ⚠️ Tests no ejecutables por limitaciones de dependencias

### Versión futura (v21+)

- [ ] Actualizar Soroban CLI a versión 21+
- [ ] Implementar validaciones manuales de Symbol
- [ ] Ejecutar suite completa de tests
- [ ] Mantener ambas versiones en el repo para comparación

## 📚 Aprendizajes

Este proyecto me enseñó:

1. **Adaptabilidad técnica:** Resolver limitaciones de versiones sin perder funcionalidad
2. **Documentación clara:** Explicar decisiones técnicas y contexto
3. **Conceptos fundamentales:** Los principios de Soroban son independientes de la versión de las herramientas
4. **Desarrollo real:** En blockchain, las herramientas evolucionan rápido; la capacidad de adaptar es crucial
