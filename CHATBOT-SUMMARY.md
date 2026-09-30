# Instructional Design Coach: Project Summary (v3)

## Overview
An interactive chatbot that walks training professionals through a full training design process. It works for any program area: sales, safety, compliance, technology adoption, customer service, healthcare, leadership, onboarding, operations, or a custom goal.

The flow follows **ADDIE**. It starts with a **Mager & Pipe** root-cause check, ties each design step to a **Kirkpatrick** level, and builds **UDL** and **adult learning principles** into practice design.

It runs in two modes. **AI mode** uses the Claude API to ask tailored questions and write tailored examples. **Offline mode** uses built-in content and works without internet. If AI fails, the tool switches to offline mode on its own.

---

## The Flow

| Step | What happens | ADDIE | Framework |
|---|---|---|---|
| 1. Performance Need | User describes the problem. The tool suggests a program area and shows why. When the need is unclear, it asks a plain-language follow-up question. | Analyze | |
| 2. Root Cause | Four yes/no/not sure questions on skill, resources, consequences, and clarity. The tool says whether training fits and lists non-training fixes. | Analyze | Mager & Pipe |
| 3. Your Context *(AI mode)* | Claude asks 2–3 follow-up questions about this situation, like baseline numbers or where performance breaks down. | Analyze | Performance consulting |
| 4. SMART Goal | User picks and edits a starter goal or writes their own. The tool checks for specifics, a number, and a deadline. | Analyze | Kirkpatrick L4 |
| 5. Audience Roles | User picks roles or adds their own. | Analyze | |
| 6. Learning Objectives | User writes observable objectives. The tool flags vague verbs. | Design | Kirkpatrick L3 |
| 7. Real-World Scenarios | User adds scenarios for each role or writes their own. | Design | Kirkpatrick L2, adult learning |
| 8. UDL Design | User picks options for all three UDL principles and adds access notes. | Design | UDL, Kirkpatrick L1 |
| Training Plan | Generated plan with next steps, non-training fixes, and a measure for each Kirkpatrick level. Copy or download. | Develop · Implement · Evaluate | Kirkpatrick L1–4 |

---

## How It Finds the Program Area

**AI mode:** Claude reads the description, picks an area, and explains its choice in one sentence. If Claude isn't confident, the tool asks the follow-up question.

**Offline mode:**

- Each area has a keyword list with synonyms (for example, Safety includes "driver," "truck," "forklift," "OSHA," and "near miss").
- It matches plurals and word endings ("negotiating" matches "negotiation").
- It catches typos. "Maintenence," "onbording," and "Salesforse" still match.
- It shows the words it matched, so users see why it chose an area.
- When the match is weak or tied, it asks: "What does this problem touch most?" Users pick a plain-language answer or type more detail.

---

## What AI Mode Adds

| Call | What Claude does |
|---|---|
| Classify | Picks the program area, explains why, and writes follow-up questions for this situation |
| Tailor | Writes SMART goals, roles, and objectives from the need, root-cause answers, and context answers |
| Scenarios | Writes 3 practice scenarios for each selected role |

Tailored items show a **✨ Tailored** tag. Every AI result is checked on the server and again in the browser before it appears.

---

## Built-In Checks

- **Root cause:** flags when training alone won't close the gap
- **SMART goal:** flags a missing number, a missing deadline, too few details, or leftover [placeholders]
- **Objectives:** flag vague verbs and leftover [placeholders]
- **Scenarios:** suggest ending with a question that forces a choice
- **Required picks:** every root-cause question, at least one role, objective, and scenario, and one option per UDL principle
- **Keep as written:** users can override goal and objective checks

---

## Technical Notes

- **Look:** Roboto with an Arial fallback, palette #2c722c, #0a7a8a, #b7b7b7, #f9f9f9, and an embedded office photo background.
- **Front end:** one HTML file with no outside libraries. Responsive, keyboard and screen-reader friendly, and respects reduced-motion settings.
- **AI endpoint:** one Vercel Function (`api/assist.js`) that calls the Claude API with forced tool use for structured JSON.
- **Security:** the API key stays on the server. The endpoint limits requests, blocks unknown websites, caps input size, validates output, and treats user text as data.
- **Default model:** Claude Haiku 4.5 for speed and low cost (about 1 cent per session). Switch models with one setting.
- **Testing:** browser tests cover detection for 11 sample needs, typos, the follow-up question, the offline flow, a mocked AI flow, and AI failure fallback. Server tests cover validation, errors, origins, and rate limits.
- **To add a program area:** add entries to `AREAS` and `FOLLOW_UP` in `index.html`, and to `AREAS` in `api/assist.js`.

---

## Portfolio Talking Points

- **Performance consulting first:** "The tool checks the root cause before it designs anything. If people can already do the task, it recommends non-training fixes."
- **Framework knowledge:** "It follows ADDIE, ties each design step to a Kirkpatrick level, and builds UDL into the plan."
- **Works for any program:** "It covers nine program areas and a custom path, and it asks a follow-up question when a need is unclear."
- **AI with guardrails:** "Claude tailors questions and examples, but the design structure stays fixed. If AI fails, the tool keeps working."
- **Responsible build:** "The API key stays on the server, AI output is validated, and user input can't redirect the AI."

---

## Next Steps

1. Deploy with GitHub and Vercel (see DEPLOYMENT-GUIDE.md)
2. Embed on the portfolio site and add it to a Storyline course
3. Later: add an Assessment step and a PDF export
4. Later: let Claude review a user's goal and objectives and suggest edits
