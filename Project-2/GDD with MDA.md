# GAME DESIGN DOCUMENT (GDD)
## **PHOBIA: A Psychological Horror Experience**

---

## **I. FICHA TÉCNICA Y CONCEPTO**

### Título
**PHOBIA**

### Género
- Primer género: **Psychological Horror / Walking Simulator**
- Segundo género: **Narrative Adventure**
- Mecánicas: **Adaptive Gameplay basado en Inteligencia Artificial Pedagógica**

### Plataforma Objetivo
- **PC (Windows/Mac/Linux)** - Versión primaria
- Consideración futura: Console ports (PS5, Xbox Series X|S)

### Motor Propuesto
- **Unity 2022 LTS+** (Versátil, robusto, ideal para experiencias narrativas en 3D)
- Alternativa: **Unreal Engine 5** (para mayor fidelidad gráfica)

### Target Audience
- **Edad mínima:** 16+ (contenido de salud mental, referencias a suicidio, violencia psicológica, violencia explícita)
- **Género:** Sin restricción
- **Perfil psicográfico:** Jugadores que buscan experiencias narrativas profundas, fans de juegos como *PT*, *Silent Hill*, *Psychological Thriller Games*

### Sinopsis / Elevator Pitch

> *"PHOBIA es un juego de horror psicológico adaptativo donde el jugador encarna a una persona sola en su apartamento, aquejada por visiones de un ente sobrenatural. Conforme avanza, participa en tests psicológicos dentro del juego que modulan dinámicamente la experiencia: sus fobias se manifiestan como enemigos, los objetos cotidianos se retuercen en alucinaciones, y cada decisión lo acerca a dos finales irreversibles: despertar curado o descubrir que ya está muerto."*

---

## **II. ANÁLISIS MDA (MECHANICS, DYNAMICS, AESTHETICS)**

### **A. AESTHETICS (Estética - La Experiencia Emocional)**

#### Emociones Objetivo
1. **Inquietud progresiva** → Transición de comodidad a paranoia
2. **Aislamiento y soledad** → Reforzado por entorno vacío y silencio puntúado
3. **Agencia comprometida** → El jugador se siente atrapado en su propia mente
4. **Revelación gradual** → Teoría del "Unreliable Narrator"
5. **Catarsis o tragedia** → Dos finales con peso emocional

#### Experiencia Deseada
- El jugador debe sentir que su salud mental se deteriora progresivamente
- Debe cuestionarse la realidad a través de pistas ambientales sutiles
- Debe tener curiosidad de lo que paso con su personaje
- Debe sentirse "visto" por el juego (personalización profunda basada en sus respuestas)
- Debe experimentar **tensión sin combate tradicional** (el horror es mental, no física)

### **B. DYNAMICS (Dinámicas - El Comportamiento Emergente)**

Las mecánicas crean estas dinámicas clave:

| Dinámica | Descripción | Ejemplo |
|----------|------------|---------|
| **Indagación Introspectiva** | El jugador responde tests que revelan sus psiquis | Test de Beck dentro del juego → Sistema detecta depresión → Enemigos se tornan más persistentes |
| **Adaptación Enemiga** | El tipo de amenaza muta según el perfil psicológico | Fobia social → Muchedumbre de espectros; Aracnofobia → Arañas gigantes |
| **Realidad Frágil** | El entorno contiene anomalías que cuestionan la cordura | Cuadro invertido, licuadora en techo, gravedad inconsistente |
| **Progresión Bifurcada** | Las decisiones en tests llevan a dos finales opuestos | Completar 5 pistas + responder afirmativamente al test final = Final "Bueno" / Rechazar = Final "Malo" |
| **Bucle de Juego Repetitivo** | En el mal final, el jugador queda atrapado en ciclo | Loop infinito de respuestas iguales |

### **C. MECHANICS (Mecánicas - Las Reglas del Sistema)**

#### **Core Mechanics**

1. **Narrative Branching basada en Tests**
   - Tests psicológicos cortos (Beck modificado, MMPI-2 simplificado)
   - Cada respuesta afecta: Parámetro de salud mental, tipo de enemigo, diálogos disponibles
   - Rango de salud mental: 0-100 (0 = cordura total, 100 = locura total)

2. **Adaptive Enemy Spawning**
   - Pool de arquetipos de enemigos:
     - Espíritu genérico (default)
     - Multitud opresiva deforme (fobia social)
     - Araña gigante hecha de cuerpos (aracnofobia)
     - Entidad de agujas (tripanofobia)
     - Entidad con hollos (tripofobia)
     - Sombras faciales (fobia a rostros)
   - Algoritmo: `EnemyType = SelectFrom(FobiaProfile) IF SanityLevel > Threshold`

