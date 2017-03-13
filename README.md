[![Build Status](https://travis-ci.org/MartinDawson/react-jPlayer.svg?branch=master)](https://travis-ci.org/MartinDawson/react-jPlayer)
[![Coverage Status](https://coveralls.io/repos/github/MartinDawson/react-jPlayer/badge.svg?branch=master)](https://coveralls.io/github/MartinDawson/react-jPlayer?branch=master)
[![dependencies Status](https://david-dm.org/martindawson/react-jPlayer/status.svg)](https://david-dm.org/martindawson/react-jPlayer)
[![devDependencies Status](https://david-dm.org/martindawson/react-jPlayer/dev-status.svg)](https://david-dm.org/martindawson/react-jPlayer?type=dev)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

# react-jPlayer
A Html5 audio/video player that has been inspired by the [jQuery](http://jquery.com/) plugin [jPlayer](http://jplayer.org/) but without the jQuery dependency and much, much better.

react-jPlayer depends on [Redux](https://github.com/reactjs/redux). Redux is a tiny 2KB and is well worth it to keep the react-jPlayer components componentized.

### Installation
```npm install --save react-jPlayer```

### Examples
Run the jPlayer examples:

```
git clone https://github.com/MartinDawson/react-jPlayer.git

cd react-jPlayer

npm install

cd ./examples

npm run dev

open http://localhost:8080/
```

### Features
* Cross compatible with many legacy different Html5 browsers
* Fully customizable, modular and componentized
* All [Html5 audio/video file types](https://developer.mozilla.org/en-US/docs/Web/HTML/Supported_media_formats) are supported
* Comes with a fully reponsive css skin for your players
* No jQuery dependency that is in the standard [jPlayer](http://jplayer.org/)
* Fast and performant

### To Note
* No flash player support because flash is dead. I also haven't been able to find a browser that React supports that also didn't support Html5 video/audio players either which makes flash useless.
* Dependency on [Redux](https://github.com/reactjs/redux)

## Supported browsers
* Chrome v15+
* FireFox v15+
* Edge 13+
* Internet Explorer 9+
* Opera v16+
* Yandex
* Windows Safari 5.1
* IOS Safari 5.1+
* Chrome for Android v36+
* Android browser 4+
* IEMobile 11¹

¹partially tested without audio/video because browserstack emulators don't support it.

## Documentation
#### `getInitialStates(jPlayers)`
A required function that deep merges the static options that you specified on your jPlayer with react-jPlayer's defaults. The result of this must be passed to your stores initial state.

##### Arguments
1. `jPlayer(s)` (Array or Function): Accepts either an array of jPlayers or a single jPlayer. 

##### Returns
(Object): The initial state for the jPlayer(s) that needs to be passed to the Redux store.

#### `reducer`
A required object. The jPlayer reducer that will be called whenever a jPlayer function is called or dispatched. Must be passed to your store.

#### `connect(jPlayer)`
Required to connect your jPlayer to the jPlayer store by wrapping Redux's original connect.

##### Arguments
1. `jPlayer`: (Function)

##### Returns
(function): A function that wraps your jPlayer. This means that you can use Redux original connect to wrap this connect with as well if you wanted to pass aditional Redux data from the store to your jPlayer.

##### Static Properties
1. `id`: The id of the jPlayer, this is whatever name you called your jPlayer function. This is passed down as a context so that react-jPlayer can internally know which jPlayer is the current one.
2. `jPlayer`: The original function that you passed in. E.g. if you wanted to read the original jPlayer's options that you specified.

##### Renders
The connected jPlayer. Any additional props that you passed in are passed through to your jPlayer so you can use them as usual.

### Components
#### `<JPlayer />`
A required component that needs to be the root of any other jPlayer components. Handles the states that are applied to the jPlayer DOM element.

#### `<GUI />`
Should wrap all of the components that the user interacts with. Handles the fading in and out when in full screen mode.

#### `<SeekBar />`
Should wrap the `<PlayBar />` and `<BufferBar />`. Handles the user being able to seek to a new time when the user clicks, drags or touches on the progress bar. 

#### `<PlayBar />`
Shows how much of the media has been played so far.

#### `<BufferBar />`
Shows how much of the media has been downloaded so far. This also takes in to consideration the user seeking to multiple points on the media and skipping parts of the media.

#### `<Poster />`
The poster to be displayed for the media. Uses `media.poster` as the src for the image.

#### `<Video />`
If the first media source that you have supplied to `media.sources` is an [video format](https://en.wikipedia.org/wiki/Video_file_format) and it is a valid url that can be played then react-jPlayer will use this component and set the `src` to what you supplied.

#### `<Audio />`
If the first media source that you have supplied to `media.sources` is an [audio format](https://en.wikipedia.org/wiki/Audio_file_format) and it is a valid url that can be played then react-jPlayer will use this component and set the `src` to what you supplied.

#### `<Title />`
Renders the media title as `media.artist` - `media.title`.

#### `<FullScreen />`
Handles clicks on this component toggling the full screen of the jPlayer.

#### `<Mute />`
Handles clicks on this component toggling the mute of the jPlayer.

#### `<Play />`
Handles clicks on this component setting the jPlayer to be paused or playing.

#### `<Repeat />`
Handles clicks on this component toggling the looping of the jPlayer.

####  `<PlaybackRateBar />`
Handles clicks, dragging or touches on this component setting the playback rate of the media.

#### `<PlaybackRateBarValue />`
This is used by the `<PlaybackRateBar />` by default so the majority of applications won't need to use this. Represents the playback rate as the width or height of the component depending on the property `verticalPlaybackRate`.

#### `<VolumeBar />`
Handles clicks, dragging or touches on this component setting the volume of the media.

#### `<VolumeBarValue />`
This is used by the `<VolumeBar />` by default so the majority of applications won't need to use this. Represents the volume as the width or height of the component depending on the property `verticalVolume`.

#### `<Download />`
Handles clicks on this component downloading the media if the `media.free` option is true. Warning: This will not make the media secure, i.e. users can still download the song from the network tab. You will need to secure the media this from the server instead.
If the browser doesn't support the `download` attribute then clicks on this component will open a new tab or window with the source media instead.

#### `<Duration />`
Renders the `durationText` of the jPlayer. Renders nothing if the duration hasn't been set yet (i.e IOS until the user manually plays the media).

#### `<CurrentTime />`
Renders the `currentTimeText` of the jPlayer.

#### `<BrowserUnsupported />`
Renders html that tells the user to update their browser if jPlayer doesn't support the specified media file.

### Misc
#### classes
classes that react-jPlayer uses internally for each component are exported for you to use for conveniance.

## Thanks
[1]: https://www.browserstack.com/
[2]: https://cloud.githubusercontent.com/assets/15030491/22504241/4240e478-e86d-11e6-8147-d2771655346a.png
[![BrowserStack][2]][1]

BrowserStack for giving me access to their testing software for free. Contact them if you have a free open-source project for a free account.
