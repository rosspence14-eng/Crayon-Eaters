# Crayon-Eaters

Crayon Lava Escape — 24-Hour Hackathon Design Brief

Document purpose: Turn the initial concept into a buildable, testable plan for a 24-hour hackathon. This is a focused game-design brief, not a promise of a large content-heavy release.

1. Recommended direction

Build a short, single-player 2D puzzle-platformer in which the player escapes a sequence of illustrated rooms while a floor-level lava hazard rises. The main hook is the contrast between childlike crayon art and urgent, readable platforming.

For the hackathon, aim for three compact rooms that teach, remix, and culminate in the same core interaction language. Each room should take roughly 30–75 seconds on a successful run. The player should understand the objective immediately, be able to experiment without a long penalty, and restart in one button press.

Recommended first playable: one complete room with movement, jumping, one reusable push/interact object, a rising hazard, an exit, a death/restart loop, and a clear win state. Make this feel good before adding more rooms or bespoke mechanics.

2. Product snapshot

•
Genre: 2D side-view puzzle-platformer / time-pressure escape game

•
Players: Casual players who enjoy quick, readable challenges

•
Session: A short run of several rooms; each room is self-contained

•
Engine/platform: Godot; target a desktop build first, and export to web only if the hackathon requires it and the team has time to test that export

•
Camera: Fixed side view per room; no scrolling for the MVP

•
Core promise: “Read the room, improvise with its objects, then make your escape before the lava catches up.”

•
Visual identity: Familiar school and home spaces drawn as rough elementary-school crayon illustrations

3. Design pillars

1.
Readable at a glance. The exit, hazard, usable objects, safe surfaces, and intended route are visually distinct.

2.
Think fast, not guess. The player should infer the puzzle from the room layout and object affordances, not search for hidden items or test arbitrary combinations.

3.
Aha, then execute. Each room has one central idea; the tension comes from applying it and traversing the route under pressure.

4.
Failure is cheap. Death restarts the room quickly, with no lost progress outside that room.

5.
Crayon charm, crisp gameplay. Art can be uneven and scribbly, but collision boundaries, hazards, and interactions remain legible.

4. Core gameplay loop

1.
Enter a room and see the exit, lava start point, and key objects.

2.
The lava begins moving after a short, consistent grace period.

3.
Read the room and identify which object or surface changes the route.

4.
Solve the room’s one main puzzle, typically by moving, activating, or repositioning an object.

5.
Platform across the resulting route while managing the rising hazard.

6.
Reach the exit to lock in success and move to the next room.

7.
If caught or falling into the hazard, restart that room immediately.

Important pacing recommendation: Start the hazard after a brief entry/read window (about 2–4 seconds), rather than instantly. This preserves pressure without making the puzzle feel unfair. If playtests show players are still confused, add an optional visual cue or a slightly longer grace period before making puzzles easier.

5. Player controls and feel

Use a minimal control set for the first playable:

•
Move: A/D or Left/Right

•
Jump: Space (support press-to-jump and variable jump height if inexpensive)

•
Interact / grab / release: E or a context-sensitive key

•
Restart room: R

•
Pause: Escape

Prioritize responsive acceleration, predictable air control, and a forgiving jump buffer / coyote-time window if the engine makes these easy. Tune movement before building room content; platforming that feels unreliable will make every puzzle feel worse.

Interaction recommendation: Give objects a clear outline or small prompt when the player is in range. If the team cannot make a robust carry system quickly, use a simple pushable object or a one-button “move object” interaction instead of implementing a broad inventory system.

6. Hazard rules

•
Lava rises from the bottom of the room at a steady, visible rate.

•
The safe region should shrink in a way players can read; use a distinct animated edge, glow, or scribbled line.

•
On contact, trigger a brief burn/fail effect, then restart the same room quickly.

•
Lava must not obscure important platforms or interaction prompts.

•
Avoid surprise hazard changes in the MVP. A steady rise gives players a fair mental model and is simpler to tune.

Tuning target: A competent first-time player should usually have enough time to understand the room and attempt the route, while a deliberate or inefficient run becomes dangerous. Use playtest observations—not intuition alone—to tune the speed and grace period.

7. Puzzle rules and authoring template

Each room should generally contain:

•
One objective: obvious from the exit or a short prompt

•
Two or three relevant interactables: more objects create noise and implementation cost

•
One main puzzle idea: for example, move a chair to reach a shelf, then use a book stack as a stepping stone

•
A visible solution path: the player can reason from object placement and silhouettes

•
A short discovery window: target 15–45 seconds to understand and solve, followed by the execution challenge

•
A clear failure recovery: restart without a long death animation or loading screen

