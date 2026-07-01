SPELLTRIS — The Complete Rundown

A full, detailed tour of everything the game is and does. Written to match the real code, feature by feature.

One line: SPELLTRIS is Tetris with words — letters rain down a deep-sea board, and any run that spells a real dictionary word clears like a line. Stack, spell, chain, and survive.

Shipping shape: the entire game is a single self-contained HTML file — one page, one script, no installs, no servers, no dependencies. Open it in a browser and it runs. That makes it trivial to host (GitHub Pages), share, back up, and mod.


1. The three game modes

Everything below is gated so the modes never bleed into each other.

Main (Classic)

The core game. Letters fall from the top under gravity. You steer each one and drop it so a run of letters spells a word. Columns that stack to the ceiling end the run.

Anti-Gravity

A completely different feel. No gravity. Each letter is fired in from an edge emitter and drifts/bounces around the board. You nudge the floating brick with thrusters and place it — it snaps to the nearest open cell and locks there, floating. Win by clearing the entire board; lose if the board floods (fills with no open cell for the next letter). Every brick is permanent until it's part of a word, so you only place letters you can actually use. Tunable emitter position, gravity bias, drift force, a float-fade, and its own auto-lock timer.

Sandbox

An in-browser live game editor. It plays like Main, but a control panel lets you free-edit the look and rules in real time and save / download / load your creation. Crucially, Sandbox is sealed off: it borrows the game's real defaults on entry and hands every one back, byte-for-byte, on exit — so Main and Anti-Gravity can never be changed by anything you do in Sandbox. (Full detail in §19.)


2. Core gameplay mechanics


Falling & steering. Move the active letter left/right; soft-drop to speed the fall; slow-fall to ease it; hard-drop to slam it down and lock instantly.
Aim by column. Tap any column on the board to send the piece there, or use the "+" drop bar above the board to pick the spawn column in real time.
Force a letter. Type any A–Z to force the next drop to be that letter — it costs 30% of your score, so it's a deliberate tool, not a free pick.
Tuck under overhangs. Press left/right toward a gap beneath a brick and the piece slides over and drops into the pocket in one move — no need to fall past the overhang first.
Lock in place. Beyond a normal landing, you can lock the brick in mid-air as a floating, gravity-immune platform (the same action the auto-lock timer triggers automatically).
Delete a falling brick. Stuck with a useless letter? Press ◀ and ▶ together to vaporize the falling brick. It costs half your current score and needs at least 2 points. When you can afford it, the brick slowly pulses blue (toggle that hint with Delete FX).



3. Word detection


Four directions. A run clears if it spells a dictionary word reading left→right, right→left, top→bottom, or bottom→top. The board is scanned across every row and column in both directions after each drop.
Shortest word. A minimum length setting decides how short a word can be to count (2 through 7). If you drop something that spells a real word but it's under the minimum, the game tells you.
Dictionary. ~39,300 words built in, all normalized to uppercase. You can add your own (see §17), and those persist in your browser.



4. Chains, combos, scoring, leveling


Chains. Clearing a word drops the stack above it. If that collapse spells another word, it clears too — and again, and again.
Combo multiplier. Each chain step raises a combo multiplier (×1.5 per step); longer words and higher levels score far more.
Leveling. You level up every N words (default 6), and the fall speed rises with each level. In Sandbox the "level up every N" pace is itself editable.
Live stats. Side panels track score, level, words, combo, plus deep metrics: fill %, danger %, tallest column, empties, locked count, letters dropped, vowel:consonant ratio, a per-letter frequency bar chart, words/min, pieces/min, average per word, best clear, longest word, best combo, max chain, letters cleared, engine speed, multiplier, tutor ops, dictionary size, and a words-by-direction breakdown (→ ← ↓ ↑) that even shows your backwards finds.



5. Backwards-word bonus

