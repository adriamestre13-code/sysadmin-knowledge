# 🪟 Creación de una Máquina Virtual con Windows 11 Enterprise

Guía paso a paso para desplegar Windows 11 Enterprise en Oracle VirtualBox y la justificación técnica de cada ajuste.

---

## 🎯 ¿Por qué Windows 11 Enterprise?

A diferencia de las versiones Home o Pro, la edición **Enterprise** incluye herramientas avanzadas indispensables para entornos corporativos y de administración de sistemas:
* **AppLocker y Windows Defender Application Control:** Control granular sobre qué aplicaciones se ejecutan.
* **DirectAccess y Always On VPN:** Conectividad remota avanzada sin intervención del usuario.
* **Credential Guard y Device Guard:** Seguridad basada en virtualización (VBS) para proteger credenciales del dominio.
* **Compatibilidad total con Active Directory y Group Policy (GPO):** Sin limitaciones de gestión en red.

---

## 🛠️ Requisitos Previos

* **Oracle VirtualBox**.
* [**ISO de evaluación de Windows 11 Enterprise**](https://www.microsoft.com/es-es/evalcenter/download-windows-11-enterprise) (descargable desde el sitio oficial de Microsoft Evaluation Center).

---

## ⚙️ Configuración Paso a Paso de la VM (y su explicación)

### 1. Nombre y Sistema Operativo
* **Tipo:** Microsoft Windows
* **Versión:** Windows 11 (64-bit)
<img width="488" height="36" alt="Captura de pantalla 2026-08-29 173910" src="https://github.com/user-attachments/assets/c5ec3187-bb7d-416e-8035-e6a4aa251553" />
* **IMPORTANTE:** Desactivar la instalación atendida, esto nos permitirá tener control sobre la instalación del SO.

### 2. Memoria RAM y Procesadores (CPU)
* **RAM:** 4096 MB (4 GB) mínimo / 8192 MB (8 GB) recomendado.
* **CPUs:** 2 vCPUs mínimo.
> **¿Por qué?** Windows 11 exige un mínimo de 4 GB de RAM y 2 núcleos para funcionar. Darle menos provocará un rendimiento extremadamente lento o errores en el instalador.

### 3. TPM 2.0 y Secure Boot
* **Habilitar EFI:** Activado.
* **Virtual TPM:** TPM 2.0.
> **¿Por qué?** Son requisitos de hardware obligatorios impuestos por Microsoft para Windows 11. VirtualBox permite emular ambos componentes para evitar trucos en el registro durante la instalación.

### 4. Disco Duro Virtual
* **Tamaño:** 64 GB mínimo.
* **Tipo de archivo:** VDI (VirtualBox Disk Image).
* **Reservado dinámicamente:** Seleccionado.
> **¿Por qué?** El espacio asignado dinámicamente solo consume espacio real en tu disco físico a medida que la VM llena el espacio, optimizando el almacenamiento del Host.

### 5. Configuración de Red
* **Modo de red:** NAT (para acceso a internet) o *Bridge* (para simular un equipo real en tu red local).
> **¿Por qué?** NAT aísla la máquina virtual del resto de tus dispositivos domésticos mientras le da acceso a la red para actualizaciones.

---

## 🚀 Proceso de Instalación

1. Inicia la VM y selecciona el archivo ISO de Windows 11 cuando lo solicite.
2. Presiona cualquier tecla cuando aparezca *“Press any key to boot from CD or DVD...”*.
3. Selecciona idioma, formato de hora y teclado.
4. Completa el asistente de instalación seleccionando la opción **Personalizada: instalar solo Windows (avanzado)**.
5. Elige el disco sin asignar y haz clic en **Siguiente**.

---

## 📌 Configuración Inicial (OOBE)
* Elige configuración para **Uso de trabajo o escuela** si vas a unir el equipo a un dominio (Active Directory) en el futuro, o configuración personal para pruebas generales.
* Instala **VirtualBox Guest Additions** (*Dispositivos > Insertar imagen de CD de las Guest Additions*) una vez iniciado el escritorio para habilitar la resolución automática de pantalla y el portapapeles compartido.
