{
"title": "July 2021 update: new metric \"Status\", UX improvements",
"date": "2021-07-06",
"url": "2021-07-update-new-metric-status",
"summary": "New metric \"Status\", UX improvements, code refactoring and more tests."
}

This is a July report on the progress of [Moiva.io](/).

## New metric "Status"

Users asked for an indication to identify libraries that are no longer active or have been deprecated.

I added a new metric and called it _"Status"_.

{{< figure src="/blog/images/2021-07-update/status-badge.png" alt="a screenshot of Moiva.io's table view with the new metric 'Status' highlighted" caption="The new metric 'Status'" >}}

Four possible values:

- ARCHIVED, if repository is archived
- LEGACY, if Library authors marked it so
- INACTIVE, if there were no commits in the last 6 months
- ACTIVE, otherwise

There is no API to determine if a particular library is marked legacy. Hence, such information is maintained manually.

## UX improvements

I made small UX improvements to help users get the most out of the Table view.

- metrics "_Types_", "_Tech Radar_" and "_License_" were converted into badges of different colors depending on the value
- each badge got a tooltip

  {{< figure src="/blog/images/2021-07-update/badges.png" alt="a screenshot of Moiva.io's table view showing a tooltip fot Tech Radar badge" caption="Tech Radar badge tooltip" >}}

- external links acquired a distinct icon

## Chore and misc.

- added a bunch of new libraries to the catalog.
- used json files for manually maintained data.
- added a bunch of tests for manually maintained data.
- refactored and cleaned up the code in many places.

---

Have any feedback or ideas about the project? I'm keen to know!

If you find the project interesting, stay tuned and Subscribe to Moiva's monthly newsletter.
