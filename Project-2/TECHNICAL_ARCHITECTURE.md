# TECHNICAL ARCHITECTURE - PHOBIA
## Especificación de Ingeniería de Software

---

## **I. STACK TECNOLÓGICO**

### **Frontend / Game Engine**
- **Motor Base:** Unity 2022 LTS (Long Term Support)
  - Razones: Ecosistema maduro, excelente soporte 3D, Asset Store extenso, comunidad global
  - Versión mínima: 2022.3 LTS
  - Versión recomendada: Unity 2022.3.17f1 o superior

### **Lenguaje Principal**
- **C#** (lenguaje principal de Unity)
  - Framework: .NET Standard 2.1
  - IDE recomendado: Visual Studio 2022 o JetBrains Rider
  - Sin uso de UnityScript (deprecado)

### **Backend / Datos**
- **Persistencia local:** JSON (SaveGame system)
- **Base de datos:** SQLite (opcional, para analytics)
- **Servidor opcional:** Node.js + Express (para estadísticas anónimas)

### **Audio**
- **Audio Engine:** Unity Audio System
- **Integraciones:** FMOD Studio o Wwise (recomendado para audio espacial avanzado)
- **Formato:** OGG Vorbis / MP3 (comprimido), WAV (lossless en desarrollo)

### **Librerías Externas (Unity)**
- **DialogueManager:** YarnSpinner (Unity Asset) o Ink
- **SaveGame Manager:** JSON.NET (Newtonsoft.Json) o Unity JsonUtility
- **StateMachine:** Custom FSM o Behavior Designer (Asset Store)
- **UI Framework:** Unity UI (uGUI) con TextMeshPro

### **Control de Versiones**
- **VCS:** Git + GitHub
- **Branching:** Git Flow
  - `main` → Builds estables
  - `develop` → Integración
  - `feature/*` → Features individuales
  - `release/*` → Preparación de lanzamiento
  - `hotfix/*` → Parches críticos

---

## **II. DIAGRAMA DE ARQUITECTURA GENERAL (C4 Model)**

```
┌─────────────────────────────────────────────────────┐
│               PHOBIA - ARCHITECTURE                 │
├─────────────────────────────────────────────────────┤

┌──────────────────────────────────────┐
│        UNITY ENGINE 2022 LTS         │
│  ┌────────────────────────────────┐  │
│  │  Rendering Engine (URP/HDRP)  │  │
│  ├────────────────────────────────┤  │
│  │  Physics Engine (PhysX)        │  │
│  ├────────────────────────────────┤  │
│  │  Audio System + Spatial Audio  │  │
│  └────────────────────────────────┘  │
│                                      │
│  ┌──────────┐  ┌──────────┐         │
│  │   C#     │  │  .NET    │         │
│  │  Scripts │  │  Std 2.1 │         │
│  └──────────┘  └──────────┘         │
└──────────────────────────────────────┘
          ↓
┌──────────────────────────────────────┐
│    Application Layer (Game Logic)    │
├──────────────────────────────────────┤
│  • GameManager (Singleton)           │
│  • PlayerController                  │
│  • EnemyManager + AI                 │
│  • TestSystem (Psychometric)         │
│  • DialogueSystem                    │
│  • SaveGame Manager                  │
│  • AudioManager                      │
│  • UIManager                         │
└──────────────────────────────────────┘
          ↓
┌──────────────────────────────────────┐
│     Data / Persistence Layer         │
├──────────────────────────────────────┤
│  • JSON Save Files                   │
│  • Config Files (InputMap, Settings) │
│  • Resource Files (Scenes, Assets)   │
│  • SQLite DB (Optional - Analytics)  │
└──────────────────────────────────────┘
          ↓ (Optional)
┌──────────────────────────────────────┐
│    Backend / Analytics Server        │
├──────────────────────────────────────┤
│  • Node.js + Express                 │
│  • Recolectar datos anónimos         │
│  • Análisis de comportamiento        │
│  • Estadísticas de finales           │
└──────────────────────────────────────┘
```

---

## **III. DIAGRAMA UML: CLASES PRINCIPALES**

### **A. Core System Classes**

