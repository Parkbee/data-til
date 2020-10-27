---
layout: post
title: Specifying line colors in Altair using scales
tags: [altair, python, visualisation]
author: Ozan Öğreden
comment: false
---

I started data related work in R and have been missing `ggplot2` ever since I started using Python for my work.
At the beginning of the new quarter, I decided to give a new Python visualisation library a shot: Altair.

While Altair's documentation is excellent in giving a taste for the Altair idioms, I found myself using DuckDuckGo and landing on Github issues of Altair too frequently for too many things.
I figured it would be useful to have a "personal cheat sheet".

## Specifying line colors in a multi series line chart

The [multi series line chart example](https://altair-viz.github.io/gallery/multi_series_line.html) in Altair documentation is a minimal example.
It's common that we need to change the colors, this can be achieved by using a scale:

```
import altair as alt
from vega_datasets import data

source = data.stocks()

sel_ = source["symbol"].isin(["AAPL", "AMZN"])
source = source.loc[sel_]

scale_color = alt.Scale(
    domain=["AAPL", "AMZN"],
    range=["#e377c2", "#17becf"]
)

c = alt.Chart(source).mark_line().encode(
    x='date',
    y='price',
    color=alt.Color(
        'symbol',
        scale=scale_color
    ),
    # NOTE: Commented out since legend merging isn't yet fixed in Vega.
    # See https://github.com/vega/vega-lite/issues/5996 and https://github.com/altair-viz/altair/issues/275
    # A workaround is posted here: https://github.com/vega/vega-lite/issues/821
    # strokeDash='symbol',
)
```
