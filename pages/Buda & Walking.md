# Buda & Walking

Buda is a **mirror**, not a metric.

---
## ðŸ• Walking as Health Signal

Use walking notes to sense:
- Nervous system state
- Energy levels
- Emotional tone
- Body rhythm

---
## Recent Walks

```query
{:title "Walking Patterns"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "ðŸ•")]]
 :limit 14
 :collapsed? false}
```

---
## Examples

What to notice:
- "Short walk, distracted â€” both of us restless"
- "Long slow walk â€” felt grounded after"
- "Pulled a lot today â€” I was rushed"
- "Buda sniffed everything â€” we both needed to slow down"
- "Quick pee walk â€” low energy for both"

---
## Patterns to Sense
### Buda's Behavior Reflects:
- **Pulling** â†’ You're rushed or anxious
- **Slow sniffing** â†’ Grounded, present
- **Distracted** â†’ Your mind is scattered
- **Playful** â†’ Good energy alignment
### Your Walking Pace Shows:
- **Rushed** â†’ Nervous system activated
- **Slow** â†’ More regulated
- **Inconsistent** â†’ Fragmented attention

---
## ðŸ”— Related
- [[ðŸ“– Personal]] - Personal hub
- [[Weekly Reflection]] - Pattern noticing
- [[Meditation Notes]] - Body awareness