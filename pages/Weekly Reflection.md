# Weekly Reflection

A gentle space to notice patterns without fixing them.

---
## ðŸŒ¿ Signals from the Week

```query
{:title "Body & Wellness Signals"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         (or
           [(clojure.string/includes? ?c "ðŸ¥—")]
           [(clojure.string/includes? ?c "ðŸ§˜â€â™‚ï¸")]
           [(clojure.string/includes? ?c "ðŸ•")]
           [(clojure.string/includes? ?c "ðŸ›Œ")]
           [(clojure.string/includes? ?c "ðŸ’§")])]
 :collapsed? false}
```

---
## ðŸ§  Attention Themes

```query
{:title "What's Been Pulling Me"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "ðŸ§­")]]
 :collapsed? false}
```

---
## ðŸŒ¤ï¸ Body State Snapshots

```query
{:title "Energy & Mood Patterns"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "ðŸŒ¤ï¸")]]
 :collapsed? false}
```

---
## ðŸ§© Gentle Pattern Prompt
- Pattern I'm noticing:
- One small experiment (optional):

**Rules:**
- Read, don't fix
- No summaries required
- Writing is optional

---
## ðŸ§˜ Closing Frame

This system gently asks:

> "What is my body, mind, and life rhythm teaching me lately?"

Listening is already enough.