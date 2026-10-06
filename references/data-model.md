# Data model

All data lives in the published artifact's shared database. Read and write it with the `ArtifactData` tool; the page reads it live.

## `events/<id>`

One document per event. Luma events use the id `luma-<slug>`; events teammates add from the page get a generated id and `source: "manual"`.

| Field | Type | Notes |
|---|---|---|
| `date` | string | `YYYY-MM-DD`, in the event's local timezone |
| `time` | string | `HH:MM`, 24-hour, in the event's local timezone |
| `title` | string | Luma name with emoji and flags removed |
| `host` | string | Host names joined with ", " and " & " before the last; "" if none |
| `location` | string | Venue or city as Luma gives it; "Online" for virtual events |
| `link` | string | `https://luma.com/<slug>` |
| `approvalRequired` | boolean | Luma requires host approval to attend |
| `note` | string, optional | "Near capacity", "Sold out" or "Waitlist"; omit when none applies |
| `summary` | string | One sentence, under 25 words, written in your own words |
| `categories` | string[] | One or two topic keys from `meta/config.topics`, most relevant first |
| `categoriesEdited` | boolean, optional | Set by the page when a teammate edits topics; the sync never changes topics on these |
| `source` | string | `"luma"` or `"manual"` |
| `gone` | boolean | `true` when a Luma event disappears from the calendar; never delete it, since teammates may have signed up |

## `signups/<eventId>__<userId>`

Written only by the page, never by Claude. `{eventId, userId, status: "requested" | "approved", updatedAt}`. `userId` is the viewer's opaque Claude id; the page resolves it to a name and avatar at render time.

## `meta/config`

`{title, subtitle, topics: [{key, label}], statusLabels: {requested, approved}, notice, lumaCalendar, calendarApiId}`. The page reads this on load, so changing a label or adding a topic here updates every open view. Up to eight topics get distinct colors.

## `meta/sync`

`{lastSyncedAt, eventCount, source, sourceLabel}`. The page shows `sourceLabel` and the last sync time under the toolbar.