```uml
┌──────────────────────────┐
│     GameManager          │
│   (Singleton Pattern)    │
├──────────────────────────┤
│ - instance: GameManager  │
│ - sanity: float          │
│ - currentAct: Act enum   │
│ - playerPhobias: Dict    │
│ - testHistory: Array     │
│ - elapsedTime: float     │
│                          │
│ + getInstance(): GM      │
│ + SetSanity(value)       │
│ + GetSanity(): float     │
│ + OnTestCompleted(test)  │
│ + SpawnEnemy(type)       │
│ + SaveGame()             │
│ + LoadGame()             │
│ + OnGameStateChanged()   │
│                          │
│ [Signals]                │
│ + sanity_changed         │
│ + enemy_spawned          │
│ + test_completed         │
│ + game_saved             │
│ + game_loaded            │
│ + act_changed            │
└──────────────────────────┘
         △
         │ uses
         │
    ┌─────┴────────┬──────────────┬───────────┐
    │              │              │           │
    ▼              ▼              ▼           ▼
┌──────────┐ ┌──────────┐ ┌──────────┐ ┌──────────┐
│ Player   │ │ Enemy    │ │ TestSys  │ │Dialogue  │
│Controller│ │Manager   │ │          │ │System    │
└──────────┘ └──────────┘ └──────────┘ └──────────┘
```

### **B. Clase PlayerController**

```
┌──────────────────────────────────┐
│     PlayerController             │
│   (Extends CharacterBody3D)      │
├──────────────────────────────────┤
│ Properties:                      │
│ - position: Vector3              │
│ - velocity: Vector3              │
│ - moveSpeed: float = 5.0         │
│ - sprintSpeed: float = 8.0       │
│ - currentSanity: float           │
│ - anchorsFound: int = 0          │
│ - inSafeZone: bool = false       │
│ - isAlive: bool = true           │
│                                  │
│ Methods:                         │
│ + _ready()                       │
│ + _physics_process(delta)        │
│ + HandleInput()                  │
│ + Move(direction: Vector3)       │
│ + TakeSanityDamage(amount)       │
│ + RegenerateSanity(rate)         │
│ + FindAnchor(anchor: Node)       │
│ + DetectThreat(): bool           │
│ + GetDamaged(source: Enemy)      │
│ + Die()                          │
│                                  │
│ [Signals]                        │
│ + anchor_found                   │
│ + threat_detected                │
│ + died                           │
│ + sanctuary_entered              │
│ + sanctuary_exited               │
└──────────────────────────────────┘
```

### **C. Clase Enemy (Polimórfica)**

```
┌────────────────────────────────┐
│     Enemy (Base Class)         │
│  (Extends CharacterBody3D)     │
├────────────────────────────────┤
│ Properties:                    │
│ - type: EnemyType enum         │
│ - position: Vector3            │
│ - speed: float                 │
│ - sanityThreshold: float       │
│ - detectionRange: float = 15   │
│ - damageRate: float = 0.5      │
│ - isPersistent: bool = true    │
│ - currentState: State FSM      │
│ - targetPlayer: Node3D         │
│                                │
│ Methods:                       │
│ + _ready()                     │
│ + _physics_process(delta)      │
│ + ChangeState(newState)        │
│ + FollowPlayer()               │
│ + PlayAnimation(anim)          │
│ + PlaySound(sfx)               │
│ + IsPlayerDetected(): bool     │
│ + DealDamage(target)           │
│                                │
│ [Virtual Methods]              │
│ + OnSpawn() [override]         │
│ + OnDetected() [override]      │
│ + OnAttack() [override]        │
└────────────────────────────────┘
         △
         │ inherits
    ┌────┴────┬───────────┬──────────┐
    │         │           │          │
    ▼         ▼           ▼          ▼
  Spider  Specter    WaterEntity  FacialEntity
  (8 legs) (Crowd)    (Liquid)    (Faces)
```

### **D. Clase TestSystem**

