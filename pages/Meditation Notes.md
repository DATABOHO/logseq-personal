# Meditation Notes

Very light tracking - presence over consistency.

---
## ðŸ§˜â€â™‚ï¸ Principles
- One line is enough
- Skipped days are neutral
- Presence > consistency
- Signals over scores

---
## Recent Practice

```query
{:title "Recent Meditation Notes"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "ðŸ§˜â€â™‚ï¸")]]
 :limit 14
 :collapsed? false}
```

---
## Examples

Good entries:
- "3 breaths before coffee â€” settled"
- "Restless sit, noticed impatience"
- "5 min body scan â€” tension in shoulders"

Not needed:
- Streak counting
- Time optimization
- Performance metrics

---
## ðŸ”— Related
- [[ðŸ“– Personal]] - Personal hub
- [[Weekly Reflection]] - Pattern noticing