Spell a word that's valid only when read backwards — the tiles read RAF but clear as FAR — and you trigger a bonus. Play pauses, an amber banner appears, and you get to tap and delete a handful of bricks for free (as many as the word is long), each with the full molten-clear effect. Words valid in both directions (TAR / RAT) don't qualify — it must be a genuine backwards-only find on a single-word solve. Toggle the whole mechanic with the Bonus button. (Detection is exact: one distinct word with a right-to-left hit and no left-to-right hit.)


6. Auto-lock timer

Flip the Timer button to give every falling brick a countdown. A small ⏱ clock shows above the board; when it hits zero the brick locks itself in place wherever it is. Cycle Off → 30s → 15s → 8s. It exists in both Main (auto-locks in place, the automatic version of the Lock action) and Anti-Gravity (snaps to nearest open cell and locks) — turning a relaxed game into a race.


7. Piece & drop variations


Tic Tac pieces. Pieces become two connected bricks (side-by-side or stacked). Rotate them four ways with Enter or the ⟳ pad button. They fall, tuck, and lock as a unit.
Cascade (auto-sweep drops). The spawn column marches across the board on its own — → left-to-right, ← right-to-left, or ⇄ bouncing back and forth (Knight-Rider style). Each new brick spawns one column over from the last. Overrides the manual + bar and Random while on.
Random spawn. Pieces drop from a random column each time; the + bar turns red and locks.
Shotgun. Blasts random locked bricks across the board with a screen shake — instant, chaotic board-shuffle.



8. The letter supply


Bag: Even vs Weighted. Even gives every letter equal odds; Weighted uses realistic English letter frequencies (harder — more vowels and common letters, with a subtle hidden drift so runs feel varied).
Letter helper. Difficulty presets can quietly steer drops toward letters that actually complete words on your current board, so there's usually something to clear. Strong on Easy, occasional on Medium, off on Hard.



9. Coaching & readability


Tutor. Highlights every spot your current letter could complete a word — a coach, not autoplay. Especially powerful in Anti-Gravity, where you can place a letter anywhere it highlights. The Debug Monitor even audits what the tutor draws versus what's truly reachable.
Next preview. Show or hide the upcoming letter for an extra challenge.



10. Sentence challenge (& sentence dots)

Set a target sentence under the board. Spell each of its words in the game — in any order — and its chip lights up blue as the board flashes; finish the whole sentence to win. Any real word still clears normally even when it's nested inside a target (FIG inside FIGHT), and the target counts when you spell it in full. Tip: finish a long target in one move so a shorter inner word doesn't clear first. While a sentence is set, any falling brick whose letter appears in the sentence is ringed with red dots on all four sides so you can spot useful letters — toggle with Sentence Dots.


11. Restricted words (educators)

Type a word into Restricted words to ban it for the game. It will never clear, and whenever it appears its bricks glow red — great for steering students away from a target spelling, or keeping a specific word off the board.


12. Visual & audio production

This is where SPELLTRIS earns its look — a working forge running underwater.


