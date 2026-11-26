# GitHub Actions Workflows para KodiaNew

Este directorio contiene los workflows de GitHub Actions para compilar KodiaNew automáticamente en la nube.

## 📋 Workflows Disponibles

### 1. `quick-test.yml` - Test Rápido ⚡

**Propósito**: Verificar que la integración de 9Router esté correcta sin compilar todo.

**Trigger**:
- Push a `feat/9router-integration`
- Manual desde GitHub Actions

**Duración**: ~5-10 minutos

**Qué hace**:
- ✅ Verifica que los 3 archivos de 9Router existan
- ✅ Verifica que contengan el código de integración
- ✅ Instala dependencias
- ✅ Genera reporte de test

**Usar para**: Verificar rápidamente que todo esté en su lugar.

---

### 2. `build-windows.yml` - Build Básico 🔨

**Propósito**: Compilar el código TypeScript y React.

**Trigger**:
- Push a `feat/9router-integration`, `main`, `master`
- Pull requests
- Manual desde GitHub Actions

**Duración**: ~30-60 minutos

**Qué hace**:
- ✅ Instala Node.js 20
- ✅ Instala Python 3.11
- ✅ Instala dependencias npm
- ✅ Compila React components (`npm run buildreact`)
- ✅ Compila cliente (`npm run compile-client`)
- ✅ Compila proyecto completo (`npm run compile`)
- ✅ Empaqueta en ZIP
- ✅ Sube artefacto a GitHub

**Usar para**: Build rápido del código compilado.

---

### 3. `build-full.yml` - Build Completo 🚀

**Propósito**: Crear un paquete completo distribuible de KodiaNew.

**Trigger**:
- Manual desde GitHub Actions
- Push de tags (ej: `v1.0.0`)

**Duración**: ~60-120 minutos

**Qué hace**:
- ✅ Instala Node.js 20.18.0
- ✅ Instala Python 3.11
- ✅ Instala Rust toolchain
- ✅ Compila React components
- ✅ Compila TypeScript completo
- ✅ Compila CLI en Rust
- ✅ Crea paquete de distribución
- ✅ Incluye documentación de 9Router
- ✅ Crea ZIP final: `KodiaNew-Windows-x64.zip`
- ✅ Si es tag, crea Release en GitHub

**Usar para**: Crear ejecutable distribuible completo.

---

## 🚀 Cómo Usar los Workflows

### Opción A: Ejecutar Manualmente

1. Ve a tu repositorio en GitHub:
   ```
   https://github.com/lamamidetodas95-collab/kodiaNew/actions
   ```

2. Selecciona el workflow que quieres ejecutar:
   - **Quick Test Build** - Para verificar rápido
   - **Build KodiaNew Windows** - Para build básico
   - **Build KodiaNew Full Package** - Para build completo

3. Click en **"Run workflow"** (botón a la derecha)

4. Selecciona el branch: `feat/9router-integration`

5. Click en **"Run workflow"** (verde)

6. Espera a que termine (verás el progreso en tiempo real)

7. Descarga el artefacto:
   - Click en el workflow completado
   - Scroll hasta "Artifacts"
   - Descarga el ZIP

---

### Opción B: Crear un Tag para Release

Para crear una release automática con el build completo:

```powershell
# En tu repositorio local
cd l:\kodia-upload

# Crear tag
git tag -a v1.0.0 -m "KodiaNew v1.0.0 - Primera release con 9Router"

# Subir tag
git push origin v1.0.0
```

Esto activará automáticamente el workflow `build-full.yml` y creará una Release en GitHub con el ZIP descargable.

---

## 📦 Qué Obtendrás

### Desde `quick-test.yml`:
- `test-report.md` - Reporte de verificación

### Desde `build-windows.yml`:
- `kodia-windows-build.zip` - Código compilado
- Carpetas `out/` y `extensions/`

### Desde `build-full.yml`:
- `KodiaNew-Windows-x64.zip` - **Paquete completo distribuible** ⭐
  - Contiene todo el código compilado
  - Ejecutable CLI (si Rust compila)
  - Documentación de 9Router
  - Listo para ejecutar

---

## ⚙️ Requisitos en GitHub Actions

Los workflows usan runners de GitHub con:

- ✅ Windows Server 2022
- ✅ Node.js 20.x
- ✅ Python 3.11
- ✅ Rust toolchain (stable)
- ✅ Visual Studio Build Tools 2022
- ✅ Windows SDK (incluido en runner)

**No necesitas instalar nada localmente** - GitHub Actions tiene todo pre-instalado.

---

## 🔧 Troubleshooting

### Si el workflow falla:

1. **Check the logs**:
   - Ve al workflow fallido
   - Click en el job que falló
   - Revisa los logs para ver el error

2. **Errores comunes**:

   - **"Cannot find module"**: Faltan dependencias
     - Solución: Workflow instala con `--legacy-peer-deps`
   
   - **"Timeout"**: El build tomó demasiado tiempo
     - Solución: Aumentar `timeout-minutes` en el workflow
   
   - **"Rust compile failed"**: CLI no compila
     - Solución: Workflow tiene `continue-on-error: true` para Rust

3. **Si necesitas modificar el workflow**:
   ```powershell
   # Editar el workflow
   code l:\kodia-upload\.github\workflows\build-full.yml
   
   # Commit y push
   cd l:\kodia-upload
   git add .github/workflows/
   git commit -m "ci: Update workflow"
   git push origin feat/9router-integration
   ```

---

## 📊 Tiempos Estimados

| Workflow | Duración | Resultado |
|----------|----------|-----------|
| quick-test | 5-10 min | Verificación rápida |
| build-windows | 30-60 min | Build básico |
| build-full | 60-120 min | Paquete completo ⭐ |

---

## 🎯 Workflow Recomendado

**Para obtener un KodiaNew ejecutable**:

1. Ejecuta **"Build KodiaNew Full Package"** manualmente
2. Espera ~90 minutos
3. Descarga `KodiaNew-Windows-x64.zip` de Artifacts
4. Extrae y ejecuta

O mejor aún:

1. Crea un tag: `git tag v1.0.0`
2. Push: `git push origin v1.0.0`
3. GitHub crea Release automáticamente
4. Descarga desde Releases (más permanente)

---

## 🔗 Enlaces Útiles

- **Actions**: https://github.com/lamamidetodas95-collab/kodiaNew/actions
- **Releases**: https://github.com/lamamidetodas95-collab/kodiaNew/releases
- **Docs GitHub Actions**: https://docs.github.com/en/actions

---

## ✅ Próximos Pasos

1. ✅ Workflows creados y pusheados
2. ⏭️ Ejecutar workflow manualmente
3. ⏭️ Descargar artefacto
4. ⏭️ Probar ejecutable
5. ⏭️ Crear release si funciona bien

---

**¡Los workflows están listos para usar!** 🚀