3. **Reality Anchors (Pistas de Realidad o de acontecimiento)**
   - Sistema de 5 objetos "anomalía" en el apartamento
   - Tipos:
     - Visual: Cuadro invertido, espejo sin reflejo
     - Física: Licuadora flotante, agua que fluye hacia arriba, cuchillo clavado en pared
     - Temporal: Reloj corriendo hacia atrás, TV mostrando el mismo frame
   - Interacción: El jugador debe recopilar 5 pistas antes de la audiencia final
   - Impacto: Cada pista reduce Sanity en 5 puntos (evidencia = estabilidad)

4. **Dialogue System con Personalización**
   - Parámetros de inicio:
     - Nombre del protagonista
     - Profesión (Programador, Escritor, Diseñador, etc.)
     - Antecedentes de salud mental (pregunta genérica)
   - Ejemplo de ramificación:
     ```
     IF profession == "programmer":
         dialogue = "Llevo 12 horas frente al monitor... creo que mis ojos juegan trucos"
     ELSE IF profession == "writer":
         dialogue = "La página en blanco me consume. ¿Es inspiración o paranoia?"
     ```

5. **Sanctuary Mechanic**
   - El apartamento es el jugador (no hay "salida")
   - Ciertos espacios son "seguros" (cama, baño) = Sanity regen +2/s
   - Espacios "peligrosos" (ventanas, puerta) = Sanity drain -1/s
   - Movimiento: Click-to-move (no hay combate directo)

#### **Progression System**

**Acto I: Normalidad Rota (Sanity: 80-60)**
- Introducción personalizada
- Anomalías sutiles (luz parpadeante, sonidos off-screen)
- Primer test psicológico (screening rápido)

**Acto II: Fragmentación (Sanity: 60-40)**
- Test Beck completo
- Enemigos adaptativos aparecen
- 3 de 5 pistas encontradas
- Diálogos de terapia (personaje psiquiatra por teléfono/video)

**Acto III: Colapso (Sanity: 40-0)**
- Test final decisivo
- Bifurcación de narrativa
- Dos escenas finales

#### **Control Scheme**
- **WASD**: Movimiento
- **E**: Interactuar / Recopilar pistas
- **ESC**: Menú / Línea de terapia (pausar el juego)
- **Mouse**: Click-to-move (alternativa)
- **No hay combate directo**: Solo evasión y escondimiento

---

## **III. MECÁNICAS DETALLADAS (GAME SYSTEM DESIGN)**

### **A. Core Loop (El Ciclo Principal)**

```
┌─────────────────────────────────────────────────────┐
│                  CORE GAMEPLAY LOOP                 │
├─────────────────────────────────────────────────────┤
│                                                     │
│  1. EXPLORE APARTMENT                               │
│     └─> Find Reality Anchors (pistas)               │
│     └─> Trigger Environmental Anomalies             │
│                          ↓                          │
│  2. ENCOUNTER THREAT                                │
│     └─> Adaptive Enemy appears (based on PHOBIA)    │
│     └─> Evade/Hide (no combat)                      │
│     └─> Sanity Drain                                │
│                          ↓                          │
│  3. REACH SANCTUARY                                 │
│     └─> Sanity Regen                                │
│     └─> Receive Therapy Dialogue (optional)         │
│                          ↓                          │
│  4. PSYCHOLOGICAL TEST                              │
│     └─> Answer questions (adapt enemies)            │
│     └─> Reach 5 pistas collected → Final Test       │
│                          ↓                          │
│  5. ENDING SEQUENCE                                 │
│     └─> Good Ending: Awakening (Drug Intoxication)  │
│     └─> Bad Ending: Suicide Loop (Trapped)          │
│                                                     │
└─────────────────────────────────────────────────────┘
```

### **B. Sistema de Salud Mental (Sanity System)**

**Parámetro Central: Sanity (0-100)**

| Rango | Estado | Comportamiento | Enemigos |
|-------|--------|-----------------|----------|
| 80-100 | Normal | Interfaz clara, sonido ambiental normal | Ninguno |
| 60-80 | Inquieto | Distorsión visual leve (viñeta), audio glitchy | Spawns esporádicos |
| 40-60 | Fragmentado | Distorsión cromática, alucinaciones auditivas | Spawns frecuentes |
| 20-40 | Desquiciado | Pantalla invertida periódicamente, UI glitchea | Spawns agresivos, multiples |
| 0-20 | Colapso | Realidad totalmente comprometida | Enemigos imparables |

**Eventos que afectan Sanity:**
- Encontrar pista: -5 (realidad se refuerza)
- Ser detectado por enemigo: -10
- Completar test: ±15 (depende de respuestas)
- Estar en Sanctuary: +2/segundo
- Ver anomalía: -3
- Completar Acto: ±20

### **C. Adaptive Psychosis Algorithm**

**Pseudocódigo:**

