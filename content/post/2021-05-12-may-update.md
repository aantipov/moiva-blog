{
    "title": "May 2021 update: A series of JS libraries reports, migration to Vite",
    "date": "2021-05-12",
    "url": "2021-05-update",
    "summary": "In the previous month I implemented my idea of finding out what kind of information one can get out of Moiva and what kind of reports one can prepare."
}

This is a monthly update on Moiva.io development progress and other things I've been busy with.

## Several reports were published in the blog
<!-- Moiva provides a lot of historical data for different metrics. -->
<!-- As March was coming to its end, I came up with an idea - why not to use such data and prepare a report covering first quarter of 2021. -->
<!--  -->
<!-- I wanted to take a snapshot of the Q1 2021 and provide information how different project performed in that period. -->
<!-- It was also interesting to me for another reason - I considered it as a test drive of Moiva, I wanted to see what kind of valuable information I can extract and what kind of reports I can prepare. -->
<!--  -->
<!-- As a result, I published 6 reports for different categories of JavaScript libraries: -->
<!-- - [Q1 2021 State of JS Frameworks](https://moiva.io/blog/2021-q1-state-of-js-frameworks/) -->
<!-- - [Q1 2021 JavaScript State Management Libraries report](https://moiva.io/blog/2021-q1-report-state-management/) -->
<!-- - [Q1 2021 JavaScript Testing Libraries and Frameworks Report](https://moiva.io/blog/2021-q1-report-js-testing-libraries/) -->
<!-- - [Q1 2021 JavaScript Build Tools and Module Bundlers report](https://moiva.io/blog/2021-q1-report-js-build-tools-bundlers/) -->
<!-- - [Q1 2021 Static Site Generators (JAMStack) report](https://moiva.io/blog/2021-q1-report-js-jamstack/) -->
<!-- - [Q1 2021 JavaScript End-to-end Testing frameworks report](https://moiva.io/blog/2021-q1-report-end-to-end-testing-frameworks/) -->

<!-- {{< tweet 1381917386312462339 >}} -->

<!-- The result was a surpise to me. I realized how much information was hidden from the Moiva users and how much of data can be extracted and nicely presented. -->
<!-- It also taught me that being able to see graphs with historical data is nice but sometimes might not be enough. Sometimes it can be more suiteable to see raw figures reflecting the current state and compare such figures side-by-side.  -->
<!--  -->
<!-- I realized that tabular data can be a valuable complement to the charts. -->

## Migration from VueCLI to Vite guide
Having migrated Moiva from VueCLI to Vite I found out there is a lack of resources describing the process.

[Vite](https://vitejs.dev/) is a new and very trendy tool these days and such a guide could bring much value to Vue users.

Hence I wrote [my own guide](https://moiva.io/blog/the-missing-migration-guide-from-vue-cli-to-vite/).

## Moiva.io development updates
__Migration to Vite__.
Vite had been on my radar for a while, but I didn't have any concrete plans to migrate to it. It didn't look to me mature enough to replace huge chunks of development setup - Webpack, Babel, etc.

The idea of migration came out of the problem I met. I wanted to update project dependencies and run into a conflict between a set of dependencies. I have to deal with similar conflicts quite often at my daily job and didn't want it to be part of my hobby project. So I thought why not give Vite a try.

The migration process, surprisingly, was almost seamless and the result was amazing - the startup time is next to zero, updates are reflecting instantly in the browser and I ditched __a lot__ of my existing dependencies.

<!-- {{< tweet 1385326827120599041 >}} -->

__Tabular data representation__. As I described above, the published series of reports taught me two things:
- the data that Moiva has at its disposal allow exctracting much more valuable information than is currently shown.
- tabular data representation can be a great complement to graphs.

I liked a lot the table view I used in the reports and I implemented a similar one in Moiva.io and got rid of the old list view.

{{< figure src="/blog/images/2021-05-update/list-view.png" alt="a screenshot of Moiva.io's libraries list - Webpack, Vite and Snowpack." caption="The old list view" >}}

{{< figure src="/blog/images/2021-05-update/tabular-view.png" alt="a screenshot of Moiva.io's table with data for Webpack, Vite and Snowpack" caption="The new table view" >}}

Tha table view is much more in line with the goal of the project - make it easier to compare software.

## What I've been reading and watching



---

If you have any feedback or ideas about the project, I'm keen to know!

If you find the project interesting, stay tuned and Subscribe to our monthly newsletter.
