# ADMS Converter Agent — Demo Script

**File to open:** `Databricks_ADMS_Converter_Mockup.html`
**Runtime:** ~5–7 minutes for the full walkthrough
**Audience:** Exelon stakeholders unfamiliar with how the agents actually show up day-to-day

## Before you start

- Open the HTML file full-screen in a browser. Everything is click-driven — no real backend, so nothing can break or time out.
- A dark bar pinned to the very top ("DEMO FLOW") is presenter-only chrome, not part of the product. It shows four stages — **Sign In → Workspace Home → Agent Hub → ADMS Converter Agent** — and you can click any stage directly if you want to skip ahead or recover from a wrong click. **Reset Demo** (top right) reloads the whole thing to a clean start.
- Everything below the dark bar is what a real user would actually see in Databricks — that's the part to keep the audience's eyes on.

## The story you're telling

The agent is a normal Databricks App, sitting in the same place as every other tool the engineer already uses, opened the same way — but once you're inside it, the interaction itself feels exactly like ChatGPT or Claude: a conversation, not a form. You tell it what you need in plain language (or one click on a suggested prompt), and it works, narrates what it's doing, and hands back results in the same thread.

---

## 1. Sign In

**What's on screen:** A standard Databricks SSO login card, workspace pre-filled to `exelon.cloud.databricks.com`.

**Say:** *"This is nothing new — same login your engineers already use every day. No separate account, no new URL to bookmark."*

**Do:** Click **Continue with Exelon SSO**. It shows a brief spinner, then lands on the workspace home page.

---

## 2. Workspace Home

**What's on screen:** A normal Databricks landing page — greeting, a promo banner about the Delivery Accelerator agents, and a "recently viewed" row. Notice the **Apps** icon in the left rail is pulsing with a tooltip pointing at it.

**Say:** *"There are two ways to get to the agents from here — same as any other Databricks App. You can click this banner, or you can click Apps in the sidebar, same as you would for any workspace app."*

**Do:** Click the **Explore Agent Hub →** button on the banner (or click the pulsing Apps icon in the rail — both go to the same place; worth showing that redundancy exists).

---

## 3. Agent Hub

**What's on screen:** A grid of all 10 Delivery Accelerator agents. Three are marked **Live** (ADMS Converter Agent, Power BI Genie, DIVE); the other seven are **Coming Soon** and greyed out.

**Say:** *"This is the whole roadmap in one place — not just the ADMS Converter. Three agents are live and running against real ORA/CCB work today; the rest are scoped and queued."*

**Do:**
1. Click into the search box and type **`ADMS`** — the grid filters down live, in front of the audience. This is the "searching for the right agent" moment — make sure to actually type it rather than paste, it reads better live.
2. Point out the **Live only** filter chip as an alternate way to narrow the list.
3. Click **Open agent →** on the **ADMS Converter Agent** card.

> Optional: if someone asks about Power BI Genie or DIVE, click their cards — a toast confirms they're live agents too, just not wired into this particular walkthrough.

---

## 4. ADMS Converter Agent

This is the main event, and it's the part most worth slowing down for. The app opens as a chat — same layout language as ChatGPT or Claude: a slim conversation-history rail on the left, the message thread in the center, and a message composer at the bottom. A breadcrumb (`Workspace / Shared / Apps / ADMS Converter Agent`) still confirms it's just a normal Databricks App underneath; clicking **Apps** in that breadcrumb jumps straight back to the Hub.

**Say:** *"This isn't a form to fill out — it's a conversation. The agent tells you what it does and what it needs, right up front."*

**Do — point out the opening message:** The agent has already introduced itself before you touch anything:
- What it's built to do (migrate legacy OMS SQL into ADMS-compatible SQL, score mapping confidence, validate, generate STTM docs and PySpark ETL)
- Exactly what it needs from you: a `.sql` file, the OpCo, the consumption channel, the target environment
- A one-click **suggested prompt** to try the sample conversion immediately

**Do — run it:** Click the suggested prompt chip (*"Convert oms_outage_summary.sql · ComEd · Electric — Distribution · DEV"*). Watch what happens in order:
1. Your message appears on the right with the file attached, like sending a message in any chat app.
2. The agent replies **"On it — converting oms_outage_summary.sql:"** and a checklist appears, ticking off each step live (parse → resolve schema → translate → validate → generate docs) — this is the same "agent is working" pattern people already recognize from Claude or ChatGPT tool calls.
3. A final summary message lands with the key results in plain language, and a **results panel slides open** on the right.

**Say while it's working:** *"This checklist isn't decoration — each line is a real step: parsing the SQL, checking every column against the ADMS data dictionary, translating the logic, validating against Databricks, generating the docs. Notice step four — it caught and fixed its own error mid-run."*

**Do — walk the results panel tabs**, same rich content as before, now living alongside the conversation instead of replacing it:

| Tab | What to point out |
|---|---|
| **SQL Translation** | Side-by-side legacy vs. translated SQL. Point at the inline comments showing exactly what was renamed (`REST_TS → restore_ts`). |
| **Mapping Confidence** | Four confidence tiers — Converted, Assumed, Guessed, Unresolved. This is the trust mechanism: *"Nothing below 'Converted' ships without an engineer's eyes on it."* |
| **Validation** | The agent actually ran the SQL — 99.8% row match, one retry it caught and fixed itself. |
| **STTM Documentation** | Auto-generated mapping workbook, exportable to `.xlsx` or pushed straight into Unity Catalog comments — this is the artifact that used to take days by hand. |
| **PySpark ETL** | The actual runnable code, ready to drop into a Workflow. |
| **Agent Trace** | The full step-by-step audit trail, including the one retry — good answer if anyone asks "how do we know it's not just guessing?" |

**Do — ask a follow-up question, right in the same thread:** Type **"Why was CUST_CNT marked Assumed?"** into the composer and send it. The agent answers in place — no separate chat panel to find, because the whole screen already is the chat. Try a made-up question too, to show it never dead-ends (it gives an honest "I'd need a live workspace connection for that" answer instead of making something up).

**Say to close:** *"Everything you just saw — the login, the search, one click to run a real conversion, asking a follow-up question — is exactly how an engineer would actually work with this agent day to day. No training, no separate tool."*

---

## If something goes off-script

- Click any stage in the top **DEMO FLOW** bar to jump directly there.
- Click **Reset Demo** to reload from scratch if the conversation or search state gets into an odd spot.
- The Hub's search box and filter chips are fully live — feel free to type something else if a question comes up (e.g., type "validation" to show it matching on task description, not just agent name).
- If you close the results panel by accident, click **Results panel** in the app's header to bring it back without losing the conversation.
- The chat history items on the left (`oms_meter_read_hist.sql`, `oms_crew_dispatch.sql`) are for visual context only — clicking them shows a toast rather than switching conversations in this walkthrough.
