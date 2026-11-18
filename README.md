# Comedero Inteligente para Gatos

Proyecto del curso **EL-1200 Introducción a la Electrónica**, Instituto Tecnológico de Costa Rica (TEC), II semestre 2026.

**Docente:** Ing. William Marín Moreno  
**Integrante:** Mathias Fernandez Valverde

## Descripción
Este proyecto consiste en un comedero automático para gatos controlado por un ESP32. El sistema detecta la presencia del gato mediante un sensor PIR y activa un servomotor para abrir temporalmente la compuerta que dispensa el alimento. Un LED indica cuándo se está sirviendo la comida.

El sistema utiliza una variable booleana (`dispensado`) para evitar servir alimento repetidamente mientras el gato permanece frente al comedero.

## Funcionamiento
1. El ESP32 inicia con la compuerta cerrada y el LED apagado.
2. El sensor PIR detecta movimiento y envía una señal HIGH al GPIO 2.
3. Si todavía no se ha dispensado alimento, el servomotor gira a 140° y el LED se enciende.
4. Después de 1,5 segundos, el servomotor vuelve a 40° y el LED se apaga.
5. La variable `dispensado` cambia a `true`, evitando una segunda dispensación mientras el sensor continúe detectando al gato.
6. Cuando el sensor deja de detectar movimiento, la variable vuelve a `false` y el sistema queda listo para una nueva detección.

## Conexiones

| Componente | Pin o terminal | Conexión al ESP32 |
|---|---|---|
| Sensor PIR HC-SR501 | OUT / S | GPIO 2 |
| Servomotor | Señal / PWM | GPIO 13 |
| LED | Ánodo, mediante resistencia de 220 Ω | GPIO 5 |
| Sensor PIR | VCC | 3V3 |
| Servomotor | V+ | 3V3 en esta simulación |
| Todos los módulos | GND | GND |

**Importante:** en un montaje físico, verifique los requisitos de alimentación del servomotor. Si requiere una fuente externa, use una fuente adecuada y conecte su GND al GND del ESP32. No fuerce la alimentación del servo desde el pin 3V3 si supera su capacidad.

El diagrama editable de Wokwi se encuentra en `firmware/diagram.json`. La explicación de las conexiones está en `docs/conexiones.md`.

## Simulación
**Proyecto en Wokwi:** PENDIENTE: pegar aquí el enlace público de la simulación.

## Código
El programa se encuentra en `firmware/sketch.ino`.  
Biblioteca utilizada: **ESP32Servo** (debe instalarse o declararse en `firmware/libraries.txt`).

## Evidencia
Agregar en esta sección capturas o fotografías del circuito y del funcionamiento. Los archivos deben guardarse en la carpeta `media/`.

- `media/diagrama-cableado.png`: captura del circuito completo.
- `media/monitor-serial.png`: captura de los mensajes de dispensación y reinicio.
- `media/video-demostracion.mp4` o un enlace al video público: demostración del proyecto.

## Lista de materiales (BOM)
La lista de materiales está en `bom/lista-materiales.md`.

## Mejoras futuras
- Incorporar un horario programado para alimentar a la mascota.
- Agregar un sensor para medir el nivel de alimento disponible.
- Enviar una notificación por Wi-Fi cuando se dispense comida o el depósito esté vacío.

## Estructura del repositorio

```text
comedero-inteligente-EL1200/
├── README.md
├── firmware/
│   ├── sketch.ino
│   ├── diagram.json
│   └── libraries.txt
├── docs/
│   └── conexiones.md
├── media/
│   └── README.md
└── bom/
    └── lista-materiales.md
```
