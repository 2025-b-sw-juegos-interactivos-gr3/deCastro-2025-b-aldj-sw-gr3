# Taller El Diseño de Doble Propósito

**Tema:** El Diseño de Doble Propósito

**Asignatura:** DESARROLLO DE JUEGOS INTERACTIVOS (ISWD823)  
**Programa:** Ingeniería de Software  
**Estudiante:** Aiden de Castro 
**Fecha:** Diciembre 2025 
**Docente:** Ing. Adrian Eguez

---

## 1. Marco Conceptual: Diseño Orientado a Stakeholder y Arquitectura Teleológica de Sistemas Lúdicos

La ingeniería de software contemporánea aplicada al dominio del desarrollo de videojuegos enfrenta un desafío epistemológico fundamental: la naturaleza de los *requisitos funcionales* está subordinada no a especificaciones técnicas, sino a la identidad del stakeholder y su métrica axiológica de valor. En términos formales, el diseño de un sistema lúdico-interactivo no parte de la pregunta "*¿qué debe hacer el sistema?*", sino de "*¿para quién existe el sistema y qué objetivo operacionalizable debe cumplir?*"

Esta distinción no es semántica; es arquitectural. Un mismo *core mechanic* (mecánica nuclear) puede instanciarse en dos sistemas cuyas arquitecturas de experiencia (Experience Architecture) divergen completamente según la función teleológica que cumplan. Consideremos el contraste:

En sistemas lúdicos de entretenimiento comercial, el stakeholder primario es el consumidor masivo dentro de un mercado competitivo. La función de utilidad del sistema se maximiza optimizando variables de engagement económico: DAU/MAU (Daily/Monthly Active Users), LTV (Lifetime Value), ARPDAU (Average Revenue Per Daily Active User), conversion rate hacia monetización, y viralidad medida por K-factor. La experiencia estética (según el framework MDA: Mechanics, Dynamics, Aesthetics) está diseñada para maximizar *retención conductual* mediante arquitecturas de recompensa variable intermitente, bucles de compulsión, y economías de escasez artificial. El diseño está subordinado a la lógica del capitalismo de atención: capturar tiempo cognitivo y convertirlo en flujo de caja recurrente.

En sistemas lúdicos serios (serious games), el stakeholder primario es una entidad institucional (sector salud, educación, defensa, corporativo) que invierte en el sistema como tecnología de cambio conductual. La función de utilidad se maximiza optimizando variables de impacto pedagógico o procedimental: transferencia de aprendizaje a contextos reales (transfer of training), retención de conocimiento en evaluaciones post-intervención, reducción de errores operacionales en métricas longitudinales, mejora en adherencia a protocolos estandarizados, y ROI (Return on Investment) medido en términos de reducción de costos por incompetencia o litigio. La experiencia está diseñada para maximizar *fidelidad procedimental* (procedural fidelity) y *validez ecológica* (ecological validity), subordinándose a la lógica del cognitivismo aplicado: estructurar andamiaje cognitivo (cognitive scaffolding) que transforme esquemas mentales.

La hipótesis central del presente análisis es que estas dos arquitecturas teleológicas son *estructuralmente incompatibles*: optimizar para una función de utilidad necesariamente degrada la otra. Un sistema no puede simultáneamente maximizar monetización mediante fricción artificial y maximizar aprendizaje mediante autenticidad procedimental. Esta tensión constituye el problema de diseño fundamental que articula el presente trabajo.

---

## 2. Concepto Núcleo: Sistema de Simulación de Operaciones Prehospitalarias

**Título Proyecto:** *Dispatch* - Sistema Dual de Simulación de Transporte Médico de Emergencia

**Mecánica Nuclear (Core Mechanic):** Gestión de transporte sanitario urgente bajo restricciones temporales, espaciales y procedimentales. El agente (jugador) opera como conductor-paramédico responsable de la cadena de supervivencia prehospitalaria: desde el dispatch inicial hasta la transferencia hospitalaria, navegando topologías urbanas variables bajo condiciones estocásticas de tráfico, urgencia clínica y protocolos operacionales.

