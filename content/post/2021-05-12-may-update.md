{
    "title": "May 2021 update: A series of JS libraries reports, migration to Vite",
    "date": "2021-05-12",
    "url": "2021-05-update",
    "summary": "In the previous month I implemented my idea of finding out what kind of information one can get out of Moiva and what kind of reports one can prepare."
}

This is a monthly update on Moiva.io's development progress and other things I've been busy with.

## Q1 2021 reports were published
Moiva provides a lot of historical data for different metrics.
While April was nearing, I came up with an idea - why not aggregate such data and prepare a report revealing the performance of different libraries and frameworks in Q1 2021.

The idea was interesting to me also for another reason - I considered it as a test drive for Moiva, I wanted to see what kind of valuable information can be extracted from Moiva.io and what kind of reports one can prepare.

As an outcome, I published 6 reports for different categories of JavaScript libraries:
- [Q1 2021 State of JS Frameworks](https://moiva.io/blog/2021-q1-state-of-js-frameworks/)
- [Q1 2021 JavaScript State Management Libraries report](https://moiva.io/blog/2021-q1-report-state-management/)
- [Q1 2021 JavaScript Testing Libraries and Frameworks Report](https://moiva.io/blog/2021-q1-report-js-testing-libraries/)
- [Q1 2021 JavaScript Build Tools and Module Bundlers report](https://moiva.io/blog/2021-q1-report-js-build-tools-bundlers/)
- [Q1 2021 Static Site Generators (JAMStack) report](https://moiva.io/blog/2021-q1-report-js-jamstack/)
- [Q1 2021 JavaScript End-to-end Testing frameworks report](https://moiva.io/blog/2021-q1-report-end-to-end-testing-frameworks/)

{{< tweet 1381917386312462339 >}}

The result surpised me. I realized how much information was hidden from Moiva's users and how much data can be extracted and nicely presented.
It also taught me that being able to see graphs with historical data is nice but might not be enough. Sometimes it can be more suiteable to see raw figures reflecting the current state and compare such figures side-by-side. 

I realized that tabular data can be a valuable complement to the charts.

## A guide to migrating from VueCLI to Vite
Having migrated Moiva from VueCLI to Vite I found out there is a lack of articles describing the process.

[Vite](https://vitejs.dev/) is a new and very trendy tool these days and such a guide could bring much value to Vue users I thought.

Hence I wrote [my own guide](https://moiva.io/blog/the-missing-migration-guide-from-vue-cli-to-vite/).

## Moiva.io updates
__Migration to Vite__.
Vite had been on my radar for a while, but I didn't have any concrete plans to migrate to it. It didn't look mature enough to replace huge chunks of development setup - Webpack, Babel, etc.

The idea of migration came out of the problem I met. I wanted to update project dependencies and run into a conflict between a set of dependencies. I have to deal with similar conflicts quite often at my daily job and didn't want it to be part of my hobby project. So I thought why not give Vite a try.

The migration process, surprisingly, was almost seamless and the result was amazing - the startup time is next to zero, updates are reflecting instantly in the browser and I ditched __a lot__ of my existing dependencies.

<!-- {{< tweet 1385326827120599041 >}} -->

__Tabular data representation__. As I described above, the published series of reports taught me two things:
- the data that Moiva has at its disposal allow extracting much more valuable information than is currently shown.
- tabular data representation can be a great complement to graphs.

I liked a lot the table view I used in the reports, so I implemented a similar view in Moiva.io and it replaced the old list view.

{{< figure src="/blog/images/2021-05-update/list-view.png" alt="a screenshot of Moiva.io's old list view with data for Webpack, Vite and Snowpack." caption="The old list view" >}}

{{< figure src="/blog/images/2021-05-update/tabular-view.png" alt="a screenshot of Moiva.io's new table view with data for Webpack, Vite and Snowpack" caption="The new table view" >}}

The table view is much more in line with the goal of the project - make it easier to compare software.

## SEO
It was a disastrous month for Moiva in terms of Google Search performance. The coverage dropped from 1.5K to 50 pages. 

{{< figure src="/blog/images/2021-05-update/google-coverage.png" alt="A screenshot from Google Search Console showing the drop of Moiva.io's page coverage from 1.5k to 50 pages" caption="A screenshot from Google Search Console" >}}
As a result, Google doesn't suggest Moiva.io in search results when people look for a software comparison.

Google seems introduced some changes in their engine and started to treat most of Moiva's pages as duplicates. I think the reason for that is that up until now Moiva's focus was on graphical representation of data, not textual. Google apparently is not good at parsing the graphical data, even though all the charts are accompanied with the accessibility information. As a result, all the pages seem the same to Google.

I hope that introduction of the table view will help here.

Another thing that could potentially contribute to the problem is that in the beginning of the year I changed the structure of the urls: `compare` parameter was replaced by a combination of `npm` and `github` parameters. In order for Google to not treat new and old urls as duplicates, I could do 2 things:
- implement 301 redirect
- provide [`rel="canonical" link tag`](https://developers.google.com/search/docs/advanced/crawling/consolidate-duplicate-urls#rel-canonical-link-method) for the pages with old urls

The first option was not practically possible because Vercel doesn't provide an option to use url's query parameters in their [redirect logic](https://vercel.com/docs/configuration#project/redirects). So I went for the second option - during the page load Moiva calculates the canonical url and adds the required link tag. But Google seems is not good yet at parsing that canonical link tag if it is added by javascript.

I have an idea of migrating from [Vercel](http://vercel.com/) to [Netlify](https://www.netlify.com/) to overcome that problem using 301 redirects and solve some other limitations of Vercel. It seems to me that Netlify is a more mature solution in many aspects.

---

If you have any feedback or ideas about the project, I'm keen to know!

If you find the project interesting, stay tuned and Subscribe to our monthly newsletter.
