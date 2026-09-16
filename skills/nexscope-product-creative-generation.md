---
name: nexscope-product-creative-generation
description: >-
  Produce marketplace-ready product creative with Nexscope's creative skills —
  remove/replace the background, run a virtual try-on for apparel, then generate
  a studio image and a short product video — using the async task pattern and
  real Nexscope operations.
api: Nexscope Ecommerce Data and Creative APIs
generated: '2026-09-16'
method: generated
source: openapi/nexscope-openapi.json
operations:
  - runBackgroundRemover
  - runAiModelSceneBackgroundReplacement
  - runVirtualTryOn
  - runSeedream5ProImageGeneration
  - runSeedance25VideoGeneration
---

# Product creative generation workflow

All calls are `POST https://api.nexscope.ai/api/skill-api/v1/skills/{skill}/run`
with `Authorization: Bearer <NEXSCOPE_API_KEY>`. Creative skills require an
**active subscription** (trial credits do not enable Creative API access).
Inspect `code` (0 = success). Calls consume credits.

Creative skills are **asynchronous**: a `run` call returns a `taskId` and a
`status` (PENDING/RUNNING/SUCCESS/FAILED/TIMEOUT). Poll
`GET /api/skill-api/v1/skills/{skill}/tasks/{taskId}` (~5s interval, guidance
only) until terminal.

1. **Clean the source image** — `runBackgroundRemover`
   (`skills/background-remover/run`) for a clean cutout, or
   `runAiModelSceneBackgroundReplacement`
   (`skills/ai-model-scene-background-replacement/run`) to drop the product into
   a new scene.
2. **Apparel try-on (optional)** — `runVirtualTryOn`
   (`skills/virtual-try-on/run`) to place apparel naturally on a model image.
3. **Generate a studio image** — `runSeedream5ProImageGeneration`
   (`skills/seedream-5-pro-image-generation/run`) for a marketplace-ready hero
   shot. (Other model families are available — banana, wan, gpt-image-2, etc.)
4. **Generate a product video** — `runSeedance25VideoGeneration`
   (`skills/seedance-2-0-video-generation` family) for a short listing/ad clip.

Notes: there is **no documented cancel/undo** for a submitted generation task
(see conventions/nexscope-conventions.yml → reversibility) — confirm prompt and
inputs before submitting, since a failed or unwanted result still consumes
credits. No idempotency key, so a retried submit is a new billable task.
