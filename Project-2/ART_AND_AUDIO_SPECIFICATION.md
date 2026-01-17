# ART & AUDIO SPECIFICATION - PHOBIA
## Dirección de Arte, Diseño Visual y Sonoro

---

## **I. DIRECCIÓN DE ARTE**

### **A. Concepto Visual General**

**Estilo:** Realismo fotográfico desquiciado + Distorsión perceptual progresiva

**Influencias Visuales:**
- *P.T.* (Kojima Productions) - Horror ambiental, repetición inquietante
- *Hellblade* (Ninja Theory) - Distorsión de realidad, perspectivas fracturadas
- *Layers of Fear* (Bloober Team) - Transformación ambiental, opresión visual
- *The Lighthouse* (Robert Eggers) - Iluminación dramática, colores desaturados

**Filosofía de Diseño:**
El mundo visual debe ser inicialmente mundano y reconocible, pero progresivamente debe volverse hostil y distorsionado, reflejando el deterioro mental del protagonista. Las anomalías no son grotescas, sino sutilmente wrongnes—cosas que están "incorrectas" de maneras que el jugador no puede articular.

---

## **B. Paleta de Colores por Acto**

### **ACTO I: "Normalidad Rota"** (Sanity: 80-60)
- **Colores Base:** Grises, azules-grises, verdes oliva desaturados
- **Saturación:** 50-60%
- **Contraste:** Bajo a medio
- **Temperatura:** Neutra (5500K)
- **Feeling:** Depresión suave, estabilidad opresiva

**Palette Hex:**
```
Gris Neutro:      #8B8680
Azul Frío:        #4A5F7F
Verde Apagado:    #6B7D5C
Sombra Principal: #3C3C3C
Luz Ambiente:     #D4D4D4
Punto Focal:      #C9A96E (madera/calidez)
```

**Référence Visual:** Un día nublado en un apartamento urbano, luz natural filtrada por cortinas.

---

### **ACTO II: "Fragmentación"** (Sanity: 60-40)
- **Colores Base:** Rojos desaturados, morados oscuros, negros
- **Saturación:** 30-45%
- **Contraste:** Medio a alto
- **Temperatura:** Cálida (rojos) y fría (azules) en conflicto
- **Feeling:** Paranoia, disociación, peligro inminente

**Palette Hex:**
```
Rojo Decadente:   #7A3D3D
Púrpura Sombra:   #42364D
Negro Opresivo:   #1A1A1A
Azul Frío Oscuro: #2C3E50
Acento Rojo:      #B54B4B
Luz Intermitente: #FFD700 (en pestañeos)
```

**Référence Visual:** Hora del crepúsculo, sombras alargadas, luz artificial parpadeante.

---

### **ACTO III: "Colapso"** (Sanity: 40-0)
- **Colores Base:** Rojo saturadobaja, blanco inverso, negro absoluto
- **Saturación:** 10-20% (B/N) pero 150%+ en rojo de acentos
- **Contraste:** Extremadamente alto, casi incierto
- **Temperatura:** Alternancia caótica (muy fría → muy cálida)
- **Feeling:** Locura, horror absoluto, realidad fracturada

**Palette Hex:**
```
Rojo Sangre:      #8B0000
Negro Puro:       #000000
Blanco Inverso:   #FFFFFF (pero distorsionado)
Púrpura Irreal:   #9D4EDD
Amarillo Tóxico:  #FFBE0B
Acento Plata:     #E0E0E0
```

**Postprocesado:** Inverted color channels, chromatic aberration, flickering gamma.

---

### **FIN BUENO: "Despertar"** 
- **Colores Base:** Azul suave, blanco limpio, verdes vivos
- **Saturación:** 70-80%
- **Contraste:** Suave
- **Temperatura:** Neutra a cálida (hospital, luz natural)
- **Feeling:** Purificación, esperanza, vida

**Palette Hex:**
```
Azul Esperanzador: #3B82F6
Blanco Puro:       #F5F5F5
Verde Vida:        #22C55E
Crema Suave:       #FFF9E6
Acento Dorado:     #F59E0B
Sombra Suave:      #E5E7EB
```

---

