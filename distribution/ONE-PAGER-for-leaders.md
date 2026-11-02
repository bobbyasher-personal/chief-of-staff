# Coach for Leaders — a Chief of Staff in a Claude skill
### A one-page brief (draft — for the author to edit and share inside their own organization, in its own tools)

**The problem.** Leaders don't lose their week to one big thing. They lose it to forty small ones: status meetings with no decision, inboxes that rank by arrival instead of leverage, commitments nobody tracks, and zero protected time to think. The work that would actually move the org — strategy, decisions, unblocking teams — is what gets squeezed out.

**What this is.** A Claude skill (a plain-markdown playbook) that runs inside our enterprise Claude, on your own Calendar/Gmail/Slack, and gives you two things:
- A **2-minute morning brief** (weekdays): the single highest-leverage action for today, who's blocked on you ranked by leverage, calendar verdicts (attend / skip / delegate / async), prep cards for your top 3 meetings, and your open commitments — every item cited to its source.
- A **Monday Chief-of-Staff pass**: what closed vs. slipped last week, what % of your meeting hours were actually high-leverage, your biggest low-leverage drain (with a proposal to kill it), your fronts and the one decision each is waiting on, and prep for your 1:1 with your manager.

**What makes it different from a summary bot.** It scores everything against YOUR Top-3 priorities, it is allowed to say "no clear signal today" instead of manufacturing insights, it tracks commitments in both directions (what you owe, what's owed to you) and learns — from one-line feedback — what useful and noisy look like for you.

**Trust model (non-negotiable).** Self-only: it reads only your own data. Read-only: it drafts, it never sends, books, or declines — you take every action. Nothing reports up: no manager view, no dashboard, no aggregation. It is a coach, not a monitoring tool, and it stays useful only as long as that's true.

**Try it (10 minutes).** 1) Add the skill to your Claude (zip -> Skills, or ~/.claude/skills/ in Claude Code). 2) Run `/coach-for-leaders calibrate` and answer 7 short questions. 3) Run `/coach-for-leaders morning` tomorrow. 4) Reply with one line — useful / noisy / missed X — and watch the next brief change.

**What I need from leadership.** A pilot group of 5–8 leaders for 3 weeks, and 15 minutes in a staff meeting to demo it live on my own calendar. I'll bring before/after numbers from my own use: focus hours protected, low-leverage hours cut, decisions unblocked.
— Draft prepared by a people leader, for fellow leaders. Edit freely; the tone to aim for is this page: short, direct, decision-first.
