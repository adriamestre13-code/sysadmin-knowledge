#  Creación de una Máquina Virtual con Ubuntu Desktop

Guía paso a paso para desplegar Ubuntu Desktop en Oracle VirtualBox y la explicación técnica de cada decisión.

---

##  ¿Por qué Ubuntu Desktop?

Ubuntu es la distribución de Linux más utilizada en entornos corporativos y de desarrollo. Dominar su versión Desktop es fundamental para IT Helpdesk y Sysadmin por varias razones:
* **Ecosistema estándar:** Es la base de muchas infraestructuras empresariales y la referencia principal para aprender la terminal Linux.
* **Gestión de paquetes (APT):** Permite practicar la instalación, actualización y administración de software mediante línea de comandos.
* **Integración con servidores:** Utiliza la misma base del sistema operativo que Ubuntu Server, lo que facilita el salto a la administración de servidores Linux.
* **Diagnóstico de redes:** Ideal para ejecutar herramientas de auditoría y análisis de red basadas en Linux.

---

##  Requisitos Previos

* **Oracle VirtualBox** instalado.
* [**ISO de Ubuntu Desktop**](https://ubuntu.com/download/desktop) (versión LTS descargable desde el sitio web oficial de Ubuntu).

---

##  Configuración Paso a Paso de la VM (y su explicación)

### 1. Nombre y Sistema Operativo
* **Tipo:** Linux
* **Versión:** Ubuntu (64-bit)
* Recuerda desmarcar la casilla de Instalación desatendida.
<img width="599" height="412" alt="Captura de pantalla 2026-09-03 100318" src="https://github.com/user-attachments/assets/142993e7-b920-4e52-b879-98f645d10d65" />


### 2. Memoria RAM y Procesadores (CPU)
* **RAM:** 2048 MB (2 GB) mínimo / 4096 MB (4 GB) recomendado.
* **CPUs:** 2 vCPUs recomendado.
* **EFI:** Con Ubuntu Desktop, no es necesario usar EFI puesto que puede funcionar perfectamente con MBR.
> **¿Por qué?** La interfaz gráfica de Ubuntu (GNOME) requiere al menos 2 GB de RAM para moverse con fluidez. Asignar 2 procesadores mejora notablemente la respuesta del sistema al compilar o actualizar software.
> <img width="599" height="409" alt="Captura de pantalla 2026-09-03 100435" src="https://github.com/user-attachments/assets/9469e12d-11ee-4fd0-85c5-82f34d62b247" />


### 3. Disco Duro Virtual
* **Tamaño:** 25 GB mínimo / 40 GB recomendado (Para este LAB se usarán 120GB).
* **Tipo de archivo:** VDI (VirtualBox Disk Image).
* **Reservar Completamente:** Deseleccionado.
> **¿Por qué?** A diferencia de Windows, Linux es más ligero en almacenamiento. La asignación dinámica evita ocupar espacio inútil en tu disco físico hasta que instales paquetes o guardes archivos.
> <img width="601" height="410" alt="Captura de pantalla 2026-09-03 101023" src="https://github.com/user-attachments/assets/2463d004-f869-4ab0-af5c-94f88889f411" />


### 4. Configuración de Red
* **Modo de red:** NAT (por defecto) o *Bridge*.
> **¿Por qué?** El modo NAT le otorga salida a Internet inmediata a la VM para descargar actualizaciones de paquetes durante y después de la instalación.
> 
> <img width="608" height="384" alt="Captura de pantalla 2026-09-03 101100" src="https://github.com/user-attachments/assets/80e03fb9-4723-41c1-b621-a954339e3147" />


---

##  Proceso de Instalación

1. Inicia la VM y selecciona el archivo ISO de Ubuntu Desktop.
2. En el menú de arranque del instalador (GRUB), selecciona **Try or Install Ubuntu**.
3. Elige el idioma y la distribución de teclado.
4. Selecciona **Instalación normal** (incluye navegador, utilidades y paquetes de oficina) y marca la casilla **Descargar actualizaciones al instalar Ubuntu**.
5. En tipo de instalación, selecciona **Borrar disco e instalar Ubuntu** (afecta solo al disco virtual de la VM).
6. Configura tu zona horaria, nombre de usuario y contraseña.

---

##  Configuración Inicial Post-Instalación
* Completa el asistente inicial de bienvenida en el escritorio.
* Instala las **VirtualBox Guest Additions** desde la terminal para habilitar pantalla completa y portapapeles compartido:
>
> <img width="638" height="461" alt="Captura de pantalla 2026-09-03 104031" src="https://github.com/user-attachments/assets/9c1c3a65-cfec-4f09-b09b-a0e8f16d194e" />
> <img width="638" height="464" alt="Captura de pantalla 2026-09-03 104055" src="https://github.com/user-attachments/assets/cbe86f71-7de6-434d-b3e1-a33f9a39ed20" />
> <img width="638" height="463" alt="Captura de pantalla 2026-09-03 105022" src="https://github.com/user-attachments/assets/6246ae29-4238-497f-a7f5-6859d78b53fa" />
> <img width="611" height="386" alt="Captura de pantalla 2026-09-03 112429" src="https://github.com/user-attachments/assets/12da77de-8989-4372-b503-02c35a21d2c4" />
> <img width="895" height="715" alt="Captura de pantalla 2026-09-03 112733" src="https://github.com/user-attachments/assets/a4b27e3f-b174-47b7-af34-560ee6a3a825" />

* Configuración y actualización de **UBUNTU**: Para ello debemos estar conectados a internet, por lo que nuestra red debe estar en NAT.
Comandos a introducir en la terminal:
>
>```bash
>apt-get update
>apt dist-upgrade
>reboot
>apt-get autoclean
>apt-get autoremove
>```

