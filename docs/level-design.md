# Level Design Specification

## Description
Individual level layouts, progression, and mechanics

## Content
---
# Snib Tower Defense Extravaganza Celebration  
## LEVEL DESIGN DOCUMENT

---

## 1. Level Structure & Progression

### Overview

- **Total Levels:** 100  
- **Stages Per Level:** 10  
- **Waves Per Stage:** 10 (plus 1 boss wave per stage)  
- **Progression:** Each level introduces a new enemy type. Each wave randomly mixes unlocked enemy types, with difficulty and enemy count scaling per stage/level.  
- **Base-Building:** Persistent base hub upgrades (unlocked between levels).  
- **Unlocks:** New towers, spells, or powerups unlocked every few levels, persistent across all levels.  
- **Pacing:** Early levels introduce mechanics, mid-game ramps up complexity, late-game focuses on mastery and multi-path chaos.  
- **Win/Loss:** Survive all stages in a level; health (HP) reduced when enemies reach the end of the path. Game over if HP reaches 0.

---

## 2. Level & Stage Naming

### Naming Conventions

- **Levels:** Each level has a unique, humorous sci-fi/fantasy title.
- **Stages:** Each stage is a “Scenario” within the level, with sub-titles reflecting the escalating challenge.

#### Example (Levels 1-5):

| Level # | Level Name                      | Stages (10 per level, sample names)                           |
|---------|---------------------------------|---------------------------------------------------------------|
| 1       | Galactic Goblin Gala            | Scenario 1: Party Crashers, Scenario 2: Punch & Pie, ...      |
| 2       | Starship Salamander Saga        | Scenario 1: Lizard Launchpad, Scenario 2: Tail of Terror, ... |
| 3       | Robo-Rat Rampage                | Scenario 1: Squeaky Intruders, Scenario 2: Cheese Protocol, ...|
| 4       | Quantum Quokka Quandary         | Scenario 1: Marsupial Mayhem, Scenario 2: Space Pouches, ...   |
| 5       | Mech-Mermaid Mischief           | Scenario 1: Siren Servers, Scenario 2: Underwater Uploads, ... |

*(Full list to be expanded in iterative design; each level and stage gets a themed sub-name for comedic flavor and environmental storytelling.)*

---

## 3. Level Layout & Environment

### Layout Principles

- **Paths:**  
  - Each stage features 1–3 winding paths; some stages add branching/merging routes for increased challenge.
  - Paths are visually distinct (glowing tracks, magical footprints, etc.).
- **Tower Placement:**  
  - Designated “build zones” adjacent to paths; some stages feature limited zones, others more open.
- **Obstacles/Scenery:**  
  - Environmental props (crashed ships, enchanted trees, sciencey debris) add visual variety and can block tower placement (not pathing).
- **Base Hub:**  
  - Persistent area accessible between levels for upgrades, not present within combat arenas.

#### Sample Stage Layout (Web-Optimized):

- **Grid Size:** 12x8 logical grid (scales to screen size)
- **Example:**   
  - Enemy spawn at top-left, path curves downward, splits into two mid-map, rejoins at bottom-right exit.
  - 8 build zones (highlighted tiles) along the path edges.
  - Obstacles: 2–3 per map, fixed per stage.

*All layouts delivered as JSON or tilemaps for HTML5 game engine.*

---

## 4. Enemy Distribution & Progression

- **Enemy Pools:**  
  - Each level introduces 1 new enemy type (500 total over 100 levels; see enemy design doc).
  - Wave composition: Random mix from unlocked enemies, with each wave increasing in quantity and composition complexity.
  - **Bosses:** Each stage has a unique boss (drawn from that level’s theme), with special abilities (shields, splits, speed, etc.).

#### Example (Level 1: Galactic Goblin Gala):

| Stage | Wave 1-3        | Wave 4-9               | Wave 10 (Boss)         |
|-------|-----------------|------------------------|------------------------|
| 1     | Goblin Grunts   | + Goblin Grenadiers    | Goblin Party King      |
| 2     | All above +     | Add Goblin Jetpackers  | Goblin DJ Zorp         |

*Repeat/expand for each level, referencing full enemy/boss roster.*

---

## 5. Objectives & Player Guidance

### Objectives

- Survive all 10 stages of a level.
- Prevent enemies from reaching the end of the path (each enemy that does removes 1 HP from player).
- Earn Snib Glitter by defeating enemies, use it to build/upgrade towers and purchase spells.
- Unlock persistent upgrades between levels.

### Player Guidance

- **Tutorials:**  
  - Level 1: Interactive tutorial with step-by-step prompts (placing towers, casting spells, explaining HP/Scoring).