Avoid hidden keys, pixel hunting, multi-step inventory chains, physics contraptions, and puzzles whose only clue is written text. Prefer visual cause and effect. The exit should be visible from the start whenever possible.

Room design test

Before implementation, describe each room in one sentence: “Move/activate X so that Y becomes reachable; then jump across Z to the exit.” If the team cannot express the room that simply, it is probably too complicated for the MVP.

8. Suggested three-room sequence

Use these as prototypes, not mandatory content. Reuse the same interaction system wherever possible.

Room
Setting
Main idea
Teaches / tests
1
Classroom
Push a chair under a low shelf or platform to create a step
Movement, jumping, object interaction; generous hazard timing
2
Kitchen
Move a lightweight stool or crate to bridge a gap or reach a counter
Apply the known interaction with tighter traversal
3
Living room or library
Reposition two familiar objects in a clear order to reach a high exit route
A short remix and final execution test




Keep the third room’s two-step sequence visually obvious; do not add a new control scheme just to make the finale harder. If time is tight, ship two well-tested rooms rather than three unfinished ones.

9. Art direction and readability

Look

•
Crayon outlines with variable thickness, scribbled fill, imperfect coloring, and simple looping animations

•
Bright paper-like background; familiar props drawn with simple silhouettes

•
Small palette per room, with strong color contrast between player, platforms, interactables, exit, and lava

•
Slightly imperfect hand-drawn presentation without visually noisy gameplay surfaces

Gameplay readability rules

•
Use consistent visual language for interactable objects (e.g., a thick outline, small sparkle, or prompt)

•
Use a unique, high-contrast color treatment for lethal lava

•
Make safe platforms solid and visually distinct from decorative background art

•
Do not rely on color alone: use shape, outline, motion, or labels as a second cue

•
Draw the player with a distinct silhouette that remains readable against all room palettes

Scope-safe art pipeline

Use a small set of reusable assets: player, exit, lava, a few platform/background pieces, and only the props required by the chosen rooms. The paper-and-crayon look is the signature, but the number of drawings must stay tightly bounded. Prioritize one appealing player animation, an animated lava edge, and a few expressive object/exit details over fully animated scenery.

Paper-to-Godot art pipeline

1.
Set the frame before drawing: choose a consistent game resolution/aspect ratio and decide the approximate on-screen size of the player and props. Draw each animation pose on the same-sized paper or inside a measured frame guide; keep the character’s feet and center position consistent from frame to frame.

2.
Capture consistently: scan if available; otherwise photograph straight-on in bright, even light. Keep the paper flat, avoid shadows and perspective, and capture all frames with the same camera distance and lighting.

3.
Clean only what is needed: crop, rotate, and adjust levels/contrast so the crayon marks read. Remove the paper background or make it transparent only when necessary; a lightly textured paper background can instead be used as a deliberate full-screen backdrop. Export assets as PNG.

4.
Keep frame registration stable: put animation frames on equal-sized canvases with a consistent pivot/feet position. Name them in order (for example, player_idle_01.png, player_idle_02.png). Test the sequence in-engine early; do not wait until every drawing is finished.

5.
Import and animate in Godot: use AnimatedSprite2D with a SpriteFrames resource for short frame-by-frame loops (idle, run, jump/fall, and optionally hurt). Use AnimationPlayer for simple non-frame-by-frame changes such as lava-edge position, exit pulse, or UI feedback. Keep collision shapes independent of the wobbly drawn outline.

Animation scope: A 2–4-frame idle and 4–6-frame run are enough to establish the handmade feel; use a single pose or a small 2-frame loop for jump/fall if needed. The lava can use 2–3 drawn edge frames or a static scribble with a simple animated rise. Avoid drawing unique full animation sets for every prop. Reuse static prop drawings and animate them with a small tilt, bounce, or scale change in Godot where appropriate.

Production guardrails: Assign one person to draw/capture while another integrates graybox gameplay, if team size allows. Agree on naming, dimensions, transparent-background rules, and a shared asset folder before parallel work. Import one rough character and one room prop early to validate the look at actual game scale. If capture or cleanup starts taking too long, keep visible paper texture and simplify to fewer frames rather than sacrificing the playable loop.

10. Audio and feedback

Audio is optional for the first playable but high value if it can be added quickly. Prioritize:

•
Soft rising/sizzling loop that signals increasing danger

•
Distinct jump and landing sounds

•
A satisfying interaction sound

•
A short failure cue and a clear success sting

Use non-audio cues too: subtle screen shake or flash on failure, a lava-edge pulse, and a small “Room Clear” moment. Keep effects brief so restarts stay fast.

