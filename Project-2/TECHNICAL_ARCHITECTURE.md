# TECHNICAL ARCHITECTURE - PHOBIA
## Especificación de Ingeniería de Software - Unreal Engine 5.7

---

## **I. STACK TECNOLÓGICO**

### **Frontend / Game Engine**
- **Motor Base:** Unreal Engine 5.7
  - Razones: Nanite/Lumen para gráficos AAA, MetaHuman para personajes realistas, Niagara VFX, Blueprint Visual Scripting, ecosistema FAB (Formerly Marketplace)
  - Versión mínima: 5.5
  - Versión recomendada: Unreal Engine 5.7

### **Lenguaje Principal**
- **Blueprint Visual Scripting** (sistema principal de desarrollo)
  - Para lógica de gameplay, IA, UI, y sistemas de juego
  - C++ opcional para optimizaciones críticas y sistemas complejos
- **C++** (opcional, para sistemas core de alto rendimiento)
  - Framework: Unreal Engine Core
  - IDE recomendado: Visual Studio 2022 o JetBrains Rider
  - Estándar: C++20

### **Backend / Datos**
- **Persistencia local:** SaveGame Object (UE nativo) serializado a binario
- **Base de datos:** SQLite (opcional, para analytics)
- **Servidor opcional:** Node.js + Express o AWS GameLift (para estadísticas anónimas)

### **Audio**
- **Audio Engine:** MetaSounds (sistema nativo UE5)
- **Integraciones:** Wwise o FMOD Studio (opcional para audio espacial avanzado)
- **Formato:** OGG Vorbis / Opus (comprimido), WAV (lossless en desarrollo)
- **Audio Attenuation:** Curvas de atenuación 3D personalizadas

### **Sistemas Nativos de Unreal**
- **Dialogue System:** Audio Dialogue Waves + Data Tables
- **SaveGame Manager:** USaveGame Class (Blueprint compatible)
- **StateMachine:** Behavior Trees + State Machines (Animation Blueprints)
- **UI Framework:** UMG (Unreal Motion Graphics) con Common UI
- **Animation:** Control Rig + Animation Blueprints
- **AI:** Behavior Trees + EQS (Environment Query System)

### **Control de Versiones**
- **VCS:** Git + GitHub / Perforce (recomendado para assets binarios grandes)
- **Branching:** Git Flow
  - `main` → Builds estables
  - `develop` → Integración
  - `feature/*` → Features individuales
  - `release/*` → Preparación de lanzamiento
  - `hotfix/*` → Parches críticos
- **LFS:** Git Large File Storage para assets (.uasset, .umap)

---

## **II. DIAGRAMA DE ARQUITECTURA GENERAL (C4 Model)**

```
┌─────────────────────────────────────────────────────┐
│            PHOBIA - UNREAL ENGINE 5.7               │
├─────────────────────────────────────────────────────┤

┌──────────────────────────────────────┐
│        UNREAL ENGINE 5.7             │
│  ┌────────────────────────────────┐  │
│  │  Rendering (Nanite + Lumen)   │  │
│  ├────────────────────────────────┤  │
│  │  Physics (Chaos Physics)       │  │
│  ├────────────────────────────────┤  │
│  │  Audio (MetaSounds)            │  │
│  ├────────────────────────────────┤  │
│  │  Niagara VFX System            │  │
│  └────────────────────────────────┘  │
│                                      │
│  ┌──────────┐  ┌──────────┐         │
│  │Blueprint │  │   C++    │         │
│  │ Scripts  │  │  (Core)  │         │
│  └──────────┘  └──────────┘         │
└──────────────────────────────────────┘
          ↓
┌──────────────────────────────────────┐
│    Application Layer (Game Logic)    │
├──────────────────────────────────────┤
│  • BP_GameMode (Game Rules)          │
│  • BP_GameState (Persistent State)   │
│  • BP_PlayerController (Input)       │
│  • BP_PlayerCharacter (Pawn)         │
│  • BP_EnemyAI + Behavior Trees       │
│  • BP_TestSystem (Psychometric)      │
│  • BP_DialogueManager                │
│  • BP_SaveGameManager                │
│  • BP_AudioManager                   │
│  • UMG_MainHUD (UI)                  │
└──────────────────────────────────────┘
          ↓
┌──────────────────────────────────────┐
│     Data / Persistence Layer         │
├──────────────────────────────────────┤
│  • SaveGame Object (Binary)          │
│  • Data Tables (CSV/JSON)            │
│  • Data Assets (Config)              │
│  • Level Streaming (Persistent)      │
│  • SQLite DB (Optional - Analytics)  │
└──────────────────────────────────────┘
          ↓ (Optional)
┌──────────────────────────────────────┐
│    Backend / Analytics Server        │
├──────────────────────────────────────┤
│  • Node.js + Express / AWS GameLift  │
│  • Recolectar datos anónimos         │
│  • Análisis de comportamiento        │
│  • Estadísticas de finales           │
└──────────────────────────────────────┘
```

