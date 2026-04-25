# Professional Space

Your second brain for data engineering work.

---
## ðŸŽ¯ Active Projects

```query
{:title "In Progress"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "Status:: In Progress")]]
 :collapsed? false}
```
### Project List
- Add your active projects here with `/project-note`

---
## ðŸ“Š Knowledge Areas
### Atria Database
- [[ðŸ“Š Atria Database]] - Main hub for Atria/Comtel DB
- Tables, schemas, and relationships
- Common queries and patterns
### Data Engineering
- [[ðŸ”§ Data Engineering]] - Concepts and best practices
- ETL patterns
- Data quality
- Pipeline design
### Tools & Technologies
- [[ðŸ› ï¸ Tools & Tech]] - Quick references
- SQL snippets
- Python patterns
- Command line tricks

---
## ðŸ“š Learning
- [[ðŸ“š Learning]] - Current learning goals and progress

```query
{:title "Learning Queue"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "#learning")]]
 :collapsed? false}
```

---
## ðŸ“ Recent Work

```query
{:title "Last 7 Days Work Logs"
 :query [:find (pull ?b [*])
         :where
         [?b :block/content ?c]
         [(clojure.string/includes? ?c "ðŸŽ¯ Today's Focus")]]
 :limit 7
 :collapsed? false}
```

---
## ðŸ” Quick References

Frequently accessed information:
- Common SQL patterns
- Data pipeline templates
- Troubleshooting guides