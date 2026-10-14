# Obsidian Ollama Translator

Plugin para Obsidian que permite traducir textos seleccionados, archivos completos o usar una modal de traducción rápida usando LLMs locales a través de **Ollama**.

## Características

- 🔒 **Privacidad total**: Todo se ejecuta localmente, no hay datos que salgan de tu máquina
- 🌐 **Múltiples idiomas**: Soporte para 40+ idiomas
- ⚡ **Tres formas de traducir**:
  - Selección de texto (atajo: `Ctrl+Shift+T`)
  - Archivo completo
  - Modal de traducción rápida (`Ctrl+Alt+T`)
- 🤖 **Gestión de modelos**: Ver, seleccionar y descargar modelos desde la configuración
- 📋 **Opciones flexibles**: Reemplazar selección, copiar al portapapeles, mostrar en modal
- 🎨 **UI integrada**: Menús contextuales, barra de estado, modales nativos

## Requisitos

- **Obsidian** v1.5.0+
- **Ollama** instalado y corriendo (por defecto en `http://localhost:11434`)
- Al menos un modelo descargado (ej: `llama3.1:8b`, `qwen2.5:7b`, `gemma2:9b`)

## Instalación

### Desde la comunidad (cuando esté disponible)

1. Abre Configuración → Community Plugins
2. Busca "Ollama Translator"
3. Instala y habilita

### Manual (desarrollo)

```bash
# Clonar el repo
git clone <repo-url>
cd obsidian-ollama-translator

# Instalar dependencias
npm install

# Compilar
npm run build

# Copiar a tu vault de Obsidian
cp -r dist/* <tu-vault>/.obsidian/plugins/ollama-translator/
```

## Uso

### 1. Configurar Ollama

1. Ve a **Configuración → Ollama Translator**
2. Verifica el **Host de Ollama** (default: `http://localhost:11434`)
3. Click en **"Probar conexión"**
4. Click en **"Cargar modelos"** o **"Descargar nuevo modelo"**
5. Selecciona tu **Modelo por defecto**

### 2. Traducir selección

- Selecciona texto en el editor
- `Ctrl+Shift+T` (o click derecho → 🌐 Traducir selección)
- Se traduce al idioma por defecto

### 3. Traducir a idioma específico

- Selecciona texto
- Click derecho → 🌐 Traducir a...
- Elige el idioma destino

### 4. Traducir archivo completo

- Click derecho en un archivo `.md` en el explorador
- 🌐 Traducir archivo completo
- Elige idioma → Se crea un archivo nuevo `_translated.md`

### 5. Traducción rápida (modal)

- `Ctrl+Alt+T` (o click en el icono 🌐 en la barra de estado)
- Escribe/pega texto → Elige idioma → Traducir
- Copia el resultado o úsalo directamente

## Atajos de teclado

| Acción             | Atajo          |
| ------------------ | -------------- |
| Traducir selección | `Ctrl+Shift+T` |
| Traducción rápida  | `Ctrl+Alt+T`   |

*Personalizables en Configuración → Hotkeys*

## Configuración

### Conexión

- **Host de Ollama**: URL del servidor (ej: `http://localhost:11434`, `http://192.168.1.100:11434`)

### Modelos

- **Modelo por defecto**: El usado para traducciones
- **Descargar modelo**: Escribe nombre (ej: `llama3.1:8b`, `qwen2.5:14b`, `mistral-nemo`)

### Traducción

- **Idioma destino por defecto**: Idioma al que traducir automáticamente
- **Prompt del sistema**: Instrucciones para el modelo (personalizable)
- **Temperatura**: 0.0-1.0 (0 = más determinístico)
- **Máximo tokens**: Límite de longitud de respuesta
- **Timeout**: Tiempo máximo de espera (ms)

### Opciones avanzadas

- **Mostrar notificaciones**: Toast al completar
- **Copiar al portapapeles**: Auto-copiar traducción
- **Reemplazar selección**: Sustituir texto original en el editor

## Modelos recomendados

| Modelo         | Tamaño | Calidad | Velocidad | Uso recomendado |
| -------------- | ------ | ------- | --------- | --------------- |
| `llama3.1:8b`  | 4.7 GB | ⭐⭐⭐⭐    | Rápido    | General         |
| `qwen2.5:7b`   | 4.4 GB | ⭐⭐⭐⭐    | Rápido    | Multilingüe     |
| `gemma2:9b`    | 5.4 GB | ⭐⭐⭐⭐    | Media     | General         |
| `llama3.1:70b` | 40 GB  | ⭐⭐⭐⭐⭐   | Lento     | Máxima calidad  |
| `qwen2.5:32b`  | 19 GB  | ⭐⭐⭐⭐⭐   | Media     | Calidad alta    |

```bash
# Descargar modelos recomendados
ollama pull llama3.1:8b
ollama pull qwen2.5:7b
ollama pull gemma2:9b
```

## Desarrollo

```bash
# Instalar dependencias
npm install

# Desarrollo (watch mode)
npm run dev

# Build producción
npm run build

# Lint
npm run lint
```

## Estructura del proyecto

```
obsidian-ollama-translator/
├── src/
│   ├── main.ts              # Plugin principal
│   ├── settings.ts          # Tipos y defaults de settings
│   ├── ollama-client.ts     # Cliente API Ollama
│   ├── translation-service.ts # Servicio de traducción
│   └── settings-tab.ts      # UI de configuración
├── styles.css               # Estilos del plugin
├── manifest.json            # Metadata del plugin
├── package.json
├── tsconfig.json
└── esbuild.config.mjs
```

## API de Ollama usada

- `GET /api/tags` - Listar modelos
- `POST /api/pull` - Descargar modelo
- `POST /api/chat` - Chat completion (streaming y no streaming)

## Solución de problemas

| Problema                       | Solución                                                |
| ------------------------------ | ------------------------------------------------------- |
| "No se pudo conectar a Ollama" | Verifica que Ollama esté corriendo: `ollama serve`      |
| "Modelo no encontrado"         | Descarga el modelo: `ollama pull <modelo>`              |
| Timeout                        | Aumenta el timeout en settings o usa modelo más pequeño |
| Traducción lenta               | Usa modelo más pequeño (8b vs 70b) o reduce max_tokens  |
| Error de CORS                  | Ollama no tiene CORS; usa en desktop o configura proxy  |

## Licencia

MIT - Libre para uso personal y comercial.

## Créditos

- [Ollama](https://ollama.ai) - Motor de inferencia local
- [Obsidian](https://obsidian.md) - Editor de notas
- Modelos: Meta (Llama), Alibaba (Qwen), Google (Gemma), Mistral AI

---

**Desarrollado para Antalciddes Olivo** - Traducciones privadas, seguras y locales.