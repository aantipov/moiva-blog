{
    "title": "The missing migration guide: from Vue CLI to Vite",
    "date": "2021-04-25",
    "url": "the-missing-migration-guide-from-vue-cli-to-vite",
    "summary": "Have an existing Vue 3 + Vue CLI project and wanna try the new trendy tool from [Evan](https://twitter.com/youyuxi)? Don't know where to start? This article should help."
}

## Introduction
I haven't updated Moiva.io npm dependencies for a while and I thought the time has come. 

The update didn't go well though. So I came up with a "workaroud". 

{{< tweet 1385326827120599041 >}}

In the process of integrating [Vite](https://vitejs.dev/) I found out there is no official guide how to do it. There is a [guide](https://vitejs.dev/guide/) how to bootstrap a new project with Vite, but no guidance for exising projects.

Hence I thought it is worth sharing the approach I took for the benefit of others interested in migrating their apps to Vite.

The migration process might vary depending on the tech stack of your project and the way it is built. Hence you might need to adjust the appoach to your needs.

To bring more context to the approach I took, Moiva is a single-page application and it used the following tech stack: Vue3, Vue CLI, Webpack, Babel, core-js, ESlint, Tailwind, Typescript.

Before diving into the migration steps, let's understand first what Vite is and what benefits it brings.

## What is Vite

The JavaScript landscape of build tools undergoes a significant change. We see a [rise](https://moiva.io/blog/2021-q1-report-js-build-tools-bundlers) of new tools experimenting with new approaches. Some of them quickly become very popular.

One of such tools which really stands out is [Vite](https://github.com/vitejs/vite) which got 9.4K stars in Q1 2021 (that is 68% growth). Compare that number with 1.2K stars that [Webpack](https://github.com/webpack/webpack) got in the same period.

![a screenshot of Vite monthly downloads and GitHub stars charts](/blog/images/2021-04-vue-cli-to-vite/vite-downloads.png)

Vite essentially does 2 things:
- provides a dev server with HMR (Hot Module Reloading)
- builds projects for production

## Benefits from migrating to Vite

Vite was created to achieve fast development feedback loop and it cleary succeeded in it:
- the dev server start time is uncomparably small
- code changes are reflected immediately in the browser

There are other substantial side benefits as well.
- Vite significantly simplifies development setup. You can throw away Webpack, Babel and Vue CLI with their plugins, loaders and complex configurations.
- Smaller production builds thanks to Rollup which Vite uses under the hood.

## Migration: Step 1 - Install required dependencies
## Migration: Step X - Cleanup


-----

