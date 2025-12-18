# Hybrid Gene
## Technical Specification

**Version**: 1.0
**Last Updated**: December 2024
**Status**: Pre-Production

---

## 1. Architecture Overview

### 1.1 System Diagram

```
┌─────────────────────────────────────────────────────────────────┐
│                         GAME MANAGER                            │
│   ┌──────────┐  ┌──────────┐  ┌──────────┐  ┌──────────┐       │
│   │  State   │  │  Scene   │  │  Save    │  │  Audio   │       │
│   │ Machine  │  │ Manager  │  │ System   │  │ Manager  │       │
│   └────┬─────┘  └────┬─────┘  └────┬─────┘  └────┬─────┘       │
└────────┼─────────────┼─────────────┼─────────────┼─────────────┘
         │             │             │             │
         ▼             ▼             ▼             ▼
┌─────────────────────────────────────────────────────────────────┐
│                          CORE SYSTEMS                           │
│  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐       │
│  │  Combat   │ │ Breeding  │ │  Monster  │ │   World   │       │
│  │  Engine   │ │  System   │ │    AI     │ │  Manager  │       │
│  └─────┬─────┘ └─────┬─────┘ └─────┬─────┘ └─────┬─────┘       │
└────────┼─────────────┼─────────────┼─────────────┼─────────────┘
         │             │             │             │
         ▼             ▼             ▼             ▼
┌─────────────────────────────────────────────────────────────────┐
│                         DATA LAYER                              │
│  ┌───────────┐ ┌───────────┐ ┌───────────┐ ┌───────────┐       │
│  │ Monster   │ │  Species  │ │   Move    │ │   Item    │       │
│  │   Data    │ │   Data    │ │   Data    │ │   Data    │       │
│  └───────────┘ └───────────┘ └───────────┘ └───────────┘       │
└─────────────────────────────────────────────────────────────────┘
```

### 1.2 Game Loop (60 FPS Target)

```
while (running) {
    deltaTime = calculateDeltaTime()

    // Input
    inputManager.poll()

    // Update
    if (gameState == BATTLE) {
        combatEngine.update(deltaTime)
        monsterAI.update(deltaTime)
    }
    worldManager.update(deltaTime)

    // Render
    renderer.draw()

    // Audio
    audioManager.update()
}
```

---

## 2. Data Structures

### 2.1 Monster

```typescript
interface Monster {
    // Identity
    id: string                    // Unique identifier
    name: string                  // Display name
    speciesId: string             // Reference to Species
    generation: 1 | 2 | 3 | 4     // Generation tier

    // Birthmark (immutable after creation)
    birthmark: {
        id: string
        name: string
        personality: string       // Flavor text
        coreAI: CoreAIType        // "aggressive" | "defensive" | "supportive" | "evasive"
        statModifiers: {
            str: number           // -0.20 to +0.20
            int: number
            agi: number
            end: number
        }
    }

    // Core Stats (mutable through growth)
    stats: {
        str: number               // Strength
        int: number               // Intelligence
        agi: number               // Agility
        end: number               // Endurance
    }

    // Derived Stats (calculated)
    derivedStats: {
        hp: number
        maxHp: number
        energy: number
        maxEnergy: number
        energyRegen: number
        moveSpeed: number
        obedience: number         // Hidden from player
    }

    // Combat
    moves: {
        basic: [Move, Move, Move, Move]     // 4 basic moves
        special: [Move, Move, Move, Move]   // 4 special moves
    }

    // Relationship
    temperament: number           // 0-100, affects obedience

    // Lineage
    parents: [string, string] | null   // Parent monster IDs

    // State
    currentHp: number
    currentEnergy: number
    statusEffects: StatusEffect[]
    state: MonsterState           // "idle" | "moving" | "attacking" | "staggered" | "ko" | "carried"
}
```

### 2.2 Species

```typescript
interface Species {
    id: string
    name: string
    type: "insect" | "mammal" | "reptilian" | "avian"

    // Base stat distributions
    baseStats: {
        str: number               // Base starting value
        int: number
        agi: number
        end: number
    }

    // Behavior
    aggressionLevel: "low" | "medium" | "high"

    // Special traits
    traits: Trait[]               // e.g., "flying"

    // Available moves this species can learn
    availableMoves: string[]      // Move IDs

    // Visual
    spriteSheet: string
    portraitImage: string
}

interface Trait {
    id: string
    name: string
    effects: TraitEffect[]
}

// Example: Flying trait
const flyingTrait: Trait = {
    id: "flying",
    name: "Flying",
    effects: [
        { type: "dodgeChance", source: "melee", value: 0.5 },
        { type: "damageTaken", source: "ranged", value: 1.2 }
    ]
}
```

