---
layout: post
title: Saving key strokes while writing parametrised SQL queries in Python scripts
tags: [vim, vscode, psycopg2]
author: Ozan Öğreden
comment: false
---

I have been using the `vscodevim` extension for VSCode for a while.
By now, I'm fairly comfortable with navigation and basic code authoring actions.

Today, I realised there's a sequence of key strokes that I repeat a lot, with frequent mistakes.

## Problem

Writing parameterised SQL to be passed to `psycopg2`, requires repeated use of the following syntax:

```
SELECT * 
FROM table.table AS t
WHERE t.name = %(name)s
```

In a "regular" text editor, typing `%(name)s` bit requires 11 key strokes.
The way I use my keyboard, reaching into the digit row for `%()` characters require somewhat large movements.
Those large movements displace my hands and decrease my typing accuracy.

## Solution

Here's a (probably poorly written) key mapping for `vscodevim` that surrounds the word hovered by the cursor: 

```
    ...
    "vim.normalModeKeyBindings": [
        {
            "before": ["b", "b"],
            "after": ["v", "a", "w", "S", ")", "i", "%", "<Esc>", "f", ")", "a", "s", "<Esc>"]
        }
    ],
    ...
```

There are a few potential gotchas:

- This won't work for single characters.
- I'm not sure if `bb` is the best key stroke to map this onto.
