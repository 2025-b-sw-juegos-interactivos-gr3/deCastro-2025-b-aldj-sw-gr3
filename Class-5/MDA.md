# Taller 1.1 — Deconstruyendo la Diversión

**Asignatura:** DESARROLLO DE JUEGOS INTERACTIVOS (ISWD823)  

**Programa:** Ingeniería de Software 

**Estudiante:** Aiden de Castro 

**Fecha:** Diciembre 2025 

**Docente:** Ing. Adrian Eguez

**Análisis de Sistemas con el framework MDA en la Ingeniería de Software de Videojuegos**

**Resumen:** Este informe aplica el framework MDA (Mecánicas, Dinámicas, Estéticas) para analizar seis géneros principales (Acción, Aventura, RPG, Estrategia, Simulación y Puzle). El objetivo es identificar patrones de diseño, polimorfismo en mecánicas y la arquitectura de los bucles de juego que generan experiencias lúdicas.



---

## Tabla de contenidos
- [Introducción](#introducción)
- [Marco Teórico — Framework MDA](#marco-teórico)
	- [Mecánicas (M)](#mecánicas-m)
	- [Dinámicas (D)](#dinámicas-d)
	- [Estéticas (A)](#estéticas-a)
- [Análisis por Género](#análisis-por-género)
	- [Acción — Devil May Cry 5](#acción)
	- [Aventura — Breath of the Wild](#aventura)
	- [RPG — Baldur's Gate 3](#rpg)
	- [Estrategia — Civilization VI](#estrategia)
	- [Simulación — Cities: Skylines](#simulación)
	- [Puzle — Portal 2](#puzle)
- [Tabla comparativa MDA](#tabla-comparativa-mda)
- [Análisis comparativo y crítico](#análisis-comparativo-y-crítico)
	- [Diferencias: Acción vs Estrategia](#diferencias)
	- [Similitudes: Polimorfismo de mecánicas](#similitudes)
	- [Híbridos: Convergencia Aventura–RPG](#híbridos)
- [Conclusión](#conclusión)
- [Referencias y notas](#referencias-y-notas)

---

## Introducción

En el desarrollo profesional de videojuegos (nivel de maestría), crear juegos es una disciplina de ingeniería de sistemas complejos. No basta con código funcional: es necesario diseñar sistemas que induzcan estados psicológicos específicos en el jugador. Un videojuego es un sistema interactivo donde agentes (jugadores) toman decisiones bajo reglas.

El framework MDA (Hunicke, LeBlanc & Zubek) permite separar la implementación técnica (Mecánicas), el comportamiento emergente (Dinámicas) y la experiencia fenomenológica (Estéticas). Este documento presenta el análisis del Taller 1.1 sobre seis géneros representativos.

## Marco teórico

El marco MDA define una jerarquía causal: desde el diseñador fluye M → D → A; desde el jugador se percibe A ← D ← M.

### Mecánicas (M)

Las mecánicas son los componentes atómicos: algoritmos, estructuras de datos, máquinas de estado, reglas condicionales. Representan los "verbos" disponibles (saltar, disparar, construir) y las reglas pasivas del entorno (gravedad, spawn rates, árboles de tecnología).

### Dinámicas (D)

Las dinámicas son los comportamientos emergentes cuando las mecánicas son puestas en ejecución por los inputs del jugador. Surgen de la interacción entre subsistemas y no siempre se programan explícitamente.

### Estéticas (A)

Las estéticas son las respuestas emocionales buscadas. LeBlanc propone ocho categorías principales: Sensation, Fantasy, Narrative, Challenge, Fellowship, Discovery, Expression y Submission. Un análisis MDA identifica qué combinación de estéticas prioriza cada sistema.

## Análisis por género

### Acción — Devil May Cry 5 (Capcom)

**Motor:** RE Engine

#### Mecánicas
- Cancelación de animaciones (jump canceling) — máquina de estados de alta prioridad de input.
- Sistema de estilo (ranking) — algoritmo que premia variedad y penaliza repetición.
- Física modificada para control "snappy".

#### Dinámicas
- Gestión riesgo/recompensa agresiva: forzar agresión constante para mantener el rango de estilo.
- "El suelo es lava": uso preferente del espacio aéreo por combos.
- Burlas tácticas usadas para manipular IA o medidores.

#### Estéticas
- Expresión, Sensación y Desafío: control estilizado, feedback sensorial intenso y curva de maestría.

#### Análisis de ingeniería
El algoritmo de puntuación altera el comportamiento del jugador: recompensa diversidad obliga a explorar profundidad de mecánicas.

### Aventura — The Legend of Zelda: Breath of the Wild (Nintendo)

**Motor:** "Chemistry Engine" (propietario)

#### Mecánicas
- Motor de "química": propiedades de materiales y reglas consistentes (madera inflamable, metal conductor, agua apaga fuego).
- Escalada universal con estamina.
- Durabilidad de armas.

#### Dinámicas
- Resolución de problemas emergente: múltiples soluciones no guionizadas.
- Exploración impulsada por líneas de visión y curiosidad en lugar de marcadores.
- Gestión de inventario improvisada por rotura de armas.

#### Estéticas
- Discovery y Fantasy; sensación de epifanía al experimentar reglas consistentes.

#### Análisis de ingeniería
Los sistemas generalizados escalan coste inicial de engineering pero multiplican situaciones jugables. Consistencia lógica reduce disonancia ludonarrativa.

### RPG — Baldur's Gate 3 (Larian Studios)

**Motor:** Divinity 4.0

#### Mecánicas
- Implementación del ruleset D&D 5e (tiradas d20 + modificadores).
- Superficies y elementos (agua+electricidad etc.).
- Árboles de diálogo condicionales mediante tags.

#### Dinámicas
- Save-scumming por RNG con consecuencias narrativas.
- Soluciones creativas (cheesing) soportadas por el sistema.
- Combate táctico posicional.

#### Estéticas
- Narrative, Fellowship y Expression: coautoría de la historia y profundidad social/rol.

#### Análisis de ingeniería
Gestión masiva de estados y flags para mantener coherencia narrativa ante múltiples acciones del jugador.

### Estrategia — Civilization VI (Firaxis)

**Motor:** Motor propietario (Firaxis)

#### Mecánicas
- Rejilla hexagonal y turnos.
- Distritos y bonificaciones por adyacencia.
- Árboles de tecnología y civismo (DAGs).

#### Dinámicas
- Snowballing (retroalimentación positiva).
- "Un turno más": retención por objetivos a distintos plazos.
- Guerra asimétrica por diferencia tecnológica.

#### Estéticas
- Challenge, Fantasy y Submission (ritmo de turnos relajante en fases).

#### Análisis de ingeniería
IA y planificación a gran escala: desafío computacional para crear agentes competentes sin "trucos".

### Simulación — Cities: Skylines (Colossal Order)

**Motor:** Unity

#### Mecánicas
- Simulación basada en agentes (Cims).
- Zonificación RCI y generación procedimental de edificios.
- Redes de flujo (agua, electricidad, aguas residuales).

#### Dinámicas
- Tráfico como antagonista emergente.
- Olas de muerte por sincronización demográfica.
- Gestión de fluidos con consecuencias físicas.

#### Estéticas
- Expression, Discovery y Sensation ("ant farm" voyeurístico).

#### Análisis de ingeniería
Límites de performance y optimizaciones (hard caps, pathfinding determinista) para mantener simulación en tiempo real.

### Puzle — Portal 2 (Valve)

**Motor:** Source Engine

#### Mecánicas
- Dispositivo de portales: conservación del momento (||v_in|| = ||v_out||).
- Elementos deterministas: cubos, botones, gels, láseres.

#### Dinámicas
- Aprendizaje iterativo — tutorización invisible.
- Recontextualización espacial (pensar en 4D topológica).
- Emergencia en speedrunning por exploits del motor.

#### Estéticas
- Challenge, Narrative y Sensation: satisfacción intelectual y humor negro.

#### Análisis de ingeniería
Necesidad de un motor de física consistente y robusto para evitar glitches en topologías dinámicas.

## Tabla comparativa MDA

| Característica | Acción (DMC5) | Aventura (BotW) | RPG (BG3) | Estrategia (Civ VI) | Simulación (Cities) | Puzle (Portal 2) |
|---|---:|---:|---:|---:|---:|---:|
| Mecánica central (M) | Combos, cancelación, medidor estilo | Motor de química, física, escalada | Tiradas d20, diálogo condicional | Rejilla hex, turnos, adyacencia | Agentes (Cims), zonificación RCI | Portales, conservación de momento |
| Bucle core | Combatir → Calificar → Mejorar | Explorar → Resolver → Mejorar | Explorar/Dialogar → Combatir → XP | Explorar → Expandir → Explotar → Turno | Zonificar → Observar → Resolver → Crecer | Entrar → Observar → Resolver → Salir |
| Dinámica clave (D) | Optimización estética, agresión constante | Jugabilidad multiplicativa, emergencia | Narrativa emergente, save-scumming | Snowballing, "un turno más" | Tráfico como antagonista, olas de muerte | Recontextualización espacial |
| Estética primaria (A) | Expresión / Sensación / Desafío | Discovery / Fantasy | Narrative / Expression | Challenge / Fantasy | Expression / Discovery | Challenge / Narrative |

## Análisis comparativo y ensayo crítico

### Diferencias: Acción (DMC5) vs. Estrategia (Civ VI)
- Frecuencia vs profundidad: DMC5 opera en milisegundos (input, latencia, frame-precisión). Civ VI opera en turnos (planificación a largo plazo).
- Implementación técnica: DMC5 optimiza latencia y sensibilidad de input; Civ VI optimiza IA y gestión de datos.

### Similitudes: Polimorfismo de mecánicas (Gestión de recursos)
- Ambos géneros comparten la abstracción "gestión de recursos"; su implementación cambia la dinámica y estética (ej. DT en DMC5 vs Oro en Civ VI).

### Híbridos: Convergencia Aventura — RPG
- Modernamente los géneros tienden a hibridarse: BotW incorpora sistemas RPG (armas, buffs), BG3 incorpora física y exploración propia de aventuras. Los motores deben soportar simulación física y persistencia de datos.

## Conclusión

El análisis MDA muestra que la diversión es el resultado de decisiones de ingeniería concretas. Mecánicas bien diseñadas generan dinámicas emergentes que, a su vez, producen estéticas específicas. Los títulos más exitosos son aquellos que permiten emergencias robustas y coherencia lógica del mundo.

## Referencias y notas

- Hunicke, LeBlanc & Zubek — MDA framework.
- Citados: Devil May Cry 5, Breath of the Wild, Baldur's Gate 3, Civilization VI, Cities: Skylines, Portal 2.

---