```
FUNCTION SpawnEnemyType():
    sanity = GetPlayerSanity()
    phobias = GetPlayerPhobias() // Extraído de Tests
    
    IF sanity < 40 AND phobia_social > 70:
        SPAWN CrowdOfSpecters(count = sanity/10)
    ELSE IF sanity < 50 AND arachnophobia > 75:
        SPAWN GiantSpiders(count = 3)
    ELSE IF sanity < 60 AND aquaphobia > 60:
        SPAWN WaterEntity()
    ELSE:
        SPAWN GenericSpirit()
    
    enemy.aggressivity = MAX(50, sanity) // More insane = faster enemy
    enemy.persistence = true // They follow forever, no despawn
```

### **D. Sistema de Diálogos Adaptativos**

**Variables de Personalización:**
- `playerName`: String (entrada inicial)
- `profession`: Enum {Programmer, Writer, Designer, Engineer, Artist, Student, Other}
- `livingArrangement`: Enum {Alone, WithFamily, WithPartner}
- `mentalHealthHistory`: Int (escala 1-10)
- `phobiaProfile[]`: Array de fobias detectadas

**Ejemplo de árbol de diálogos:**

```
SCENE: Therapist Call
IF profession == "programmer" AND mentalHealthHistory > 7:
    therapist: "Trabajar desde casa puede ser aislante. 
               ¿Has notado patrones de insomnio?"
ELSE IF profession == "writer":
    therapist: "La creatividad puede mezclar realidad con ficción.
               ¿Dónde termina tu personaje y empiezas tú?"
ELSE:
    therapist: "Cuéntame cómo ha sido tu semana..."
```

### **E. Inventory & Reality Anchors**

**Sistema Simple:**
- No hay "inventario" tradicional
- Pistas se registran automáticamente cuando se encuentran
- UI muestra: `[Pistas encontradas: 3/5]`
- Efecto: Cada pista refuerza "este puede ser un sueño"

**Las 5 Pistas pueden ser:**
1. Cuadro de fotografía personal invertido (visual)
2. Licuadora flotando en el techo (física)
3. Agua fluyendo hacia arriba en el fregadero (física)
4. TV repitiendo el mismo segundo (temporal)
5. Reflejo del jugador no coincide con movimiento (espejo/realidad)

### **F. Save System & Branching**

**Autosave en checkpoints:**
- Después de cada test
- Después de encontrar pista
- Antes de escena de test final

**Ramificaciones críticas:**
- Final Test: "¿Quieres continuar?" (YES/NO)
  - **YES** → Good Ending (despierta en hospital)
  - **NO** → Bad Ending (descubre el suicidio, loop infinito)

**Nota:** No hay "Nueva Partida+" pero el final malo permite reintentos desde el test final.

---

## **IV. NARRATIVA Y MUNDO (WORLDBUILDING)**

### **A. Premisa General**

Un profesional de X años, viviendo en un departamento urbano, comienza a experimentar una progresiva desconexión de la realidad. Está bajo cuidado médico (prescribe ansiolíticos/antidepresivos) pero la medicación misma se vuelve sospechosa. ¿Está realmente enfermo o está siendo perseguido por algo sobrenatural?

El juego revela (dependiendo de las elecciones del jugador):
- **Camino Bueno:** Toda la experiencia fue una alucinación causada por intoxicación farmacológica. El protagonista despierta en un hospital o su hogar, con posibilidad de recuperación.
- **Camino Malo:** El protagonista ya estaba muerto desde el principio, atrapado en el momento de su suicidio, condenado a revivirlo infinitamente.

### **B. Personajes Principales**

#### **1. El Protagonista (Reflejo del Jugador)**
- **Nombre:** Definido por el jugador
- **Profesión:** Seleccionada por el jugador
- **Edad:** ~25-40 años (implícita)
- **Psicología:** Inicialmente racional, progresivamente fragmentado
- **Objetivo:** Entender qué está sucediendo / Escapar del apartamento (imposible) / Despertar
- **Desarrollo:** Su mentalidad se adapta a las respuestas del jugador

#### **2. Dr. Matthias Krell (Terapeuta)**
- **Rol:** Voz de la razón / Catalizador de pruebas psicológicas
- **Interacción:** Llamadas telefónicas o videoconferencias periódicas
- **Diálogos:** Varían según la salud mental del jugador
  - Si Sanity baja: "Parece que hemos empeorado... Necesitamos ajustar la medicación"
  - Si Sanity sube: "Veo progreso. Sigue con el protocolo"
- **Twist (Final Bueno):** Es real, el médico que lo atiende en el hospital
- **Twist (Final Malo):** Nunca existió, era una alucinación más

#### **3. La Entidad / El Espíritu**
- **Naturaleza:** Ambigua
  - ¿Manifestación psicológica?
  - ¿Ente sobrenatural?
  - ¿Proyección del inconsciente?
