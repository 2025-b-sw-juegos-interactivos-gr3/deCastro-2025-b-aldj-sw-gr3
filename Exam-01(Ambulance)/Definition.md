Examen 001
¡Hola a todos, futuros ingenieros de sistemas!
Prepárense para un desafío emocionante que pondrá a prueba sus habilidades en gráficos 3D y desarrollo de juegos. Aquí encontrarán toda la información para su próximo examen.
 
🎯 Tu Misión: El Examen de "Recoger y Entregar"
 
El objetivo de este examen es diseñar y construir un juego 3D funcional utilizando la biblioteca Babylon.js.
La mecánica principal del juego debe ser simple pero bien implementada: el jugador debe poder recoger uno o más paquetes (u objetos) de un lugar específico y entregarlos en otro lugar designado. No olvidar que a parte de la funcionalidad el juego debe de tener las texturas, modelos objetos que representen al juego como lo hemos estado practicando en clase.
 
Requisitos Mínimos:
 
Un Jugador: Un objeto (cubo, esfera, modelo 3D) que el estudiante pueda controlar (por ejemplo, con las teclas WASD o flechas).
Un Paquete: Un objeto que se puede "recoger".
Una Zona de Recogida: El lugar donde el paquete comienza.
Una Zona de Entrega: El lugar donde el paquete debe ser soltado.
Mecánica de Recogida: Cuando el jugador se acerca al paquete y presiona una tecla (ej. "Espacio" o "E"), el paquete debe "unirse" al jugador.
Mecánica de Entrega: Cuando el jugador (con el paquete) llega a la zona de entrega y presiona una tecla, el paquete debe "soltarse" en esa zona.
Estado: El juego debe saber si el jugador tiene o no un paquete (no se puede recoger otro si ya tiene uno, no se puede entregar si no tiene nada).
 
🎨 Elige tu Aventura: 25 Temas para tu Juego
 
Para que cada proyecto sea único, aquí tienes 25 ideas temáticas. ¡Elige una y hazla tuya!

Conductor de Ambulancia: Recoge un paciente (un objeto) y llévalo rápido al hospital.

🛠️ Kit de Herramientas de Babylon.js
 
Para completar esta misión, probablemente necesitarás usar los siguientes conceptos y funciones. ¡Investígalos!
BABYLON.Engine y BABYLON.Scene: El corazón de tu aplicación. El motor (engine) renderiza la escena (scene).
Cámaras y Luces:
BABYLON.FreeCamera: Una cámara simple en primera persona, útil para controlar con el teclado.
BABYLON.HemisphericLight: La forma más fácil de iluminar toda tu escena para que puedas ver tus objetos.
Creación de Objetos (Meshes):
BABYLON.MeshBuilder: Tu mejor amigo para este proyecto.
BABYLON.MeshBuilder.CreateBox("nombre", {size: 2}, scene);
BABYLON.MeshBuilder.CreateSphere("nombre", {diameter: 2}, scene);
BABYLON.MeshBuilder.CreateGround("nombre", {width: 10, height: 10}, scene);
Materiales:
BABYLON.StandardMaterial: Para dar color a tus objetos.
material.diffuseColor = new BABYLON.Color3(1, 0, 0); (Esto crearía un material rojo).
Manejo de Input (Teclado):
scene.onKeyboardObservable: La forma moderna de manejar el teclado. Te permite "observar" eventos de teclado (tecla presionada, tecla soltada) y reaccionar a ellos.
Lógica de "Recoger" (¡La Clave!):
Parenting (Emparantamiento): Este es el truco principal. Para "recoger" un objeto, simplemente lo conviertes en "hijo" del jugador.
paquete.parent = jugador;
Una vez que es hijo, se moverá, rotará y escalará junto con su padre (el jugador).
Lógica de "Dejar":
Para "soltar" el objeto, simplemente rompes esa relación de parentesco.
paquete.parent = null;
Detección de Proximidad:
¿Cómo saber si estás "cerca" de un objeto para recogerlo?
BABYLON.Vector3.Distance(vector1, vector2): Puedes obtener la posición de tu jugador (jugador.position) y la del paquete (paquete.position) y calcular la distancia entre ellos.
let distancia = BABYLON.Vector3.Distance(jugador.position, paquete.position);
Si distancia < 2 (o un valor pequeño), entonces permites que el jugador presione la tecla para recoger.
 
💻 Código de Ejemplo: Recoger y Dejar
 
