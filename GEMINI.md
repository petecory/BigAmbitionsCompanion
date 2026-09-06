# Workspace Rules & Coding Guidelines

## Typography & Formatting Constraints
- **NEVER use em dashes ("—")**: Always use standard hyphens ("-") with space padding instead. Do NOT emit the em dash character anywhere in code, copy, user-facing text, comments, or documentation.
- **NO emojis**: Use Lucide React icons exclusively across the application UI.

## Code Standards
- Always verify TypeScript compiles cleanly with `npx tsc --noEmit` before finishing tasks.
- Keep the Executive Overview high-density and fit for a single desktop viewport.
- Never display mock/placeholder logistics or supply chain data until real telemetry routes are implemented.
- **ALWAYS use stylized custom dropdowns**: Never use raw, unstyled native HTML `<select>` elements. Dropdowns must be beautifully styled, theme-aware, custom popover components with search filtering where appropriate.
- **Always follow the facts when building something that relates to data, dont guess anything**: Never substitute synthetic constants, hardcoded guesses, or arbitrary fallbacks when real telemetry is missing or being calculated. Ground calculations strictly on recorded facts and historical data.

## Git & Deployment Rules
- **NEVER run `git push` under any circumstances unless the user explicitly tells you to push**: Commits and pushes to remote repositories (GitHub/Vercel) must strictly be requested by the user. Do NOT push proactively.

## Uncle Fred AI & Voice Engine Architecture
- **In-Game Voice Dataset**: 53 studio audio clips extracted from Big Ambitions reside on Desktop at `Desktop\UncleFred_AudioClips` and in `Desktop\uncle_fred_voice_dataset.zip`.
- **Dialogues Database**: Transcripts for all in-game Uncle Fred messages are stored in `web/src/data/uncleFredDialogues.json`.
- **Local Voice Engine (RTX 3060 12GB)**:
  - Runs a local FastAPI microservice at `engine/tts/server.py` on port `8020` (`http://127.0.0.1:8020`).
  - Uses XTTS-v2 with CUDA acceleration on the user's NVIDIA GeForce RTX 3060.
  - Startup script: `engine/tts/start_voice_engine.bat`.
  - Frontend client: `web/src/lib/uncleFredAudio.ts` with auto-playback and per-message replay buttons in `web/src/components/UncleFredAdvisor.tsx`.
- **Fine-Tuning Pipeline**:
  - Scripts located in `engine/training/`: `prepare_dataset.py`, `train.py`, and `run_training.bat`.
  - Transcribes and aligns the 53 clips using Whisper, then fine-tunes XTTS-v2 weights.

## Companion Mod & Telemetry Architecture
- **Shared C# Engine**: `mod/AmbitionProSync/TelemetryEngine.cs` (modVersion `2.3.0`).
- **Telemetry Endpoint**: Strict loopback HTTP server on `http://127.0.0.1:8765/` serving real-time JSON game state.
- **Steam Workshop Mod**: ID `3793615072`, native mod entry `mod/BigAmbitionsCompanion.Steam/BigAmbitionsCompanionNativeMod.cs` implementing `ModBigAmbitionsBase` with `[ModEntryOnCityLoad]`.
- **MelonLoader Standalone**: `mod/AmbitionProSync/AmbitionProSyncMod.cs`.
- **Workshop Showcase Screenshots**: Stored in `docs/images/` and referenced in Steam description via raw GitHub URLs.