---

## **III. DIAGRAMA DE BLUEPRINTS: CLASES PRINCIPALES**

### **A. Core System Blueprints**

```
┌──────────────────────────────────────┐
│     BP_GameInstance                  │
│   (Persists across levels)           │
├──────────────────────────────────────┤
│ Variables:                           │
│ - Sanity: Float (80.0)               │
│ - CurrentAct: E_ActType (Enum)       │
│ - PlayerPhobias: Map<String, Float>  │
│ - TestHistory: Array<F_TestResult>   │
│ - ElapsedTime: Float                 │
│ - SaveGameRef: BP_SaveGame           │
│                                      │
│ Functions:                           │
│ + GetSanity() → Float                │
│ + SetSanity(Value: Float)            │
│ + OnTestCompleted(Test: F_TestData)  │
│ + SpawnEnemy(Type: E_EnemyType)      │
│ + SaveGame(Slot: Int)                │
│ + LoadGame(Slot: Int)                │
│ + OnGameStateChanged()               │
│                                      │
│ Event Dispatchers:                   │
│ + OnSanityChanged(NewValue: Float)   │
│ + OnEnemySpawned(Type, Location)     │
│ + OnTestCompleted(Results)           │
│ + OnGameSaved(Success: Bool)         │
│ + OnActChanged(NewAct: E_ActType)    │
└──────────────────────────────────────┘
         △
         │ references
         │
    ┌────┴─────┬──────────┬───────────┐
    │          │          │           │
    ▼          ▼          ▼           ▼
┌─────────┐┌─────────┐┌─────────┐┌─────────┐
│BP_Player││BP_Enemy ││BP_Test  ││BP_Dialog│
│Character││  AI     ││System   ││Manager  │
└─────────┘└─────────┘└─────────┘└─────────┘
```

### **B. Blueprint BP_PlayerCharacter**

```
┌────────────────────────────────────────┐
│     BP_PlayerCharacter                 │
│   (Parent: Character)                  │
├────────────────────────────────────────┤
│ Components:                            │
│ - CameraComponent                      │
│ - SpringArmComponent                   │
│ - CharacterMovement                    │
│ - HealthComponent (Custom)             │
│ - SanityComponent (Custom)             │
│ - AudioComponent                       │
│                                        │
│ Variables:                             │
│ - WalkSpeed: Float (150.0)             │
│ - SprintSpeed: Float (300.0)           │
│ - CurrentSanity: Float                 │
│ - AnchorsFound: Int (0)                │
│ - InSafeZone: Bool (false)             │
│ - IsAlive: Bool (true)                 │
│ - ThreatLevel: Float (0.0)             │
│                                        │
│ Functions:                             │
│ + BeginPlay()                          │
│ + Tick(DeltaTime)                      │
│ + HandleMovementInput()                │
│ + HandleLookInput()                    │
│ + Sprint()                             │
│ + StopSprinting()                      │
│ + TakeSanityDamage(Amount: Float)      │
│ + RegenerateSanity(Rate: Float)        │
│ + OnAnchorFound(Anchor: Actor)         │
│ + DetectNearbyThreat() → Bool          │
│ + Die()                                │
│                                        │
│ Event Dispatchers:                     │
│ + OnAnchorFound                        │
│ + OnThreatDetected                     │
│ + OnPlayerDied                         │
│ + OnSanctuaryEntered                   │
│ + OnSanctuaryExited                    │
└────────────────────────────────────────┘
```

### **C. Blueprint BP_EnemyBase (Polimórfico)**

