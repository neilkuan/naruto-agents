# Skill: Weekly Summary

## Purpose
Generate a weekly rollup of team activity, progress, and priorities.

## Steps
1. Read `memory/daily/` for the past 7 days of team logs
2. Read each agent's `memory/daily/` for their recent activity
3. Read `memory/MEMORY.md` for ongoing priorities and context
4. Compile by theme (not by day):
   - **Completed** — what shipped or was delivered this week
   - **In Progress** — what's actively being worked on
   - **Blocked / Needs Attention** — risks, blockers, decisions needed
   - **Next Week** — upcoming priorities based on patterns and pending items

## Output
A concise weekly summary in markdown, organized by theme. Max 30 lines.
