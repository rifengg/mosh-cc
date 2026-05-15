# Patches

All patches are cherry-picked from existing upstream PRs against
[mobile-shell/mosh](https://github.com/mobile-shell/mosh). Nothing here is original
work — credit belongs to the upstream authors.

**Base:** upstream `master` at commit `decd9b7` (post-1.4.0)

**Scope rule:** Terminal-emulation and build-correctness patches only. Each must be
backed by an upstream PR. No changes to networking, auth, crypto, or the State
Synchronization Protocol.

## Included

| PR | Author | Category | Summary | Drop when |
|----|--------|----------|---------|-----------|
| [#1380](https://github.com/mobile-shell/mosh/pull/1380) | @antonme | terminal | SGR 2 (faint) + SGR 9 (strikethrough) support | Merged upstream and released |
| [#1382](https://github.com/mobile-shell/mosh/pull/1382) | @vapier | build | `config.h` include in `select.h` | Merged upstream and released |

## Excluded

| PR | Reason |
|----|--------|
| [#1297](https://github.com/mobile-shell/mosh/pull/1297) | SSH agent forwarding. Large (1,300+ lines), security-sensitive, outside terminal-emulation scope. |

## Candidates (not yet included)

These may be added in a future release after testing:

| PR | Author | Summary |
|----|--------|---------|
| [#1355](https://github.com/mobile-shell/mosh/pull/1355) | @dabeibao | Cursor shape support (`ESC[N q`) |
| [#1383](https://github.com/mobile-shell/mosh/pull/1383) | @zedinosaur | OSC 7 current working directory |
| [#1384](https://github.com/mobile-shell/mosh/pull/1384) | @zedinosaur | CSI XDA terminal feature detection |

## Rebase policy

We track upstream `master`. When upstream merges a patch we carry, we drop it from
our stack on the next rebase. The goal is to shrink this list over time, not grow it.
