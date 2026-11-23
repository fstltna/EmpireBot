# EmpireBot

A bot player for Wolfpack Empire, written in Hollywood with RapaGUI.

## Files

- `EmpireBot.hws` is the main script.
- `EmpireBot.xml` is the RapaGUI interface definition. It is loaded at startup and must sit next to the script or executable.

## Requirements

- Hollywood 9 or newer
- RapaGUI 2 or newer

## Running

    Hollywood EmpireBot.hws

To compile it, use Hollywood's compile option as usual. Ship `EmpireBot.xml` alongside the executable, or link it in with `-linkfiles`.

## What a poll does

1. Connects to the server and logs in (`user`, `coun`, `pass`, `play`).
2. Runs the "Commands each poll" list from the settings. Separate commands with `;`.
3. Runs the queued commands, oldest first. A command is removed from the queue only after the server has answered it.
4. Fetches `bmap <map area>`, `dump *` and `sdump *`, then updates the Map, Ships and Sectors tabs.
5. Calls `p_BotThink()`, which can queue more commands with `p_BotDo()`.
6. Logs out (`quit`), so the bot never keeps your country busy.

## Game files (`.ebot`)

Game files are plain `key=value` text. They hold the server settings, the polling options and the command queue.

The password is stored in plain text.

## Extending the bot

Strategy goes in `p_BotThink()`. When it runs, `g.sectors` and `g.ships` contain records keyed by the column names from `dump` and `sdump`, such as `x`, `y`, `des`, `eff`, `mob`, `civ`, `mil` and `food`.
