# Voxel Kick - Browser-Based Voxel Car Soccer

## Concept & Vision

A low-gravity, moon-like car soccer game rendered in a voxel aesthetic. Players pilot a blocky car around a closed arena, flipping and boosting to strike an oversized ball into the opponent's goal. The feel is floaty and playful—part Rocket League, part Minecraft, with pastel colors and satisfying physics. Single player vs AI in a sandbox setup.

## Design Language

### Aesthetic Direction
Pastel voxel aesthetic—soft colors on chunky geometry. Think "cozy arcade in space." The voxel style is finer than Minecraft (roughly half the block size relative to object scale) for better readability.

### Color Palette
- **Primary (Player car)**: `#7EC8E3` (soft sky blue)
- **Secondary (AI car)**: `#E3A57D` (warm peach)
- **Ball**: `#F5F5DC` (soft cream) with `#FFD700` (gold) accents
- **Field/Ground**: `#C8E6C9` (soft mint green)
- **Walls**: `#E8D5E0` (dusty rose)
- **Goals**: `#FFB6C1` (light pink) for player, `#98D8C8` (seafoam) for AI
- **Sky/Background**: `#2D1B4E` (deep purple) gradient to `#5B4B8A` (muted violet)
- **Boost particles**: `#FFFACD` (lemon chiffon)
- **UI Text**: `#FFFFFF` with subtle shadow

### Typography
- **Primary**: "Press Start 2P" (Google Fonts) - retro pixel feel
- **Fallback**: monospace

### Motion Philosophy
- Floaty, low-gravity feel (jump arcs feel lunar)
- Car rotation is smooth but snappy on input
- Ball has satisfying bounce and momentum transfer
- Boost creates visible exhaust particles
- Camera follows car with slight lag for smoothness

## Layout & Structure

### Arena Layout (1v1 Medium)
- **Field**: ~80x50 voxel units
- **Walls**: 4 walls enclosing the field (no ceiling, open to sky)
- **Goals**: Opposing goal nets at each end, ~15 units wide, ~8 units tall
- **Ceiling**: None (open top for aerial plays)
- **Car scale**: ~3x2x4 voxels (width x height x length)
- **Ball scale**: ~4 voxel diameter (same as car width+height)

### Camera
- Third-person chase cam behind car
- Distance: ~15 units back, ~8 units up
- Smooth follow with lerp (0.1 factor)
- Looks slightly ahead of car's velocity

## Features & Interactions

### Core Mechanics

**Car Movement**
- W: Accelerate forward
- S: Reverse/brake
- A/D: Steer left/right (rotates car yaw)
- Space: Jump (single jump in air, double-jump available)
- Shift: Boost (limited fuel, regenerates on ground)

**Physics (Moon-like)**
- Gravity: ~1/6 of Earth gravity
- Air control: Full rotation control while airborne
- Ground friction: Moderate (cars slide slightly)
- Ball bounce: Elastic (0.8 restitution)
- Car-ball collision: Momentum transfer based on velocity

**Flip Mechanic**
- Double-tap space or press while airborne to flip
- Flips are directional based on last movement input
- Flip adds extra impulse to ball on contact

**Boost**
- Limited boost meter (100 units)
- Drains 30 units per boost activation
- Regenerates 15 units/second while grounded
- Boosts forward in car's facing direction
- Visual: Particle trail from car's rear

**AI Opponent**
- Simple state machine: Attack ball, Defend goal, Return to center
- Avoids walls with basic steering
- Occasionally jumps and flips toward ball
- Difficulty: Moderate (beatable but challenging)

### Scoring
- Ball fully crosses goal line = 1 point
- On score: Ball resets to center, both cars reset to starting positions
- No timer (sandbox mode)

### Controls Display
- Show current controls in corner
- Display score (Player vs AI)

## Component Inventory

### Car (Voxel)
- 3x2x4 voxel box composition
- Slightly rounded feel (chamfered edges via multiple boxes)
- Colored top/sides, darker undercarriage
- Wheels: 4 small voxel cylinders at corners
- States: Grounded, Airborne, Boosting (with particles)

### Ball
- ~4 unit diameter sphere made of voxels (icosphere approximation)
- Subtle rotation on movement
- Glow/shine effect
- Bounces off all surfaces

### Arena Walls
- Thick voxel walls (~2 units)
- Pastel color with subtle grid pattern
- Clear goal openings at each end

### Goals
- Frame made of voxels
- Net: Translucent or grid pattern
- Glows briefly on score

### UI Overlay
- Score display: "0 - 0" centered top
- Controls hint: Bottom-left
- Boost meter: Small bar near score

## Technical Approach

### Stack
- Single HTML file
- Three.js for 3D rendering (via CDN)
- No build step required

### Architecture
- Game loop via requestAnimationFrame
- Simple physics (no physics engine—custom velocity/collision)
- Voxel objects built from BoxGeometry primitives
- Collision detection: AABB for simplicity

### Performance Targets
- 60 FPS on modern browsers
- Low poly count (voxel aesthetic keeps triangles manageable)
- Instanced rendering where possible

## MVP Scope (V1 - Playable if Ugly)

1. ✅ Driveable car with keyboard controls
2. ✅ Ball with physics and bouncing
3. ✅ Arena with walls and goals
4. ✅ Basic AI opponent
5. ✅ Goal detection and scoring
6. ✅ Ball/car reset on score
7. ✅ Jump and double-jump
8. ✅ Boost mechanic
9. ✅ Score display
10. ⬜ Flip mechanics (stretch if time)

