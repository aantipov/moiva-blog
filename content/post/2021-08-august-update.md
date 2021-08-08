{
"title": "August 2021 update: shareable and downloadable charts, new charts for metrics in the Table",
"date": "2021-08-05",
"url": "2021-08-update-share-charts-new-suggestions",
"summary": "Thanks to my vacation in July, Moiva got multiple nice features and improvements: ability to copy/share/download charts, rewritten suggestions mechanism, and many new charts."
}

This is an August report on the progress of [Moiva.io](/).

## Copy/download/share charts

This is the feature I'm mostly excited about - all charts now include a popup menu that allows users to copy charts to the clipboard, share charts on Twitter, and download charts.

{{< figure src="/blog/images/2021-08-update/chart-menu.gif" alt="a gif video of how the new charts menu works" caption="The new charts menu in action" >}}

It should make it easier for users to use the findings of comparisons elsewhere.

## A chart for every metric in the Table

A table view is useful for presenting static and numerical data. When the number of libraries in comparison is small, it serves the purpose very well. As the number of libraries increases, it becomes more difficult to make sense of the raw figures. This is where graphical data representation would be very beneficial.

Thinking that way, I added a small icon to every numeric metric in the Table. Clicking on the icon invokes a pop-up window with a bar chart where all the libraries are sorted by the metric’s value.

{{< figure src="/blog/images/2021-08-update/metric-chart.png" alt="a screenshot of Moiva.io's new feature - a chart for numeric metrics in the Table" caption="GitHub Stars chart" >}}

## New Suggestions mechanism

When a user evaluates a library, Moiva suggests alternatives to compare.

{{< figure src="/blog/images/2021-08-update/suggestions.png" alt="a screenshot of how Moiva.io's suggestions feature works" caption="Moiva's suggestions" >}}

In the past, the mechanism of suggestions used Moiva’s Catalog which categorised its libraries. The process of adding new libraries was tiresome because the mechanism had several downsides:

- every library had to belong to only one particular category. Choosing a category or creating a new one was a non-trivial task. For example, should React and Vue date-picker libraries belong to one category or different categories? Should Express and NextJS belong to the same category?
- the catalog was maintained in a [separate repository](https://github.com/aantipov/moiva-catalog), each Category had a separate file, and from time to time I had to compile it and put it to Moiva’s repo.

To facilitate adding new libraries, I refactored the Catalog:

- to use Tags instead of Categories: each library is assigned a number of tags, not a Category
- store the libraries as a plain list in a single file under the Moiva's repository
- use tags of selected libraries to suggest alternatives
- sort suggestions based on “similarity” to the selected ones. The more tags a library has in common with the tags of selected libraries, the more “similar” it is.

I the future, I plan to include GitHub Stars and Npm Downloads numbers, and libraries statuses to improve the sorting algorithm.

## Tooltips in Suggestions

Before adding suggested alternatives to comparison, it might be helpful to glance quickly at the descriptions and other details of the libraries, such as the number of Stars and Npm downloads.

On that basis, I added tooltips to the list of suggested alternatives. The tooltips contain the following information:

- name
- description
- stars and npm downloads numbers
- tags

{{< figure src="/blog/images/2021-08-update/suggestion-tooltip.png" alt="a screenshot of how Moiva.io's suggestions tooltips work" caption="Suggestions tooltip" >}}

## “About” page

Every respectable web app must have an "About" page. And so does Moiva - [https://moiva.io/about/](https://moiva.io/about/).

---

Have any feedback or ideas about the project? I'm keen to know!

If you find the project interesting, stay tuned and Subscribe to Moiva's monthly newsletter.
