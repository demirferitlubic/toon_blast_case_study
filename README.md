# Toon Blast — Product Case Study

## Overview

This is a case study on **Toon Blast by Peak**.

The purpose of this project is to analyze a real player experience problem, propose a product solution, define the relevant primary metrics, supporting metrics, guardrail metrics and design an experiment to evaluate whether the solution creates measurable value.

The analysis focuses on one question:

> **How can Toon Blast reduce player frustration after repeated level failures without removing the challenge that makes progression rewarding?**

---

# 1. Understanding the Product

Toon Blast is a level-based puzzle game where players clear cubes, create combinations, use power-ups, and complete level-specific objectives within a limited number of moves.

A simplified core loop is:

**Enter Level → Solve Puzzle → Win or Fail → Receive Progress/Rewards → Continue**

When a player wins:

**Win → Progress → Rewards → Next Level**

When a player loses:

**Fail → Retry / Use Resources / Leave Session**

The second flow is particularly interesting from a product perspective since a failed level is not necessarily a negative experience. Difficulty creates challenge, and challenge makes progression rewarding.

However, repeated failures can potentially move the player from:

**Challenge → Frustration → Session Exit**

The product problem is therefore not simply:

> "How can we make difficult levels easier?"

Instead, the question should be:

> **How can we preserve difficulty while reducing unnecessary frustration?**

---

# 2. Product Problem

Imagine a player who encounters a difficult level.

The journey could look like this:

```text
Attempt 1 → Fail
Attempt 2 → Fail
Attempt 3 → Fail
Attempt 4 → ?
```

At this point, several behaviors are possible.

The player might:

- retry immediately,
- use a booster,
- spend resources,
- take a break,
- or leave the session entirely.

Repeated failures may be healthy when the player still believes the level is achievable.

The problem appears when the player stops thinking:

> "I can beat this."

and starts thinking:

> "I'm stuck."

From a product perspective, this creates an important intervention point.

---

# 3. Product Goal

The goal is to:

**Increase continued engagement among players experiencing repeated level failures without significantly reducing game difficulty or monetization potential.**

This means simply giving players unlimited moves would be a bad solution.

It would solve frustration by destroying part of the challenge.

The intervention needs to be limited and targeted.

---

# 4. Hypothesis

### Hypothesis

> If players receive a small temporary assistance option after several consecutive failures on the same level, they will be more likely to continue playing instead of ending the session.

The intervention should only appear when there is evidence that the player is struggling.

For the initial experiment, I would define this trigger as:

**3 consecutive failures on the same level.**

The exact number should eventually be determined through player data.

---

# 5. Proposed Feature — Retry Assist

After failing the same level three consecutive times, the player receives a one-time **Retry Assist** before the next attempt.

Example:

```text
That was close!

Choose one boost for your next attempt:

[ Rocket ]     [ Bomb ]
```

The player chooses one temporary starting advantage for the next attempt.

The feature has several important characteristics:

### It is triggered by behavior

The feature does not appear for every player.

It appears only after repeated failures.

### It maintains player agency

Instead of automatically changing the level, the player chooses the assistance.

### It preserves difficulty

The player still needs to solve the level.

The feature provides a small advantage rather than guaranteeing success.

### It creates a clear experiment

The impact can be measured against players who experience the existing retry flow.

---

# 6. Why Three Failures?

Three failures would only be the starting assumption for the experiment.

Showing assistance too early could:

- reduce the feeling of challenge,
- give away unnecessary resources,
- reduce booster demand.

Showing it too late could mean the player has already become frustrated and left.

The trigger itself could therefore become another experiment later.

For example:

```text
Variant A → Assist after 3 failures
Variant B → Assist after 5 failures
```

But the first experiment should remain simple.

---

# 7. Primary KPI

The main behavior we want to influence is whether struggling players continue playing.

Therefore, my primary KPI would be:

## Post-Failure Retry Rate

```text
Players who start another attempt after the trigger
---------------------------------------------------
Players who reach the repeated-failure trigger
```

For example:

If 10,000 players fail the same level three times and 7,000 start another attempt:

```text
Retry Rate = 7,000 / 10,000
           = 70%
```

If Retry Assist increases this from 70% to 74%, that would represent a meaningful behavioral change worth investigating further.

However, this metric cannot be evaluated alone.

---

# 8. Secondary KPIs

## Level Completion Rate

We should measure whether Retry Assist actually helps players progress.

```text
Players who successfully complete the level
--------------------------------------------
Players who attempt the level
```

---

## Completion Within Next 3 Attempts

This would be particularly useful for this experiment.

Instead of measuring overall completion, I would examine whether struggling players complete the level within their next three attempts after reaching the trigger.

This gives a more direct connection between the intervention and the outcome.

---

## Session Continuation Rate

We can measure the percentage of players who continue playing after the difficult level instead of ending their session.

For example:

```text
Players who continue to another level/activity
-----------------------------------------------
Players who reach the failure trigger
```

---

## Session Length

If players continue instead of leaving, average session length may increase.

However, this metric should not be interpreted alone.

Longer sessions could also mean that players remain stuck for longer.

---

# 9. Longer-Term Metrics

The experiment should also monitor whether the intervention creates longer-term behavioral changes.

Examples include:

### D1 Retention

Percentage of players who return the next day.

```text
Users returning on Day 1
------------------------
Users acquired/observed on Day 0
```

### D7 Retention

Percentage of players who return seven days later.

However, I would not use retention as the primary KPI for this specific experiment.

