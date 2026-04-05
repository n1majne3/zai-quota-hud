# Countdown Display at 100% Quota

## Problem

When the ZAI token quota reaches 100%, the statusline shows `ZAI █████ 100%` with no indication of when usage will reset. Users have no way to know how long they need to wait.

## Solution

When `pct >= 100`, append a countdown showing time remaining until the next reset.

**Before:** `ZAI █████ 100%`
**After:** `ZAI █████ 100% ⏳ 4h 32m`

## Implementation

### File: `scripts/statusline.mjs`

Modify the `formatOutput()` function:

1. Read `nextResetTime` from the `TOKENS_LIMIT` limit object (already returned by the API)
2. If `pct >= 100` and `nextResetTime` is present and in the future:
   - Compute diff: `nextResetTime - Date.now()`
   - Format as `Xh Ym` (hours + minutes), `Ym` (under 1 hour), or `Xs` (under 1 minute)
   - Append `⏳ {formatted}` before the color reset
3. If `nextResetTime` is missing or in the past, show just the percentage (no countdown)

### Format rules

- >= 1 hour: `Xh Ym` (e.g., `4h 32m`)
- >= 1 minute but < 1 hour: `Ym` (e.g., `32m`)
- < 1 minute: `Xs` (e.g., `45s`)

## Scope

- Single file change: `scripts/statusline.mjs`
- No new dependencies
- No API changes
- No cache changes (60s TTL is sufficient; the countdown will recalculate on each statusline refresh)

## Edge Cases

- `nextResetTime` field missing from API response: fall back to percentage-only display
- `nextResetTime` is in the past: fall back to percentage-only display
- Non-integer or invalid `nextResetTime` value: fall back to percentage-only display