**Dominio del Problema:** El sistema modela el *Emergency Medical Services (EMS) workflow*, donde la variable dependiente crítica es el *response time* (tiempo de respuesta) y la *patient outcome probability* (probabilidad de resultado favorable del paciente), mediados por decisiones de navegación, adherencia a protocolos de seguridad vial, y evaluación clínica básica en campo.

**Espacio de Estados:** El jugador navega un grafo de decisiones donde cada nodo representa una elección (ruta, velocidad, protocolo) y cada arista tiene costos asociados (tiempo, riesgo, adherencia normativa). El sistema diverge en dos implementaciones con funciones de costo radicalmente opuestas: una arquitectura arcade que penaliza tiempo absoluto (maximizar velocidad), y una arquitectura procedimental que penaliza desviación de best practices (maximizar adherencia a Standard Operating Procedures).

---

## 3. Análisis Comparativo: Arquitecturas de Sistema Divergentes

| **Característica de Diseño** | **Versión 1: Juego de Entretenimiento** | **Versión 2: Juego Serio** |
|---|---|---|
| **Título (Sugerido)** | "Ambulance Chaos Tycoon" / "Emergency Rush" | "Dispatch: Simulador de Operaciones de Emergencia" |
| **Estética MDA (Propósito)** | **Mecánica:** Conducción arcade con dinámicas de colisión tolerante, tiempos de entrega como métrica principal. **Dinámmica:** Caos controlado, presión temporal acelerada, recompensas inmediatas. **Estética:** Fantasía (ser un héroe arriesgado), Desafío (gestionar rutas bajo presión), Expresión (customizar ambulancia). | **Mecánica:** Simulación realista con físicas precisas, protocolos procedimentales integrados. **Dinámica:** Predictibilidad controlada, rigor en la toma de decisiones, consecuencias realistas. **Estética:** Maestría (dominar procedimientos), Desafío (adherencia a protocolos bajo estrés), Descubrimiento (aprendizaje de mejores prácticas). |
| **Bucle de Juego (Core Loop)** | 1. **Recibir llamada** → 2. **Acelerar (ignorar tráfico/peatones)** → 3. **Recoger paciente** → 4. **Ignorar límites de velocidad** → 5. **Llegar al hospital** → 6. **Ganar dinero + puntos de experiencia** → 7. **Desbloquear mejoras (neumáticos turbo, colores, aceleración)** → 8. **Completar misiones especiales para pase de batalla**. | 1. **Recibir llamada** → 2. **Activar protocolos de seguridad (cinturón, verificación de equipo)** → 3. **Navegar respetando señales de tráfico** → 4. **Evaluar estado del paciente (vitales, triaje)** → 5. **Comunicarse con hospital (ETA, datos críticos)** → 6. **Conducir con precaución hacia destino** → 7. **Documentar incidente y evaluación** → 8. **Recibir feedback sobre adherencia a protocolo**. |
| **Modelo de Negocio / Financiación** | **Free-to-Play (F2P) con Monetización Agresiva.** Financiado por microtransacciones, pases de batalla de temporada, y contenido DLC (nuevos mapas, vehículos especiales). Modelo de retención: crear "puntos de fricción" que incentiven compras. | **B2B por Licencia Anual / Licitación Institucional.** Vendido a hospitales, institutos de formación en emergencias médicas y cuerpos de bomberos como módulo de capacitación y certificación. No aplica monetización en jugador final; el "retorno" es la reducción de errores operacionales y mejora en estándares de seguridad. |
| **Mecánicas de Monetización** | 1. **Gemas Premium:** Comprar aceleración de cooldowns, extender gasolina, revivir misiones fallidas. 2. **Pases de Batalla (Temporada 8 semanas):** Desbloquear diseños de ambulancias exclusivos, sirenas personalizadas, accesorios interiores. 3. **Loot Boxes:** Cajas de botín tras misiones exitosas con probabilidades variables (cosmética rara/común). 4. **Battle Pass Gratuito + Premium:** El pase básico ofrece progresión lenta; el premium acelera obtención de recompensas. 5. **DLC de Mapas:** Nuevos escenarios urbanos con mecánicas especiales (destrucción ambiental, zonas de desastre). | No aplica. El "ingreso" para la institución cliente es indirecto: reducción de costos de litigio por error operacional, mejora documentada en eficiencia de respuesta, certificación de competencia personal. El software es un bien de capital, no un servicio recurrente con microcompras. |
| **Mecánicas de Ludificación (Gamificación)** | 1. **Puntos/Moneda in-game:** Dinero ganado por rapidez en entregas (incentiva velocidad irresponsable). 2. **Sistema de Niveles:** Progresión visual con hito cada 10 entregas (FOMO). 3. **Leaderboards Globales:** Clasificación por dinero ganado en temporada (competencia social). 4. **Insignias Cosméticas:** "Temerano", "Piloto Caótico", "Chocador Serial" (refuerza identidad de riesgo). 5. **Recompensas Variables (RNG):** Loot boxes tras misiones para mantener engagement impredecible. 6. **Streak Bonuses:** Cadenas de misiones exitosas generan multiplicadores de dinero (presión psicológica para continuar jugando). | 1. **Insignias de Competencia:** "Protocolo de Triaje Dominado", "Comunicaciones Efectivas", "Manejo Deficitario Resuelto" (refuerza dominio procedimental). 2. **Barras de Progreso por Módulo:** Visualización clara de compleción de temas (higiene en emergencias, ACLS básico, comunicación radio). 3. **Feedback Inmediato Correctivo:** Errores generan alertas visuales/auditivas con explicación procedimental (ej: "Has excedido velocidad permitida en zona escolar: riesgo de cohesión aumentado 40%"). 4. **Sistema de Certificación Escalado:** Niveles de certificación (Básico → Intermedio → Experto) con exámenes integrados. 5. **Análisis de Desempeño Post-Misión:** Reporte detallado de adherencia a protocolo, tiempos de respuesta, errores evitados. 6. **Competencia Intra-institucional (opcional):** Leaderboards por hospital/equipo, pero con métricas de "seguridad y precisión", no "velocidad". |
| **Métrica de Éxito (KPI)** | 1. **Retención (D7, D30, D90):** % de usuarios que retornan a día 7, 30, 90. Target: >35% D7. 2. **ARPDAU (Average Revenue Per Daily Active User):** Ingreso promedio por usuario activo diario. Target: $0.80-$1.20 ARPDAU. 3. **Conversión al Pase de Batalla:** % de F2P que compran pase. Target: 3-5%. 4. **LTV (Lifetime Value):** Ingresos totales por usuario a lo largo de vida. Target: $15-$25 LTV. 5. **Viral Coefficient:** Promedio de nuevos usuarios invitados por usuario existente. Target: >1.2. 6. **Sesiones/Día:** Promedio de sesiones de juego por usuario. Target: >2.5 sesiones/día. | 1. **Tasa de Compleción del Módulo:** % de alumnos que finalizan el programa. Target: >90%. 2. **Mejora Pre-Test vs. Post-Test:** Diferencia de puntuación en examen de certificación antes vs. después. Target: mejora de 25-40 puntos. 3. **Retención de Conocimiento (3 meses):** Re-evaluación a los 3 meses para medir retención. Target: >80% de puntuación mantenida. 4. **Adherencia a Protocolo (In-Situ):** Auditorías en campo observando cumplimiento de procedimientos tras capacitación. Target: >85% cumplimiento. 5. **Reducción de Incidentes:** Tasa de errores operacionales documentados pre vs. post capacitación. Target: reducción de 30-50%. 6. **ROI Institucional:** Costo del software dividido entre ahorros por reducción de litigio/errores. Target: ROI >200% en 2 años. |

