# Luma Team Tracker

A Claude skill that turns any public Luma calendar into a shared tracker for your team.

Conference weeks now come with a Luma calendar of 50, 100, sometimes 300 side events. This skill solves two problems that come with that.

**1. Knowing what's worth your time.** Today, figuring out which events matter means opening every one and reading its description. This skill does that reading for you. Every event lands on one page with a one-sentence summary and topic tags, and the page syncs with Luma daily, so it stays the single source of truth as new events get added.

**2. Planning coverage as a team.** Once you know which events matter, the next question is who's going to which ones. Usually that gets sorted out in a Slack thread that's out of date by Tuesday. Here, each teammate marks the events they've requested or been approved for, so everyone can see where the team will be, where two people are doubled up, and which high-priority events nobody has covered yet. That gives you something concrete to discuss when you plan your event strategy.

## What you get

Give Claude a Luma calendar link. You get back a live page with:

- **Every event on one page**, grouped by day, in the event's local time.
- **A one-sentence summary of each event**, written from its Luma description, so you know what it is without clicking through.
- **Topic tags and filters** chosen for that calendar (for a fintech conference: Payments, Institutional, Developer, Founders & Capital, and so on). Teammates can correct a tag with two clicks.
- **Team sign-ups and coverage.** Each person marks Requested or Approved (or Interested and Going for open-registration events). A "Team activity" filter shows only events someone is covering, and combining it with a topic filter shows your coverage for that topic. People are identified by their Claude login, so there's nothing to set up.
- **A daily sync from Luma.** New events appear, changed times and venues update, and events that get pulled are flagged instead of deleted so nobody loses their sign-up.

## Use it

Once the skill is installed, ask Claude something like:

> Make a team tracker for https://luma.com/your-calendar

Claude reads the calendar, writes the summaries, picks topics, publishes the tracker, and sets up the daily sync. For a calendar of a few dozen events this takes a few minutes. Then share the page with your team from its Share menu.

It works with any public Luma calendar: conference side events, a city's tech calendar, a community's event series.

## Install

**Claude apps (web, desktop, mobile):** download this repository as a zip (Code → Download ZIP) and add it as a custom skill. Anthropic's guide: [Use skills in Claude](https://support.claude.com/en/articles/12512180-use-skills-in-claude).

**Claude Code:** clone it into your skills folder.

```bash
git clone https://github.com/kalebjake/luma-team-tracker ~/.claude/skills/luma-team-tracker
```

## Requirements and limits

- **Team sign-ups** rely on Claude artifacts with shared storage. To let teammates sign up, share the page with them at Contributor access (Team or Enterprise workspaces) or invite them by email as Editors (personal accounts), and keep the public link off. If your account doesn't have shared storage, the skill builds a read-only version with the summaries and topics but no sign-ups.
- **The daily sync** is a Claude scheduled task. If your account can't create scheduled tasks, ask Claude to "sync my Luma tracker" whenever you want an update.
- **Luma data** comes from the same endpoints Luma's own website uses. They aren't a documented public API, so a change on Luma's side could break the sync until the skill is updated. If that happens, please open an issue.
- Summaries are written by Claude from each event's public description. They're a fast way to triage, not a substitute for reading the page of an event you plan to attend.

## What's in the repo

| Path | What it is |
|---|---|
| `SKILL.md` | The instructions Claude follows, step by step |
| `assets/tracker.html` | The tracker page template |
| `references/data-model.md` | How events, sign-ups and settings are stored |
| `references/topics.md` | Starting topic sets for common kinds of events |
| `references/sync-task.md` | The prompt template for the daily sync |

## Contributing

Issues and pull requests are welcome, especially new topic sets for other kinds of events, fixes when Luma changes something, and ideas from teams who use it during a real conference week.

## License

MIT. See [LICENSE](LICENSE).
