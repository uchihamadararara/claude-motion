# Motion Graphics Creation Guide

## Goal
Create a polished, premium motion-graphics explainer that visually demonstrates the idea **IDEA → CODE → MOTION**. The voiceover is about using Claude Sonnet and code to create motion graphics. The video must illustrate the narration, not merely place captions over unrelated moving shapes.

The voiceover timing is defined by `voiceover.srt`. The total duration is **54.596 seconds**. Follow the provided subtitle wording and timings exactly. Do not rewrite, translate, paraphrase, or invent extra narration. An actual voiceover audio file has not been supplied, so do not synthesize or pretend that a voice recording exists. Build the visuals to the subtitle timeline and use a restrained sound bed / carefully timed UI sound effects only if the repository's current sound pipeline can support them cleanly.

## Visual direction
- High-end motion-design showreel combined with a clear educational explainer.
- Core visual metaphor: an idea becomes structured code, code becomes animated graphics, then the result becomes a finished video.
- Use a restrained palette: warm off-white / charcoal / one vivid coral-orange accent. Keep contrast and text legibility high.
- Use one coherent type system. Prefer the fonts already installed in the repository; avoid adding unnecessary font dependencies.
- Make elements transform into the next scene. Prefer connected morphs, shape-to-type transformations, mask/reveal, dimensional layering, grid alignment, and precise kinetic typography over ordinary cuts and fades.
- Include moments of UI-style motion, code becoming visual forms, charts/diagrams that draw themselves, and one convincing 2D-to-3D depth moment. Keep each technique relevant to the exact narration at that time.
- Use spring-like motion with controlled settling and tiny overshoot at most. Keep easing deliberate and consistent.
- Use clear foreground/midground/background depth through scale, overlap, lighting/shading and parallax within a fixed composition. No fake depth made only from a random blur.
- Make something meaningful happen frequently. At 120 BPM, a beat is 0.5 seconds, so use the beat as a timing reference if helpful. Do not force a visible action on every beat when it harms readability.
- Sound effects, if used, should be subtle, precisely timed to visible actions, and never irritating. Do not let the sound bed overpower spoken-word space.

## Avoid
- Generic template-looking scenes, random decorative captions, filler subtitles, unrelated text, and narration that is not in the supplied SRT.
- Repeated fade-in/fade-out animation as the main transition method.
- Bouncy easing, excessive overshoot, constant zooming, camera shake, glows, lens flares, RGB split, particle bursts, noisy gradients, and gratuitous effects.
- Static holds longer than necessary, cramped typography, elements colliding, unreadable tiny labels, inconsistent icon strokes, and motion that is unrelated to the meaning.
- Any claims on screen that are not supported by the voiceover or this brief. The existing narration says the experiment was made with Claude's free plan; it does not mean all rendering infrastructure is universally free.

## Story flow aligned to the SRT
Use these as story beats, not as rigid scene boundaries. Preserve visual continuity by transforming the prior scene into the next where possible.

1. **00:00–00:05 | Hook: AI beyond answers**  
   Start with a strong visual hook. A simple AI/chat interface answers with text, then the answer expands into a living motion-graphics canvas. The transition should immediately communicate that the AI can create a whole animated video, not just text. Avoid a generic chatbot mockup that simply fades away.

2. **00:05–00:10 | The surprising free-plan reveal**  
   The animated canvas condenses into a clear “FREE PLAN” / Claude-related typographic moment, then seamlessly feeds the next scene. Keep the claim visually restrained and avoid copying official branding assets unless already present in the repository.

3. **00:10–00:15 | Give an idea to Claude Sonnet**  
   Show a compact idea card or sketch being translated into structured code. Code lines should be purposeful visual elements, not large blocks of unreadable fake code. Show a relationship between the idea and the resulting composition.

4. **00:15–00:20 | Kinetic typography**  
   Make typography the main animated subject. Letters/words can assemble, stretch, mask, and lock to a clean grid. The visuals should demonstrate actual kinetic type rather than add a floating title on top of unrelated shapes.

5. **00:20–00:25 | Graphics, transitions, sound**  
   Show a coherent sequence of animated shapes/diagram/chart/UI elements. Use a visible transition that transforms one element into the next. If a sound cue is used, synchronize it to a visible action.

6. **00:25–00:30 | No After Effects / no manual frame-by-frame work**  
   Show a timeline or stack of manually placed frames collapsing into a concise code-driven system that controls many frames. Do not make unsupported claims about replacing all professional tools; illustrate the exact contrast in the narration.

7. **00:30–00:35 | Idea → Claude Sonnet → code → render**  
   Create a clean, satisfying pipeline diagram. Each stage should activate in order, and the last stage should turn into the actual animated result. This is a central visual payoff.

