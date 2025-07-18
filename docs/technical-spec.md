# Technical Specification

## Description
Architecture, performance, and platform requirements

## Content
---
# Technical Specification Document  
## Snib Tower Defense Extravaganza Celebration

---

### 1. **Platform & Engine**

#### 1.1 Platform
- **Supported:** Web Browsers (Desktop & Mobile)
    - Chrome 90+, Firefox 88+, Safari 14+, Edge 90+
- **Instant Play:** No installation, runs directly via Snib Platform CDN.
- **Responsive:** Must adapt to phones, tablets, and desktops.

#### 1.2 Engine & Stack
- **Primary Engine:** Phaser.js 3.90.0 (Required)
    - HTML5 Canvas & WebGL rendering, chosen for browser performance and Snib compatibility.
    - Supports modular architecture for large-scale TD games.
- **Languages:** JavaScript (ES6+), TypeScript (optional for maintainability)
- **UI:** Phaser + HTML5/CSS3 overlays for menus when necessary (DOM elements for text input, accessibility, etc.)
- **Styling:** CSS3, Flexbox/Grid for overlays
- **Audio:** Web Audio API via Phaser.Sound
- **Asset Pipeline:** All assets (images/audio) pre-packed, loaded via Phaser.Loader with progress bar.

---

### 2. **Performance & Optimization**

#### 2.1 Constraints
- **Max Total Game Size:** 10MB (compressed, initial load)
- **Max RAM Usage:** 500MB
- **Target FPS:** 60 (on mid-tier mobile hardware)
- **Asset Budget:** 50MB (images + audio)
- **Image Size:** max 2MB per file (prefer <500kb for most)
- **Audio:** max 3min/track, OGG/MP3/WebM, use compressed formats.

#### 2.2 Asset Loading
- **Initial Load:** Core game code, splash UI, minimal assets (max 3s load)
- **Deferred/On-Demand:** Level, tower, and enemy assets loaded as needed (using Phaser.Loader.on('filecomplete'), destroy unused assets between levels)
- **Texture Atlases:** Use TexturePacker or similar to combine sprites into atlases for towers, enemies, effects.
- **Sound Sprites:** Combine SFX into single audio files, use Phaser’s audio sprite system.

#### 2.3 Optimization
- **Mobile Scaling:** Use Phaser.Scale.FIT and responsive containers.
- **Low-Res Fallbacks:** Provide fallback images for low-end devices.
- **Pooling:** Pool enemy/tower/bullet objects to reduce GC churn.
- **Efficient Pathfinding:** Pre-calculate enemy paths per stage, cache waypoints.
- **Culling:** Only render/display objects within viewport.
- **Audio:** Pause/mute audio when tab is not active (auto-handled by Phaser, but test for compatibility).

---

### 3. **Game Architecture (Phaser.js Specific)**

#### 3.1 Scene Structure
- **BootScene:** Preloads core assets, sets up scale/config.
- **MainMenuScene:** Title, start, settings, credits.
- **LevelSelectScene:** Map/progression, persistent base management.
- **GameScene:** Core gameplay loop (tower defense board, waves, HUD, input).
- **PauseScene (Overlay):** Pause menu over current scene.
- **GameOverScene:** Results, stats, retry options.
- **VictoryScene:** Celebration, unlocks, continue.

#### 3.2 Core Systems (in GameScene)
- **Path System:** Predefined paths per stage. Use Phaser.Curves.Path for enemy movement.
- **Enemy Spawner:** Spawns enemy waves per stage, supports randomization within unlocked pool.
- **Tower Placement:** Drag/drop or tap/click-to-place, grid or free-form (snapping logic).
- **Tower System:** Base class, extend for unique behaviors (basic, slow, AoE, anti-air, spawner, hero, vehicle).
- **Projectile/Effect System:** Pool projectiles, animate effects, manage collisions.
- **Spell System:** UI for casting spells, area targeting, cooldowns.
- **HUD/UI:** Phaser.Group for health, stage/wave, Snib Glitter, build menu.
- **Currency System:** Snib Glitter, animated pop-outs when enemies defeated.
- **Base-Building/Persistence:** LocalStorage for persistent upgrades/unlocks.
- **Upgrade Tree:** Persistent progression, unlock new towers/spells/powerups.

---

### 4. **Responsive Design**

- **Scale Mode:** Phaser.Scale.FIT (maintains aspect, fits to screen)
- **UI Layout:** Anchor HUD elements to corners/edges, auto-relayout for orientation changes.
- **Touch Input:** Large tap targets, drag-to-place for towers, swipe/click for spell targeting.
- **Keyboard/Mouse:** WASD/arrow for panning (desktop), mouse wheel/zoom, click-to-place.
- **Accessibility:** High-contrast mode, optional font size increase.

---

### 5. **Input Handling**