### **FIN MALO: "Loop Infinito"**
- **Colores Base:** Rojo sangre, negro total, ocasionalmente blanco inverso
- **Saturación:** Máxima (rojo) o nula (B/N)
- **Contraste:** Doloroso (máximo)
- **Temperatura:** Extremo cálido (rojo)
- **Feeling:** Infierno, desesperación infinita, locura permanente

**Palette Hex:**
```
Rojo Infernal:    #C41E3A
Negro Vacío:      #0A0E27
Blanco Inverso:   #FFFFFF (glitchea)
Rojo Alterno:     #FF0000
Gris Muerte:      #4A4A4A
Púrpura Espíritu: #6A0572
```

---

## **C. Estilos Visuales de Elementos**

### **1. El Apartamento (Ambiente Principal)**

**Estilo General:** Lowpoly realista (stylized realism)

**Características:**
- Geometría moderada (~50K polígonos máximo)
- Texturas 2K (difusión, normal, roughness)
- Iluminación baked + real-time dinámico
- Materiales PBR (Physically Based Rendering)

**Zonas Específicas:**

#### **Dormitorio**
- Cama de madera simple, con sábanas desordenadas
- Escritorio con laptop y papeles esparcidos
- Espejo de cuerpo completo (anomalía: reflejo desfasado)
- Foto en marco (anomalía: invertida)
- Ventana con cortinas cerradas (luz filtra levemente)
- Piso: Madera desgastada
- Mood: Refugio personal, pero opresivo

#### **Baño**
- Espejo (anomalía principal: sin reflejo sincronizado)
- Inodoro, lavabo, bañera simples
- Toallero con toalla sucia
- Botiquin con medicamentos
- Piso: Baldosa gris
- Anomalía visual: Agua fluye hacia arriba en ocasiones
- Mood: Sanitario, clínico, desagradable

#### **Sala de Estar**
- Sofá gris desmantelado (lugar de escape)
- Televisor antiguo (muestra glitches)
- Mesa de centro con restos de comida
- Ventana grande (peligro; exterior oscuro)
- Estanterías con libros
- Piso: Moqueta gastada
- Mood: Espacio de confinamiento, centro de encuentros

#### **Cocina**
- Refrigerador simple (sonidos extraños)
- Estufa y fregadero (anomalía: agua ascendente)
- Licuadora suspendida en el techo (anomalía visual)
- Despensa con comida podrida
- Piso: Baldosa adhesiva
- Mood: Decadencia, abandono

#### **Pasillo**
- Puerta principal (no abre)
- Retratos de personas (se retuercen progresivamente)
- Bombillas que parpadean
- Alfombra desgastada
- Mood: Transición ansiosa, punto de no retorno

#### **Terraza** (Solo Final Malo)
- Barandal de acero
- Vista de la ciudad/acera
- Propio cuerpo caído abajo
- Viento intenso (efecto de audio)
- Cielo rojo/distorsionado
- Mood: Horror absoluto, muerte inevitable

---

### **2. La Entidad (Nemigo Principal)**

**Forma Base:** Humanoidea, andrajo sa, sin rasgos claros

**Características Visuales:**
- Cuerpo translúcido/fantasmal
- Movimientos jerky (no fluidos)
- Colores: Tonos grises, azules, ocasionalmente rojo
- No tiene cara definida (ojos negros vacíos)
- Aura de neblina alrededor

**Transformaciones según Fobia del Jugador:**

#### **Si Aracnofobia > 75%: Araña Gigante**
- Tamaño: 3-4 metros de envergadura
- 8 patas largas, crujientes (SFX de quebrarse)
- Cuerpo humanoidea en el centro
- Ojos múltiples (8-10) brillando rojo
- Textura: Quitina negra, velludo
- Animación: Movimiento de insecto (rápido, jerky)
- Sonido: Crujidos, chirridos

#### **Si Fobia Social > 70%: Multitud de Espectros**
- Múltiples figuras translúcidas (10-20+)
- Rostros humanos pero borrosos
- Voces superpuestas (coros ansiosos)
- Movimiento: Abarcan al jugador, lo cierran
- Colores: Grises fríos con toque púrpura
- Efecto: Agobio visual, claustrofobia

#### **Si Aquafobia > 60%: Entidad Acuática**
- Forma fluida, no definida
- Agua fluyendo constantemente
- Extremidades como tentáculos
- Superficie reflectante, espejo ondulante
- Colores: Azules profundos, turquesas
- Sonido: Agua gorgoteando, presión submarina

