# 🌱 Huerta Emoji

**Diseñá tu cantero de huerta con emojis — 100% offline, liviano y táctil.**

[![Build APK](https://github.com/TU_USUARIO/huerta-emoji/actions/workflows/android.yml/badge.svg)](https://github.com/TU_USUARIO/huerta-emoji/actions/workflows/android.yml)

---

## 📱 ¿Qué hace la app?

| Función | Descripción |
|---------|-------------|
| 🌿 **Grilla visual** | Diseñá tu huerta en una grilla de emojis configurable (hasta 30×40) |
| 🪴 **Gestión de plantas** | Agregá, editá y eliminá plantas con emoji, nombre y distancia mínima |
| ⚠️ **Validación** | Detecta automáticamente plantas demasiado cerca (marcadas en rojo) |
| 🤝 **Asociaciones** | Sugerencias de plantas compatibles (ej: 🍅 + 🌿) |
| 💾 **Guardado** | Guarda múltiples diseños en el dispositivo (sin internet) |
| 🖼️ **Exportación** | Exportá tu diseño como PNG o texto de emojis |
| ⚙️ **Configurable** | Cambiá el tamaño de la grilla en cualquier momento |

---

## 🗂️ Estructura del proyecto

```
huerta-emoji/
├── app/
│   └── src/main/
│       ├── assets/
│       │   └── app.html              ← Toda la lógica de la app (HTML + CSS + JS)
│       ├── java/com/huerta/cantero/
│       │   └── MainActivity.kt       ← Shell Android con WebView
│       ├── res/
│       │   ├── layout/activity_main.xml
│       │   └── values/{strings,themes,colors}.xml
│       └── AndroidManifest.xml
├── .github/
│   └── workflows/
│       └── android.yml               ← CI/CD para generar APK automáticamente
├── build.gradle
├── settings.gradle
└── README.md
```

---

## 🚀 Cómo usar el proyecto

### Requisitos
- **Android Studio** Hedgehog (2023.1) o superior, **o**
- Solo una cuenta de GitHub (para el APK automático)

### Opción A — Compilar localmente

```bash
# 1. Clonar el repositorio
git clone https://github.com/TU_USUARIO/huerta-emoji.git
cd huerta-emoji

# 2. Dar permisos al wrapper de Gradle
chmod +x gradlew

# 3. Compilar el APK de debug
./gradlew assembleDebug

# 4. El APK estará en:
# app/build/outputs/apk/debug/app-debug.apk
```

### Opción B — Abrir en Android Studio

1. Abrí Android Studio → **Open** → seleccioná la carpeta `huerta-emoji`
2. Esperá que sincronice Gradle (primera vez tarda ~3 min)
3. Menú **Build → Build Bundle(s) / APK(s) → Build APK(s)**
4. El APK aparecerá en `app/build/outputs/apk/debug/`

---

## ⚙️ Cómo generar el APK con GitHub Actions

### Primera vez

1. **Subí el proyecto a GitHub:**
   ```bash
   git init
   git add .
   git commit -m "🌱 Initial commit - Huerta Emoji app"
   git branch -M main
   git remote add origin https://github.com/TU_USUARIO/huerta-emoji.git
   git push -u origin main
   ```

2. GitHub Actions **se ejecuta automáticamente** al hacer push.

3. Cada push a `main` dispara el workflow.

---

## 📥 Cómo descargar el APK desde GitHub Actions

1. Ir a tu repositorio en GitHub
2. Click en la pestaña **"Actions"** (menú superior)
3. Click en el último workflow exitoso (ícono ✅ verde)
4. Bajar hasta la sección **"Artifacts"**
5. Click en **`huerta-emoji-apk-XX`** para descargar el ZIP
6. Descomprimir → obtener `app-debug.apk`

> 💡 **Tip:** También podés ir directo a  
> `https://github.com/TU_USUARIO/huerta-emoji/actions`

---

## 📲 Cómo instalar en Android

### Paso 1 — Habilitar instalación desde fuentes desconocidas

**Android 8.0+:**
- Ajustes → Aplicaciones → (nombre del navegador/gestor de archivos) → Instalar aplicaciones desconocidas → **Permitir**

**Android 7.0 o anterior:**
- Ajustes → Seguridad → **Fuentes desconocidas** → Activar

### Paso 2 — Transferir e instalar el APK

**Opción 1 — USB:**
```
1. Conectá el teléfono con cable USB
2. Copiá app-debug.apk al almacenamiento interno
3. Abrí el gestor de archivos en el teléfono
4. Localizá app-debug.apk y tocá para instalar
```

**Opción 2 — Google Drive / Email:**
```
1. Subí el APK a Google Drive
2. Desde el teléfono, abrilo y tocá "Instalar"
```

**Opción 3 — ADB (para desarrolladores):**
```bash
adb install app-debug.apk
```

---

## 🌱 Cómo usar la app

### Diseñar tu cantero

1. **Seleccioná una planta** en la fila de chips de colores
2. **Tocá celdas** de la grilla para colocarla
3. Podés **arrastrar el dedo** para pintar varias celdas
4. Usá **🧹 Borrar** para eliminar celdas individuales
5. El ícono **⚙️** permite cambiar el tamaño de la grilla
6. El ícono **🗑️** limpia toda la grilla

### Validaciones automáticas

- Las celdas en **rojo** indican que dos plantas iguales están demasiado cerca
- La distancia mínima está definida por planta (ej: 🍅 Tomate = 50 cm = 5 celdas)

### Asociaciones

- La pestaña **🤝 Asociaciones** muestra qué plantas combinan bien
- Aparecen **sugerencias automáticas** basadas en tu diseño actual

### Exportar

- **📋 Copiar texto:** Copia la grilla de emojis al portapapeles
- **⬇️ Guardar .txt:** Descarga un archivo de texto con el diseño
- **🖼️ Exportar PNG:** Genera una imagen del cantero

---

## 🔧 Modificar la app

Toda la lógica visual está en un único archivo:

```
app/src/main/assets/app.html
```

Para agregar plantas por defecto, editá el array en el JS:

```javascript
let plants = [
  { id: 'lechuga',   emoji: '🥬', name: 'Lechuga',   dist: 30 },
  { id: 'tomate',    emoji: '🍅', name: 'Tomate',     dist: 50 },
  // Agregá aquí...
  { id: 'brocoli',   emoji: '🥦', name: 'Brócoli',    dist: 40 },
];
```

Para agregar asociaciones:

```javascript
const ASSOCIATIONS = [
  // type: 'good' | 'warn' | 'bad'
  { a: 'tomate', b: 'albahaca', type: 'good', note: 'Se protegen mutuamente' },
];
```

---

## 📋 Requisitos mínimos

| Requisito | Valor |
|-----------|-------|
| Android | 5.0 (API 21) o superior |
| RAM | 512 MB (funciona en 2-4 GB perfectamente) |
| Almacenamiento | ~5 MB |
| Internet | **No requerido** — 100% offline |
| Permisos | Ninguno requerido |

---

## 🛠️ Stack técnico

| Capa | Tecnología |
|------|-----------|
| Shell Android | Kotlin + WebView |
| Interfaz | HTML5 + CSS3 + JavaScript vanilla |
| Almacenamiento | localStorage (datos del juego) |
| Build | Gradle 8.4 + AGP 8.2 |
| CI/CD | GitHub Actions |

---

## 📄 Licencia

MIT — Libre para usar, modificar y distribuir.

---

*Hecho con 🌱 para planificar huertas de forma visual y táctil.*
