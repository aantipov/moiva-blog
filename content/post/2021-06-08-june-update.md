{
    "title": "June 2021 update: improved Table view, SEO fixes",
    "date": "2021-06-08",
    "url": "2021-06-update-improved-table-view",
    "summary": "I continued to work on improving the Table view, which I introduced a month ago. And I was refactoring Moiva while solving SEO issues."
}

This is a June report on the progress of [Moiva.io](http://moiva.io) and other things I’ve been working on.

<!-- ## Improved table view -->
<!-- About a month ago I introduced a table view for presenting data. I found out that it brings a lot of value and I gave it a central place. The Charts are mainly used to present historical data and are helpful in seeing trends. The Table is kind of snapshot of the current state that displays raw data. Hence, the Table and Charts perfectly complement each other. -->
<!--  -->
<!-- Moiva evaluates Npm packages and GitHub repositories using roughly 20 metrics. And the number keeps growing. To help users navigate through those metrics, I grouped them into three categories: "Popularity", "Maintenance" and "Miscellaneous". Each category got highlighted with a different background color. -->
<!--  -->
<!-- {{< figure src="/blog/images/2021-06-update/tabular-view-old.png" alt="a screenshot of Moiva.io's old table view with data for Webpack, Vite and Snowpack" caption="The old table view" >}} -->
<!--  -->
<!-- {{< figure src="/blog/images/2021-06-update/tabular-view.png" alt="a screenshot of Moiva.io's new table view with data for Webpack, Vite and Snowpack" caption="The updated table view" >}} -->
<!--  -->
<!-- "Stars" and "New Stars" metrics were combined into a single row. The same was done for "Downloads" and "Downloads Growth". -->
<!--  -->
<!-- I also added a new metric called "Vulnerabilities". It shows a number of vulnerabilities in the repository. Thank you to [Snyk.io](https://snyk.io/) for providing the data. -->
<!--  -->
<!-- {{< tweet 1392947957964623874 >}} -->

<!-- ## Removed "Issues" chart -->
<!-- The "Recently updated issues" chart was available on Moiva. -->
<!--  -->
<!-- {{< figure src="/blog/images/2021-06-update/issues-chart.png" alt="a screenshot of Moiva.io's Issues chart with data for Moment, DayJS and date-fns libraries" caption="Issues Chart" >}} -->
<!--  -->
<!-- My idea was to show the number of bugs reports and other types of issues being opened and closed. It should have indicated how quickly the issues are being resolved, as well as a proportion of bugs to the remainder of the issues. -->
<!--  -->
<!-- At the time I implemented the chart I was struggling to find proper data. I chose an API that provided a list of repository issues sorted by last update date. The combination of that data with the issues statuses and labels should have yielded a good approximation of how many issues are being opened/closed. -->
<!--  -->
<!-- Later on, I discovered I was wrong. I examined data from a number of well-known repositories and noticed that many old closed issues were constantly being updated, primarily due to new comments. It made the issues appear in Moiva as "recently closed", undermining the chart's main purpose. -->
<!--  -->
<!-- I decided to remove the chart and come up with more meaningful issues metrics later. -->

<!-- ## Migration to Netlify -->
<!-- Moiva was migrated from Vercel to Netlify. -->
<!--  -->
<!-- I was hoping that migration would help me fix some of Moiva's SEO issues. I found out I was too optimistic; their redirection logic constraints don't make my situation any better. -->
<!--  -->
<!-- Nevertheless, I think I've discovered a solution. Netlify is implementing a new feature called [Edge Handlers](https://docs.netlify.com/routing/edge-handlers/). It will allow intercepting and modifying requests and responses on-the-fly, which should be enough for me to implement the required redirection logic and add the necessary headers to responses. -->

## SEO fixes
Moiva is a single-page application (SPA) without server-side rendering (SSR). Because Google has historically favoured server-rendered web pages, such architecture comes with a set of SEO issues.

Moreover, Moiva had content-related SEO issues: Google considered Moiva's pages to be of low value because of their emphasis on graphical representation of data. The charts use `<canvas />` elements, which Google cannot read, and I made the mistake of not giving it a textual fallback. Charts accessibility attributes like `aria-label` were apparently of no help there.

As a result, Google flagged Moiva's pages as duplicates, and they were removed from the Index.

{{< figure src="/blog/images/2021-06-update/google-coverage.png" alt="A screenshot from Google Search Console showing the drop of Moiva.io's page coverage from 1.5k to 23 pages" caption="A screenshot from Google Search Console" >}}

I took a number of steps to resolve the problem.

- dived into SEO topic to figure out what and how I can improve.
- made sure Google understands the Table view by properly labeling the headers and providing the [`scope`](https://developer.mozilla.org/en-US/docs/Learn/HTML/Tables/Advanced#the_scope_attribute) attribute.
- all charts received fallback textual information.
- improved the page's internal structure by careful use of headers and sections.

{{% msg %}}
Along the way, I refactored the code and extended the usage of [Vue's Reactivity APIs](https://v3.vuejs.org/api/basic-reactivity.html). I love it! It greatly simplified the logic, eliminated a number of pain points, and made it possible to build more advanced functionality in the future.
{{% /msg %}}

It is still too early to say if my tweaks helped in any way in improving the SEO. Keeping my fingers crossed 🤞

## "Recommended reading" section
Moiva does its best to evaluate libraries as comprehensively as possible using many kinds of data and presenting them in charts and table. Moiva does its best to help developers make their own judgement about libraries and how they compare to each other.

That said, I see there is sometimes a need in experts' judgement or being aware about important updates regarding the status of a library. For example, when a user compares Date utility libraries would be nice to let a user know that authors of Moment.js recommend replace it with other libraries (thanks to [@muratsutunc](https://twitter.com/muratsutunc) for pointing out the problem). Another example, when a user compares UI Frameworks would be nice to provide a link to an in-depth performance comparison.

To cover that need I introduced a new section in Moiva "Recommended reading" which would suggest links to high quality blog posts and important libraries updates relevant to the currently selected libraries.

At the moment there is one link only - [JavaScript Frameworks, Performance Comparison 2020](https://javascript.plainenglish.io/javascript-frameworks-performance-comparison-2020-cd881ac21fce) by [@RyanCarniato](https://twitter.com/RyanCarniato). I will be adding more good links soon. If you have good articles in mind, let me know.


## Updated repos names
Repositories names are being changed quite often. The most frequent changes:
- moving a repository under a different organization account
- changing letters case

It causes a problem. 
Moiva uses its Catalog to categorise popular libraries, provide suggestions to users and to establish connection between repositories and npm packages.
Whenever a repository from the Catalog changes its name, Moiva becomes unable to locate it there and, as a result, can't provide suggestions and load Npm package data.
The user experience degrades. And it also might affect SEO.

Therefore it is important to maintain Catalog's repositories names up-to-date.


## Utility scripts in Deno
To update repositories names and do some other chore stuff, I usually write NodeJS scripts. One of my pain points was the lack of TypeScript support. I realized that I became a TypeScript addict and desperately need it everywhere. 

I decided to give Deno a try and it didn't dissapoint me. Out-of-the-box TypeScript support and built-in Fetch change the game.

## Kudos
Moiva doesn't have a good exposure yet, its audience is quite narrow at the moment. That makes every user and supporter especially valuable. I'm very gratefull to everyone who helps spread the word and provides valuable feedback. 

It's very important to me to know that I build something valuable.

I'd like to highlight the following nice people:
- [@magnemg](https://twitter.com/magnemg) and [@dcorbacho](https://twitter.com/dcorbacho) for the continous help with spreading the word about Moiva.
- [@muratsutunc](https://twitter.com/muratsutunc) for the feedback and pointing out the problem with legacy libraries.
- [@devtheory_](https://twitter.com/devtheory_) for publishing a youtube video with Moiva (starts at 8:35)
{{< youtube id="4AxQ8Ft7VzU?start=517s" >}}


---

Have any feedback or ideas about the project? I'm keen to know!

If you find the project interesting, stay tuned and Subscribe to Moiva's monthly newsletter.
