# PROJECT MANAGEMENT - PHOBIA
## Planificación Ágil y Gestión de Tareas

---

## **I. ESTRUCTURA GENERAL DEL PROYECTO**

**Duración Total:** 20 semanas (~5 meses)  
**Equipo:** 4-6 personas (1 Lead, 1 Programmer, 1 Narrative Designer, 1 Artist, 1 Audio, 1 QA)  
**Metodología:** Scrum (Sprints de 2 semanas)  
**Herramienta Recomendada:** GitHub Projects (integrado con repo), Trello o Jira

---

## **II. ÉPICAS Y DESGLOSE**

### **ÉPICA 1: Gestión e Investigación Inicial** ⏱️ 2 semanas
**Objetivo:** Validar concepto, establecer documentación base, preparar equipo

#### User Stories:

**US-1.1:** Como productor, necesito un GDD completo para validar el scope
- Tarea: Redactar GDD (¡HECHO! ✓)
- Estimación: 40 horas
- Responsable: Game Designer Lead
- Criterios de aceptación:
  - [ ] Concepto narrativo claro
  - [ ] Mecánicas definidas
  - [ ] Análisis MDA completo
  - [ ] Referencias visuales incluidas

**US-1.2:** Como artista, necesito referencias visuales para el apartamento
- Tarea: Crear moodboard de paleta de colores, inspiración visual
- Estimación: 16 horas
- Responsable: Art Director
- Criterios de aceptación:
  - [ ] 10+ imágenes de referencia
  - [ ] Paleta de colores por acto
  - [ ] Inspiración de UI mockups

**US-1.3:** Como programador, necesito la arquitectura técnica definida
- Tarea: Diagrama UML, stack tecnológico, patrones de diseño
- Estimación: 20 horas
- Responsable: Lead Programmer
- Criterios de aceptación:
  - [ ] Diagrama de clases completado
  - [ ] Patrones de diseño documentados
  - [ ] Stack decidido (Godot 4.x)

**US-1.4:** Como sound designer, necesito paleta de audio definida
- Tarea: Referenciar música, crear lista de SFX necesarios
- Estimación: 12 horas
- Responsable: Audio Director
- Criterios de aceptación:
  - [ ] 5+ referencias de compositores
  - [ ] 30+ efectos de sonido catalogados
  - [ ] Briefing de doblaje preparado

---

### **ÉPICA 2: Configuración Técnica y Pipeline** ⏱️ 1 semana
**Objetivo:** Establecer repositorio, workflow, herramientas de desarrollo

#### User Stories:

**US-2.1:** Como desarrollador, necesito un repositorio configurado con estructura base
- Tarea: Inicializar proyecto Unity, carpetas de assets, configuración de Git LFS
- Estimación: 8 horas
- Responsable: Lead Programmer

**US-2.2:** Como QA, necesito un sistema de bug tracking
- Tarea: Configurar GitHub Issues, labels, templates
- Estimación: 4 horas
- Responsable: QA Lead

---

### **ÉPICA 3: Core Gameplay Loop** ⏱️ 4 semanas
**Objetivo:** Implementar mecánica central: exploración, detección de pistas, encuentros con entidades

#### User Stories:

**US-3.1:** Como jugador, necesito controlar al protagonista en el apartamento
- Tarea: Implementar movimiento (WASD, Click-to-move), colisiones
- Estimación: 20 horas
- Responsable: Programmer
- Criterios de aceptación:
  - [ ] Movimiento fluido 60 FPS
  - [ ] Detección de colisiones funcional
  - [ ] Cámara follow smooth

**US-3.2:** Como jugador, necesito encontrar pistas de realidad anomalías
- Tarea: Sistema de interacción, recolecta de pistas, UI contador
- Estimación: 24 horas
- Responsable: Programmer
- Criterios de aceptación:
  - [ ] 5 pistas interactuables
  - [ ] Animaciones de recolecta
  - [ ] Contador UI funcional