- **Forma:** Adapta su apariencia según las fobias del jugador
- **Intención:** Ambigua; parece perseguir pero también proteger (twist final)
- **Función narrativa:** Espejo del viaje psicológico del jugador

### **C. Actos y Estructura Narrativa**

#### **ACTO I: LA PUERTA DEL SUEÑO (Horas 0-2)**
- **Escena inicial:** Despertar en el apartamento, confusión suave
- **Evento catalizador:** Primera aparición de la entidad
- **Test:** Screening rápido (5 preguntas sobre síntomas)
- **Tono:** Inquietud creciente, aún hay duda sobre la realidad
- **Culminación:** Primera llamada con el terapeuta

#### **ACTO II: LA FRAGMENTACIÓN (Horas 2-6)**
- **Evento central:** Test de Beck completo (20 preguntas)
- **Mecánica:** Aparecen enemigos adaptativos basados en respuestas
- **Progresión:** El jugador busca las 3 primeras pistas
- **Punto medio:** Aparentemente, "la medicación no funciona"
- **Tono:** Horror psicológico, paranoias crecientes
- **Culminación:** El terapeuta sugiere cambio de tratamiento

#### **ACTO III: EL COLAPSO (Horas 6-10)**
- **Crisis:** La realidad se desmorona visiblemente
- **Desafío:** Encontrar las últimas 2 pistas
- **Test Final:** "¿Deseas continuar la terapia?"
  - **Respuesta 1 (Afirmativo):** Camino al final bueno
  - **Respuesta 2 (Negativo):** Camino al final malo
- **Culminación:** Escena de resolución

#### **ESCENA FINAL - CAMINO BUENO (30 min)**
- **Locación:** Hospital o casa del protagonista
- **Evento:** Despertar. El doctor está presente.
- **Revelación:** "Tuviste una reacción adversa a la medicación. Alucinaciones severas."
- **Diálogos de cierre:** Se abre puerta a recuperación
- **Tono:** Catártico, ligeramente esperanzador, bittersweet
- **Créditos:** Se ejecutan con el protagonista en terapia (recuperándose)

#### **ESCENA FINAL - CAMINO MALO (30 min)**
- **Locación:** La terraza del apartamento
- **Evento:** El jugador ve su propio cuerpo caído en la acera (o en el piso de abajo)
- **Revelación:** "Ya estaba muerto. Todo fue el instante antes de caer."
- **Conciencia:** El protagonista entiende que revivirá este momento infinitamente
- **Tono:** Horror absoluto, desesperación, Lovecraftiano
- **Créditos:** Loop infinito de la misma escena (mecánica de juego)

### **D. Temas Narrativos**

1. **Salud Mental Estigmatizada:** ¿Quién define la "realidad" de una mente enferma?
2. **Soledad Urbana:** Vivir en la ciudad pero completamente aislado
3. **Identidad Fragmentada:** El juego refleja la del jugador
4. **Libre Albedrío vs. Destino:** ¿Pueden tus decisiones cambiar el final?
5. **Realidad Subjetiva:** La única realidad es la experiencia del individuo

---

## **V. DISEÑO DE NIVELES (LEVEL DESIGN)**

### **A. Mapa Único: El Apartamento (70 m²)**

**Características:**
- Mundo lineal pero explorable en todas direcciones
- Un único entorno que se transforma progresivamente
- Espacios claramente diferenciados

#### **Zonas del Apartamento:**

```
┌─────────────────────────────────────┐
│        APARTMENT LAYOUT              │
├─────────────────────────────────────┤
│                                     │
│  ┌─────────┐         ┌──────────┐   │
│  │ BEDROOM │─────────│ BATHROOM │   │
│  │ (Safe)  │         │ (Puzzle) │   │
│  └─────────┘         └──────────┘   │
│      │                     │         │
│  ┌───┴──────────────────────┴───┐   │
│  │    LIVING ROOM             │   │
│  │    (Main Encounter Area)    │   │
│  │    • Sofa (Hide)            │   │
│  │    • Window (Danger)        │   │
│  │    • TV (Anomaly)           │   │
│  └────────────┬────────────────┘   │
│               │                     │
│  ┌────────────┴──────────────┐    │
│  │ KITCHEN     │ HALLWAY     │    │
│  │ (Danger)    │ (Neutral)   │    │
│  │ • Fridge    │ • Door      │    │
│  │ • Sink      │ • Mirror    │    │
│  └─────────────┴──────────────┘    │
│                                     │
│  ┌────────────────────────────┐    │
│  │ TERRAZA (Final Scene Only) │    │
│  └────────────────────────────┘    │
│                                     │
└─────────────────────────────────────┘
```

#### **Detalles de Zonas:**