- **HUD:**  
  - HP (hearts icon), Current Glitter (currency icon), Stage/Wave indicator, Build/Spell buttons.
- **Path Indicators:**  
  - Arrows showing upcoming enemy path.
- **Hover/Touch Info:**  
  - On build zones, shows tower cost and stats.
- **Failure Feedback:**  
  - When enemies breach, shake screen, play “ouch” sound, decrement HP visibly.

---

## 6. Difficulty Curve & Pacing

- **Early Game:**  
  - Fewer, slower enemies; simple paths; generous build zones.  
  - 1–2 tower types available; basic spells.
- **Mid Game:**  
  - More/faster enemies; multi-path stages; environmental hazards.
  - More tower and spell types unlocked; enemy resistances introduced.
- **Late Game:**  
  - Complex maze-like maps; multiple enemy abilities (flying, immune, shielded).
  - All tower types, spells, and powerups unlocked; enemy swarms and multi-boss waves.

*Difficulty scales by increasing enemy HP, speed, special abilities, and wave size per progression model.*

---

## 7. Environmental Storytelling

- **Stage Introductions:**  
  - Short, humorous comic-style splash panels before each level.
- **Environmental Props:**  
  - Each level’s background and obstacles reflect the theme (e.g., “Robo-Rat Rampage” has junkyard tech, spinning gears, etc.).
- **Dynamic Elements:**  
  - Occasional interactive objects (tap to get bonus Glitter, block a path for one wave, etc.) for player engagement.

---

## 8. UI & Accessibility

- **Responsive Layout:**  
  - UI scales and repositions for all screen sizes and orientations.  
  - Large, touch-friendly buttons for mobile.
- **Build Menu:**  
  - Pops up with icons for each unlocked tower/spell, cost, and build button.  
  - Drag-and-drop (mouse/touch) to placement.
- **Pause/Menu:**  
  - Pause, restart, and fast-forward buttons; clear visual feedback.

---

## 9. Technical & Performance Considerations

- **Engine:**  
  - HTML5/JavaScript (recommend Phaser.js for tilemaps, asset streaming, and performance).
- **Asset Management:**  
  - Levels load in chunks; stream enemy/tower art as needed.
  - Use SVG or compressed spritesheets for backgrounds/characters.
  - Limit concurrent active assets (<50 on-screen at once).
- **Screen Adaptation:**  
  - Levels designed for 16:9 and 9:16 aspect ratios; scalable grid for all devices.
- **Touch/Mouse Input:**  
  - All interactive elements (build zones, menus, buttons) sized for easy finger/tap use.

---

## 10. Implementation Examples

### Example Level Layout JSON

```json
{
  "level": 1,
  "stage": 1,
  "paths": [
    [{"x":0,"y":0},{"x":2,"y":2},{"x":4,"y":4},{"x":7,"y":7}],
    [{"x":0,"y":0},{"x":1,"y":3},{"x":3,"y":5},{"x":7,"y":7}]
  ],
  "buildZones": [{"x":1,"y":1},{"x":2,"y":3},{"x":4,"y":3},{"x":5,"y":6}],
  "obstacles": [{"x":3,"y":2,"type":"tree"},{"x":6,"y":5,"type":"crash_site"}]
}
```

---

## 11. Level Progression Summary Table (Sample)

| Level | New Enemy Introduced   | Tower/Spell/Powerup Unlock    | Path Count | Map Complexity | Boss Theme         |
|-------|------------------------|-------------------------------|------------|---------------|--------------------|
| 1     | Goblin Grunt           | Basic Tower                   | 1          | Simple        | Goblin Party King  |
| 2     | Salamander Spitter     | Slow Tower                    | 1          | Simple        | Salamander Queen   |
| 3     | Robo-Rat Runner        | AoE Tower                     | 2          | Moderate      | Rat Overlord       |
| ...   | ...                    | ...                           | ...        | ...           | ...                |

---

## 12. Open Issues & Iteration Notes

- **Character/Enemy Design:** Full enemy roster (500+) to be iteratively designed, referenced by level.
- **Tower/Spell Types:** Finalize unique mechanics and visuals per unlock, ensure balance.
- **Scoring Table:** To be included in the main GDD, ensuring each enemy type is referenced and valued.
- **Playtesting:** Levels to be adjusted for pacing and difficulty based on feedback.
- **Performance:** Asset limits and streaming to be validated during implementation.

---

*This document provides the foundational structure and actionable guidance for level implementation, ensuring web-optimized, engaging, and scalable level design for Snib Tower Defense Extravaganza Celebration.*

---


---
*Generated on 7/17/2025*