---

## 4. Análisis de Dependencias Estructurales entre Modelo de Negocio y Arquitectura Mecánica

### Economía F2P y Diseño de Fricción Intencional: Arquitectura de Monetización como Constraint de Sistema

El modelo F2P impuso restricciones que se transformaron en pilares del diseño. Específicamente:

1. **Creación Deliberada de Fricción Temporal:** El bucle base se diseñó con tiempos de "cooldown" (esperas entre misiones). Sin aplicar inversión monetaria, un jugador puede esperar 15 minutos para la siguiente misión. Las Gemas Premium aceleran este cooldown a 2 minutos. **Esta fricción no es accidental; es por diseño.** Sin ella, el F2P colapsaría: el jugador completaría todo contenido en 12 horas sin necesidad de revisitar. La "fricción" es el combustible que hace deseables las MTX.

2. **Monetización de la Progresión:** El sistema de niveles y desbloqueos se aceleró intencionalmente. Alcanzar el nivel máximo en F2P requiere ~150 horas. En Premium (con Pases de Batalla), 40 horas. Este delta crea FOMO (Fear of Missing Out): si no compras el pase, "pierdes" cosmética exclusiva.

3. **Recompensas Variables como Motor de Engagement:** Las Loot Boxes tras misiones se diseñaron específicamente para explotar la psicología de recompensa variable intermitente (principio de Skinner). La probabilidad de obtener cosmética "rara" es 2%, lo que genera engagement psicológico adictivo e impulsa re-intentos y compras de "rolls" adicionales.

