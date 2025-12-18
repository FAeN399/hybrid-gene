# QA Checklist

Verification steps before integration.

---

## Pre-Merge Checklist

### Code Quality
- [ ] No hardcoded IDs outside allocated range
- [ ] No debug code left in (console.log, test values)
- [ ] Consistent naming conventions
- [ ] No commented-out code blocks

### ID Compliance
- [ ] All new IDs within assigned range
- [ ] ID-Register.md updated
- [ ] No collisions with existing IDs

### Functionality
- [ ] Feature works as described
- [ ] No regressions in existing features
- [ ] Edge cases handled

### Documentation
- [ ] Code comments where non-obvious
- [ ] README updated if needed
- [ ] Changelog entry prepared

---

## Monster Checklist

- [ ] Species ID valid (1-4)
- [ ] Generation valid (1-4)
- [ ] Base stats within expected range
- [ ] Birthmark ID exists
- [ ] Available moves reference valid Move IDs
- [ ] Sprite/art assets present (or placeholder noted)

---

## Move Checklist

- [ ] Category correct
- [ ] Energy cost balanced
- [ ] Cooldown reasonable
- [ ] Damage formula tested
- [ ] Status effects reference valid Effect IDs
- [ ] Animation/VFX noted

---

## Combat Checklist

- [ ] Damage calculation correct
- [ ] Obedience roll working
- [ ] Core AI activates on ignored commands
- [ ] Energy regeneration decays over time
- [ ] Status effects apply/expire correctly
- [ ] KO state handled

---

## Breeding Checklist

- [ ] Same-species requirement enforced
- [ ] Same-generation requirement enforced
- [ ] Stat inheritance formula correct
- [ ] Move inheritance filters by species
- [ ] Birthmark randomly generated
- [ ] Cooldown applied to parents

---

## Capture Checklist

- [ ] HP threshold check (< 25%)
- [ ] Success rate scales correctly
- [ ] Wake chance on continued battle
- [ ] Carry state applies speed penalty
- [ ] Temperament starts low for wild captures

---

## Performance Checklist

- [ ] No frame drops in battle (60 FPS target)
- [ ] Memory usage stable
- [ ] No infinite loops
- [ ] Asset loading optimized

---

## Final Sign-off

```
Reviewer: _______________
Date: _______________
Branch: _______________
Verdict: [ ] APPROVED  [ ] REJECTED
Notes: _______________
```
