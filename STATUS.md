# Current Status

Compact current snapshot for the main browser sweep and benchmark numbers.

Use this file for "where are we right now?".
Use `RESEARCH.md` for why the numbers changed and what was tried.
Use `corpora/STATUS.md` for the long-form corpus canaries.

## Browser Accuracy

Official browser regression sweep:

| Browser | Status |
|---|---|
| Chrome | `7680/7680` |
| Safari | `7680/7680` |
| Firefox | `7680/7680` |

Notes:
- This is the 4-font × 8-size × 8-width × 30-text browser corpus.
- The public accuracy page is effectively a regression gate now, not the main steering metric.

## Benchmark Snapshot

Latest local `bun run benchmark-check` snapshot on this machine:

### Top-level batch

| Metric | Value |
|---|---|
| `prepare()` | `17.00ms` |
| `layout()` | `0.10ms` |
| DOM batch | `4.10ms` |
| DOM interleaved | `42.15ms` |

### Long-form corpus stress

| Corpus | analyze() | measure() | prepare() | layout() | segs (analyze→prepared) | lines @ 300px |
|---|---:|---:|---:|---:|---:|---:|
| Japanese prose (story 2) | `1.90ms` | `4.30ms` | `6.30ms` | `0.02ms` | `1,773→2,667` | `193` |
| Japanese prose | `4.20ms` | `8.70ms` | `12.90ms` | `0.04ms` | `3,606→5,044` | `380` |
| Korean prose | `2.30ms` | `8.20ms` | `10.40ms` | `0.05ms` | `5,282→9,679` | `428` |
| Chinese prose | `6.40ms` | `15.50ms` | `22.20ms` | `0.06ms` | `5,433→7,949` | `626` |
| Chinese prose (story 2) | `3.90ms` | `9.00ms` | `13.40ms` | `0.04ms` | `3,271→4,745` | `375` |
| Thai prose | `8.60ms` | `6.50ms` | `15.50ms` | `0.06ms` | `10,281→10,281` | `1,024` |
| Myanmar prose | `0.60ms` | `0.90ms` | `1.50ms` | `<0.01ms` | `797→797` | `81` |
| Myanmar prose (story 2) | `0.40ms` | `0.60ms` | `1.00ms` | `<0.01ms` | `498→498` | `54` |
| Urdu prose | `2.50ms` | `3.30ms` | `5.90ms` | `0.03ms` | `6,051→6,051` | `351` |
| Khmer prose | `5.50ms` | `4.20ms` | `9.60ms` | `0.06ms` | `11,109→11,109` | `591` |
| Hindi prose | `4.10ms` | `6.70ms` | `10.80ms` | `0.06ms` | `9,958→9,958` | `653` |
| Arabic prose | `21.30ms` | `41.10ms` | `66.60ms` | `0.20ms` | `37,603→37,603` | `2,643` |

Notes:
- These are current Chrome-side numbers from `bun run benchmark-check`, not the older cross-browser raw snapshot in `pages/benchmark-results.txt`.
- `layout()` remains the resize hot path; `prepare()` is where script-specific cost still lives.
- Long-form corpus rows now split `prepare()` into analysis and measurement phases, which makes it easier to tell whether a script is expensive because of segmentation/glue work or because of raw width measurement volume.

## Pointers

- Historical cross-browser raw benchmark snapshot: `pages/benchmark-results.txt`
- Long-form corpus canary status: `corpora/STATUS.md`
- Full exploration log: `RESEARCH.md`
