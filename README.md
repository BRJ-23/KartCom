# KartCom (Work In Progress)
---

## 📝 El Problema
Actualmente, para usar intercomunicadores de diferentes marcas, dependemos de llevar el teléfono móvil encima y hacer una llamada a través de este.

## 💡 La Solución
KartCom se conecta por Bluetooth al intercomunicador simulando ser un teléfono móvil. Captura el audio y lo retransmite a través de una señal de corto alcance usando el chip **NRF24L01+**. 
El resultado: comunicación instantánea en la pista, privada y sin depender de ningún dispositivo.

## 🧩 Arquitectura de Hardware
El proyecto está diseñado para ser lo más compacto y económico posible.

* **Microcontrolador:** ESP32 (WROOM-32). Elegido por su soporte nativo de Bluetooth Classic.
* **Módulo de Radio:** NRF24L01+ (Versión PA/LNA con antena externa) para garantizar un alcance de +200 metros.
* **Alimentación:** Batería LiPo 3.7V (aprox. 800mAh) + Módulo de carga TP4056.

## 💻 Arquitectura de Software (ESP-IDF)
Debido a la necesidad de gestionar audio bidireccional en tiempo real, el proyecto abandona el IDE de Arduino para utilizar **ESP-IDF** y aprovechar los dos núcleos del procesador mediante **FreeRTOS**:

* **Core 0 (Modo Teléfono):** Mantiene la conexión Bluetooth Classic (Perfil HFP - Audio Gateway) con el casco, recibiendo y enviando el audio.
* **Core 1 (Modo Walkie-Talkie):** Lee los datos usando y los emite/recibe a través de la antena del NRF24L01+.
* **Memoria Compartida:** Se utilizan *Ring Buffers* para pasar el flujo de audio entre núcleos de forma segura y sin cortes.

## 🚀 Roadmap
Este proyecto está en fase de desarrollo activo. Aquí están los hitos a completar:

- [ ] Implementar el ejemplo base `hfp_ag` para conectar el ESP32 al intercomunicador.
- [ ] Conseguir extraer el flujo de audio (PCM) del micrófono del casco.
- [ ] Configurar la comunicación SPI con el módulo NRF24L01+.
- [ ] Integrar FreeRTOS y los Ring Buffers para comunicar ambos procesos.
- [ ] Pruebas de latencia y calidad de audio con dos dispositivos.
- [ ] Diseño y publicación de la carcasa en impresión 3D.

## 🛠️ Cómo contribuir
Si eres un entusiasta de este tipo de proyectos, ¡toda ayuda es bienvenida! Siéntete libre de abrir *Issues* con sugerencias o lanzar *Pull Requests*.

## 📄 Licencia
Este proyecto es de código abierto. Con licencia MIT.
