# 03 · Six review rounds — the grower's asks, as asked

This is the part the workshop is about: a working screen, a real user, and
short asks that each turned into a feature the same hour. Spelling kept.

## Round 1

> when you click to edit a pest it opens at the top of the page but it doesnt
> look like that happened when you are scrolled down … it's also hard to test
> this since all the thresholds have passed can we go back to the degreedays
> in spring maybe so i can see how the now would look when there are pests
> active, also can we put a calender and a graph of the degree days

Built: the editor opens in place of the row; a **View as of** date on every
tab; a 📈 Season tab with the cumulative chart and a month calendar.
Found on the way: with the rewind, every real day after the as-of date
counted as "forecast" and May still looked like September — the engine now
ignores anything more than 14 days past "today" (a real forecast never
reaches further).

## Round 2

> if you have multiple locations can we have an option to view both in the
> graph and add a snapshot option for the graph and calender

> are the calender exports already in or do we still need to add those, also
> can we have an option to group the pests into categories and then have the
> option to turn on or off those pests by location say if one location
> doesnt grow any evergreens they wouldnt need to see any of the evergreen
> pest group

Built: all-locations overlay (six validated colours, fixed per location),
📷 PNG snapshots, 📆 .ics for the month, and **host categories** seeded from
the guide's host column (the guide's own grouping is taxonomic — mites,
scales — which does not answer "no evergreens here") with per-location
switches.

## Round 3

> can we make the pest categories editable? in case people want to add
> different categories and edit which pests including ones they add … and
> can we get a calendar export for individual events not just the whole month

Built: a category manager (add, rename, delete, tick pests in), also placed on
Setup at the next ask; per-event .ics from a calendar chip or a Now row.

## Round 4

> can we also have a feature to zoom in on the degree day graph, look at a
> smaller time frame and also optionally show the degree day line from the
> previous year

Built: zoom presets and drag, y-axis from the window's low; last year from the
Open-Meteo archive, shifted a year to line up.

## Round 5

> do we still need some excel exports and backup features and features
> needed to be able to easily share with a colleague, remember we want to
> protect the api token for licor and can we expand the forecast check tool,
> i'd like to have more data and even an excel export to show the difference
> between the multiple weather source datas high and lows across a larger
> span of time

Built: see 04. The token rule is a design, not a filter: the token is not an
input to any builder, and a browser probe plants one and checks the outputs.

## Round 6

> it doesnt seem to be allowing me to compare the newa station … could we
> make it so you can compare multiple newa stations so that you can find the
> one that is the best match for your location, maybe this forecast check
> should be in the setup section

Checked first (it did compare, in a fresh browser — hers was a stale cache;
the check now says so). Built: **Compare these stations** — the nearest NEWA
stations over 30/60/90 days, each against Open-Meteo and the attached station,
with a Use button. The forecast check moved to Setup, beside the sources.
