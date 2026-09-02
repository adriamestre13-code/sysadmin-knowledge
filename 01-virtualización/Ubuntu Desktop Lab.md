# 🐧 Creación de una Máquina Virtual con Ubuntu Desktop

Guía paso a paso para desplegar Ubuntu Desktop en Oracle VirtualBox y la explicación técnica de cada decisión.

---

## 🎯 ¿Por qué Ubuntu Desktop?

Ubuntu es la distribución de Linux más utilizada en entornos corporativos y de desarrollo. Dominar su versión Desktop es fundamental para IT Helpdesk y Sysadmin por varias razones:
* **Ecosistema estándar:** Es la base de muchas infraestructuras empresariales y la referencia principal para aprender la terminal Linux.
* **Gestión de paquetes (APT):** Permite practicar la instalación, actualización y administración de software mediante línea de comandos.
* **Integración con servidores:** Utiliza la misma base del sistema operativo que Ubuntu Server, lo que facilita el salto a la administración de servidores Linux.
* **Diagnóstico de redes:** Ideal para ejecutar herramientas de auditoría y análisis de red basadas en Linux.

---

## 🛠️ Requisitos Previos

* **Oracle VirtualBox** instalado.
* [**ISO de Ubuntu Desktop**](https://ubuntu.com/download/desktop) (versión LTS descargable desde el sitio web oficial de Ubuntu).

---

## ⚙️ Configuración Paso a Paso de la VM (y su explicación)

### 1. Nombre y Sistema Operativo
* **Tipo:** Linux
* **Versión:** Ubuntu (64-bit)
* Recuerda desmarcar la casilla de Instalación desatendida.
<img width="913" height="719" alt="Captura de pantalla 2026-09-02 192106" src="https://github.com/user-attachments/assets/a1cd04bf-a999-4363-91ec-c0b5d32332bc" />

### 2. Memoria RAM y Procesadores (CPU)
* **RAM:** 2048 MB (2 GB) mínimo / 4096 MB (4 GB) recomendado.
* **CPUs:** 2 vCPUs recomendado.
* **EFI:** Con Ubuntu Desktop, no es necesario usar EFI puesto que puede funcionar perfectamente con MBR.
> **¿Por qué?** La interfaz gráfica de Ubuntu (GNOME) requiere al menos 2 GB de RAM para moverse con fluidez. Asignar 2 procesadores mejora notablemente la respuesta del sistema al compilar o actualizar software.
> <img width="913" height="721" alt="Captura de pantalla 2026-09-02 192351" src="https://github.com/user-attachments/assets/a1e7329e-aa29-4da9-899a-7537a2e8fc41" />

### 3. Disco Duro Virtual
* **Tamaño:** 25 GB mínimo / 40 GB recomendado.
* **Tipo de archivo:** VDI (VirtualBox Disk Image).
* **Reservar Completamente:** Deseleccionado.
> **¿Por qué?** A diferencia de Windows, Linux es más ligero en almacenamiento. La asignación dinámica evita ocupar espacio inútil en tu disco físico hasta que instales paquetes o guardes archivos.
> <img width="914" height="721" alt="Captura de pantalla 2026-09-02 192504" src="https://github.com/user-attachments/assets/ca350597-b492-40c3-853f-745f8af36fd2" />

### 4. Configuración de Red
* **Modo de red:** NAT (por defecto) o *Bridge*.
> **¿Por qué?** El modo NAT le otorga salida a Internet inmediata a la VM para descargar actualizaciones de paquetes durante y después de la instalación.

---

## 🚀 Proceso de Instalación

1. Inicia la VM y selecciona el archivo ISO de Ubuntu Desktop.
2. En el menú de arranque del instalador (GRUB), selecciona **Try or Install Ubuntu**.
3. Elige el idioma y la distribución de teclado.
4. Selecciona **Instalación normal** (incluye navegador, utilidades y paquetes de oficina) y marca la casilla **Descargar actualizaciones al instalar Ubuntu**.
5. En tipo de instalación, selecciona **Borrar disco e instalar Ubuntu** (afecta solo al disco virtual de la VM).
6. Configura tu zona horaria, nombre de usuario y contraseña.

---

## 📌 Configuración Inicial Post-Instalación
* Completa el asistente inicial de bienvenida en el escritorio.
* Instala las **VirtualBox Guest Additions** desde la terminal para habilitar pantalla completa y portapapeles compartido:
  ```bash
  sudo apt update
  sudo apt install -y build-essential dkms linux-headers-$(uname -r)