**US-3.3:** Como jugador, necesito refugiarme en zonas seguras
- Tarea: Sistema de sanidad, regeneración en dormitorio/baño
- Estimación: 16 horas
- Responsable: Programmer
- Criterios de aceptación:
  - [ ] Barra de sanidad visible
  - [ ] Regeneración en zonas seguras
  - [ ] Drain en zonas peligrosas

**US-3.4:** Como jugador, necesito encontrar una entidad amenazante
- Tarea: Prototipo de enemigo, AI básica (seguimiento simple)
- Estimación: 32 horas
- Responsable: Programmer + Artist (modelo simple)
- Criterios de aceptación:
  - [ ] Enemigo visible y animado
  - [ ] Sigue al jugador cuando está cerca
  - [ ] Daña sanidad al detectar

---

### **ÉPICA 4: Sistema de Tests Psicológicos** ⏱️ 3 semanas
**Objetivo:** Implementar tests adaptativos que modulan la experiencia

#### User Stories:

**US-4.1:** Como jugador, necesito responder screening inicial (5 preguntas)
- Tarea: UI de test, lógica de respuestas, almacenamiento
- Estimación: 20 horas
- Responsable: Programmer + UI Designer
- Criterios de aceptación:
  - [ ] Test con 5 preguntas
  - [ ] Respuestas guardadas en JSON
  - [ ] Transición fluida

**US-4.2:** Como jugador, necesito responder Test de Beck (20 preguntas)
- Tarea: Test completo con scoring, análisis de síntomas
- Estimación: 28 horas
- Responsable: Programmer + Narrative Designer
- Criterios de aceptación:
  - [ ] 20 preguntas funcionales
  - [ ] Scoring automático (0-63)
  - [ ] Perfil de fobias generado

**US-4.3:** Como sistema, necesito adaptar enemigos según perfil psicológico
- Tarea: Algoritmo de spawning adaptativo, tipos de enemigos
- Estimación: 40 horas
- Responsable: Programmer
- Criterios de aceptación:
  - [ ] Aracnofobia → Arañas gigantes
  - [ ] Fobia social → Multitud de espectros
  - [ ] Otros arquetipos funcionales

**US-4.4:** Como jugador, necesito test final decisivo
- Tarea: Test final (1 pregunta crítica), bifurcación de ending
- Estimación: 16 horas
- Responsable: Programmer + Narrative Designer
- Criterios de aceptación:
  - [ ] Test funcional
  - [ ] YES → Good Ending
  - [ ] NO → Bad Ending

---

### **ÉPICA 5: Sistema de Diálogos Adaptativos** ⏱️ 3 semanas
**Objetivo:** Crear árbol de diálogos que responda a personalización del jugador

#### User Stories:

**US-5.1:** Como jugador, necesito seleccionar mi nombre y profesión al inicio
- Tarea: Pantalla de creación de personaje, almacenamiento de datos
- Estimación: 12 horas
- Responsable: Programmer + UI Designer

**US-5.2:** Como jugador, necesito dialogar con mi terapeuta (Dr. Krell)
- Tarea: Sistema de diálogos, cinemáticas de llamadas telefónicas
- Estimación: 36 horas
- Responsable: Narrative Designer + Programmer
- Criterios de aceptación:
  - [ ] 15+ líneas de diálogo adaptativas
  - [ ] Diálogos varían según profesión
  - [ ] Reacciona a salud mental del jugador

**US-5.3:** Como jugador, escucho susurros y fragmentos de voz durante encuentros
- Tarea: Audio implícito (no texto), generador de diálogos fragmentados
- Estimación: 20 horas
- Responsable: Audio Director + Programmer

---

### **ÉPICA 6: Narrativa y Cinemáticas** ⏱️ 4 semanas
**Objetivo:** Implementar estructura narrativa con dos finales

