# Ojo de Zeus 2 🔱

[![Python](https://img.shields.io/badge/Python-3.9%2B-blue.svg)](#)
[![OSINT](https://img.shields.io/badge/Category-OSINT-brightgreen.svg)](#)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](#)
[![Platform](https://img.shields.io/badge/Platforms-Linux%20%7C%20macOS%20%7C%20Termux-informational.svg)](#)

**Ojo de Zeus 2** es una herramienta **OSINT en Python** para verificar si **usuarios o correos** existen en distintos sitios. Utiliza múltiples métodos (URL final, contenido, códigos HTTP, etc.), permite **crear/gestionar métodos** por sitio y funciona tanto en modo **gráfico** (Firefox + GeckoDriver) como en **modo oculto**.

---

## 📚 Tabla de Contenidos
- [Historia](#-historia)
- [Características](#-características)
- [Instalación](#-instalación)
  - [Linux / macOS](#-linux--macos)
  - [Termux (Android)](#-termux-android)
  - [Windows (opcional)](#-windows-opcional)
- [Uso](#-uso)
- [Estructura del proyecto](#-estructura-del-proyecto)
- [Requisitos](#-requisitos)
- [Notas de modo gráfico (Firefox/GeckoDriver)](#-notas-de-modo-gráfico-firefoxgeckodriver)
- [Solución de problemas (FAQ)](#-solución-de-problemas-faq)
- [Roadmap](#-roadmap)
- [Contribuciones](#-contribuciones)
- [Licencia](#-licencia)
- [Créditos](#-créditos)

---

## 🧭 Historia
Hola, Desde pequeño me ha apasionado la informática y la seguridad digital.  
Un incidente reciente, en el que un familiar sufrió el robo de un celular, me motivó a crear esta herramienta. Aunque el valor del dispositivo no era lo importante, supe que el ladrón empezo a hacer mal uso del contenido personal.  

Gracias a una cuenta ingresada en el teléfono que aunque no tenia su nombre pero si un usuario y un correo puede hacer lo que ahora **OJO DE ZEUS 2** ase pude rastrear la identidad del delincuente y ubicarlo en sus zonas frecuentes. Esa experiencia me inspiró a desarrollar **Ojo de Zeus 2**, con la idea de que cualquiera pueda contar con una herramienta similar para obtener datos OSINT de manera sencilla sin que tenga mucha experiencia y asi ayudar a que mas que a recuperar las cosas materiales podamos recuperar lo todavia mas valioso nuestros datos privados que fueron tomados por la fuerza.
  **Ojo de Zeus 2**.

---

## ✨ Características
- **Verificación OSINT** de usuarios/correos en múltiples sitios:
  - Seguimiento de **URL final** y redirecciones.
  - Búsqueda de **fragmentos de contenido** (selectores/patrones).
  - Inspección de **códigos de estado HTTP** y errores típicos.
- **Gestor de métodos/sitios**: agregar, probar, comparar y eliminar métodos guardados.
- **Multiplataforma**: Linux, macOS, **Termux** (Android) y SBCs (p. ej., Orange Pi).
- **Tolerante a fallos**: intenta no cerrarse ante errores de red/sitio.
- **Modo gráfico y headless**: usa Firefox + GeckoDriver si hay GUI; si no, intenta sin GUI.

---

## ⚙️ Instalación

### 🔹 Linux / macOS
> Recomendado usar entorno virtual.


# 1) Crear y activar venv
```bash     
python3 -m venv venv
source venv/bin/activate
```

# 2) Actualizar pip e instalar dependencias
```bash
pip install --upgrade pip
pip install -r requirements.txt
```

# 3) (Opcional) Comprobar versión de Python
```bash
python3 --version
```

### 🔹 Termux (Android)
> Pasos probados en Termux moderno. No intentes instalar "pip" con pkg: ya viene con Python.


# 1) Actualizar paquetes
```bash
pkg update -y && pkg upgrade -y
```

# 2) Dependencias básicas
```bash
pkg install -y git python
```

# 3) (Opcional) Herramientas de compilación si alguna lib lo pide
```bash
pkg install -y clang make
```

# 4) Clonar e instalar
```bash
git clone https://github.com/KxK-code/ojo-de-zeus-2.git
cd ojo-de-zeus-2
pip install --upgrade pip
pip install -r requirements.txt
```

# 5) Ejecutar (ver sección "Uso" más abajo)
'''bash
 python3 ojo_de_zeus_2.py
```

**Notas rápidas para Termux:**
- Si ves algo como *“Installing pip is forbidden”*, significa que intentaste instalar **pip** con `pkg`. No lo hagas; ya viene con `python`.
- Si alguna dependencia de `requirements.txt` falla en Termux, instala primero sus binarios (ej. `pkg install libxml2 libxslt`) y reintenta `pip install -r requirements.txt`.

### 🔹 Windows (opcional)
> Si lo necesitas en Windows nativo:

```powershell
# 1) Python 3.9+ instalado y agregado al PATH
# 2) En PowerShell, dentro del proyecto:
python -m venv venv
.\venv\Scripts\Activate.ps1
pip install --upgrade pip
pip install -r requirements.txt
```

---

## 🚀 Uso
Ejecuta el menú principal:

```bash
python3 ojo_de_zeus_2.py
```

Ejemplo de salida:
```text
[*] Verificando: usuario=ejemplo123
[✓] Encontrado en: sitioA
[✗] No encontrado en: sitioB
[✓] Encontrado en: sitioC
```

Sugerencias:
- Corre primero con 1–2 sitios para validar dependencias.
- Guarda métodos que funcionen; elimina los rotos desde el menú.

---

## 📂 Estructura del proyecto
```text
ojo-de-zeus-2/
├─ motores/
│  ├─ buscador_auto_graficos.py
│  ├─ creador_auto_graficos.py
│  ├─ comparador.py
│  └─ utils.py
├─ sitios.json             # Métodos y sitios guardados (editable)
├─ ojo_de_zeus_2.py        # Menú principal
├─ requirements.txt        # Dependencias Python
└─ README.md
```

> *La estructura puede variar ligeramente según las versiones; mantén `sitios.json` bajo control (respáldalo).*

---

## 🧩 Requisitos
- **Python 3.9+**
- Conexión a Internet estable.
- (Opcional modo gráfico) **Firefox** + **GeckoDriver** en el `PATH`.

---

## 🖥️ Notas de modo gráfico (Firefox/GeckoDriver)
- **Debian/Ubuntu/Orange Pi**:
  ```bash
  sudo apt-get update
  sudo apt-get install -y firefox-esr
  ```
- **GeckoDriver**: descarga binario para tu arquitectura y colócalo en un directorio del `PATH` (por ejemplo `/usr/local/bin`). Verifica:
  ```bash
  geckodriver --version
  ```
- Sin GUI disponible → el programa intenta **headless** cuando corresponda.

---

## 🛠️ Solución de problemas (FAQ)

**1) Termux dice “Installing pip is forbidden”.**  
No instales `pip` con `pkg`. Usa:
```bash
pkg install -y python
pip --version
```

**2) Falló `pip install -r requirements.txt` por una lib del sistema.**  
Instala la lib por `pkg` (Termux) o `apt` (Debian) y reintenta:
```bash
# Termux (ejemplos)
pkg install -y libxml2 libxslt openssl

# Debian/Ubuntu (ejemplos)
sudo apt-get install -y libxml2-dev libxslt1-dev
```

**3) No detecta Firefox/GeckoDriver.**  
Revisa que ambos estén en `PATH`:
```bash
which firefox
which geckodriver
```
Si no aparecen, instala y exporta `PATH` o mueve el binario a `/usr/local/bin`.

**4) ¿Dónde están los métodos guardados?**  
En `sitios.json`. Haz respaldo antes de editar.

**5) ¿Puedo correrlo en Orange Pi sin monitor?**  
Sí. Usa SSH y modo headless. Si luego agregas GUI (Xfce/Weston), podrás usar Firefox/GeckoDriver.

---

## 🗺️ Roadmap
- Nuevos métodos: `json_response_check`, `captcha_detect`, `custom_selector_check`.
- Modo servicio con **API REST**.
- Panel web ligero para ejecutar búsquedas.
- Exportación a CSV/JSON enriquecido con metadatos.

---

## 🤝 Contribuciones
1. Crea un *fork*.
2. Abre rama: `feat/tu-mejora`.
3. Asegura compatibilidad con Termux y Linux.
4. Pull Request con pasos de prueba y capturas, si es posible.

---

## 📄 Licencia
**MIT** — úsalo, modifícalo y compártelo manteniendo los créditos.

---

## 🙌 Créditos
Proyecto creado y mantenido por **Kike_kike (KxK-code)**.  
Agradecimientos a la comunidad OSINT por ideas, pruebas y retroalimentación.

---  