### 2.3 Move

```typescript
interface Move {
    id: string
    name: string
    description: string

    // Classification
    category: "physical" | "magic" | "buff" | "debuff" | "heal" | "aoe"
    tier: "basic" | "special"

    // Costs
    energyCost: number
    cooldown: number              // Seconds

    // Effects
    baseDamage: number            // 0 for non-damage moves
    scalingStat: "str" | "int" | null
    scalingRatio: number          // Multiplier for scaling stat

    statusEffect: StatusEffect | null
    buffEffect: BuffEffect | null

    // Targeting
    range: number                 // Units
    aoeRadius: number             // 0 for single target
    targetType: "enemy" | "ally" | "self" | "all"

    // Requirements
    learnRequirements: {
        stats?: Partial<Stats>    // Minimum stats to learn
        speciesTypes?: string[]   // Which species can learn this
    }
}
```

### 2.4 Birthmark

```typescript
interface Birthmark {
    id: string
    name: string
    description: string

    // Personality (flavor)
    personality: string           // e.g., "Bold", "Timid", "Curious"

    // Core AI archetype
    coreAI: "aggressive" | "defensive" | "supportive" | "evasive"

    // Stat growth modifiers
    statModifiers: {
        str: number               // -0.20 to +0.20
        int: number
        agi: number
        end: number
    }
}

// Generation function
function generateRandomBirthmark(): Birthmark {
    const birthmarks = getBirthmarkPool()
    return birthmarks[Math.floor(Math.random() * birthmarks.length)]
}
```

### 2.5 Status Effect

```typescript
interface StatusEffect {
    id: string
    name: string
    type: "poison" | "stun" | "freeze" | "slow" | "blind" | "burn"

    // Duration
    duration: number              // Seconds
    remainingDuration: number

    // Effect values
    damagePerSecond?: number      // For DoT effects
    movementModifier?: number     // For slow (e.g., 0.5 = 50% speed)
    accuracyModifier?: number     // For blind
    attackModifier?: number       // For burn

    // Stacking
    stackable: boolean
    maxStacks: number
}
```

---

## 3. Core Systems

### 3.1 Combat Engine

```typescript
class CombatEngine {
    private monsters: Monster[]
    private battleDuration: number
    private energyRegenDecay: number

    update(deltaTime: number): void {
        this.battleDuration += deltaTime

        for (const monster of this.monsters) {
            if (monster.state === "ko") continue

            // Update energy regeneration (slows over time)
            this.updateEnergy(monster, deltaTime)

            // Update status effects
            this.updateStatusEffects(monster, deltaTime)

            // Update cooldowns
            this.updateCooldowns(monster, deltaTime)

            // Process AI decisions
            this.processAI(monster)

            // Update movement and position
            this.updateMovement(monster, deltaTime)
        }

        // Check collisions and resolve combat
        this.resolveCollisions()

        // Check battle end conditions
        this.checkBattleEnd()
    }

    private updateEnergy(monster: Monster, dt: number): void {
        // Energy regen slows as battle continues
        const decayFactor = 1 / (1 + this.battleDuration / 60)  // Halves every 60 seconds
        const regenRate = monster.derivedStats.energyRegen * decayFactor

        monster.currentEnergy = Math.min(
            monster.derivedStats.maxEnergy,
            monster.currentEnergy + regenRate * dt
        )
    }

    calculateDamage(attacker: Monster, target: Monster, move: Move): number {
        // Base damage
        let damage = move.baseDamage

        // Stat scaling
        if (move.scalingStat && move.scalingRatio) {
            damage += attacker.stats[move.scalingStat] * move.scalingRatio
        }

        // Defense reduction (simplified)
        const defense = target.stats.end * 0.5
        damage = Math.max(1, damage - defense)

        // Trait modifiers (e.g., flying)
        damage = this.applyTraitModifiers(damage, attacker, target, move)

        // Random variance (90-110%)
        damage *= 0.9 + Math.random() * 0.2

        return Math.floor(damage)
    }
}
```

### 3.2 Monster AI System

