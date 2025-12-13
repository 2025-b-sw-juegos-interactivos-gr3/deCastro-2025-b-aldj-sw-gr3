📝 Game Design Document (GDD) - Puntos Clave y Comparativa

El GDD es el documento maestro de un proyecto de videojuegos. Es una "guía viva" que evoluciona constantemente, sirviendo como fuente de verdad única para todos los miembros del equipo (diseñadores, programadores, artistas, productores).

🧠 Mapa Mental de la Estructura de un GDD (Mermaid)

Este diagrama representa las secciones esenciales que componen un GDD completo, abarcando desde la visión hasta los detalles de implementación.

mindmap
    root((Game Design Document - GDD))
        A(1. Concepto y Visión: La Esencia del Juego)
            A1(Resumen Ejecutivo (Pitch): ¿Por qué es divertido y único?)
            A2(Objetivo del Juego: Tema, Tono, Promesa (Premise))
            A3(Género y Plataformas: (Ej: RPG Táctico, PC/Consola))
            A4(Público Objetivo: Demografía, Motivaciones e Intereses)
        B(2. Jugabilidad (Gameplay): Las Reglas y la Interacción)
            B1(Mecánicas Principales: El Core Loop)
                B1a(Loop de Juego Central: (Ej: Explorar -> Luchar -> Mejorar))
                B1b(Controles y Movimiento: Esquemas de control, físicas y cámara)
                B1c(Reglas y Sistemas: Puntuación, Economía, Crafteo, Tablas de Balance)
            B2(Interfáz de Usuario (UI/UX): La Comunicación con el Jugador)
                B2a(HUD: Elementos en pantalla (Vida, Mapa, Barras de Recursos))
                B2b(Menús y Navegación: Diseño de flujos (Main Menu, Pausa, Inventario))
            B3(Diseño de Niveles: El Espacio de Juego)
                B3a(Estructura y Progresión: Lineal, Abierto, Curva de Dificultad)
                B3b(Mapas o Layouts Clave: Bocetos, Puntos de Interés, Desafíos)
        C(3. Contenido y Narrativa: El Mundo y la Historia)
            C1(Historia / Lore: El Universo del Juego)
                C1a(Sinopsis: Resumen de la trama principal)
                C1b(Arco Narrativo: Introducción, Clímax, Resolución)
            C2(Personajes: Roles y trasfondos)
                C2a(Protagonistas/Antagonistas: Habilidades y Motivaciones Clave)
                C2b(NPCs y Clases: Tipos de interacciones, diálogo y sistemas de facciones)
            C3(Enemigos / IA: Desafíos y Comportamientos)
                C3a(Tipos de Enemigos y Patrones: Diseño, Lógica de combate, Debilidades)
        D(4. Arte y Audio: La Experiencia Sensorial)
            D1(Estilo Visual: La Dirección Artística)
                D1a(Concept Art de Referencia: Moodboards, Estilo de arte (Ej: Pixel Art, Realista))
                D1b(Paleta de Colores y Ambiente: Definición de la atmósfera y el mood)
            D2(Audio: Diseño Sonoro)
                D2a(Música (Banda Sonora): Temas principales, Pistas dinámicas, Ambientes)
                D2b(Efectos de Sonido (SFX): Interacción, Combate, Pistas de Foley)
                D2c(Doblaje y Diálogo: Lista de líneas y requerimientos de actores de voz)
        E(5. Aspectos Técnicos y de Producción: La Ejecución)
            E1(Tecnología: Herramientas y Stack)
                E1a(Motor de Juego (Engine): (Ej: Unity, Unreal) y Lenguajes)
                E1b(Herramientas Necesarias: (Ej: Git, Jira, Perforce, Blender, Photoshop))
            E2(Plan de Producción: Tiempo y Recursos)
                E2a(Hitos (Milestones) y Entregables: Fechas clave y Alcance (Scope) por fase)
                E2b(Riesgos Identificados: (Ej: Fallo técnico, Desbalance, Retrasos en arte))
            E3(Monetización: El Modelo de Negocio)
                E3a(Modelo de Negocio: (Ej: F2P con Microtransacciones, Pago Único Premium, DLCs))


🎮 Comparativa con Ejemplos Reales: El Espectro del GDD

El GDD no es un formato único, sino un espectro que va desde un documento de alta formalidad y detalle hasta una colección de notas ágiles.

1. GDD Formal (Teórico / Tradicional)

Esta estructura busca documentar todo el juego antes de comenzar la producción intensiva. Es común en proyectos con grandes presupuestos, licencias, o cuando se usa la metodología Waterfall.

Aspecto

GDD Ideal (Teórico)

Documento

Único, grande y completo.

Énfasis

Detalle absoluto y previsión de todas las características.

Propósito

Servir como un contrato o plan maestro.

Metodología

Suele asociarse a flujos lineales (Waterfall).

2. GDD Ágil (La Práctica Moderna)

En la industria moderna, el GDD es un "Documento Vivo" que se gestiona de forma iterativa, priorizando el prototipo y la adaptación:

Documento Vivo y Fragmentado: En lugar de un GDD estático, existe un GDD Core (Visión, Público, Mecánica Central) y una colección de documentos satélite específicos (Level Design Docs, System Specs) alojados en herramientas como Confluence o Notion.

Enfoque en el Prototipo Iterativo: El documento se mantiene incompleto intencionalmente. Solo se documenta la mecánica que está a punto de ser construida o probada en el siguiente sprint.

Minimal GDD (Vision Zero): Para la fase inicial de "pitch" o validación, se usa un "Vision Document" o "One-Pager" ultracorto (cubriendo solo las secciones A y B1 del mapa mental) antes de desarrollar la documentación completa.

3. Ejemplo de Caso: El GDD de 'Apocalypse Now' (Formal y Visionario)

El GDD para el videojuego de Apocalypse Now (el documento PDF) es un ejemplo de un GDD altamente tradicional, formal y exhaustivo, contrastando con el enfoque ágil:

## Mapa Mental

La representación gráfica del mapa mental está disponible como SVG en el repositorio. Si tu visor Markdown no renderiza Mermaid, abre el SVG directamente.

- Archivo: [mindmap GDD.svg](mindmap%20GDD.svg)

<img src="mindmap GDD.svg" alt="Mapa mental GDD" style="max-width:100%;height:auto;" />