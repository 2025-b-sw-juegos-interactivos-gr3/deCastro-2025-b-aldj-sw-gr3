# PHOBIA - A Psychological Horror Game
## Proyecto Final: Diseño de Videojuegos, Arquitectura y Análisis

---

## 📋 Descripción del Proyecto

**PHOBIA** es un juego de terror psicológico narrativo donde el jugador encarna a una persona aislada en su apartamento, aquejada por visiones de una entidad sobrenatural. Lo único que lo mantiene conectado con la realidad es su relación con un terapeuta y la búsqueda de pistas que demuestren si está viviendo un sueño.

### Concepto Central
El juego **adapta dinámicamente su experiencia** basándose en un sistema de tests psicológicos reales (Beck, screening) que el jugador responde mientras avanza. Los enemigos que enfrenta, los diálogos que escucha, y finalmente el final que obtiene, todo depende de su perfil psicológico.

### Pregunta Narrativa
> *"¿Estoy loco, o está sucediendo algo real? ¿Y cuál es la diferencia?"*

---

## 🎮 Características Principales

✨ **Adaptación Narrativa Profunda**
- Tests psicológicos reales integrados al gameplay
- Enemigos que mutan según tus fobias específicas
- Diálogos personalizados según tu profesión y respuestas

🧠 **Horror Psicológico sin Combate**
- Vulnerabilidad constante (no hay armas)
- Únicamente evasión y exploración
- La amenaza viene de tu propia mente

🎭 **Narrativa Bifurcada**
- Final "Bueno": Despierta en un hospital (alucinación por medicación)
- Final "Malo": Descubre que ya está muerto (atrapado en loop infinito)
- Las decisiones tienen peso real

🏠 **Un Único Entorno Transformable**
- El apartamento se distorsiona progresivamente
- 5 pistas de realidad anómalas para encontrar
- Espacios seguros vs. espacios peligrosos

---

## 📁 Estructura de Documentación

Este repositorio contiene la **documentación completa de pre-producción** necesaria para producir PHOBIA:

### 1. **GDD with MDA.md** - Documento de Diseño de Juego
La especificación completa del juego con:
- Ficha técnica y concepto
- **Análisis MDA detallado** (Mechanics, Dynamics, Aesthetics)
- Mecánicas de gameplay
- Estructura narrativa completa
- Diseño de niveles (apartamento)
- Sistema de tests psicológicos
- Descripción de enemigos adaptativos
- Referencias visuales y sonoras

**Lecturas:** 120+ páginas | **Tiempo:** 4-6 horas

### 2. **PROJECT_MANAGEMENT.md** - Planificación Ágil
Gestión de proyecto con enfoque Scrum:
- 9 Épicas principales
- 35+ User Stories detalladas
- Sprints de 2 semanas (20 semanas totales)
- Matriz RACI (Responsabilidades)
- Cronograma de hitos
- Gestión de riesgos y mitigación
- Herramientas recomendadas (GitHub Projects, Trello, Jira)
- Estimaciones de tiempo por tarea

**Lecturas:** 40+ páginas | **Tiempo:** 2-3 horas

### 3. **TECHNICAL_ARCHITECTURE.md** - Ingeniería de Software
Especificación técnica completa:
- Stack tecnológico (Godot 4.3+, GDScript)
- Diagramas UML de clases
- Diagrama de máquina de estados (AI del enemigo)
- Patrones de diseño (Singleton, Observer, Factory, Strategy, etc.)
- Sistema de persistencia (Save Game JSON)
- API de eventos y Signals
- Optimizaciones y presupuesto de performance
- Testing strategy
- Documentación de convenciones de código

**Lecturas:** 50+ páginas | **Tiempo:** 3-4 horas