| Zona | Seguridad | Eventos | Pistas Posibles |
|------|-----------|---------|-----------------|
| **Dormitorio** | Alta (+2 sanity/s) | Pesadillas, TV habla, espejo se anima | Foto invertida, reloj al revés |
| **Baño** | Media | Agua anómala, reflejo desfasado | Espejo sin reflejo, agua ascendente |
| **Sala** | Baja | Apariciones principales, TV glitchea | Cuadro invertido, luz parpadeante |
| **Cocina** | Baja | Objetos flotan, nevera susurra | Licuadora flotante, comida podrida |
| **Pasillo** | Media | Ecos, sombras en las paredes | Puerta que no abre, retratos se tuercen |
| **Ventanas** | Muy Baja | Siluetas afuera, presión atmósférica | Suicidio visible en final malo |
| **Terraza** | N/A | SOLO FINAL: Propio cuerpo caído | Final Malo trigger |

### **B. Flujo de Dificultad y Progresión Espacial**

```
Acto I: Exploración libre (todas las zonas accesibles)
  ↓
Acto II: Apariciones peligrosas en cocina/sala (dormitorio aún seguro)
  ↓
Acto III: Amenaza en toda parte (solo dormitorio es refugio temporal)
  ↓
Escena Final: Obligado a ir a la terraza
```

### **C. Pistas y Anomalías por Zona**

**Dormitorio - Pista 1: Fotografía Invertida**
- Descripción: Una foto del protagonista joven está boca abajo en el escritorio
- Impacto: "¿Cuándo fue tomada?"
- Sanity: -5

**Baño - Pista 2: Espejo Sin Reflejo**
- Descripción: El reflejo no copia los movimientos exactamente (lag de 2 segundos)
- Impacto: "Mi reflejo tiene su propia voluntad"
- Sanity: -5

**Cocina - Pista 3: Licuadora Flotante**
- Descripción: Licuadora suspendida en el aire, encima del refrigerador
- Impacto: "Las leyes de la física no aplican"
- Sanity: -5

**Fregadero - Pista 4: Agua Ascendente**
- Descripción: El agua fluye hacia arriba cuando se abre la llave
- Impacto: "La gravedad se invirtió"
- Sanity: -5

**Sala - Pista 5: TV Repetida**
- Descripción: La TV siempre muestra el mismo segundo (el protagonista notando anomalías)
- Impacto: "¿Está grabado? ¿Estoy en un loop?"
- Sanity: -5

---

## **VI. ARTE Y AUDIO (LOOK & FEEL)**

### **A. Dirección Visual**

#### **Estilo General**
- **Realismo fotográfico desquiciado:** El apartamento es mundano, pero progresivamente distorsionado
- **Influencias visuales:**
  - *Hellblade: Senua's Sacrifice* (distorsión perceptual)
  - *Layers of Fear* (entorno hostil que se transforma)
  - *P.T.* (horror ambiental y repetición)

#### **Paleta de Colores**

| Acto | Colores | Saturación | Efecto |
|------|---------|-----------|--------|
| **Acto I** | Grises, azules fríos, verdes apagados | 60% | Normalidad opresiva |
| **Acto II** | Rojos desaturados, sombras púrpuras | 40% | Distorsión temprana |
| **Acto III** | Rojo intenso, negro, blanco inverso | 10-150% | Realidad fracturada |
| **Fin Bueno** | Azul esperanzador, blanco limpio | 100% | Purificación |
| **Fin Malo** | Negro total, rojo sangre | Máximo | Infierno |

#### **Elementos Visuales Clave**

1. **Viñeta Dinámica:** Aumenta conforme desciende Sanity
2. **Chromatic Aberration:** Glitch visual que intensifica en tensión
3. **Screen Flicker:** Distorsión temporal
4. **Reflection Lag:** El reflejo no sincroniza exacto
5. **Volumetric Fog:** Niebla que emerge de la nada
6. **Lighting Flickers:** Luces que parpadean sin razón

### **B. Diseño de Personajes / Entidades**

#### **La Entidad (Adaptive Form)**

**Estado Base:** Humanoidea, andrajosa, sin características claras

**Transformación según fobias:**
- **Aracnofobia:** Forma de araña (cuerpo humanoide, 8 extremidades)
- **Fobia social:** Multitud de rostros (espectros solapados)
- **Acuafobia:** Entidad líquida (agua con forma humana)
- **Nomofobia (sin teléfono):** Sombra de alguien siempre buscando conectarse

### **C. Sonido y Audio**

#### **Música**

**Estilo:** Minimalista, disonante, ansioso