```
┌────────────────────────────────────────┐
│     BP_EnemyBase                       │
│  (Parent: Character - Abstract)        │
├────────────────────────────────────────┤
│ Components:                            │
│ - SkeletalMeshComponent                │
│ - AIController (Custom)                │
│ - PawnSensing                          │
│ - AudioComponent                       │
│ - NiagaraComponent (VFX)               │
│                                        │
│ Variables:                             │
│ - EnemyType: E_EnemyType               │
│ - MoveSpeed: Float (200.0)             │
│ - DetectionRange: Float (1500.0)       │
│ - AttackRange: Float (200.0)           │
│ - SanityDamageRate: Float (5.0/s)      │
│ - IsPersistent: Bool (true)            │
│ - CurrentState: E_AIState              │
│ - TargetPlayer: BP_PlayerCharacter     │
│ - BehaviorTree: BT_EnemyAI             │
│                                        │
│ Functions:                             │
│ + BeginPlay()                          │
│ + Tick(DeltaTime)                      │
│ + OnPlayerDetected(Player)             │
│ + OnPlayerLost()                       │
│ + MoveToTarget(Location: Vector)       │
│ + AttackPlayer()                       │
│ + PlaySpawnAnimation()                 │
│ + PlayChaseSound()                     │
│                                        │
│ Events (Implementable):                │
│ + OnSpawn() [Blueprint Implementable]  │
│ + OnDetected() [Blueprint Implementable│
│ + OnAttack() [Blueprint Implementable] │
│                                        │
│ Event Dispatchers:                     │
│ + OnSpawned                            │
│ + OnDetectedPlayer                     │
│ + OnLostPlayer                         │
│ + OnAttackedPlayer                     │
└────────────────────────────────────────┘
         △
         │ inherits
    ┌────┴────┬────────┬──────────┬──────────┐
    │         │        │          │          │
    ▼         ▼        ▼          ▼          ▼
  BP_     BP_      BP_Water  BP_Facial  BP_Generic
  Spider  Specter  Entity    Entity     Spirit
```

### **D. Blueprint BP_TestSystem**

```
┌────────────────────────────────────────┐
│     BP_TestSystem                      │
│   (Parent: Actor)                      │
├────────────────────────────────────────┤
│ Variables:                             │
│ - CurrentTest: F_TestData              │
│ - AllTests: Map<E_TestType, DataTable> │
│ - PlayerResponses: Array<Int>          │
│ - PhobiaProfile: Map<String, Float>    │
│ - TestInProgress: Bool                 │
│ - CurrentQuestionIndex: Int            │
│                                        │
│ Data Tables:                           │
│ - DT_ScreeningTest (DataTable)         │
│ - DT_BeckTest (DataTable)              │
│ - DT_ZungTest (DataTable)              │
│                                        │
│ Functions:                             │
│ + StartTest(Type: E_TestType)          │
│ + SubmitAnswer(Answer: Int)            │
│ + CalculateScore() → Int               │
│ + GeneratePhobiaProfile()              │
│ + GetNextPhobia() → E_EnemyType        │
│ + SaveTestResults()                    │
│ + LoadNextQuestion()                   │
│                                        │
│ Event Dispatchers:                     │
│ + OnTestStarted(Type: E_TestType)      │
│ + OnQuestionDisplayed(Question: Text)  │
│ + OnTestCompleted(Results)             │
│ + OnPhobiaDetected(Type, Intensity)    │
│ + OnProfileGenerated(Profile)          │
└────────────────────────────────────────┘
```

### **E. Blueprint BP_DialogueManager**

```
┌────────────────────────────────────────┐
│     BP_DialogueManager                 │
│   (Parent: Actor)                      │
├────────────────────────────────────────┤
│ Variables:                             │
│ - DialogueDataTable: DT_Dialogues      │
│ - CurrentDialogue: F_DialogueNode      │
│ - PlayerName: String                   │
│ - PlayerProfession: String             │
│ - ConversationLog: Array<F_DialogueLine│
│ - IsDialoguePlaying: Bool              │
│ - CurrentSpeaker: E_SpeakerType        │
│                                        │
│ Components:                            │
│ - AudioComponent (Voice)               │
│                                        │
│ Functions:                             │
│ + LoadDialogue(DialogueID: Name)       │
│ + AdaptDialogue(Context: Map)          │
│ + PlayDialogue()                       │
│ + GetNextChoice() → Array<FText>       │
│ + SelectChoice(ChoiceID: Int)          │
│ + SubstituteVariables(Text) → FText    │
│ + PlayVoiceOver(Sound: USoundWave)     │
│                                        │
│ Event Dispatchers:                     │
│ + OnDialogueStarted                    │
│ + OnDialogueEnded                      │
│ + OnChoicePresented(Choices)           │
│ + OnDialogueProgressed(Line)           │
└────────────────────────────────────────┘
```