### 4. **ART_AND_AUDIO_SPECIFICATION.md** - Dirección de Arte
Guía visual y sonora:
- Dirección de arte general (realismo + distorsión)
- **Paleta de colores por acto** (con códigos Hex)
- Diseño del apartamento (zonas específicas)
- Diseño de la entidad (forma base + transformaciones)
- Pistas de realidad (5 anomalías)
- Especificación UI/UX
- **Paleta musical por acto** (BPM, instrumentación)
- Catálogo completo de SFX (40+ efectos)
- Sistema de audio espacial 3D
- Guía de doblaje (Dr. Krell, protagonista)
- Referencias visuales y sonoras
- Pipeline de producción de arte

**Lecturas:** 60+ páginas | **Tiempo:** 3-4 horas

### 5. **EXECUTIVE_SUMMARY.md** - Síntesis Ejecutiva
Resumen ejecutivo del proyecto:
- Visión y propuesta de valor
- Análisis FODA
- Cronograma y presupuesto estimado
- Métricas de éxito
- Riesgos y mitigación
- Plan de validación pre-producción

**Lecturas:** 15 páginas | **Tiempo:** 30-45 min

### 6. **README.md** - Este Archivo
Guía rápida del proyecto y cómo navegar la documentación.

---

## 🎬 Resumen de Contenido

### Análisis MDA (Lo Más Importante)

**AESTHETICS** (¿Qué siente el jugador?)
- Inquietud progresiva
- Aislamiento y soledad
- Agencia comprometida
- Catarsis o tragedia

**DYNAMICS** (¿Cómo interactúan las mecánicas?)
- Indagación Introspectiva: Tests revelan psiquis
- Adaptación Enemiga: Amenazas responden a fobias
- Realidad Frágil: Anomalías cuestionan cordura
- Progresión Bifurcada: Decisiones llevan a finales opuestos

**MECHANICS** (¿Cuáles son las reglas?)
- Sistema de Sanidad (0-100)
- Tests Psicológicos (Screening, Beck, Fobias, Final)
- Recolección de 5 pistas de realidad
- AI de Enemigo basada en FSM
- Diálogos adaptativos
- Exploración limitada a apartamento de 70m²

---

## 🕹️ Estructura del Juego

### **Duración Total:** 8-12 horas

### **Acto I: Normalidad Rota** (2 horas)
Introducción personalizada, primer test, aparición de la entidad.

### **Acto II: Fragmentación** (4 horas)
Test Beck completo, enemigos adaptativos, escalada de paranoia.

### **Acto III: Colapso** (2-3 horas)
Test final decisivo, bifurcación de narrativa.

### **Escena Final A: Despertar** (30 min)
El jugador despierta en un hospital. Era una alucinación por medicación. Final esperanzador.

### **Escena Final B: Loop Infinito** (30 min)
El jugador descubre que ya estaba muerto. Atrapado en ciclo infinito. Horror absoluto.

---

## 👥 Equipo Recomendado

- **1 Lead Designer/Productor** - Visión general, toma de decisiones
- **1 Lead Programmer** - Arquitectura, sistemas core
- **1 Narrative Designer** - Diálogos, estructura narrativa
- **1 3D Artist** - Modelado del apartamento y enemigos
- **1 Audio Designer/Composer** - Música y SFX
- **1 QA Lead** - Testing y bug tracking

**Total:** 4-6 personas | **Duración:** 20 semanas (~5 meses)

---

## 💻 Stack Tecnológico

| Aspecto | Selección |
|---------|-----------|
| **Motor** | Unity 2022 LTS+ |
| **Lenguaje** | C# (.NET Standard 2.1) |
| **Audio** | Built-in AudioServer |
| **3D Modeling** | Blender 4.x |
| **Versionado** | Git + GitHub |
| **Project Mgmt** | GitHub Projects |

---

## 📊 Cronograma (20 Semanas)