#### **Si Fobia a Rostros > 65%: Cara Infinita**
- Rostro humano distorsionado, grande
- Características faciales se tuercen constantemente
- Ojos que siguen al jugador
- Boca abierta emitiendo sonidos no-humanos
- Colores: Piel grisácea, labios rojo sangre
- Efecto: Incomodidad psicológica, uncanny valley

#### **Default: Espíritu Genérico**
- Forma semi-sólida, etérea
- Colores: Grises, azules, blanco fantasmal
- Movimiento: Flotante, fluido pero erratic
- Sonido: Respiración, susurros

---

### **3. Pistas de Realidad (Reality Anchors)**

Cada pista tiene un modelo 3D, una animación, y un efecto visual distintivo.

#### **Pista 1: Fotografía Invertida**
- Modelo: Marco simple de madera (~500 polígonos)
- Textura: Foto invertida de persona joven
- Animación: Giro lento (360° cada 8 segundos)
- Efecto: Brillo sutil, partículas de polvo
- Sonido: Crujido al acercarse
- Interacción: Click → "Esta foto... ¿cuándo fue?"

#### **Pista 2: Espejo sin Reflejo Sincronizado**
- Modelo: Espejo de pared estándar
- Reflejo programado: 2 segundos de lag
- Efecto: Pantalla distorsiona
- Sonido: Especie de "pulso" (heart beat)
- Interacción: Observar movimiento desincronizado
- Desencadenante: Horror psicológico

#### **Pista 3: Licuadora Flotante**
- Modelo: Licuadora simple (Blen der asset)
- Posición: Suspendida en el techo de la cocina
- Animación: Lentamente rota (360° cada 10 seg)
- Efecto: Sombra incorrecta (como si estuviera en suelo)
- Sonido: Zumbido eléctrico suave
- Interacción: "Eso... no debería estar ahí arriba"

#### **Pista 4: Agua Ascendente**
- Modelo: Fregadero con grifo abierto
- Partícula Sistema: Agua fluye hacia ARRIBA
- Efecto: Inversión de gravedad visual
- Sonido: Agua fluyendo, pero pitch elevado
- Interacción: Acercarse al fregadero
- Desencadenante: Puzzle de realidad

#### **Pista 5: TV Reproduciendo Loop**
- Modelo: TV antiguo (CRT style)
- Contenido de Pantalla: Misma escena en repeat (jugador viendo anomalías)
- Efecto: Parpadeo de pantalla
- Sonido: Hum de TV, diálogos fragmentados
- Interacción: Mirar la pantalla, reconocer la recursión
- Meta: "¿Estoy viendo mi propio juego?"

---

## **D. Interfaz de Usuario (UI)**

### **Estilo Visual del UI**

**Concepto:** Minimalista, clínico, con elementos de distorsión progresiva

**Fuente Primaria:** Monoespaciada (tipo terminal/código)
- Nombre: Courier New, Inconsolata o JetBrains Mono
- Razón: Sugiere interfaz clínica, "sistema", frialdad

**Colores de UI:**
- **Acto I:** Blanco/gris sobre fondo oscuro (limpio)
- **Acto II:** Blanco con tinte rojo (inquietud)
- **Acto III:** Rojo/blanco invertido (caos)

### **Elementos de UI**

#### **Barra de Sanidad (Sanity Bar)**
- **Posición:** Esquina superior derecha
- **Tamaño:** 200px ancho × 20px alto
- **Estilo:** Barra de progreso lineal
- **Color progresivo:**
  - Verde (80-100): Normal
  - Amarillo (60-80): Inquietud
  - Naranja (40-60): Peligro
  - Rojo (20-40): Crisis
  - Negro/Blanco invertido (0-20): Locura
- **Animación:** Parpadea cuando cae bajo 30
- **Con postprocesado:** Distorsión de pantalla aumenta proporcionalmente

#### **Contador de Pistas (Anchors Counter)**
- **Posición:** Esquina superior izquierda
- **Formato:** `[Pistas: 3/5]`
- **Color:** Blanco
- **Animación:** Brillo al encontrar pista
- **Sonido:** Campana suave (feedback positivo)