### **F. Blueprint BP_SaveGame**

```
┌────────────────────────────────────────┐
│     BP_SaveGame                        │
│   (Parent: USaveGame)                  │
├────────────────────────────────────────┤
│ Variables (Saved):                     │
│ - SaveVersion: String ("1.0")          │
│ - PlayerName: String                   │
│ - Profession: String                   │
│ - CreatedAt: DateTime                  │
│ - LastPlayedAt: DateTime               │
│ - PlayTime: Float                      │
│ - CurrentAct: E_ActType                │
│                                        │
│ - PlayerState: F_PlayerState           │
│   • Position: Vector                   │
│   • Rotation: Rotator                  │
│   • Sanity: Float                      │
│   • Health: Float                      │
│   • AnchorsFound: Array<Int>           │
│                                        │
│ - TestHistory: Array<F_TestResult>     │
│ - PhobiaProfile: Map<String, Float>    │
│ - EnemiesEncountered: Array<F_Encounter│
│ - DialogueLog: Array<F_DialogueLine>   │
│ - GameSettings: F_GameSettings         │
│ - Checksum: String                     │
└────────────────────────────────────────┘
```

### **G. Blueprint BP_SaveGameManager**

```
┌────────────────────────────────────────┐
│     BP_SaveGameManager                 │
│   (Parent: Actor - Singleton)          │
├────────────────────────────────────────┤
│ Variables:                             │
│ - SaveSlotName: String ("SaveSlot")    │
│ - CurrentSaveSlot: Int (0)             │
│ - SaveGameObject: BP_SaveGame          │
│                                        │
│ Functions:                             │
│ + SaveGame(SlotIndex: Int) → Bool      │
│ + LoadGame(SlotIndex: Int) → Bool      │
│ + DeleteSave(SlotIndex: Int)           │
│ + GetSaveMetadata(Slot) → F_Metadata   │
│ + DoesSaveExist(Slot: Int) → Bool      │
│ + SerializeGameState() → BP_SaveGame   │
│ + DeserializeGameState(SaveData)       │
│ + ValidateSaveFile(Slot) → Bool        │
│ + CalculateChecksum(Data) → String     │
│                                        │
│ Event Dispatchers:                     │
│ + OnGameSaved(Success: Bool)           │
│ + OnGameLoaded(Success: Bool)          │
│ + OnSaveDeleted                        │
│ + OnSaveCorrupted                      │
└────────────────────────────────────────┘
```

### **H. UMG Widget: WBP_MainHUD**

```
┌────────────────────────────────────────┐
│     WBP_MainHUD                        │
│   (Parent: UserWidget)                 │
├────────────────────────────────────────┤
│ Widget Components:                     │
│ - ProgressBar_Sanity                   │
│ - TextBlock_AnchorCount                │
│ - Image_ThreatIndicator                │
│ - CanvasPanel_Main                     │
│ - Overlay_Distortion                   │
│                                        │
│ Variables:                             │
│ - CurrentSanity: Float                 │
│ - MaxSanity: Float (100.0)             │
│ - AnchorsFound: Int                    │
│ - ThreatActive: Bool                   │
│                                        │
│ Functions:                             │
│ + NativeConstruct()                    │
│ + UpdateSanityBar(Value: Float)        │
│ + UpdateAnchorCount(Count: Int)        │
│ + ShowThreatWarning()                  │
│ + HideThreatWarning()                  │
│ + ApplyDistortionEffect(Intensity)     │
│ + SetColorblindMode(Mode: E_CBMode)    │
│                                        │
│ Animations:                            │
│ - Anim_ThreatPulse                     │
│ - Anim_SanityDrain                     │
│ - Anim_DistortionWave                  │
└────────────────────────────────────────┘
```

---

## **IV. BEHAVIOR TREE: AI DEL ENEMIGO**

