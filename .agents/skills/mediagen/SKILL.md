---
name: mediagen
description: How to drive `mediagen`, a non-interactive CLI that generates and edits images and generates short videos, writing every result to a local file and printing its path. Covers what it can and cannot do, one-time setup, four commands worth copying, and the rules that keep a paid request from being wasted.
---

# mediagen

Images and video from a command line: every result is written to a local file and the path
is printed. Each successful call is a paid vendor request — and for video the money is
spent when the task is created, minutes before the clip exists.

Flags, models, sizes, exit codes and more examples live in the CLI itself:

```bash
mediagen --help
mediagen image generate --help
mediagen video generate --help
```

## What it does

- `image generate "<prompt>"` — a new image from a description.
- `image edit "<prompt>" --image ./photo.jpg` — a change to an existing image: restyle,
  recolour, add or remove something, render text (CJK or Latin) into it, upscale (the same
  `--image` with a larger `--size`), or combine several references (repeat `--image`, and
  say which image is which in the prompt).
- `video generate "<prompt>"` — a short clip from text, or from one first frame.
- `video status <task-id>` — collect a clip whose run was interrupted. Reads only; it
  cannot spend money.

## What it cannot do

Audio, documents, long-form video, editing or joining existing clips, describing or
analysing an image (it writes images, it cannot see them), and local pixel work — crop,
resize, convert, compress. Those belong to other tools.

## If the project already generates media

Another CLI, a hosted service, a script in the repo, a provider the user already pays for:
use that one. `mediagen` is one option among several, so reach for it when it is what the
project has, or when the user asks for it by name.

## Setup, once

This skill carries no binary: `mediagen` must already be on `PATH`, and the pi package that
delivered this skill does not put it there. If `command -v mediagen` prints nothing:

```bash
npm install -g @yandy0725/mediagen-cli
```

Then one pass per machine:

```bash
mediagen config show                          # any command writes and validates config.toml on first use
mediagen login --api-key sk-...               # the key for the default provider; --provider <name> for another
mediagen auth status                          # which key each provider would use, masked
```

Providers, their protocols and their models live in `config.toml`; `mediagen config add`
creates an entry without hand-editing, and `mediagen config show` prints what resolves.
The README covers the file's shape.

## Four commands worth copying

```bash
# a new image; files land in --out-dir (default: config output_dir, else the cwd)
mediagen image generate "a red fox in fresh snow, soft morning light" --out-dir ./out

# change a local image (local paths are read and sent as data URLs)
mediagen image edit "make the sky sunset orange, keep the composition" --image ./photo.jpg

# a video task without waiting for the render (the id comes back immediately)
mediagen video generate "a fox running through deep snow, golden hour" --no-wait --json

# collect a task you already paid for; nothing is created and nothing is billed
mediagen video status cgt-20261028-abcd --json
```

These go to whichever entry `config.toml` marks as its default. `--provider <name>` picks a
different entry from that file; the names in the CLI's own examples are only what the first
run seeds, and `mediagen config show` prints the ones this machine has.

Add `--json` whenever you intend to parse the result: without it stdout is one absolute
path per line and warnings go to stderr. Keep `--n` at 1 while iterating on a prompt: on
some dialects each image is a separate paid request (`image generate --help` says which).

## Rules

1. Report the saved path(s) exactly as printed. That is the deliverable; a generation the
   user cannot find was wasted money.
2. Never re-run a request that already produced files, and never re-submit a video task
   whose id you have: `video status <id>` collects it without paying again. Retry only a
   clean failure that produced no task at all.
3. Never print an API key. The CLI only ever prints it masked.
4. When your own command timeout is short, prefer `video generate --no-wait --json`: a
   blocking generate that you kill mid-poll leaves a paid task behind.
