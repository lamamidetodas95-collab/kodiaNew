# KodiaNew - Kodia con 9Router Integrado

Este es un fork de **Kodia** (VS Code fork con AI) con integración nativa de **9Router** para usar modelos de IA gratuitos sin límites.

## 🎯 ¿Qué es esto?

**KodiaNew** incluye soporte nativo para [9Router](https://github.com/decolua/9router), un router de APIs de IA que permite:

- ✅ Usar modelos premium **gratis** (Claude Sonnet 4.5, GPT-4, DeepSeek, etc.)
- ✅ Sin límites de uso (depende de tu instancia de 9Router)
- ✅ Integración nativa (no necesitas configurar providers externos)
- ✅ Failover automático entre proveedores

## 🚀 Cambios Realizados

Se modificaron **3 archivos principales** para agregar el provider `nineRouter`:

### 1. `src/vs/workbench/contrib/void/common/modelCapabilities.ts`
- Agregado endpoint por defecto: `http://localhost:20128`
- Agregados modelos del catálogo de 9Router

### 2. `src/vs/workbench/contrib/void/common/voidSettingsTypes.ts`
- Agregada información de display para 9Router
- Documentación en español

### 3. `src/vs/workbench/contrib/void/electron-main/llmMessage/sendLLMMessage.impl.ts`
- Implementación del cliente SDK para 9Router
- Manejo de mensajes compatible con OpenAI API

## 📋 Requisitos Previos

1. **9Router corriendo localmente**:
   ```bash
   git clone https://github.com/decolua/9router
   cd 9router
   npm install
   npm start
   ```
   Por defecto corre en `http://localhost:20128`

2. **Dependencias de compilación**:
   - Node.js 20.x
   - Python 3.x
   - Windows Build Tools (si estás en Windows)

## 🔧 Compilar KodiaNew

### Windows

```powershell
# Instalar dependencias
npm install

# Compilar React components
npm run buildreact

# Compilar cliente
npm run compile-client

# Compilar todo
npm run compile
```

### Linux/Mac

```bash
# Instalar dependencias
npm install

# Compilar
npm run compile
```

## 🎮 Uso

Una vez compilado:

1. Abre KodiaNew
2. Ve a Settings → Void → Providers
3. Selecciona **9Router** como provider
4. Los modelos disponibles son:
   - `kr/claude-sonnet-4.5` - Claude Sonnet 4.5 (Kiro AI)
   - `kr/glm-5` - GLM-5 (Kiro AI)
   - `opencode/claude-sonnet-4.5` - Claude Sonnet 4.5 (OpenCode)
   - `deepseek-chat` - DeepSeek Chat
   - `deepseek-reasoner` - DeepSeek Reasoner

5. Empieza a codear con IA gratis! 🎉

## 📚 Documentación Adicional

- [INTEGRATION_9ROUTER.md](./INTEGRATION_9ROUTER.md) - Guía técnica de integración
- [README_9ROUTER_ES.md](./README_9ROUTER_ES.md) - Documentación completa en español
- [CHANGELOG_9ROUTER.md](./CHANGELOG_9ROUTER.md) - Registro de cambios
- [QUICK_START.md](./QUICK_START.md) - Guía de inicio rápido
- [WINDOWS_QUICKSTART.md](./WINDOWS_QUICKSTART.md) - Guía específica para Windows

## 🔍 Verificar Integración

Ejecuta el script de verificación:

```powershell
.\verify-9router-integration.ps1
```

Este script verifica que todos los cambios de 9Router estén correctamente integrados.

## 🤝 Contribuir

Este es un proyecto personal para uso propio. Si encuentras bugs o mejoras:

1. Abre un Issue
2. Haz un Pull Request
3. Contacta al mantenedor

## 📄 Licencia

Este proyecto hereda la licencia de Kodia/VS Code. Ver [LICENSE.txt](./LICENSE.txt) para más detalles.

## 🙏 Créditos

- **Kodia**: https://github.com/voideditor/void (VS Code fork con AI)
- **9Router**: https://github.com/decolua/9router (AI Router gratuito)
- **VS Code**: https://github.com/microsoft/vscode (Editor base)

---

**Nota**: Este fork es para uso personal y educativo. Respeta los términos de servicio de los proveedores de IA que uses a través de 9Router.
