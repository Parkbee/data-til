---
layout: post
title: A container to save Altair charts easily
tags: [altair, visualisation]
author: Ozan Öğreden
comment: false
---

Altair and Vega-lite work perfectly well together.
They considerably reduced the time I spend from finalising an analysis and reporting the results.
However, I find setting up  `altair_saver` (and keeping the set up functioning) cumbersome.
(And once done, it just exacerbates the anxiety I feel when I think of having to recreate my working environment should my laptop be replaced.)

I made [a thing](https://github.com/oguzhanogreden/deneb) that addresses this issue.

Here's how I use it.
I create a `PLOTS_FOLDER` variable in each notebook I work.
This usually looks like:

```
from pathlib import Path

# ...

PLOTS_FOLDER = Path('/Users/oguzhan/x-analysis/Outputs/Plots')
PLOTS_FOLDER.mkdir(exist_ok=True, parents=True)
```

I point the `deneb` container to this folder:

```
cd /Users/oguzhan/x-analysis/Outputs/Plots
docker run --volume="$PWD:/watch deneb /watch"
```

Now I can just work happily and PNGs of the charts I create will accumulate in the folder:

```
# ...
# ... Then I make an Altair chart.
# ... chart = alt.Chart(...) etc

chart_path = PLOTS_FOLDER / 'descriptive_chart_name.json'
chart.save(chart_path)
```
