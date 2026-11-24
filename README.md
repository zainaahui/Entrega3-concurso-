[readme.md](https://github.com/user-attachments/files/35348140/readme.md)
# 🏗️ El edificio que no se cae — Con Repara Felix

Simulación educativa e interactiva sobre ingeniería sísmica chilena, inspirada en las investigaciones de **Juan Carlos de la Llera** (*Concurso Chile Re-Descubre*). El jugador experimenta en tiempo real durante **1 minuto** cómo distintas tecnologías de protección sísmica mantienen en pie un edificio de 10 pisos y protegen a sus habitantes durante terremotos de distinta magnitud.

---

## 🎬 Video de demostración

### Opción 1: Reproductor de video directo (`.mp4` / GitHub)

<div align="center">


  <video src="assets/demo.mp4" controls width="100%" poster="assets/preview.png">
    Tu navegador no soporta la reproducción directa de video. Puedes verlo en <a href="assets/demo.mp4">assets/demo.mp4</a>.
  </video>
</div>


* 🔬 **Contexto científico real:** [Sistema de protección sísmica como modelo de I+D — Juan Carlos de la Llera](https://www.youtube.com/watch?v=-X_EoVsu1ow).

---

## ✨ Características principales

### 1. Guía interactivo: Felipe Repara Feliz

* **Assets vectoriales dinámicos (`SVG` de alta resolución):** Incluye 4 poses y expresiones que reaccionan en tiempo real a los eventos de la simulación:
  * `idle`: Posando feliz con su martillo dorado en alto.
  * `wow`: Asombrado al observar el funcionamiento de la aislación sísmica y los disipadores.
  * `repair`: Blandiendo su martillo dorado con destellos al reparar grietas estructurales.
  * `panic`: Sudando y sujetándose la gorra cuando el sismo supera la magnitud $6.0$ Richter.
* **Mecánica del Martillo Dorado:** Permite reparar grietas acumuladas y restaurar ventanas rotas en medio de la partida.

### 2. Física estructural de 10 pisos y 3 tipos de fundación

El simulador resuelve un modelo dinámico de edificio de corte de 10 niveles sometido a movimiento basal:

1. **Base rígida (`1 dedo` / Tecla `1`):** El edificio está anclado directamente al suelo; transmite toda la aceleración sísmica, generando grandes deformaciones y grietas.
2. **Aislación sísmica (`2 dedos` / Tecla `2`):** Incorpora una interfaz deslizante tipo péndulo en la base que desacopla el movimiento del suelo respecto a la estructura.
3. **Disipadores de energía (`3 dedos` / Tecla `3`):** Amortiguadores diagonales (como en la *Torre Titanium* en Santiago) que absorben energía cinética y reducen el balanceo.

### 3. Ventanas con residentes y rescate en terremotos fuertes

* El edificio cuenta con **30 ventanas** distribuidas en sus 10 pisos.
* Cuando la magnitud alcanza niveles fuertes ($M \ge 5.0$), las ventanas se iluminan en alerta y **aparecen vecinos pidiendo ayuda**.
* Si la deriva entre pisos es excesiva (especialmente con *Base rígida* en sismos sobre $M = 5.6$), los vidrios ceden y **los personajes caen del edificio** hasta rebotar a salvo en las **colchonetas inflables de rescate** ubicadas a los costados de la mesa vibratoria.

### 4. Audio procedural (Web Audio API)

Todos los efectos sonoros se sintetizan en tiempo real sin necesidad de archivos externos:

* **Retumbo sísmico y subgraves:** Escalan dinámicamente según la magnitud Richter y la fase de la onda.
* **Crujidos de concreto:** Proporcionales al daño estructural acumulado en cada piso.
* **Vidrios rotos, silbido de caída y rebote:** Se activan cada vez que un vecino cae hacia la colchoneta de rescate.
* **Martillo dorado y alertas sísmicas:** Efectos musicales al reparar o cambiar de sistema estructural.

---

## 🎮 Controles

### Opción A: Control por cámara web (MediaPipe Hands)

* **Mano derecha:** Ciérrala para mantener calma ($0.0$) y ábrela gradualmente para aumentar la intensidad del sismo hasta $8.8$ Richter.
* **Mano izquierda:**
  * `1 dedo` levantado: **Base rígida**
  * `2 dedos` levantados: **Aislación sísmica**
  * `3 dedos` levantados: **Disipadores**

### Opción B: Teclado y ratón (Sin cámara)

* **Deslizador inferior** o teclas `↑` / `↓`: Ajustar la magnitud del sismo.
* Teclas `1`, `2`, `3` o botones inferiores: Cambiar el tipo de base del edificio.
* Botón **`🔨 Reparar`** o tecla `R`: Usar el martillo dorado de Felipe Repara Feliz para reparar grietas.
* Botón **`Sonido`** o tecla `M`: Silenciar / activar el audio.

---

## 🚀 Instalación y ejecución

El proyecto está contenido íntegramente en un único archivo autónomo (`index.html`), sin dependencias locales adicionales:

1. Descarga o guarda el archivo `index.html`.
2. Para jugar **con cámara web**, ábrelo mediante un servidor local (`http://localhost`) o un entorno `HTTPS` (requisito de seguridad de los navegadores para acceder a `getUserMedia`). Por ejemplo:

   ```bash
   npx serve .
   ```

   o con Python:

   ```bash
   python3 -m http.server 8080
   ```

3. Para jugar **sin cámara**, puedes abrir `index.html` directamente con doble clic en cualquier navegador moderno (Chrome, Edge, Firefox, Safari).

---

## 🧠 Propósito educativo

Al finalizar la ronda de **1 minuto**, la pantalla de resultados compara el porcentaje máximo de deformación registrado en cada sistema estructural y muestra el porcentaje de reducción logrado gracias a la **aislación sísmica**, reforzando el valor de la ingeniería chilena en la protección de vidas e infraestructura crítica.
