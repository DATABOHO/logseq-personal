# Personal Space

A gentle space for noticing, remembering, and orienting.

---
## ðŸ“… Journal
- [[journals]] - All daily entries
- Recent reflections: Use query below
### Recent Journal Entries
```query
{:title "Last 7 Days"
 :query [:find (pull ?p [*])
         :where
         [?p :block/journal? true]
         [?p :block/journal-day ?d]
         [(>= ?d ?start)]]
 :inputs [:7d-before]
 :collapsed? false}
```

---
## ðŸŒ± Life Areas

Gentle tracking of what matters:
- [[Meditation Notes]] - Breath and presence (light)
- [[Buda & Walking]] - Walking as health signal
- **Connection** - Relationships and community
- **Play** - Joy and creativity
- **Growth** - Learning and evolving
- **Rest** - Sleep and restoration
### Body Awareness
- **Food** - Signals, not macros (ðŸ¥—)
- **Sleep** - Use `/sleep-reentry` after rough nights
- **Movement** - Gentle and intuitive
- **Hydration** - Simple awareness

---
## â¸ï¸ Paused Notes

Things set aside without guilt:

```query
{:title "Paused Items"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "â¸ï¸ Paused")]]
 :collapsed? false}
```

---
## ðŸ”„ Re-Entry

Returning after time away? Use the `/re-entry` template.

---
## ðŸ’­ Reflections

Deeper thoughts and patterns noticed over time.
### Weekly Pattern Noticing
- [[Weekly Reflection]] - Automatic queries for body signals and themes
- Read, don't fix
- Patterns over perfection

---
## Rules of Use

1. Today's page only
2. Bullets over prose
3. Signals over scores
4. Patterns over perfection
5. Kindness over consistency
6. If it feels heavy, stop

**This is a place to listen, not optimize.**