The feature directly affects retry behavior, while retention is influenced by many other systems.

---

# 10. Guardrail Metrics

Improving engagement is not enough if the feature damages another important part of the product.

Therefore, I would monitor several guardrail metrics.

## Booster Usage

Giving players assistance could change how frequently they use their existing boosters.

---

## Purchase Conversion

```text
Purchasing Players
------------------
Active Players
```

If free assistance substantially reduces purchasing behavior, the feature could increase engagement while hurting monetization.

---

## ARPDAU

**Average Revenue Per Daily Active User**

```text
Daily Revenue
-------------
Daily Active Users
```

This would help identify broader monetization effects.

---

## Attempts Per Level

If attempts per difficult level collapse dramatically, the intervention might be making levels too easy.

That would be a warning signal.

---

# 11. A/B Test Design

Eligible players would be randomly assigned to two groups.

## Control

Players experience the current game.

After three consecutive failures:

**No Retry Assist appears.**

---

## Treatment

Players experience the proposed feature.

After three consecutive failures:

**Retry Assist appears before the next attempt.**

---

### Experiment Flow

```text
Player enters difficult level
            ↓
          Fails
            ↓
          Fails
            ↓
          Fails
            ↓
      Eligibility Trigger
            ↓
      Random Assignment
        ↙         ↘
   CONTROL      TREATMENT
      ↓             ↓
Existing Flow    Retry Assist
        ↘         ↙
        Measure Results
```

---

# 12. Player Segmentation

Looking only at the overall average could hide important differences.

I would therefore analyze the results across several segments.

### Difficulty Segment

Players struggling on extremely difficult levels may react differently from players struggling on normal levels.

### Player Experience

Newer players and experienced players may value assistance differently.

### Paying vs Non-Paying Players

The feature could have different monetization effects between these groups.

### Booster Ownership

Players with many available boosters might respond differently from players with few resources.

Segmentation should primarily be used to understand the experiment after the overall result is evaluated rather than creating dozens of variants before the experiment begins.

---

# 13. Success Criteria

I would consider the experiment promising if the treatment group shows:

**Higher post-failure retry rate**

and

**Higher session continuation**

while maintaining:

**Stable monetization metrics**

and

**A reasonable level completion curve.**

The purpose is not to maximize a single KPI.

A product decision should consider the whole system.

---

# 14. Possible Outcomes

## Scenario 1 — Retry Rate ↑ / Completion ↑ / Revenue Stable

This would be a strong signal to consider launching the feature more broadly.

---

## Scenario 2 — Retry Rate ↑ / Completion ↑ / Revenue ↓ Significantly

The feature may be helping players too much.

Possible iteration:

- trigger later,
- reduce the strength of the assistance,
- limit frequency.

---

## Scenario 3 — Retry Rate ↑ / Completion Unchanged

The feature may encourage another attempt without actually helping the player overcome the difficulty.

The assistance itself might need redesign.

---

## Scenario 4 — No Meaningful Change

The hypothesis may be wrong.

Repeated failure may not be the main reason players leave.

The feature should not be launched simply because development work was already spent on it.

---

# 15. Future Iterations

If the first experiment works, several more sophisticated approaches could be explored.

## Dynamic Trigger

Instead of always triggering after three failures, assistance could depend on:

- level difficulty,
- previous player performance,
- number of remaining moves at failure,
- recent failure history.

---

## Personalized Assistance

Different player behaviors could trigger different assistance.

For example, a player repeatedly failing with only one objective remaining may need a different intervention from a player failing far from completion.

---

## Difficulty-Based Targeting

The feature could be limited to levels where data shows unusually high:

- failure rate,
- session exit rate,
- attempts per completion.

This would reduce unnecessary assistance.

---

# 16. Alternative Solutions Considered

Retry Assist is not the only possible solution.

Other approaches could include:

### Additional Moves

Easy to understand, but could directly interfere with monetization and difficulty.

### Automatic Difficulty Reduction

Could improve completion but risks making progression feel artificial.

### Tactical Hints

Could teach players without directly giving resources, but creating useful context-aware hints would be more complex.

### Free Booster

Simple and measurable, but could reduce perceived booster value if given too frequently.

For an initial experiment, I selected **Retry Assist** because it is simple to understand, easy to test, preserves player choice, and creates measurable behavioral outcomes.

---

# 17. Product Thinking Framework

The reasoning behind the case can be summarized as:

```text
PLAYER BEHAVIOR
      ↓
Repeated Level Failure
      ↓
POTENTIAL PROBLEM
      ↓
Frustration / Session Exit
      ↓
HYPOTHESIS
      ↓
Small Assistance → More Continued Play
      ↓
SOLUTION
      ↓
Retry Assist
      ↓
EXPERIMENT
      ↓
Control vs Treatment
      ↓
MEASURE
      ↓
Retry + Completion + Monetization
      ↓
DECISION
      ↓
Launch / Iterate / Kill
```

---

# 18. Key Takeaway

The objective of this proposal is not to make Toon Blast easier.

The objective is to intervene at a moment where challenge may be turning into frustration.

A successful product change would help more players remain engaged while preserving the difficulty, progression, and monetization systems that make the game sustainable.

This is ultimately a balancing problem:

**Challenge ↔ Frustration**

and the correct answer should be determined through player behavior and experimentation rather than intuition alone.

---

## Disclaimer

This is an independent product analysis created for portfolio and educational purposes.

The analysis is based on publicly observable gameplay and does not use internal Peak data.

This project is not affiliated with or endorsed by Peak.