```
┌──────────────────────────────────┐
│     TestSystem                   │
│   (Extends Node)                 │
├──────────────────────────────────┤
│ Properties:                      │
│ - currentTest: Test obj          │
│ - allTests: Dict<TestType>       │
│ - playerResponses: Array         │
│ - phobiaProfile: Dict            │
│ - testInProgress: bool           │
│                                  │
│ Methods:                         │
│ + StartTest(type: TestType)      │
│ + SubmitAnswer(answer: int)      │
│ + CalculateScore(): int          │
│ + GeneratePhobiaProfile()        │
│ + GetNextPhobia(): EnemyType     │
│ + SaveTestResults()              │
│ + OnTestCompleted()              │
│                                  │
│ [Signals]                        │
│ + test_started                   │
│ + test_completed                 │
│ + phobia_detected                │
│ + profile_generated              │
└──────────────────────────────────┘
     │
     ├──→ ┌─────────────────┐
     │    │ Test (Template) │
     │    ├─────────────────┤
     │    │ - testID: int   │
     │    │ - questions:[]  │
     │    │ - scoring:Algo  │
     │    └─────────────────┘
     │
     └──→ ┌─────────────────────┐
          │ Question            │
          ├─────────────────────┤
          │ - text: String      │
          │ - answers: Array    │
          │ - weights: Array    │
          │ - phobiaType: enum  │
          └─────────────────────┘
```

### **E. Clase DialogueSystem**

```
┌──────────────────────────────────┐
│     DialogueSystem               │
│   (Extends Node)                 │
├──────────────────────────────────┤
│ Properties:                      │
│ - dialogueTree: JSON             │
│ - currentDialogue: Node          │
│ - playerName: String             │
│ - playerProfession: String       │
│ - conversationLog: Array         │
│ - isDialoguePlaying: bool        │
│                                  │
│ Methods:                         │
│ + LoadDialogue(dialogueID)       │
│ + AdaptDialogue(context)         │
│ + PlayDialogue()                 │
│ + GetNextChoice(): Array         │
│ + SelectChoice(choiceID)         │
│ + SubstituteVariables(text)      │
│ + PlayVoiceOver(voice)           │
│ + GetDialogueByContext()         │
│                                  │
│ [Signals]                        │
│ + dialogue_started               │
│ + dialogue_ended                 │
│ + choice_presented               │
│ + dialogue_progressed            │
└──────────────────────────────────┘
```

### **F. Clase SaveGameManager**

```
┌────────────────────────────────────┐
│     SaveGameManager                │
│   (Extends Node - Singleton)       │
├────────────────────────────────────┤
│ Properties:                        │
│ - saveDir: String                  │
│ - currentSaveSlot: int             │
│ - saveData: Dictionary             │
│                                    │
│ Methods:                           │
│ + SaveGame(slot: int)              │
│ + LoadGame(slot: int)              │
│ + DeleteSave(slot: int)            │
│ + GetSaveMetadata(slot): Dict      │
│ + SerializeGameState()             │
│ + DeserializeGameState(data)       │
│ + ValidateSaveFile(slot): bool     │
│ + EncryptSave() [future]           │
│                                    │
│ [Signals]                          │
│ + game_saved                       │
│ + game_loaded                      │
│ + save_deleted                     │
│ + save_corrupted                   │
└────────────────────────────────────┘
```

### **G. Clase UIManager**

```
┌──────────────────────────────────┐
│     UIManager                    │
│   (Extends CanvasLayer)          │
├──────────────────────────────────┤
│ Properties:                      │
│ - hud: HUD (Custom node)         │
│ - menu: Menu (Custom node)       │
│ - sanityBar: ProgressBar         │
│ - anchorsCounter: Label          │
│ - threatIndicator: AnimatedSprite│
│                                  │
│ Methods:                         │
│ + UpdateSanityBar(value)         │
│ + UpdateAnchorCount(count)       │
│ + ShowThreatWarning()            │
│ + HideThreatWarning()            │
│ + ShowTestUI()                   │
│ + HideTestUI()                   │
│ + DisplayDialogue(text)          │
│ + ShowMenu()                     │
│ + ApplyGraphicalDistortion(val)  │
│ + SetColorblindMode(mode)        │
│                                  │
│ [Signals]                        │
│ + ui_updated                     │
│ + menu_shown                     │
│ + menu_hidden                    │
└──────────────────────────────────┘
```

---

## **IV. DIAGRAMA DE ESTADOS: AI DEL ENEMIGO**

