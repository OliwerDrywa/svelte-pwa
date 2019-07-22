![icon](https://github.com/cerivitos/svelte-pwa-now/blob/master/src/assets/favicon-32x32.png)
Svelte PWA Now starter
=============
A simple Svelte starter template with:

- Tailwind CSS (from [https://github.com/marcograhl/tailwindcss-svelte-starter](https://github.com/marcograhl/tailwindcss-svelte-starter))
- Rollup copy assets plugin to serve static folders (eg. data or images)
- Now integration
- PWA ready, including basic service worker and social sharing meta data boilerplate

## Getting started

Make sure [Node.js](https://nodejs.org) is installed. Clone the repo and

```bash
npm install
```

Start by

```bash
npm run dev
```

and go to [localhost:5000](http://localhost:5000).

Build for production using

```bash
npm run build
```

and serve the `dist` folder.

## Details

### Tailwind

Find out more about Tailwind CSS [here](https://tailwindcss.com). To extend Tailwind classes, go to `tailwind.config.js` and put in your customizations as an object under `extend`.

```bash
module.exports = {
  theme: {
    extend: {
      colors: {
        backgroundColor: "#f6f5f5",
        primaryColor: "#5bd1d7",
        secondaryColor: "#248ea9",
        accentColor: "#556fb5"
      }
    }
  },
  variants: {},
  plugins: []
};
```

For example, the template comes with custom colors which can then be used in html like `<div class="backgroundColor"></div>`.

Be sure to indicate `postcss` to your style tags like this

```bash
<style type="text/postcss"></style>
```

to see proper syntax highlighting and parsing in VS code.

More details can be found [here](https://tailwindcss.com/docs/configuration).

### Now integration

The template includes optional integration with the [Now hosting service](https://zeit.co/now). The easiest way to get started is to link your Github repo to Now, which allows all pushes to be built and served automatically. The included `now.json` tells Now to automatically run the rollup build command (via `package.json`) and serve the `dist` folder.

If applicable, be sure to include your custom web domain under `alias` to tell Now to automatically alias your output to your domain.

```bash
{
  "version": 2,
  "alias": "https://ADD-DOMAIN-NAME-HERE",
  "builds": [
    {
      "src": "package.json",
      "use": "@now/static-build"
    }
  ],
  "routes": [
    {
      "src": "/(.*)",
      "headers": { "cache-control": "max-age=0,must-revalidate" },
      "dest": "dist/$1"
    }
  ]
}
```

There is also a `.nowignore` file which tells Now to ignore specified files, similar to `.gitignore`.

More info on Now integration with Github can be found [here](https://zeit.co/docs/v2/integrations/now-for-github#staging-aliases-for-each-pull-request).

If you do not need Now integration, feel free to remove `now.json` and `.nowignore`.

### Rollup copy assets plugin

By default, Rollup does not copy static folders to `dist` when building. If you have folders with static assets like data files or images, put the folder path in `rollup.config.js` like so.

```bash
...
import copy from "rollup-plugin-copy-assets";

const production = !process.env.ROLLUP_WATCH;
export default {
  ...
  plugins: [
    ...
    copy({
      assets: ["src/assets", "src/MORE-STATIC-FOLDERS"]
    }),
    ...
  ]
  ...
};
```

### PWA boilerplate

#### Icons

The commonly required icons are at `src/assets`. Be sure to use the same filenames as they are referred to in the metadata at `dist/index.html`. Tip: Use [Real Favicon Generator](https://realfavicongenerator.net/) which automatically creates all the required icon sizes, and simply unzip the generated asset bundle into `src/assets`.

#### index.html metadata

The icons are all utilized in the `<meta></meta>` tags for Facebook, Twitter and Google indexing among others. Be sure to customize your app title and descriptions in all the tags.

#### Service worker

This template includes a basic service worker at `dist/service-worker.js` which simply checks against the currently held cache and loads from network if required. Feel free to further customize it for your needs.

#### Manifest

Customize `dist/manifest.json` with your PWA's info for installation. Note that the manifest requires a 512x512 icon which is not generated by [Real Favicon Generator](https://realfavicongenerator.net/). You have to manually create that one on your own using something like [https://onlinepngtools.com/resize-png](https://onlinepngtools.com/resize-png).

## License

MIT
