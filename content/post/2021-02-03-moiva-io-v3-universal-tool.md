{
    "title": "Moiva.io v3: a universal tool to Evaluate, Discover and Compare software",
    "date": "2021-02-16",
    "summary": "I rewrote Moiva.io from scratch and made it a universal and flexible tool to suit every software developer's taste be it a JavaScript, Python or [put your favourite language here] developer."
}

Hi, Alexey is here. I have some exciting news for you.

I rewrote [Moiva.io](https://moiva.io/) from scratch and made it a universal and flexible tool to suit every software developer's taste be it a JavaScript, Python or [put your favourite language here] developer.

This article marks a third major release of Moiva.

## What's new (in short)
- ability to search for and get data for any GitHub repository (in addition to search and comparison of Npm packages).
- possibility to bring (relatevily easy) Search, Suggestion and Comparison capabilities to other languages packages like [Maven](https://mvnrepository.com/) (Java), [PIP](https://pypi.org/) (Python) or [Packagist](https://packagist.org/) (PHP).
- last but not least, Moiva got [open-sourced](https://github.com/aantipov/moiva).

## Why did I do it
At first, I wanted to focus on JavaScript ecosystem, making npm packages first-class citizens at Moiva.io.

The goal was to provide developers with a good tool to evaluate and compare npm packages in different dimensions - Popularity, Maintenance, Security, etc.

But very soon I realized that there are many JavaScript or JavaScript related projects which don't have any published npm packages.

Think of, for example, frameworks like `Meteor`. 

Moiva.io could potentially be usefull for evaluation of those projects as well thanks to GitHub charts (Contributors, Issues, Commits Frequency, etc.), but search functionality was limited to npm packages only and everything was built around the concept of npm packages.

On the other hand, if Moiva gets open up to evaluation and comparison of any GitHub project, it will essentially make a universal tool and make it usefull to many more developers.

So I got convinced that Moiva.io should become more Universal and Agile, I just need to come up with a good idea how to do it and how it should work.

## AHA moment
At the beginning the idea looked vague and blurred. I didn't have a good idea how to put together existing functionality for npm packages and the new one for GitHub repositories.

I could implement separate pages for Npm and GitHub, but that was not ideal. Both have a lot in common when comparing JavaScript projects.

Then `AHA` moment came - everything became clear, I realized how to put together different things and since then I didn't have a chance to take a rest before implementation was finished.

In the future articles I want to cover some of the implementation details and decisions I made.

In the mean time, if you are interested, you can also check the [repository's readme](https://github.com/aantipov/moiva/) with the explanation of the Library concept I came up with while implementing the GitHub support.

## What's next
I clearly see a huge potential for [Moiva.io](https://moiva.io/) to become a really useful tool for many developers.

It can grow and become better in different directions.
I mention a few most evident to me and, probably, most important:
- enable search/suggestion/comparison for more languages package systems (Maven, PIP, etc.).
- add more usefull charts and data, both generic and language/package-system specific.
- improve significantly alternatives suggestion system. Currently it's based on [Moiva Catalog](https://github.com/aantipov/moiva-catalog) and needs a lot of data to be put there. I see a way how community could help and contribute there.

Stay tuned and Subsribe to the newsletter. I want to publish more interesting content about Moiva development.