11. MVP scope and cutline

Must have

•
One playable character with reliable movement and jump

•
One complete room as the minimum viable slice; aim for two or three static rooms only after the slice is stable

•
One reusable object interaction, such as pushing or grabbing/releasing

•
Rising lava hazard with visible movement and collision

•
Exit detection, room completion, death, and instant room restart

•
Clear start/retry/win flow and basic instructions

•
Consistent crayon visual treatment, even if assets are simple

Should have if time allows

•
Three polished rooms with increasing challenge

•
Basic sound effects and a music/hazard loop

•
Simple room transition, title screen, and end card

•
A small amount of squash/stretch or object feedback

•
Best-time display or total completion time

Cut first if behind schedule

•
More than one interaction type

•
Moving platforms, enemies, combat, collectibles, branching routes, or procedural rooms

•
Complex physics, inventory, checkpoints within a room, or a level editor

•
Multiple character abilities, story scenes, dialogue-heavy exposition, or elaborate menus

•
Any art polish that delays a complete playable loop

Scope guardrail: Do not add a feature unless it improves the readability, satisfaction, or replayability of the core room loop and can be completed without threatening the first complete room.

12. Build order for a 24-hour hackathon

A suggested sequence (adjust to team size and tools):

1.
0–2 hours — Align and prototype: agree on Godot version, target platform, controls, room dimensions, collision rules, art dimensions/naming, and visual references; create a graybox test room and capture/import one sample drawing.

2.
2–6 hours — Core movement: implement movement, jumping, platforms, hazard collision, exit, death, and restart. Test the feel immediately.

3.
6–10 hours — First complete room: add the selected object interaction and one solvable puzzle; ensure a full start-to-win loop works.

4.
10–14 hours — Make the game legible: import the first consistent paper-drawn assets, add the crayon style, hazard animation, interactable cues, simple HUD/instructions, and audio if easy. Validate all art in-game at final display scale.

5.
14–18 hours — Add room variations: build room two and, only if on schedule, room three using existing mechanics and assets.

6.
18–21 hours — Playtest and tune: have someone unfamiliar play without coaching; fix confusion, unfair jumps, softlocks, and unclear interactions.

7.
21–24 hours — Stabilize and present: fix critical bugs, test a fresh build, prepare title/end screens and a short demo, and avoid risky feature additions.

For a small team, assign clear ownership (core gameplay, rooms/art, integration/audio) but keep one person responsible for integration and playable builds. Integrate continuously; do not wait until the final hours to combine work.

13. Playtesting and success criteria

Run short tests with people who did not design the rooms. Observe silently before explaining anything.

Track:

•
Can players identify the exit and hazard within a few seconds?

•
Do players notice the relevant object and understand how to interact with it?

•
How long does it take to discover the intended solution?

•
Do deaths feel earned, or do players blame unclear controls / invisible collision?

•
Can players restart and attempt again immediately?

•
Does the room teach something that the next room reuses?

Hackathon success criteria: A new player can begin without explanation, understand the core premise, solve and escape at least one room, and describe the crayon style or lava pressure as a memorable hook. If the build has three rooms but the first is confusing, it is not a successful scope trade.

14. Key risks and mitigations

Risk
Why it matters
Mitigation
Puzzle and hazard compete for attention
Players may feel rushed before they understand what to do
Brief grace period, stable hazard speed, clear object cues
Platforming feels imprecise
Repeated failures seem unfair rather than challenging
Tune movement in a graybox before level production; add coyote time / jump buffering if practical
Crayon visuals reduce contrast
Important objects and platforms become hard to parse
Keep gameplay silhouettes bold; reserve rough texture for fill and decoration
Too many bespoke mechanics
Integration and debugging consume the hackathon
One reusable interaction; vary room layout, not systems
Content is added before the loop is fun
Many rooms amplify weak controls or confusing rules
Complete and playtest one vertical slice first
Team integration happens late
Individually finished pieces may not work together
Use shared conventions and frequent playable builds




15. Decisions to confirm

The document assumes a keyboard-controlled Godot desktop game and a small team. Before implementation, confirm:

1.
Which Godot version and target platform are you using (desktop, web, or both)?

2.
How many people are on the team, and what are their strengths (programming, art, audio, design)?

3.
Is the judging/demo format more important than a replayable game, and is there a required theme or platform?

4.
Do you want a rising lava floor in every room, or should a few rooms use spreading lava while keeping the same core rules?

5.
Should the game have a story wrapper (e.g., a child’s imagination during a school day), or stay purely arcade-like?

These answers can tune the schedule and technical plan, but they are not blockers for starting with the graybox first room.