#### **Indicador de Amenaza**
- **Posición:** Centro inferior de pantalla
- **Forma:** Pulso circular que crece
- **Color:** Rojo intermitente cuando enemigo cercano
- **Sonido:** Latido cardíaco acelerado (binaural)

#### **Menú Principal**
- **Título:** "PHOBIA" en fuente Glitch/distorsionada
- **Opciones:**
  - New Game
  - Load Game
  - Settings
  - Credits
  - Exit
- **Animación:** Título flota/levanta lentamente
- **Fondo:** Imagen estática del apartamento (Acto I)
- **Música:** Tema minimalista oscuro

#### **Pantalla de Tests**
- **Fondo:** Blanco clínico
- **Texto:** Negro, Monoespaciado
- **Preguntas:** Centradas, tamaño legible (16pt)
- **Opciones de Respuesta:** Botones simples (A, B, C, D)
- **Progresión:** Barra de progreso del test
- **Transición:** Fade suave entre preguntas

#### **Cinemática / Diálogos**
- **Posición:** Lower third (parte inferior de pantalla)
- **Fondo:** Barra negra semi-transparente
- **Nombre del Hablante:** Azul (#3B82F6)
- **Diálogo:** Blanco
- **Tamaño:** Subtítulos en 14-16pt
- **Velocidad:** Texto aparece letra por letra (typewriter effect)

---

## **E. Mockups de Interfaz**

### **HUD Gameplay (Acto I)**
```
┌─────────────────────────────────────────────────────┐
│ [Pistas: 2/5]     PHOBIA                  ████░░░░░ │
│                                                     │
│                                                     │
│  (Apartamento 3D renderizado)                       │
│                                                     │
│                                                     │
│                                                     │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### **HUD Gameplay (Acto III)**
```
┌─────────────────────────────────────────────────────┐
│ [Pistas: 5/5]     PHOBIA              ░░░░░░░░░░░░ │
│                                                     │
│  ╔═══════════════════════════════════╗             │
│  ║ (Distorsión cromática)            ║             │
│  ║ (Invertido ocasionalmente)        ║             │
│  ║ (Ruido visual)                    ║             │
│  ╚═══════════════════════════════════╝             │
│                                                     │
│                    ⚠️ THREAT NEARBY                │
│                    ◉ (Pulso rojo)                  │
└─────────────────────────────────────────────────────┘
```

### **Pantalla de Test**
```
┌─────────────────────────────────────────────────────┐
│                                                     │
│              PSYCHOLOGICAL ASSESSMENT               │
│                                                     │
│                                                     │
│  Pregunta 3 de 5:                                   │
│  ¿Cuán frecuentemente te sientes deprimido?         │
│                                                     │
│  [ A ] Nunca o casi nunca                          │
│  [ B ] Algunos días                                │
│  [ C ] Más de la mitad de los días                 │
│  [ D ] Casi todos los días                         │
│                                                     │
│                                                     │
│  ========== ░░░░░░░░░░░░░░░░ 60%                   │
│                                                     │
└─────────────────────────────────────────────────────┘
```

---

## **II. ESPECIFICACIÓN DE AUDIO**

### **A. Dirección Sonora General**

**Concepto:** Psicoacústico, inquietante, immersivo

**Influencias:**
- *Silent Hill 2* (Akira Yamaoka) - Ambient horror, drones
- *Amnesia: The Dark Descent* (Mikko Tikkanen) - Tensión mediante ausencia
- *The Lighthouse* (Mark Korven) - Sonido organico, experimentación
- *Midsommar* (Peder Kurevik) - Horror en luz día, disonancia

**Filosofía:**
- El sonido **comunica estado mental** más que la música
- **Silencio** es tan importante como el ruido
- Uso de **spatial audio** (3D) para inmersión
- **Frecuencias bajas** para inquietud subconsciente (subsónico cuando sea seguro)

---

### **B. Paleta Musical por Acto**

#### **ACTO I: Normalidad Rota**
**BPM:** 80-90 (lento, deprimente)  
**Instrumentación:** Piano discordante, sintetizadores ambientales, drones bajos  
**Carácter:** Melancólico, ligeramente inquietante  
**Tempo:** Constante, ritmo débil  

**Tracks Recomendados:**
1. **"Opening Theme"** (2 min) - Introducción suave
2. **"Apartment Ambient"** (Loop, 4 min) - Música de fondo exploración
3. **"First Encounter"** (1:30) - Aparición de entidad
4. **"Sanctuary"** (3 min, loop) - Música en dormitorio seguro
5. **"Therapy Call"** (2 min) - Conversación con doctor

**Compositores Referencia:**
- Trent Reznor (The Social Network soundtrack)
- Disasterpeace (It Follows)
- Jon Hopkins (Electronic ambient)

---

#### **ACTO II: Fragmentación**
**BPM:** 100-120 (ansiedad creciente)  
**Instrumentación:** Strings tensas, sintetizadores dañados, percusión minimalista  
**Carácter:** Paranoico, tensión creciente  
**Tempo:** Incrementa ligeramente, ritmo presente  

**Tracks:**
1. **"Paranoia Rising"** (2:30) - Escalada de tensión
2. **"Enemy Approach"** (1:45) - Acercamiento del enemigo
3. **"Chase Theme"** (2 min, loop) - Persecución
4. **"Desperation"** (2 min) - Búsqueda de refugio
5. **"Test Chamber"** (3 min) - Ambiente de test psicológico

**Compositores Referencia:**
- Akira Yamaoka (Silent Hill)
- Jóhann Jóhannsson (Sicario)
- Ben Frost (Electronic/Experimental)

---

#### **ACTO III: Colapso**
**BPM:** 140+ (frenético)  
**Instrumentación:** Strings distorsionados, percusión caótica, ruido blanco, drones estridentes  
**Carácter:** Horror puro, locura, realidad fracturada  
**Tempo:** Acelerado, ritmo desincronizado a veces  

**Tracks:**
1. **"Reality Breaks"** (2:30) - Colapso de realidad
2. **"Relentless Pursuit"** (2 min, loop) - Persecución imparable
3. **"Mind Shatters"** (3 min) - Punto de quiebre psicológico
4. **"Final Confrontation"** (3:30) - Enfrentamiento final

**Compositores Referencia:**
- John Carpenter (Synth horror)
- Lustmord (Dark ambient)
- Throbbing Gristle (Industrial horror)

---

#### **FIN BUENO: "Despertar"**
**BPM:** 70-80 (calmante)  
**Instrumentación:** Strings suaves, piano esperanzador, sintetizadores pacíficos  
**Carácter:** Catártico, esperanzador, bittersweet  
**Tempo:** Lento, ritmo suave  

**Track:**
- **"Awakening"** (4 min) - Despertar en hospital, recuperación

**Referencia:** Ólafur Arnalds, Nils Frahm (Piano minimalista)

---

#### **FIN MALO: "Loop Infinito"**
**BPM:** Variable (caótico)  
**Instrumentación:** Ruido blanco, drones desesperados, gritos procesados, silencio inquietante  
**Carácter:** Infierno, desesperación infinita, locura fija  
**Tempo:** Irregular, anticíclico  

**Track:**
- **"Infinite Loop"** (6 min) - Bucle de muerte/maldición

**Referencia:** MERZBOW (Noise), Oneohtrix Point Never

---

### **C. Efectos de Sonido (SFX) - Catálogo Completo**

#### **Categoría: Ambiente del Apartamento**

| SFX | Descripción | Duración | Formato |
|-----|-------------|----------|---------|
| Windexficatories in distance | Viento lejano por ventana | 8s | WAV Loop |
| Clock ticking | Reloj del dormitorio | 2s | WAV Loop |
| Fridge hum | Zumbido del refrigerador | 4s | WAV Loop |
| Lightbulb flicker | Bombilla parpadeando | 0.8s | WAV |
| Water drip | Gota de agua (grifería) | 1.2s | WAV Loop |
| Floorboard creak | Crujido de piso de madera | 0.6s | WAV |
| Door creak | Puerta rechina (cerrada) | 1s | WAV |
| Footsteps on wood | Pasos del jugador | Variante | WAV |
| Footsteps on tile | Pasos en baldosa | Variante | WAV |

#### **Categoría: Interacción del Jugador**

| SFX | Descripción | Duración | Uso |
|-----|-------------|----------|-----|
| Item pickup | Sonido de recoger pista | 0.5s | Encontrar Reality Anchor |
| Menu select | Click suave de menú | 0.3s | Seleccionar opción |
| Menu hover | Hover de botón | 0.2s | Pasar sobre opción |
| Notification chime | Campana de notificación | 0.7s | Pista encontrada |
| Error tone | Sonido de error | 0.4s | Acción inválida |
| Typing | Teclear máquina | 0.1s x N | Entrada de texto |

#### **Categoría: Entidad/Enemigo**

| SFX | Descripción | Duración | Uso |
|-----|-------------|----------|-----|
| Spirit whoosh | Viento de espíritu | 1.2s | Aparición |
| Spirit scream | Grito procesado (lejano) | 2s | Ataque |
| Spider skittering | Crujidos de patas | 1.5s | Movimiento araña |
| Spider hiss | Silbido de araña | 0.8s | Advertencia araña |
| Crowd whisper | Susurros de multitud | 3s | Entidad social |
| Water gurgle | Burbujeo de agua | 2s | Entidad acuática |
| Heartbeat | Latido cardíaco | 0.6s | Persecución |
| Breathing heavy | Respiración acelerada | 1.2s | Ansiedad |

#### **Categoría: Anomalías**

| SFX | Descripción | Duración | Uso |
|-----|-------------|----------|-----|
| Glass shatter | Vidrio quebrándose | 1.2s | Distorsión visual |
| Electrical zap | Descarga eléctrica | 0.5s | Glitch de realidad |
| Reverse rush | Sonido al revés | 1s | Gravedad inversa |
| Distortion wave | Onda de distorsión | 1.5s | Anomalía |
| Temporal glitch | Salto de tiempo | 0.8s | Error de tiempo |

#### **Categoría: Interfaz/Diálogos**

| SFX | Descripción | Duración | Uso |
|-----|-------------|----------|-----|
| Test start | Sonido de inicio de test | 0.6s | Comenzar test |
| Test answer | Respuesta registrada | 0.4s | Seleccionar opción test |
| Test complete | Test completado | 1.5s | Fin de test |
| Dialogue line | Línea de diálogo | Variable | Charla terapeuta |
| Phone ring | Teléfono sonando | 2s | Llamada entrante |

---

### **D. Sistema de Audio Espacial (3D)**

**Implementación:** Godot's built-in Spatial Audio + HRTF (Head-Related Transfer Function)

**Configuración:**
- Distancia de sonido máxima: 30 metros
- Atenuación: -6dB por duplicación de distancia
- Reverberación ambiental: Varía por zona (baño reverberante, sala seca)

**Puntos de Escucha (Listener):**
- Attached a la cámara del jugador (immersive)
- Reacciona a movimiento de cabeza (si usar VR en futuro)

**Ejemplos de Uso:**
- Pasos del enemigo en 3D (distancia variable)
- Susurros del espíritu viniendo de direcciones específicas
- Teléfono "llamando" desde dormitorio
- Ventana (viento viene de dirección correcta)

---

### **E. Doblaje (Voice Acting)**

#### **Personaje Principal: Dr. Matthias Krell (Terapeuta)**

**Perfil de Voz:**
- **Edad:** 50-60 años
- **Acento:** Neutral español (castellano recomendado) o Latino
- **Tono:** Cálido, profesional, ligeramente mecánico (AI sugerida)
- **Personalidad:** Cuidadoso, atento, pero con duda implícita

**Líneas de Diálogo (Muestra):**

*Acto I:*
> "Hola, soy el Dr. Krell. Veo en tu historial que has estado experimentando síntomas de ansiedad. ¿Cómo ha sido tu semana?"

*Acto II:*
> "Parece que los síntomas han empeorado. La medicación no parece estar funcionando como esperábamos. Necesitamos ajustar la dosis."

*Acto III:*
> "Escúchame bien. Lo que estás experimentando puede ser una reacción adversa severa. Debes confiar en mí. Sigo aquí contigo."

*Final Bueno:*
> "Despertaste. Fue una alucinación severa causada por la medicación. Te recuperarás. No estás solo."

**Casting:**
- Actor profesional de doblaje con experiencia en horror/thriller
- Capaz de variar tono según salud mental del jugador
- Grabación en estudio profesional, sin ruido de fondo
- Post-producción: Light EQ, normalización, compresión

#### **Sonidos No-Diálogo:**

**Protagonista:**
- Respiración (normal, ansiosa, jadeante)
- Gemidos, murmullos internos
- Gritos ocasionales (estímulo de ataque)
- Sollozos (moments of breakdown) - Optional

**Voces de Entidad:**
- Susurros sin palabras (algoritmo generador o processed voice)
- Gritos distorsionados
- Lenguaje incomprehensible
- Eco de voces pasadas del jugador

---

### **F. Licenciamiento de Audio**

**Opción 1: Composición Original** (Recomendado pero costoso)
- Presupuesto: $3,000-8,000 USD
- Tiempo: 8-12 semanas
- Ventaja: Sonido único, copyright total
- Compositor: Buscar portafolio de juegos de horror

**Opción 2: Licencias Royalty-Free**
- Fuentes: Epidemic Sound, AudioJungle, Incompetech
- Presupuesto: $500-1,500 USD
- Ventaja: Rápido, económico
- Desventaja: Menos único

**Opción 3: Combinación Híbrida** (Recomendado)
- Composición original para momentos clave (opening, finales)
- Música ambient royalty-free para exploración
- Presupuesto: $2,000-4,000 USD

---

## **III. REFERENCIAS Y GUÍA DE ESTILO**

### **Referencias Visuales (Moodboards)**

**Búsqueda de inspiración:**
- Pinterest board: "Psychological Horror Interior Design"
- Películas: *Hereditary*, *Invisible Man* (2020), *Midsommar*, *The Lighthouse*
- Fotógrafos: Gregory Crewdson (fotocomposición surreal)
- Concept art: Simon Stålenhag (Ciencia ficción distópica)

**Imágenes clave a recopilar:**
1. Apartamentos urbanos minimalistas (base realista)
2. Iluminación de horror (sombras dramáticas)
3. Distorsiones visuales (glitch art, databending)
4. Entidades fantásticas (diseño creature)
5. Interfaces clínicas/médicas (UI referencia)

---

### **Influencias Sonoras (Playlists)**

**Música:**
- Spotify: "Dark Ambient Horror" playlists
- Compositores clave: Akira Yamaoka, Trent Reznor, John Carpenter, Jóhann Jóhannsson
- Géneros: Dark Ambient, Industrial, Drone, Experimental Electroacoustic

**SFX:**
- Freesound.org (community SFX library)
- Epidemic Sound SFX library
- Generador de SFX: Bfxr (8-bit), jsfxr (browser-based)

---

## **IV. PIPELINE DE PRODUCCIÓN DE ARTE**

### **Workflow 3D:**
```
Concepto 2D
    ↓
Blockout 3D (Low-poly)
    ↓
Modelado Detallado (Sculpting en Blender)
    ↓
UV Mapping
    ↓
Texturizado (Substance Painter o similar)
    ↓
Rigging y Animación
    ↓
Exportar como FBX/GLB
    ↓
Importar a Unity (configurar import settings)
    ↓
Lighting/Shading con URP/HDRP
    ↓
Optimización (LOD, Occlusion Culling)
```

### **Workflow Audio:**
```
Composición (DAW: Reaper)
    ↓
Grabación de SFX
    ↓
Edición y Post-producción
    ↓
Normalización y Mastering
    ↓
Exportar formatos (OGG/MP3 para engine, WAV para desarrollo)
    ↓
Implementación en Unity (AudioClip, AudioSource)
    ↓
Configurar Spatial Blend y Reverb Zones
    ↓
Pruebas de spatial audio con Audio Mixer
```

---

## **V. GUÍA DE CALIDAD**

### **Verificación de Arte:**
- [ ] Texturas sin seams visibles
- [ ] Polígonos optimizados (target: <100K total)
- [ ] Iluminación consistente con paleta de acto
- [ ] Anomalías visuales claras pero sutiles
- [ ] Performance: 60 FPS en hardware target

### **Verificación de Audio:**
- [ ] Niveles normalizados (-3dB headroom)
- [ ] Sin clicks/pops en loops
- [ ] Espacial audio testado con auriculares
- [ ] Diálogos claros, sin distorsión
- [ ] Sync de SFX con animaciones

---

**Especificación de Arte y Audio: Completa y lista para producción**