| Escena | Compositor Inspiración | BPM | Instrumentación |
|--------|----------------------|-----|-----------------|
| **Menú** | Akira Yamaoka (Silent Hill) | 80 | Sintetizador ambiental |
| **Exploración** | Trent Reznor (The Social Network) | 90-110 | Piano discordante + síntesis |
| **Encuentro** | Jóhann Jóhannsson | 120-140 | Strings tensos, drones bajos |
| **Santuario** | Disasterpeace (It Follows) | 60-80 | Pad suave, piano tranquilo |
| **Test** | John Carpenter | 100 | Sintetizador pulsante |

#### **Efectos de Sonido**

- **Pasos:** Variación según material (moqueta, baldosa, madera)
- **Respiración del jugador:** Se acelera conforme baja Sanity
- **Susurros:** Voz distorsionada del terapeuta, fragmentos de diálogos pasados
- **Anomalías:** Sonidos imposibles (gravedad inversa, tiempo al revés)
- **Ataque/Persecución:** Sonido envolvente 3D, pitch que sube

#### **Diálogo**

- **Terapeuta:** Voz cálida pero ligeramente mecánica (puede ser IA)
- **Protagonista:** Sin voz (el jugador es él) o susurros internos
- **La Entidad:** Sonidos no-humanos, ecos, distorsión

**Idioma:** Español (doblaje profesional) con opciones de subtítulos en múltiples idiomas

### **D. UI/UX Design**

#### **HUD Minimalista**

**En juego:**
- Contador de pistas: `[Pistas: 3/5]` (esquina superior izq)
- Indicador de Sanity: Barra sutil (se desaturiza conforme cae) - esquina superior der
- Indicadores de amenaza: Pulsación de luz si entidad está cerca
- Sin minimapa (refuerza la desorientación)

**Menús:**
- Fuente: Monoespaciada (tipo terminal) para reflejar fragmentación
- Contraste alto (blanco/negro inverso en final malo)
- Animaciones lentas (enfatiza la incomodidad)

---

## **VII. ARQUITECTURA DE SOFTWARE (INGENIERÍA)**

### **A. Tecnología Propuesta**

**Motor:** Unity 2022 LTS+
- **Ventajas:**
  - Ecosistema maduro y ampliamente adoptado
  - Excelente soporte para desarrollo 3D
  - Asset Store con recursos extensos
  - Comunidad global de desarrollo de juegos de terror
  - Herramientas de profiling y optimización robustas
  
**Backend (si se expande):** Node.js + Express (para análisis anónimo de datos de jugador)
- Analytics: Qué fobias son más comunes, qué final prevalece

**Lenguaje de scripting:** C# (nativo de Unity, robusto y ampliamente documentado)

### **B. Diagrama de Clases Conceptual (UML)**

```
┌─────────────────────────────────────────────────────┐
│                   ARCHITECTURE                      │
├─────────────────────────────────────────────────────┤

┌──────────────┐
│ GameManager  │ (Singleton)
├──────────────┤
│ - sanity: float
│ - currentAct: Enum
│ - phobiaProfile: Dict
│ - onSanityChanged: Signal
│ - onEnemySpawned: Signal
└────────┬─────┘
         │
         ├─→ PlayerController
         ├─→ TestSystem
         ├─→ EnemyManager
         └─→ DialogueSystem

┌──────────────────────┐
│ PlayerController     │
├──────────────────────┤
│ - position: Vector3
│ - movementSpeed: f
│ - currentSanity: f
│ + Move(direction)
│ + GetDamaged(amount)
│ + FindAnchor(anchor)
└──────────────────────┘

┌──────────────────────┐
│ TestSystem           │
├──────────────────────┤
│ - currentTest: Test
│ - responses: Array
│ + SpawnTest(type)
│ + AnalyzeResponses()
│ + ReturnPhobiaProfile()
└──────────────────────┘

┌──────────────────────┐
│ Enemy               │
├──────────────────────┤
│ - type: Enum
│ - sanityThreshold: f
│ - position: Vector3
│ - behavior: FSM
│ + FollowPlayer()
│ + PlaySound()
│ + IsDetected()
└──────────────────────┘

┌──────────────────────┐
│ DialogueSystem      │
├──────────────────────┤
│ - dialogueTree: JSON
│ - playerName: String
│ - profession: Enum
│ + LoadDialogue(id)
│ + AdaptDialogue(vars)
│ + PlayDialogue()
└──────────────────────┘

┌──────────────────────┐
│ RealityAnchor       │
├──────────────────────┤
│ - type: Enum
│ - location: Vector3
│ - isFound: bool
│ + Interact()
│ + PlayAnimation()
│ + ReduceSanity()
└──────────────────────┘
```

### **C. Patrones de Diseño Seleccionados**

