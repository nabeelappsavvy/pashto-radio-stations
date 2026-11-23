# Pashto Radio — station list

This repo holds **one file that matters: `stations.json`**. The Pashto Radio
Android app (`com.rs.pashto_radio`) downloads it at launch, so editing this
file updates every installed app — no app update needed.

Raw URL the app reads:
`https://raw.githubusercontent.com/nabeelappsavvy/pashto-radio-stations/main/stations.json`

## How to edit (GitHub web UI)

1. Open `stations.json` above → click the pencil (Edit) icon.
2. Change what you need (see format below) → **Commit changes**.
3. Apps pick up the change on next launch (they also keep a cached copy, so a
   broken edit never leaves users with an empty list — but please keep the
   JSON valid: double quotes, commas between items, no trailing comma).

## Format

`stations.json` is a list of station objects:

| Field       | Meaning |
|-------------|---------|
| `name`      | Display name in the app. |
| `streamUrl` | Direct stream URL (MP3/AAC/HLS). Must actually play — test it in a browser/VLC first. |
| `website`   | Station homepage (optional, can be `""`). |
| `logo`      | Logo image URL (optional, can be `""`). |
| `bitrate`   | Stream bitrate in kbps (number, e.g. `128`). |
| `codec`     | `MP3`, `AAC`, etc. |
| `language`  | `pashto`, `persian` or `dari`. |
| `country`   | Country the station is based in. |
| `category`  | `pashto` → shows under **Pashto Stations**; `iran` → shows under **Popular in Iran**. |
| `order`     | Display order (integer). Lower shows first. The app sorts by this. |
| `active`    | `true` = shown in the app. Set to `false` to hide a station without deleting it (e.g. its stream died). |

## Rules of thumb

- **Dead stream?** Set `"active": false` first; delete the entry later once sure.
- **New station?** Copy an existing block, change the fields, give it the next
  `order` number in its category.
- A background checker re-tests every `streamUrl` regularly and flags dead
  ones, so the list stays clean.

## Planned flow

Longer term this file is generated, not hand-edited: **Airtable** (editing
surface) → sync + link checker → this `stations.json` → the app. The schema
above (especially `order` and `active`) is designed for that sync.