| Fase | Semanas | Hito |
|------|---------|------|
| **Initiación** | 1-2 | GDD aprobado, equipo setup |
| **Alpha** | 3-5 | Core loop jugable |
| **Core Dev** | 6-10 | Mecánicas y narrativa funcionales |
| **Asset Production** | 11-14 | Arte, audio, doblaje |
| **Polish & QA** | 15-18 | Playtesting, optimización |
| **Launch** | 19-20 | Build final, deployment |

---

## 🎯 Cómo Usar Esta Documentación

### Para Productores/Directores
1. Leer: **EXECUTIVE_SUMMARY.md** (30 min)
2. Revisar: **GDD with MDA.md** (visión general, 1-2 horas)
3. Validar: **PROJECT_MANAGEMENT.md** (cronograma, presupuesto)

### Para Programadores
1. Leer: **TECHNICAL_ARCHITECTURE.md** (completo)
2. Revisar: **GDD with MDA.md** (sección III: Mecánicas Detalladas)
3. Implementar: Usar patrones de diseño especificados

### Para Artistas
1. Leer: **ART_AND_AUDIO_SPECIFICATION.md** (Arte)
2. Revisar: **GDD with MDA.md** (sección VI: Arte y Audio)
3. Crear: Moodboards basados en referencias

### Para Audio Designer
1. Leer: **ART_AND_AUDIO_SPECIFICATION.md** (Audio)
2. Revisar: **GDD with MDA.md** (sección VI: Arte y Audio)
3. Crear: Paleta musical y catálogo SFX

### Para Narrative Designer
1. Leer: **GDD with MDA.md** (sección IV: Narrativa)
2. Revisar: **ART_AND_AUDIO_SPECIFICATION.md** (Voice Acting)
3. Escribir: Árbol de diálogos adaptativo

---

## 📈 Métricas de Éxito

✓ 70%+ de jugadores completan Acto II  
✓ 50%+ completan un final  
✓ Promedio de sesión: 8-12 horas  
✓ 80%+ reportan sentir ansiedad/inquietud  
✓ 60 FPS consistentes (60 en PC, 30 en consola)  
✓ 0 bugs críticos en lanzamiento  

---

## ⚠️ Consideraciones Éticas

PHOBIA aborda temas sensibles:
- Salud mental
- Suicidio
- Alucinaciones
- Trastornos de ansiedad

**Compromisos:**
- Disclaimer inicial sobre contenido sensible
- Recursos de ayuda (líneas de crisis) incluidas
- Lenguaje responsable, sin glorificación
- Consulta con expertos en salud mental
- Trigger warnings configurables

---

## 🔗 Referencias y Inspiración

### Juegos de Referencia
- *Hellblade: Senua's Sacrifice* - Representación de psicosis
- *What Remains of Edith Finch* - Narrativa intimista
- *P.T.* - Tensión psicológica
- *The Stanley Parable* - Narrativa no lineal
- *Amnesia: The Dark Descent* - Horror sin combate
- *Layers of Fear* - Transformación ambiental

### Literatura
- *The Yellow Wallpaper* (Charlotte Perkins Gilman)
- *The Tell-Tale Heart* (Edgar Allan Poe)

### Cine
- *Memento* (Christopher Nolan)
- *Black Swan* (Darren Aronofsky)
- *The Lighthouse* (Robert Eggers)
- *Hereditary* (Ari Aster)

---

## 📝 Documentación Técnica

### Sobre los Documentos
- **Total de páginas:** 280+ páginas
- **Tiempo de lectura completa:** 12-16 horas
- **Formatos:** Markdown (.md)
- **Actualización:** Conforme se avance en desarrollo

### Control de Versiones
- Todos los documentos están versionados en Git
- Cambios se trackean y documentan
- Historial completo disponible en commits

---

## 🚀 Próximos Pasos

### **Fase 1: Validación (Semana 1)**
- [ ] Revisar GDD con equipo
- [ ] Playtesting de concepto (5-10 testers)
- [ ] Feedback y ajustes
- [ ] **Gate:** GDD aprobado