```
                  ┌─────────────┐
                  │   SPAWN     │
                  └──────┬──────┘
                         │
                         ▼
            ┌────────────────────────┐
            │   IDLE (Patrol)        │
            │   - Random movement    │
            │   - Listening...       │
            └────────┬───────────────┘
                     │ isPlayerNear?
                     │ (detectionRange)
                     ▼
            ┌────────────────────────┐
            │   SEARCHING            │
            │   - Investigate area   │
            │   - Play search sounds │
            └────────┬───────────────┘
                     │ foundPlayer?
                     │ (los check)
                     ▼
            ┌────────────────────────┐
            │   CHASING              │
            │   - Follow player      │
            │   - Increase speed     │
            │   - Play chase audio   │
            └────────┬───────────────┘
                     │ gotPlayer?
                     │ (distance < 2m)
                     ▼
            ┌────────────────────────┐
            │   ATTACKING            │
            │   - Drain sanity -5/s  │
            │   - Play attack sounds │
            │   - Animation          │
            └────────┬───────────────┘
                     │ playerEscaped?
                     │ (distance > 20m)
                     ▼
                  SEARCHING
                  (loop)

Transition Conditions:
  IDLE → SEARCHING: distance < 12m
  SEARCHING → IDLE: playerNotFound for 10 seconds
  CHASING → IDLE: playerOutOfRange for 15 seconds
  ATTACKING → CHASING: playerDistance > 3m
```

---

## **V. SISTEMA DE PERSISTENCIA (SAVE GAME)**

### **Estructura de SaveGame.json**

```json
{
  "version": "1.0",
  "playername": "Diego",
  "profession": "programmer",
  "createdAt": "2026-01-16T10:30:00Z",
  "lastPlayedAt": "2026-01-16T12:45:30Z",
  "playTime": 7200,
  "currentAct": 2,
  
  "playerState": {
    "position": {"x": 10.5, "y": 0.0, "z": 8.2},
    "sanity": 45.7,
    "health": 100,
    "isAlive": true,
    "anchorsFound": [0, 2, 3],
    "anchorsCollected": 3,
    "totalAnchors": 5
  },
  
  "testHistory": [
    {
      "testType": "screening",
      "completedAt": "2026-01-16T10:45:00Z",
      "responses": [1, 0, 2, 1, 0],
      "score": 4
    },
    {
      "testType": "beck",
      "completedAt": "2026-01-16T11:30:00Z",
      "responses": [0, 1, 2, 1, 1, 0, 2, 1, 0, 1, 2, 1, 0, 1, 2, 1, 0, 1, 2, 1],
      "score": 28,
      "severity": "moderate"
    }
  ],
  
  "phobiaProfile": {
    "socialPhobia": 78,
    "arachnophobia": 25,
    "aquaphobia": 15,
    "nomophobia": 65,
    "claustrophobia": 42,
    "dominantPhobia": "socialPhobia"
  },
  
  "enemiesEncountered": [
    {
      "type": "genericSpirit",
      "encounteredAt": "2026-01-16T10:50:00Z",
      "escaped": true
    },
    {
      "type": "specter_crowd",
      "encounteredAt": "2026-01-16T11:15:00Z",
      "escaped": true
    }
  ],
  
  "dialogueLog": [
    {
      "speaker": "therapist",
      "line": "Dr. Krell: ¿Cómo ha sido tu semana?",
      "timestamp": "2026-01-16T10:35:00Z"
    },
    {
      "speaker": "therapist",
      "line": "Dr. Krell: Parece que hemos empeorado. Necesitamos ajustar la medicación.",
      "timestamp": "2026-01-16T11:45:00Z"
    }
  ],
  
  "settings": {
    "language": "es",
    "subtitles": true,
    "colorblindMode": "deuteranopia",
    "masterVolume": 0.8,
    "musicVolume": 0.6,
    "sfxVolume": 0.9,
    "difficultySetting": "normal"
  },
  
  "checksum": "a3f5e7d9c2b1f4e8"
}
```

---

## **VI. API DE EVENTOS Y SIGNALS**

### **Signal Map (Godot's Event System)**