```
BT_EnemyAI (Behavior Tree)
│
├─ Selector (Root)
│  │
│  ├─ Sequence: "Attack Player"
│  │  ├─ Decorator: IsPlayerInAttackRange?
│  │  ├─ Task: PlayAttackAnimation
│  │  ├─ Task: DealSanityDamage
│  │  └─ Task: PlayAttackSound
│  │
│  ├─ Sequence: "Chase Player"
│  │  ├─ Decorator: CanSeePlayer?
│  │  ├─ Task: MoveToPlayer
│  │  ├─ Task: UpdateChaseSpeed
│  │  └─ Task: PlayChaseSound
│  │
│  ├─ Sequence: "Search For Player"
│  │  ├─ Decorator: HeardPlayer?
│  │  ├─ Task: MoveToLastKnownPosition
│  │  ├─ Task: LookAround
│  │  └─ Wait: 2.0 seconds
│  │
│  └─ Sequence: "Patrol"
│     ├─ Task: GetRandomPatrolPoint (EQS)
│     ├─ Task: MoveToLocation
│     └─ Wait: 3.0 seconds

Blackboard Keys:
- TargetPlayer: Object (BP_PlayerCharacter)
- LastKnownPlayerLocation: Vector
- CurrentState: Enum (E_AIState)
- DetectionRadius: Float (1500.0)
- AttackRadius: Float (200.0)
- PatrolPoint: Vector
```

### **Environment Query System (EQS)**

```
EQS_FindPatrolPoint
│
├─ Generator: Points in Radius
│  └─ Radius: 2000 units
│
├─ Tests:
│  ├─ Distance to Player (Weight: 0.3)
│  ├─ Path Exists (Weight: 0.5)
│  └─ Visibility (Weight: 0.2)
│
└─ Scoring: Weighted Sum
```

---

## **V. SISTEMA DE PERSISTENCIA (SAVE GAME)**

### **Estructura de F_PlayerState (Struct)**

```cpp
USTRUCT(BlueprintType)
struct FPlayerState
{
    GENERATED_BODY()
    
    UPROPERTY(BlueprintReadWrite)
    FVector Position;
    
    UPROPERTY(BlueprintReadWrite)
    FRotator Rotation;
    
    UPROPERTY(BlueprintReadWrite)
    float Sanity;
    
    UPROPERTY(BlueprintReadWrite)
    float Health;
    
    UPROPERTY(BlueprintReadWrite)
    TArray<int32> AnchorsFound;
    
    UPROPERTY(BlueprintReadWrite)
    int32 AnchorsCollected;
    
    UPROPERTY(BlueprintReadWrite)
    bool IsAlive;
};
```

### **Blueprint SaveGame Flow**

```
┌─────────────────────────┐
│ Player presses "Save"   │
└───────────┬─────────────┘
            │
            ▼
┌─────────────────────────────────┐
│ BP_SaveGameManager              │
│ → CreateSaveGameObject()        │
└───────────┬─────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│ Collect data from:              │
│ - BP_GameInstance               │
│ - BP_PlayerCharacter            │
│ - BP_TestSystem                 │
│ - BP_DialogueManager            │
└───────────┬─────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│ Populate BP_SaveGame object     │
│ with F_PlayerState, etc.        │
└───────────┬─────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│ Calculate Checksum              │
│ (MD5 hash of critical data)     │
└───────────┬─────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│ SaveGameToSlot()                │
│ (UE function - binary file)     │
└───────────┬─────────────────────┘
            │
            ▼
┌─────────────────────────────────┐
│ Dispatch OnGameSaved event      │
│ Show "Game Saved" notification  │
└─────────────────────────────────┘
```

---

## **VI. EVENT SYSTEM (EVENT DISPATCHERS)**

### **Event Dispatcher Map**

```
BP_GameInstance (Central Hub):
├─ OnSanityChanged(NewValue: Float)
├─ OnEnemySpawned(Type: E_EnemyType, Location: Vector)
├─ OnEnemyDefeated(Enemy: BP_EnemyBase)
├─ OnTestStarted(Type: E_TestType)
├─ OnTestCompleted(Results: F_TestResult)
├─ OnAnchorFound(AnchorID: Int)
├─ OnDialogueTriggered(DialogueID: Name)
├─ OnActChanged(NewAct: E_ActType)
├─ OnGameSaved(SlotIndex: Int)
├─ OnGameLoaded(SlotIndex: Int)
├─ OnThreatDetected()
├─ OnThreatLost()
└─ OnEndingReached(EndingType: E_EndingType)

BP_PlayerCharacter:
├─ OnMoved(NewPosition: Vector)
├─ OnSanctuaryEntered()
├─ OnSanctuaryExited()
├─ OnThreatDetected()
├─ OnSanityDamageTaken(Amount: Float)
└─ OnPlayerDied()

BP_EnemyBase:
├─ OnSpawned(Location: Vector)
├─ OnDetectedPlayer()
├─ OnLostPlayer()
├─ OnAttackedPlayer()
└─ OnDestroyed()

BP_TestSystem:
├─ OnQuestionDisplayed(Question: FText)
├─ OnAnswerSubmitted(Choice: Int)
├─ OnTestCompleted(Score: Int, Phobias: Map)
└─ OnPhobiaDetected(Type: String, Intensity: Float)

WBP_MainHUD:
├─ OnSanityBarUpdated(Value: Float)
├─ OnThreatIndicatorActivated()
├─ OnDialoguePanelShown()
├─ OnMenuOpened()
└─ OnMenuClosed()

BP_AudioManager:
├─ OnMusicTrackChanged(Track: USoundBase)
├─ OnSoundEffectPlayed(SFX: USoundBase)
├─ OnSpatialAudioUpdated(Location: Vector)
└─ OnDialogueVoiceStarted()
```

