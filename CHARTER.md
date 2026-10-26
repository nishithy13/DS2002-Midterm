# Team charter: Hurricane Helene Analytics

## Members
- Ishan Alla (GitHub: ishanallasanagala)
- Nishith Yalamanchi (GitHub: nishithy13)
- Sid Luthra (GitHub: sidluthra1)

## Goals
- **good result:** A reproducible, well-documented ETL and analysis notebook that runs top-to-bottom via Restart and Run All and clearly answers all five business questions with defensible numbers.
- **what each person wants:** Ishan wants to build a bulletproof pandas/SQL data cleaning pipeline and SKU consolidation workflow; Nishith wants to master resilient API ingestion, timezone alignment, and meteorological joins; Sid wants to drive robust data analysis across Q1–Q5 and clear visual storytelling.
- **time limits:** Midterm exams and coursework in other UVA classes on Tuesdays/Thursdays; we will front-load data cleaning and API ingestion early each week.
- **what to avoid:** Editing the same notebook simultaneously (causing Git merge conflicts) or analyzing dirty data before logging cleaning decisions.

## Roles

| Role | Owner | Backup |
|---|---|---|
| cleaning + decision log | Ishan Alla | Sid Luthra |
| weather API + join | Nishith Yalamanchi | Ishan Alla |
| analysis Q1-Q5 | Sid Luthra | Nishith Yalamanchi |
| charts + presentation | Sid Luthra | Nishith Yalamanchi |

## Question owners

| Question | Owner | Reviewer |
|---|---|---|
| Q1 demand surge | Nishith Yalamanchi | Ishan Alla |
| Q2 SKU consolidation | Sid Luthra | Ishan Alla |
| Q3 weather correlation | Nishith Yalamanchi | Sid Luthra |
| Q4 stores and geography | Sid Luthra | Nishith Yalamanchi |
| Q5 signal or artifact | Ishan Alla | Nishith Yalamanchi |

## How we work
- **repo url:** https://github.com/nishithy13/DS2002-Midterm
- **notebook owner this week:** Ishan Alla
- **meeting time:** Zoom during class hours (Mondays and Wednesdays 9:00 AM – 10:00 AM)
- **channel:** iMessage group chat, replying within 3 hours (ASAP)
- **how we decide:** Check the raw data first; if still split, the role owner decides and records the rationale and row count in the decision log.
- **if someone goes quiet:** Check in after 24 hours; escalate to a call after 48 hours, and email the instructor if unresolved before the weekly checkpoint.