8. **00:35–00:40 | Free plan emphasis**  
   Reinforce the free-plan message with a simple confident typographic moment that grows out of the previous scene. Avoid flashing labels or sales-ad styling.

9. **00:40–00:45 | AI is more than text**  
   A text response turns into useful visual objects: typography, shapes, a UI component, and a graph. Clearly show the shift from text output to an actual animation system.

10. **00:45–00:50 | Ideas become actual animation**  
    Deliver the strongest transformation: a rough idea/sketch becomes structured code and then a layered, dimensional animated composition. This should be the visual climax, with clear depth and clean motion rather than effects for their own sake.

11. **00:50–00:54.596 | Audience question / ending**  
    Resolve into a bold, legible question based on the exact final subtitle. Finish cleanly. A seamless loop is welcome only if it can be achieved without damaging the ending or subtitle readability.

## Technical rules for this repository
- This project is an existing **Remotion + React + TypeScript** project. Continue using its architecture. Do not replace the whole repository with a standalone HTML file just because one reference technique mentions HTML.
- The repository currently registers `EffortVideo` and `ArticleCover` in `src/Root.tsx`.
- The current `EffortVideo` composition is approximately **22 seconds, 1080×1080**, using `FPS` and timeline values from `src/lib.ts` / `timeline.json`.
- `package.json` currently renders `EffortVideo` to `out/effort-silent.mp4`, generates sound using `npm run sfx`, then muxes to `out/effort.mp4` via ffmpeg. The `build` script runs `sfx`, `render`, and `mux`.
- `.github/workflows/render.yml` runs `npm ci`, installs Remotion's browser, executes `npm run build`, and uploads `out/effort.mp4` as the `claude-motion-video` artifact.
- Therefore, inspect the real source files and existing project instructions before editing. Add a **new dedicated composition** for this 54.596-second video and preserve the existing `EffortVideo` demo. Update the rendering script and GitHub Actions workflow so they explicitly render the new composition and upload the matching output path. Do not leave the workflow silently rendering the old 22-second square demo.
- Target **1920×1080, 16:9, 60 fps** if the current pipeline supports it reliably. At 60 fps the requested 54.596-second duration must be represented by an integer frame count, so a tiny frame-grid rounding difference is expected. Keep the subtitles timed to the supplied SRT as closely as frame boundaries allow.
- Use deterministic frame-based animation. Avoid runtime timers or animation state that changes unpredictably between renders. Remotion components should render correctly for any frame/scrub position.
- Do not fake having reviewed a rendered video. Render drafts, inspect representative frames/contact sheets, fix layout or animation defects, and render again. Verify the final MP4 exists and is playable before reporting completion.
- Keep dependency changes minimal. Run the available typecheck/build/render commands and report any checks that could not be completed.
- Upload the final MP4 as a GitHub Actions artifact. Avoid committing the rendered MP4 into the normal source repository unless there is a specific reason; generated video files should generally be delivered as workflow artifacts.

## Reference video files
If these files are present in the repository root, treat them as visual references:
- `reference-motion-01.mp4`
- `reference-motion-02.mp4`

Inspect them only as reference material. If direct video viewing is unavailable in the coding environment, use FFmpeg to extract a few evenly spaced representative frames/contact sheets when available. Borrow pacing, depth, transitions and visual treatment, but do not copy unrelated text or reproduce the reference videos shot-for-shot. The supplied SRT and this guide remain the source of truth for the new video. If the reference files are absent or cannot be inspected, continue using the written direction below and do not stop the project.

## Guidance from the supplied motion-design references
- One UI element can morph through multiple states: button → loader → check → music player → slider → toggle → tab indicator → chart → command palette → toast. Use this as inspiration for continuous morphing and direct-manipulation logic, not as a mandatory literal sequence for this explainer.
- A strong short motion-design reel uses a limited palette, one type system, kinetic typography, shape morphing, a UI/data moment, a clear 2D-to-3D moment, and a strong title ending. Adapt the techniques to this full-length voiceover rather than shortening the video to 15 seconds.
- A recipe/cocktail reference demonstrates how measurements, components and progress can appear in a clear step-by-step explainer. Borrow its clarity and incremental assembly only where it helps explain the idea-to-code-to-motion pipeline; do not add cocktail content.

## Required review before calling it finished
1. Verify every subtitle line and timestamp against `voiceover.srt`.
2. Create a storyboard/timeline before implementation, then continue through implementation instead of stopping at the storyboard.
3. Run typecheck and the actual render pipeline.
4. Inspect a contact sheet or representative frames across the whole video, especially every scene transition and the final title.
5. Fix overlapping/missing text, weak depth, generic fades, inconsistent style, empty holds and sound effects that feel too loud or random.
6. Confirm the final video duration, resolution, frame rate, output location, and GitHub Actions artifact name. State honestly whether a full render and visual inspection succeeded.