| Patrón | Uso | Justificación |
|--------|-----|---------------|
| **Singleton** | GameManager | Solo debe haber un gestor de estado del juego |
| **Observer** | onSanityChanged Signal | Cambios de cordura disparan eventos (UI, Enemigos) |
| **State Machine** | AI del Enemigo | Estados: Idle, Searching, Chasing, Attacking |
| **Factory** | EnemySpawner | Crear diferentes tipos de enemigos dinámicamente |
| **Strategy** | DialogueSystem | Diferentes estrategias de diálogo según contexto |
| **Adapter** | TestSystem → PHOBIA Profile | Convertir respuestas de test a parámetros de juego |

### **D. Diagrama de Estados: Máquina de Estados del Enemigo**

```
┌──────────────┐
│    IDLE      │  (Enemigo espera)
└──────┬───────┘
       │ PlayerDetected
       ↓
┌──────────────┐
│  SEARCHING   │  (Buscando activamente)
└──────┬───────┘
       │ PlayerSpotted
       ↓
┌──────────────┐
│   CHASING    │  (Persigue al jugador)
└──────┬───────┘
       │ PlayerCaught
       ↓
┌──────────────┐
│  ATTACKING   │  (Drenando sanity)
└──────┬───────┘
       │ PlayerEscaped (Sanctuary)
       ↓
┌──────────────┐
│    IDLE      │  (Vuelve a esperar)
└──────────────┘
```

### **E. Sistema de Persistencia y Datos**

**Guardar Partida (JSON):**
```json
{
  "playerName": "Diego",
  "profession": "programmer",
  "currentAct": 2,
  "sanity": 45.7,
  "anchorsFound": [1, 3, 4],
  "testResponses": {
    "screening": [1, 0, 2, 1, 0],
    "beck": [/* 20 respuestas */],
    "finalTest": null
  },
  "phobiaProfile": {
    "socialPhobia": 78,
    "arachnophobia": 25,
    "aquaphobia": 15,
    "nomophobia": 65
  },
  "playTime": 7200,
  "ending": null
}
```

**Backend Analytics (Opcional):**
- Servidor recolecta (anónimamente) qué finales elige la mayoría
- Distribución de fobias detectadas
- Tiempo promedio por acto

---

## **VIII. CRONOGRAMA DE PRODUCCIÓN (ESTIMADO)**

*(Baseado en equipo de 4-6 personas, metodología Agile / Scrum)*

| Fase | Duración | Hitos |
|------|----------|-------|
| **Pre-producción** | 2 semanas | GDD final, concepto art, wireframes UI |
| **Prototipo Alpha** | 4 semanas | Core loop playable, un test funcional, una entidad |
| **Desarrollo Core** | 8 semanas | Todos los tests, 3 tipos de enemigos, 4 pistas, diálogos |
| **Pulido y QA** | 3 semanas | Balanceo, audio final, UI/UX refinement |
| **Beta Cerrada** | 2 semanas | Playtesting externo, ajustes finales |
| **Lanzamiento** | 1 semana | Build final, deployment, comunicados |
| **Post-lanzamiento** | Ongoing | Patches, feedback community, DLC narrativos (opcional) |

**Total Estimado:** 20 semanas (~5 meses)

---

## **IX. MÉTRICAS DE ÉXITO (DEFINICIÓN DE ÉXITO)**

### **Métricas de Engagement**
- ✓ 70% de jugadores completan al menos Acto II
- ✓ 50% juegan hasta un final (bueno o malo)
- ✓ Promedio de sesión: 8-12 horas
- ✓ Replay rate: 25% (para explorar el otro final)

### **Métricas de Impacto Narrativo**
- ✓ 80%+ de jugadores reportan sentir ansiedad/inquietud en encuestas post-juego
- ✓ 60%+ reconocen los temas de salud mental
- ✓ Redes sociales: Comunidad activa debatiendo los finales

### **Métricas Técnicas**
- ✓ Framerate consistente: 60 FPS (1080p, 30 FPS aceptable en consolas)
- ✓ Carga del juego: < 3 minutos
- ✓ Bugs críticos: 0 en lanzamiento

### **Métricas de Accesibilidad**
- ✓ Subtítulos en 5+ idiomas
- ✓ Modo daltónico (paleta invertible)
- ✓ Opción para reducir photosensitive triggers

---

## **X. RIESGOS Y MITIGACIÓN**

| Riesgo | Impacto | Probabilidad | Mitigación |
|--------|---------|-------------|-----------|
| **Scope creep** | Retrasos, presupuesto | Alta | Documentación clara del MVP, sprints cortos |
| **Narrativa compleja** | Confusión jugador | Media | Playtesting temprano, ajustes de claridad |
| **Sensibilidad de contenido** | Controversia / Rechazo | Media | Warnings claros, disclaimers sobre salud mental |
| **Performance en adaptación IA** | Freezes durante spawns | Baja | Optimización pre-generada de enemigos |
| **Audio sincronización** | Diálogos desfasados | Baja | Pipeline de audio robusto, testing continuo |

