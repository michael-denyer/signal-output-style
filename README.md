# Signal

A custom [output style](https://code.claude.com/docs/en/output-styles) for Claude Code. It makes Claude answer first, keep replies proportional to the question, and attach a unit, a source and a measured/estimated label to every number it reports.

It keeps Claude Code's built-in software engineering instructions (`keep-coding-instructions: true`), so it changes how Claude talks, not how it codes.

## Install

User level, available in every project:

```bash
curl -fsSL https://raw.githubusercontent.com/michael-denyer/signal-output-style/main/signal.md -o ~/.claude/output-styles/signal.md
```

Project level, checked in alongside the code:

```bash
curl -fsSL https://raw.githubusercontent.com/michael-denyer/signal-output-style/main/signal.md -o .claude/output-styles/signal.md
```

Create the directory first if it does not exist (`mkdir -p ~/.claude/output-styles`).

## Activate

In the terminal, run `/config` and pick **Signal** under **Output style**. Claude Code writes the choice to `.claude/settings.local.json`.

Anywhere else, including the desktop app, set the field yourself in a settings file:

```json
{
  "outputStyle": "Signal"
}
```

The output style is part of the system prompt, which Claude Code reads once at session start. Run `/clear` or start a new session for the change to take effect.

The standalone `/output-style` command was removed in Claude Code v2.1.91. Use `/config` or the setting above.

## What it enforces

**Answer first.** The result, diagnosis or recommendation goes in line one. A single word or a single command can be the whole reply.

**Length tracks the question.** One fact gets one line. A design or risk question gets a recommendation plus its support. When the call is close, Claude takes the shorter form.

**Numbers carry their provenance.** "28% slower, 2.12 vs 2.95 tok/s" instead of "much slower", with the source, the as-of time or SHA, and the command that regenerates it.

**No claim of done without a check.** Every claim is labelled verified, assumed or unknown, and a verified one names the check that ran. Failed and skipped checks get reported rather than smoothed over.

**Scannable points.** Points are separated by a blank line, not packed into a tight list that the terminal renderer collapses. A point that helps the reader decide what to skip opens with `▸ **Fix:**`, `▸ **Why:**`, `▸ **Recommendation:**` or `▸ **Next:**`.

**No performance.** Three kinds of phrasing are out, each shown by example rather than an exhaustive list: candor markers ("honestly", "to be clear"), integrity labels on Claude's own work ("rigorous", "I won't fabricate") and praise of your observation ("good catch"). Announcing that you are being truthful undermines the thing you are announcing.

**Hand-offs are paste-ready.** Anything left for you to run arrives as a command block with the real paths and names filled in. Two or more commands come as one script to paste once, without `set -e`, so a failure leaves your terminal open with its output.

## Make it yours

The file is one page of Markdown with no build step. Edit `signal.md` and reload the session.

The parts most worth tuning for your own work are the examples of performance in `## Cut`, which are personal, and the `▸` tag set in `## Format`. Keep the guard that comes with the tags: a tag on every point marks nothing, so tag only where the reader is choosing what to skip.

## Licence

MIT. See [LICENSE](LICENSE).
