# Samsara Take-home assessment

## Overview

I wanted to use the VueJS framework, which I currently use at North Face, and continuing to learn, so I set up a [vue cli hello world boiler plate](https://cli.vuejs.org/guide/creating-a-project.html#vue-create)
using [npm](https://www.npmjs.com/) locally on my computer, ingesting the `data.json` file and figured out how to ingest the data into the `App`, then followed the [documentation](https://cli.vuejs.org/guide/deployment.html) on how to make it work with Github Pages while also running into some issues displaying. Please let me know if this does not load.

## Understanding the design

After opening the file in Figma locally, I interpreted the design to be a `features list`, with rotating images, and a `modal` to display the additional lorem ipsum text expanding on the features. The rotating images was signled by the UI element underneath each feature title. The modal was determined by the close icon, additional data and icon sitting in the upper right hand corner on top of each feature image.

## Components & Data

There are 5 components total. Each component is used to render the specific element using standard vue single file template component structure. Data is served from a data directory through a [data.json](https://github.com/cweachock/samsara-takehome/blob/master/src/data/data.json) file. This way data is kept separate from the component, and could be potentially used to serve dynamic data down the road. This is then loaded through the `App` and passed as values in each component reference.

- [Button.vue](https://github.com/cweachock/samsara-takehome/blob/master/src/components/Button.vue)
- [Logo.vue](https://github.com/cweachock/samsara-takehome/blob/master/src/components/Logo.vue)
- [Media.vue](https://github.com/cweachock/samsara-takehome/blob/master/src/components/Media.vue)
- [Modal.vue](https://github.com/cweachock/samsara-takehome/blob/master/src/components/Modal.vue)
- [TextBlock.vue](https://github.com/cweachock/samsara-takehome/blob/master/src/components/textBlock.vue)

## Future state and improvements

Overall, I liked working on this! It was fun to open a figma prototype (normally I use Invision at North Face) and poke around since I am familiar with it. But there were a couple improvements and adjustments I would like to make. Below are a few listed. For example

- Getting the mixins to work properly with `SASS`, the version I was using was not playing nicely for some reason with newer versions of sass, would need to investigate!
- Refactor the `setInterval` or the rotating images and content to use a library or `requestAnimationFrame` to properly set it up.
- Finish working on the design and get feedback
- Add global `CSS` includes and imports to be on app level
- Update the `Media` component to be responsive (ie `srcset` `sizes` see about [responsive images](https://developer.mozilla.org/en-US/docs/Learn/HTML/Multimedia_and_embedding/Responsive_images) from MDN]
- Build out more `SASS` styles or mixins

## Closing

Overall, I hope you enjoyed my submission and I look forward to hearing everyones feedback :)

## Project setup

```
npm install
```

### Compiles and hot-reloads for development

```
npm run serve
```

### Compiles and minifies for production

```
npm run build
```

### Run your tests

```
npm run test
```

### Lints and fixes files

```
npm run lint
```

### Customize configuration

See [Configuration Reference](https://cli.vuejs.org/config/).
