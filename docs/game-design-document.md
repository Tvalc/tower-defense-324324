# Game Design Document

## Description
Overall game vision, mechanics, and core design decisions

## Content
---
# Game Design Document (GDD)
## Snib Tower Defense Extravaganza Celebration

---

## 1. Game Overview

**Game Title:** Snib Tower Defense Extravaganza Celebration  
**Genre:** Tower Defense with Persistent Base-Building & Progression  
**Platform:** Web (Desktop & Mobile Browsers; HTML5/JavaScript)  
**Elevator Pitch:**  
A wild, cartoonish tower defense adventure where sci-fi and fantasy collide! Defend against waves of zany creatures, build and upgrade a persistent base, and unlock ever-more absurd towers, spells, and powerups as you progress through 100 unique levels.  

---

## 2. Gameplay Mechanics

### Core Gameplay Loop

1. **Base-Building/Preparation:**  
   Between levels, players invest in persistent structures and upgrades in their "Snib HQ"—unlocked and improved using Snib Glitter.
2. **Level Start:**  
   Select a level (each with a unique theme and map). Review available towers, spells, and upgrades.
3. **Stage Progression:**  
   Each level has 10 stages. Every stage features a unique enemy path layout, requiring fresh tower placement and strategy.
4. **Wave Defense:**  
   Survive 10 escalating waves of enemies per stage, culminating in a themed boss.
5. **Combat:**  
   Place towers, cast spells, and deploy powerups to defeat enemies. Earn Snib Glitter, unlock new towers or spells, and progress.
6. **Persistence:**  
   After level completion, return to Snib HQ to unlock/upgrade towers, passive bonuses, or spells for future runs.

### Level & Stage Theming

- **Levels:** 100, with funny sci-fi/fantasy names (see Appendix A for sample naming conventions).
- **Stages:** 10 per level, each with a unique map layout and path(s).

**Sample Level Names:**  
- Level 1: "The Giggling Goblin Glade"  
- Level 2: "Robot Rumble Ravine"  
- Level 3: "Space Lizard Lagoon"  
- Level 4: "Cyber Unicorn Uplands"  
- ...  
*(Complete list to be generated in Appendix A)*

**Sample Stage Names for Level 1:**  
- Stage 1: "Tiny Troll Trail"  
- Stage 2: "Hobgoblin Hurdle"  
- ...  
- Stage 10: "Gob-King's Last Laugh"

### Tower Types

**Core Towers (Unlocakable via Progression):**  
| Type              | Name Suggestion            | Description                                        |
|-------------------|---------------------------|----------------------------------------------------|
| Basic             | Snib Slinger              | Fast, single-target shots                          |
| Slow              | Gelatinous Goozer         | Slows enemies on hit                               |
| Area-of-Effect    | Kaboom Kettle             | Lobs bombs, AOE splash                             |
| Constant Fire     | Zap-o-Matic               | Continuous beam, moderate damage                   |
| Anti-Air          | Sky Nibbler               | Targets flying enemies exclusively                  |
| Summoner          | Minion Manufactory        | Spawns friendly creatures on path                  |
| Hero Tower        | Heroic Hall               | Deploys a unique hero with abilities               |
| Vehicle Launchpad | Snib Mobile HQ            | Sends vehicles on the path to crush enemies        |
*(Each tower is upgradable in damage, range, special effects, etc.)*

### Enemy Types

- **Total:** 500 unique enemies, distributed so every new level introduces at least one new creature.
- **Variety:** Mix of fantasy (goblins, trolls, necromancers) and sci-fi (robots, aliens, space jellyfish).
- **Special Abilities:** Some fly, some are fast, some are shielded, some split into smaller units, some stealthy, etc.

**Example Enemy Table (Level 1):**  
| Enemy Name           | Theme      | Ability          | Health | Speed | Snib Glitter Value |
|----------------------|------------|------------------|--------|-------|-------------------|
| Giggling Goblin      | Fantasy    | None             | 10     | 1.0   | 1                 |
| Squeaky Imp          | Fantasy    | Fast             | 8      | 2.0   | 1                 |
| Robo-Scamper         | Sci-Fi     | Armored          | 15     | 1.2   | 2                 |
| ...                  | ...        | ...              | ...    | ...   | ...               |
*(Full enemy list in Appendix B)*

- **Bosses:** Each stage 10 features a unique boss with special behaviors.

### Level Design

- **Map:** Each stage features a distinct path(s) and strategic tower locations.
- **Responsive:** Maps auto-scale for desktop/mobile, leveraging touch and mouse input.

### Win/Loss Conditions

- **Win:** Defeat all waves + boss in a stage. Complete all 10 stages in a level to advance.
- **Loss:** Player health (starts at 20 per stage) reaches zero if too many enemies cross the map.

### Scoring System

**Currency:** Snib Glitter  
- **Awarded:** For each enemy defeated, based on difficulty.
- **Used For:** Tower placement/upgrades (during stage), persistent base upgrades (between levels).

