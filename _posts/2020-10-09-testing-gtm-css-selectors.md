---
layout: post
title: Testing GTM CSS Selectors Beforehand
tags: [CSS_Selectors, GTM]
author: Ece Degirmenci
comment: false
---
## Problem 

This one is about a misconception I had about CSS Selectors - because it seems simple at first (and it is for the simple tasks) 
but then I’d wasted a lot of time when I was trying to track buttons on pages that don’t provide any class or id information. 

A bit of background here - instead of building separate click triggers or use regular expressions to track different buttons 
(doesn’t track buttons dynamically anyways), we can use `CSS Selectors` in GTM which can be a very powerful matching option while setting up the GTM triggers. 
However it can get really cumbersome to set up. 

## Solution

Instead here is a one-line JavaScript command that would allow testing the CSS Selectors beforehand. 

Go to developer tool > console > type the command below: 

```
google_tag_manager["GTM-XXXXXX"].dataLayer.get('gtm.element')
```

This command will access to GTM account within JavaScript. Here `google_tag_manager["GTM-XXXXXX”]` 
we need to add the GTM ID for the related container. 
Then this will go to the DataLayer and look into the GTM element that should be matched up. 

Then we can try our CSS Selector with the .matches(“) option which return a bool based on the CSS Selector option we input 
where to make it more narrow we can slowly refine it to test it with adding up direct decendents. 

For the `park now` button on go.parkbee.net/start-booking/26806 we would have entered the below (which will return TRUE)

```
google_tag_manager["GTM-XXXXXX"].dataLayer.get('gtm.element').matches('div.get-access-button button')
```

## Final Thoughts

I’ve got very excited about this shortcut, I am curios to see if I can use a similar command 
(without the GTM container option) to ease selections with `Web Scraping`. 

PS: We can only use CSS selectors on actual HTML elements - we can’t do that on strings or any other options.
