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
- Faster deployments due to decreased build time.

## Step 1 - Install required dependencies
In order to find out what dependencies need to be installed I bootstraped a new project with `npm init @vitejs/app` and followed the prompts.

Then I looked into the created `package.json` file:

```json
{
  "name": "new-vite-project",
  "version": "0.0.0",
  "scripts": {
    "dev": "vite",
    "build": "vue-tsc --noEmit && vite build",
    "serve": "vite preview"
  },
  "dependencies": {
    "vue": "^3.0.5"
  },
  "devDependencies": {
    "@vitejs/plugin-vue": "^1.2.1",
    "@vue/compiler-sfc": "^3.0.5",
    "typescript": "^4.1.3",
    "vite": "^2.1.5",
    "vue-tsc": "^0.0.24"
  }
}
```

That file tells us that besides `vite` package we need to install the following packages:
- `@vitejs/plugin-vue` to support development of VueJS based projects
- `@vue/compiler-sfc` to teach the bundler understand VueJS single file components. You don't need to install this package explicitly if you are using NPM v7 because NPM will install it automatically as a peer dependency of `@vitejs/plugin-vue`.
- `typescript` and `vue-tsc` for types checking using command line. You may skip these dependencies if you rely on types checking using IDE.

I installed the required dependencies in my project.

## Step 2 - Add Vite configuration file
I copied the generated `vite.config.ts` to my project.

```ts
import { defineConfig } from 'vite'
import vue from '@vitejs/plugin-vue'

// https://vitejs.dev/config/
export default defineConfig({
  plugins: [vue()]
})
```
The only adjustment I did here was adding the `@` alias (similar to [Webpack aliases](https://webpack.js.org/configuration/resolve/#resolvealias)).
```ts
export default defineConfig({
  resolve: { alias: { '@': '/src' } },
  plugins: [vue()],
});
```

## Step 3 - Move index.html to the root folder
Vite [treats](https://vitejs.dev/guide/#index-html-and-project-root) `index.html` as the entry point to your application and it should be put to the root folder.

Hence I moved my `index.html` from `/public` to `/` folder.

The only change to the `index.html` I made was specifying a link to the entry point of my code:
```html
  <script type="module" src="/src/main.ts"></script>
</body>
```

## Step 4 - Adjust tailwind.config.ts
Migration to Vite broke styling of my application. It worked perfectly fine in development environment, but styling was partly broken in production builds. 

I figured out soon that it was caused be the move of the `index.html` file - Tailwind stopped considering that file while collecting the used classes. Hence style definitions for classes from that file were not included in the production build. 

The problem was fixed easily by tweaking the `tailwind.config.js` file and specifying the correct path to the `index.html` file.
```js
module.exports = {
  purge: {
    content: ['./index.html', './src/**/*.vue'],
  },
  theme: {...},
  variants: {},
  plugins: [],
};

```

## Step 5 - Adjust tsconfig.ts
I looked into the generated `tsconfig.json` file

```json
{
  "compilerOptions": {
    "target": "esnext",
    "module": "esnext",
    "moduleResolution": "node",
    "strict": true,
    "jsx": "preserve",
    "sourceMap": true,
    "resolveJsonModule": true,
    "esModuleInterop": true,
    "lib": ["esnext", "dom"],
    "types": ["vite/client"]
  },
  "include": ["src/**/*.ts", "src/**/*.d.ts", "src/**/*.tsx", "src/**/*.vue"]
}
```
and adjusted my `tsconfig.json` file accordingly.

## Step 6 - Adjust npm tasks
I used generated `package.json` (from Step 1) to adjust the tasks to build, preview and start the server:
```json
"scripts": {
  "dev": "vite",
  "build": "vue-tsc --noEmit && vite build",
  "serve": "vite preview"
}
```
`"build"` task includes `vue-tsc --moEmit` command to type check the code.

I also had to adjust the `lint` task and run `eslint` directly instead of relying on Vue CLI: `"lint": "vue-cli-service lint"` became `"lint": "eslint --ext .ts,.js,.vue"`.

Having done that, I accomplished "feature parity" with the previous setup. The app can now be developed, built and deployed.

We just need not to forget to do one last thing.

## Final Step - Cleanup
We are almost there. The only thing left is to remove the dependencies which are no longer needed.

I removed Vue CLI and its plugins, and core-js. The result was impressive: `package-lock.json` file became lighter by ~35k lines.

![a screenshot from GitHub showing the amount of changes made to package-lock.file](/blog/images/2021-04-vue-cli-to-vite/lockfile.png)


## Conclusion
At first, I didn't believe in the success of the endeavour. 

Vite is still a very young project (1 year old) and to replace such a huge chunk of the development setup (Webpack and Babel with their plugins/loaders) seemed to be impossible to achieve.

Turned out the migration went very easy, almost seamless.

As a result, I got huge improvements in the development process, less dependencies to care about, decreased deployment time (from 2 min to 1 min), and slighly smaller production bundles.

Amazing work was done by [Evan You](https://twitter.com/youyuxi), the author of Vite and VueJS. I can't stop being amazed by the work that guy is doing. Always mind-blowing!

-----

