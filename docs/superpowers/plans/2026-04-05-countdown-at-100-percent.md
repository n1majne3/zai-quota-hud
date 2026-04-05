# Countdown at 100% Quota Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use superpowers:subagent-driven-development (recommended) or superpowers:executing-plans to implement this plan task-by-task. Steps use checkbox (`- [ ]`) syntax for tracking.

**Goal:** Show a time-until-reset countdown in the statusline when token quota reaches 100%.

**Architecture:** Add a `formatCountdown()` helper that formats `nextResetTime` into a human-readable string like `4h 32m`. Modify `formatOutput()` to append the countdown when `pct >= 100` and a valid future `nextResetTime` exists.

**Tech Stack:** Node.js (ESM), no new dependencies.

---

### Task 1: Add formatCountdown helper

**Files:**
- Modify: `scripts/statusline.mjs` (insert after `bar()` function, line 26)

- [ ] **Step 1: Add the formatCountdown function**

Insert after line 26 (closing brace of `bar()` function):

```javascript
function formatCountdown(nextResetTime) {
  const ms = new Date(nextResetTime).getTime() - Date.now();
  if (ms <= 0) return null;
  const totalMin = Math.floor(ms / 60_000);
  const h = Math.floor(totalMin / 60);
  const m = totalMin % 60;
  const s = Math.floor((ms % 60_000) / 1000);
  if (h > 0) return `${h}h ${m}m`;
  if (m > 0) return `${m}m`;
  return `${s}s`;
}
```

- [ ] **Step 2: Commit**

```bash
git add scripts/statusline.mjs
git commit -m "feat: add formatCountdown helper"
```

---

### Task 2: Update formatOutput to show countdown at 100%

**Files:**
- Modify: `scripts/statusline.mjs:99-104` (the `formatOutput` function)

- [ ] **Step 1: Replace formatOutput with countdown logic**

Replace the existing `formatOutput` function (lines 99-104) with:

```javascript
function formatOutput(data) {
  const tokensLimit = (data.limits || []).find((l) => l.type === 'TOKENS_LIMIT');
  if (!tokensLimit) return `${DIM}ZAI: no data${RESET}`;
  const pct = tokensLimit.percentage || 0;
  let suffix = '';
  if (pct >= 100 && tokensLimit.nextResetTime) {
    const cd = formatCountdown(tokensLimit.nextResetTime);
    if (cd) suffix = ` ⏳ ${cd}`;
  }
  return `${colorForPercent(pct)}ZAI ${bar(pct, 5)} ${pct}%${suffix}${RESET}`;
}
```

- [ ] **Step 2: Commit**

```bash
git add scripts/statusline.mjs
git commit -m "feat: show reset countdown when quota is at 100%"
```
