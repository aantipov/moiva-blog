{
    "title": "April 2021 update: GitHub Stars chart and Catalog page",
    "date": "2021-04-06",
    "url": "2021-04-update-github-stars-chart",
    "summary": "GitHub Stars chart, Catalog of Libraries and Tools, and more"
}

Hey folks, Alexey is here.

This is a monthly update on Moiva.io development progress.

## "New GitHub Stars monthly" chart
GitHub stars is a measure of popularity and Moiva has been showing stars counts right from the beginning. The problem though is that bare stars amount doesn't tell much about the current state of popularity.
Who knows, maybe a popular in the past project was deprecated and in that case it would be wrong to rely on that metric as a measure of popularity.

What's more important and interesting is to see how much stars a project gets right now and how that value changes with time. It would be really cool to visualize it and be able to see popularity trends and compare them between alternative projects.

Hence, meet a new chart in our Popularity category - "New GitHub Stars monthly".

![a screenshot of the new Moiva GitHub Stars chart](/blog/images/2021-04-update/github-stars.png)

In terms of implemenation it was probably the most difficult chart so far.

At first, it was not clear where to get data.

GitHub provides `stargazers` REST api which gives a list of users who starred the repository, but without dates. Turned out that the API does provide dates of stars if you provide a specific header. But then a new problem came in - the api has a 400 pages limit. It means that you can get only first 400*100=40k stars which imposed a significant problem for old good projects.

I looked around and found that GitHub GraphQL provides the required information without such limits. Half a problem solved. Another half of a problem was to come up with a plan how to load/store data and avoid a situation where Moiva reaches GitHub's rate limit. Thanks to [Cloudflare KV Data Store](https://developers.cloudflare.com/workers/learning/how-kv-works) I avoided the hassle of setting up and working with a database.

## "Catalog" page was added
When a user evaluates a library which is "known" to Moiva, then Moiva provides a list of suggestions for comparison. Besides, Moiva shows a category to which the library belongs to.

![a screenshot how suggestions work and look](/blog/images/2021-04-update/suggestions-category.png)

That information comes from Moiva's [Catalog](https://github.com/aantipov/moiva-catalog). I thought that the Catalog might be usefull to users on its own and would be nice to expose it. 

So I created a [Catalog](https://moiva.io/catalog) page which lists all the libraries grouped into categories.

![a screenshot of the new Moiva's Catalog page](/blog/images/2021-04-update/catalog.png)

## New GitHub/NPM switch control
Back in February, when I announced that it's possible to search for, evaluate and compare any GitHub projects, I made GitHub a default search.

![a screenshot of the new Moiva's Catalog page](/blog/images/2021-04-update/npm-search-hint.png)

Search for npm packages was preserved and users could activate it with a simple `:n` prefix. I added a hint above the search field to let users know about that.

![a screenshot of the new Moiva's Catalog page](/blog/images/2021-04-update/npm-search-hint-results.png)

Then I checked statistics and found that only 10% of searches are npm-searches. It was strange to me, because I believe most of Moiva users at this stage come from JavaScript ecosystem and they should be interested more in searching for NPM packages rather than GitHub repositories. Search for NPM packages has one advantage - users see NPM-related statistics like NPM Downloads and NPM releases.

It seemed that users didn't pay attention to the tiny hint and they were not aware of the possibility to search for NPM packages.

I decided to made the search type switch more prominent and "user friendly" - using a dropdown selector.

![a screenshot of the new Moiva's Catalog page](/blog/images/2021-04-update/search-type-switch.png)

First results are promising - 40-50% search requests are NPM searches.

## Accessibility for all
I believe accessibility is important, especially for projects that rely heaviliy on visual representation of data, such as charts.

Charts play crucial role in Moiva and it was important to make them accessibile. I added a special `aria-` attribute to every chart an provided and aggregated description based on the contents of the chart.

For example, for the following chart 

![a screenshot of the new Moiva's Catalog page](/blog/images/2021-04-update/accessibility-chart-example.png)

Moiva provides the following description

![a screenshot of the new Moiva's Catalog page](/blog/images/2021-04-update/accessibility-aria-data.png)


## My article featured on the main page at Hacker News
Having migrated Moiva's apis to Cloudflare Workers, I decided to share my knowledge and wrote an article [Vercel Serverless Functions vs Cloudflare Workers](https://moiva.io/blog/vercel-serverless-functions-vs-cloudflare-workers).

I was pleased to see a good reception of it at Hacker News - it got a bunch of comments and was even featured on the main page.

## Traffic
In terms of traffic, March was the most successful month so far with 4252 visitors.

![a screenshot of the new Moiva's Catalog page](/blog/images/2021-04-update/traffic.png)

## Last but not least
Worth mentioning some of many other updates and changes:
- I added Open Graph metadata to help Moiva get more traction in social media.
- I "fixed" the old issue with the confusingly small size of React. Not it includes the size of React-Dom package.
- NPM fixed the issue with one of their apis which caused problems for "NPM Releases" chart.


---

If you have any feedback or ideas about the project, I'm keen to know!

If you find the project interesting, stay tuned and Subscribe to our monthly newsletter.
