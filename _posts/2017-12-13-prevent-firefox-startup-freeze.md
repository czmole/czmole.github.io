---
layout: post
title: Prevent Firefox startup freeze when using multiple tabs
---

By default, when starting up Firefox it will reload all tabs inside, including pinned tabs. This is crazy sometimes if you have a lot of such tabs (I do :P mostly I use this as temporary bookmark/return to some page in a short time or for Gmail tabs)

There are these preferences for normal and pinned tabs that you can inspect and modify on the about:config page.

`
browser.sessionstore.restore_on_demand
browser.sessionstore.restore_pinned_tabs_on_demand
`

You can open the about:config page via the location/address bar.

You can accept the warning and click “I’ll be careful” to continue.

Once `browser.sessionstore.restore_pinned_tabs_on_demand` is set as true all pinned tabs won’t be loaded at browser startup but by clicking each of them. Same story for the non-pineed tabs when enabling `browser.sessionstore.restore_on_demand`

Hope it helps and saves some time! Cheers!