```typescript
class MonsterAI {
    processCommand(monster: Monster, command: Command): boolean {
        // Calculate obedience
        const obedience = this.calculateObedience(monster)

        // Roll against obedience
        const roll = Math.random() * 100

        if (roll < obedience) {
            // Command accepted
            this.executeCommand(monster, command)
            this.showFeedback(monster, "accepted")  // Green flash
            return true
        } else {
            // Command ignored - fall back to Core AI
            this.executeCoreAI(monster)
            this.showFeedback(monster, "ignored")   // Red flash
            return false
        }
    }

    private calculateObedience(monster: Monster): number {
        const BASE_OBEDIENCE = 20
        const INT_WEIGHT = 0.4
        const TEMP_WEIGHT = 0.6

        return BASE_OBEDIENCE +
               (monster.stats.int * INT_WEIGHT) +
               (monster.temperament * TEMP_WEIGHT)
    }

    private executeCoreAI(monster: Monster): void {
        switch (monster.birthmark.coreAI) {
            case "aggressive":
                this.aggressiveBehavior(monster)
                break
            case "defensive":
                this.defensiveBehavior(monster)
                break
            case "supportive":
                this.supportiveBehavior(monster)
                break
            case "evasive":
                this.evasiveBehavior(monster)
                break
        }
    }

    private aggressiveBehavior(monster: Monster): void {
        // Target nearest enemy
        const target = this.findNearestEnemy(monster)
        if (target) {
            // Move toward and attack
            this.moveToward(monster, target)
            this.useRandomAttack(monster, target)
        }
    }

    private defensiveBehavior(monster: Monster): void {
        // Maintain distance, counter when attacked
        const nearestEnemy = this.findNearestEnemy(monster)
        if (nearestEnemy) {
            const distance = this.getDistance(monster, nearestEnemy)
            if (distance < SAFE_DISTANCE) {
                this.moveAway(monster, nearestEnemy)
            }
        }
        // Only attack if enemy is attacking us
        if (this.isBeingTargeted(monster)) {
            this.useDefensiveAttack(monster)
        }
    }

    private supportiveBehavior(monster: Monster): void {
        // Prioritize ally buffs and heals
        const ally = this.findAlly(monster)
        if (ally && ally.currentHp < ally.derivedStats.maxHp * 0.5) {
            this.useHealingMove(monster, ally)
        } else if (ally) {
            this.useBuffMove(monster, ally)
        }
    }

    private evasiveBehavior(monster: Monster): void {
        // Avoid damage, flee if low HP
        if (monster.currentHp < monster.derivedStats.maxHp * 0.3) {
            this.flee(monster)
        } else {
            this.keepDistance(monster)
        }
    }
}
```

### 3.3 Breeding System

```typescript
class BreedingSystem {
    canBreed(parent1: Monster, parent2: Monster): BreedResult {
        // Same species check
        if (parent1.speciesId !== parent2.speciesId) {
            // Exception: G3 cross-species for G4
            if (parent1.generation === 3 && parent2.generation === 3) {
                if (this.isValidG4Combination(parent1, parent2)) {
                    return { canBreed: true, resultGeneration: 4 }
                }
            }
            return { canBreed: false, reason: "Different species" }
        }

        // Same generation check
        if (parent1.generation !== parent2.generation) {
            return { canBreed: false, reason: "Different generations" }
        }

        // Cooldown check
        if (this.isOnCooldown(parent1) || this.isOnCooldown(parent2)) {
            return { canBreed: false, reason: "Breeding cooldown active" }
        }

        // Determine result generation
        let resultGen = Math.min(parent1.generation + 1, 3) as 1 | 2 | 3

        return { canBreed: true, resultGeneration: resultGen }
    }

    breed(parent1: Monster, parent2: Monster): Monster {
        const result = this.canBreed(parent1, parent2)
        if (!result.canBreed) throw new Error(result.reason)

        // Determine offspring species
        const species = this.determineSpecies(parent1, parent2, result.resultGeneration)

        // Calculate inherited stats
        const stats = this.calculateInheritedStats(parent1, parent2)

        // Inherit moves
        const moves = this.inheritMoves(parent1, parent2, species)

        // Generate new birthmark
        const birthmark = generateRandomBirthmark()

        // Create offspring
        const offspring: Monster = {
            id: generateUUID(),
            name: this.generateName(species),
            speciesId: species.id,
            generation: result.resultGeneration,
            birthmark: birthmark,
            stats: stats,
            derivedStats: this.calculateDerivedStats(stats, birthmark),
            moves: moves,
            temperament: 50,  // Bred monsters start neutral
            parents: [parent1.id, parent2.id],
            currentHp: 0,     // Will be set to maxHp
            currentEnergy: 0,
            statusEffects: [],
            state: "idle"
        }

        offspring.currentHp = offspring.derivedStats.maxHp
        offspring.currentEnergy = offspring.derivedStats.maxEnergy

        // Apply cooldowns
        this.applyCooldown(parent1)
        this.applyCooldown(parent2)

        return offspring
    }

    private calculateInheritedStats(p1: Monster, p2: Monster): Stats {
        const inherit = (stat: keyof Stats): number => {
            const average = (p1.stats[stat] + p2.stats[stat]) / 2
            const variance = 0.8 + Math.random() * 0.4  // 80-120%
            return Math.floor(average * variance)
        }

        return {
            str: inherit("str"),
            int: inherit("int"),
            agi: inherit("agi"),
            end: inherit("end")
        }
    }

    private inheritMoves(p1: Monster, p2: Monster, species: Species): MonsterMoves {
        const allParentMoves = [
            ...p1.moves.basic, ...p1.moves.special,
            ...p2.moves.basic, ...p2.moves.special
        ]

        const learnableMoves = allParentMoves.filter(move =>
            species.availableMoves.includes(move.id)
        )

        // Fill slots, prioritizing inherited moves
        // ... implementation details
    }
}
```