Deep-sea, bioluminescent theme. A dark abyss background with drifting motes and slow glowing blobs, cyan/coral/jade/amber accents, and a glassy, blurred UI. Rounded Fredoka display font.
Molten-metal clears. Every cleared cell flashes white-hot and cools like stamped steel — white-amber → orange → deep red → into the abyss — over roughly 2.2 seconds on a real cooling curve, drawn behind the tiles so refilled cells cover it.
Molten falling bricks. The bricks that detach and tumble off the board are glowing metal too, cooling through the same color ramp as they spin and fade — fast when they fall fast, slow when they linger, exactly like real thermal mass. Works in both modes (falling in Main, drifting in Anti-Gravity).
Wispy smoke. Smoke curls up off cleared cells in front of everything (toggleable; the cooling glow stays regardless).
3-D lightning + thunder + camera kick. Each solve can fire a screen-space lightning bolt with a screen-blend flash, a thunder clip, and a real camera shake (applied to the page body so the electrified stage filter can't flatten it).
Storm Mode. An ambient background thunderstorm — random strikes roll through between solves.
Debris tumble. Cleared bricks spin off the board and fade; reduced-motion devices simply clear them without the tumble.
Sound. Landing, clearing, and UI cues, plus the thunder clip; fully mutable.



13. Watch the AI play (Demo & hand-off)


Watch Demo. From the start screen, let the game play itself — it picks a mode and drives a synthetic player that reads the board and places letters, all the way to game over.
AI Play (live hand-off). Mid-game, hand your current run to the AI — same mode, same board, no restart. A badge appears with Take Over (grab the game back and keep playing) and Exit. The AI adapts to settings you change on the fly.



14. Controls reference

Keyboard

KeyAction◀ ▶Move the falling letter left / right▼Soft drop (faster while held)▲Slow fall (ease the descent)SpaceHard drop — slam down and lockShiftLock the brick in mid-air as a floating platformEnterRotate a Tic Tac (two-brick) piece+ / −Speed the game up / downA–ZForce the next letter (costs 30% of score)◀ + ▶Press together to delete the falling brick (costs half score)EscPause/Mute`Open the Debug Monitor

On-screen pad mirrors all movement: ◀ ▶ move, ▲ slow, ▼ soft drop, Drop hard-drop, Lock, and ⟳ rotate. Tap a column to aim.


15. The control bar

Split into two rows: game functions on top, housekeeping below (dimmed slightly to read as secondary). Several buttons are compact icons now — ☰ Menu, ⏸ / ▶ Pause, ▶AI AI Play, ▦▦▦ Hide UI — each with a tooltip.


⇅ Button size — cycle every control-bar button through Small / Medium / Large for your screen (driven by one CSS variable).
▦▦▦ Hide UI — collapse the whole bar down to just this button; tap to bring it back.


Top row: Pause · ▶AI · Tutor · Next · Bag · Random · Cascade · Shotgun · Tic Tac · Timer · Delete FX · Sentence Dots · Bonus · Lightning · Storm Mode · Smoke · (Anti-Gravity tuners: Emitter, Gravity, Force, Timer, Float Fade).
Bottom row: Hide UI · Menu · Button size · Words · How to play · Sound.

(Mode-specific buttons hide automatically: classic-only buttons vanish in Anti-Gravity, and vice-versa.)


16. Difficulty presets

On the start screen, one tap bundles many settings:


Easy — 2-letter words, even bag, slow fall, Tutor on, strong letter helper (always something to clear).
Medium — 3-letter minimum, weighted bag, normal speed, occasional help.
Hard — 4-letter minimum, weighted bag, fast, next-piece hidden, no letter help — pure luck of the draw.
Custom — set Board width, Tile size, Fall speed, Shortest word, and the letter pool yourself. Touching speed or shortest-word flips you to Custom.



17. Dictionary management (Words)

The Words button opens a dictionary manager: add your own words, import and export word lists, and everything you add is saved on your device (localStorage) so it persists between sessions. Restricted words (§11) live alongside as a per-game ban list.


18. Debug Monitor + Built-In Test (power users)


Debug / Tutor Monitor. Press ` for a live diagnostics panel: active difficulty and letter-help, every mode, the falling piece, engine and board stats, and what the tutor draws versus what's actually reachable.
Black-box recorder. If an error ever occurs, the game auto-pauses and the panel opens so nothing is lost; you can page back through recent board snapshots or copy the full state. The event log is a ring buffer (last 60 events) and snapshots keep the most recent 8.
Built-In Test (BIT). A self-check that runs only on the home screen and restores itself afterward — it never touches a live game. It runs recorder self-tests plus headless game-engine checks that exercise the real word-finder, line-scanner, clear-detector, gravity, and nearest-empty logic on a private in-memory board using randomized, property-based (fuzz) inputs seeded fresh each run (the seed is shown, so any failure is reproducible). Validated across tens of thousands of runs; it has even caught flaws in its own tests rather than the game.



19. Sandbox mode — the in-browser editor

Pick Sandbox on the start screen. It plays like Main, with a live editor panel (top-right, collapsible) you can use while playing:

Board & rules


Board width / height (Apply & reset rebuilds just the sandbox board)
Shortest word (2–7), Fall speed, Level up every N words, Tile size (S/M/L), Auto-lock timer (Off/30/15/8s)
Rules checkboxes: Next-letter preview, Weighted bag, Random spawn, Tic-Tac pieces, Sentence dots, Lightning, Ambient storm, Smoke, Backwards-word bonus


Look


Color pickers for the main glow, background, deep background, coral, jade, amber, and text, plus the hot / mid / cool ember colors of the cooling-metal ramp — every change is instant.


Save your mod


Save / Load to browser storage, Download a spelltris-sandbox.json, Import someone else's, and Reset back to defaults. The – button collapses the panel.


The isolation guarantee (why Main & Anti-Gravity are safe). The instant you enter Sandbox, it takes a photograph of the real defaults — board size, shortest word, speed, level pace, tile size, every rule toggle, and all colors. The moment you leave (Menu), it hands every one of those values back, byte-for-byte. A guard also prevents re-photographing your edits as "defaults" if you restart the sandbox. This was proven in simulation: deliberately wrecking all 20+ values and then exiting returns the defaults identical to their original state. Sandbox's controls touch only the sandbox game; the other two modes cannot be edited and never change.


20. Modding the file directly

For anyone who wants to open the HTML and tinker, the file is dotted with plain-English notes at the spots people actually change — a welcome banner, the theme colors, board size (columns/rows/shortest word), the word list, the timer choices, level pacing, the hot-metal colors, fall speed, and the thunder-sound URL — plus short "you can leave this alone" one-liners over the heavy logic (the word-finder, gravity, the after-drop director, the self-test, and the AI). No jargon; just "change this number, save, reload."


21. Accessibility & robustness


Reduced motion is respected — the celebratory tumble is skipped for devices that ask for less motion.
Responsive layout — the board, tiles, and the "+" bar rescale to any width and board size; a taller board is used on narrow screens.
Self-healing — an error auto-pauses and records rather than crashing; the BIT keeps the engine honest.
Everything persists where it should (custom words, saved sandbox mods) and nothing where it shouldn't (Sandbox edits never leak).



22. Architecture at a glance


One file: all HTML, CSS, and JavaScript in a single page inside one IIFE — no build step, no dependencies.
Layered canvases for depth background, effects, the molten heat glow (behind tiles), and smoke (in front), plus a screen-space lightning canvas and a body-level debris layer.
CSS custom properties drive the whole theme and the control-bar sizing, which is exactly what makes live recoloring and the size stepper possible.
localStorage for custom words and saved sandbox mods.
Additive by design: every feature added over the project is gated so it never alters the classic or anti-gravity behavior — new modes and toggles sit beside the core, never inside it.



Feature checklist

Modes: Main · Anti-Gravity · Sandbox · Watch-Demo · live AI hand-off
Word play: 4-direction detection · adjustable minimum length · ~39,300-word dictionary · custom words · chains · combo multiplier · leveling
Mechanics: aim by column · "+" drop bar · force-a-letter · tuck-under · hard drop · lock-in-place · delete-a-brick · backwards-word bonus · auto-lock timer · Tic-Tac pieces · Cascade · Random spawn · Shotgun · Even/Weighted bag · letter helper
Coaching/UX: Tutor · Next preview · Sentence challenge · Sentence dots · Restricted words · difficulty presets · two-row icon control bar · button-size stepper · Hide UI
Production: molten-metal clears · molten falling bricks · smoke · 3-D lightning + thunder · Storm Mode · camera shake · bioluminescent depth background · sound
Power tools: Debug Monitor · black-box recorder · Built-In Test with headless fuzz engine checks
Safety: Sandbox isolation (byte-identical restore) · reduced-motion support · error auto-pause · in-file modder notes