Aquí tienes un ejemplo completo y funcional. Cópialo, guárdalo como index.html y ábrelo en tu navegador.
Usa WASD para mover el cubo azul (Jugador).
Usa la Barra Espaciadora para recoger y dejar el cubo rojo (Paquete).
HTML
 
 
Plain Text
<!DOCTYPE html><html><head><meta charset="UTF-8"><title>Babylon.js - Ejemplo de Recoger y Dejar</title><style>html, body {
            overflow: hidden;
            width: 100%;
            height: 100%;
            margin: 0;
            padding: 0;
        }        #renderCanvas {
            width: 100%;
            height: 100%;
            touch-action: none;
        }
    </style><script src="https://cdn.babylonjs.com/babylon.js"></script><script src="https://cdn.babylonjs.com/loaders/babylonjs.loaders.min.js"></script></head><body><canvas id="renderCanvas"></canvas><script>const canvas = document.getElementById("renderCanvas");
        const engine = new BABYLON.Engine(canvas, true);
        // Variable de estado para saber si tenemos el paquetelet paqueteEnMano = false;
        // Mapa para rastrear las teclas presionadaslet inputMap = {};
        const createScene = function () {
            const scene = new BABYLON.Scene(engine);
            scene.collisionsEnabled = true;
            // --- Cámara y Luz ---const camera = new BABYLON.FreeCamera("camera1", new BABYLON.Vector3(0, 5, -10), scene);
            camera.setTarget(BABYLON.Vector3.Zero());            camera.attachControl(canvas, true);
            const light = new BABYLON.HemisphericLight("light1", new BABYLON.Vector3(0, 1, 0), scene);
            light.intensity = 0.7;
            // --- Materiales (Colores) ---const matJugador = new BABYLON.StandardMaterial("matJugador", scene);
            matJugador.diffuseColor = new BABYLON.Color3(0, 0.5, 1); // Azulconst matPaquete = new BABYLON.StandardMaterial("matPaquete", scene);
            matPaquete.diffuseColor = new BABYLON.Color3(1, 0, 0); // Rojoconst matZona = new BABYLON.StandardMaterial("matZona", scene);
            matZona.diffuseColor = new BABYLON.Color3(0, 1, 0); // Verde            matZona.alpha = 0.5; // Semitransparenteconst matSuelo = new BABYLON.StandardMaterial("matSuelo", scene);
            matSuelo.diffuseColor = new BABYLON.Color3(0.5, 0.5, 0.5); // Gris// --- Objetos ---const suelo = BABYLON.MeshBuilder.CreateGround("suelo", { width: 20, height: 20 }, scene);
            suelo.material = matSuelo;
            const jugador = BABYLON.MeshBuilder.CreateBox("jugador", { size: 1 }, scene);
            jugador.material = matJugador;            jugador.position.y = 0.5;
            const paquete = BABYLON.MeshBuilder.CreateBox("paquete", { size: 0.5 }, scene);
            paquete.material = matPaquete;            paquete.position = new BABYLON.Vector3(5, 0.25, 5);
            const zonaEntrega = BABYLON.MeshBuilder.CreateGround("zonaEntrega", { width: 3, height: 3 }, scene);
            zonaEntrega.material = matZona;            zonaEntrega.position = new BABYLON.Vector3(-5, 0.01, -5); // 0.01 para estar sobre el suelo// --- Lógica de Input ---            scene.actionManager = new BABYLON.ActionManager(scene);
            scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction(BABYLON.ActionManager.OnKeyDownTrigger, function (evt) {
                inputMap[evt.sourceEvent.key.toLowerCase()] = true;
            }));
            scene.actionManager.registerAction(new BABYLON.ExecuteCodeAction(BABYLON.ActionManager.OnKeyUpTrigger, function (evt) {
                inputMap[evt.sourceEvent.key.toLowerCase()] = false;
            }));
            // --- Lógica de Recoger / Dejar (Al presionar Espacio) ---            scene.onKeyboardObservable.add((kbInfo) => {
                if (kbInfo.type === BABYLON.KeyboardEventTypes.KEYDOWN) {
                    if (kbInfo.event.key === " ") { // Barra espaciadora// 1. Lógica para RECOGERif (!paqueteEnMano) {
                            let dist = BABYLON.Vector3.Distance(jugador.position, paquete.position);
                            if (dist < 2) { // Si está suficientemente cercaconsole.log("¡Paquete recogido!");
                                paquete.parent = jugador; // ¡La magia! El paquete ahora es hijo del jugador                                paquete.position = new BABYLON.Vector3(0, 0.7, 0); // Posición relativa al jugador (encima)
                                paqueteEnMano = true;
                            }
                        }
                        // 2. Lógica para DEJARelse {
                            let dist = BABYLON.Vector3.Distance(jugador.position, zonaEntrega.position);
                            if (dist < 2) { // Si está suficientemente cerca de la zonaconsole.log("¡Paquete entregado!");
                                paquete.parent = null; // ¡La magia! El paquete ya no tiene padre
                                paquete.position = zonaEntrega.position.clone(); // Dejarlo en la zona
                                paquete.position.y = 0.25; // Ponerlo sobre la zona
                                paqueteEnMano = false;
                            }
                        }
                    }
                }
            });
            // --- Game Loop (Movimiento del jugador) ---const velocidad = 0.1;
            scene.onBeforeRenderObservable.add(() => {
                if (inputMap["w"]) {
                    jugador.position.z += velocidad;
                }
                if (inputMap["s"]) {
                    jugador.position.z -= velocidad;
                }
                if (inputMap["a"]) {
                    jugador.position.x -= velocidad;
                }
                if (inputMap["d"]) {
                    jugador.position.x += velocidad;
                }
            });
            return scene;
        };
        const scene = createScene();
        engine.runRenderLoop(function () {
            scene.render();
        });
        window.addEventListener("resize", function () {
            engine.resize();
        });
    </script></body></html>
 
 
¡Mucha suerte en su examen! ¡Diviértanse creando!
 
 
El enlace del repositorio y EL VIDEO del juego funcionando y explicacion del codigo debe estar en el canal de 003 - Examen 01 (enlace)  (El codigo fuente debe estar en una nueva carpeta dentro del repositorio del estudiante llamada "Examen-01"
 