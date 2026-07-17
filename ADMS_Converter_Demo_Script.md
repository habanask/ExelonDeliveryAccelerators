# ADMS Converter Agent — Demo Script

**File to open:** `Databricks_ADMS_Converter_Mockup.html`
**Runtime:** ~5–7 minutes for the full walkthrough
**Audience:** Exelon stakeholders unfamiliar with how the agents actually show up day-to-day

## Before you start

- Open the HTML file full-screen in a browser. Everything is click-driven — no real backend, so nothing can break or time out.
- A dark bar pinned to the very top ("DEMO FLOW") is presenter-only chrome, not part of the product. It shows four stages — **Sign In → Workspace Home → Agent Hub → ADMS Converter Agent** — and you can click any stage directly if you want to skip ahead or recover from a wrong click. **Reset Demo** (top right) reloads the whole thing to a clean start.
- Everything below the dark bar is what a real user would actually see in Databricks — that's the part to keep the audience's eyes on.

## The story you're telling

Most people picture "AI agents" as a chatbot in a corner. This walkthrough shows the opposite: the agent *is* a normal Databricks App, sitting in the same place as every other tool the engineer already uses, opened the same way, with a chat assistant available only if you want to ask it something.

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

This is the main event. The app looks exactly like any other Databricks App: a left-hand input panel and a results area on the right, with a breadcrumb (`Workspace / Shared / Apps / ADMS Converter Agent`) confirming it's just an app like any other. Clicking **Apps** in that breadcrumb jumps straight back to the Hub if you need to.

**Say:** *"Everything on the left is exactly what an engineer would fill in for a real migration task."*

**Do — walk the sidebar:**
- **Source SQL:** already has `oms_outage_summary.sql` staged (18.2 KB).
- **OpCo / Consumption Channel / Target Environment:** pre-filled dropdowns (ComEd, Electric — Distribution, DEV).
- **Existing STTM (optional):** where a prior mapping doc can be reused instead of starting cold.

**Do — run it:** Click **▶ Run Conversion**. There's a ~2 second loading state (standing in for the agent actually parsing, mapping, and validating), then the results populate automatically on the first tab.

**Say while it's loading:** *"In production this is the agent parsing the SQL, checking every table and column against the ADMS data dictionary, translating the logic, and validating the result against Databricks — all before it ever puts anything in front of an engineer."*

**Walk the six result tabs, in order:**

| Tab | What to point out |
|---|---|
| **SQL Translation** | Side-by-side legacy vs. translated SQL. Point at the inline comments showing exactly what was renamed (`REST_TS → restore_ts`). |
| **Mapping Confidence** | Four confidence tiers — Converted, Assumed, Guessed, Unresolved. This is the trust mechanism: *"Nothing below 'Converted' ships without an engineer's eyes on it."* |
| **Validation** | The agent actually ran the SQL — 99.8% row match, one retry it caught and fixed itself. |
| **STTM Documentation** | Auto-generated mapping workbook, exportable to `.xlsx` or pushed straight into Unity Catalog comments — this is the artifact that used to take days by hand. |
| **PySpark ETL** | The actual runnable code, ready to drop into a Workflow. |
| **Agent Trace** | The full step-by-step audit trail, including the one retry — good answer if anyone asks "how do we know it's not just guessing?" |

**Do — show Genie:** Click the floating spark icon (bottom right). A canned Q&A is already there (*"Why was CUST_CNT marked Assumed?"*). Type a new question and hit send to show it responds live — the reply in this mockup is illustrative, but the pattern is real: the assistant is scoped to *this run*, not a generic chatbot.

**Say to close:** *"Everything you just saw — the login, the search, the click into the app — is exactly how an engineer gets here on their own, no training required."*

---

## If something goes off-script

- Click any stage in the top **DEMO FLOW** bar to jump directly there.
- Click **Reset Demo** to reload from scratch if the run/search state gets into an odd spot.
- The Hub's search box and filter chips are fully live — feel free to type something else if a question comes up (e.g., type "validation" to show it matching on task description, not just agent name).
