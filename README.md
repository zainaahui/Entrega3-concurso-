# El edificio que no se cae

**Experiencia interactiva educativa de 1 minuto** para el concurso *Chile Re-Descubre*, inspirada en el trabajo del ingeniero chileno **Juan Carlos de la Llera** en protección sísmica de edificios.

Los niños controlan con las manos una **mesa vibratoria de laboratorio** frente a la cámara web y descubren, probando, cómo la aislación sísmica y los disipadores de energía protegen un edificio durante un terremoto.

- **Archivo único:** `mesa-vibratoria-de-la-llera.html` (HTML + CSS + JavaScript, con las imágenes incrustadas).
- **Sin instalación ni build:** se abre en un navegador moderno con webcam.
- **Idioma:** español.

---

## Cómo se juega

El juego dura **60 segundos**. El **Tío Constructor**, personaje guía en la esquina inferior derecha, va explicando qué hacer.

| Mano | Gesto | Efecto |
|---|---|---|
| **Derecha** | Puño cerrado | Mesa en calma |
| **Derecha** | Mano abierta | Sismo fuerte (hasta M 8,8). Cuanto más abierta, mayor la magnitud |
| **Izquierda** | 1 dedo levantado | Base rígida |
| **Izquierda** | 2 dedos | Aislación sísmica (péndulo de fricción) |
| **Izquierda** | 3 dedos | Disipadores de energía (como la Torre Titanium) |

El cambio de base se confirma cuando el gesto se mantiene unos 0,35 s, para evitar cambios accidentales.

### Guion del minuto

| Tiempo | Qué ocurre |
|---|---|
| 0 s | El guía saluda |
| 6 s | Explica la mano derecha (intensidad) |
| 15 s | Base rígida: sacudir fuerte y ver las grietas |
| 28 s | Aislación sísmica |
| 40 s | Disipadores |
| 50 s | Desafío final: un sismo gigante, comparando las tres bases |
| 60 s | Pantalla de resultados con la deformación máxima de cada base |

El guía también **reacciona a lo que haces**: se asombra si la base rígida se agrieta o si la aislación casi no deja deformar el edificio.

### Sin cámara

Si no hay webcam o se niega el permiso, el juego sigue funcionando:

- Deslizador **«Sin cámara»** para la intensidad.
- Botones de base, o teclas **1 / 2 / 3**.
- Flechas **↑ / ↓** para subir o bajar la magnitud.
- Tecla **M** para silenciar.

---

## Qué muestra la pantalla

- **Título y reloj** con barra de progreso de 60 s.
- **Gráfico de intensidad** de los últimos 15 s, con la magnitud (Richter) en tiempo real y su nivel (calma, leve, moderado, fuerte, gigante).
- **Escena de laboratorio:** mesa vibratoria con el edificio de 10 pisos, cuya fachada usa una textura tomada de una foto de la torre. La deformación se ve piso a piso, con contorno punteado del edificio sin deformar, cambio de color y grietas según el daño.
- **Fundación visible:** bloque fijo, plato cóncavo con deslizador (péndulo de fricción) o amortiguadores diagonales en cada piso.
- **Miniatura de la cámara** con las manos detectadas (derecha en naranja, izquierda en turquesa).

## Sonido (Web Audio API)

Todo el audio se sintetiza en el navegador y responde a la magnitud que controlas:

- **Retumbo del suelo:** más fuerte y más agudo al subir la magnitud, pulsando al ritmo de la mesa.
- **Crujidos de concreto:** su frecuencia depende de la deformación y el daño de la base elegida (muchos con base rígida, pocos con aislación).
- **Alarma:** sirena de dos tonos desde aproximadamente M 5,2, que sube de tono con la magnitud.
- **Efectos:** jingle distinto por cada base, tono de inicio y fanfarria final.

El audio se activa al pulsar **«¡Empezar!»**, porque los navegadores exigen un gesto del usuario.

---

## La ciencia detrás (modelo didáctico)

Es una simulación **simplificada** pensada para enseñar, no para diseñar estructuras reales.