4. **Streaks y Presión Psicológica:** Los bonificadores de cadenas de misiones exitosas (100% → 150% de dinero en cadena de 5 misiones) generan ansiedad: si pierdes una misión, pierdes el multiplicador. Esto crea presión para "jugar una más", alargando sesiones y exponiendo al jugador a más puntos de conversión.

**Síntesis:** El modelo F2P no constituye una capa de monetización aplicada post-diseño; representa un *meta-constraint arquitectural* que redefine completamente el espacio de diseño válido. La economía F2P requiere la construcción deliberada de "pain points" (puntos de dolor) sistémicos—esperas artificiales, progresión asintótica, escasez de recursos—que crean *perceived value* (valor percibido) para las MTX. Estos constraints generan un diseño sub-óptimo desde la perspectiva de user experience pura, pero óptimo desde la función objetivo de maximización de ARPDAU. La viabilidad comercial del F2P depende estructuralmente de la existencia de estas fricciones: eliminarlas colapsa el modelo de negocio.

### Validez Ecológica y Eliminación de Affordances Lúdicas: Diseño Procedimental como Constraint Epistémico

El propósito pedagógico introdujo restricciones estructurales que refundaron el diseño:

1. **Eliminación de la Tolerancia de Colisión:** En la Versión 1 (Entretenimiento), chocar contra vehículos civiles es una mecánica aceptada; genera "caos divertido". En la Versión 2, esto es **inaceptable pedagógicamente**. Las colisiones innecesarias violarían protocolos reales, entrenarían incompetencia y crearían aprendizaje espurio. Se eliminó esta mecánica. Ahora, golpear un vehículo civil genera penalización en puntuación y feedback negativo (incidente documentado).

2. **Restricción de Velocidad Contextual:** La Versión 1 premia la velocidad máxima. La Versión 2 introduce zonas de restricción de velocidad (escolares, residenciales) donde exceder límites genera penalización y feedback procedimental. Esto es "menos divertido" arcade, pero es **esencial** para entrenar juicio contextual real.

3. **Introducción de Protocolos Procedimentales Explícitos:** La Versión 1 omite procedimientos: solo "recoge y entrega". La Versión 2 requiere:
   - Verificación de seguridad del vehículo (pre-misión)
   - Evaluación de triaje del paciente (en escena)
   - Comunicación de datos vitales al hospital (en ruta)
   - Documentación post-entrega
   
   Estos no son "más divertidos", pero son **estructuralmente necesarios** para que el aprendizaje sea transferible al contexto real.

4. **Eliminación de "Poder-ups" Arcade:** La Versión 1 incluye "neumáticos turbo" desbloqueables que multiplican velocidad. Estos no tienen equivalente realista. En la Versión 2, se eliminan completamente. El "progreso" no es velocidad, sino competencia procedimental.

5. **Realismo en Consecuencias:** En la Versión 1, los errores son inconvenientes (pierdes dinero). En la Versión 2, los errores tienen **consecuencias realistas documentadas:**
   - Exceso de velocidad → Mayor riesgo de accidente (simulado: posibilidad de fallo en ruta)
   - Omisión de triaje → Paciente llega en peor estado (feedback visual/estadístico)
   - Comunicación incorrecta → Hospital no preparado (misión falla)

