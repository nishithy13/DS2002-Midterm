# Team charter: Iceman

## Members
- Ishan Alla (GitHub: ishanallasanagala)
- Nishith Yalamanchi (GitHub: nishithy13)
- Sid Luthra (GitHub: sidluthra1)

## Goals
- **good result:** A reproducible, well-documented ETL and analysis notebook that runs top-to-bottom via Restart and Run All and clearly answers all five business questions with defensible numbers.
- **what each person wants:** Ishan wants to build a bulletproof pandas/SQL data cleaning pipeline and weather/SKU workflows; Sid wants to drive data cleaning, SKU consolidation, and analysis across Q1-Q4; Nishith wants to contribute to demand surge analysis and team coordination.
- **time limits:** Midterm exams and coursework in other UVA classes on Tuesdays/Thursdays; we front-load data cleaning and API ingestion early each week.
- **what to avoid:** Editing the same notebook simultaneously (causing Git merge conflicts) or analyzing dirty data before logging cleaning decisions.

## Roles

| Role | Owner | Backup |
|---|---|---|
| cleaning + decision log | Ishan Alla | Sid Luthra |
| weather API + join | Ishan Alla | Sid Luthra |
| analysis Q1-Q5 | Sid Luthra | Ishan Alla |
| charts + presentation | Sid Luthra | Nishith Yalamanchi |

## Question owners

| Question | Owner | Reviewer |
|---|---|---|
| Q1 demand surge | Sid Luthra, Ishan Alla, and Nishith Yalamanchi | Ishan Alla |
| Q2 SKU consolidation | Sid Luthra and Ishan Alla | Nishith Yalamanchi |
| Q3 weather correlation | Ishan Alla and Sid Luthra | Nishith Yalamanchi |
| Q4 store and geography | Sid Luthra | Ishan Alla |
| Q5 signal or artifact | Ishan Alla | Sid Luthra |

## How we work
- **repo url:** https://github.com/nishithy13/DS2002-Midterm
- **notebook owner this week:** Ishan Alla
- **meeting time:** Zoom on Mondays and Wednesdays at 9:00 AM
- **channel:** iMessage group chat, replying within 3 hours
- **how we decide:** Check the raw data first; if still split, the role owner decides and records the rationale and row count in the decision log.
- **if someone goes quiet:** Check in after 24 hours; escalate to a call after 48 hours, and email the instructor if unresolved before the weekly checkpoint.