- **Edificio de corte de 10 pisos** (masas, resortes y amortiguadores). Altura de piso 3,2 m, primer periodo cercano a 1 s.
- **Tres edificios se simulan en paralelo** con el mismo sismo, así que al cambiar de base se ve cómo le va a cada uno.
- **Base rígida:** amortiguamiento de unos 5 %.
- **Aislación:** capa de base con periodo aproximado de 2,6 s y amortiguamiento viscoso equivalente de unos 15 %. Se modela el efecto de un péndulo de fricción de forma lineal.
- **Disipadores:** amortiguamiento aumentado en cada piso.
- **Daño:** cuando la deriva de entrepiso supera 0,4 %, el piso acumula daño, pierde rigidez y se ve agrietado. Si no hay sismo por unos segundos, la maqueta se repara sola.
- **Sismo:** la magnitud se convierte en aceleración máxima del suelo con una relación simplificada (`0,01 · 10^(0,28·(M−3))` g) y una frecuencia entre 0,8 y 1,05 Hz, con un segundo armónico para que no sea una sinusoide pura.
- **Exageración visual:** los desplazamientos se dibujan ×3.

---

## Tecnología

- **Canvas 2D** para toda la escena y el gráfico.
- **Google MediaPipe Hands** (cargado desde jsDelivr) para detectar hasta dos manos y distinguir derecha de izquierda. La imagen de la cámara se espeja antes de analizarla.
- **Web Audio API** para el sonido sintético.
- **JavaScript sin frameworks.** La integración numérica usa subpasos de 1/600 s.

## Requisitos

- Navegador moderno (Chrome o Edge recomendados) con webcam.
- **Conexión a internet** para cargar MediaPipe y la tipografía.
- Contexto seguro para la cámara: `https://` o `localhost`.

## Cómo ejecutarlo

Abrir el archivo directamente con doble clic puede bloquear la cámara. Lo más seguro es servirlo en local:

```bash
python3 -m http.server 8000
# luego abrir http://localhost:8000/mesa-vibratoria-de-la-llera.html
```

También puede subirse a cualquier hosting estático con HTTPS.

## Consejos para la exhibición

- Buena iluminación frontal; evitar contraluz.
- Las manos deben verse **de frente** a la cámara, sin tapar la mano izquierda con la derecha.
- Probar el volumen del equipo y los parlantes antes del evento.
- Si el espacio es ruidoso, la tecla **M** y el deslizador de volumen del sistema ayudan a ajustar.

---

## Personalización

Las constantes principales están al inicio del bloque de física del script:

| Constante | Significado |
|---|---|
| `N` | Número de pisos |
| `HS` | Altura de piso (m) |
| `KM` | Rigidez por masa de cada piso |
| `KB`, `CB` | Rigidez y amortiguamiento del aislador |
| `BETA` | Amortiguamiento de cada tipo de base |
| `SCRIPT` | Textos y tiempos del guía |
| `COL` | Colores de cada base |

## Estructura del archivo

1. Estilos (tema diurno y colorido).
2. Escena, gráfico y pantallas de inicio y fin.
3. Audio.
4. Modelo físico y movimiento del suelo.
5. Estado del juego y guía.
6. Cámara y reconocimiento de manos.
7. Simulación y dibujo.

---

## Limitaciones conocidas

- Modelo simplificado de comportamiento lineal con daño aproximado; la escala de Richter se usa de forma didáctica.
- El conteo de dedos es en 2D y puede fallar con poca luz o si la mano está de lado.
- La torre usada para la textura de fachada corresponde a la Torre Titanium, según la foto aportada.
- Las alarmas y los crujidos son sintéticos, no grabaciones reales.

## Créditos y derechos

- **Tema científico:** trabajo en protección sísmica de **Juan Carlos de la Llera** (Pontificia Universidad Católica de Chile y CIGIDEN). Este juego es un homenaje educativo y no está afiliado a él ni a sus instituciones.
- **Textura de fachada:** recortada de la foto de la torre proporcionada para el proyecto.
- **Personaje guía «Tío Constructor»:** imagen aportada por el equipo. **Antes de presentar el proyecto, confirma que tienes derechos o licencia para usarla**, ya que se parece mucho a un personaje comercial existente. Si el concurso exige material original, reemplázala por un diseño propio: basta cambiar el asset del guía.
- **MediaPipe Hands:** Google, licencia Apache 2.0.