**Síntesis:** La arquitectura de juegos serios impone un *fidelity constraint* (restricción de fidelidad) que subordina el diseño a la validez ecológica del dominio simulado. Mecánicas lúdicas que violen protocolos reales—colisiones tolerantes, aceleración no realista, omisión de procedimientos—generan *negative transfer* (transferencia negativa): el aprendizaje en el entorno simulado interfiere con el desempeño en el entorno real. Por tanto, el diseño serio requiere la eliminación sistemática de affordances arcade que contradicen best practices del dominio. Esta eliminación reduce la "flow experience" (experiencia de flujo) en sentido csikszentmihalyiano, pero maximiza la *instructional validity* (validez instruccional). El trade-off es estructural: no se puede optimizar simultáneamente para diversión arcade y para transferencia de aprendizaje cuando ambas requieren arquitecturas mecánicas incompatibles.

### Ludificación como Mecanismo Dual: Motivación Extrínseca vs. Andamiaje Cognitivo

Las estructuras de ludificación (puntos, insignias, leaderboards, feedback loops) constituyen *isomorphic mechanisms* (mecanismos isomórficos) cuya función depende completamente del sistema objetivo en que se insertan:

| **Mecánica** | **Versión 1 (Entretenimiento)** | **Versión 2 (Serio)** | **Divergencia de Propósito** |
|---|---|---|---|
| **Puntos/Moneda** | **Dinero ganado por rapidez.** Propósito: Motivación extrínseca. Diseño: Mayor velocidad = más dinero. Efecto: Incentiva comportamiento de riesgo (velocidad irresponsable). Psicología: Activar dopamina del "lucro" (motivación extrínseca). | **Dinero no existe; reemplazado por "Puntuación de Protocolo" (0-100%).** Propósito: Refuerzo de precisión. Diseño: Adherencia a protocolo = puntuación alta. Efecto: Incentiva rigor procedimental y seguridad. Psicología: Activar satisfacción de "dominio" (motivación intrínseca). | **Misma mecánica superficial (acumular puntos), pero operan sobre motivaciones psicológicas opuestas:** F2P externaliza motivación (dinero como proxy de estatus); Serio internaliza motivación (dominio técnico como satisfacción). |
| **Insignias/Badges** | "Temerano", "Piloto Caótico", "Chocador Serial". Propósito: Identidad de personaje arriesgado. Psicología: Explotar necesidad de estatus social ("soy el jugador más atrevido"). Efecto: Celebra comportamiento irresponsable, refuerza engagement de riesgo. | "Protocolo de Triaje Dominado", "Comunicación Efectiva", "Manejo de Emergencia Cardíaca". Propósito: Certificación de competencia. Psicología: Explotar necesidad de competencia reconocida ("soy técnicamente competente"). Efecto: Celebra aprendizaje, refuerza adherencia a estándares. | **Mismo mecanismo (reconocimiento visual), pero celebran valores opuestos.** F2P premia "audacia"; Serio premia "precisión". |
| **Leaderboards** | Clasificación global por dinero acumulado. Propósito: Competencia social viral. Psicología: Necesidad de dominancia social (estar en top 10 global). Efecto: Incentiva juego acelerado, MTX competitivo ("compro pase para estar en top"). Monetización: El leaderboard se convierte en **herramienta de venta** (FOMO social). | Leaderboards intra-institucionales (hospital/equipo) por "Puntuación de Seguridad". Propósito: Competencia colegiada, no social. Psicología: Necesidad de reconocimiento pares (estar en top dentro de mi equipo). Efecto: Incentiva precisión, fomenta cultura de seguridad institucional. Monetización: N/A (no hay). |
| **Recompensas Variables (RNG)** | **Loot Boxes:** Cajas con probabilidades. Propósito: Explotar psicología de "slot machine". Diseño: 2% rara, 18% común. Efecto: Engagement adictivo, impulsividad de compra ("siguiente roll quizá sea raro"). Psicología: Explotar cerebro para deseo variable intermitente (Schedules de Reforzamiento). Monetización: **Directa:** Compras de rolls adicionales generan 40-60% de ingresos. | **Feedback Inmediato Correctivo:** Errores generan alertas con explicaciones procedimentales. Propósito: Refuerzo de error (learning sciences). Diseño: Error → Alerta visual → Explicación → Oportunidad de re-intento. Efecto: Aprendizaje acelerado, retención de correcciones. Psicología: Explotar neuroplasticidad y aprendizaje por corrección. Monetización: N/A. |

