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
<img width="911" height="718" alt="Captura de pantalla 2026-09-02 190631" src="https://github.com/user-attachments/assets/3fbdec91-ea96-40d4-a058-b5be22aa2ece" />

* **IMPORTANTE:** Desactivar la instalación desatendida, esto nos permitirá tener control total sobre la instalación del SO.

### 2. Memoria RAM y Procesadores (CPU)
* **RAM:** 4096 MB (4 GB) mínimo / 8192 MB (8 GB) recomendado.
* **CPUs:** 2 vCPUs mínimo.
> **¿Por qué?** Windows 11 exige un mínimo de 4 GB de RAM y 2 núcleos para funcionar. Darle menos provocará un rendimiento extremadamente lento o errores en el instalador.
>
> <img width="911" height="718" alt="Captura de pantalla 2026-09-02 190832" src="https://github.com/user-attachments/assets/848659d4-ba4e-4990-bd25-ee9bc20d54a4" />


### 3. TPM 2.0 y Secure Boot
* **Habilitar EFI:** Activado.
* **Virtual TPM:** TPM 2.0.
> **¿Por qué?** Son requisitos de hardware obligatorios impuestos por Microsoft para Windows 11. VirtualBox permite emular ambos componentes para evitar trucos en el registro durante la instalación.

### 4. Disco Duro Virtual
* **Tamaño:** 64 GB mínimo.
* **Tipo de archivo:** VDI (VirtualBox Disk Image).
* **Espacio asignado:** Desmarcar la opción de Reservar completamente.
> **¿Por qué?** El espacio asignado dinámicamente solo consume espacio real en tu disco físico a medida que la VM llena el espacio, optimizando el almacenamiento del Host.
>
> <img width="911" height="719" alt="Captura de pantalla 2026-09-02 191110" src="https://github.com/user-attachments/assets/6d7fdd41-eaf4-4eaa-99b6-bc3a99a2edd5" />


### 5. Configuración de Red
* **Modo de red:** NAT (para acceso a internet) o *Bridge* (para simular un equipo real en tu red local). La arquitectura de red será explicada más adelante.
> **¿Por qué?** NAT aísla la máquina virtual del resto de tus dispositivos domésticos mientras le da acceso a la red para actualizaciones.
>
> <img width="913" height="719" alt="Captura de pantalla 2026-09-02 191330" src="https://github.com/user-attachments/assets/9fcd6ab1-a812-4786-a5c8-19d6ed2b64cd" />


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
* Instala **VirtualBox Guest Additions** (*Dispositivos > Insertar imagen de CD de las Guest Additions (En mi MV no sale porque ya está instalado)*) una vez iniciado el escritorio para habilitar la resolución automática de pantalla y el portapapeles compartido.

<img width="1087" height="707" alt="Captura de pantalla 2026-09-02 191511" src="https://github.com/user-attachments/assets/d06efd8f-08b9-4fdb-b2c9-a1531d590538" />
<img width="1088" height="705" alt="Captura de pantalla 2026-09-02 191557" src="https://github.com/user-attachments/assets/41fd6964-7326-40b7-875e-87127615f85b" />