```
GameManager (Central Hub):
├─ sanity_changed(newValue: float)
├─ enemy_spawned(enemyType: Enum, position: Vector3)
├─ enemy_defeated(enemy: Node)
├─ test_started(testType: Enum)
├─ test_completed(results: Dictionary)
├─ anchor_found(anchorID: int)
├─ dialogue_triggered(dialogueID: String)
├─ act_changed(newAct: Enum)
├─ game_saved(slot: int)
├─ game_loaded(slot: int)
├─ threat_detected()
├─ threat_lost()
└─ ending_reached(endingType: Enum)

PlayerController:
├─ moved(newPosition: Vector3)
├─ sanctuary_entered()
├─ sanctuary_exited()
├─ threat_detected()
├─ sanity_damage_taken(amount: float)
└─ died()

Enemy:
├─ spawned(position: Vector3)
├─ detected_player()
├─ lost_player()
├─ attacked_player()
└─ destroyed()

TestSystem:
├─ test_question_displayed(question: String, answers: Array)
├─ answer_submitted(choice: int)
├─ test_completed(score: int, phobias: Dictionary)
└─ phobia_detected(type: String, intensity: float)

UIManager:
├─ sanity_bar_updated(value: float)
├─ threat_indicator_activated()
├─ dialogue_panel_shown()
├─ menu_opened()
└─ menu_closed()

AudioManager:
├─ music_track_changed(trackName: String)
├─ sound_effect_played(sfxName: String)
├─ spatial_audio_updated(position: Vector3)
└─ dialogue_voice_started()
```

---

## **VII. PATRONES DE DISEÑO APLICADOS**

### **1. Singleton (GameManager)**
```csharp
public class GameManager : MonoBehaviour
{
    private static GameManager _instance;
    
    public static GameManager Instance
    {
        get
        {
            if (_instance == null)
            {
                _instance = FindObjectOfType<GameManager>();
                if (_instance == null)
                {
                    GameObject go = new GameObject("GameManager");
                    _instance = go.AddComponent<GameManager>();
                }
            }
            return _instance;
        }
    }
    
    private void Awake()
    {
        if (_instance != null && _instance != this)
        {
            Destroy(this.gameObject);
            return;
        }
        _instance = this;
        DontDestroyOnLoad(this.gameObject);
    }
    
    public float sanity = 80.0f;
}
```

### **2. Observer Pattern (Unity Events)**
```csharp
// En GameManager:
public UnityEvent<float> OnSanityChanged = new UnityEvent<float>();

// En PlayerController:
private void Start()
{
    GameManager.Instance.OnSanityChanged.AddListener(OnSanityChangedHandler);
}

private void OnSanityChangedHandler(float newValue)
{
    Debug.Log($"Sanidad ahora en: {newValue}");
    UIManager.Instance.UpdateSanityBar(newValue);
}
```

### **3. State Machine (Enemy AI)**
```csharp
public abstract class EnemyState
{
    protected Enemy enemy;
    
    public EnemyState(Enemy enemy)
    {
        this.enemy = enemy;
    }
    
    public virtual void Enter() { }
    public virtual void Exit() { }
    public virtual void Update() { }
    public virtual void FixedUpdate() { }
}

// Subclases: IdleState, SearchState, ChaseState, AttackState
public class IdleState : EnemyState
{
    public IdleState(Enemy enemy) : base(enemy) { }
    
    public override void Enter()
    {
        // Lógica de entrada
    }
}
```

### **4. Factory Pattern (Enemy Spawning)**
```csharp
public class EnemyFactory : MonoBehaviour
{
    [System.Serializable]
    public class EnemyPrefabMapping
    {
        public string enemyType;
        public GameObject prefab;
    }
    
    [SerializeField]
    private List<EnemyPrefabMapping> enemyPrefabs;
    
    private Dictionary<string, GameObject> prefabDict;
    
    private void Awake()
    {
        prefabDict = new Dictionary<string, GameObject>();
        foreach (var mapping in enemyPrefabs)
        {
            prefabDict[mapping.enemyType] = mapping.prefab;
        }
    }
    
    public Enemy CreateEnemy(string type, Vector3 position)
    {
        if (!prefabDict.ContainsKey(type))
            type = "spirit"; // default
            
        GameObject instance = Instantiate(prefabDict[type], position, Quaternion.identity);
        return instance.GetComponent<Enemy>();
    }
}
```