**Síntesis Teórica:** La ludificación no constituye un conjunto neutro de herramientas; opera como *purpose amplifier* (amplificador de propósito) cuyo efecto depende del sistema objetivo. En arquitecturas F2P, la ludificación implementa *operant conditioning* (condicionamiento operante) bajo schedules de reforzamiento variable (Skinner) para maximizar engagement conductual y conversión monetaria. La psicología operante aquí explota necesidades de estatus social, aversión a pérdida (loss aversion), y FOMO (fear of missing out) para generar gasto impulsivo. En arquitecturas pedagógicas, la misma estructura implementa *mastery learning frameworks* (marcos de aprendizaje por dominio) y *formative assessment* (evaluación formativa continua), donde el feedback inmediato opera como correctivo cognitivo que facilita la formación de *mental models* (modelos mentales) precisos. 

La paradoja: mecanismos estructuralmente idénticos (puntos acumulativos, reconocimiento visual) generan outcomes psicológicos opuestos según su embedding contextual. En F2P, externalizan motivación (reducir autonomía, aumentar dependencia de recompensas extrínsecas). En sistemas serios, internalizan competencia (aumentar autonomía mediante dominio procedimental certificado). Esta divergencia evidencia que la ludificación no es "buena" o "mala" per se; es *teleologically ambiguous* (teleológicamente ambigua), adquiriendo valencia moral según la función objetivo del sistema hospedador.

---

## 5. Conclusiones: Arquitectura Teleológica como Determinante Estructural del Diseño de Sistemas Lúdicos

El análisis comparativo del sistema *Dispatch* evidencia una tesis central en la ingeniería de software aplicada a dominios lúdicos: **un concepto mecánico nuclear (core concept) no define un sistema; la función teleológica define el sistema**. Dos implementaciones que comparten la misma ontología superficial ("transportar pacientes en ambulancia") divergen completamente en su arquitectura de experiencia, economía, mecánicas de refuerzo y métricas de éxito cuando sus funciones objetivo son estructuralmente incompatibles.

**Versión Entretenimiento ("Ambulance Chaos Tycoon"):** Implementa una arquitectura de economía de atención donde el engagement conductual se maximiza mediante diseño de fricción intencional, schedules de reforzamiento variable, y FOMO sistémico. Los protocolos reales son constraints a violar (fuente de "diversión transgresiva"). Success function: $S = f(D7\_retention, ARPDAU, LTV)$.

**Versión Seria ("Dispatch: EMS Simulator"):** Implementa una arquitectura de fidelidad procedimental donde la transferencia de aprendizaje se maximiza mediante validez ecológica, feedback correctivo inmediato, y andamiaje cognitivo estructurado. Los protocolos reales son el contenido instruccional (objetivo de internalización). Success function: $S = f(\Delta_{competence}, transfer\_validity, adherence\_improvement)$.

La incompatibilidad no es accidental sino estructural: optimizar la primera función necesariamente degrada la segunda, y viceversa. Un sistema no puede simultáneamente maximizar monetización mediante fricción artificial *y* maximizar aprendizaje mediante autenticidad procedimental sin colapsar en incoherencia.

**Implicación para la praxis profesional:** El diseño de sistemas lúdicos no comienza con la pregunta "¿qué mecánicas implementamos?", sino con "¿qué función objetivo optimizamos y para qué stakeholder?". Esta decisión subordina completamente todas las decisiones subsecuentes: modelo de negocio, arquitectura de bucles, sistemas de refuerzo, métricas de evaluación y criterios de validación. La ingeniería de videojuegos, correctamente comprendida, es ingeniería de funciones objetivo operacionalizadas mediante arquitecturas de experiencia coherentes. El presente análisis demuestra que la coherencia teleológica—la alineación rigurosa entre propósito declarado y arquitectura implementada—constituye el criterio de calidad fundamental en el diseño de sistemas lúdicos profesionales.

---

**Entregable Completado:** Ficha de Diseño Dual + Análisis Comparativo  
**Profesor/Revisor:** [A completar por estudiante/docente]  
**Fecha de Entrega:** Diciembre 2025

