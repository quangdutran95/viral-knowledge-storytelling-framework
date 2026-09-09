# Changelog

## [1.9.1] - 2026-09-09

### Added
- VKSF Chat Orchestrator protocol.
- Strict 12-phase default execution order.
- User-facing phase progress headers.
- Anti-skip checklist preventing direct jump to Angle/Hook/Script.
- `/full`, `/batch`, `/story`, `/hook`, `/analyze` routing rules.
- `VKSF-CHAT.md` ChatGPT invocation guide.

### Changed
- Default `VKSF: {topic}` now explicitly maps to the full pipeline.
- AI-COS must parse and route commands before calling specialist engines.
- Unsupported/skipped phases must be explicitly marked instead of silently omitted.

## [1.9.0] - 2026-09-09

### Added
- Communication Concept Intelligence Layer.
- Concept-as-mechanism model.
- Concept Library with mechanism, use case, perception shift, strength and risk.
- Perception Transformation engine.
- Concept Stacking.
- Concept Matrix.
- Truth Gate for factual accuracy, context, numbers, scarcity, comparison and promise safety.
- Concept propagation from title/hook into narrative, micro-hook, visual, emotional beat and payoff.
- Separate Concept Intelligence prompt.
- Concept Intelligence Map template.

### Changed
- End-to-end architecture now flows through Communication Concept before Title/Hook.
- Hook design is no longer only wording optimization; it includes perception transformation and concept selection.
- Learning can track winning communication concepts alongside hooks, angles, stories and territories.

## [1.8.0] - 2026-09-09

### Added
- Retention Intelligence Engine.
- Segment-by-segment retention modeling.
- Retention Curve Map as a pre-publish prediction layer.
- Micro-Hook Engine.
- Question Chain retention checks.
- Progress Engine for information/story/emotion/meaning progress.
- Swipe-Risk Engine.
- Emotional Rhythm analysis.
- Micro, Mid and Final Payoff timing.
- Retention Score /100.
- Automatic retention rewrite loop when score is below threshold.
- Performance learning: predicted retention vs actual retention.

### Changed
- Production Pack now includes a Retention Map before storyboard generation.
- Narrative Intelligence is now evaluated together with retention dynamics.
- Full Auto pipeline now runs Retention Intelligence before Production.
- Quality Gate includes progress, micro-hook, swipe-risk and payoff timing checks.

## [1.7.0] - 2026-09-09

### Added
- Narrative Intelligence Engine.
- Story Mining, Story Worthiness, Tension Engine, Question Chain, Micro-Detail Engine, Story Loop Engine, Turning Point, Emotional Payoff and Meaning extraction.

## [1.6.0] - 2026-09-09

### Added
- Content Universe Intelligence Layer.
- Universe Core, Territory Map, Theme Matrix, Content Gap Detection, Coverage, Cannibalization and Saturation logic.

## [1.5.0] - 2026-09-09

### Added
- Story + Angle + Hook Intelligence Layer.
- Source classification, Worldview/Reframe, Angle Matrix, Hook Matrix and Promise → Payoff contract.

## [1.4.0] - 2026-09-09

### Added
- Personal Storytelling Engine.
- Experience Engine, Problem Mining, Worldview/Reframe and Mirror Story.
- Content Universe architecture.

## [1.3.0] - 2026-09-09

### Added
- AI Content Operating System.
- Batch, Production, Learning and Full Auto modes.

## [1.2.0] - 2026-09-09

### Added
- Batch Content Factory.
- Prioritization, duplicate/cannibalization checks, clustering and calendar.

## [1.1.0] - 2026-09-09

### Added
- Master Prompt v1.1.
- Topic diagnosis, angle selection, hook engine, retention check and quality gate.

## [1.0.0] - 2026-09-09

### Added
- VKSF system foundation, emotion, retention, story, knowledge, whiteboard, ending, share and analytics systems.