---

## **VII. DATA STRUCTURES (STRUCTS & ENUMS)**

### **Enumerations**

```cpp
// EnemyType Enum
UENUM(BlueprintType)
enum class E_EnemyType : uint8
{
    GenericSpirit   UMETA(DisplayName = "Generic Spirit"),
    Spider          UMETA(DisplayName = "Arachnophobia"),
    Specter_Crowd   UMETA(DisplayName = "Social Phobia"),
    WaterEntity     UMETA(DisplayName = "Aquaphobia"),
    FacialEntity    UMETA(DisplayName = "Facial Recognition"),
    PhoneMonster    UMETA(DisplayName = "Nomophobia")
};

// ActType Enum
UENUM(BlueprintType)
enum class E_ActType : uint8
{
    Act1_Screening  UMETA(DisplayName = "Act 1: Screening"),
    Act2_Beck       UMETA(DisplayName = "Act 2: Beck Test"),
    Act3_Zung       UMETA(DisplayName = "Act 3: Zung Test"),
    Act4_Finale     UMETA(DisplayName = "Act 4: Finale")
};

// AIState Enum
UENUM(BlueprintType)
enum class E_AIState : uint8
{
    Idle        UMETA(DisplayName = "Idle/Patrol"),
    Searching   UMETA(DisplayName = "Searching"),
    Chasing     UMETA(DisplayName = "Chasing"),
    Attacking   UMETA(DisplayName = "Attacking")
};

// TestType Enum
UENUM(BlueprintType)
enum class E_TestType : uint8
{
    Screening   UMETA(DisplayName = "Initial Screening"),
    Beck        UMETA(DisplayName = "Beck Anxiety"),
    Zung        UMETA(DisplayName = "Zung Depression")
};
```

### **Structures**

```cpp
// F_TestResult
USTRUCT(BlueprintType)
struct FTestResult
{
    GENERATED_BODY()
    
    UPROPERTY(BlueprintReadWrite)
    E_TestType TestType;
    
    UPROPERTY(BlueprintReadWrite)
    FDateTime CompletedAt;
    
    UPROPERTY(BlueprintReadWrite)
    TArray<int32> Responses;
    
    UPROPERTY(BlueprintReadWrite)
    int32 Score;
    
    UPROPERTY(BlueprintReadWrite)
    FString Severity; // "mild", "moderate", "severe"
};

// F_DialogueLine
USTRUCT(BlueprintType)
struct FDialogueLine
{
    GENERATED_BODY()
    
    UPROPERTY(BlueprintReadWrite)
    FString Speaker;
    
    UPROPERTY(BlueprintReadWrite)
    FText LineText;
    
    UPROPERTY(BlueprintReadWrite)
    USoundWave* VoiceOver;
    
    UPROPERTY(BlueprintReadWrite)
    FDateTime Timestamp;
};

// F_EnemyEncounter
USTRUCT(BlueprintType)
struct FEnemyEncounter
{
    GENERATED_BODY()
    
    UPROPERTY(BlueprintReadWrite)
    E_EnemyType Type;
    
    UPROPERTY(BlueprintReadWrite)
    FDateTime EncounteredAt;
    
    UPROPERTY(BlueprintReadWrite)
    bool Escaped;
    
    UPROPERTY(BlueprintReadWrite)
    float SanityLost;
};
```

---

## **VIII. PERFORMANCE Y OPTIMIZACIONES**

### **Target Performance**
- **FPS:** 60 FPS (1080p PC), 30 FPS (Console - PS5/XSX)
- **Latencia de Input:** < 50ms
- **Tiempo de carga:** < 45 segundos (con SSDs)
- **Memoria:** < 4GB (PC), < 3GB (console target)

