🌿 Sage Habit Tracker & Progression Dashboard
An advanced, automated monthly habit tracking and gamified progression system built entirely in Microsoft Excel. This workbook is designed as a self-contained productivity app, using robust spreadsheet architecture to handle dynamic streak calculations, non-scheduled rest days, and an RPG-style experience point (XP) leveling system.

🚀 Key Features
31-Day Check-in Grid: Interactive monthly tracker equipped with automated checkboxes and validation controls.
Rest-Day Tolerance (—): Built-in logic that allows users to schedule rest days (e.g., gym 3x/week) without breaking or penalizing their consecutive active streaks.
Future-Date Protection: Streal calculations are bound to the current date, ensuring future unlogged days do not reset active streaks or register as failures.
Text-Based Progress Bars: Device-independent, highly-visual progress metrics rendered directly in cells using block-text formatting (■■■■░░░░░░).
RPG-Style Leveling System: Earn 10 XP for every completed habit check-in, leveling up from a Novice Tracker to a Legendary Achiever.
Automated Badges & Achievements: Instantly unlocks credentials like the "Week on Fire" (7+ day streak) or "Mind & Body Master" based on underlying data trends.
Self-Contract Personal Incentives: Link physical rewards to spreadsheet levels, automatically changing from 🔒 LOCKED to 🔓 UNLOCKED as you progress.
📐 Workbook Architecture & Formulas
To ensure maximum performance and maintain a clean, readable layout, the workbook utilizes a three-sheet architecture:

1. Habit Tracker (The Frontend Dashboard)
This is the primary user interface containing executive KPI summary cards, the visual progress log, and the check-in calendar grid.

Overall Success Rate (Cell B6):
=IFERROR(AVERAGE(G13:G27), 0)
Target Completion Days (Column E): Dynamically sets completion targets based on the chosen habit frequency:
=IF(D13="Daily",31,IF(D13="6x/week",26,IF(D13="5x/week",22,IF(D13="4x/week",18,IF(D13="3x/week",13,IF(D13="2x/week",9,IF(D13="1x/week",4,0)))))))
Graphical Progress Bar (Column I): Compiles completion metrics into a horizontal visual gauge:
=REPT("■", ROUND(G13*10,0)) & REPT("░", 10 - ROUND(G13*10,0))
Active Streak Lookup (Column H): Queries the backend database to pull the most recent active streak value, ignoring future blank columns:
=IFERROR(LOOKUP(9.99999999999999E+307, Streak_Helper!J13:AN13), 0)
2. Streak_Helper (The Calculation Engine)
A hidden database sheet that runs sequential day-by-day calculations to track consistency trends and evaluate active streaks.

Day-by-Day Streak Accumulator (e.g., Column K): Checks if the logged date has passed today's date, increments the streak count on success (✔), preserves the streak count on a rest-day (—), and resets on a miss:
=IF('Habit Tracker'!K$12>DATE(2026,8,18), "", IF('Habit Tracker'!K13="✔", IF(ISNUMBER(J13), J13+1, 1), IF('Habit Tracker'!K13="—", IF(ISNUMBER(J13), J13, 0), 0)))
3. Milestones and Rewards (The Gamified Incentives)
Translates check-in aggregates into leveling mechanics, unlockable badges, and tangible self-incentive goals.

Current XP Level (Cell C6): Evaluates absolute experience points and returns your current status title:
=IF(C7>=1000, "Level 4: Legendary Achiever 🏆", IF(C7>=500, "Level 3: Consistency Master 🔮", IF(C7>=250, "Level 2: Habit Builder 🛡️", "Level 1: Novice Tracker ⚔️")))
Automated Badge Unlocks (Column H): Checks cross-sheet conditions to unlock major accomplishments:
# "Week on Fire" Badge (Triggered by any habit streak >= 7 days)
=IF('Habit Tracker'!F6>=7, "🏆 UNLOCKED", "🔒 LOCKED")

# "Ultimate Legend" Badge (Triggered by overall success rate >= 80% and a 14+ day streak)
=IF(AND('Habit Tracker'!B6>=0.8, 'Habit Tracker'!F6>=14), "🏆 UNLOCKED", "🔒 LOCKED")
🎨 Theme & Styling
The design uses a professional, cohesive Sage Green & Slate Gray theme tailored for personal wellness and goal tracking:

Primary Sage Header: #4E6544 (gives the sheet a calming, app-like visual structure).
Clean Gridlines: Gridlines are disabled (showGridLines = False) with structured borders and shading to maximize layout clarity.
Zebra Striping: #F3F6F2 alternated across data rows to ensure seamless scannability across the wide 31-day horizon.
📂 How to Load and Start Tracking
Download the Habit_Tracker_Dashboard-v2.xlsx file from the Studio panel.
Open the workbook in Microsoft Excel or Google Sheets.
Overwrite the sample habit names in Column B on the first sheet with your personal tracking goals.
Log your progress daily using the quick dropdown controls (✔ for completed, — for rest days, and clear/empty for missed days) and watch your XP dashboard grow!
Gemini Notebook can be inaccurate; please double check its responses.