#### User Stories:

**US-6.1:** Como narrador, necesito Acto I con introducción clara
- Tarea: Cinemática de apertura, primeros diálogos, ambiente
- Estimación: 28 horas
- Responsable: Narrative Designer + Cinematics Artist

**US-6.2:** Como narrador, necesito Acto II con escalada de tensión
- Tarea: Progresión de anomalías, encuentros frecuentes, revelaciones
- Estimación: 32 horas
- Responsable: Narrative Designer + Programmer

**US-6.3:** Como narrador, necesito Acto III con bifurcación
- Tarea: Acto final hacia dos caminos distintos
- Estimación: 24 horas
- Responsable: Narrative Designer

**US-6.4:** Como jugador, necesito final "Bueno" (Despertar en Hospital)
- Tarea: Cinemática de awakening, diálogos de esperanza, créditos
- Estimación: 20 horas
- Responsable: Cinematics Artist + Voice Actor
- Criterios de aceptación:
  - [ ] Cinemática de 5 minutos
  - [ ] Voz del doctor reveladora
  - [ ] Música esperanzadora

**US-6.5:** Como jugador, necesito final "Malo" (Descubrir Suicidio / Loop)
- Tarea: Cinemática de terraza, visualización de propio cuerpo, loop infinito
- Estimación: 20 horas
- Responsable: Cinematics Artist + Audio Designer
- Criterios de aceptación:
  - [ ] Cinemática aterradora de 5 minutos
  - [ ] Loop mecánico implementado
  - [ ] Audio de horror maximizado

---

### **ÉPICA 7: Arte, Animación y Audio** ⏱️ 4 semanas
**Objetivo:** Crear assets visuales y sonoros de producción

#### User Stories:

**US-7.1:** Como artista, necesito modelar el apartamento (3D low-poly)
- Tarea: Modelado 3D, UVs, texturas
- Estimación: 80 horas
- Responsable: 3D Artist

**US-7.2:** Como artista, necesito animar al protagonista y enemigos
- Tarea: Rigging, animaciones de movimiento, interacción
- Estimación: 60 horas
- Responsable: Animator

**US-7.3:** Como artista, necesito efectos visuales (distorsión, glitch, vignette)
- Tarea: Shaders personalizados, post-processing
- Estimación: 40 horas
- Responsable: Technical Artist

**US-7.4:** Como audio designer, necesito música original o licensed
- Tarea: Composición/Licencias de 8 tracks, integración en engine
- Estimación: 120 horas (composición) o 20 horas (licencias)
- Responsable: Composer

**US-7.5:** Como audio designer, necesito SFX variados y 3D spatial audio
- Tarea: Grabación/síntesis de 40+ efectos, integración con Wwise/FMOD
- Estimación: 60 horas
- Responsable: Audio Designer

**US-7.6:** Como voice director, necesito doblaje de Dr. Krell y voz del juego
- Tarea: Casting, grabación, post-producción de audio
- Estimación: 24 horas (dirección) + 40 horas (actor)
- Responsable: Voice Director + Voice Actor

---

### **ÉPICA 8: UI/UX y Polish** ⏱️ 2 semanas
**Objetivo:** Pulir interfaz, hacer juego intuitivo y accesible

#### User Stories:

**US-8.1:** Como jugador, necesito menú principal limpio e inmersivo
- Tarea: Diseño de menu, animaciones, transiciones
- Estimación: 20 horas
- Responsable: UI Designer + Programmer

**US-8.2:** Como jugador, necesito HUD minimalista durante gameplay
- Tarea: Indicadores de sanity, pistas, amenaza
- Estimación: 16 horas
- Responsable: UI Designer

**US-8.3:** Como jugador con daltonismo, necesito modo colorblind
- Tarea: Paleta alternativa, toggle en opciones
- Estimación: 12 horas
- Responsable: UI Designer