### **Técnicas de Optimización Unreal**
1. **Nanite:** Geometría virtualizada automática (no necesita LODs manuales)
2. **Lumen:** Global Illumination dinámica (sin baking)
3. **World Partition:** Streaming automático de niveles grandes
4. **HLOD (Hierarchical LOD):** Simplificación automática de assets distantes
5. **Object Pooling:** Sistema de pooling para enemigos y VFX
6. **Async Loading:** Cargar assets en background
7. **Occlusion Culling:** Precomputed Visibility Volumes
8. **GPU Profiling:** Unreal Insights para identificar cuellos de botella

### **Memory Budget**
| Resource | Budget |
|----------|--------|
| Texturas (con streaming) | 1.5 GB |
| Audio (MetaSounds) | 600 MB |
| Skeletal Meshes | 500 MB |
| Blueprints/Logic | 200 MB |
| Niagara VFX | 300 MB |
| UI/UMG | 100 MB |
| **Total** | **~3.2 GB** |

### **Shader Compilation**
- Usar Shader Model 6.0+
- PSO (Pipeline State Object) caching
- Async Shader Compilation activado

---

## **IX. BLUEPRINT BEST PRACTICES**

### **Naming Conventions**

```
Prefixes:
- BP_       → Blueprint Classes
- WBP_      → UMG Widgets
- BT_       → Behavior Trees
- BB_       → Blackboards
- EQS_      → Environment Queries
- DT_       → Data Tables
- E_        → Enums
- F_        → Structs
- M_        → Materials
- MI_       → Material Instances
- T_        → Textures
- SM_       → Static Meshes
- SK_       → Skeletal Meshes
- A_        → Animation Assets
- AB_       → Animation Blueprints
- NS_       → Niagara Systems

Examples:
- BP_PlayerCharacter
- WBP_MainHUD
- BT_EnemyAI
- DT_DialogueData
- E_EnemyType
- F_TestResult
```

### **Blueprint Organization**

```
Content/
├─ Blueprints/
│  ├─ Characters/
│  │  ├─ Player/
│  │  │  └─ BP_PlayerCharacter
│  │  └─ Enemies/
│  │     ├─ BP_EnemyBase
│  │     ├─ BP_Spider
│  │     └─ BP_Specter
│  ├─ GameModes/
│  │  ├─ BP_GameMode
│  │  └─ BP_GameInstance
│  ├─ Systems/
│  │  ├─ BP_TestSystem
│  │  ├─ BP_DialogueManager
│  │  └─ BP_SaveGameManager
│  └─ UI/
│     ├─ WBP_MainHUD
│     ├─ WBP_MainMenu
│     └─ WBP_TestInterface
├─ Data/
│  ├─ DataTables/
│  │  ├─ DT_ScreeningTest
│  │  └─ DT_Dialogues
│  └─ DataAssets/
│     └─ DA_GameSettings
├─ AI/
│  ├─ BehaviorTrees/
│  │  └─ BT_EnemyAI
│  ├─ Blackboards/
│  │  └─ BB_EnemyData
│  └─ EQS/
│     └─ EQS_FindPatrolPoint
└─ Materials/
   ├─ M_Character
   └─ MI_Enemy_Specter
```

### **Blueprint Performance Tips**

1. **Evitar Tick cuando sea posible:**
   - Usar Timers en lugar de Tick
   - Usar Event Dispatchers para comunicación
   
2. **Cast Optimization:**
   - Usar Interfaces en lugar de Casts repetidos
   - Cachear referencias en BeginPlay

3. **Macros y Functions:**
   - Usar Functions para lógica reutilizable
   - Macros para operaciones simples sin overhead

4. **Async Operations:**
   - Usar Async Loading para assets grandes
   - Delay nodes para operaciones costosas

---

## **X. C++ INTEGRATION (OPCIONAL)**

### **Cuándo usar C++ vs Blueprint**

**Usar Blueprint para:**
- Lógica de gameplay
- Prototyping rápido
- UI/UX interactions
- Event handling
- Configuración de assets

**Usar C++ para:**
- Sistemas core de alto rendimiento
- Math operations intensivas
- Custom collision systems
- Multiplayer replication (futuro)
- Plugins y extensions

### **Ejemplo: Clase C++ Base**