### **Fase 2: Preparación Técnica (Semanas 2-3)**
- [ ] Crear repositorio GitHub con Git LFS
- [ ] Instalar Unity 2022 LTS
- [ ] Configurar proyecto Unity (URP)
- [ ] Onboarding de equipo
- [ ] **Gate:** Repo funcional

### **Fase 3: Prototipado (Semanas 4-5)**
- [ ] Core loop implementado
- [ ] Primer prototipo del enemigo
- [ ] Sistema de sanidad
- [ ] **Gate:** 15-20 min jugables

### **Fase 4: Desarrollo (Semanas 6-16)**
- Sprints de 2 semanas
- Integración continua
- Testings regulares

### **Fase 5: Polish & Lanzamiento (Semanas 17-20)**
- Playtesting extensivo
- Optimizaciones finales
- Lanzamiento

---

## 📞 Contacto y Colaboración

Para preguntas, sugerencias, o colaboración:
- **Propietario del Proyecto:** [Tu nombre/Discord/Email]
- **Repositorio:** [Link a GitHub]
- **Servidor Discord:** [Opcional]

---

## 📜 Licencia

Este proyecto es parte de un curso académico de Diseño de Videojuegos.  
Derechos reservados © 2026  

*(Especificar licencia apropiada según política de institución educativa)*

---

## 🎓 Créditos Académicos

**Curso:** Diseño de Videojuegos, Arquitectura y Análisis  
**Institución:** [Nombre de Institución]  
**Semestre:** Bimestre 2, 2026  
**Profesor/Mentor:** [Nombre]  

**Equipo de Desarrollo:**
- Game Design Lead: [Nombre]
- Programmer: [Nombre]
- Artist: [Nombre]
- Audio Designer: [Nombre]
- Narrative Designer: [Nombre]
- QA Lead: [Nombre]

---

## 📚 Cómo Navegar Este Repositorio

```
Project-2/
├── GDD with MDA.md                    ← EMPEZAR AQUÍ (Concepto Principal)
├── EXECUTIVE_SUMMARY.md               ← Síntesis Rápida
├── PROJECT_MANAGEMENT.md              ← Planificación Ágil
├── TECHNICAL_ARCHITECTURE.md          ← Ingeniería de Software
├── ART_AND_AUDIO_SPECIFICATION.md     ← Dirección de Arte & Audio
└── README.md                          ← Este archivo
```

---

## ✅ Checklist de Pre-Producción Completada

- [x] GDD completo con análisis MDA
- [x] Planificación de proyecto (Épicas, User Stories, Sprints)
- [x] Arquitectura técnica (UML, patrones, stack)
- [x] Especificación de arte y audio (paletas, diseños, referencias)
- [x] Cronograma detallado (20 semanas)
- [x] Presupuesto estimado ($11k-26k USD)
- [x] Gestión de riesgos identificados
- [x] Métricas de éxito definidas
- [x] Documentación ejecutiva

**Estado:** 🟢 **PRE-PRODUCCIÓN COMPLETADA**

---

## 🎬 Conclusión

**PHOBIA** es un proyecto ambicioso que combina:
- ✨ Narrativa profunda y personalizada
- 🎮 Mecánicas innovadoras adaptativas
- 🧠 Responsabilidad con salud mental
- 🎨 Dirección de arte cohesiva
- 🎵 Sonido inmersivo y psicoacústico

Con la documentación completa, equipo dedicado, y metodología Agile rigurosa, este juego puede convertirse en una experiencia memorable.

**¿Estamos listos para hacer que suceda?**

---

**Fecha de Creación:** Enero 16, 2026  
**Versión:** 1.0  
**Estado:** Pre-producción (Listo para Desarrollo)  
**Última Actualización:** 2026-01-16

---

*"¿Estoy loco, o está sucediendo algo real? ¿Y cuál es la diferencia?"* — PHOBIA
