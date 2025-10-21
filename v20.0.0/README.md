# Hello Tiburona v20.0.0 🦈

## Estado: Implementación funcional con limitaciones

---

## 📋 Información de Versión

- **Soroban CLI:** 20.0.0
- **Soroban SDK:** 20.5.0
- **Entorno:** Windows 10
- **Fecha:** Octubre 2025

---

## ✅ Funcionalidades Implementadas

Todas las funciones según especificación:
- `initialize()` - Inicializa el contrato con admin
- `hello()` - Registra saludos
- `get_contador()` - Consulta el contador de saludos
- `get_ultimo_saludo()` - Consulta último saludo de un usuario
- `reset_contador()` - Resetea contador (solo admin)

---

## ⚠️ Limitaciones de v20.0.0

1. **`soroban contract init` no disponible**
   - Solución: Estructura creada manualmente

2. **Validaciones de Symbol limitadas**
   - `Symbol::to_string()` no existe en v20.x
   - El SDK valida internamente

3. **Tests no ejecutables**
   - Incompatibilidad de dependencias `stellar-xdr` con `arbitrary`
   - Tests escritos pero no verificables

4. **Sin optimización**
   - Comando `soroban contract optimize` no disponible

---

## 📊 Resultados

### Compilación exitosa ✅
```bash
cargo check
cargo build --target wasm32-unknown-unknown --release
```

### WASM generado
- **Tamaño:** 2.5KB
- **Ubicación:** `target/wasm32-unknown-unknown/release/hello_tiburona.wasm`

---

## 📸 Capturas

Ver carpeta `img/` para evidencia de:
- Compilación exitosa
- Generación de WASM
- Verificación de archivos

---

## 🔗 Documentación del Problema

**Issue reportado:** [#18 - Dificultad para instalar Soroban CLI versión actual](https://github.com/BuenDia-Builders/codigofutura/issues/18)

Documenta:
- Problema de instalación de versión actual
- Solución temporal con v20.0.0
- Recomendación de usar WSL

---

## ➡️ Migración a v23.1.4

Debido a las limitaciones, se implementó una **versión completa usando WSL**.

Ver: [../v23.1.4/README.md](../v23.1.4/README.md)

---

## 💡 Lecciones Aprendidas

- Documentar problemas ayuda a encontrar soluciones
- Las versiones antiguas pueden ser un punto de partida
- La estructura del código es más importante que las herramientas
- Los conceptos fundamentales se mantienen entre versiones