**US-8.4:** Como jugador sordo/hipoacúsico, necesito subtítulos
- Tarea: Sistema de subtítulos, sincronización con audio
- Estimación: 20 horas
- Responsable: Programmer

**US-8.5:** Como jugador, necesito opciones de accesibilidad avanzada
- Tarea: Reducir fotosensibilidad, remapping controles, tamaño texto
- Estimación: 24 horas
- Responsable: Programmer + UI Designer

---

### **ÉPICA 9: QA y Balanceo** ⏱️ 2 semanas
**Objetivo:** Testing exhaustivo, balanceo de dificultad, pulido final

#### User Stories:

**US-9.1:** Como QA, necesito script de testing para bugs críticos
- Tarea: Crear checklist de bugs (crash, softlocks, glitches)
- Estimación: 16 horas
- Responsable: QA Lead

**US-9.2:** Como designer, necesito balanceo de dificultad
- Tarea: Ajustar velocidad enemigos, drain de sanity, spawn rates
- Estimación: 20 horas
- Responsable: Game Designer + Programmer

**US-9.3:** Como QA, necesito playtesting con jugadores externos
- Tarea: Organizar 10-15 sesiones, recolectar feedback
- Estimación: 30 horas
- Responsable: QA Lead + Producer

**US-9.4:** Como equipo, necesito versión beta candidata
- Tarea: Build final, verificación de performance
- Estimación: 12 horas
- Responsable: Lead Programmer + QA

---

## **III. PLAN DE SPRINTS**

### **Sprint 1-2: Weeks 1-2 (Iniciación)**
- ✓ Finalizar GDD
- ✓ Crear moodboards
- ✓ Diagrama UML
- ✓ Lista de SFX/Música
- ✓ Inicializar repositorio

**Entregable:** GDD aprobado, Repo setup, Moodboards

---

### **Sprint 3-4: Weeks 3-4 (Core Mechanics Prototipo)**
- Movimiento del jugador funcional
- Sistema básico de sanity
- Prototipo de enemigo simple
- Primer test (screening)

**Entregable:** Prototipo Alpha jugable (15-20 min)

---

### **Sprint 5-6: Weeks 5-6 (Adaptive Systems)**
- Test completo (Beck + Fobias)
- Algoritmo de spawning adaptativo
- Múltiples tipos de enemigos
- Sistema de pistas (3/5 funcionales)

**Entregable:** Mecánicas adaptativas funcionales

---

### **Sprint 7-8: Weeks 7-8 (Narrativa y Diálogos)**
- Árbol de diálogos personalizado
- Cinemáticas de Acto I
- Sistema de llamadas telefónicas
- Doblaje en progreso

**Entregable:** Narrativa Acto I playable

---

### **Sprint 9-10: Weeks 9-10 (Actos II-III)**
- Progresión de anomalías
- Actos II y III estructurados
- Cinemáticas de finales
- Test final decisivo

**Entregable:** Juego completo (estructura narrativa)

---

### **Sprint 11-12: Weeks 11-12 (Arte y Audio Completo)**
- Modelado 3D apartamento final
- Animaciones completas
- Música compuesta/licensed
- SFX integrados
- Doblaje final

**Entregable:** Assets finales integrados

---

### **Sprint 13-14: Weeks 13-14 (UI/UX y Pulido)**
- Menú principal final
- HUD pulido
- Modos de accesibilidad
- Subtítulos en 5 idiomas

**Entregable:** Juego pulido, interfaz profesional

---

### **Sprint 15-16: Weeks 15-16 (QA Beta)**
- Playtesting externo (10-15 usuarios)
- Bug fixing
- Balanceo final
- Optimizaciones de performance

**Entregable:** Build Beta Cerrada

---

### **Sprint 17-18: Weeks 17-18 (Polish Final)**
- Últimos ajustes narrativos
- Fixes de bugs críticos
- Optimización final
- Preparación de launcher

