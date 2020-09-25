---
layout: post
title: Default `solid_capstyle=` is problematic for short lines 
tags: [matplotlib, visualisation]
author: Ozan Öğreden
comment: false
---

Today I needed to plot "parking action timelines" for a project.
Here is a simplified version of what I wanted to get, an 8 hour parking action from exactly 10:00 to 18:00:

![](/data-til/assets/images/solid_capstyle_final.png)

But what's happening at the edges? The line doesn't seem to be exactly 8 hours.
The same happens for very short parking actions.
For instance, here is one that is as short as 15 minutes:

![](/data-til/assets/images/solid_capstyle_15min_lw6.png)

By the looks of it, you would think it's 20 minutes.
What's going on?

When I simplified my example, I noticed that changing the linewidth is changing the length of the line:

![](/data-til/assets/images/solid_capstyle_15min_lw18.png)

This is a very simple `Axes.plot()` call, so there's not much I could be doing wrong:

```
x_1 = [datetime(2020, 9, 2, 12)] * 2
x_1[1] += timedelta(minutes=15)

fig, ax = plt.subplots(figsize=(12, 2))

# ...

ax.plot(
    [x_1[0], x_1[1]],
    [0, 0],
    lw=18,
    color='k',
)

# ...
```

[It turns out](https://stackoverflow.com/a/10297860) the [default capstyle of Line2D is 'projecting'](https://matplotlib.org/gallery/lines_bars_and_markers/joinstyle.html#cap-styles). 
Here's how the matplotlib documentation demonstrates this:

![](https://matplotlib.org/_images/sphx_glr_joinstyle_002.png)

Passing the correct argument...

```
# ...

axes.plot(
    [x_1[0], x_1[1]],
    [0, 0],
    linewidth=6,
    color='k',
    solid_capstyle='butt' 
)

# ...
```

... the line is indeed 20 minutes long:

![](/data-til/assets/images/solid_capstyle_15min_lw6_fixed.png)