### **5. Adapter Pattern (Test → Game Profile)**
```gdscript
class_name PhobiaAdapter
extends Node

func adapt_test_responses(responses: Array) -> Dictionary:
    var profile = {
        "socialPhobia": _calculate_score(responses, "social"),
        "arachnophobia": _calculate_score(responses, "arachnophobia"),
        "aquaphobia": _calculate_score(responses, "aqua")
    }
    return profile

func _calculate_score(responses: Array, type: String) -> float:
    var score = 0.0
    # ... scoring logic
    return score
```

### **6. Strategy Pattern (Dialogue Adaptation)**
```gdscript
class_name DialogueStrategy
extends Node

var strategy: Callable

func execute_dialogue(context: Dictionary) -> String:
    return strategy.call(context)

# En DialogueSystem:
if profession == "programmer":
    dialogue_strategy = func(ctx): return "Trabajar 12 horas en código..."
else:
    dialogue_strategy = func(ctx): return "¿Cómo ha sido tu semana?"
```

---

## **VIII. FLUJO DE DATOS (DATA FLOW DIAGRAM)**

```
┌────────────┐
│  Player    │
│  Input     │
└─────┬──────┘
      │
      ▼
┌────────────────────┐
│ PlayerController   │
│ - Process Input    │
│ - Move player      │
└─────┬──────────────┘
      │
      ├─────────────────────┐
      │                     │
      ▼                     ▼
┌──────────────┐      ┌──────────────┐
│ Collision    │      │ GameManager  │
│ Detection    │      │ - Track State│
└──────┬───────┘      └──────┬───────┘
       │                     │
       └─────────┬───────────┘
                 │
                 ▼
        ┌────────────────┐
        │ Event Dispatch │
        │ (Signals)      │
        └────────┬───────┘
                 │
         ┌───────┴────────┐
         │                │
         ▼                ▼
    ┌────────┐      ┌─────────┐
    │ UIUpdate│      │Gameplay │
    │ Manager │      │Effects  │
    └────────┘      └─────────┘
         │                │
         ▼                ▼
    ┌────────┐      ┌─────────┐
    │UI      │      │Audio    │
    │Render  │      │Effect   │
    └────────┘      └─────────┘
```

---

## **IX. PERFORMANCE Y OPTIMIZACIONES**

### **Target Performance**
- **FPS:** 60 FPS (1080p), 30 FPS (console)
- **Latencia de Input:** < 50ms
- **Tiempo de carga:** < 3 minutos
- **Memoria:** < 2GB (PC), < 1GB (console target)

### **Técnicas de Optimización**
1. **LOD (Level of Detail):** Apartamento se simplifica en distancia
2. **Culling:** Objetos fuera de cámara no se renderizan
3. **Object Pooling:** Enemigos reutilizados en lugar de crear/destruir
4. **Profiling:** Uso de Unity Profiler y Frame Debugger para identificar cuellos de botella
5. **Shader Caching:** Compilar shaders en tiempo de desarrollo

### **Memory Budget**
| Resource | Budget |
|----------|--------|
| Texturas | 800 MB |
| Audio | 500 MB |
| Modelos 3D | 400 MB |
| Scripts | 100 MB |
| UI Assets | 50 MB |
| **Total** | **~1.85 GB** |

---

## **X. SEGURIDAD Y PROTECCIÓN**

### **Save Game Validation**
```gdscript
func validate_save_file(save_data: Dictionary) -> bool:
    # Verificar estructura
    if not save_data.has("version"):
        return false
    
    # Verificar checksum
    var checksum = _calculate_checksum(save_data)
    return checksum == save_data.get("checksum")

func _calculate_checksum(data: Dictionary) -> String:
    # Simple: MD5 de campos críticos
    return MD5.new().update(str(data["playerState"])).digest()
```

### **Antifraud (Opcional)**
- No permitir modificación de `sanity` manualmente
- Validar consistencia de tests (no respuestas contradictorias)
- Detectar speedhack (tiempo de juego inconsistente)

### **Privacy**
- Datos de jugador se guardan **localmente** por defecto
- Analytics opcional, **completamente anónimo**
- No recopilar datos personales más allá de nombre de usuario

