# Protocol: Persona Calibration

**Principle:** Personas should improve based on evidence about their judgments, not self-confidence.

## When to calibrate

Update calibration when a persona:

- Makes a useful material catch that should increase trust in a specific review lane.
- Produces a false positive, especially an unsupported claim that something is missing or broken.
- Misses a material issue another reviewer or runtime evidence catches.
- Causes avoidable rework through unclear ownership, weak handoff, or stale assumptions.
- Repeatedly catches useful issues in a specific domain.
- Produces a noisy review or a meaningful strong/weak assignment-fit signal.

Do not create a calibration entry merely because a persona participated in a review or task. Use calibration during Talent Planning, reviewer selection, AARs, and model-selection updates only when the session produced one of the signals above.

## Storage

Store member-specific calibration in:

```text
management/personas/<member-slug>/calibration.md
```

Use `management/calibration/team-calibration.md` only when a project needs cross-team rollups.

## Calibration entry format

```markdown
## <YYYY-MM-DD> - <Session or review label>

**Role in session:** owner / reviewer / advisor / executive
**Evidence:** files, tests, review findings, user feedback, AAR, or final result
**Signal:** bug caught / bug missed / false positive / noisy review / strong assignment / weak assignment / verification gap
**Impact:** quality, speed, safety, trust, rework, or cost
**Adjustment:** how future assignment, review, or persona behavior should change
**Promote to persona.md:** yes/no
**Review cadence:**
```

## Metrics to track

Prefer simple counts and recent examples over complex scoring:

- Real issues caught.
- Real issues missed.
- False positives, especially unsupported "missing" or "broken" claims.
- Review comments accepted vs. declined as noise.
- Rework caused or prevented.
- Verification gaps caught before final.
- Handoff clarity.
- Learning adoption: whether previous calibration changed later behavior.

## How to use calibration

- Prefer reviewers with recent evidence of useful signal in the domain.
- Add a second reviewer when calibration shows a persona has blind spots.
- Update `persona.md` when calibration changes mission, review lens, risks, success signals, or development focus.
- Use `learnings.md` for one-off lessons and `calibration.md` for evidence about judgment quality over time.
- Do not punish experimentation. Calibration is for routing and improvement, not blame.

## Atlas's role

- Capture calibration evidence when review quality changes trust in a persona.
- Use calibration before assigning reviewers or accepting high-impact recommendations.
- Prune stale calibration during Talent Planning.