### 3.4 Growth System

```typescript
class GrowthSystem {
    // Decay thresholds by generation
    private static DECAY_THRESHOLDS = {
        1: 50,
        2: 75,
        3: 100,
        4: 150
    }

    applyStatGain(monster: Monster, stat: keyof Stats, baseGain: number): void {
        const threshold = GrowthSystem.DECAY_THRESHOLDS[monster.generation]
        const currentStat = monster.stats[stat]

        // Calculate decay multiplier
        const decayMultiplier = 1 / (1 + currentStat / threshold)

        // Apply birthmark modifier
        const birthmarkMod = 1 + monster.birthmark.statModifiers[stat]

        // Final gain
        const actualGain = baseGain * decayMultiplier * birthmarkMod

        monster.stats[stat] += actualGain

        // Recalculate derived stats
        this.recalculateDerivedStats(monster)
    }

    // Called during combat based on actions
    onAttack(monster: Monster): void {
        this.applyStatGain(monster, "str", BASE_STR_GAIN)
    }

    onUseAbility(monster: Monster): void {
        this.applyStatGain(monster, "int", BASE_INT_GAIN)
    }

    onMove(monster: Monster, distance: number): void {
        this.applyStatGain(monster, "agi", BASE_AGI_GAIN * distance)
    }

    onTakeDamage(monster: Monster, damage: number): void {
        this.applyStatGain(monster, "end", BASE_END_GAIN * (damage / 10))
    }
}
```

### 3.5 Capture System

```typescript
class CaptureSystem {
    attemptTranquilize(target: Monster): TranqResult {
        const hpPercent = (target.currentHp / target.derivedStats.maxHp) * 100

        // Must be below 25% HP
        if (hpPercent > 25) {
            return { success: false, reason: "Target HP too high (need < 25%)" }
        }

        // Calculate success chance
        // 50% at 25% HP, scales to 100% at 5% HP
        const successChance = Math.min(1, (25 - hpPercent) / 20 + 0.5)

        const roll = Math.random()

        if (roll < successChance) {
            target.state = "carried"
            return { success: true, monster: target }
        } else {
            return { success: false, reason: "Tranquilization failed" }
        }
    }

    updateCarriedMonster(carried: Monster, battleActive: boolean): void {
        if (!battleActive) return

        // 10% chance per update to wake up if battle continues
        if (Math.random() < 0.1) {
            carried.state = "idle"
            carried.currentHp = carried.derivedStats.maxHp * 0.1  // Wakes at 10% HP
            // Monster becomes hostile
        }
    }

    completeCapture(monster: Monster): Monster {
        // Reset state
        monster.state = "idle"
        monster.currentHp = monster.derivedStats.maxHp
        monster.currentEnergy = monster.derivedStats.maxEnergy
        monster.statusEffects = []

        // Wild monsters start with low temperament
        monster.temperament = 20

        return monster
    }
}
```