**Sample Snib Glitter Table:**  
| Enemy Tier             | Example Enemies        | Snib Glitter Value |
|------------------------|-----------------------|-------------------|
| Basic                  | Giggling Goblin       | 1                 |
| Fast                   | Squeaky Imp           | 1                 |
| Armored                | Robo-Scamper          | 2                 |
| Flying                 | Sky Pixie             | 2                 |
| Boss                   | Gob-King              | 10                |
| Elite/Boss (late game) | Alien Overlord        | 20+               |

---

## 3. Art and Sound

### Visual Style

- **Super Cartoonish:**  
  - Bright colors, exaggerated proportions, expressive enemies/towers.
  - Animation focus on comedic, over-the-top effects (Snib Glitter "explosions," squishy goblins, etc.)
- **Map Visuals:**  
  - Each level has distinct visual theming (fantasy forests, alien worlds, etc.).

### Sound Design

- **Music:**  
  - Sci-fi/fantasy grand opera style; bombastic, whimsical, and energetic.
- **SFX:**  
  - Comical tower fire, creature noises, Snib Glitter pops and explosions.

---

## 4. User Interface

### HUD Elements

- **Player Health:** (Hearts or cartoon HP bar)
- **Stage & Wave:** (E.g., “Stage 3-7, Wave 5/10”)
- **Snib Glitter Counter:**  
- **Tower Build Menu:** Accessible at all times, shows unlocked towers, costs, and build button.
- **Spell Menu:** Quick-access for casting spells (once unlocked).
- **Tower Placement:** After selecting, tap/click to place, confirm/cancel UI.
- **Pause/Menu/Settings:** Simple, large touch/mouse-friendly buttons.

### Menus

- **Main Menu:**  
  - Start Game
  - Continue  
  - Base Building (Snib HQ)  
  - Settings (audio, controls, graphics)
  - Credits

- **Pause Menu:**  
  - Resume  
  - Restart Stage  
  - Return to Main Menu

- **Level Selection:**  
  - Map overview with unlocked levels and progress.
  - Level info and preview.

- **Game Over/Victory:**  
  - Stats summary, Snib Glitter earned, unlocks preview.

---

## 5. Technical Specifications

- **Game Engine:**  
  - *Recommended:* [Phaser 3](https://phaser.io/) for 2D HTML5 games (robust, performant, open-source, supports responsive input).
- **Languages:**  
  - JavaScript/TypeScript, HTML5, CSS3.
- **Performance:**  
  - Optimize for minimal asset loads, sprite batching, and consider asset streaming for mobile.
- **Input:**  
  - Mouse (desktop), Touch (mobile/tablet)—all critical UI and gameplay elements must be touch/mouse friendly.
- **Responsive Design:**  
  - Layouts scale and reposition for portrait/landscape and various device sizes.

---

## 6. Development Timeline

### Milestones (Example):

| Milestone                    | Deliverables                                              | Target Date |
|------------------------------|----------------------------------------------------------|-------------|
| Prototype                    | Core tower defense loop, 1 level, 3 towers, 5 enemies    | Month 1     |
| Core System Implementation   | 10 levels, base-building, progression/unlocks            | Month 2     |
| Content Expansion            | 50 levels, 20 tower/enemy types, sound & art pass        | Month 3     |
| Full Content Pass            | 100 levels, 500 enemies, all towers/spells, all bosses   | Month 4     |
| UX/UI Polish                 | Responsive UI, smooth input, accessibility pass          | Month 5     |
| Beta/Testing                 | Balancing, bug fixing, performance tuning                | Month 6     |
| Launch                       | Release on web, marketing rollout                        | Month 7     |

---

## 7. Additional Features

- **Upgrades/Customization:**  
  - Persistent Snib HQ: Build/upgrade labs, forges, libraries for permanent improvements (tower stats, spell unlocks, passive income, etc.).
  - Tower and Spell Upgrade Trees: Each tower/spell has upgrade paths to customize playstyle.
- **No Multiplayer/Co-op:**  
  - Focus on single-player progression and replayability.

---

## 8. Market Analysis

- **Target Audience:**  
  - Casual gamers, mobile/tablet players, fans of tower defense and base building.
  - Age range: 10–40, with family-friendly humor and visuals.
- **Key Competitors:**  
  - Bloons TD, Kingdom Rush, Plants vs. Zombies.
- **Key Differentiators:**  
  - Massive variety of enemies and towers, persistent base-building progression, comedic sci-fi/fantasy blend, highly responsive web gameplay.

---

## Success Metrics

- **Player Retention:** % of players returning each day/week
- **Level Completion:** % of players clearing each level; points where players churn
- **Session Length:** Average time per session
- **Tower/Enemy Diversity Used:** Are players experimenting with all content
- **Feedback Rating:** User reviews, ratings on web portals

---

## Appendix A: Level & Stage Names  
*(To be generated in detail in future iterations.)*

## Appendix B: Enemy List  
*(500 unique enemies—spreadsheet/JSON to be developed.)*

---

### Potential Conflicts/Notes:

- No existing characters, mechanics, or systems documented—this GDD establishes all initial systems and content.  
- When creating 500 enemies and 1000 stage names, ensure naming style matches the above (“funny, sci-fi, and fantasy themed”) for consistency.

---

**End of Document**


---
*Generated on 7/17/2025*
