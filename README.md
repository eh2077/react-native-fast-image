# FastImage

FastImage, performant React Native image component.

[![npm](https://img.shields.io/npm/v/npm.svg)]()
[![CircleCI](https://img.shields.io/circleci/project/github/RedSparr0w/node-csgo-parser.svg)]()
[![license](https://img.shields.io/github/license/DylanVann/react-native-fast-image.svg)]()

<p align="center" >
  <img src="sample.png" title="SDWebImage logo" float=left>
  <br>
  <em>Comparing FastImage to Image in the example app.</em>
</p>

React Native's `Image` component handles image caching like browsers
for the most part.
If the server is returning proper cache control
headers for images you'll generally get the sort of built in
caching behavior you'd have in a browser.
Even so many people have noticed:

- Flickering.
- Cache misses.
- Low performance loading from cache.
- Low performance in general.

`FastImage` is an `Image` replacement that solves these issues.
`FastImage` is a wrapper around
[SDWebImage (iOS)](https://github.com/rs/SDWebImage)
and
[Glide (Android)](https://github.com/bumptech/glide).

## Features

- [x] Aggressively cache images.
- [x] Add authorization headers.
- [x] Prioritize images.

## Usage

```bash
yarn add react-native-fast-image
react-native link
```

```js

import FastImage from 'react-native-fast-image'

const YourImage = () =>
  <FastImage
    style={styles.image}
    source={{
      uri: 'https://unsplash.it/400/400?image=1',
      headers:{ Authorization: 'someAuthToken' },
      priority: FastImage.priority.normal,
    }}
    resizeMode={FastImage.resizeMode.contain}
  />
```

## Properties

`source?: object`

Source for the remote image to load.

---

`source.uri?: string`

Remote url to load the image from. e.g. `'https://facebook.github.io/react/img/logo_og.png'`.

---

`source.headers?: object`

Headers to load the image with. e.g. `{ Authorization: 'someAuthToken' }`.

---

`source.priority?: enum`

- `FastImage.priority.low` - Low Priority
- `FastImage.priority.normal` **(Default)** - Normal Priority
- `FastImage.priority.high` - High Priority

---

`resizeMode?: enum`

- `FastImage.resizeMode.contain` **(Default)** - Scale the image uniformly (maintain the image's aspect ratio) so that both dimensions (width and height) of the image will be equal to or less than the corresponding dimension of the view (minus padding).
- `FastImage.resizeMode.cover` - Scale the image uniformly (maintain the image's aspect ratio) so that both dimensions (width and height) of the image will be equal to or larger than the corresponding dimension of the view (minus padding).
- `FastImage.resizeMode.stretch` - Scale width and height independently, This may change the aspect ratio of the src.
- `FastImage.resizeMode.center` - Do not scale the image, keep centered.

---

`onLoad?: () => void`

Called on a successful image fetch.

---

`onError?: () => void`

Called on an image fetching error.