**Entregable:** Build Release Candidate

---

### **Sprint 19-20: Weeks 19-20 (Lanzamiento)**
- Últimas pruebas
- Deployment en plataforma
- Comunicados de prensa
- Monitoreo post-launch

**Entregable:** Juego en venta / distribución

---

## **IV. MATRIZ RACI (Responsabilidades)**

| Tarea | Lead | Programmer | Designer | Artist | Audio | QA |
|-------|------|-----------|----------|--------|-------|-----|
| GDD | R | C | R | C | C | I |
| Architecture | R | R | C | - | - | C |
| Core Mechanics | C | R | R | C | - | C |
| Adaptive Systems | C | R | R | - | - | C |
| Narrativa | R | C | R | C | C | C |
| Assets | C | C | C | R | R | C |
| QA | I | C | C | C | C | R |
| Release | R | R | C | C | C | C |

**R** = Responsible (Ejecuta)  
**A** = Accountable (Responsable final)  
**C** = Consulted (Consultado)  
**I** = Informed (Informado)

---

## **V. RIESGOS Y PLANES DE MITIGACIÓN**

| # | Riesgo | Impacto | Probabilidad | Mitigación | Contingencia |
|---|--------|---------|-------------|-----------|------------|
| 1 | Scope Creep | Retrasos 2-3 sprints | Alta | MVP definido, sprints rígidos | Reducir features secundarias |
| 2 | Dificultad en IA adaptativa | Enemigos no responden | Media | Algoritmo simple primero, iterate | Usar IA predefinida por escena |
| 3 | Sensibilidad de contenido | Rechazo comunidad | Media | Disclaimers claros, consultores | Versión "light" sin suicidio |
| 4 | Falta de compositor | Delay audio | Baja | Licencias royalty-free backup | Usar assets de Godot Asset Store |
| 5 | Performance deficiente | Framerate bajo | Baja | Profiling temprano, optimización | Reducir resolución assets |
| 6 | Playtesting datos insuficientes | Juego desbalanceado | Media | Beta cerrada 15+ usuarios | Parches post-launch |

---

## **VI. HERRAMIENTAS Y RECURSOS**

### **Software de Desarrollo**
- **Engine:** Unity 2022 LTS+
- **Versionado:** Git + GitHub (con Git LFS para assets grandes)
- **Project Management:** GitHub Projects / Trello
- **Comunicación:** Discord + Slack
- **Diseño:** Blender 4.x (3D), Aseprite (2D), Figma (UI)
- **Audio:** REAPER (DAW), Audacity (Post-prod), Wwise/FMOD (Integración)

### **Hardware Mínimo (Equipo)**
- PC de desarrollo: 16GB RAM, RTX 3070 (rendering)
- Micrófono profesional (doblaje)
- Monitores calibrados (color)

### **Presupuesto Estimado (si freelance)**
- Compositor: $3,000-8,000
- Voice Actor (dublaje): $2,000-5,000
- 3D Artist freelance: $4,000-10,000
- QA/Testing: $2,000-3,000
- **Total estimado:** $11,000-26,000 USD

---

## **VII. MÉTRICAS DE PROGRESO**

### Burn Down Chart (Esperado)
```
Sprint 1  ████████████████████ 100% Estimation
Sprint 2  ███████████████░░░░░░ 75%
Sprint 3  ██████████░░░░░░░░░░░ 50%
Sprint 4  █████░░░░░░░░░░░░░░░░ 25%
Sprint 5  ░░░░░░░░░░░░░░░░░░░░░ 0% (Completado)
```

### KPIs de Éxito
- **Velocity:** 40-50 story points por sprint
- **Bug Escape Rate:** < 5 bugs críticos por sprint
- **Playtester Satisfaction:** 8+/10 promedio
- **Time to Complete:** < 20 minutos promedio por sesión

---

**Documento de PM: Listo para ejecución con equipo**
