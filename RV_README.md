> _Please read the original README to make better sense of what follows_

## Why the fork?

- Even though the `view` layer is free to use, Mozzila explicitly asks people to modify it for their own use.

- The existing code has logics specific to Mozzila's use case.

- For RV we want to customise the toolbar & secondary bar, only enable needed features and disabling other ones.

- This makes it future-proof in case of further customization (css, etc.) or even allowing downloads if user has RV gold.

## Why not other ready-made React Wrappers?

- Based on research current of this guide, the most popular library's [react-pdf](https://github.com/wojtekmaj/react-pdf) does not offer extensive controls, which need to be built out by ourselves.

- Critical features like pinch/pan/zoom must be added using another different libraries.

- Fully-featured ones charge fees.

- More dependencies on top of `pdf.js`, which in itself has no dependency.

- Existing users are already used to the look & feel of Mozzila's `viewer`.

## Development Setup

- Simply `npm i` and you're good to go. `gulp-cli` has been added as a devDep so no need to follow the original instruction. All other points still apply.

- If you have `vs-code`, you can just serve `web/viewer.html`using `Live Server Extension` and start coding.

## Basic Architecture

- The code is well organized & documented, so you're more than welcome to explore.

- For our usage, the key files live inside `src/web`.

- `viewer.js` is the main entrypoint It selects DOM elements and set other config before initializing `app.js`, which then initializes all the other UI & rendering components.

- There's also a shared `eventBus` in each component to help decouple them.

- UI-wise, most of the time we would want to look at `toolbar.js` & `secondary_toolbar.js`.

## What has been added

- The git commits are more informative. However, the most important changes are

  1. This is now a private package named `@crimson-education/rv-pdf-viewer` with version control.

  2. The separated gulp task named `rv` in `gulpfile.js`. This outputs a minified bundle specifically for RV frontend.

## Gotchas

- Take care not to format the html-comment directive inside `web/viewer.html` as it breaks the custom builder and may break the production bundle.

## Maintenance consideration

- Changes should ideally not alter existing logics, kind of like the `open-closed` principle. This makes it easier ti rebase with the original branch the need arises.
