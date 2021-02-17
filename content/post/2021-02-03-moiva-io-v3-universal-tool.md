{
    "title": "Moiva.io v3: a universal tool to Evaluate, Discover and Compare software",
    "date": "2021-02-16",
    "url": "universal-tool-to-evaluate-discover-compare-software",
    "summary": "I rewrote Moiva.io from scratch and made it a universal and flexible tool to suit every software developer's taste be it a JavaScript, Python or [put your favourite language here] developer."
}

Hi, Alexey is here. I have some exciting news for you.

I rewrote [Moiva.io](https://moiva.io/) from scratch and made it a universal and flexible tool to suit every software developer's taste be it a JavaScript, Python or [put your favourite language here] developer.

This article marks a third major release of Moiva.

## What's new (in short)
- ability to search for and get data for any GitHub repository (in addition to search and comparison of Npm packages).
- possibility to bring (relatively easy) Search, Suggestion, and Comparison capabilities to other languages packages like [Maven](https://mvnrepository.com/) (Java), [PIP](https://pypi.org/) (Python), or [Packagist](https://packagist.org/) (PHP).
- last but not least, Moiva got [open-sourced](https://github.com/aantipov/moiva).

## Why did I do it
At first, I wanted to focus on JavaScript ecosystem, making npm packages first-class citizens at Moiva.io.

The goal was to provide developers with a good tool to evaluate and compare npm packages in different dimensions - Popularity, Maintenance, Security, etc.

But very soon I realized that there are many JavaScript-related projects which don't have any published npm packages.

Think of, for example, frameworks like `Meteor`. 

Moiva.io could potentially be useful for the evaluation of those projects as well thanks to GitHub charts (Contributors, Issues, Commits Frequency, etc.), but search functionality was limited to npm packages only and everything was built around the concept of npm packages.

On the other hand, if Moiva gets opened up to evaluation and comparison of any GitHub project, it will essentially convert Moiva into a universal tool and make it useful to many more developers.

So I got convinced that Moiva.io should become more Universal and Agile, I just need to come up with a good idea of how to do it and how it should work.

## AHA moment
In the beginning, the idea looked vague and blurred. I didn't have a good idea how to put together existing functionality for npm packages and the new one for GitHub repositories.

I could implement separate pages for Npm and GitHub, but that was not ideal. Both have a lot in common when comparing JavaScript projects.

Then the `AHA` moment came - everything became clear, I realized how to put together different things and since then I didn't have a chance to take a rest before implementation was finished.

Here is the essence of the idea.

### One Search for All
The same single search field can be used to search for both Npm packages and GitHub repositories. It can be easily achieved via search modifiers (prefixes).

Default search is for GitHub. 

The search prefixed with `n:` is for Npm packages.

![](/blog/images/universal-tool/search.png)

What I like about that solution is that it can be easily extended in the future to search for other things as well.

### Show only relevant charts
If a user selected only GitHub repositories without connected Npm packages, then we can just hide Npm related charts. No reason to show them.

It's similar to how Google Trends and Developer Usage charts work - they are shown only when there are data for the selected Npm packages.

At the same time, if the user selected a mix of Npm and Github projects, we will show Npm related charts for the selected Npm packages.

### Handling of Monorepo cases
If a user selected several npm packages which belong to the same repository, then we could have duplication in GitHub charts.

Moiva should be clever enough to handle such cases gracefully - do deduplication and show GitHub charts only for the first selected Npm package.

In future articles I want to cover some of the implementation details and decisions I made.

In the meantime, if you are interested, you can also check the [repository's readme](https://github.com/aantipov/moiva/) with the explanation of the Library concept I came up with while implementing the GitHub support.

### NPM data for GitHub repositories
Many Npm packages serve as main artifacts for their GitHub repository. 
Wouldn't it be great if Moiva could magically know and show Npm charts when a user selects one of such repositories?
Moiva already has [Moiva Catalog](https://github.com/aantipov/moiva-catalog)

## What's next
I clearly see a huge potential for [Moiva.io](https://moiva.io/) to become a really useful tool to many developers.

It can grow and become better in different directions.
I will mention a few most evident to me and, probably, most important:
- enable search/suggestion/comparison for more languages' package systems (Maven, PIP, etc.).
- add more useful charts and data, both generic and language/package-system specific.
- improve significantly the alternatives suggestion system. Currently, it's based on [Moiva Catalog](https://github.com/aantipov/moiva-catalog) and needs a lot of data to be put there. I see a way how the community could help and contribute there.

Stay tuned and Subscribe to the newsletter. I want to publish more interesting content about Moiva development.