---

## **XI. REFERENCIAS Y INSPIRACIÓN**

### **Juegos de Referencia**
1. **Hellblade: Senua's Sacrifice** - Representación de psicosis, audio inmersivo
2. **What Remains of Edith Finch** - Narrativa intimista, exploración ambiental
3. **P.T.** - Tensión psicológica, entorno único, repetición inquietante
4. **The Stanley Parable** - Narrativa no lineal, cuestionamiento de libre albedrío
5. **Amnesia: The Dark Descent** - Horror sin combate, evasión
6. **Layers of Fear** - Transformación ambiental, perspectiva distorsionada

### **Influencias Narrativas**
1. *The Yellow Wallpaper* (Charlotte Perkins Gilman) - Locura por aislamiento
2. *The Tell-Tale Heart* (Edgar Allan Poe) - Narrador poco confiable
3. *Memento* (Christopher Nolan) - Fragmentación narrativa
4. *Black Swan* (Darren Aronofsky) - Dualidad psicológica, paranoia

### **Influencias Sonoras**
1. Akira Yamaoka (Silent Hill series)
2. Trent Reznor & Atticus Ross (The Social Network, Watchmen)
3. Jóhann Jóhannsson (Sicario, Mandy)

### **Recursos de Consulta**
- DSM-5 (Manual Diagnóstico de Trastornos Mentales)
- Beck Anxiety Inventory (BAI) - Adaptado para juego
- "Video Games and the Uncanny" - Academic papers

---

## **XII. CONSIDERACIONES ÉTICAS Y DE ACCESIBILIDAD**

### **Salud Mental**
- **Disclaimer inicial:** Aviso sobre contenido sensible
- **Resources:** Vínculos a líneas de crisis / asociaciones de salud mental
- **Trigger warnings:** Opcionales, configurables en menú
- **Tono responsable:** No glorificar la enfermedad mental

### **Accesibilidad**
- **Modo colorblind:** Paleta ajustable
- **Subtítulos:** Obligatorios, configurables en tamaño
- **Control remapeable:** Todos los inputs customizables
- **Opción de reducir estrés:** Dificultad baja = Sanity decae más lentamente

### **Inclusividad en Narrativa**
- **Profesiones variadas:** Reflejar diversidad de protagonistas
- **Sin presunciones de género:** Personaje género-neutro por defecto
- **Diversidad en representación de salud mental:** No es "demencia = villano"

---

## **APÉNDICE: PREGUNTAS DEL TEST PSICOLÓGICO ADAPTATIVO**

### **Screening Inicial (5 preguntas, ~2 min)**
1. "En la última semana, ¿cuántos días te sentiste deprimido?" (0-7)
2. "¿Has perdido interés en actividades que disfrutabas?" (Sí/No)
3. "¿Duermes más o menos de lo normal?" (Más/Normal/Menos)
4. "¿Has tenido pensamientos sobre hacerte daño?" (Sí/No) [CRÍTICO]
5. "¿Vives solo o acompañado?" (Solo/Familia/Pareja) [PERSONALIZACIÓN]

### **Test de Beck Completo (20 preguntas, ~10 min)**
*(Evaluación de síntomas depresivos, cada ítem 0-3 puntos)*

Ejemplos:
- "Siento tristeza todo el tiempo" (0-3)
- "Me cuesta concentrarme en tareas" (0-3)
- "He perdido el apetito" (0-3)
- "Veo el futuro sin esperanza" (0-3)
- [... 16 más ...]

**Resultado:** Score 0-63. Rangos:
- 0-13: Mínimo
- 14-19: Leve
- 20-28: Moderado
- 29-63: Severo

### **Detección de Fobias Específicas (10 preguntas adaptativas)**
*El sistema solo hace las que sean relevantes según respuestas previas*

- "Estar rodeado de mucha gente me causa ansiedad" (Fobia Social)
- "Las arañas me ponen nervioso" (Aracnofobia)
- "El agua profunda me asusta" (Aquafobia)
- "No poder acceder a mi teléfono me estresa" (Nomofobia)
- "Ver sangre me causa mareos" (Hemofobia)
- [... etc ...]

### **Test Final Decisivo (1 pregunta, irreversible)**
**"El protocolo terapéutico ha alcanzado su límite. Los síntomas no mejoran con medicación estándar. ¿Deseas continuar con la terapia experimental, o prefieres abandonar el tratamiento?"**

- **"Continuar"** → Good Ending
- **"Abandonar"** → Bad Ending

---

**[FIN DEL DOCUMENTO]**

---

*Documento preparado como especificación profesional de pre-producción. Listo para pasar a fase de prototipado y validación con playtesting.*

*Versión: 1.0 | Fecha: Enero 2026 | Estado: Para Revisión*