---

## **XI. TESTING STRATEGY**

### **Unit Tests (Unity Test Framework / NUnit)**
```csharp
using NUnit.Framework;
using UnityEngine;

[TestFixture]
public class GameManagerTests
{
    [Test]
    public void TestSanityDrain()
    {
        var gm = new GameObject().AddComponent<GameManager>();
        float initialSanity = gm.sanity;
        
        gm.ApplySanityDamage(10.0f);
        
        Assert.AreEqual(initialSanity - 10.0f, gm.sanity, 0.01f);
    }
    
    [Test]
    public void TestPhobiaDetection()
    {
        var testSystem = new GameObject().AddComponent<TestSystem>();
        int[] responses = {3, 3, 3, 3, 3, 3, 3, 3, 3, 3}; // Max score
        
        var phobia = testSystem.AnalyzeResponses(responses);
        Assert.IsTrue(phobia.ContainsKey("socialPhobia"));
    }
}
```

### **Integration Tests**
- Flujo completo: Start → Test → Encounter → Save
- Cinemáticas reproducen correctamente
- Diálogos se adaptan según datos guardados

### **Playtesting (Manual)**
- 10-15 jugadores externos
- Recopilar feedback sobre:
  - Claridad narrativa
  - Dificultad y pacing
  - Comprensión de mecánicas
  - Respuesta emocional

---

## **XII. DIAGRAMA DE DESPLIEGUE**

```
┌─────────────────────────────────────────┐
│         User's Machine                  │
├─────────────────────────────────────────┤
│  ┌──────────────────────────────────┐   │
│  │  Unity Runtime (Player)          │   │
│  │  ┌────────────────────────────┐  │   │
│  │  │ PSYCHE Game (Executable)   │  │   │
│  │  │ - C# Compiled Code         │  │   │
│  │  │ - Assets (3D, Audio, UI)   │  │   │
│  │  │ - SaveGame Data (JSON)     │  │   │
│  │  └────────────────────────────┘  │   │
│  └──────────────────────────────────┘   │
│                                         │
│  ┌────────────────────────────────────┐ │
│  │ Godot Runtime Config               │ │
│  │ - Graphics Settings                │ │
│  │ - Input Mapping                    │ │
│  │ - Audio Configuration              │ │
│  └────────────────────────────────────┘ │
│                                         │
│  ┌────────────────────────────────────┐ │
│  │ Local Filesystem                   │ │
│  │ - user://saves/ (SaveGames)        │ │
│  │ - user://settings/ (Config)        │ │
│  └────────────────────────────────────┘ │
└─────────────────────────────────────────┘
         │
         │ (Optional)
         ▼
┌─────────────────────────────────────────┐
│    Analytics Server (Node.js/Backend)   │
├─────────────────────────────────────────┤
│ - Recolectar datos anónimos             │
│ - Almacenar en SQLite/PostgreSQL        │
│ - API REST para dashboards              │
└─────────────────────────────────────────┘
```

---

## **XIII. DOCUMENTACIÓN Y REFERENCIAS TÉCNICAS**

### **Unity Documentation**
- https://docs.unity3d.com/
- Unity Scripting API (C#)
- UnityEvents and Delegates
- GameObject/Component Architecture
- Unity Manual and Tutorials

### **Arquitectura Software**
- SOLID Principles
- Design Patterns (Gang of Four)
- MVC/MVVM Patterns

### **Convenciones de Código**

**Naming (Convenciones de C# Unity):**
- PascalCase: Clases, Métodos públicos, Propiedades
- camelCase: Variables locales, parámetros
- _camelCase: Variables privadas (comienzan con _)
- [SerializeField]: Propiedades editables en inspector

**Ejemplo:**
```csharp
public class EnemySpawner : MonoBehaviour
{
    private const int MAX_ENEMIES = 5;
    
    [SerializeField]
    private float spawnTimer;
    
    private int _currentEnemyCount = 0;
    
    private void Start()
    {
        InitializeSpawnTimer();
    }
    
    private void InitializeSpawnTimer()
    {
        // ...
    }
}
```

---

**Arquitectura Técnica: Completa y lista para implementación**