---

## 4. Input System

### 4.1 Controller Mapping

```typescript
interface ControllerMapping {
    // Stances (D-Pad)
    DPAD_UP: "stance_aggressive"
    DPAD_DOWN: "stance_defensive"
    DPAD_LEFT: "stance_supportive"
    DPAD_RIGHT: "stance_passive"

    // Monster selection
    L1: "select_monster_1"
    R1: "select_monster_2"

    // Moves (while holding L1 or R1)
    A: "move_slot_1"     // Basic 1 or Special 1
    B: "move_slot_2"     // Basic 2 or Special 2
    X: "move_slot_3"     // Basic 3 or Special 3
    Y: "move_slot_4"     // Basic 4 or Special 4

    // Advanced (L1+L2 or R1+R2)
    L1_L2: "advanced_monster_1"   // Switch to special moves
    R1_R2: "advanced_monster_2"

    // Items
    L2: "item_monster_1"
    R2: "item_monster_2"
}
```

### 4.2 Command Queue

```typescript
class CommandQueue {
    private queues: Map<string, Command[]> = new Map()  // Per monster
    private cooldowns: Map<string, number> = new Map()

    private static COMMAND_COOLDOWN = 0.5  // Seconds
    private static MAX_QUEUE_SIZE = 1

    queueCommand(monsterId: string, command: Command): boolean {
        // Check cooldown
        const cooldown = this.cooldowns.get(monsterId) || 0
        if (cooldown > 0) return false

        // Check queue size
        const queue = this.queues.get(monsterId) || []
        if (queue.length >= CommandQueue.MAX_QUEUE_SIZE) return false

        // Add to queue
        queue.push(command)
        this.queues.set(monsterId, queue)

        // Apply cooldown
        this.cooldowns.set(monsterId, CommandQueue.COMMAND_COOLDOWN)

        return true
    }

    update(deltaTime: number): void {
        // Decrease cooldowns
        for (const [id, cd] of this.cooldowns) {
            this.cooldowns.set(id, Math.max(0, cd - deltaTime))
        }
    }

    getNextCommand(monsterId: string): Command | null {
        const queue = this.queues.get(monsterId)
        if (!queue || queue.length === 0) return null
        return queue.shift() || null
    }
}
```

---

## 5. State Management

### 5.1 Game States

```typescript
enum GameState {
    MAIN_MENU = "main_menu",
    OVERWORLD = "overworld",
    BATTLE = "battle",
    ARENA = "arena",
    CUTSCENE = "cutscene",
    MENU = "menu",           // In-game pause menu
    BREEDING = "breeding",
    BASE = "base"
}

class GameStateMachine {
    private currentState: GameState = GameState.MAIN_MENU
    private stateHandlers: Map<GameState, StateHandler>

    transition(newState: GameState, data?: any): void {
        const oldHandler = this.stateHandlers.get(this.currentState)
        oldHandler?.onExit()

        this.currentState = newState

        const newHandler = this.stateHandlers.get(newState)
        newHandler?.onEnter(data)
    }
}
```

### 5.2 Monster States

```typescript
enum MonsterState {
    IDLE = "idle",
    MOVING = "moving",
    ATTACKING = "attacking",
    USING_ABILITY = "using_ability",
    STAGGERED = "staggered",
    KO = "ko",
    CARRIED = "carried"
}

class MonsterStateMachine {
    private monster: Monster
    private currentState: MonsterState
    private stateTimer: number = 0

    update(deltaTime: number): void {
        this.stateTimer -= deltaTime

        switch (this.currentState) {
            case MonsterState.STAGGERED:
                if (this.stateTimer <= 0) {
                    this.transition(MonsterState.IDLE)
                }
                break
            case MonsterState.ATTACKING:
                if (this.stateTimer <= 0) {
                    this.transition(MonsterState.IDLE)
                }
                break
            // ... other states
        }
    }

    transition(newState: MonsterState, duration?: number): void {
        this.currentState = newState
        this.monster.state = newState
        this.stateTimer = duration || 0
    }
}
```

---

## 6. Save System

### 6.1 Save Data Structure