```cpp
// PhobiaCharacter.h
#pragma once

#include "CoreMinimal.h"
#include "GameFramework/Character.h"
#include "PhobiaCharacter.generated.h"

UCLASS()
class PHOBIA_API APhobiaCharacter : public ACharacter
{
    GENERATED_BODY()

public:
    APhobiaCharacter();

protected:
    virtual void BeginPlay() override;

public:
    virtual void Tick(float DeltaTime) override;
    virtual void SetupPlayerInputComponent(class UInputComponent* PlayerInputComponent) override;

    // Sanity System
    UPROPERTY(BlueprintReadWrite, Category = "Sanity")
    float CurrentSanity;

    UPROPERTY(BlueprintReadWrite, Category = "Sanity")
    float MaxSanity;

    UFUNCTION(BlueprintCallable, Category = "Sanity")
    void TakeSanityDamage(float Damage);

    UFUNCTION(BlueprintCallable, Category = "Sanity")
    void RegenerateSanity(float Rate);

    // Event Dispatchers
    DECLARE_DYNAMIC_MULTICAST_DELEGATE_OneParam(FOnSanityChanged, float, NewValue);
    UPROPERTY(BlueprintAssignable, Category = "Events")
    FOnSanityChanged OnSanityChanged;
};
```

```cpp
// PhobiaCharacter.cpp
#include "PhobiaCharacter.h"

APhobiaCharacter::APhobiaCharacter()
{
    PrimaryActorTick.bCanEverTick = true;
    CurrentSanity = 80.0f;
    MaxSanity = 100.0f;
}

void APhobiaCharacter::BeginPlay()
{
    Super::BeginPlay();
}

void APhobiaCharacter::Tick(float DeltaTime)
{
    Super::Tick(DeltaTime);
}

void APhobiaCharacter::SetupPlayerInputComponent(UInputComponent* PlayerInputComponent)
{
    Super::SetupPlayerInputComponent(PlayerInputComponent);
}

void APhobiaCharacter::TakeSanityDamage(float Damage)
{
    CurrentSanity = FMath::Clamp(CurrentSanity - Damage, 0.0f, MaxSanity);
    OnSanityChanged.Broadcast(CurrentSanity);
}

void APhobiaCharacter::RegenerateSanity(float Rate)
{
    CurrentSanity = FMath::Clamp(CurrentSanity + Rate, 0.0f, MaxSanity);
    OnSanityChanged.Broadcast(CurrentSanity);
}
```

---

## **XI. TESTING STRATEGY**

### **Automated Testing (Gauntlet Framework)**

```cpp
// PhobiaFunctionalTest.h
#pragma once

#include "CoreMinimal.h"
#include "FunctionalTest.h"
#include "PhobiaFunctionalTest.generated.h"

UCLASS()
class PHOBIA_API APhobiaFunctionalTest : public AFunctionalTest
{
    GENERATED_BODY()

public:
    UFUNCTION(BlueprintCallable)
    void TestSanitySystem();

    UFUNCTION(BlueprintCallable)
    void TestEnemySpawning();

    UFUNCTION(BlueprintCallable)
    void TestSaveGameSystem();
};
```

### **Blueprint Testing**

```
Test_SanityDrain (Blueprint)
│
├─ Arrange:
│  ├─ Spawn BP_PlayerCharacter
│  └─ Set initial sanity = 80
│
├─ Act:
│  └─ Call TakeSanityDamage(10)
│
├─ Assert:
│  └─ Check sanity == 70
│
└─ Cleanup:
   └─ Destroy test actors
```

### **Playtesting Metrics (Analytics)**

```cpp
// Track in BP_GameInstance
TMap<FString, int32> PlayerMetrics;

Metrics to Track:
- Deaths per enemy type
- Average sanity level
- Test completion time
- Anchors found rate
- Endings reached distribution
- Common paths taken
```

---

## **XII. DEPLOYMENT**

### **Build Configuration**

```
Development Build:
- Full debug symbols
- Console commands enabled
- Performance stats visible

Shipping Build:
- Optimized code (O2/O3)
- No debug info
- Encrypted pak files
- Anti-cheat integration (optional)
```

### **Platform Targets**

```
Primary: PC (Windows/Linux via Proton)
Secondary: PS5, Xbox Series X/S
Future: Steam Deck optimization
```

### **Packaging Settings**

```
Project Settings → Packaging:
- Use Pak File: True
- Encrypt Pak: True (Shipping)
- Compress: Zlib
- Include prerequisites: True
- Full Rebuild: False (iterative)
```

---