- **Touch:** Tap/drag to select, place, cast spells.
- **Mouse:** Click/drag for placement, UI navigation.
- **Keyboard:** Shortcuts for build menu, spell activation (desktop).
- **Multi-Input:** Prevent double-firing between input types.

---

### 6. **Persistence & Progression**

- **Storage:** Phaser’s localStorage wrapper.
- **Persistent Data:** Unlocked towers, spells, upgrades, base-building structures.
- **Session Data:** Current level, progress, temporary powerups.
- **No Server-Side:** All persistence is client-side; warn users about clearing browser data.

---

### 7. **Browser Compatibility & Deployment**

- **WebGL First:** Fallback to Canvas 2D if WebGL unavailable.
- **Web Audio API:** Fallback to HTML5 Audio if needed (with degraded experience).
- **CORS:** All assets must be served from Snib CDN or with correct CORS headers.
- **No Offline Support:** Online play only; warn if connection lost.
- **No Plugins/Native:** No Flash, no Java, no desktop integration.

---

### 8. **UI & Menus**

- **HUD:** Health, current stage/wave, Snib Glitter, build menu button, spell button(s).
- **Build Menu:** List of unlocked towers with cost, hover/click for description, “Build” button.
- **Tower Placement:** Ghost preview on valid tiles, snap-to-grid or circle.
- **Menu Screens:** Main menu (Play, Settings, Credits), Pause (Resume, Restart, Quit), Game Over, Victory.
- **Settings:** Music/sfx volume, graphics quality (low/high), controls info.
- **Persistent Base:** Separate view for upgrades, unlocks, and base management.

---

### 9. **Art & Audio Pipeline**

- **Images:** PNG/WebP preferred, SVG for vector UI icons.
    - Sprite sheets for towers/enemies, background tiles, effects.
    - Max 2MB/image, prefer <500KB.
- **Audio:** OGG/MP3/WebM for music/SFX, <3min/track.
    - Music: Looping, grand sci-fi/fantasy opera style.
    - SFX: Cartoonish, exaggerated.
    - Audio Sprites for SFX.
- **Compression:** Use TinyPNG, WebP, and audio compression tools before upload.

---

### 10. **Milestones & Timeline (Example)**

| Milestone              | Description                          | Target Weeks |
|------------------------|--------------------------------------|--------------|
| Project Setup          | Repo, CI, Phaser config, scaffolding |      1       |
| Core Gameplay Loop     | Board, pathing, enemy spawns, towers |      2       |
| UI & HUD               | HUD, menus, build/spell UI           |      2       |
| 20 Levels, 40 Enemies  | Level structure, enemy behaviors     |      3       |
| Art & Audio Pass 1     | Placeholder to stylized assets       |      2       |
| Persistence/Base Build | Upgrades, unlocks, localStorage      |      2       |
| Content Expansion      | All 100 levels, 500 enemies          |      4       |
| Final Polish & QA      | Optimize, bug-fix, deploy            |      2       |

---

### 11. **Security & Data**

- **No Personal Data:** No account system, only local progression.
- **LocalStorage:** Check for quota errors, warn user if space runs out.
- **No File Access:** No file uploads/downloads, no external asset loading (except via CDN with CORS).

---

### 12. **Example Phaser.js Implementation Patterns**

- **Scene Transitions:** Use Phaser.SceneManager for smooth fades.
- **Object Pooling:** Use Phaser.GameObjects.Group for enemy/tower pools.
- **Tweened Animations:** For Snib Glitter, use Phaser.Tweens.add for burst effects.
- **HUD:** Fixed-to-camera containers for health, currency, menus.
- **Pathfinding:** Predefine waypoints; use Phaser.Curves.Path or A* grid if needed.

---

### 13. **Known Limitations & Risks**

- **Client-Side Only:** No server-side anti-cheat, user data not recoverable.
- **Asset Budget:** Strictly monitor asset sizes; optimize aggressively.
- **Mobile Memory:** Avoid memory leaks; profile on iOS/Android browsers.
- **Performance:** Test on low-end devices, optimize draw calls and update loops.
- **Audio:** iOS/Safari may require user gesture to start audio.

---

### 14. **References**

- [Phaser.js 3.90.0 Documentation](https://phaser.io/docs/3.90.0)
- [Snib Platform Asset/CDN Guidelines](#)
- [HTML5 Game Optimization Guide](https://developer.mozilla.org/en-US/docs/Games/Techniques)

---

**This technical specification is tailored for rapid, scalable, and maintainable browser-based TD development on the Snib platform. All architectural, performance, and deployment decisions comply with the stated platform constraints.**

---

**Next Steps:**  
- Begin with core scene and asset pipeline setup.  
- Prioritize performance and asset optimization from the start.  
- Coordinate with design/art for sprite and audio atlas planning.  
- Review/update this document as implementation progresses.


---
*Generated on 7/17/2025*