```typescript
interface SaveData {
    version: string
    timestamp: number

    // Player
    player: {
        name: string
        position: { x: number, y: number, mapId: string }
        currency: number
        playtime: number
    }

    // Monsters
    roster: Monster[]          // All owned monsters
    activeParty: [string, string]  // IDs of active monsters

    // Inventory
    inventory: {
        items: { itemId: string, quantity: number }[]
        ingredients: { ingredientId: string, quantity: number }[]
    }

    // Progress
    progress: {
        arenaRanks: { [regionId: string]: Rank }
        unlockedRegions: string[]
        defeatedBosses: string[]
        capturedLegendaries: string[]
        discoveredG4Recipes: string[]
    }

    // World State
    worldState: {
        capturedMonsterIds: string[]  // Prevent respawn
        openedChests: string[]
        completedEvents: string[]
    }

    // Base
    base: {
        capacity: number
        upgrades: string[]
        npcs: string[]
    }

    // Settings
    settings: {
        // ... user preferences
    }
}
```

### 6.2 Serialization

```typescript
class SaveSystem {
    private static SAVE_KEY = "hybrid_gene_save"

    save(data: SaveData): void {
        const serialized = JSON.stringify(data)
        localStorage.setItem(SaveSystem.SAVE_KEY, serialized)
    }

    load(): SaveData | null {
        const serialized = localStorage.getItem(SaveSystem.SAVE_KEY)
        if (!serialized) return null

        try {
            const data = JSON.parse(serialized) as SaveData
            return this.migrate(data)  // Handle version differences
        } catch {
            return null
        }
    }

    private migrate(data: SaveData): SaveData {
        // Handle save file migrations between versions
        // ...
        return data
    }
}
```

---

## 7. Performance Considerations

### 7.1 Limits

| System | Limit | Reason |
|--------|-------|--------|
| Battle entities | 4 max (2v2) | AI + collision complexity |
| Particle effects | 50 per entity | Visual clarity + performance |
| Pathfinding nodes | 1000 per map | Memory + CPU |
| Status effects per monster | 5 max | UI space + balance |

### 7.2 Optimization Strategies

```typescript
// Object pooling for projectiles/effects
class ObjectPool<T> {
    private pool: T[] = []
    private factory: () => T

    acquire(): T {
        return this.pool.pop() || this.factory()
    }

    release(obj: T): void {
        this.pool.push(obj)
    }
}

// Spatial partitioning for collision
class SpatialGrid {
    private cellSize: number
    private cells: Map<string, Entity[]>

    getNearbyEntities(position: Vector2, radius: number): Entity[] {
        // Only check relevant cells
    }
}

// Throttled AI updates
class AIManager {
    private updateInterval = 100  // ms
    private lastUpdate: Map<string, number> = new Map()

    shouldUpdate(monsterId: string, currentTime: number): boolean {
        const last = this.lastUpdate.get(monsterId) || 0
        if (currentTime - last > this.updateInterval) {
            this.lastUpdate.set(monsterId, currentTime)
            return true
        }
        return false
    }
}
```

---

## 8. Constants & Configuration

```typescript
// config/balance.ts
export const BALANCE = {
    // Growth
    BASE_STR_GAIN: 0.1,
    BASE_INT_GAIN: 0.1,
    BASE_AGI_GAIN: 0.05,
    BASE_END_GAIN: 0.08,

    // Combat
    COMMAND_COOLDOWN: 0.5,
    STAGGER_DURATION: 0.3,
    ENERGY_REGEN_BASE: 5,
    ENERGY_DECAY_RATE: 60,  // Seconds to halve regen

    // Capture
    TRANQ_MIN_HP_PERCENT: 25,
    TRANQ_BASE_CHANCE: 0.5,
    TRANQ_WAKE_CHANCE: 0.1,
    CARRY_SPEED_MODIFIER: 0.5,

    // Breeding
    BREEDING_COOLDOWN: 3600,  // Seconds
    STAT_INHERITANCE_VARIANCE: 0.4,  // +/- 20%

    // Obedience
    BASE_OBEDIENCE: 20,
    INT_OBEDIENCE_WEIGHT: 0.4,
    TEMP_OBEDIENCE_WEIGHT: 0.6,
    WILD_START_TEMPERAMENT: 20,
    BRED_START_TEMPERAMENT: 50
}

// config/generations.ts
export const GENERATION_CONFIG = {
    1: { decayThreshold: 50, maxMonsters: 16 },
    2: { decayThreshold: 75, maxMonsters: null },
    3: { decayThreshold: 100, maxMonsters: 100 },
    4: { decayThreshold: 150, maxMonsters: 6 }
}
```

---

*Document End*
