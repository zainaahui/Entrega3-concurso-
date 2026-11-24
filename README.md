[readme_del_proyecto.md](https://github.com/user-attachments/files/35333014/readme_del_proyecto.md)
# El edificio que no se cae

Simulación interactiva en tiempo real de una mesa vibratoria para explorar cómo la ingeniería sísmica chilena protege las estructuras frente a terremotos mediante distintos sistemas de fundación y disipación de energía.

---

## Tema elegido

**Ingeniería sísmica y protección estructural en Chile**, inspirado en el trabajo y las investigaciones del ingeniero estructural chileno **Juan Carlos de la Llera** en el desarrollo de sistemas de aislación sísmica y disipadores de energía aplicados a edificios e infraestructura crítica (como hospitales y torres de gran altura, por ejemplo, la Torre Titanium).

---

## Descripción conceptual

Chile es uno de los países más sísmicos del mundo, lo que ha impulsado soluciones de vanguardia para evitar el colapso y reducir los daños estructurales durante terremotos de gran magnitud.

Esta aplicación modela un **edificio de corte de 10 pisos** montado sobre una mesa vibratoria virtual, permitiendo experimentar y comparar en una sesión de **1 minuto** tres estrategias constructivas:

1. **Base rígida:** El edificio está empotrado directamente al suelo. Transmite íntegramente el movimiento sísmico a la estructura, generando altas deformaciones entre pisos y acumulación de daño (grietas) cuando la magnitud es elevada.
2. **Aislación sísmica:** La estructura descansa sobre apoyos deslizantes que funcionan como un péndulo invertido. El suelo se desplaza bajo el edificio mientras la superestructura permanece casi inmóvil, reduciendo drásticamente las deformaciones internas.
3. **Disipadores de energía:** Incorpora amortiguadores diagonales entre pisos que absorben la energía cinética del balanceo y la transforman en calor, frenando rápidamente las oscilaciones.

La experiencia está acompañada por un guía virtual (**el Tío Constructor**), un sismógrafo en vivo en escala Richter, retroalimentación visual de grietas y un motor de audio generativo que adapta el retumbo, los crujidos estructurales y las alarmas según la intensidad del sismo.

---

## Instrucciones de uso e interacción

### Requisitos previos
* Un navegador web moderno (Chrome, Edge, Firefox o Safari).
* Cámara web (opcional, recomendada para la experiencia gestual).
* Debido a las políticas de seguridad de los navegadores para el acceso a la cámara (`getUserMedia`), se recomienda abrir el archivo `index.html` a través de un servidor local (por ejemplo, *Live Server* en VS Code o `python -m http.server`) o mediante `https://`.

### Controles mediante cámara (MediaPipe Hands)
Al presionar **¡Empezar!** y conceder permiso a la cámara, podrás controlar la simulación usando ambas manos frente a la pantalla:

* **Mano derecha — Intensidad del sismo:**
  * **Mano cerrada (puño):** Calma sísmica (magnitud $0.0$).
  * **Mano abierta:** Aumenta progresivamente la magnitud del terremoto hasta niveles gigantes (similares al sismo del Maule 2010, ~8.8).
* **Mano izquierda — Tipo de protección estructural:**
  * **1 dedo levantado:** Base rígida.
  * **2 dedos levantados:** Aislación sísmica.
  * **3 dedos levantados:** Disipadores de energía.

*(Nota: Mantén la seña de la mano izquierda durante unos instantes para confirmar el cambio de sistema estructural).*

### Controles alternativos (sin cámara)
Si no dispones de cámara o prefieres usar teclado y ratón:
* **Botones inferiores:** Haz clic directamente sobre *Base rígida*, *Aislación sísmica* o *Disipadores* (o usa las teclas `1`, `2` y `3`).
* **Deslizador (*Sin cámara*):** Arrastra el control deslizante para ajustar la magnitud del sismo (o usa las flechas `↑` y `↓` del teclado).
* **Sonido:** Activa o desactiva el audio con el botón **Sonido** o presionando la tecla `M`.

---

## Tecnologías empleadas

* **MediaPipe (`@mediapipe/hands`):** Biblioteca de visión por computador ejecutada directamente en el navegador para la detección y seguimiento en tiempo real de 21 puntos clave (*landmarks*) por mano, permitiendo distinguir lateralidad (izquierda/derecha), grado de apertura de la palma y conteo de dedos sin necesidad de servidores externos.
* **HTML5 Canvas 2D:** Renderizado en tiempo real de la mesa vibratoria, la deformación por piso del edificio de 10 niveles, los aisladores pendulares, los disipadores diagonales, las grietas dinámicas, el paisaje y el gráfico del sismógrafo.
* **Motor de física en JavaScript:** Integración numérica de subpasos ($\Delta t = 1/600\text{ s}$) para resolver ecuaciones de movimiento de un sistema de múltiples grados de libertad con rigidez degradable por daño estructural.
* **Web Audio API:** Síntesis procedural de sonido en tiempo real (ruido browniano filtrado para el retumbo sísmico, osciladores subgraves, crujidos de concreto proporcionales a la deformación y alarma sísmica).
* **CSS3 & HTML5 Semántico:** Interfaz responsiva con soporte para pantallas táctiles, manejo de preferencias de movimiento reducido (`prefers-reduced-motion`) y etiquetas de accesibilidad ARIA.
