# Laboratorio 1: Introducción al Análisis de Tráfico de Red con Wireshark

## 📋 Descripción del Proyecto
Este laboratorio documenta un ejercicio práctico de análisis de tráfico de red utilizando **Wireshark** en un entorno controlado sobre **Kali Linux** virtualizado en **VirtualBox**. El objetivo principal es identificar componentes clave de una captura de red, aplicar filtros de visualización y diferenciar entre tráfico cifrado y en texto plano.

## 🛠️ Entorno Técnico y Herramientas
* **Sistema Operativo:** Kali Linux (x86_64)
* **Plataforma de Virtualización:** Oracle VirtualBox (Red NAT, IP asignada: `10.0.2.15`)
* **Herramienta de Análisis:** Wireshark (v4.6.6)
* **Interfaz Capturada:** `eth0`

---

## 🔬 Fases del Laboratorio y Hallazgos

### 1. Configuración de la Interfaz y Captura Inicial
* Se configuró la interfaz de red virtual `eth0` para iniciar la captura de paquetes en tiempo real.
* Se recopilaron más de 20,000 paquetes de tráfico de red mixto (principalmente protocolos orientados a conexión como TCP y QUIC).

### 2. Filtrado de Tráfico DNS (Domain Name System)
* **Filtro aplicado:** `dns`
* **Evidencia observada:** Se aislaron las consultas y respuestas de resolución de nombres de dominio realizadas por los servicios del sistema y el navegador hacia el servidor DNS local (`192.168.80.1`).
* **Relevancia:** Permite auditar qué dominios externos intenta consultar o resolver una máquina dentro de la red.

### 3. Identificación de Tráfico Web en Texto Plano (HTTP)
* **Filtro aplicado:** `http`
* **Evidencia observada:** Se capturó exitosamente una petición y respuesta HTTP no cifrada (`GET /success.txt?ipv4`), detallando las capas del modelo OSI, puertos de origen/destino y la estructura del payload en texto plano.
* **Relevancia:** Demuestra los riesgos de seguridad asociados al uso de protocolos no cifrados, donde la información puede ser leída o interceptada fácilmente en tránsito.

---

## 🚀 Cómo Reproducir este Laboratorio
1. Levantar la máquina virtual de Kali Linux en VirtualBox utilizando el adaptador en modo NAT.
2. Iniciar Wireshark con privilegios de superusuario (`sudo wireshark`).
3. Seleccionar la interfaz `eth0` y hacer clic en el botón de iniciar captura.
4. Generar tráfico de red controlado y aplicar los filtros de visualización `dns` u `http` según corresponda.
